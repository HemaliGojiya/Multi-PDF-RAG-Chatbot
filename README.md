📄 Multi-PDF RAG Chatbot

A Retrieval-Augmented Generation (RAG) chatbot that lets you upload and query multiple documents — PDF, DOCX, PowerPoint, and TXT — in a single conversational interface. Built with LangChain, FAISS vector search, OpenAI GPT-4o-mini, and Streamlit.


📌 Table of Contents


Overview
Architectural Diagram
Tools & Technologies
Project Structure
Setup & Installation
Environment Variables
Running the Application
How It Works
Features



Overview

Upload one or more documents and ask questions about their content in plain English. The app extracts, chunks, and embeds document text into a FAISS vector store, then retrieves the most relevant context for each query and passes it to GPT-4o-mini to generate accurate, grounded answers.


Architectural Diagram

Show Image

The pipeline works in two stages:

Ingestion: Documents → Unstructured parser → Text chunks → OpenAI Embeddings → FAISS Vector Store

Retrieval: User query → FAISS retriever → Relevant context → Prompt + Context → GPT-4o-mini → Response


Tools & Technologies

TechnologyPurposeLangChainRAG chain orchestrationOpenAI GPT-4o-miniLLM for answer generationOpenAI EmbeddingsText embedding for vector searchFAISSLocal vector store & similarity searchUnstructuredMulti-format document parsing (PDF, DOCX, PPTX, TXT)LangChain HubPre-built RAG prompt (rlm/rag-prompt)StreamlitInteractive chat UItiktokenToken-based text splitting


Project Structure

Multi-PDF-RAG-Chatbot/
│
├── rag.py                    # Main app — document loading, chunking, RAG chain, Streamlit UI
├── requirements.txt          # Project dependencies
├── .gitignore                # Files excluded from Git
├── Architectural_Diagram.png # System architecture diagram
└── README.md


Setup & Installation

Prerequisites


Python 3.10+
An OpenAI API key


Install Dependencies

bash# Create and activate a virtual environment (recommended)
python -m venv venv
source venv/bin/activate       # macOS/Linux
venv\Scripts\activate          # Windows

# Install dependencies
pip install -r requirements.txt


Note: unstructured[all-docs] installs all parsers for PDF, DOCX, PPTX, and TXT support. This may take a few minutes.




Environment Variables

Create a .env file in the root directory:

envOPENAI_API_KEY=your_openai_api_key_here


⚠️ Never commit your .env file to Git. It is already covered by .gitignore.




Running the Application

bashstreamlit run rag.py

Then open your browser at http://localhost:8501.


How It Works


Upload documents using the sidebar — supports PDF, DOCX, PPTX, and TXT files (multiple files at once).
Document parsing — unstructured extracts raw text from each file regardless of format.
Text chunking — text is split into overlapping chunks (1000 tokens, 300 overlap) using RecursiveCharacterTextSplitter.
Embedding — chunks are embedded using OpenAI Embeddings and stored in a local FAISS vector store.
Retrieval — when you ask a question, FAISS retrieves the most semantically relevant chunks.
Generation — the retrieved context and your question are passed to GPT-4o-mini via the rlm/rag-prompt template, which returns a grounded answer.



Features


📂 Multi-document support — upload and query multiple files simultaneously
🗂️ Multi-format parsing — handles PDF, DOCX, PPTX, and TXT via unstructured
🔍 Semantic search — FAISS vector store for fast, accurate retrieval
🧠 GPT-4o-mini — cost-efficient OpenAI model for high-quality responses
💬 Chat history — conversation context preserved across turns in the session
⚡ Simple setup — single Python file, minimal config, runs locally
