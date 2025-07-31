# RAG with Ollama and Qwen3

This project implements a Retrieval-Augmented Generation (RAG) system using Ollama with the Qwen3 model, ChromaDB for vector storage, and LangChain for orchestration.

## Features

- **Local Model**: Uses Ollama with Qwen3 to run the LLM model locally
- **Vector Database**: ChromaDB for embedding storage and search
- **PDF Processing**: Automatically loads and processes PDF documents
- **Simple Interface**: Easy-to-use Python script for document queries

## Prerequisites

- Python 3.8 or higher
- macOS, Linux or Windows
- At least 8GB RAM (16GB recommended for better performance)

## Installation and Setup

### 1. Install Ollama

#### On macOS:

```bash
# Download and install from the official site
curl -fsSL https://ollama.ai/install.sh | sh

# Or using Homebrew
brew install ollama
```

#### On Linux:

```bash
curl -fsSL https://ollama.ai/install.sh | sh
```

#### On Windows:

Download the installer from [https://ollama.ai/download](https://ollama.ai/download)

### 2. Start the Ollama Service

```bash
# Start Ollama (runs as a background service)
ollama serve
```

### 3. Install the Qwen3 Model

```bash
# Install the Qwen3 model (this may take several minutes)
ollama pull qwen2.5:7b

# Verify the model is installed
ollama list
```

### 4. Clone the Repository

```bash
git clone https://github.com/Emilf16/RAG-WITH-OLLAMA-QWEN3.git
cd RAG-WITH-OLLAMA-QWEN3
```

### 5. Create Python Virtual Environment

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate

# On Windows:
# venv\Scripts\activate
```

### 6. Install Python Dependencies

```bash
# Install required dependencies
pip install langchain-community
pip install langchain-ollama
pip install langchain-core
pip install langchain-text-splitters
pip install chromadb
pip install pypdf
pip install python-dotenv

# Or create a requirements.txt and install everything at once:
pip install -r requirements.txt
```

### 7. Configure Environment Variables (Optional)

```bash
# Create .env file if you need specific configurations
echo "OLLAMA_BASE_URL=http://localhost:11434" > .env
```

## Usage

### 1. Prepare Your Documents

Place your PDF files in the `data/` folder. The script is configured to process the `documento_prueba.pdf` file by default, which contains example information about the RAG system.

### 2. Run the Script

```bash
# Make sure Ollama is running
ollama serve

# In another terminal, run the RAG script
python rag_local.py
```

### 3. Make Queries

The script will load the documents, create the embeddings, and allow you to ask questions about the PDF content.

## Project Structure

```
RAG-WITH-OLLAMA-QWEN3/
├── README.md                 # This file
├── rag_local.py             # Main RAG script
├── requirements.txt         # Python dependencies
├── .gitignore              # Files to ignore in Git
├── .env                    # Environment variables (optional)
├── data/                   # Folder for PDF files
│   └── documento_prueba.pdf # Example document with RAG content
├── chroma_db/              # Vector database (auto-generated)
└── venv/                   # Python virtual environment
```

## Useful Ollama Commands

```bash
# List installed models
ollama list

# Run a model interactively
ollama run qwen2.5:7b

# Update a model
ollama pull qwen2.5:7b

# Remove a model
ollama rm qwen2.5:7b

# View system information
ollama ps
```

## Troubleshooting

### Ollama won't connect

```bash
# Verify Ollama is running
ps aux | grep ollama

# Restart the service
ollama serve
```

### Insufficient memory error

- Make sure you have at least 8GB of available RAM
- Consider using a smaller model if you have memory limitations

### ChromaDB issues

```bash
# Delete the database and allow it to regenerate
rm -rf chroma_db/
```

### Python dependencies

```bash
# If there are conflicts, reinstall in a clean environment
deactivate
rm -rf venv/
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Customization

### Change the Model

Edit `rag_local.py` and change the model name in the `ChatOllama` configuration.

### Process Different PDFs

Change the `PDF_FILENAME` variable in `rag_local.py` to process different documents.

### Adjust Embedding Parameters

Modify the `RecursiveCharacterTextSplitter` parameters for different chunk sizes.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-functionality`)
3. Commit your changes (`git commit -am 'Add new functionality'`)
4. Push to the branch (`git push origin feature/new-functionality`)
5. Create a Pull Request

## License

This project is under the MIT License. See the `LICENSE` file for more details.

## References

- [Ollama Documentation](https://ollama.ai/docs)
- [LangChain Documentation](https://python.langchain.com/)
- [ChromaDB Documentation](https://docs.trychroma.com/)
- [Qwen Model Information](https://huggingface.co/Qwen)
