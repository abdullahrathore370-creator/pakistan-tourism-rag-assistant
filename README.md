# Pakistan Tourism RAG Assistant

An AI-powered Retrieval-Augmented Generation (RAG) assistant for exploring tourism information about Pakistan.

The system ingests tourism information from PDF documents, stores the knowledge as vector embeddings in Supabase, retrieves relevant information through semantic search, and uses an AI Agent to generate conversational responses.

## Features

- PDF-based knowledge ingestion
- City-level document chunking
- Vector embeddings
- Semantic similarity search
- Supabase vector database
- AI Agent-based responses
- n8n workflow automation
- Text-based conversational interface
- Voice interaction through the frontend
- Single workflow for ingestion and retrieval

## Architecture

```text
                    ┌─────────────────────┐
                    │      Frontend       │
                    │  Text / Voice Chat  │
                    │     PDF Upload      │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │        n8n          │
                    │   Webhook Trigger   │
                    └──────────┬──────────┘
                               │
                         ┌─────┴─────┐
                         │   Switch  │
                         └─────┬─────┘
                               │
              ┌────────────────┴────────────────┐
              │                                 │
              ▼                                 ▼
       ┌───────────────┐                 ┌───────────────┐
       │   Ingestion   │                 │     Chat      │
       │    Pipeline   │                 │    Pipeline   │
       └───────┬───────┘                 └───────┬───────┘
               │                                 │
               ▼                                 ▼
       ┌───────────────┐                 ┌───────────────┐
       │ Extract PDF   │                 │   AI Agent    │
       └───────┬───────┘                 └───────┬───────┘
               │                                 │
               ▼                                 ▼
       ┌───────────────┐                 ┌───────────────┐
       │ City Chunks   │                 │   Supabase    │
       └───────┬───────┘                 │ Vector Search │
               │                         └───────┬───────┘
               ▼                                 │
       ┌───────────────┐                         │
       │   Embeddings  │◄────────────────────────┘
       └───────┬───────┘
               │
               ▼
       ┌───────────────┐
       │    Supabase   │
       │ Vector Store  │
       └───────────────┘
