# MedRAG-AutoGen: Agentic RAG for Reliable Medical Question Answering

Welcome to **MedRAG-AutoGen**, a cutting-edge project that integrates **Retrieval-Augmented Generation (RAG)** with **Agentic AI** to ensure **accurate, reliable, and context-aware answers** to user questions  particularly in the domain of **medical documents and diabetes medication information**.

---

##  Project Vision

The motivation behind this project is to **elevate standard RAG pipelines** by adding a layer of **agentic intelligence**, where multiple intelligent agents collaborate to:

- **Retrieve**, **rank**, and **validate** document snippets,
- **Filter irrelevant or low-confidence content**, and
- **Assemble final answers with a focus on correctness, relevance, and completeness**.

This is especially important in **medical domains**, where misinformation can have serious consequences, but it can be used for other fields.

---

## 🧠 Architecture Overview

```mermaid
flowchart TD
    Q[User Query]
    Q --> E[Encode Query with BGE-small]
    E --> S[FAISS Search]
    S --> C[Candidate Chunks]
    C --> R[Re-Ranker Agent]
    R --> V[Validator Agent]
    V --> F[Filtered Chunks (Validated)]
    F --> A[Final Answer Assembly]
```

## Key Components
1.  RAG Base
- Embedding Model: bge-small (sentence-transformers) for efficient, high-quality vector representations.

- Vector Store: FAISS index to search a large set of document chunks.

- Document Chunking: Fine-grained splitting to maximize retrieval relevance.

2. Agentic Enhancement
- Re-Ranker Agent: Given a user query and multiple document chunks, it reorders them based on relevance.

- Validator Agent: For each top chunk, this agent decides:

- Does it answer the question?

- Is the information medically relevant and trustworthy?

- Responds with "YES" - reason or "NO" - reason.

3. Accuracy Pipeline
Only validated chunks are included in the final answer.

The system explicitly rejects vague, partial, or non-relevant chunks using agent validation.

This dramatically reduces hallucination risk — a common RAG issue.

```bash
query = "What are Meglitinides medicines and how they work?"

1. Chunks retrieved from FAISS
2. Re-ranked by relevance
3. Validated by agent (e.g., "YES - mentions repaglinide and insulin secretion")
4. Final answer built from only validated chunks
```
## Inference Engine
This project uses Ollama to run the language models locally with GPU acceleration.

- Model Used: deepseek-r1:70b

- Usage: Both the re_ranker_agent and validator_agent run on deepseek-r1:70b via the ollama_client.

- Why Ollama? It allows for fast, secure, and customizable local LLM inference perfect for handling sensitive or regulated content like medical text.
- 
 ## Sample Output
```bash
 Final Combined Answer based on user query:

Meglitinides are rapid-acting insulin secretagogues such as repaglinide (Prandin) and nateglinide (Starlix).
They stimulate the pancreas to release insulin in response to meals.
Combination drugs like PrandiMet combine repaglinide with metformin for dual action.
```
## Innovation Highlights
- Agentic validation ensures answer relevance and factuality.

- Multi-stage reasoning pipeline combining search, reasoning, and filtering.

- Tailored for medical question answering, but easily adaptable to any domain.

- Designed for high performance using ollama + GPU inference.

## Future Ideas
- Add explanation agent to summarize why a chunk is relevant.

- Integrate Hallucination Detection.

- Support multi-document reasoning over PDF collections.

## Acknowledgements
Built with ❤️ using:

- [LangChain / AutoGen agents]

- [FAISS]

- [bge-small embeddings]

- [Ollama for LLM runtime]

- And your drive to build accurate AI, not just smart AI.

## License
MIT License — please cite or link back if you build on this project.

