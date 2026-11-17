# 🩺 Medical RAG Chatbot

An AI-powered Medical Question Answering System built using **Retrieval-Augmented Generation (RAG)**, LangChain, Google Gemini, Pinecone, and Flask.

The chatbot retrieves relevant medical information from *The Gale Encyclopedia of Medicine (5th Edition, 2015)* and uses Google Gemini to generate context-aware answers based on the retrieved content.

---

## 📌 Project Overview

Medical information is widely available, but finding relevant and understandable information can be challenging. General-purpose AI chatbots may also generate answers that are not grounded in a specific medical reference.

This project addresses that challenge by implementing a **Retrieval-Augmented Generation (RAG) architecture**.

Instead of relying entirely on the language model's pretrained knowledge, the system retrieves relevant content from a dedicated medical knowledge base and provides that context to the LLM before generating a response.

### Key Objectives

- Build a domain-specific medical question-answering chatbot.
- Use a medical encyclopedia as the primary knowledge source.
- Implement semantic search using vector embeddings.
- Retrieve relevant information using Pinecone.
- Generate context-aware responses using Google Gemini.
- Develop an interactive web application using Flask.

---

## ✨ Key Features

- **Medical Knowledge Retrieval:** Retrieves relevant medical information from The Gale Encyclopedia of Medicine.
- **Retrieval-Augmented Generation:** Combines semantic retrieval with generative AI.
- **Semantic Search:** Uses vector embeddings to identify contextually relevant information.
- **Vector Database:** Stores and searches medical document embeddings using Pinecone.
- **LLM Integration:** Uses Google Gemini through LangChain for response generation.
- **Interactive Web Interface:** Provides a simple chat interface built with Flask, HTML, and CSS.
- **Context-Based Responses:** Generates answers using retrieved medical context rather than relying only on general model knowledge.

---

## 🛠️ Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Backend | Flask |
| LLM | Google Gemini |
| LLM Framework | LangChain |
| Vector Database | Pinecone |
| Embeddings | Hugging Face |
| Frontend | HTML, CSS, JavaScript |
| Document Processing | PyMuPDF |
| Environment Management | Python Virtual Environment |
| Version Control | Git, GitHub |

---

## 🏗️ System Architecture

The application follows a Retrieval-Augmented Generation workflow.

```text
          Medical Encyclopedia PDF
                    |
                    v
             Text Extraction
                    |
                    v
             Text Chunking
                    |
                    v
           Hugging Face Embeddings
                    |
                    v
             Pinecone Vector DB
                    |
                    |
             USER QUESTION
                    |
                    v
           Question Embedding
                    |
                    v
          Semantic Similarity Search
                    |
                    v
          Relevant Document Retrieval
                    |
                    v
           Context + User Question
                    |
                    v
              LangChain
                    |
                    v
             Google Gemini
                    |
                    v
          Context-Aware Response
                    |
                    v
              Flask Web App
                    |
                    v
                User
```

### RAG Workflow

**1. Document Processing**

- Load the medical encyclopedia PDF.
- Extract textual content from the document.
- Split the extracted text into smaller chunks.
- Generate vector embeddings for the text chunks.

**2. Vector Database Storage**

- Store document embeddings in Pinecone.
- Maintain the medical knowledge base for semantic retrieval.

**3. User Query Processing**

- Accept medical questions through the Flask chat interface.
- Convert the user query into an embedding.
- Perform similarity search against the Pinecone vector database.

**4. Context Retrieval**

- Retrieve relevant medical document chunks.
- Combine the retrieved information with the user's question.

**5. Response Generation**

- Pass the question and retrieved context to Google Gemini through LangChain.
- Generate a response grounded in the retrieved medical information.
- Display the generated response in the chatbot interface.

---

## 📚 Knowledge Source

This project uses the following medical reference as its knowledge source:

**The Gale Encyclopedia of Medicine – 2nd Edition **

- Editor: Jacqueline L. Longe
- Publisher: Gale
- Edition: Second Edition
- Volume: 1

The encyclopedia provides medical information covering diseases, disorders, symptoms, treatments, medical terminology, and related healthcare topics.

