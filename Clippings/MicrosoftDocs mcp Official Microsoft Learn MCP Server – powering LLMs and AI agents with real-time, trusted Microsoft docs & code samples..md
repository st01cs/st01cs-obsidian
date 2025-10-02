---
title: "MicrosoftDocs/mcp: Official Microsoft Learn MCP Server – powering LLMs and AI agents with real-time, trusted Microsoft docs & code samples."
source: "https://github.com/MicrosoftDocs/mcp"
author:
  - "[[partychen]]"
published:
created: 2025-10-01
description: "Official Microsoft Learn MCP Server – powering LLMs and AI agents with real-time, trusted Microsoft docs & code samples. - MicrosoftDocs/mcp"
tags:
  - "clippings"
---
**[mcp](https://github.com/MicrosoftDocs/mcp)** Public

Official Microsoft Learn MCP Server – powering LLMs and AI agents with real-time, trusted Microsoft docs & code samples.

[learn.microsoft.com](https://learn.microsoft.com/ "https://learn.microsoft.com")

CC-BY-4.0, MIT licenses found

[Code of conduct](https://github.com/MicrosoftDocs/.github/blob/main/CODE_OF_CONDUCT.md)

[Security policy](https://github.com/MicrosoftDocs/mcp/blob/main/SECURITY.md)

[950 stars](https://github.com/MicrosoftDocs/mcp/stargazers) [101 forks](https://github.com/MicrosoftDocs/mcp/forks) [12 watching](https://github.com/MicrosoftDocs/mcp/watchers) [Branches](https://github.com/MicrosoftDocs/mcp/branches) [Tags](https://github.com/MicrosoftDocs/mcp/tags) [Activity](https://github.com/MicrosoftDocs/mcp/activity) [Custom properties](https://github.com/MicrosoftDocs/mcp/custom-properties)

Public repository

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/MicrosoftDocs/mcp?resume=1)

The Microsoft Learn MCP Server is a remote MCP Server that enables clients like GitHub Copilot and other AI agents to bring trusted and up-to-date information directly from Microsoft's official documentation. It supports streamable http transport, which is lightweight for clients to use.

> Please note that this project is in Public Preview and implementation may significantly change prior to our General Availability.

1. [🎯 Overview](https://github.com/MicrosoftDocs/#-overview)
2. [🌐 The Microsoft Learn MCP Server Endpoint](https://github.com/MicrosoftDocs/#-the-microsoft-learn-mcp-server-endpoint)
3. [🛠️ Currently Supported Tools](https://github.com/MicrosoftDocs/#%EF%B8%8F-currently-supported-tools)
4. [🔌 Installation & Getting Started](https://github.com/MicrosoftDocs/#-installation--getting-started)
5. [❓ Troubleshooting](https://github.com/MicrosoftDocs/#-troubleshooting)
6. [🔮 Future Enhancements](https://github.com/MicrosoftDocs/#-future-enhancements)
7. [📚 Additional Resources](https://github.com/MicrosoftDocs/#-additional-resources)

## 🎯 Overview

Your AI assistant should automatically use these tools for Microsoft-related topics. With both search and fetch capabilities, you can get quick answers or comprehensive deep dives. To ensure that it always consults the official documentation, you can add phrases like `search Microsoft docs`, `deep dive`, `fetch full doc`.

> "Give me the Azure CLI commands to create an Azure Container App with a managed identity. **search Microsoft docs** "

> "Is gpt-4.1-mini available in EU regions? **fetch full doc** "

> "Are you sure this is the right way to implement `IHttpClientFactory` in a.NET 8 minimal API? **search Microsoft docs and fetch full doc** "

> "Show me the complete guide for implementing authentication in ASP.NET Core. **fetch full doc** "

> "show me detailed, runnable python code sample to do harms eval using azure ai foundry evaluation sdk"

> "I need to understand Azure Functions end-to-end. **search Microsoft docs and deep dive** "

> "Get me the full step-by-step tutorial for deploying a.NET application to Azure App Service. **search Microsoft docs and deep dive** "

- **High-Quality Content Retrieval**: Search and retrieve relevant content from Microsoft's official documentation in markdown format.
- **Code Sample Discovery**: Find official Microsoft/Azure code snippets and examples with language-specific filtering.
- **Semantic Understanding**: Uses advanced vector search to find the most contextually relevant documentation for any query.
- **Real-time Updates**: Access the latest Microsoft documentation as it's published.

The Microsoft Learn MCP Server is accessible to any IDE, agent, or tool that supports the Model Context Protocol (MCP). Any compatible client can connect to the following **remote MCP endpoint**:

```
https://learn.microsoft.com/api/mcp
```

> **Note:** This URL is intended for use **within a compliant MCP client** via Streamable HTTP, such as the recommended clients listed in our [Getting Started](https://github.com/MicrosoftDocs/#-installation--getting-started) section. It does not support direct access from a web browser and may return a `405 Method Not Allowed` error if accessed manually. For developers who need to build their own solution, please follow the mandatory guidelines in the [Building a Custom Client](https://github.com/MicrosoftDocs/#%EF%B8%8F-building-a-custom-client) section to ensure your implementation is resilient and supported.

**Example JSON configuration:**

```
{
  "microsoft.docs.mcp": {
    "type": "http",
    "url": "https://learn.microsoft.com/api/mcp"
  }
}
```

| Tool Name | Description | Input Parameters |
| --- | --- | --- |
| `microsoft_docs_search` | Performs semantic search against Microsoft official technical documentation | `query` (string): The search query for retrieval |
| `microsoft_docs_fetch` | Fetch and convert a Microsoft documentation page into markdown format | `url` (string): URL of the documentation page to read |
| `microsoft_code_sample_search` | Search for official Microsoft/Azure code snippets and examples | `query` (string): Search query for Microsoft/Azure code snippets   `language` (string, optional): Programming language filter. |

The Microsoft Learn MCP Server supports quick installation across multiple development environments. Choose your preferred client below for streamlined setup:

| Client | One-click Installation | MCP Guide |
| --- | --- | --- |
| **VS Code** |  | [VS Code MCP Official Guide](https://code.visualstudio.com/docs/copilot/chat/mcp-servers) |
| **Claude Desktop** | View Instructions 1. Open Claude Desktop   2\. Go to **Settings → Integrations**   3\. Click **Add Integration**   4\. Enter URL: `https://learn.microsoft.com/api/mcp`   5\. Click **Connect** | [Claude Desktop Remote MCP Guide](https://support.anthropic.com/en/articles/11503834-building-custom-integrations-via-remote-mcp-servers) |
| **Claude Code** | View Instructions 1. Open a CLI   2\. Type `claude mcp add --transport http microsoft_docs_mcp https://learn.microsoft.com/api/mcp` and press enter   3\. (optional) Type `--scope user` directly after `claude mcp add` to make this MCP server available in Claude Code for all of your projects | [Claude Code Remote MCP Guide](https://docs.anthropic.com/en/docs/claude-code/mcp) |
| **Visual Studio** | Manual configuration required   Use `"type": "http"` | [Visual Studio MCP Official Guide](https://learn.microsoft.com/en-us/visualstudio/ide/mcp-servers?view=vs-2022) |
| **Cursor IDE** |  | [Cursor MCP Official Guide](https://docs.cursor.com/context/model-context-protocol) |
| **Roo Code** | Manual configuration required   Use `"type": "streamable-http"` | [Roo Code MCP Official Guide](https://docs.roocode.com/features/mcp/using-mcp-in-roo) |
| **Cline** | Manual configuration required   Use `"type": "streamableHttp"` | [Cline MCP Official Guide](https://docs.cline.bot/mcp/connecting-to-a-remote-server) |
| **Gemini CLI** | Manual configuration required   View Config **Note**: Add an `mcpServer` object to `.gemini/settings.json` file   ``` {   "Microsoft Learn MCP Server": {      "httpUrl": "https://learn.microsoft.com/api/mcp"     } } ``` | [How to set up your MCP server](https://github.com/google-gemini/gemini-cli/blob/main/docs/tools/mcp-server.md#how-to-set-up-your-mcp-server) |
| **Qwen Code** | Manual configuration required   View Config **Note**: Add an `mcpServer` object to `.qwen/settings.json` file   ``` {   "Microsoft Learn MCP Server": {      "httpUrl": "https://learn.microsoft.com/api/mcp"     } } ``` | [Configure the MCP server in settings.json](https://qwenlm.github.io/qwen-code-docs/en/cli/tutorials/#configure-the-mcp-server-in-settingsjson) |
| **GitHub** | Manual configuration required   View Config **Note**: Navigate to Settings → Coding agent   ``` {   "mslearn": {     "command": "npx",     "args": [       "-y",       "mcp-remote",       "https://learn.microsoft.com/api/mcp"     ],  "tools":["*"]   } } ``` |  |
| **ChatGPT** | Manual configuration required   View Instructions 1. Open ChatGPT in the browser   2\. Go to **Settings → Connectors → Advanced settings → Turn Developer mode on**   3\. Go back to connectors and click **create**   4\. Give the connector a **name**, enter **URL** `https://learn.microsoft.com/api/mcp`, set **authentication** to `No authentication` and **trust** the application   5\. Click **create** | [ChatGPT Official Guide](https://platform.openai.com/docs/guides/developer-mode) |

For clients that don't support native remote MCP servers or if you prefer local configuration, you can use `mcp-remote` as a proxy:

| Client | Manual Configuration | MCP Guide |
| --- | --- | --- |
| **Claude Desktop (legacy config)** | View Config **Note**: Only use this if Settings → Integrations doesn't work   ``` {   "microsoft.docs.mcp": {     "command": "npx",     "args": [       "-y",       "mcp-remote",       "https://learn.microsoft.com/api/mcp"     ]   } } ``` Add to `claude_desktop_config.json` | [Claude Desktop MCP Guide](https://modelcontextprotocol.io/quickstart/user) |
| **Windsurf** | View Config ``` {   "microsoft.docs.mcp": {     "command": "npx",     "args": [       "-y",       "mcp-remote",       "https://learn.microsoft.com/api/mcp"     ]   } } ``` | [Windsurf MCP Guide](https://docs.windsurf.com/windsurf/cascade/mcp) |
| **Kiro** | View Config ``` {   "microsoft.docs.mcp": {     "command": "npx",     "args": [       "-y",       "mcp-remote",       "https://learn.microsoft.com/api/mcp"     ]   } } ``` | [Kiro MCP Guide](https://kiro.dev/docs/mcp/index) |

1. **For VS Code**: Open GitHub Copilot in VS Code and [switch to Agent mode](https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode)
2. **For Claude Desktop**: After adding the integration, you'll see the MCP tools icon in the chat interface
3. You should see the Learn MCP Server in the list of available tools
4. Try a prompt that tells the agent to use the MCP Server, such as "what are the az cli commands to create an Azure container app according to official Microsoft Learn documentation?"
5. The agent should be able to use the MCP Server tools to complete your query

> If your use case requires a direct, programmatic integration, it is essential to understand that MCP is a **dynamic protocol, not a static API**. The available tools and their schemas will evolve.
> 
> To build a resilient client that will not break as the service is updated, you should adhere to the following principles:
> 
> 1. **Discover Tools Dynamically:** Your client should fetch current tool definitions from the server at runtime (e.g., using `tools/list`). **Do not hard-code tool names or parameters.**
> 2. **Refresh on Failure:** Your client should handle errors during `tool/invoke` calls. If a tool call fails with an error indicating it is missing or its schema has changed (e.g., an HTTP 404 or 400 error), your client should assume its cache is stale and automatically trigger a refresh by calling `tools/list`.
> 3. **Handle Live Updates:** Your client should listen for server notifications (e.g., `listChanged`) and refresh its tool cache accordingly.

## ❓ Troubleshooting

Even tool-friendly models like Claude Sonnet 4 sometimes fail to call MCP tools by default; use system prompts to encourage usage.

Here's an example of a Cursor rule (a system prompt) that will cause the LLM to utilize `microsoft.docs.mcp` more frequently:

```
## Querying Microsoft Documentation

You have access to MCP tools called \`microsoft_docs_search\`, \`microsoft_docs_fetch\`, and \`microsoft_code_sample_search\` - these tools allow you to search through and fetch Microsoft's latest official documentation and code samples, and that information might be more detailed or newer than what's in your training data set.

When handling questions around how to work with native Microsoft technologies, such as C#, F#, ASP.NET Core, Microsoft.Extensions, NuGet, Entity Framework, the \`dotnet\` runtime - please use these tools for research purposes when dealing with specific / narrowly defined questions that may occur.
```

| Issue | Possible Solution |
| --- | --- |
| Connection errors | Verify your network connection and that the server URL is correctly entered |
| No results returned | Try rephrasing your query with more specific technical terms |
| Tool not appearing in VS Code | Restart VS Code or check that the MCP extension is properly installed |
| HTTP status 405 | Method not allowed happens when a browser tries to connect to the endpoint. Try using the MCP Server through VS Code GitHub Copilot or [MCP Inspector](https://modelcontextprotocol.io/docs/tools/inspector) instead. |

- [Ask questions, share ideas](https://github.com/MicrosoftDocs/mcp/discussions)
- [Create an issue](https://github.com/MicrosoftDocs/mcp/issues)

The Microsoft Learn MCP Server team is working on several enhancements:

- Improved telemetry to help inform server enhancements
- Expanding coverage to additional Microsoft documentation sources
- Improved query understanding for more precise results
- [Microsoft Learn MCP Server product documentation](https://learn.microsoft.com/training/support/mcp)
- [Microsoft MCP Servers](https://github.com/microsoft/mcp)
- [Microsoft Learn](https://learn.microsoft.com/)
- [Model Context Protocol Specification](https://modelcontextprotocol.io/)

## Releases

No releases published

## Packages

No packages published