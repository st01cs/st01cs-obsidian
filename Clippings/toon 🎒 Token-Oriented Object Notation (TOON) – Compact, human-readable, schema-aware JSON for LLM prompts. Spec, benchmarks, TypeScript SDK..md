---
title: "toon-format/toon: 🎒 Token-Oriented Object Notation (TOON) – Compact, human-readable, schema-aware JSON for LLM prompts. Spec, benchmarks, TypeScript SDK."
source: "https://github.com/toon-format/toon"
author:
  - "[[johannschopplich]]"
published:
created: 2025-11-14
description: "🎒 Token-Oriented Object Notation (TOON) – Compact, human-readable, schema-aware JSON for LLM prompts. Spec, benchmarks, TypeScript SDK. - toon-format/toon"
tags:
  - "clippings"
---
如果你还在用原生JSON喂LLM，那你其实在浪费tokens、增加延迟和成本！  
试试TOON（Token-Oriented Object Notation），它像YAML一样清晰，像CSV一样紧凑。  
  
优势显著：  
- 节省30%~60% tokens  
- 成本降低最多50%  
- 尤其适合表格数据处理  
  
这不仅是节省，更是效率革命。用更少的token传递同样信息，直接降低调用费用和响应时间。对大规模数据交互的应用尤其关键。  
  
值得思考的是：虽然CSV和TOON都把键和值分开存储，是否会影响LLM的“记忆”与理解？这是未来值得研究的方向。  
  
也有人担心LLM训练时习惯了JSON格式，变换格式会不会影响生成质量？这点还需实测验证，但探索新格式本身就是推动效率创新的关键。  
  
总之，转向TOON或者类似紧凑格式，是降低LLM调用门槛和成本的必由之路。技术人必须拥抱这种token效率的提升，才能真正玩转大模型时代。

🎒 Token-Oriented Object Notation (TOON) – Compact, human-readable, schema-aware JSON for LLM prompts. Spec, benchmarks, TypeScript SDK.

