---
name: rag-pipeline-review
description: Review a retrieval-augmented generation (RAG) pipeline's chunking, embedding, retrieval, and reranking configuration against common failure modes. Use whenever the user asks to review, audit, debug, or improve a RAG pipeline, retrieval quality, or vector search setup (pgvector, ChromaDB, Qdrant), or reports hallucination, missed context, or poor answer quality from a knowledge base.
---

# RAG Pipeline Review

Work through this checklist against the actual code/config, not from
memory of what a "typical" RAG pipeline looks like. For each row, mark
pass/fail and, on fail, give one concrete fix — not a generic tip.

## Checklist

| Dimension | What to check | Common failure |
|---|---|---|
| Chunking vs structure | Does chunk size/split logic respect the document's real structure (headings, tables, legal clauses)? | Fixed-size splitting cuts mid-clause in structured/legal documents |
| Embedding vs corpus language | Is the embedding model confirmed multilingual if the corpus mixes Thai and English (or any two languages)? | English-only embedding model silently underperforms on Thai queries |
| Overlap | Is there chunk overlap, and is it proportional to chunk size (typically 10-20%)? | Zero overlap loses context at chunk boundaries |
| Retrieval top-k vs context window | Is top-k sized against the model's actual usable context, not just "however many fit"? | Too-high top-k dilutes relevant chunks with noise |
| Reranking | Is there a reranking step after initial vector retrieval, or is raw cosine-similarity order trusted directly? | No reranking lets near-duplicate or tangential chunks crowd out the best match |
| Metadata filtering | Can retrieval be scoped by metadata (source, date, doc type) before or alongside vector search? | Missing filter lets stale or wrong-source documents compete unfairly |
| Eval set | Is there a golden set of (query, expected source/answer) pairs to test changes against? | Changes to chunking/embedding get shipped on vibes, regressions go unnoticed |
| Freshness | Is there a re-indexing trigger when source documents change, or is the index static? | Stale index answers from a superseded document version |

## Output

Produce a short table (dimension → pass/fail → note) followed by a ranked
list of 1-3 concrete next actions, ordered by expected impact on answer
quality — not by ease of implementation. If nothing fails, say so plainly
rather than inventing a minor nit to report.

**Completion criterion:** every row above has an explicit pass/fail, not
"looks fine" — if you can't verify a row from the code/config in front of
you, mark it "unable to verify" rather than assuming pass.
