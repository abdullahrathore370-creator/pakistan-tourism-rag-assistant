# Pakistan Tourism RAG Assistant

A Retrieval-Augmented Generation (RAG) assistant built to provide information about tourism in Pakistan using a dedicated tourism knowledge base.

The application allows users to ask questions about Pakistani cities, attractions, historical places, food, landmarks, culture, and notable people. Instead of relying only on the model's general knowledge, the system retrieves relevant information from the stored tourism documents before generating a response.

## What I Built

The project consists of a frontend connected to an n8n workflow. The workflow handles both document ingestion and user queries through a single webhook.

Tourism information is provided through PDF documents. The PDF is processed, extracted into text, divided into city-level chunks, converted into vector embeddings, and stored in Supabase.

When a user asks a question, the AI Agent searches the Supabase vector store for relevant information and uses the retrieved content to generate the response.

The frontend also supports voice interaction, allowing the user to speak a question and receive a spoken response.

## How It Works

The application has two main paths inside the same n8n workflow.

### Document Ingestion

1. A tourism PDF is uploaded from the frontend.
2. The PDF is sent to the n8n webhook.
3. n8n extracts the text from the document.
4. The extracted content is divided into city-level chunks.
5. Embeddings are generated for the chunks.
6. The documents and embeddings are stored in Supabase.
7. The stored information becomes available for retrieval.

Each city is kept as a separate chunk so that information belonging to the same city remains together during retrieval.

### Question Answering

1. The user enters or speaks a question.
2. The frontend sends the question to the n8n webhook.
3. n8n routes the request to the chat path.
4. The AI Agent receives the user's question.
5. The AI Agent uses the Supabase vector store as a retrieval tool.
6. Relevant information is retrieved from the tourism knowledge base.
7. The retrieved information is used to generate the response.
8. The response is returned to the frontend.

## System Architecture

Frontend → n8n Webhook → Switch

### Ingestion

PDF Upload → Extract PDF → Create City Chunks → Gemini Embeddings → Supabase Vector Store

### Retrieval

User Query → Prepare Query → AI Agent → Supabase Vector Store → Retrieved Context → AI Response → Frontend

## Main Components

### Frontend

The frontend is a single-page application built with HTML, CSS, and JavaScript.

It provides:

- PDF upload
- Knowledge base ingestion
- Text chat
- Voice input
- Voice output
- Quick questions
- Chat responses

### n8n

n8n handles the complete backend workflow.

A single webhook receives both ingestion and chat requests. A Switch node checks the request type and sends it to the appropriate path.

The two request types are:

- `ingest` — used for PDF ingestion
- `chat` — used for user questions

### Supabase

Supabase is used as the vector database.

The tourism documents are stored together with their vector embeddings so that relevant information can be retrieved using semantic similarity.

### Google Gemini

Google Gemini is used for generating vector embeddings for the tourism knowledge base and user queries.

### AI Agent

The AI Agent processes the user's question and uses the Supabase vector store as a tool to retrieve relevant tourism information.

The agent is instructed to answer using information available in the knowledge base and avoid inventing information that is not supported by the retrieved documents.

## Knowledge Base

The knowledge base contains information about Pakistani cities and tourism-related topics.

The information can include:

- Famous locations
- Tourist attractions
- Historical places
- Food
- Landmarks
- Culture
- Notable people
- Historical information

The ingestion process keeps each city's information together as an individual chunk to preserve context during retrieval.

## Database

The project uses a Supabase `documents` table for storing the tourism content and embeddings.

The table contains:

- `id`
- `content`
- `metadata`
- `embedding`

The vector column is configured to store the embeddings generated for the knowledge base.

## Example Questions

The assistant can be used to ask questions such as:

- What are the historical highlights of Islamabad?
- What famous places can I visit in Lahore?
- What food is Karachi known for?
- What are the major attractions in Hunza?
- Tell me about the historical places in Peshawar.

## Technology Stack

| Technology | Purpose |
| --- | --- |
| n8n | Workflow automation and backend processing |
| Supabase | Vector database and document storage |
| Google Gemini | Text embeddings |
| AI Agent | Query processing and response generation |
| HTML | Frontend structure |
| CSS | Frontend styling |
| JavaScript | Frontend functionality |
| Webhooks | Frontend and n8n communication |
| RAG | Knowledge retrieval and context-based generation |

## Project Structure

- `frontend/` — frontend application
- `workflow/` — n8n workflow
- `knowledge-base/` — tourism knowledge base documents
- `README.md` — project documentation

## Project Goal

The goal of this project is to build a practical RAG application that connects document ingestion, embeddings, vector search, AI Agents, workflow automation, and a frontend into one working system.

The project demonstrates how information from documents can be converted into a searchable knowledge base and then used by an AI Agent to answer user questions based on retrieved context.

## Future Improvements

- Expand the knowledge base with more Pakistani cities
- Add more tourism documents
- Add multilingual support
- Improve retrieval accuracy
- Add conversation history
- Add personalized travel planning
- Add additional tourism data sources
- Deploy the frontend publicly

## Author

Muhammad Abdullah Shujaat

BS Software Engineering  
SZABIST University
