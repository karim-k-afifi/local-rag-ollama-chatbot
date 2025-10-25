# Local RAG Chatbot for Insurellm 🤖

## Overview 📝

This project implements a Retrieval-Augmented Generation (RAG) chatbot designed to answer questions about **Insurellm**, an insurance tech company. It runs entirely locally, using **Ollama** to serve language models (like Llama 3.2), **ChromaDB** as a vector store, and **Sentence Transformers** for embeddings.

The chatbot leverages documents stored in the `knowledge-base` directory, which contains information about Insurellm's company details, products, employees, and contracts. Users can interact with the chatbot through a **Gradio** web interface. This version utilizes the official `openai` Python library to communicate with Ollama's OpenAI-compatible API.

## Features ✨

* **Local & Private:** Runs entirely on your machine. Your data stays local. 🏠
* **Insurellm Knowledge:** Answers questions specifically about Insurellm based on provided documents.
* **RAG Implementation:** Retrieves relevant document snippets before generating an answer. 🔍
* **Chat History:** Remembers the context of the current conversation session. 🧠
* **Local LLMs:** Powered by Ollama (e.g., Llama 3.2).
* **Local Embeddings:** Uses Sentence Transformers for document embeddings.
* **Vector Storage:** Employs ChromaDB for efficient document chunk storage and retrieval.
* **Web Interface:** Simple and interactive chat UI provided by Gradio. 💬
* **(Optional) Visualization:** Includes t-SNE plots to visualize the document embedding space. 📊

## Prerequisites 🛠️

* **Python:** Version 3.10 or 3.11 recommended.
* **Conda (or venv):** For managing Python environments.
* **Ollama:** Installed and running locally. Ensure the model specified in `.env` is pulled (e.g., `ollama pull llama3.2`). * **Git:** (Optional) For version control.

## Setup Instructions ⚙️

1.  **Clone the Repository (if applicable):**
    ```bash
    git clone <your-repo-url>
    cd <your-repo-name>
    ```
    *(Or create a project folder and place your `.ipynb` / `.py` file inside).*

2.  **Create and Activate Conda Environment:**
    *Use the environment created previously or make a new one.*
    ```bash
    # Create environment (if you haven't already)
    # conda create -n rag_solution python=3.11 -y 
    
    # Activate the environment
    conda activate rag_solution 
    ```

3.  **Install Dependencies:**
    *Ensure you install the fixed `pydantic` version first.*
    ```bash
    pip install pydantic==2.11.0
    pip install gradio openai langchain-core langchain-community langchain-text-splitters langchain-chroma chromadb sentence-transformers huggingface-hub scikit-learn plotly numpy python-dotenv ipykernel ipywidgets
    ```
    *(Consider creating a `requirements.txt` file for easier installation: `pip install -r requirements.txt`)*

4.  **Configure Environment Variables:**
    * Rename `.env.example` to `.env`.
    * Edit `.env` if needed. Defaults should work for a standard local Ollama setup. **Ensure `OLLAMA_URL` includes `/v1`**.
        ```dotenv
        OLLAMA_URL=http://localhost:11434/v1
        OLLAMA_MODEL=llama3.2:latest 
        OLLAMA_API_KEY=ollama 
        ```

5.  **Prepare Knowledge Base Documents:**
    * Ensure you have a `knowledge-base` folder in your project root.
    * Inside `knowledge-base`, create subfolders matching your data categories:
        * `company` (containing files like `about.md`, `overview.md`, `careers.md`)
        * `contracts` (containing individual contract `.md` files)
        * `employees` (containing individual employee profile `.md` files)
        * `products` (containing product description `.md` files)
    * Place your Markdown (`.md`) documents into the corresponding subfolders. 
## Running the Chatbot ▶️

1.  **Ensure Ollama is Running:**
    Open a *separate* terminal and run:
    ```bash
    ollama serve
    ```
    *(Wait for the server to start).*

2.  **Activate Your Conda Environment:**
    In your project terminal:
    ```bash
    conda activate rag_solution
    ```

3.  **Run the Jupyter Notebook or Python Script:**
    * **Using Jupyter Lab:**
        ```bash
        jupyter lab
        ```
        Then open your `.ipynb` file and run all cells.
    * **Using a Python Script (`.py`):**
        ```bash
        python your_script_name.py 
        ```

4.  **Access the Gradio Interface:**
    * The script output will provide a local URL (e.g., `http://127.0.0.1:7860`).
    * Open this URL in your web browser to start chatting! 🎉

## Example Questions 🤔

You can ask questions like:

* "Tell me about Insurellm."
* "Who founded Insurellm?"
* "What products does Insurellm offer?"
* "Summarize the contract with GreenValley Insurance."
* "Who is Alex Chen?"
* "How many employees does Insurellm have?"

## Project Structure 📁

````

your-project-folder/
├── local\_rag\_chatbot.ipynb   \# Or your .py script
├── knowledge-base/           \# Folder for your Insurellm documents
│   ├── company/
│   │   ├── about.md
│   │   └── overview.md
│   ├── contracts/
│   │   └── Contract with Apex Reinsurance.md
│   ├── employees/
│   │   └── Alex Chen.md
│   └── products/
│       └── Carllm\_details.md
├── vector\_db/                \# Created automatically by ChromaDB
├── .env                      \# Local environment variables (DO NOT COMMIT)
├── .env.example              \# Example environment variables template
├── .gitignore                \# Files/folders for Git to ignore
└── README.md                 \# This file

```

## Notes 📝

* The first time you run the script, it will download the Sentence Transformer embedding model (approx. 90MB) and build the ChromaDB vector store, which might take a minute depending on the number of documents.
* The current script deletes and rebuilds the `vector_db` on each run. You can modify the `create_vector_store` function to load an existing database if preferred.
```