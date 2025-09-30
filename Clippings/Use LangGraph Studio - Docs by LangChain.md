---
title: "Use LangGraph Studio - Docs by LangChain"
source: "https://docs.langchain.com/langgraph-platform/quick-start-studio"
author:
  - "[[Docs by LangChain]]"
published:
created: 2025-09-30
description:
tags:
  - "clippings"
---
[LangGraph Studio](https://docs.langchain.com/langgraph-platform/langgraph-studio) supports connecting to two types of graphs:

- Graphs deployed on [LangGraph Platform](https://docs.langchain.com/langgraph-platform/#langgraph-platform).
- Graphs running locally via the [LangGraph Server](https://docs.langchain.com/langgraph-platform/#local-development-server).

## LangGraph Platform

LangGraph Studio is accessed from the LangSmith UI, within the **LangGraph Platform Deployments** tab. For applications that are [deployed](https://docs.langchain.com/langgraph-platform/deployment-quickstart) on LangGraph Platform, you can access Studio as part of that deployment. To do so, navigate to the deployment in LangGraph Platform within the LangSmith UI and click the **LangGraph Studio** button. This will load the Studio UI connected to your live deployment, allowing you to create, read, and update the [threads](https://docs.langchain.com/oss/python/langgraph/persistence#threads), [assistants](https://docs.langchain.com/langgraph-platform/assistants), and [memory](https://docs.langchain.com/oss/python/concepts/memory) in that deployment.

## Local development server

To test your application locally using LangGraph Studio, follow the [local application quickstart](https://docs.langchain.com/langgraph-platform/local-server) first.

Next, install the [LangGraph CLI](https://docs.langchain.com/langgraph-platform/langgraph-cli):

This will start the LangGraph Server locally, running in-memory. The server will run in watch mode, listening for and automatically restarting on code changes. Read this [reference](https://docs.langchain.com/langgraph-platform/cli#dev) to learn about all the options for starting the API server. You will see the following logs:

```
> Ready!
>
> - API: [http://localhost:2024](http://localhost:2024/)
>
> - Docs: http://localhost:2024/docs
>
> - LangGraph Studio Web UI: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
```

Once running, you will automatically be directed to LangGraph Studio. For an already running server, access Studio by either:

1. Directly navigate to the following URL: `https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024`.
2. Within LangSmith, navigate to the **LangGraph Platform Deployments** tab, click the **LangGraph Studio** button, enter `http://127.0.0.1:2024` and click **Connect**.

If running your server at a different host or port, simply update the `baseUrl` to match.

### (Optional) Attach a debugger

For step-by-step debugging with breakpoints and variable inspection:

Then attach your preferred debugger:

Add this configuration to `launch.json`:

```
{
    "name": "Attach to LangGraph",
    "type": "debugpy",
    "request": "attach",
    "connect": {
      "host": "0.0.0.0",
      "port": 5678
    }
}
```

## Troubleshooting

For issues getting started, refer to the [troubleshooting guide](https://docs.langchain.com/langgraph-platform/troubleshooting-studio).

## Next steps

See the following guides for more information on how to use Studio:

- [Run application](https://docs.langchain.com/langgraph-platform/invoke-studio)
- [Manage assistants](https://docs.langchain.com/langgraph-platform/manage-assistants-studio)
- [Manage threads](https://docs.langchain.com/langgraph-platform/threads-studio)
- [Iterate on prompts](https://docs.langchain.com/langgraph-platform/iterate-graph-studio)
- [Debug LangSmith traces](https://docs.langchain.com/langgraph-platform/clone-traces-studio)
- [Add node to dataset](https://docs.langchain.com/langgraph-platform/datasets-studio)