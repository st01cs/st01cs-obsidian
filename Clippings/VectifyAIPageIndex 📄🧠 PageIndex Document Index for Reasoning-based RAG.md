---
title: "VectifyAI/PageIndex: 📄🧠 PageIndex: Document Index for Reasoning-based RAG"
source: https://github.com/VectifyAI/PageIndex
author:
  - "[[rejojer]]"
published:
created: 2025-09-30
description: "📄🧠 PageIndex: Document Index for Reasoning-based RAG - VectifyAI/PageIndex"
tags:
  - clippings
  - rag
---
**[PageIndex](https://github.com/VectifyAI/PageIndex)** Public

📄🧠 PageIndex: Document Index for Reasoning-based RAG

[pageindex.ai](https://pageindex.ai/ "https://pageindex.ai")

[MIT license](https://github.com/VectifyAI/PageIndex/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/VectifyAI/PageIndex?resume=1)

---

🚨 **New Release:**[PageIndex MCP](https://github.com/VectifyAI/pageindex-mcp)

Bring PageIndex into Claude, Cursor, and any MCP-enabled agent. Chat to long PDFs the human-like, reasoning-based way 📖

Are you frustrated with vector database retrieval accuracy for long professional documents? Traditional vector-based RAG relies on semantic *similarity* rather than true *relevance*. But **similarity ≠ relevance** — what we truly need in retrieval is **relevance**, and that requires **reasoning**. When working with professional documents that demand domain expertise and multi-step reasoning, similarity search often falls short.

Inspired by AlphaGo, we propose **[PageIndex](https://vectify.ai/pageindex)**, a **reasoning-based RAG** system that simulates how **human experts** navigate and extract knowledge from long documents through **tree search**, enabling LLMs to *think* and *reason* their way to the most relevant document sections. It performs retrieval in two steps:

1. Generate a "Table-of-Contents" **tree structure index** of documents
2. Perform reasoning-based retrieval through **tree search**

[![](https://camo.githubusercontent.com/eba6bcf31cac3996d09e2b03fe8282b77a562f765ee54aaab2190f37e45d0fc8/68747470733a2f2f646f63732e70616765696e6465782e61692f696d616765732f636f6f6b626f6f6b2f766563746f726c6573732d7261672e706e67)](https://camo.githubusercontent.com/eba6bcf31cac3996d09e2b03fe8282b77a562f765ee54aaab2190f37e45d0fc8/68747470733a2f2f646f63732e70616765696e6465782e61692f696d616765732f636f6f6b626f6f6b2f766563746f726c6573732d7261672e706e67)

### 💡 Features

Compared to traditional vector-based RAG, PageIndex features:

- **No Vectors Needed**: Uses document structure and LLM reasoning for retrieval.
- **No Chunking Needed**: Documents are organized into natural sections, not artificial chunks.
- **Human-like Retrieval**: Simulates how human experts navigate and extract knowledge from complex documents.
- **Transparent Retrieval Process**: Retrieval based on reasoning — say goodbye to approximate vector search ("vibe retrieval").

PageIndex powers a reasoning-based RAG system that achieved [98.7% accuracy](https://github.com/VectifyAI/Mafin2.5-FinanceBench) on FinanceBench, showing state-of-the-art performance in professional document analysis (see our [blog post](https://vectify.ai/blog/Mafin2.5) for details).

- 🛠️ Self-host — run locally with this open-source repo
- ☁️ **[Cloud Service](https://dash.pageindex.ai/)** — try instantly with our 🖥️ [Dashboard](https://dash.pageindex.ai/) or 🔌 [API](https://docs.pageindex.ai/quickstart), no setup required

Check out this simple [*Vectorless RAG Notebook*](https://github.com/VectifyAI/PageIndex/blob/main/cookbook/pageindex_RAG_simple.ipynb) — a minimal, hands-on, reasoning-based RAG pipeline using **PageIndex**.

---

PageIndex can transform lengthy PDF documents into a semantic **tree structure**, similar to a *"table of contents"* but optimized for use with Large Language Models (LLMs). It's ideal for: financial reports, regulatory filings, academic textbooks, legal or technical manuals, and any document that exceeds LLM context limits.

Here is an example output. See more [example documents](https://github.com/VectifyAI/PageIndex/tree/main/tests/pdfs) and [generated trees](https://github.com/VectifyAI/PageIndex/tree/main/tests/results).

```
...
{
  "title": "Financial Stability",
  "node_id": "0006",
  "start_index": 21,
  "end_index": 22,
  "summary": "The Federal Reserve ...",
  "nodes": [
    {
      "title": "Monitoring Financial Vulnerabilities",
      "node_id": "0007",
      "start_index": 22,
      "end_index": 28,
      "summary": "The Federal Reserve's monitoring ..."
    },
    {
      "title": "Domestic and International Cooperation and Coordination",
      "node_id": "0008",
      "start_index": 28,
      "end_index": 31,
      "summary": "In 2023, the Federal Reserve collaborated ..."
    }
  ]
}
...
```

You can either generate the PageIndex tree structure with this open-source repo or try our ☁️ **[Cloud Service](https://dash.pageindex.ai/)** — instantly accessible via our 🖥️ [Dashboard](https://dash.pageindex.ai/) or 🔌 [API](https://docs.pageindex.ai/quickstart), with no setup required.

---

You can follow these steps to generate a PageIndex tree from a PDF document.

```
pip3 install --upgrade -r requirements.txt
```

Create a `.env` file in the root directory and add your API key:

```
CHATGPT_API_KEY=your_openai_key_here
```
```
python3 run_pageindex.py --pdf_path /path/to/your/document.pdf
```
**Optional parameters**  
You can customize the processing with additional optional arguments:

```
--model                 OpenAI model to use (default: gpt-4o-2024-11-20)
--toc-check-pages       Pages to check for table of contents (default: 20)
--max-pages-per-node    Max pages per node (default: 10)
--max-tokens-per-node   Max tokens per node (default: 20000)
--if-add-node-id        Add node ID (yes/no, default: yes)
--if-add-node-summary   Add node summary (yes/no, default: yes)
--if-add-doc-description Add doc description (yes/no, default: yes)
```

**Markdown support**  
We also provide a markdown support for PageIndex. You can use the \`-md\` flag to generate a tree structure for a markdown file.
```
python3 run_pageindex.py --md_path /path/to/your/document.md
```

> Notice: in this function, we use "#" to determine node heading and their levels. For example, "##" is level 2, "###" is level 3, etc. Make sure your markdown file is formatted correctly. If your Markdown file was converted from a PDF or HTML, we don’t recommend using this function, since most existing conversion tools cannot preserve the original hierarchy. Instead, use our [PageIndex OCR](https://pageindex.ai/blog/ocr), which is designed to preserve the original hierarchy, to convert the PDF to a markdown file and then use this function.

---

This repo is designed for generating PageIndex tree structure for simple PDFs, but many real-world use cases involve complex PDFs that are hard to parsed by classic python tools. However, extracting high-quality text from PDF documents remains a non-trivial challenge. Most OCR tools only extract page-level content, losing the broader document context and hierarchy.

To address this, we introduced PageIndex OCR — the first long-context OCR model designed to preserve the global structure of documents. PageIndex OCR significantly outperforms other leading OCR tools, such as those from Mistral and Contextual AI, in recognizing true hierarchy and semantic relationships across document pages.

- Experience next-level OCR quality with PageIndex OCR at our [Dashboard](https://dash.pageindex.ai/).
- Integrate seamlessly PageIndex OCR into your stack via our [API](https://docs.pageindex.ai/quickstart).

[![](https://private-user-images.githubusercontent.com/13518252/475789785-eb35d8ae-865c-4e60-a33b-ebbd00c41732.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMTczMDMsIm5iZiI6MTc1OTIxNzAwMywicGF0aCI6Ii8xMzUxODI1Mi80NzU3ODk3ODUtZWIzNWQ4YWUtODY1Yy00ZTYwLWEzM2ItZWJiZDAwYzQxNzMyLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA5MzAlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwOTMwVDA3MjMyM1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTdjZGJhZGIyYzQ3ZWJmMzYyNzg4NzZlNmY3YWE2YTQyYWFjMWM4ZTljNzE1ZjFkYjQxYTBmYWI2ZmZiNTU0ZjEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.tAqrYfI3BYUJTjiYrdcWenabqT--D_kn2P2tjScZMH0)](https://private-user-images.githubusercontent.com/13518252/475789785-eb35d8ae-865c-4e60-a33b-ebbd00c41732.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMTczMDMsIm5iZiI6MTc1OTIxNzAwMywicGF0aCI6Ii8xMzUxODI1Mi80NzU3ODk3ODUtZWIzNWQ4YWUtODY1Yy00ZTYwLWEzM2ItZWJiZDAwYzQxNzMyLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA5MzAlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwOTMwVDA3MjMyM1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTdjZGJhZGIyYzQ3ZWJmMzYyNzg4NzZlNmY3YWE2YTQyYWFjMWM4ZTljNzE1ZjFkYjQxYTBmYWI2ZmZiNTU0ZjEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.tAqrYfI3BYUJTjiYrdcWenabqT--D_kn2P2tjScZMH0)

---

[Mafin 2.5](https://vectify.ai/mafin) is a state-of-the-art reasoning-based RAG model designed specifically for financial document analysis. Powered by **PageIndex**, it achieved a market-leading [**98.7% accuracy**](https://vectify.ai/blog/Mafin2.5) on the [FinanceBench](https://arxiv.org/abs/2311.11944) benchmark — significantly outperforming traditional vector-based RAG systems.

PageIndex's hierarchical indexing enabled precise navigation and extraction of relevant content from complex financial reports, such as SEC filings and earnings disclosures.

👉 See the full [benchmark results](https://github.com/VectifyAI/Mafin2.5-FinanceBench) and our [blog post](https://vectify.ai/blog/Mafin2.5) for detailed comparisons and performance metrics.

[![](https://private-user-images.githubusercontent.com/8255061/440120069-571aa074-d803-43c7-80c4-a04254b782a3.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMTczMDMsIm5iZiI6MTc1OTIxNzAwMywicGF0aCI6Ii84MjU1MDYxLzQ0MDEyMDA2OS01NzFhYTA3NC1kODAzLTQzYzctODBjNC1hMDQyNTRiNzgyYTMucG5nP1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI1MDkzMCUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNTA5MzBUMDcyMzIzWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9OTlmNmI1YjUwMjMxOTcxMjNlZTBhNmNlNjAzNTRmZjliN2NlM2RlZjUwZTBkYTQxZjZhM2NmN2Q2NmY2ZDdkNiZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QifQ.MEbYjTGmA_twKgOJOFS7_oe-IAEAOjxYljl3r6FMVa0)](https://github.com/VectifyAI/Mafin2.5-FinanceBench)

---

- 📖 Explore our [Tutorials](https://docs.pageindex.ai/doc-search) for practical guides and strategies, including *Document Search* and *Tree Search*.
- 🧪 Browse the [Cookbook](https://docs.pageindex.ai/cookbook/vectorless-rag-pageindex) for practical recipes and advanced use cases.
- ⚙️ Refer to the [API Documentation](https://docs.pageindex.ai/quickstart) for integration details and configuration options.

Leave a star if you like our project. Thank you!

[![](https://private-user-images.githubusercontent.com/13518252/481667856-eae4ff38-48ae-4a7c-b19f-eab81201d794.gif?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMTczMDMsIm5iZiI6MTc1OTIxNzAwMywicGF0aCI6Ii8xMzUxODI1Mi80ODE2Njc4NTYtZWFlNGZmMzgtNDhhZS00YTdjLWIxOWYtZWFiODEyMDFkNzk0LmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA5MzAlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwOTMwVDA3MjMyM1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTgyY2E4MTg3ZDUwMTE3ZTQyZDc4NTYxOTdiYzQ1ODAwM2ExMjNhZDY5NTEyNzVlMGEzNjlhYzFlNjYyZTAyMGImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.cqXob0NIslls6IIitBs5hbyv7MhZ5o7Vl7YU84RuFe8)](https://private-user-images.githubusercontent.com/13518252/481667856-eae4ff38-48ae-4a7c-b19f-eab81201d794.gif?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTkyMTczMDMsIm5iZiI6MTc1OTIxNzAwMywicGF0aCI6Ii8xMzUxODI1Mi80ODE2Njc4NTYtZWFlNGZmMzgtNDhhZS00YTdjLWIxOWYtZWFiODEyMDFkNzk0LmdpZj9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTA5MzAlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUwOTMwVDA3MjMyM1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTgyY2E4MTg3ZDUwMTE3ZTQyZDc4NTYxOTdiYzQ1ODAwM2ExMjNhZDY5NTEyNzVlMGEzNjlhYzFlNjYyZTAyMGImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.cqXob0NIslls6IIitBs5hbyv7MhZ5o7Vl7YU84RuFe8)

---

© 2025 [Vectify AI](https://vectify.ai/)

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Python 78.6%](https://github.com/VectifyAI/PageIndex/search?l=python)
- [Jupyter Notebook 21.4%](https://github.com/VectifyAI/PageIndex/search?l=jupyter-notebook)