# 🔍 Day 8 — Retrieval-Augmented Generation (RAG): Grounding LLMs with External Knowledge

**Date:** 2026-03-26  
**Topic:** RAG — Making LLMs Factual and Up-to-Date  
**Papers:** [RAG (2020)](https://arxiv.org/abs/2005.11401) · [REALM (2020)](https://arxiv.org/abs/2002.08909) · [Self-RAG (2023)](https://arxiv.org/abs/2310.11511)  
**Level:** 🟡 Intermediate

---

## The Problem: LLMs Hallucinate

Large Language Models store knowledge in their parameters, but this has critical limitations:

- **Hallucination** — LLMs confidently generate incorrect or fabricated facts
- **Stale knowledge** — Training data has a cutoff date; the model can't know recent events
- **No source attribution** — Users can't verify where an answer came from
- **Domain gaps** — LLMs lack expertise in specialized or proprietary domains

**The core idea of RAG**: Instead of asking the model to "remember" everything, **retrieve relevant documents at inference time** and let the model reason over them.

---

## How RAG Works

### The Two-Stage Pipeline

```
User Query → [Retriever] → Top-K Relevant Documents → [Generator (LLM)] → Grounded Answer
```

1. **Retrieve**: Given a user query, search a knowledge base (vector DB, search index) for the most relevant documents or passages
2. **Augment**: Inject the retrieved context into the LLM's prompt
3. **Generate**: The LLM produces an answer grounded in the retrieved evidence

### Architecture Components

| Component | Role | Common Choices |
|---|---|---|
| **Embedding model** | Encode queries + docs into vectors | `text-embedding-3-small`, `bge-large`, `e5-mistral` |
| **Vector database** | Store and search embeddings efficiently | FAISS, Pinecone, Weaviate, Chroma, Qdrant |
| **Chunking strategy** | Split documents into meaningful pieces | Fixed-size, sentence-level, semantic chunking |
| **Reranker** | Re-score retrieved docs for relevance | Cohere Rerank, `bge-reranker`, cross-encoders |
| **Generator** | Produce the final answer | GPT-4, Claude, LLaMA, Mistral |

---

## The Original RAG Paper (Lewis et al., 2020)

The original paper introduced two variants:

### RAG-Sequence
Retrieves documents **once** and uses the same set of documents to generate the **entire** output sequence.

### RAG-Token
Retrieves documents **per token** — at each generation step, the model can attend to different retrieved documents. More flexible but more expensive.

Both models combine a **DPR (Dense Passage Retrieval)** retriever with a **BART** generator, trained end-to-end.

> **Key insight**: By training retriever + generator jointly, the model learns *what to retrieve* to produce better answers.

---

## Advanced RAG Techniques

### 1. Chunking Strategies
| Strategy | Description | Best For |
|---|---|---|
| **Fixed-size** | Split every N tokens | Simple, fast |
| **Sentence-level** | Split at sentence boundaries | Preserving meaning |
| **Semantic** | Group by topic/meaning using embeddings | Complex documents |
| **Parent-child** | Retrieve small chunks, expand to parent | Precision + context |

### 2. Query Optimization
- **HyDE (Hypothetical Document Embeddings)** — Generate a hypothetical answer, embed it, and use that for retrieval
- **Query decomposition** — Break complex questions into sub-queries
- **Step-back prompting** — Ask a more general question first for better retrieval

### 3. Self-RAG (2023)
The model learns to:
- Decide **when** to retrieve (not every query needs retrieval)
- **Critique** retrieved passages for relevance
- **Evaluate** its own generation for factual support

This makes RAG adaptive rather than always-on.

---

## RAG vs. Fine-Tuning

| Aspect | RAG | Fine-Tuning |
|---|---|---|
| **Knowledge update** | Instant (update the index) | Requires retraining |
| **Cost** | Lower (no GPU training) | Higher (GPU hours) |
| **Hallucination** | Reduced (grounded in sources) | Still possible |
| **Domain adaptation** | Good for factual recall | Better for style/behavior |
| **Latency** | Higher (retrieval step) | Lower (single pass) |
| **Best for** | Dynamic, factual QA | Task-specific behavior |

> 💡 **In practice, the best systems combine both**: fine-tune for behavior + RAG for knowledge.

---

## Building a RAG Pipeline (Simplified)

```python
# Pseudocode for a basic RAG pipeline
from langchain import VectorStore, LLM, RetrievalQA

# 1. Load and chunk documents
docs = load_documents("knowledge_base/")
chunks = split_into_chunks(docs, chunk_size=512, overlap=50)

# 2. Create embeddings and store in vector DB
vectorstore = VectorStore.from_documents(chunks, embedding_model)

# 3. Create retrieval chain
retriever = vectorstore.as_retriever(search_kwargs={"k": 5})
qa_chain = RetrievalQA(llm=LLM("gpt-4"), retriever=retriever)

# 4. Query
answer = qa_chain.run("What are the side effects of Drug X?")
```

---

## Evaluation Metrics for RAG

| Metric | Measures |
|---|---|
| **Context Relevance** | Are retrieved chunks actually relevant? |
| **Faithfulness** | Does the answer stick to the retrieved context? |
| **Answer Relevance** | Does the answer address the user's question? |
| **Groundedness** | Can every claim be traced to a source? |

Popular evaluation frameworks: **RAGAS**, **TruLens**, **DeepEval**

---

## Key Concepts

| Term | Meaning |
|---|---|
| **Dense retrieval** | Use neural embeddings for similarity search |
| **Sparse retrieval** | Use TF-IDF / BM25 keyword matching |
| **Hybrid search** | Combine dense + sparse for better recall |
| **Reranking** | Re-score retrieved docs with a cross-encoder |
| **Agentic RAG** | LLM decides when/what to retrieve dynamically |
| **GraphRAG** | Use knowledge graphs instead of flat documents |
| **Multimodal RAG** | Retrieve images, tables, and text together |

---

## 🔗 Resources
- [RAG Original Paper (Lewis et al.)](https://arxiv.org/abs/2005.11401)
- [Self-RAG Paper](https://arxiv.org/abs/2310.11511)
- [LangChain RAG Tutorial](https://python.langchain.com/docs/tutorials/rag/)
- [LlamaIndex Documentation](https://docs.llamaindex.ai/)
- [RAGAS Evaluation Framework](https://docs.ragas.io/)

---

*Day 8 of the AI/ML Foundations series — RAG is the bridge between static LLMs and dynamic, trustworthy AI systems. 🚀*
