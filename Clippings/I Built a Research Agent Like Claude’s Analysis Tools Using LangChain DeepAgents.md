---
title: "I Built a Research Agent Like Claude’s Analysis Tools Using LangChain DeepAgents"
source: "https://medium.com/@sagarnreddy/i-built-a-research-agent-like-claudes-analysis-tools-using-langchain-deepagents-795f51a3a63f"
author:
  - "[[Sagar]]"
published: 2025-08-14
created: 2025-10-31
description: "I Built a Research Agent Like Claude’s Analysis Tools Using LangChain DeepAgents Have you ever wondered how Claude’s advanced analysis capabilities work behind the scenes? After experimenting …"
tags:
  - "clippings"
---
[Sitemap](https://medium.com/sitemap/sitemap.xml)

![](https://miro.medium.com/v2/resize:fit:640/format:webp/0*0sd2FMnCZa3Uzy7T.png)

Have you ever wondered how Claude’s advanced analysis capabilities work behind the scenes? After experimenting with LangChain’s DeepAgent framework, I built my own intelligent stock research agent that rivals professional-grade analysis tools. Here’s how I did it — and how you can too.

## The Problem with Basic AI Agents

Most AI chatbots excel at conversations but struggle with complex, multi-step research tasks. They lack the ability to:

- Plan systematically across multiple analysis phases
- Use specialized tools for different types of data
- Coordinate expert perspectives (fundamental vs technical analysis)
- Synthesize findings into actionable recommendations

This is where DeepAgents shine. Unlike simple tool-calling agents, they incorporate planning, specialized sub-agents, file management, and comprehensive reasoning — just like Claude’s research capabilities.

## What I Built: A Complete Stock Research System

My agent performs comprehensive stock analysis by combining:

✅ Real-time financial data (prices, ratios, market cap)  
✅ Technical indicators (RSI, moving averages, trend signals)  
✅ Financial statement analysis (revenue, debt, profitability)  
✅ Multi-perspective analysis via specialized sub-agents  
✅ Professional reporting with clear recommendations

## The Architecture: Three-Layer Intelligence

## Layer 1: Custom Financial Tools

First, I built specialized tools that gather and process financial data:

```c
@tool
def get_stock_price(symbol: str) -> str:
    """Get current stock price and basic information."""
    try:
        stock = yf.Ticker(symbol)
        info = stock.info
        hist = stock.history(period="1d")
        
        current_price = hist['Close'].iloc[-1]
        result = {
            "symbol": symbol,
            "current_price": round(current_price, 2),
            "company_name": info.get('longName', symbol),
            "market_cap": info.get('marketCap', 0),
            "pe_ratio": info.get('trailingPE', 'N/A'),
            "52_week_high": info.get('fiftyTwoWeekHigh', 0),
            "52_week_low": info.get('fiftyTwoWeekLow', 0)
        }
        return json.dumps(result, indent=2)
    except Exception as e:
        return json.dumps({"error": str(e)})
```

## Layer 2: Specialized Sub-Agents

The magic happens with specialized sub-agents, each an expert in their domain:

```c
fundamental_analyst = {
    "name": "fundamental-analyst",
    "description": "Performs deep fundamental analysis of companies",
    "prompt": """You are an expert fundamental analyst with 15+ years of experience. 
    Focus on:
    - Financial statement analysis
    - Ratio analysis (P/E, P/B, ROE, ROA, Debt-to-Equity)
    - Growth metrics and trends
    - Industry comparisons
    - Intrinsic value calculations
    Always provide specific numbers and cite your sources."""
}

technical_analyst = {
    "name": "technical-analyst", 
    "description": "Analyzes price patterns, technical indicators, and trading signals",
    "prompt": """You are a professional technical analyst specializing in chart analysis.
    Focus on:
    - Price action and trend analysis
    - Technical indicators (RSI, MACD, Moving Averages)
    - Support and resistance levels
    - Entry/exit recommendations
    Provide specific price levels and timeframes."""
}

risk_analyst = {
    "name": "risk-analyst",
    "description": "Evaluates investment risks and provides risk assessment",
    "prompt": """You are a risk management specialist.
    Focus on:
    - Market risk analysis
    - Company-specific risks
    - Sector and industry risks
    - Regulatory and compliance risks
    Always quantify risks and suggest mitigation strategies."""
}
```

## Layer 3: Master Orchestrator

The main agent coordinates everything with systematic planning:

```c
research_instructions = """You are an elite stock research analyst with access to multiple specialized tools and sub-agents. 

Your research process should be systematic and comprehensive:

1. **Initial Data Gathering**: Collect basic stock information and price data
2. **Fundamental Analysis**: Deep dive into financial statements and ratios
3. **Technical Analysis**: Analyze price patterns and technical indicators
4. **Risk Assessment**: Identify and evaluate potential risks
5. **Synthesis**: Combine all findings into a coherent investment thesis
6. **Recommendation**: Provide clear buy/sell/hold recommendation with price targets

Always use specific data and numbers to support your analysis."""

# Create the DeepAgent
stock_research_agent = create_deep_agent(
    tools=[get_stock_price, get_financial_statements, get_technical_indicators],
    instructions=research_instructions,
    subagents=[fundamental_analyst, technical_analyst, risk_analyst],
    model=ollama_model
)
```

## The User Experience: Simple Query, Professional Analysis

I wrapped everything in a clean Gradio interface that makes complex analysis accessible:

```c
def run_stock_research(query: str):
    """Run the stock research agent and return comprehensive analysis."""
    try:
        result = stock_research_agent.invoke({
            "messages": [{"role": "user", "content": query}]
        })
        
        messages = result.get("messages", [])
        if messages:
            if isinstance(messages[-1], dict):
                return messages[-1].get("content", "")
            elif hasattr(messages[-1], "content"):
                return messages[-1].content
        
        return "Error: No response received."
    except Exception as e:
        return f"Error: {str(e)}"

# Simple Gradio UI
with gr.Blocks() as demo:
    gr.Markdown("## 📊 Stock Research Agent")
    query_input = gr.Textbox(label="Research Query", lines=6)
    run_button = gr.Button("Run Analysis")
    output_box = gr.Textbox(label="Research Report", lines=20)
    
    run_button.click(fn=run_stock_research, inputs=query_input, outputs=output_box)

demo.launch(server_name="0.0.0.0", server_port=7860)
```

## How It Works: The Magic Behind the Scenes

When you ask: *“Analyze Apple Inc. (AAPL) for a 6-month investment”*

1. Planning Phase: Master agent creates structured research workflow
2. Data Collection: Tools gather real-time prices, financials, technical indicators
3. Expert Analysis: Each sub-agent provides specialized insights
4. Synthesis: Master agent combines all perspectives
5. Report Generation: Professional recommendation with specific price targets
![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*0_ik0dzrkBoCtNVPWRHa1Q.png)

## Why This Approach Works

Traditional Agent: Single AI → Simple tool calls → Basic response  
DeepAgent: Planning → Specialized experts → Data synthesis → Professional analysis

The difference is like consulting one generalist versus assembling a team of specialists.

## Getting Started: 5-Minute Setup

```c
# Install dependencies
pip install deepagents langchain-ollama yfinance gradio langchain-core

# Set up local LLM with Ollama
ollama pull gpt-oss

# Run the agent
python stock_research_agent.py
```

Navigate to `http://localhost:7860` and start analyzing stocks immediately.

## The Bigger Picture

Building this agent taught me that true AI capability isn’t about having the smartest model — it’s about systematic orchestration of specialized tools and expertise.

DeepAgents represent a fundamental shift from “smart chatbots” to “intelligent systems” that can handle complex, real-world workflows.

*Want the complete implementation? The full code is available in my G* [*itHub*](https://github.com/sagar-n/deepagents)*. Follow me for more deep dives into practical AI applications.*

💻 Software Developer | 🧠 Exploring AI & Agents | ✍️ Sharing real-world tech stories & hands-on tutorials

## Responses (4)

Write a response[What are your thoughts?](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Fmedium.com%2F%40sagarnreddy%2Fi-built-a-research-agent-like-claudes-analysis-tools-using-langchain-deepagents-795f51a3a63f&source=---post_responses--795f51a3a63f---------------------respond_sidebar------------------)

```c
This is such a great article! By the way, how is the response speed of the deepagent you built?
```

7

## More from Sagar

## Recommended from Medium

[

See more recommendations

](https://medium.com/?source=post_page---read_next_recirc--795f51a3a63f---------------------------------------)