[toonformat.dev](https://toonformat.dev/ "https://toonformat.dev")

[MIT license](https://github.com/toon-format/toon/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/toon-format/toon?resume=1)

<table><thead><tr><th colspan="2"><span>Name</span></th><th colspan="1"><span>Name</span></th><th><p><span>Last commit message</span></p></th><th colspan="1"><p><span>Last commit date</span></p></th></tr></thead><tbody><tr><td colspan="3"><p><span><a href="https://github.com/toon-format/toon/commit/7f8c2379fd4cd3399a0e41e79dcc807cdf2b8f3c">docs: update playground section</a></span></p><p><span><a href="https://github.com/toon-format/toon/commit/7f8c2379fd4cd3399a0e41e79dcc807cdf2b8f3c">7f8c237</a> ·</span></p><p><a href="https://github.com/toon-format/toon/commits/main/"><span><span><span>193 Commits</span></span></span></a></p></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/tree/main/.github">.github</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/tree/main/.github">.github</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/95ac0b0cbc1ec3ac9db425e77f93ae13870035ec">ci(test): run tests on packages in ci (</a><a href="https://github.com/toon-format/toon/pull/111">#111</a><a href="https://github.com/toon-format/toon/commit/95ac0b0cbc1ec3ac9db425e77f93ae13870035ec">)</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/tree/main/.vscode">.vscode</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/tree/main/.vscode">.vscode</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/f105551c3e5419e3fa423c88e56ede3e88066d0e">chore: initial commit</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/tree/main/benchmarks">benchmarks</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/tree/main/benchmarks">benchmarks</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/2e7a27c3c07d096398150a719faa7343670fbca0">chore: upgrade tsdown</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/tree/main/packages">packages</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/tree/main/packages">packages</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/f798bba09521dabaa9933cdfa7197cfb77eeb0c8">test(cli): add tests for stdin input (</a><a href="https://github.com/toon-format/toon/pull/107">#107</a><a href="https://github.com/toon-format/toon/commit/f798bba09521dabaa9933cdfa7197cfb77eeb0c8">)</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/blob/main/.editorconfig">.editorconfig</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/blob/main/.editorconfig">.editorconfig</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/f105551c3e5419e3fa423c88e56ede3e88066d0e">chore: initial commit</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/blob/main/.gitignore">.gitignore</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/blob/main/.gitignore">.gitignore</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/e414ca3671f756a1b1185c221567f297743f5fa9">fix: handle empty list items and nested objects in list items (</a><a href="https://github.com/toon-format/toon/pull/65">#65</a><a href="https://github.com/toon-format/toon/commit/e414ca3671f756a1b1185c221567f297743f5fa9">)</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/blob/main/.npmrc">.npmrc</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/blob/main/.npmrc">.npmrc</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/f105551c3e5419e3fa423c88e56ede3e88066d0e">chore: initial commit</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/blob/main/LICENSE">LICENSE</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/blob/main/LICENSE">LICENSE</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/f105551c3e5419e3fa423c88e56ede3e88066d0e">chore: initial commit</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/blob/main/README.md">README.md</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/blob/main/README.md">README.md</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/7f8c2379fd4cd3399a0e41e79dcc807cdf2b8f3c">docs: update playground section</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/toon-format/toon/blob/main/SPEC.md">SPEC.md</a></p></td><td colspan="1"><p><a href="https://github.com/toon-format/toon/blob/main/SPEC.md">SPEC.md</a></p></td><td><p><a href="https://github.com/toon-format/toon/commit/e8ae024e540ee55e87508e6390abf39452f7c953">feat!: remove optional length marker option <code>[#N]</code> in favor of <code>[N]</code></a></p></td><td></td></tr><tr><td colspan="3"></td></tr></tbody></table>

[![TOON logo with step‑by‑step guide](https://github.com/toon-format/toon/raw/main/.github/og.png)](https://github.com/toon-format/toon/blob/main/.github/og.png)

**Token-Oriented Object Notation** is a compact, human-readable serialization format designed for passing structured data to Large Language Models with significantly reduced token usage. It's intended for *LLM input* as a lossless, drop-in representation of JSON data.

TOON's sweet spot is **uniform arrays of objects** – multiple fields per row, same structure across items. It borrows YAML's indentation-based structure for nested objects and CSV's tabular format for uniform data rows, then optimizes both for token efficiency in LLM contexts. For deeply nested or non-uniform data, JSON may be more efficient.

TOON achieves CSV-like compactness while adding explicit structure that helps LLMs parse and validate data reliably. Think of it as a translation layer: use JSON programmatically, convert to TOON for LLM input.

- [Why TOON?](https://github.com/toon-format/#why-toon)
- [Key Features](https://github.com/toon-format/#key-features)
- [When Not to Use TOON](https://github.com/toon-format/#when-not-to-use-toon)
- [Benchmarks](https://github.com/toon-format/#benchmarks)
- [Playgrounds](https://github.com/toon-format/#playgrounds)
- [📋 Full Specification](https://github.com/toon-format/spec/blob/main/SPEC.md)
- [Installation & Quick Start](https://github.com/toon-format/#installation--quick-start)
- [CLI](https://github.com/toon-format/#cli)
- [Format Overview](https://github.com/toon-format/#format-overview)
- [API](https://github.com/toon-format/#api)
- [Using TOON in LLM Prompts](https://github.com/toon-format/#using-toon-in-llm-prompts)
- [Notes and Limitations](https://github.com/toon-format/#notes-and-limitations)
- [Syntax Cheatsheet](https://github.com/toon-format/#syntax-cheatsheet)
- [Other Implementations](https://github.com/toon-format/#other-implementations)

## Why TOON?

AI is becoming cheaper and more accessible, but larger context windows allow for larger data inputs as well. **LLM tokens still cost money** – and standard JSON is verbose and token-expensive:

```
{
  "users": [
    { "id": 1, "name": "Alice", "role": "admin" },
    { "id": 2, "name": "Bob", "role": "user" }
  ]
}
```

YAML conveys the same infromation with **fewer tokens**:

```
users:
  - id: 1
    name: Alice
    role: admin
  - id: 2
    name: Bob
    role: user
```

TOON conveys the same information with **even fewer tokens**:

```
users[2]{id,name,role}:
  1,Alice,admin
  2,Bob,user
```

## Key Features

- 💸 **Token-efficient:** typically 30-60% fewer tokens on large uniform arrays vs formatted JSON <sup><a href="https://github.com/toon-format/#user-content-fn-1-64def696446a2b9fdf7b06e683df0a3a">1</a></sup>
- 🤿 **LLM-friendly guardrails:** explicit lengths and fields enable validation
- 🍱 **Minimal syntax:** removes redundant punctuation (braces, brackets, most quotes)
- 📐 **Indentation-based structure:** like YAML, uses whitespace instead of braces
- 🧺 **Tabular arrays:** declare keys once, stream data as rows
- 🔗 **Optional key folding:** collapses single-key wrapper chains into dotted paths (e.g., `data.metadata.items`) to reduce indentation and tokens

TOON excels with uniform arrays of objects, but there are cases where other formats are better:

- **Deeply nested or non-uniform structures** (tabular eligibility ≈ 0%): JSON-compact often uses fewer tokens. Example: complex configuration objects with many nested levels.
- **Semi-uniform arrays** (~40–60% tabular eligibility): Token savings diminish. Prefer JSON if your pipelines already rely on it.
- **Pure tabular data**: CSV is smaller than TOON for flat tables. TOON adds minimal overhead (~5-10%) to provide structure (array length declarations, field headers, delimiter scoping) that improves LLM reliability.
- **Latency-critical applications**: If end-to-end response time is your top priority, benchmark on your exact setup. Some deployments (especially local/quantized models like Ollama) may process compact JSON faster despite TOON's lower token count. Measure TTFT, tokens/sec, and total time for both formats and use whichever is faster.

See [benchmarks](https://github.com/toon-format/#benchmarks) for concrete comparisons across different data structures.

## Benchmarks

Benchmarks are organized into two tracks to ensure fair comparisons:

- **Mixed-Structure Track**: Datasets with nested or semi-uniform structures (TOON vs JSON, YAML, XML). CSV excluded as it cannot properly represent these structures.
- **Flat-Only Track**: Datasets with flat tabular structures where CSV is applicable (CSV vs TOON vs JSON, YAML, XML).

### Retrieval Accuracy

Benchmarks test LLM comprehension across different input formats using 209 data retrieval questions on 4 models.

**Show Dataset Catalog**

#### Dataset Catalog

| Dataset | Rows | Structure | CSV Support | Eligibility |
| --- | --- | --- | --- | --- |
| Uniform employee records | 100 | uniform | ✓ | 100% |
| E-commerce orders with nested structures | 50 | nested | ✗ | 33% |
| Time-series analytics data | 60 | uniform | ✓ | 100% |
| Top 100 GitHub repositories | 100 | uniform | ✓ | 100% |
| Semi-uniform event logs | 75 | semi-uniform | ✗ | 50% |
| Deeply nested configuration | 11 | deep | ✗ | 0% |
| Valid complete dataset (control) | 20 | uniform | ✓ | 100% |
| Array truncated: 3 rows removed from end | 17 | uniform | ✓ | 100% |
| Extra rows added beyond declared length | 23 | uniform | ✓ | 100% |
| Inconsistent field count (missing salary in row 10) | 20 | uniform | ✓ | 100% |
| Missing required fields (no email in multiple rows) | 20 | uniform | ✓ | 100% |

**Structure classes:**

- **uniform**: All objects have identical fields with primitive values
- **semi-uniform**: Mix of uniform and non-uniform structures
- **nested**: Objects with nested structures (nested objects or arrays)
- **deep**: Highly nested with minimal tabular eligibility

**CSV Support:** ✓ (supported), ✗ (not supported – would require lossy flattening)

**Eligibility:** Percentage of arrays that qualify for TOON's tabular format (uniform objects with primitive values)

Each format's overall performance, balancing accuracy against token cost:

```
TOON           ████████████████████   26.9  │  73.9% acc  │  2,744 tokens
JSON compact   █████████████████░░░   22.9  │  70.7% acc  │  3,081 tokens
YAML           ██████████████░░░░░░   18.6  │  69.0% acc  │  3,719 tokens
JSON           ███████████░░░░░░░░░   15.3  │  69.7% acc  │  4,545 tokens
XML            ██████████░░░░░░░░░░   13.0  │  67.1% acc  │  5,167 tokens
```

TOON achieves **73.9%** accuracy (vs JSON's 69.7%) while using **39.6% fewer tokens**.

**Note on CSV:** Excluded from ranking as it only supports 109 of 209 questions (flat tabular data only). While CSV is highly token-efficient for simple tabular data, it cannot represent nested structures that other formats handle.

#### Per-Model Accuracy

Accuracy across 4 LLMs on 209 data retrieval questions:

```
claude-haiku-4-5-20251001
→ TOON           ████████████░░░░░░░░    59.8% (125/209)
  JSON           ███████████░░░░░░░░░    57.4% (120/209)
  YAML           ███████████░░░░░░░░░    56.0% (117/209)
  XML            ███████████░░░░░░░░░    55.5% (116/209)
  JSON compact   ███████████░░░░░░░░░    55.0% (115/209)
  CSV            ██████████░░░░░░░░░░    50.5% (55/109)

gemini-2.5-flash
→ TOON           ██████████████████░░    87.6% (183/209)
  CSV            █████████████████░░░    86.2% (94/109)
  JSON compact   ████████████████░░░░    82.3% (172/209)
  YAML           ████████████████░░░░    79.4% (166/209)
  XML            ████████████████░░░░    79.4% (166/209)
  JSON           ███████████████░░░░░    77.0% (161/209)

gpt-5-nano
→ TOON           ██████████████████░░    90.9% (190/209)
  JSON compact   ██████████████████░░    90.9% (190/209)
  JSON           ██████████████████░░    89.0% (186/209)
  CSV            ██████████████████░░    89.0% (97/109)
  YAML           █████████████████░░░    87.1% (182/209)
  XML            ████████████████░░░░    80.9% (169/209)

grok-4-fast-non-reasoning
→ TOON           ███████████░░░░░░░░░    57.4% (120/209)
  JSON           ███████████░░░░░░░░░    55.5% (116/209)
  JSON compact   ███████████░░░░░░░░░    54.5% (114/209)
  YAML           ███████████░░░░░░░░░    53.6% (112/209)
  XML            ███████████░░░░░░░░░    52.6% (110/209)
  CSV            ██████████░░░░░░░░░░    52.3% (57/109)
```

**Key tradeoff:** TOON achieves **73.9% accuracy** (vs JSON's 69.7%) while using **39.6% fewer tokens** on these datasets.

**Performance by dataset, model, and question type**

| Question Type | TOON | JSON compact | JSON | CSV | YAML | XML |
| --- | --- | --- | --- | --- | --- | --- |
| Field Retrieval | 99.6% | 99.3% | 99.3% | 100.0% | 98.2% | 98.9% |
| Aggregation | 54.4% | 47.2% | 48.8% | 44.0% | 47.6% | 41.3% |
| Filtering | 56.3% | 57.3% | 50.5% | 49.1% | 51.0% | 47.9% |
| Structure Awareness | 88.0% | 83.0% | 83.0% | 85.9% | 80.0% | 80.0% |
| Structural Validation | 70.0% | 45.0% | 50.0% | 80.0% | 60.0% | 80.0% |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `csv` | 72.0% | 2,352 | 118/164 |
| `toon` | 73.8% | 2,518 | 121/164 |
| `json-compact` | 69.5% | 3,953 | 114/164 |
| `yaml` | 68.3% | 4,982 | 112/164 |
| `json-pretty` | 68.3% | 6,360 | 112/164 |
| `xml` | 69.5% | 7,324 | 114/164 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `toon` | 81.1% | 7,232 | 133/164 |
| `json-compact` | 76.8% | 6,794 | 126/164 |
| `yaml` | 75.6% | 8,347 | 124/164 |
| `json-pretty` | 76.2% | 10,713 | 125/164 |
| `xml` | 74.4% | 12,023 | 122/164 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `csv` | 73.3% | 1,406 | 88/120 |
| `toon` | 72.5% | 1,548 | 87/120 |
| `json-compact` | 71.7% | 2,349 | 86/120 |
| `yaml` | 71.7% | 2,949 | 86/120 |
| `json-pretty` | 68.3% | 3,676 | 82/120 |
| `xml` | 68.3% | 4,384 | 82/120 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `toon` | 62.9% | 8,780 | 83/132 |
| `csv` | 61.4% | 8,528 | 81/132 |
| `yaml` | 59.8% | 13,142 | 79/132 |
| `json-compact` | 55.3% | 11,465 | 73/132 |
| `json-pretty` | 56.1% | 15,158 | 74/132 |
| `xml` | 48.5% | 17,105 | 64/132 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `json-compact` | 63.3% | 4,819 | 76/120 |
| `toon` | 57.5% | 5,799 | 69/120 |
| `json-pretty` | 59.2% | 6,797 | 71/120 |
| `yaml` | 48.3% | 5,827 | 58/120 |
| `xml` | 46.7% | 7,709 | 56/120 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `json-compact` | 92.2% | 574 | 107/116 |
| `toon` | 95.7% | 666 | 111/116 |
| `yaml` | 91.4% | 686 | 106/116 |
| `json-pretty` | 94.0% | 932 | 109/116 |
| `xml` | 92.2% | 1,018 | 107/116 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `toon` | 100.0% | 544 | 4/4 |
| `json-compact` | 100.0% | 795 | 4/4 |
| `yaml` | 100.0% | 1,003 | 4/4 |
| `json-pretty` | 100.0% | 1,282 | 4/4 |
| `csv` | 25.0% | 492 | 1/4 |
| `xml` | 0.0% | 1,467 | 0/4 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `csv` | 100.0% | 425 | 4/4 |
| `xml` | 100.0% | 1,251 | 4/4 |
| `toon` | 0.0% | 474 | 0/4 |
| `json-compact` | 0.0% | 681 | 0/4 |
| `json-pretty` | 0.0% | 1,096 | 0/4 |
| `yaml` | 0.0% | 859 | 0/4 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `csv` | 100.0% | 566 | 4/4 |
| `toon` | 75.0% | 621 | 3/4 |
| `xml` | 100.0% | 1,692 | 4/4 |
| `yaml` | 75.0% | 1,157 | 3/4 |
| `json-compact` | 50.0% | 917 | 2/4 |
| `json-pretty` | 50.0% | 1,476 | 2/4 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `csv` | 75.0% | 489 | 3/4 |
| `yaml` | 100.0% | 996 | 4/4 |
| `toon` | 100.0% | 1,019 | 4/4 |
| `json-compact` | 75.0% | 790 | 3/4 |
| `xml` | 100.0% | 1,458 | 4/4 |
| `json-pretty` | 75.0% | 1,274 | 3/4 |

| Format | Accuracy | Tokens | Correct/Total |
| --- | --- | --- | --- |
| `csv` | 100.0% | 329 | 4/4 |
| `xml` | 100.0% | 1,411 | 4/4 |
| `toon` | 75.0% | 983 | 3/4 |
| `yaml` | 25.0% | 960 | 1/4 |
| `json-pretty` | 25.0% | 1,230 | 1/4 |
| `json-compact` | 0.0% | 755 | 0/4 |

##### claude-haiku-4-5-20251001

| Format | Accuracy | Correct/Total |
| --- | --- | --- |
| `toon` | 59.8% | 125/209 |
| `json-pretty` | 57.4% | 120/209 |
| `yaml` | 56.0% | 117/209 |
| `xml` | 55.5% | 116/209 |
| `json-compact` | 55.0% | 115/209 |
| `csv` | 50.5% | 55/109 |

##### gemini-2.5-flash

| Format | Accuracy | Correct/Total |
| --- | --- | --- |
| `toon` | 87.6% | 183/209 |
| `csv` | 86.2% | 94/109 |
| `json-compact` | 82.3% | 172/209 |
| `yaml` | 79.4% | 166/209 |
| `xml` | 79.4% | 166/209 |
| `json-pretty` | 77.0% | 161/209 |

##### gpt-5-nano

| Format | Accuracy | Correct/Total |
| --- | --- | --- |
| `toon` | 90.9% | 190/209 |
| `json-compact` | 90.9% | 190/209 |
| `json-pretty` | 89.0% | 186/209 |
| `csv` | 89.0% | 97/109 |
| `yaml` | 87.1% | 182/209 |
| `xml` | 80.9% | 169/209 |

##### grok-4-fast-non-reasoning

| Format | Accuracy | Correct/Total |
| --- | --- | --- |
| `toon` | 57.4% | 120/209 |
| `json-pretty` | 55.5% | 116/209 |
| `json-compact` | 54.5% | 114/209 |
| `yaml` | 53.6% | 112/209 |
| `xml` | 52.6% | 110/209 |
| `csv` | 52.3% | 57/109 |

**How the benchmark works**

This benchmark tests **LLM comprehension and data retrieval accuracy** across different input formats. Each LLM receives formatted data and must answer questions about it (this does **not** test model's ability to generate TOON output).

#### Datasets Tested

Eleven datasets designed to test different structural patterns and validation capabilities:

**Primary datasets:**

1. **Tabular** (100 employee records): Uniform objects with identical fields – optimal for TOON's tabular format.
2. **Nested** (50 e-commerce orders): Complex structures with nested customer objects and item arrays.
3. **Analytics** (60 days of metrics): Time-series data with dates and numeric values.
4. **GitHub** (100 repositories): Real-world data from top GitHub repos by stars.
5. **Event Logs** (75 logs): Semi-uniform data with ~50% flat logs and ~50% with nested error objects.
6. **Nested Config** (1 configuration): Deeply nested configuration with minimal tabular eligibility.

**Structural validation datasets:**7\. **Control**: Valid complete dataset (baseline for validation) 8. **Truncated**: Array with 3 rows removed from end (tests \[N\] length detection) 9. **Extra rows**: Array with 3 additional rows beyond declared length 10. **Width mismatch**: Inconsistent field count (missing salary in row 10) 11. **Missing fields**: Systematic field omissions (no email in multiple rows)

#### Question Types

209 questions are generated dynamically across five categories:

- **Field retrieval (33%)**: Direct value lookups or values that can be read straight off a record (including booleans and simple counts such as array lengths)
	- Example: "What is Alice's salary?" → `75000`
	- Example: "How many items are in order ORD-0042?" → `3`
	- Example: "What is the customer name for order ORD-0042?" → `John Doe`
- **Aggregation (30%)**: Dataset-level totals and averages plus single-condition filters (counts, sums, min/max comparisons)
	- Example: "How many employees work in Engineering?" → `17`
	- Example: "What is the total revenue across all orders?" → `45123.50`
	- Example: "How many employees have salary > 80000?" → `23`
- **Filtering (23%)**: Multi-condition queries requiring compound logic (AND constraints across fields)
	- Example: "How many employees in Sales have salary > 80000?" → `5`
	- Example: "How many active employees have more than 10 years of experience?" → `8`
- **Structure awareness (12%)**: Tests format-native structural affordances (TOON's \[N\] count and {fields}, CSV's header row)
	- Example: "How many employees are in the dataset?" → `100`
	- Example: "List the field names for employees" → `id, name, email, department, salary, yearsExperience, active`
	- Example: "What is the department of the last employee?" → `Sales`
- **Structural validation (2%)**: Tests ability to detect incomplete, truncated, or corrupted data using structural metadata
	- Example: "Is this data complete and valid?" → `YES` (control dataset) or `NO` (corrupted datasets)
	- Tests TOON's \[N\] length validation and {fields} consistency checking
	- Demonstrates CSV's lack of structural validation capabilities

#### Evaluation Process

1. **Format conversion**: Each dataset is converted to all 6 formats (TOON, JSON compact, JSON, CSV, YAML, XML).
2. **Query LLM**: Each model receives formatted data + question in a prompt and extracts the answer.
3. **Validate deterministically**: Answers are validated using type-aware comparison (e.g., `50000` = `$50,000`, `Engineering` = `engineering`, `2025-01-01` = `January 1, 2025`) without requiring an LLM judge.
- **Models tested**: `claude-haiku-4-5-20251001`, `gemini-2.5-flash`, `gpt-5-nano`, `grok-4-fast-non-reasoning`
- **Token counting**: Using `gpt-tokenizer` with `o200k_base` encoding (GPT-5 tokenizer)
- **Temperature**: Not set (models use their defaults)
- **Total evaluations**: 209 questions × 6 formats × 4 models = 5,016 LLM calls

### Token Efficiency

Token counts are measured using the GPT-5 `o200k_base` tokenizer via [`gpt-tokenizer`](https://github.com/niieani/gpt-tokenizer). Savings are calculated against formatted JSON (2-space indentation) as the primary baseline, with additional comparisons to compact JSON (minified), YAML, and XML. Actual savings vary by model and tokenizer.

The benchmarks test datasets across different structural patterns (uniform, semi-uniform, nested, deeply nested) to show where TOON excels and where other formats may be better.

#### Mixed-Structure Track

Datasets with nested or semi-uniform structures. CSV excluded as it cannot properly represent these structures.

```
🛒 E-commerce orders with nested structures  ┊  Tabular: 33%
   │
   TOON                █████████████░░░░░░░    72,771 tokens
   ├─ vs JSON          (−33.1%)               108,806 tokens
   ├─ vs JSON compact  (+5.5%)                 68,975 tokens
   ├─ vs YAML          (−14.2%)                84,780 tokens
   └─ vs XML           (−40.5%)               122,406 tokens

🧾 Semi-uniform event logs  ┊  Tabular: 50%
   │
   TOON                █████████████████░░░   153,211 tokens
   ├─ vs JSON          (−15.0%)               180,176 tokens
   ├─ vs JSON compact  (+19.9%)               127,731 tokens
   ├─ vs YAML          (−0.8%)                154,505 tokens
   └─ vs XML           (−25.2%)               204,777 tokens

🧩 Deeply nested configuration  ┊  Tabular: 0%
   │
   TOON                ██████████████░░░░░░       631 tokens
   ├─ vs JSON          (−31.3%)                   919 tokens
   ├─ vs JSON compact  (+11.9%)                   564 tokens
   ├─ vs YAML          (−6.2%)                    673 tokens
   └─ vs XML           (−37.4%)                 1,008 tokens

──────────────────────────────────── Total ────────────────────────────────────
   TOON                ████████████████░░░░   226,613 tokens
   ├─ vs JSON          (−21.8%)               289,901 tokens
   ├─ vs JSON compact  (+14.9%)               197,270 tokens
   ├─ vs YAML          (−5.6%)                239,958 tokens
   └─ vs XML           (−31.0%)               328,191 tokens
```

#### Flat-Only Track

Datasets with flat tabular structures where CSV is applicable.

```
👥 Uniform employee records  ┊  Tabular: 100%
   │
   CSV                 ███████████████████░    46,954 tokens
   TOON                ████████████████████    49,831 tokens   (+6.1% vs CSV)
   ├─ vs JSON          (−60.7%)               126,860 tokens
   ├─ vs JSON compact  (−36.8%)                78,856 tokens
   ├─ vs YAML          (−50.0%)                99,706 tokens
   └─ vs XML           (−66.0%)               146,444 tokens

📈 Time-series analytics data  ┊  Tabular: 100%
   │
   CSV                 ██████████████████░░     8,388 tokens
   TOON                ████████████████████     9,120 tokens   (+8.7% vs CSV)
   ├─ vs JSON          (−59.0%)                22,250 tokens
   ├─ vs JSON compact  (−35.8%)                14,216 tokens
   ├─ vs YAML          (−48.9%)                17,863 tokens
   └─ vs XML           (−65.7%)                26,621 tokens

⭐ Top 100 GitHub repositories  ┊  Tabular: 100%
   │
   CSV                 ███████████████████░     8,513 tokens
   TOON                ████████████████████     8,745 tokens   (+2.7% vs CSV)
   ├─ vs JSON          (−42.3%)                15,145 tokens
   ├─ vs JSON compact  (−23.7%)                11,455 tokens
   ├─ vs YAML          (−33.4%)                13,129 tokens
   └─ vs XML           (−48.8%)                17,095 tokens

──────────────────────────────────── Total ────────────────────────────────────
   CSV                 ███████████████████░    63,855 tokens
   TOON                ████████████████████    67,696 tokens   (+6.0% vs CSV)
   ├─ vs JSON          (−58.8%)               164,255 tokens
   ├─ vs JSON compact  (−35.2%)               104,527 tokens
   ├─ vs YAML          (−48.2%)               130,698 tokens
   └─ vs XML           (−64.4%)               190,160 tokens
```

**Show detailed examples**

**Savings:** 13,130 tokens (59.0% reduction vs JSON)

**JSON** (22,250 tokens):

```
{
  "metrics": [
    {
      "date": "2025-01-01",
      "views": 5715,
      "clicks": 211,
      "conversions": 28,
      "revenue": 7976.46,
      "bounceRate": 0.47
    },
    {
      "date": "2025-01-02",
      "views": 7103,
      "clicks": 393,
      "conversions": 28,
      "revenue": 8360.53,
      "bounceRate": 0.32
    },
    {
      "date": "2025-01-03",
      "views": 7248,
      "clicks": 378,
      "conversions": 24,
      "revenue": 3212.57,
      "bounceRate": 0.5
    },
    {
      "date": "2025-01-04",
      "views": 2927,
      "clicks": 77,
      "conversions": 11,
      "revenue": 1211.69,
      "bounceRate": 0.62
    },
    {
      "date": "2025-01-05",
      "views": 3530,
      "clicks": 82,
      "conversions": 8,
      "revenue": 462.77,
      "bounceRate": 0.56
    }
  ]
}
```

**TOON** (9,120 tokens):

```
metrics[5]{date,views,clicks,conversions,revenue,bounceRate}:
  2025-01-01,5715,211,28,7976.46,0.47
  2025-01-02,7103,393,28,8360.53,0.32
  2025-01-03,7248,378,24,3212.57,0.5
  2025-01-04,2927,77,11,1211.69,0.62
  2025-01-05,3530,82,8,462.77,0.56
```

---

**Savings:** 6,400 tokens (42.3% reduction vs JSON)

**JSON** (15,145 tokens):

```
{
  "repositories": [
    {
      "id": 28457823,
      "name": "freeCodeCamp",
      "repo": "freeCodeCamp/freeCodeCamp",
      "description": "freeCodeCamp.org's open-source codebase and curriculum. Learn math, programming,…",
      "createdAt": "2014-12-24T17:49:19Z",
      "updatedAt": "2025-10-28T11:58:08Z",
      "pushedAt": "2025-10-28T10:17:16Z",
      "stars": 430886,
      "watchers": 8583,
      "forks": 42146,
      "defaultBranch": "main"
    },
    {
      "id": 132750724,
      "name": "build-your-own-x",
      "repo": "codecrafters-io/build-your-own-x",
      "description": "Master programming by recreating your favorite technologies from scratch.",
      "createdAt": "2018-05-09T12:03:18Z",
      "updatedAt": "2025-10-28T12:37:11Z",
      "pushedAt": "2025-10-10T18:45:01Z",
      "stars": 430877,
      "watchers": 6332,
      "forks": 40453,
      "defaultBranch": "master"
    },
    {
      "id": 21737465,
      "name": "awesome",
      "repo": "sindresorhus/awesome",
      "description": "😎 Awesome lists about all kinds of interesting topics",
      "createdAt": "2014-07-11T13:42:37Z",
      "updatedAt": "2025-10-28T12:40:21Z",
      "pushedAt": "2025-10-27T17:57:31Z",
      "stars": 410052,
      "watchers": 8017,
      "forks": 32029,
      "defaultBranch": "main"
    }
  ]
}
```

**TOON** (8,745 tokens):

```
repositories[3]{id,name,repo,description,createdAt,updatedAt,pushedAt,stars,watchers,forks,defaultBranch}:
  28457823,freeCodeCamp,freeCodeCamp/freeCodeCamp,"freeCodeCamp.org's open-source codebase and curriculum. Learn math, programming,…","2014-12-24T17:49:19Z","2025-10-28T11:58:08Z","2025-10-28T10:17:16Z",430886,8583,42146,main
  132750724,build-your-own-x,codecrafters-io/build-your-own-x,Master programming by recreating your favorite technologies from scratch.,"2018-05-09T12:03:18Z","2025-10-28T12:37:11Z","2025-10-10T18:45:01Z",430877,6332,40453,master
  21737465,awesome,sindresorhus/awesome,😎 Awesome lists about all kinds of interesting topics,"2014-07-11T13:42:37Z","2025-10-28T12:40:21Z","2025-10-27T17:57:31Z",410052,8017,32029,main
```

## Playgrounds

Experiment with TOON format interactively using these community-built tools:

- **[Format Tokenization Playground](https://www.curiouslychase.com/playground/format-tokenization-exploration)** – Compare token usage across CSV, JSON (pretty/compressed), YAML, and TOON formats. Use preset datasets or paste your own data to see real-time token comparisons.
- **[TOON Tools](https://toontools.vercel.app/)** – Full toolkit including bidirectional converters (JSON, CSV, XML, YAML ↔ TOON), token counter with side-by-side comparison, TOON validator, batch file converter, and format playground.
```
# npm
npm install @toon-format/toon

# pnpm
pnpm add @toon-format/toon

# yarn
yarn add @toon-format/toon
```

**Example usage:**

```
import { encode } from '@toon-format/toon'

const data = {
  users: [
    { id: 1, name: 'Alice', role: 'admin' },
    { id: 2, name: 'Bob', role: 'user' }
  ]
}

console.log(encode(data))
// users[2]{id,name,role}:
//   1,Alice,admin
//   2,Bob,user
```

## CLI

Command-line tool for converting between JSON and TOON formats.

### Usage

```
npx @toon-format/cli [options] [input]
```

**Standard input:** Omit the input argument or use `-` to read from stdin. This enables piping data directly from other commands.

**Auto-detection:** The CLI automatically detects the operation based on file extension (`.json` → encode, `.toon` → decode). When reading from stdin, use `--encode` or `--decode` flags to specify the operation (defaults to encode).

```
# Encode JSON to TOON (auto-detected)
npx @toon-format/cli input.json -o output.toon

# Decode TOON to JSON (auto-detected)
npx @toon-format/cli data.toon -o output.json

# Output to stdout
npx @toon-format/cli input.json

# Pipe from stdin (no argument needed)
cat data.json | npx @toon-format/cli
echo '{"name": "Ada"}' | npx @toon-format/cli

# Explicit stdin with hyphen (equivalent to above)
cat data.json | npx @toon-format/cli -

# Decode from stdin
cat data.toon | npx @toon-format/cli --decode
```

### Options

| Option | Description |
| --- | --- |
| `-o, --output <file>` | Output file path (prints to stdout if omitted) |
| `-e, --encode` | Force encode mode (overrides auto-detection) |
| `-d, --decode` | Force decode mode (overrides auto-detection) |
| `--delimiter <char>` | Array delimiter: `,` (comma), `\t` (tab), `\|` (pipe) |
| `--indent <number>` | Indentation size (default: `2`) |
| `--stats` | Show token count estimates and savings (encode only) |
| `--no-strict` | Disable strict validation when decoding |
| `--key-folding <mode>` | Key folding mode: `off`, `safe` (default: `off`) - collapses nested chains |
| `--flatten-depth <number>` | Maximum segments to fold (default: `Infinity`) - requires `--key-folding safe` |
| `--expand-paths <mode>` | Path expansion mode: `off`, `safe` (default: `off`) - reconstructs dotted keys |

### Examples

```
# Show token savings when encoding
npx @toon-format/cli data.json --stats -o output.toon

# Tab-separated output (often more token-efficient)
npx @toon-format/cli data.json --delimiter "\t" -o output.toon

# Pipe-separated output
npx @toon-format/cli data.json --delimiter "|" -o output.toon

# Lenient decoding (skip validation)
npx @toon-format/cli data.toon --no-strict -o output.json

# Key folding for nested data
npx @toon-format/cli data.json --key-folding safe -o output.toon

# Stdin workflows
echo '{"name": "Ada", "age": 30}' | npx @toon-format/cli --stats
cat large-dataset.json | npx @toon-format/cli --delimiter "\t" > output.toon
```

## Format Overview

### Objects

Simple objects with primitive values:

```
encode({
  id: 123,
  name: 'Ada',
  active: true
})
```

```
id: 123
name: Ada
active: true
```

Nested objects:

```
encode({
  user: {
    id: 123,
    name: 'Ada'
  }
})
```

```
user:
  id: 123
  name: Ada
```

New in spec v1.5: Optionally collapse single-key wrapper chains into dotted paths to reduce tokens. Enable with `keyFolding: 'safe'`.

Standard nesting:

```
data:
  metadata:
    items[2]: a,b
```

With key folding:

```
data.metadata.items[2]: a,b
```

Round-trip with path expansion:

```
import { decode, encode } from '@toon-format/toon'

const original = { data: { metadata: { items: ['a', 'b'] } } }

const toon = encode(original, { keyFolding: 'safe' })
// → "data.metadata.items[2]: a,b"

const restored = decode(toon, { expandPaths: 'safe' })
// → Matches original structure
```

See §13.4 in the [specification](https://github.com/toon-format/spec/blob/main/SPEC.md#134-key-folding-and-path-expansion) for folding rules and safety guarantees.

### Arrays

```
encode({
  tags: ['admin', 'ops', 'dev']
})
```

```
tags[3]: admin,ops,dev
```

When all objects share the same primitive fields, TOON uses an efficient **tabular format**:

```
encode({
  items: [
    { sku: 'A1', qty: 2, price: 9.99 },
    { sku: 'B2', qty: 1, price: 14.5 }
  ]
})
```

```
items[2]{sku,qty,price}:
  A1,2,9.99
  B2,1,14.5
```

**Tabular formatting applies recursively:** nested arrays of objects (whether as object properties or inside list items) also use tabular format if they meet the same requirements.

```
encode({
  items: [
    {
      users: [
        { id: 1, name: 'Ada' },
        { id: 2, name: 'Bob' }
      ],
      status: 'active'
    }
  ]
})
```

```
items[1]:
  - users[2]{id,name}:
    1,Ada
    2,Bob
    status: active
```

Arrays that don't meet the tabular requirements use list format:

```
items[3]:
  - 1
  - a: 1
  - text
```

When objects appear in list format, the first field is placed on the hyphen line:

```
items[2]:
  - id: 1
    name: First
  - id: 2
    name: Second
    extra: true
```

When you have arrays containing primitive inner arrays:

```
encode({
  pairs: [
    [1, 2],
    [3, 4]
  ]
})
```

```
pairs[2]:
  - [2]: 1,2
  - [2]: 3,4
```

Empty containers have special representations:

```
encode({ items: [] }) // items[0]:
encode([]) // [0]:
encode({}) // (empty output)
encode({ config: {} }) // config:
```

### Quoting Rules

TOON quotes strings **only when necessary** to maximize token efficiency:

- Inner spaces are allowed; leading or trailing spaces force quotes.
- Unicode and emoji are safe unquoted.
- Quotes and control characters are escaped with backslash.

Keys are unquoted if they match the identifier pattern: start with a letter or underscore, followed by letters, digits, underscores, or dots (e.g., `id`, `userName`, `user_name`, `user.name`, `_private`). All other keys must be quoted (e.g., `"user name"`, `"order-id"`, `"123"`, `"order:id"`, `""`).

#### String Values

String values are quoted when any of the following is true:

| Condition | Examples |
| --- | --- |
| Empty string | `""` |
| Leading or trailing spaces | `" padded "`, `"  "` |
| Contains active delimiter, colon, quote, backslash, or control chars | `"a,b"` (comma), `"a\tb"` (tab), `"a\|b"` (pipe), `"a:b"`, `"say \"hi\""`, `"C:\\Users"`, `"line1\\nline2"` |
| Looks like boolean/number/null | `"true"`, `"false"`, `"null"`, `"42"`, `"-3.14"`, `"1e-6"`, `"05"` |
| Starts with `"- "` (list-like) | `"- item"` |
| Looks like structural token | `"[5]"`, `"{key}"`, `"[3]: x,y"` |

**Examples of unquoted strings:** Unicode and emoji are safe (`hello 👋 world`), as are strings with inner spaces (`hello world`).

### Type Conversions

Some non-JSON types are automatically normalized for LLM-safe output:

| Input | Output |
| --- | --- |
| Number (finite) | Decimal form, no scientific notation (e.g., `-0` → `0`, `1e6` → `1000000`) |
| Number (`NaN`, `±Infinity`) | `null` |
| `BigInt` | If within safe integer range: converted to number. Otherwise: quoted decimal string (e.g., `"9007199254740993"`) |
| `Date` | ISO string in quotes (e.g., `"2025-01-01T00:00:00.000Z"`) |
| `undefined` | `null` |
| `function` | `null` |
| `symbol` | `null` |

## API

Converts any JSON-serializable value to TOON format.

**Parameters:**

- `value` – Any JSON-serializable value (object, array, primitive, or nested structure). Non-JSON-serializable values (functions, symbols, undefined, non-finite numbers) are converted to `null`. Dates are converted to ISO strings, and BigInts are emitted as decimal integers (no quotes).
- `options` – Optional encoding options:
	- `indent?: number` – Number of spaces per indentation level (default: `2`)
	- `delimiter?: ',' | '\t' | '|'` – Delimiter for array values and tabular rows (default: `','`)
	- `keyFolding?: 'off' | 'safe'` – Enable key folding to collapse single-key wrapper chains into dotted paths (default: `'off'`). When `'safe'`, only valid identifier segments are folded
	- `flattenDepth?: number` – Maximum number of segments to fold when `keyFolding` is enabled (default: `Infinity`). Values 0-1 have no practical effect

**Returns:**

A TOON-formatted string with no trailing newline or spaces.

**Example:**

```
import { encode } from '@toon-format/toon'

const items = [
  { sku: 'A1', qty: 2, price: 9.99 },
  { sku: 'B2', qty: 1, price: 14.5 }
]

encode({ items })
```

**Output:**

```
items[2]{sku,qty,price}:
  A1,2,9.99
  B2,1,14.5
```

#### Delimiter Options

The `delimiter` option allows you to choose between comma (default), tab, or pipe delimiters for array values and tabular rows. Alternative delimiters can provide additional token savings in specific contexts.

Using tab delimiters instead of commas can reduce token count further, especially for tabular data:

```
const data = {
  items: [
    { sku: 'A1', name: 'Widget', qty: 2, price: 9.99 },
    { sku: 'B2', name: 'Gadget', qty: 1, price: 14.5 }
  ]
}

encode(data, { delimiter: '\t' })
```

**Output:**

```
items[2    ]{sku    name    qty    price}:
  A1    Widget    2    9.99
  B2    Gadget    1    14.5
```

**Benefits:**

- Tabs are single characters and often tokenize more efficiently than commas.
- Tabs rarely appear in natural text, reducing the need for quote-escaping.
- The delimiter is explicitly encoded in the array header, making it self-descriptive.

**Considerations:**

- Some terminals and editors may collapse or expand tabs visually.
- String values containing tabs will still require quoting.

Pipe delimiters offer a middle ground between commas and tabs:

```
encode(data, { delimiter: '|' })
```

**Output:**

```
items[2|]{sku|name|qty|price}:
  A1|Widget|2|9.99
  B2|Gadget|1|14.5
```

Converts a TOON-formatted string back to JavaScript values.

**Parameters:**

- `input` – A TOON-formatted string to parse
- `options` – Optional decoding options:
	- `indent?: number` – Expected number of spaces per indentation level (default: `2`)
	- `strict?: boolean` – Enable strict validation (default: `true`)
	- `expandPaths?: 'off' | 'safe'` – Enable path expansion to reconstruct dotted keys into nested objects (default: `'off'`). Pairs with `keyFolding: 'safe'` for lossless round-trips

**Returns:**

A JavaScript value (object, array, or primitive) representing the parsed TOON data.

**Example:**

```
import { decode } from '@toon-format/toon'

const toon = \`
items[2]{sku,qty,price}:
  A1,2,9.99
  B2,1,14.5
\`

const data = decode(toon)
// {
//   items: [
//     { sku: 'A1', qty: 2, price: 9.99 },
//     { sku: 'B2', qty: 1, price: 14.5 }
//   ]
// }
```

**Strict Mode:**

By default, the decoder validates input strictly:

- **Invalid escape sequences**: Throws on `"\x"`, unterminated strings.
- **Syntax errors**: Throws on missing colons, malformed headers.
- **Array length mismatches**: Throws when declared length doesn't match actual count.
- **Delimiter mismatches**: Throws when row delimiters don't match header.
- Format familiarity and structure matter as much as token count. TOON's tabular format requires arrays of objects with identical keys and primitive values only. When this doesn't hold (due to mixed types, non-uniform objects, or nested structures), TOON switches to list format where JSON can be more efficient at scale.
	- **TOON excels at:** Uniform arrays of objects (same fields, primitive values), especially large datasets with consistent structure.
	- **JSON is better for:** Non-uniform data, deeply nested structures, and objects with varying field sets.
	- **CSV is more compact for:** Flat, uniform tables without nesting. TOON adds structure (`[N]` array lengths, delimiter scoping, deterministic quoting) that improves LLM reliability with minimal token overhead.
- **Token counts vary by tokenizer and model.** Benchmarks use a GPT-style tokenizer (cl100k/o200k); actual savings will differ with other models (e.g., [SentencePiece](https://github.com/google/sentencepiece)).
- **TOON is designed for LLM input** where human readability and token efficiency matter. It's **not** a drop-in replacement for JSON in APIs or storage.

TOON works best when you show the format instead of describing it. The structure is self-documenting – models parse it naturally once they see the pattern.

Wrap your encoded data in a fenced code block (label it \`\`\`toon for clarity). The indentation and headers are usually enough – models treat it like familiar YAML or CSV. The explicit array lengths (`[N]`) and field headers (`{field1,field2}`) help the model track structure, especially for large tables.

For output, be more explicit. When you want the model to **generate** TOON:

- **Show the expected header** (`users[N]{id,name,role}:`). The model fills rows instead of repeating keys, reducing generation errors.
- **State the rules:** 2-space indent, no trailing spaces, `[N]` matches row count.

Here's a prompt that works for both reading and generating:

```
Data is in TOON format (2-space indent, arrays show length and fields).

\`\`\`toon
users[3]{id,name,role,lastLogin}:
  1,Alice,admin,2025-01-15T10:30:00Z
  2,Bob,user,2025-01-14T15:22:00Z
  3,Charlie,user,2025-01-13T09:45:00Z
\`\`\`

Task: Return only users with role "user" as TOON. Use the same header. Set [N] to match the row count. Output only the code block.
```

## Syntax Cheatsheet

**Show format examples**

```
// Object
{ id: 1, name: 'Ada' }          → id: 1
                                  name: Ada

// Nested object
{ user: { id: 1 } }             → user:
                                    id: 1

// Primitive array (inline)
{ tags: ['foo', 'bar'] }        → tags[2]: foo,bar

// Tabular array (uniform objects)
{ items: [                      → items[2]{id,qty}:
  { id: 1, qty: 5 },                1,5
  { id: 2, qty: 3 }                 2,3
]}

// Mixed / non-uniform (list)
{ items: [1, { a: 1 }, 'x'] }   → items[3]:
                                    - 1
                                    - a: 1
                                    - x

// Array of arrays
{ pairs: [[1, 2], [3, 4]] }     → pairs[2]:
                                    - [2]: 1,2
                                    - [2]: 3,4

// Root array
['x', 'y']                      → [2]: x,y

// Empty containers
{}                              → (empty output)
{ items: [] }                   → items[0]:

// Special quoting
{ note: 'hello, world' }        → note: "hello, world"
{ items: ['true', true] }       → items[2]: "true",true
```

## Other Implementations

### Official Implementations

- **Python:**[toon\_format](https://github.com/toon-format/toon-python) *(in development)*
- **Rust:**[toon\_format](https://github.com/toon-format/toon-rust) *(in development)*

### Community Implementations

- **.NET:**[ToonSharp](https://github.com/0xZunia/ToonSharp)
- **C++:**[ctoon](https://github.com/mohammadraziei/ctoon)
- **Clojure:**[toon](https://github.com/vadelabs/toon)
- **Crystal:**[toon-crystal](https://github.com/mamantoha/toon-crystal)
- **Dart:**[toon](https://github.com/wisamidris77/toon)
- **Elixir:**[toon\_ex](https://github.com/kentaro/toon_ex)
- **Gleam:**[toon\_codec](https://github.com/axelbellec/toon_codec)
- **Go:**[gotoon](https://github.com/alpkeskin/gotoon)
- **Java:**[JToon](https://github.com/felipestanzani/JToon)
- **Scala:**[toon4s](https://github.com/vim89/toon4s)
- **Lua/Neovim:**[toon.nvim](https://github.com/thalesgelinger/toon.nvim)
- **OCaml:**[ocaml-toon](https://github.com/davesnx/ocaml-toon)
- **PHP:**[toon-php](https://github.com/HelgeSverre/toon-php)
- **R**: [toon](https://github.com/laresbernardo/toon)
- **Ruby:**[toon-ruby](https://github.com/andrepcg/toon-ruby)
- **Swift:**[TOONEncoder](https://github.com/mattt/TOONEncoder)
- **Kotlin:**[Kotlin-Toon Encoder/Decoder](https://github.com/vexpera-br/kotlin-toon)

## Credits

- Logo design by [鈴木ックス(SZKX)](https://x.com/szkx_art)

## License

[MIT](https://github.com/toon-format/toon/blob/main/LICENSE) License © 2025-PRESENT [Johann Schopplich](https://github.com/johannschopplich)

## Releases 18

[\+ 17 releases](https://github.com/toon-format/toon/releases)

## Packages

No packages published  

## Languages

- [TypeScript 99.9%](https://github.com/toon-format/toon/search?l=typescript)
- [JavaScript 0.1%](https://github.com/toon-format/toon/search?l=javascript)

[^1]: For flat tabular data, CSV is more compact. TOON adds minimal overhead to provide explicit structure and validation that improves LLM reliability.