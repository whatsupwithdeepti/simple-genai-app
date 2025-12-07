# 📘 Simple GenAI App — LangChain + FAISS + Groq Llama

This project is a Simple GenAI Retrieval-Augmented Generation (RAG) App built using:

LangChain

Web scraping + text processing

HuggingFace embeddings

FAISS vector database

Groq Llama-3.1 (fast inference)

The notebook demonstrates the full GenAI workflow from data ingestion → vectorization → retrieval → LLM answering using LangChain’s modern components.

## 🚀 What This App Does

✔ Scrapes documentation from a live webpage

✔ Cleans & loads page content into LangChain Document format

✔ Splits content into overlapping chunks

✔ Converts text chunks into dense HuggingFace embeddings

✔ Stores vectors in a FAISS vector database

✔ Retrieves relevant chunks based on a user query

✔ Uses Groq Llama-3.1 to answer questions purely from retrieved context

✔ Demonstrates an end-to-end RAG pipeline inside a single notebook


## 🛠️ Tech Stack
🔹 Python + Jupyter Notebook

Main development environment.

🔹 LangChain

WebBaseLoader for scraping

RecursiveCharacterTextSplitter for chunking

create_retrieval_chain and create_stuff_documents_chain

Modern Runnable architecture

🔹 Embeddings

sentence-transformers/all-mpnet-base-v2 via HuggingFace

🔹 Vector Store

FAISS (fast, lightweight, in-memory ANN search)

🔹 LLM (Groq)

llama-3.1-8b-instant (super-fast inference)

Optional: llama-3.1-70b-versatile

## 📂 Project Structure
📁 simple-genai-app/
 ├── SimpleGenAIapp.ipynb   # Full RAG pipeline notebook
 └── README.md              # Project documentation

## ▶️ How to Run the Notebook
1. Clone the repository

```bash
git clone https://github.com/whatsupwithdeepti/simple-genai-app.git
cd simple-genai-app 
```

2. Install dependencies

3. Add environment variables

Create a .env file:

HF_TOKEN=your_huggingface_token

LANGCHAIN_API_KEY=your_langsmith_key

LANGCHAIN_PROJECT=your_project_name

GROQ_API_KEY=your_groq_key

4. Run the notebook
jupyter notebook SimpleGenAIapp.ipynb

## 🧠 Pipeline Overview
1️⃣ Data Ingestion
loader = WebBaseLoader(url)
documents = loader.load()

2️⃣ Chunking
text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=200)
chunks = text_splitter.split_documents(documents)

3️⃣ Embeddings
embeddings = HuggingFaceEmbeddings(model_name="sentence-transformers/all-mpnet-base-v2")

4️⃣ Vector DB
vectorstore = FAISS.from_documents(chunks, embeddings)

5️⃣ Retrieval Chain + LLM
retriever = vectorstore.as_retriever()
retrieval_chain = create_retrieval_chain(retriever, document_chain)

6️⃣ Ask a Question
response = retrieval_chain.invoke({"input": "Your question here"})

## 📝 Example Question

"LangSmith has two usage limits: what are they?"

The app retrieves relevant documentation, processes it, and generates an LLM-based answer only using the retrieved context.

## 📌 Future Improvements

Add Streamlit / Gradio UI

Store FAISS index locally for persistence

Add multi-page web scraping

Add reranking using BGE or Cohere reranker

Add evaluation metrics

Build this into a full RAG microservice

## 🤝 Contributing

Feel free to fork and improve the project. PRs are welcome!

## ⭐ Author

Built by Deepti Jethwani
A beginner-friendly GenAI RAG notebook for learning LangChain, FAISS, and Groq LLMs.
