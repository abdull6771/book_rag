# Retrieval-Augmented Generation (RAG) with LangChain, Pinecone, and ChromaDB

This repository contains a Python-based **Retrieval-Augmented Generation (RAG)** system for processing PDF documents, as detailed in the Jupyter notebook `rag_langchain_book_pdf.ipynb`. The system extracts text from a PDF (`book.pdf`), creates embeddings, stores them in **Pinecone** and **ChromaDB**, and answers queries using **LangChain** and a local **Ollama** LLM (`llama3`). It also compares the performance of Pinecone and ChromaDB for retrieval tasks.

This project is ideal for developers, data scientists, and AI enthusiasts looking to build or experiment with RAG pipelines for document-based question answering.

---

## Features

- **PDF Processing**: Extracts and chunks text from `book.pdf` using `PyPDFLoader` and `RecursiveCharacterTextSplitter`.
- **Embedding Creation**: Converts text chunks into 384-dimensional embeddings using Hugging Face’s `all-MiniLM-L6-v2`.
- **Vector Storage**: Stores embeddings in Pinecone (cloud-based) and ChromaDB (local) for efficient similarity search.
- **RAG Pipeline**: Uses LangChain’s `RetrievalQA` chain with an Ollama-hosted `llama3` LLM to answer queries.
- **Performance Comparison**: Evaluates Pinecone and ChromaDB based on response time and setup complexity.
- **Cleanup**: Includes scripts to delete Pinecone indexes and ChromaDB collections to free resources.

---

## Prerequisites

To run this project, ensure you have:

- A PDF file named `book.pdf` in the working directory.
- A Pinecone account with an API key (free tier available).
- Ollama installed locally with the `llama3` model (`ollama pull llama3`).
- Python 3.8 or higher.
- Required libraries (see installation below).

---

## Installation

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/abdull6771/book_rag.git
   cd book_rag
   ```

2. **Set Up a Virtual Environment** (optional but recommended):

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies**:

   ```bash
   pip install -r requirements.txt
   ```

   Or install directly:

   ```bash
   pip install langchain langchain-community langchain-ollama pinecone-client chromadb sentence-transformers pypdf
   ```

4. **Configure Pinecone**:

   - Sign up for a Pinecone account and obtain your API key and environment (e.g., `us-west1-gcp`).
   - Update the notebook with your credentials:

     ```python
     os.environ['PINECONE_API_KEY'] = 'your-pinecone-api-key'
     PINECONE_ENV = 'your-pinecone-environment'
     ```

5. **Set Up Ollama**:

   - Install Ollama following the official instructions.
   - Pull the `llama3` model:

     ```bash
     ollama pull llama3
     ```

6. **Prepare the PDF**:

   - Place your `book.pdf` file in the repository’s root directory.

---

## Usage

1. **Open the Notebook**: Launch Jupyter Notebook or JupyterLab:

   ```bash
   jupyter notebook rag_langchain_book_pdf.ipynb
   ```

2. **Run the Notebook**:

   - Execute the cells sequentially to:
     - Load and preprocess `book.pdf`.
     - Create and store embeddings in Pinecone and ChromaDB.
     - Set up RAG pipelines.
     - Test queries and compare Pinecone vs. ChromaDB performance.
     - Clean up resources.
   - Modify the sample queries in Step 6 to match your `book.pdf` content (e.g., “What is the main theme of the book?”).

3. **Customize Queries**: Edit the `queries` list in the notebook to ask specific questions about your PDF:

   ```python
   queries = [
       "What is the main topic of the book?",
       "Summarize the key points from chapter one.",
       "What examples are provided in the book?"
   ]
   ```

4. **Clean Up**: The final cell deletes the Pinecone index and ChromaDB collection to avoid unnecessary costs or storage.

---

## Project Structure

```
your-repo-name/
│
├── rag_langchain_book_pdf.ipynb  # Main Jupyter notebook with RAG implementation
├── book.pdf                     # Your input PDF (not included; add your own)
├── chroma_db/                   # Directory for ChromaDB data (created automatically)
├── requirements.txt             # Python dependencies
└── README.md                    # This file
```

---

## Notes and Tips

- **Large PDFs**: If `book.pdf` is large, adjust `chunk_size` (e.g., 500) or `chunk_overlap` (e.g., 200) in the notebook to balance retrieval accuracy and performance.
- **Scanned PDFs**: If your PDF contains images, use OCR tools like `pytesseract` with `pdf2image`. Contact me for a modified notebook with OCR support.
- **Performance Tuning**: Increase `k` in `search_kwargs` (e.g., `k=5`) to retrieve more chunks for complex queries.
- **Advanced RAG**: Experiment with prompt templates, hybrid search, or reranking to improve answer quality.
- **Deployment**: Build a UI with Chainlit or deploy the pipeline as an API.

---

## Pinecone vs. ChromaDB

| **Feature** | **Pinecone** | **ChromaDB** |
| --- | --- | --- |
| **Type** | Cloud-based, managed | Open-source, self-hosted |
| **Scalability** | Highly scalable, production-ready | Limited by local hardware |
| **Setup** | Requires account and API key | Easy local setup |
| **Cost** | Free tier (100K vectors); paid for scale | Free |
| **Performance** | \~500ms for small indexes | Slower for large datasets; hardware-based |
| **Use Case** | Production apps, high throughput | Prototyping, local development |

**Recommendation**:

- Use **Pinecone** for scalable, production-grade applications.
- Use **ChromaDB** for prototyping or self-hosted environments.

---

## Contributing

Contributions are welcome! To contribute:

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a pull request.

Please include tests and documentation for new features.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.

---

## Acknowledgments

- LangChain for the RAG framework.
- Pinecone and ChromaDB for vector database support.
- Ollama for local LLM inference.
- Hugging Face for embedding models.

---

## Contact

For questions, issues, or suggestions, open an issue on GitHub or reach out via your-email@example.com. If you need help with OCR, large PDFs, or deployment, let me know!

Happy coding!