**Note:** The original medical reference PDF is not included in this GitHub repository. Users must obtain their own legally authorized copy.

---

## 📂 Project Structure

```text
Medical-RAG-Chatbot/
│
├── app.py
│
├── store_index.py
│
├── setup.py
│
├── requirements.txt
│
├── .gitignore
│
├── notebook/
│   └── trails.ipynb
│
├── src/
│   ├── __init__.py
│   ├── helper.py
│   └── prompt.py
│
├── templates/
│   └── chat.html
│
├── static/
│   └── style.css
│
└── README.md
```

### File Descriptions

| File / Directory | Description |
|---|---|
| `app.py` | Main Flask application and chatbot interface |
| `store_index.py` | Document embedding and vector index creation workflow |
| `setup.py` | Project package configuration |
| `requirements.txt` | Python dependencies |
| `src/helper.py` | Helper functions for document processing and related operations |
| `src/prompt.py` | Prompt template for context-based response generation |
| `notebook/` | Jupyter Notebook used during experimentation |
| `templates/` | HTML templates for the chatbot |
| `static/` | CSS styling and frontend assets |

---

## ⚙️ Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Ruthu543/Medical-RAG-Chatbot.git
```

### 2. Navigate to the Project Directory

```bash
cd Medical-RAG-Chatbot
```

### 3. Create a Virtual Environment

```bash
python -m venv .venv
```

### 4. Activate the Virtual Environment

**Windows:**

```powershell
.venv\Scripts\activate
```

**Linux / macOS:**

```bash
source .venv/bin/activate
```

### 5. Install Dependencies

```bash
pip install -r requirements.txt
```

### 6. Configure Environment Variables

Create a `.env` file in the project root directory.

Add your API credentials:

```env
GOOGLE_API_KEY=your_google_gemini_api_key
PINECONE_API_KEY=your_pinecone_api_key
```

Use your own API credentials. Never upload the `.env` file to GitHub.

### 7. Configure Pinecone

- Create a Pinecone account.
- Create or configure a vector index.
- Use an index compatible with your embedding model's vector dimensions.
- Configure the index name and connection settings according to your application code.
- Ensure the index contains the processed medical document embeddings.

The configured Pinecone index used by this project is named `medical-chatbot`.

**Important:** The vector index is not included in this repository. You must configure and populate your own index before running the application if you do not already have one.

### 8. Run the Application

```bash
python app.py
```

Open the local URL displayed by Flask in your browser.

---

## 🔐 Environment Variables

| Variable | Description |
|---|---|
| `GOOGLE_API_KEY` | API key for Google Gemini |
| `PINECONE_API_KEY` | API key for Pinecone |

Keep all credentials in environment variables rather than hardcoding them in Python files.

---

## 💡 Example Use Cases

Users can ask questions related to medical topics covered by the encyclopedia, such as:

- What is acromegaly?
- What are the symptoms of diabetes?
- What is the difference between gigantism and acromegaly?
- What causes hypertension?
- What are the common symptoms of asthma?

The chatbot retrieves relevant information from the medical knowledge base and generates an answer using the retrieved context.

---

## 🔮 Future Enhancements

- Display source references and page numbers alongside generated answers.
- Improve retrieval accuracy using hybrid search and reranking.
- Add conversation history and multi-turn question answering.
- Implement user authentication and chat history storage.
- Add document-level metadata filtering.
- Deploy the application to a cloud platform.
- Improve response evaluation using retrieval and generation metrics.

---

## ⚠️ Medical Disclaimer

This chatbot is developed for educational and informational purposes only.

It is not a substitute for professional medical advice, diagnosis, or treatment. The generated responses may contain inaccuracies or incomplete information. Always consult a qualified healthcare professional for medical concerns and decisions.

---

## 👩‍💻 Author

**Ruthu**

GitHub: [Ruthu543](https://github.com/Ruthu543)

Project Repository: [Medical-RAG-Chatbot](https://github.com/Ruthu543/Medical-RAG-Chatbot)

---

⭐ If you find this project useful, consider giving the repository a star!
