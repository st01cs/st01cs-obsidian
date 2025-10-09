---
title: "LangGraph Human-in-the-loop (HITL) Deployment with FastAPI"
source: "https://shaveen12.medium.com/langgraph-human-in-the-loop-hitl-deployment-with-fastapi-be4a9efcd8c0"
author:
  - "[[Shaveen Silva]]"
published: 2025-03-26
created: 2025-10-09
description: "LangGraph Human-in-the-loop (HITL) Deployment with FastAPI I recently needed to convert a Human-in-the-Loop (HITL) AI agent, built using LangGraph, to be accessible via APIs from a backend. During …"
tags:
  - "clippings"
---
[Sitemap](https://shaveen12.medium.com/sitemap/sitemap.xml)

![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*1DCfzYG2fqhdIad7rRHH1g.jpeg)

I recently needed to convert a Human-in-the-Loop (HITL) AI agent, built using LangGraph, to be accessible via APIs from a backend. During initial testing, the agent relied on the Python `input()` function to gather human input—something that isn’t feasible in a backend environment.

This tutorial won’t cover how to build AI agents in LangGraph. Instead, it focuses on how to configure HITL agents so they can be deployed and served through a backend.

As an example, I’ll be using this [Kaggle notebook](https://www.kaggle.com/code/shaveensilva/day-3-building-an-agent-with-langgraph) featuring a barista chatbot designed to take customer orders. In this implementation, human input is captured using the Python `input()` function and then passed back into the graph to continue the conversation flow.

To adapt this for a backend deployment, we need to solve a few key challenges. Specifically, the graph must pause when human input is required, notify the frontend that input is needed, and then resume once the input has been received. This introduces three main problems that need to be addressed:

1. **Persisting the graph state** — So the flow can be resumed later without losing context.
2. **Pausing the graph when human input is required** — Preventing it from running ahead before user interaction.
3. **Resuming the graph with the provided human input** — Ensuring it picks up exactly where it left off

## State

LangGraph offers built-in **checkpointers**, which automatically save the state of the graph at each node. To enable this functionality, you need to provide a checkpointer when compiling the graph. Additionally, a `thread_id` must be passed during graph invocation to uniquely identify and persist the state across multiple runs or user sessions.

```c
from langgraph.checkpoint.memory import MemorySaver

workflow = StateGraph(State)
workflow.add_node(node_a)
workflow.add_node(node_b)
workflow.add_edge(START, "node_a")
workflow.add_edge("node_a", "node_b")
workflow.add_edge("node_b", END)

checkpointer = MemorySaver()
graph = workflow.compile(checkpointer=checkpointer)

thread_config = {"configurable": {"thread_id": "1"}}
graph.invoke({"foo": ""}, thread_config)
```

The example above uses `MemorySaver()`, which stores the graph state in memory. While this works for testing or simple use cases, it's not suitable for production environments, where state persistence must be more robust. To address this, LangGraph also provides other checkpointing options, including support for SQL and Redis databases. Check out the [docs](https://langchain-ai.github.io/langgraph/concepts/persistence/) for information.

## Pausing

Next, we need to **pause the graph** to wait for human input. LangGraph provides an `interrupt()` method to handle this, allowing the graph to temporarily stop execution until the required input is received.

```c
def human_node(state: State):
    value = interrupt(
        # Any JSON serializable value to surface to the human.
        # For example, a question or a piece of text or a set of keys in the state
       {
          "text_to_revise": state["some_text"]
       }
    )
    # Update the state with the human's input or route the graph based on the input.
    return {
        "some_text": value
    }
```

Wherever you would typically use the `input()` function, replace it with a call to `interrupt()`. This allows the graph to pause and wait for human input in a backend-compatible way. You can pass relevant information to `interrupt()` that you want the user to see before responding.

For example, in the case above, the user will be shown the `some_text` attribute from the graph state, providing context before they enter their input.

```c
graph.get_state(thread_config).tasks[0].interrupts[0].value
```

The line of code given above can be used to retrieve the information passed to the interrupt.

## Resuming

To resume the graph with the human input, you need to pass a `Command` object containing the user's response to the `invoke()` method. This should be done along with the appropriate `thread_id` in the thread configuration, like so:

```c
thread_config = {"configurable": {"thread_id": "1"}}
  state = graph_with_menu.invoke(
        Command(resume = "Human Input"), 
        config=thread_config)
```

This will restart the graph from the node where the `interrupt()` was triggered, with the human input passed to resume. However, it's important to note that the graph resumes execution from the **beginning of that node**, not from the exact line where the `interrupt()` occurred.

To avoid duplicating logic or altering the state unintentionally, it’s best practice to place the `interrupt()` call **at the start of the node**.

Great! At this point, we’ve successfully addressed all three key challenges.

Below, I’ve taken the original graph from the Kaggle notebook, replaced all `input()` calls with `interrupt()` statements, and integrated it into a FastAPI backend. The following endpoints are now available for interacting with the graph:

```c
from fastapi import FastAPI
from chatagent import graph_with_menu
from langgraph.types import Command
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
@app.get("/")
def read_root():
    return {"message": "Welcome to your FastAPI backend!"}

@app.get("/chat_initiate")
def read_item(thread_id: str, response: str = None):
    thread_config = {"configurable": {"thread_id": thread_id}}    
    state = graph_with_menu.invoke(
        {"messages": [],
         "order": [],
         "finished": False}, 
        config=thread_config)

    return {
        "AIMessage": state["messages"][-1].content,
        "state": state,
        "thread_id": thread_id
    }

@app.get("/chat-continue")
def continue_chat(thread_id: str, response: str):
    thread_config = {"configurable": {"thread_id": thread_id}}
    state = graph_with_menu.invoke(
        Command(resume = response), 
        config=thread_config)

    return {
        "AIMessage": state["messages"][-1].content,
        "state": state,
        "thread_id": thread_id
    }
```

I’ve set up two endpoints:

1. One to **start the chat**
2. Another to **continue the conversation** with human input

While information can be passed to the `interrupt()` function, in this case, it hasn’t been used directly. Instead, the latest AI message—available from the graph state—is what the user needs in order to respond. This message can be retrieved and shown to the user from the state itself.

The complete fastAPI backend for this project can be found [here](https://github.com/Shaveen12/HumanInTheLoop).

Even though the example used above is a very simple one, the same structure and tools discussed can be used to build complex Human-in-the-Loop (HITL) graphs with multiple decision points and branching logic suitable for real-world applications.

Feel free to reach out if you have any questions or if you’re working on something similar — would love to hear about it!

Computer Science and Engineering undergraduate with a passion for all things technology. [shaveensilva.com](http://shaveensilva.com/)

## Responses (4)

Write a response[What are your thoughts?](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Fshaveen12.medium.com%2Flanggraph-human-in-the-loop-hitl-deployment-with-fastapi-be4a9efcd8c0&source=---post_responses--be4a9efcd8c0---------------------respond_sidebar------------------)

```c
This article is incredibly insightful and helpful
```

4

```c
how does the frontend or any app that consumes the /chat_initiate know that now they have to call /chat-continue ?
```

4

```c
this is insightful. but how did you handle it in ui side will be off interest also
```

## More from Shaveen Silva

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--be4a9efcd8c0---------------------------------------)