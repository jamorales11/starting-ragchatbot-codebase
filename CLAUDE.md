# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a RAG (Retrieval-Augmented Generation) system for querying course materials. The application uses ChromaDB for vector storage, Anthropic's Claude for AI generation, and provides a web interface for interaction.

## Development Commands

### Setup and Installation
```bash
# Install dependencies
uv sync

# Set up environment variables
cp .env.example .env
# Then edit .env to add your ANTHROPIC_API_KEY
```

### Running the Application
```bash
# Quick start (recommended)
chmod +x run.sh
./run.sh

# Manual start
cd backend && uv run uvicorn app:app --reload --port 8000
```

### Access Points
- Web Interface: `http://localhost:8000`
- API Documentation: `http://localhost:8000/docs`

## Architecture

### Backend Structure (`backend/`)
- **`app.py`**: FastAPI application entry point, API endpoints, and static file serving
- **`rag_system.py`**: Main orchestrator that coordinates all RAG components
- **`vector_store.py`**: ChromaDB integration for vector storage and semantic search
- **`ai_generator.py`**: Anthropic Claude API integration for response generation
- **`document_processor.py`**: Document parsing and chunking logic
- **`session_manager.py`**: User session and conversation history management
- **`search_tools.py`**: Tool management system for search capabilities
- **`models.py`**: Pydantic models and data structures
- **`config.py`**: Configuration management and environment variables

### Frontend Structure (`frontend/`)
- **`index.html`**: Main web interface
- **`script.js`**: Client-side JavaScript for API interaction
- **`style.css`**: UI styling

### Key Dependencies
- **ChromaDB 1.0.15**: Vector database for semantic search
- **Anthropic 0.58.2**: Claude API integration
- **Sentence Transformers 5.0.0**: Text embeddings
- **FastAPI 0.116.1**: Web framework
- **Uvicorn 0.35.0**: ASGI server

## Environment Configuration

Required environment variables in `.env`:
- `ANTHROPIC_API_KEY`: Your Anthropic API key for Claude access

## Data Flow

1. Documents are processed and chunked by `DocumentProcessor`
2. Text embeddings are created and stored in ChromaDB via `VectorStore`
3. User queries are embedded and used for semantic search
4. Retrieved context is sent to Claude via `AIGenerator` for response generation
5. Session history is maintained through `SessionManager`

## Important Notes

- The application automatically loads documents from the `docs/` directory on startup
- ChromaDB data is stored in `backend/chroma_db/` (gitignored)
- The system uses uv as the Python package manager
- For Windows users, Git Bash is recommended for running commands
- Always use uv to run the server, do not use pip
- use uv to run Python files