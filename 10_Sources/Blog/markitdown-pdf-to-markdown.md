---
type: source
status: draft
created: 2026-07-11
title: "MarkItDown: PDF to Markdown for RAG Pipelines [2026 Guide]"
authors:
- Jason Zhou
organisation: AI Builder Club
source_type: blog
venue: AI Builder Club — Build AI Agents Course, Chapter 3.10
url: https://www.aibuilderclub.com/blog/markitdown-microsoft-convert-files-markdown-llm
year: 2026
date_published: 2026-06-02
anthropic: false
topic:
- topic/tool-use
tags:
- markitdown
- rag
- course
nlm_id:
nlm_skip: false
watchlist_channel: aibuilderclub
---

# MarkItDown: PDF to Markdown for RAG Pipelines [2026 Guide]

> Jason Zhou, "MarkItDown: PDF to Markdown for RAG Pipelines [2026 Guide]", AI Builder Club, Build AI Agents Course, 2 June 2026, https://www.aibuilderclub.com/blog/markitdown-microsoft-convert-files-markdown-llm.

## Summary

Microsoft's open-source `markitdown` library converts PDFs, Office documents, and a dozen-plus other formats into Markdown that keeps its structure — headings stay headings, tables stay tables — rather than the flattened text a naive extractor produces. The lesson's headline claim is that routing documents through `markitdown` before sending them to an LLM typically cuts token usage by 30 to 50% compared with raw PDF text, on top of the retrieval-quality gain from preserved structure.

## Key Concepts

- Structure preservation is the core value proposition: a financial table converted through `markitdown` keeps labelled columns an LLM can reason over, where naive extraction flattens the same table into an unstructured token stream.
- Fifteen-plus supported formats span PDF (including scanned pages via an OCR plugin), Office documents, images with EXIF metadata, audio via speech transcription, HTML, structured data formats, archives, and YouTube URLs.
- An official `markitdown-mcp` server lets Claude Desktop call a `convert_to_markdown` tool directly during a conversation, removing a manual preprocessing step from the workflow.
- Compared against Docling, Marker, Unstructured, and LlamaParse, `markitdown` trades top-end table-extraction accuracy (82% F1 versus 88 to 92% for specialised competitors) for minimal setup, format breadth, and an unrestricted MIT licence.

## Terminology

- Structure-preserving conversion — converting a source document to Markdown while keeping its semantic structure (headings, tables, lists) intact, rather than producing flattened plain text.
- OCR plugin — an add-on using LLM vision at 300 DPI to extract text from scanned or image-based PDF pages, at the cost of an added API call per page.

## Architecture and Implementation

Installation is `pip install 'markitdown[all]'` for full format support, with narrower installs available for specific formats. The Python API is a single `MarkItDown().convert()` call per file; a worked example iterates a documents directory, converts each file, and chunks the resulting Markdown for downstream embedding. Production guidance draws a hard line on the API surface: use `convert_local()` or `convert_stream()` in any user-facing application, and never expose the bare `convert()` method, which accepts and fetches remote URIs directly.

## Code Examples

A directory-iteration example converting mixed-format files to Markdown ahead of chunking, and the `claude_desktop_config.json` entry wiring in the `markitdown-mcp` server for native document handling inside Claude Desktop.

## Best Practices

- Restrict any user-facing deployment to `convert_local()` or `convert_stream()`; never expose `convert()` directly, since it accepts arbitrary remote URIs.
- Enable the OCR plugin selectively, only for scanned or image-heavy documents, since it adds a per-page LLM API cost.
- Run `markitdown` as a containerised conversion microservice when isolation matters, rather than in-process with the main application.
- Route documents through `markitdown` before chunking and embedding in a RAG pipeline rather than embedding raw extracted text.

## Warnings and Anti-Patterns

- Exposing the bare `convert()` method in a user-facing application accepts arbitrary remote URIs as input, which is a real attack surface, not a theoretical one.
- Complex multi-column layouts and dense legal documents produce measurably worse extraction (82% F1) than the library's headline cases; a pipeline depending on perfect table fidelity for such documents should evaluate a specialised alternative instead.
- Table extraction uses XML parsing rather than a machine-learning model, so merged cells or deeply nested headers can silently lose data.

## Related Concepts

- [[tool-use]]
- [[mcp]]
- [[20_People/ai-builder-club/profile|AI Builder Club]]

## Future Work

The lesson notes native video support is absent (only audio transcription is handled), which it flags as a current gap rather than a planned feature.

## References

- MarkItDown: PDF to Markdown for RAG Pipelines [2026 Guide] — https://www.aibuilderclub.com/blog/markitdown-microsoft-convert-files-markdown-llm
