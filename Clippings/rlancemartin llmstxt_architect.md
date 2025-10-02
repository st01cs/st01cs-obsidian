---
title: rlancemartin/llmstxt_architect
source: https://github.com/rlancemartin/llmstxt_architect
author:
  - "[[rlancemartin]]"
published:
created: 2025-10-01
description: Contribute to rlancemartin/llmstxt_architect development by creating an account on GitHub.
tags:
  - clippings
  - llm
---
**[llmstxt\_architect](https://github.com/rlancemartin/llmstxt_architect)** Public

[MIT license](https://github.com/rlancemartin/llmstxt_architect/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/rlancemartin/llmstxt_architect?resume=1)

## LLMsTxt Architect

`llms.txt` is an emerging standard for communicating website contents to LLMs. It is a markdown file listing URLs within a site and their *descriptions*, giving LLMs a guide [to help fetch and read pages](https://github.com/langchain-ai/mcpdoc) in order to accomplish tasks. LLMsTxt Architect is a Python package that builds [LLMs.txt](https://llmstxt.org/) automatically, using LLMs to automate the process. It can start with a list of URLs or an existing `llms.txt` file, and a user can specify the LLM provider, model, prompt used to generate description along with other options.

[![llms_txt_architecture](https://private-user-images.githubusercontent.com/122662504/428229107-485eecde-fdd2-475d-bc07-8d1fd7ed8295.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkzMTA4OTIsIm5iZiI6MTc1OTMxMDU5MiwicGF0aCI6Ii8xMjI2NjI1MDQvNDI4MjI5MTA3LTQ4NWVlY2RlLWZkZDItNDc1ZC1iYzA3LThkMWZkN2VkODI5NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTAwMVQwOTIzMTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03NjRmYjVjYTJkNTBmZjgwZDAxODI3ZDMyYTc1YzBmNGI4ZWY3ZTJiZTVjOGVjZjliMDdiNzFkMWVhMjQ0M2ZhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ZAhWKXqCRb4QBJiT1xml5QfHS_wI5u4AZ_S2HbvSAP0)](https://private-user-images.githubusercontent.com/122662504/428229107-485eecde-fdd2-475d-bc07-8d1fd7ed8295.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkzMTA4OTIsIm5iZiI6MTc1OTMxMDU5MiwicGF0aCI6Ii8xMjI2NjI1MDQvNDI4MjI5MTA3LTQ4NWVlY2RlLWZkZDItNDc1ZC1iYzA3LThkMWZkN2VkODI5NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTAwMVQwOTIzMTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT03NjRmYjVjYTJkNTBmZjgwZDAxODI3ZDMyYTc1YzBmNGI4ZWY3ZTJiZTVjOGVjZjliMDdiNzFkMWVhMjQ0M2ZhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.ZAhWKXqCRb4QBJiT1xml5QfHS_wI5u4AZ_S2HbvSAP0)

## Quickstart

You can run this tool with many [LLM providers](https://python.langchain.com/api_reference/langchain/chat_models/langchain.chat_models.base.init_chat_model.html). For example, Anthropic (be sure `ANTHROPIC_API_KEY` is set):

```
$ curl -LsSf https://astral.sh/uv/install.sh | sh
$ uvx --from llmstxt-architect llmstxt-architect --urls https://langchain-ai.github.io/langgraph/concepts --max-depth 1 --llm-name claude-3-7-sonnet-latest --llm-provider anthropic --project-dir tmp
```

Local model via Ollama (be sure [Ollama is installed](https://ollama.com/download) and the model is pulled):

```
$ ollama pull llama3.2:latest
$ uvx --from llmstxt-architect llmstxt-architect --urls https://langchain-ai.github.io/langgraph/concepts --max-depth 1 --llm-name llama3.2:latest --llm-provider ollama --project-dir tmp
```

Both will use [RecursiveURLLoader](https://python.langchain.com/docs/integrations/document_loaders/recursive_url/) with `max-depth` 1 to only load the provided page. While running you will see:

[![process_overview](https://private-user-images.githubusercontent.com/122662504/428235524-dd5448a6-8924-4f5d-8d2c-b49ce25507e5.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkzMTA4OTIsIm5iZiI6MTc1OTMxMDU5MiwicGF0aCI6Ii8xMjI2NjI1MDQvNDI4MjM1NTI0LWRkNTQ0OGE2LTg5MjQtNGY1ZC04ZDJjLWI0OWNlMjU1MDdlNS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTAwMVQwOTIzMTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yNzllMDZiMDc4MzlhNjYxZjIzMjU1YmRlMjMxZmY1M2Y0MTdiMTgwZWY3MzZhYjc0Yjg2ZjIwYmI5ODI0YTViJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.H8qZDFzcsiWc6_kZ9Guu1v-i_otYT8je6e-JLFj9r90)](https://private-user-images.githubusercontent.com/122662504/428235524-dd5448a6-8924-4f5d-8d2c-b49ce25507e5.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkzMTA4OTIsIm5iZiI6MTc1OTMxMDU5MiwicGF0aCI6Ii8xMjI2NjI1MDQvNDI4MjM1NTI0LWRkNTQ0OGE2LTg5MjQtNGY1ZC04ZDJjLWI0OWNlMjU1MDdlNS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUxMDAxJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MTAwMVQwOTIzMTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yNzllMDZiMDc4MzlhNjYxZjIzMjU1YmRlMjMxZmY1M2Y0MTdiMTgwZWY3MzZhYjc0Yjg2ZjIwYmI5ODI0YTViJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.H8qZDFzcsiWc6_kZ9Guu1v-i_otYT8je6e-JLFj9r90)

The resulting `llms.txt` file for this example input page:

```
[Concepts](https://langchain-ai.github.io/langgraph/concepts): LLM should read this page when seeking to understand LangGraph framework concepts, exploring agent patterns, or learning about LangGraph Platform deployment options. The page covers key concepts including LangGraph basics, agentic patterns, multi-agent systems, memory, persistence, streaming, and various LangGraph Platform deployment options (Self-Hosted, Cloud SaaS, BYOC).
```

You can see some of the `llms.txt` files generated with this tool:

- [https://langchain-ai.github.io/langgraph/llms.txt](https://langchain-ai.github.io/langgraph/llms.txt)
- [https://python.langchain.com/llms.txt](https://python.langchain.com/llms.txt)

### Installation

You can also install the package with `pip`, and use the CLI:

```
$ python3 -m venv .venv
$ source .venv/bin/activate  # On Windows: .venv\Scripts\activate
$ pip install llmstxt-architect
$ llmstxt-architect --urls https://langchain-ai.github.io/langgraph/concepts --max-depth 1 --llm-name claude-3-7-sonnet-latest --llm-provider anthropic --project-dir test
```

Use it in a notebook:

```
import asyncio
from llmstxt_architect.main import generate_llms_txt

await generate_llms_txt(
      urls=["https://langchain-ai.github.io/langgraph/concepts"],
      max_depth=1,
      llm_name="claude-3-7-sonnet-latest",
      llm_provider="anthropic",
      project_dir="test",
  )
```

Use it in a script:

```
import asyncio
from llmstxt_architect.main import generate_llms_txt

async def main():
      await generate_llms_txt(
          urls=["https://langchain-ai.github.io/langgraph/concepts"],
          max_depth=1,
          llm_name="claude-3-7-sonnet-latest",
          llm_provider="anthropic",
          project_dir="test_script",
      )

if __name__ == "__main__":
      asyncio.run(main())
```

## Configurations

The full list of configurations is available in the [CLI help](https://github.com/langchain-ai/llmstxt-architect/blob/main/llmstxt_architect/cli.py).

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `--urls` | List\[str\] | (Required if not using `--existing-llms-file`) | List of URLs to process |
| `--existing-llms-file` | str | (Required if not using `--urls`) | Path to an existing llms.txt file to extract URLs from and update |
| `--update-descriptions-only` | flag | False | Update only descriptions in existing llms.txt while preserving structure and URL order |
| `--max-depth` | int | 5 | Maximum recursion depth for URL crawling |
| `--llm-name` | str | "claude-3-sonnet-20240229" | LLM model name |
| `--llm-provider` | str | "anthropic" | LLM provider |
| `--project-dir` | str | "llms\_txt" | Main project directory to store all outputs |
| `--output-dir` | str | "summaries" | Directory within project-dir to save individual summaries |
| `--output-file` | str | "llms.txt" | Output file name for combined summaries |
| `--summary-prompt` | str | "You are creating a summary..." | Prompt to use for summarization |
| `--blacklist-file` | str | None | Path to a file containing blacklisted URLs to exclude (one per line) |
| `--extractor` | str | "default" | HTML content extractor to use (choices: "default" (Markdownify), "bs4" (BeautifulSoup)) |

### URLs

You can pass multiple URLs that you want to use as the basis for the `llms.txt` file. The [RecursiveURLLoader](https://python.langchain.com/docs/integrations/document_loaders/recursive_url/) will crawl *each* URL to the maximum depth as specified by `--max-depth` and use an LLM to summarize all of the resulting pages.

```
---urls https://langchain-ai.github.io/langgraph/concepts https://langchain-ai.github.io/langgraph/tutorials
--max-depth 1
```

Max depth can be used to increase the search depth:

```
- max_depth=1: Returns only the initial page itself
  - max_depth=2: Returns the initial page plus direct links from that page
  - max_depth=3: Returns the initial page, direct links, and links found on those pages
  etc.
```

If you have an existing `llms.txt` file (locally or remotely), you can extract the URLs from it and generates a completely new `llms.txt` with freshly generated descriptions. The original file's structure (headers, ordering, etc.) is *not preserved* by default.

```
# Use a local file
llmstxt-architect --existing-llms-file path/to/llms.txt

# Or use a remote file
llmstxt-architect --existing-llms-file https://example.com/llms.txt
```

As an example:

```
uvx --from llmstxt-architect llmstxt-architect --existing-llms-file https://js.langchain.com/llms.txt --update-descriptions-only --llm-nameclaude-3-7-sonnet-latest --llm-provider anthropic --project-dir langchain_docs_js_updated
```

If you have an `llms.txt` file that you want to preserve the structure of, you can use the `--update-descriptions-only` flag. This will preserve all structural elements (headers, subheaders, newlines) and the exact ordering of URLs while only updating the descriptions. It also maintains the exact ordering of URLs, preserves titles from the original file, and only updates the descriptions for each URL. This is particularly useful when the existing `llms.txt` file has a carefully curated structure that you want to maintain and you want to improve descriptions without changing the organization.

```
# Use a local file
llmstxt-architect --existing-llms-file path/to/llms.txt --update-descriptions-only

# Or use a remote file
llmstxt-architect --existing-llms-file https://example.com/llms.txt --update-descriptions-only
```

### Model

The package uses LLMs for generating descriptions for each URL in the `llms.txt` file. By default, it's configured for Anthropic's Claude models, but you can easily select from many different [LLM providers](https://python.langchain.com/api_reference/langchain/chat_models/langchain.chat_models.base.init_chat_model.html):

1. Install the corresponding package (e.g., `pip install langchain-openai`)
2. Set the appropriate API key (e.g., `export OPENAI_API_KEY=your_api_key_here`)
3. Specify the provider and model with the `--llm-provider` and `--llm-name` options, e.g., using the [LLM provider names as shown here](https://python.langchain.com/api_reference/langchain/chat_models/langchain.chat_models.base.init_chat_model.html)

```
--llm-provider openai --llm-name gpt-4o
```

1. [Install Ollama](https://ollama.com/download)
2. Pull your desired model (e.g., `ollama pull llama3.2:latest`)
3. Install the package: `pip install langchain-ollama`
4. Specify the provider and model with the `--llm-provider` and `--llm-name` options, e.g.,

```
--llm-provider ollama --llm-name llama3.2:latest
```

### Prompt

By default, it uses this prompt (see [llmstxt\_architect/cli.py](https://github.com/langchain-ai/llmstxt-architect/blob/main/llmstxt_architect/cli.py)):

```
"You are creating a summary for a webpage to be used in a llms.txt file "
"to help LLMs in the future know what is on this page. Produce a concise "
"summary of the key items on this page and when an LLM should access it."
```

You can override this prompt with the `--summary-prompt` option, e.g.,

```
--summary-prompt "You are creating a summary for a webpage to be used in a llms.txt file ..."
```

### Extractor

You can specify which built-in extractor to use with the `--extractor` CLI option:

```
# Use BeautifulSoup extractor
llmstxt-architect --urls https://example.com --extractor bs4

# Use default Markdownify extractor
llmstxt-architect --urls https://example.com --extractor default
```

For advanced use cases, you can override the default extractor in the Python API with your own custom extractor function, e.g.,

```
def my_extractor(html: str) -> str:
    """
    Extract content from HTML using xxx.
    
    Args:
        html (str): The HTML content to extract from
        
    Returns:
        content (str): Extracted text content
    """
    
    # TODO: Implement your custom extractor here
    
    return content

import asyncio
from llmstxt_architect.main import generate_llms_txt

await generate_llms_txt(
      urls=["https://langchain-ai.github.io/langgraph/concepts"],
      max_depth=1,
      llm_name="claude-3-7-sonnet-latest",
      llm_provider="anthropic",
      project_dir="test",
      extractor=my_extractor
  )
```

LLMsTxt Architect provides checkpoint functionality to handle interruptions during processing. It creates a project directory to store all outputs. While running, it saves each page's summary to the output directory and updates a checkpoint file (summarized\_urls.json) to track which pages have been processed. If the process is interrupted, you can simply run the same command again to resume from where it left off.

- **Progress tracker**: `<project_dir>/<output_dir>/summarized_urls.json`
- **Individual summaries**: `<project_dir>/<output_dir>/<url>.txt`
- **Combined output llms.txt file**: `<project_dir>/<output_file>`

All paths are configurable with:

```
--project-dir, --output-dir, --output-file
```

If processing is interrupted (timeout, network issues, etc.), simply run the same command again. The tool will:

1. Skip already processed pages using the checkpoint file
2. Resume processing from where it left off
3. Update the output file periodically (every 5 documents)
4. Generate a complete, sorted llms.txt file upon completion

This is particularly valuable when processing large websites or when using rate-limited API-based LLMs.

### URL Blacklisting

You can exclude specific URLs from your `llms.txt` file by providing a blacklist file:

```
# Create a blacklist file
cat > blacklist.txt << EOF
# Deprecated pages
https://example.com/old-version/
https://example.com/beta-feature

# Pages with known issues
https://example.com/broken-page
EOF
```

The name of the blacklist file is configurable with the `--blacklist-file` option.

The blacklist file should contain one URL per line. Empty lines and lines starting with `#` are ignored. The tool will:

1. Skip summarization of blacklisted URLs during crawling
2. Filter out blacklisted URLs from the final llms.txt file
3. Report how many blacklisted URLs were excluded

This is useful for excluding deprecated documentation, beta features, or pages with known issues.

## Testing

The package includes tests for various usage scenarios. To run the tests:

```
# Run all tests
python tests/test_all.py

# Run individual tests
python tests/test_uvx_claude.py    # Test UVX with Claude
python tests/test_uvx_ollama.py    # Test UVX with Ollama
python tests/test_script_claude.py # Test Python script import
python tests/test_api.py           # Test API usage
python tests/test_cli.py           # Test CLI argument parsing
```

The tests verify:

- UVX package execution with Claude
- UVX package execution with local Ollama models
- Python script import functionality
- API usage
- CLI argument parsing

All tests check for the creation of the expected output files (llms.txt, summaries directory, and summarized\_urls.json) and ensure the proper functionality of the CLI interface.

To clean up all test directories:

```
python tests/cleanup.py
```

The test system automatically cleans up after itself, removing test directories both before and after test runs to ensure a clean environment.

Once you have a `llms.txt` file, you can connect to it with a code tool. Aa an example, you can use an MCP server (as shown below and [here](https://github.com/langchain-ai/mcpdoc)) to connect to it.

```
"mcpServers": {
      "langgraph-docs-mcp": {
        "command": "uvx",
        "args": [
          "--from",
          "mcpdoc",
          "mcpdoc",
          "--urls",
          "LangGraph:<path-to-repo>/llmstxt_generator/<project-dir>/llms.txt",
          "--transport",
          "stdio",
          "--port",
          "8081",
          "--host",
          "localhost",
          "--allowed-domains",
          "*"
        ]
      },
    }
```

## License

MIT

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Python 100.0%](https://github.com/rlancemartin/llmstxt_architect/search?l=python)