---
title: "jpjacobpadilla/SearchAI: Search the web with advanced filters and LLM-friendly output formats!"
source: "https://github.com/jpjacobpadilla/SearchAI"
author:
  - "[[jpjacobpadilla]]"
published:
created: 2025-09-30
description:
tags:
  - "clippings"
---
**[SearchAI](https://github.com/jpjacobpadilla/SearchAI)** Public

Search the web with advanced filters and LLM-friendly output formats!

[pypi.org/project/search-ai-core](https://pypi.org/project/search-ai-core "https://pypi.org/project/search-ai-core")

[MIT license](https://github.com/jpjacobpadilla/SearchAI/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/jpjacobpadilla/SearchAI?resume=1) [![](https://github.com/jpjacobpadilla/SearchAI/raw/381e4e9c369ee1f73fa945e68e1a09ce39289196/searchai.png)](https://github.com/jpjacobpadilla/SearchAI/raw/381e4e9c369ee1f73fa945e68e1a09ce39289196/searchai.png) Search the web with advanced filters and LLM-friendly output formats!

```
from search_ai import search

results = search('What is the best LLM in 2025?')

for result in results:
    print(result.title)
```

Output:

```
LLM Leaderboard 2025 - Verified AI Rankings
Best LLM Models 2025: Top 10 AI Models Ranked & Compared
Top 7 LLMs Ranked in 2025: GPT-4o, Gemini, Claude & More
10 Best Large Language Models (LLMs) in 2025 - Beebom
Best Large Language Models (LLMs) of 2025 - TechRadar
Top 9 Large Language Models as of September 2025 | Shakudo
Top 15 LLMs in 2025: Best Large Language Models
Top LLMs in 2025: Comparing Claude, Gemini, and GPT-4 LLaMA
Best LLM Models 2025 - Complete Guide to Top 7 AI Language Models
15 Best LLM Models in 2025 | Top AI Language Models Ranked
```

### Install

```
$ pip install search-ai-core
```

### Using filters

```
from search_ai import search, Filters

search_filters = Filters(
    in_title="python",              # Only include results with "python" in the title
    tlds=[".edu", ".org"],          # Restrict results to .edu and .org domains
    https_only=True,                # Only include websites that support HTTPS
    exclude_sites='quora.com',      # Exclude results from quora.com
    exclude_filetypes='pdf'         # Exclude PDF documents from results
)

results = search(filters=search_filters)
for result in results:
    print(result.title)
```

Output:

```
Welcome to Python.org
Python Tutorial - W3Schools
Python (programming language) - Wikipedia
Learn Python - Free Interactive Python Tutorial
CS50's Introduction to Programming with Python | Harvard University
Real Python: Python Tutorials
Python for Everybody Specialization - Coursera
scikit-learn: machine learning in Python — scikit-learn 1.6.1 ...
Table Of Contents - Learn Python the Hard Way
Python Institute - PROGRAM YOUR FUTURE
```

### Regional targeting

```
from search_ai import search, Filters, Regions

search_filters = Filters(region=Regions.JAPAN)

results = search('Python', filters=search_filters)

for result in results:
    print(result.title)
```

Output:

```
Welcome to Python.org
python.jp: プログラミング言語 Python 総合情報サイト
【入門】Pythonとは｜活用事例やメリット、できること、学習方法 ...
ゼロからのPython入門講座 - python.jp
Pythonの開発環境を用意しよう！（Windows） - Progate
Python - Wikipedia
プログラミング言語のPythonとは？その特徴と活用方法 - 発注ナビ
Python試験・資格、データ分析試験・資格を運営する一般社団法人 ...
Pythonの導入方法｜ソフトの利用方法 - 東京経済大学
Pythonとは？開発に役立つ使い方、トレンド記事やtips - Qiita
```

Once extracted, you can retrieve the results in either Markdown or JSON format for further processing.

If the `extend` argument is set to `True`, the content of the result's websites will also be included in the output. To achieve this functionality, SearchAI uses [Playwright](https://github.com/microsoft/playwright) to load and extract content from websites. In addition to extracting the main content of a page, SearchAI also tries to find metadata on pages, such as an author name and twitter handle.

Getting results in markdown ([example](https://github.com/jpjacobpadilla/SearchAI/blob/c8c160a8d57e51ccb1c215ad27d652809a3d6da9/examples/markdown_example.py)):

```
SearchResults.markdown(
    extend=False,           # Set to True to fetch and include page content
    content_length=1000,    # Limit the length of extracted content
    ignore_links=False,     # Exclude hyperlinks in the content
    ignore_images=True,     # Exclude images from the content
    only_page_content=False # If True, omits metadata from the output
)
```

Getting results in json ([example](https://github.com/jpjacobpadilla/SearchAI/blob/c8c160a8d57e51ccb1c215ad27d652809a3d6da9/examples/json_example.py)):

```
SearchResults.json(
    extend=False,           # Set to True to fetch and include page content
    content_length=1000,    # Limit the length of extracted content
    ignore_links=False,     # Exclude hyperlinks in the content
    ignore_images=True,     # Exclude images from the content
)
```

### Using proxies

If you'd like to use proxies, you can create a proxy object using `Proxy` and pass it into either `search` or `async_search`.

```
from search_ai import Proxy, search

proxy = Proxy(
    protocol="[protocol]",
    host="[host]",
    port=9999,
    username="optional username",
    password="optional password"
)

search('query', proxy=proxy)
```

### Async support

SearchAI also supports Asyncio! Instead of using `search`, use `async_search`. The async version will return an `AsyncSearchResults` which will contain multiple instances of `AsyncSearchResult`.

```
from search_ai import async_search

results = await async_search(...)
await results.json(extend=True)
```

## All filters

You can narrow down searches by including filters like so:

Here is a complete list of all the filters in SearchAI:

| Filter | Description | Example (one) | Example (many) |
| --- | --- | --- | --- |
| `region` | Only show results from specific regions | `Regions.US_ENGLISH` |  |
| `time_span` | Timespan for the search | `Timespans.PAST_WEEK` |  |
| `sites` | Only show results from specific domains | `"example.com"` | `["example.com", "another.com"]` |
| `tlds` | Only show results from specific top-level domains (e.g. `.gov`, `.edu`) | `".edu"` | `[".edu", ".gov"]` |
| `filetype` | Only show documents of a specific file type (only one allowed) | `"pdf"` |  |
| `https_only` | Only show websites that support HTTPS | `True` |  |
| `exclude_sites` | Exclude results from specific domains | `"facebook.com"` | `["facebook.com", "twitter.com"]` |
| `exclude_tlds` | Exclude results from specific top-level domains | `".xyz"` | `[".xyz", ".ru"]` |
| `exclude_filetypes` | Exclude documents with specific file types | `"doc"` | `["doc", "xls"]` |
| `exclude_https` | Exclude HTTPS pages | `True` |  |
| `any_keywords` | Require at least one word anywhere in the page | `"python"` | `["python", "django"]` |
| `all_keywords` | Require all of these words somewhere in the page | `"ai"` | `["ai", "ml", "nlp"]` |
| `exact_phrases` | Include results with exact phrases | `"machine learning"` | `["deep learning", "language model"]` |
| `exclude_all_keywords` | Exclude pages containing certain words | `"ads"` | `["ads", "tracking"]` |
| `exclude_exact_phrases` | Exclude results with exact phrases | `"click here"` | `["click here", "buy now"]` |
| `in_title` | Require specific words in the title | `"resume"` | `["resume", "portfolio"]` |
| `in_url` | Require specific words in the URL | `"blog"` | `["blog", "tutorial"]` |
| `in_text` | Require specific words in the page text | `"case study"` | `["case study", "example"]` |
| `not_in_title` | Exclude pages with specific words in the title | `"login"` | `["login", "signup"]` |
| `not_in_url` | Exclude pages with specific words in the URL | `"register"` | `["register", "checkout"]` |
| `not_in_text` | Exclude pages with specific words in the page text | `"error"` | `["error", "404"]` |

The `search` and `async_search` functions have the following parameters that you can use to optimize your searches with:

| Parameter | Type | Description | Default |
| --- | --- | --- | --- |
| `query` | `str` | The search query string. | `""` |
| `filters` | `Filters \| None` | Optional `Filters` object to narrow search results. | `None` |
| `count` | `int` | Number of results to return. | `10` |
| `offset` | `int` | Number of results to skip at the beginning. | `0` |
| `proxy` | `Proxy \| None` | Optional `Proxy` object to route requests through a proxy. | `None` |

## Releases 3

[\+ 2 releases](https://github.com/jpjacobpadilla/SearchAI/releases)

## Packages

No packages published  

## Languages

- [Python 100.0%](https://github.com/jpjacobpadilla/SearchAI/search?l=python)