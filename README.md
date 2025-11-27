# 📘 Notion-Workspace-RAG-System
Retrieval-Augmented Generation on Entire Notion Workspace
Built with Notion API + OpenAI + ChromaDB

🚀 # Overview
This project turns your entire Notion Workspace into a private AI knowledge base, enabling Retrieval-Augmented Generation (RAG) without using ChatGPT Team/Enterprise.

It automatically:

Fetches all pages/subpages from a Notion workspace root

Extracts structured page text

Splits text into optimal chunks

Generates OpenAI embeddings

Stores embeddings in a persistent ChromaDB vector store

Answers your questions using top-K retrieved chunks

All data is local.
No external services.
No vendor lock-in.

flowchart TD

    subgraph Notion Workspace
        A1[Page 1]
        A2[Page 2]
        A3[Page 3]
        A4[Database Items ...]
    end

    subgraph Notion API Layer
        B1[Integration Token Auth]
        B2[Fetch Page Blocks]
    end

    subgraph Local Processing
        C1[Text Extractor]
        C2[Text Splitter<br/>Chunking 500-800 chars]
        C3[Metadata Builder]
    end

    subgraph Vector Database (Chroma)
        D1[Embedding<br/>text-embedding-3-small]
        D2[Upsert Chunks]
        D3[Query Similarity Search]
    end

    subgraph LLM Reasoning (GPT)
        E1[Build RAG Prompt]
        E2[Generate Final Answer]
    end

    User[(You)]
    
    User -->|Ask Question| E1
    E1 -->|Needs Context| D3
    D3 -->|Return Top-K Chunks| E1
    Notion Workspace --> B1 --> B2 --> C1 --> C2 --> C3 --> D2
