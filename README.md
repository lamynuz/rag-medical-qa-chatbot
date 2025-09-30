# RAG-based Medical Q&A Chatbot

This project demonstrates a **Retrieval-Augmented Generation (RAG)** system for a medical question-answering chatbot. The system uses a local Large Language Model (LLM) to answer questions based on a provided knowledge base of PDF documents, ensuring factual and context-aware responses without relying on external APIs. It uses LangChain as the framework. The model has been chosen for the purpose on running this project on an Apple M1 8GB RAM.
---

### Key Features 🔍

-   **Document Loading**: Loads medical information from multiple PDF files using `PyPDFLoader` and `DirectoryLoader`.
-   **Text Splitting**: Chunks the raw text from the PDFs into smaller, manageable pieces using `RecursiveCharacterTextSplitter`.
-   **Hugging Face Embeddings**: Converts the text chunks into vector embeddings using a HuggingFace model (`sentence-transformers/all-MiniLM-L6-v2`).
-   **FAISS Vector Store**: Stores the generated embeddings in a local FAISS database for fast and efficient semantic search.
-   **Local LLM Integration**: Uses a local `Llama-3.2-3B-Instruct-Q2_K.gguf` model via `LlamaCpp` to generate answers, keeping the entire process offline and private.
-   **Retrieval Chain**: Constructs a RAG chain that first retrieves the most relevant document chunks based on a user's query and then uses the LLM to formulate a precise answer, adhering strictly to the provided context.

---

### How It Works

The notebook outlines a standard RAG pipeline:

1.  **Data Ingestion**: It reads all PDF files from the `data/` directory.
2.  **Chunking**: The text from the documents is split into overlapping chunks of a specified size.
3.  **Embedding**: These chunks are transformed into numerical vectors (embeddings).
4.  **Vector Store**: The embeddings are stored in a local FAISS index.
5.  **Retrieval**: When a question is asked, the system uses the vector store to find the most relevant document chunks.
6.  **Generation**: The retrieved chunks are passed to the local LLM, which generates a concise answer based *only* on the provided context. The model is instructed to say it doesn't know if the answer isn't in the context, preventing hallucinations.

---

### Pre-requisites:

1. For full project functionality, you'll need to download the specified local LLM and place it in the appropriate `models/` directory.
2. Have a HUGGINGFACEHUB_API_TOKEN in the .env file
3. PDFs in the `data/` directory. Example: The Gale encyclopedia of medicine
