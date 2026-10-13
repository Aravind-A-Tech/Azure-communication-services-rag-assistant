# Azure Communication Services Documentation Assistant

A Retrieval-Augmented Generation (RAG) project that enables question answering over Azure Communication Services documentation using Python, Ollama, and FAISS.

The project retrieves relevant documentation chunks and uses a locally running Large Language Model (LLM) to generate context-grounded answers to user questions.

## Project Overview

Finding relevant information in technical documentation can be time-consuming. This project explores how Retrieval-Augmented Generation can make Azure documentation easier to search and understand through natural-language questions.

The current implementation focuses on **Azure Communication Services (ACS)** documentation, with the potential to extend the pipeline to other Azure services.

## Architecture

```text
Microsoft Learn Documentation
            |
            v
    Document Downloader
            |
            v
  Markdown Documents
            |
            v
      Text Chunking
            |
            v
  Ollama Embedding Model
    (nomic-embed-text)
            |
            v
       FAISS Index
            |
            v
      User Question
            |
            v
    Query Embedding
            |
            v
  Relevant Chunk Retrieval
            |
            v
   Context + User Question
            |
            v
       Ollama LLM
        (llama3.2)
            |
            v
      Generated Answer
```

## Features

- **Documentation ingestion:** Downloads Azure Communication Services documentation from Microsoft Learn.
- **Markdown processing:** Cleans and stores documentation as Markdown files.
- **Text chunking:** Splits documents into smaller, overlapping chunks for retrieval.
- **Embedding generation:** Generates vector embeddings using Ollama's `nomic-embed-text` model.
- **Vector search:** Uses FAISS for similarity-based retrieval of relevant documentation.
- **Context-grounded answers:** Uses the `llama3.2` model to answer questions using retrieved context.
- **Local execution:** Runs the embedding and language models locally through Ollama, without requiring a paid LLM API.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application logic and document processing |
| Jupyter Notebook | Development and experimentation |
| Requests | Downloading web content |
| Beautiful Soup | HTML parsing and link extraction |
| tqdm | Download progress tracking |
| Ollama | Local model execution |
| nomic-embed-text | Text embedding generation |
| FAISS | Vector similarity search |
| NumPy | Numerical operations on embeddings |

## Project Structure

```text
Azure-communication-services-rag-assistant/
├── Notebooks/
│   ├── 01_download_azure_docs.ipynb
│   └── 02_build_rag_chatbot.ipynb
├── docs/
│   └── Azure_Communication_Services/
├── faiss_index/
├── README.md
├── requirements.txt
└── .gitignore
```

- `01_download_azure_docs.ipynb`: Discovers documentation links, downloads Markdown content, and saves the files locally.
- `02_build_rag_chatbot.ipynb`: Loads the documents, creates chunks and embeddings, builds the FAISS index, and runs the question-answering loop.
- `docs/`: Stores downloaded documentation.
- `faiss_index/`: Stores the generated vector index and chunk metadata.

Generated documentation and index files may be excluded from Git and recreated locally.

## Prerequisites

- Python 3.10 or a compatible version
- Jupyter Notebook or VS Code with Jupyter support
- Ollama installed and running
- Sufficient local memory and disk space for the selected models and document collection

## Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/Aravind-A-Tech/Azure-communication-services-rag-assistant.git
cd Azure-communication-services-rag-assistant
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows using Git Bash:

```bash
source .venv/Scripts/activate
```

### 3. Install Python dependencies

```bash
pip install -r requirements.txt
```

### 4. Download the Ollama models

Make sure Ollama is installed and running, then execute:

```bash
ollama pull nomic-embed-text
ollama pull llama3.2
```

### 5. Download the documentation

Open and run all required cells in:

`Notebooks/01_download_azure_docs.ipynb`

The notebook downloads and stores the documentation under:

`docs/Azure_Communication_Services/`

Run the notebook from the project root or configure its working directory to point to the project root.

### 6. Build the RAG pipeline

Open and run:

`Notebooks/02_build_rag_chatbot.ipynb`

The notebook processes the downloaded documents, generates embeddings, creates the FAISS index, and prepares the retrieval pipeline.

### 7. Ask questions

Run the final cells in Notebook 2 and enter questions at the prompt.

Example questions:

- How do I configure Azure Communication Services?
- How do I generate access tokens?
- What is call automation in Azure Communication Services?

Enter `exit` to stop the interactive session.

## How Retrieval-Augmented Generation Works

1. **Ingestion:** Documentation is downloaded and stored locally.
2. **Chunking:** Long documents are divided into smaller text segments with overlap.
3. **Embedding:** Each chunk is converted into a numerical vector.
4. **Indexing:** The vectors are added to a FAISS index for efficient similarity search.
5. **Retrieval:** A user's question is embedded, and similar document chunks are retrieved.
6. **Generation:** The retrieved context and question are passed to the LLM to generate an answer.

This approach allows the model to use relevant documentation instead of relying solely on information learned during training.

## Current Limitations

- The current implementation supports Azure Communication Services documentation only.
- The embedding model and LLM must be available through a running Ollama installation.
- The FAISS index must be generated locally before retrieval can work.
- The current retrieval process uses vector similarity search without a separate reranking stage.
- Answers depend on the quality and relevance of the retrieved documentation.
- The implementation does not yet provide a web interface or production deployment.

## Future Enhancements

- Extend document ingestion to additional Azure services.
- Improve chunking and retrieval strategies.
- Include document source references in generated answers.
- Support incremental documentation updates.
- Add evaluation metrics for retrieval quality and answer accuracy.
- Develop a web interface or REST API.
- Explore cloud deployment options.

## Learning Objectives

This project demonstrates practical implementation of:

- Retrieval-Augmented Generation (RAG)
- Document ingestion and preprocessing
- Text embeddings and vector representations
- Vector similarity search using FAISS
- Local LLM integration with Ollama
- Context-based question answering
- Python development using Jupyter Notebooks

## Author

**Aravind A**

GitHub: [Aravind-A-Tech](https://github.com/Aravind-A-Tech)

---

*This project is intended for learning and experimentation with RAG-based document assistants.*
