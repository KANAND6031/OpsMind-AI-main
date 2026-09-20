# 🚀 OpsMind AI – Context-Aware Corporate Knowledge Brain

OpsMind AI is an AI-powered Enterprise Knowledge Management System that enables employees to interact with corporate documentation and Standard Operating Procedures (SOPs) using natural language.

The system uses **Retrieval-Augmented Generation (RAG)** to retrieve relevant information from uploaded SOP documents and generate contextually grounded, factually verifiable responses using Google Gemini 2.5 Flash and local dense Transformer embeddings.

---

## 📄 Academic Internship Report in LaTeX

A comprehensive, university-level academic internship report has been prepared for the Department of Computer Science and Engineering, Indian Institute of Information Technology Senapati, Manipur.

### 📂 Report Structure

```text
OpsMind-AI-main/
├── report.tex                    # Master LaTeX report document
├── main.tex                      # Wrapper entrypoint pointing to report.tex
├── report.bib                    # BibTeX bibliography database
├── report.pdf                    # Compiled complete academic report (43 pages)
├── report_file/                  # High-resolution diagrams, screenshots, and logos
│   ├── iiit manipur.png          # IIIT Manipur Institute Emblem
│   ├── upload_dashboard.png      # Document Ingestion & Analytics UI
│   ├── chat_empty.png            # Conversational Assistant Interface
│   └── chat_qa_citation.png      # Query Answering & Source Attribution UI
│
├── chapters/
│   ├── 1_Introduction.tex        # 1.1 Outline, 1.2 Problem Statement, 1.3 Motivation, 1.4 Purpose
│   ├── 2_Literature_Survey.tex   # IR Evolution, Sentence-BERT, MiniLM, RAG, HNSW & Vector DBs
│   ├── 3_Requirement.tex         # Functional, Non-Functional, Hardware/Software Specs, Use Cases
│   ├── 4_System_Design.tex       # Multi-Tier Architecture, Ingestion/Query Flows, Schemas, Algorithms
│   ├── 5_Implementation.tex      # PDF Parsing, ONNX Embeddings, Vector Search, LLM SDK, Frontend UI
│   ├── 6_Results.tex             # Evaluation on 46-pg SOP, 205 Chunks, Scores, Latency & Visual Figures
│   └── 7_Conclusion.tex          # Key Contributions, System Limitations, and Future Roadmap
```

### 🛠️ How to Compile the LaTeX Report

To compile the complete report from source:

```bash
# 1. First LaTeX compilation pass
pdflatex -interaction=nonstopmode report.tex

# 2. Process BibTeX citations
bibtex report

# 3. Resolve cross-references and table of contents
pdflatex -interaction=nonstopmode report.tex

# 4. Final typesetting pass
pdflatex -interaction=nonstopmode report.tex
```

---

# 📌 Features

### 📄 SOP Upload & Processing
* Multi-part PDF upload with MIME validation
* Automatic text extraction via `pdfjs-dist`
* Sliding-window chunking ($1,000$ characters with $100$ character overlap)
* Operational domain section categorization
* In-process 384-dimensional dense vector embeddings (`all-MiniLM-L6-v2`)
* Atomic chunk insertion and vector indexing in MongoDB Atlas

---

### 🤖 AI-Powered Question Answering
* Natural language search with query embedding generation
* Approximate Nearest Neighbor (ANN) cosine similarity search
* Strict anti-hallucination confidence gating ($\tau = 0.65$)
* Context-grounded generative synthesis using Google Gemini 2.5 Flash

---

### 📚 Source Citations & Auditability
Every generated response includes complete provenance:
* Originating SOP File Name
* Exact Page Number
* Operational Section Header
* Chunk Index
* Cosine Similarity Score
* Interactive modal overlay for inspecting raw text excerpts

---

### 📊 Document Analytics & Admin Panel
* Real-time metrics: Total Ingested Pages, Indexed Chunks, Embedding Dimensions ($384$), Active AI Model
* Administrative SOP repository management (inventory review, atomic purging, re-indexing)
* Dual-theme dark/light responsive interface

---

# 🏗 System Architecture

```text
                    ┌───────────────────────────────┐
                    │      React Single Page UI     │
                    │   (Vite + Tailwind CSS)       │
                    └──────────────┬────────────────┘
                                   │ REST / JSON (Axios)
                                   ▼
                    ┌───────────────────────────────┐
                    │       Node.js / Express       │
                    │      Orchestration Server     │
                    └──────────────┬────────────────┘
                                   │
             ┌─────────────────────┼─────────────────────┐
             │                     │                     │
             ▼                     ▼                     ▼
     ┌───────────────┐     ┌───────────────┐     ┌───────────────┐
     │ MongoDB Atlas │     │ Transformers  │     │ Google Gemini │
     │ Vector Search │     │ all-MiniLM-L6 │     │   2.5 Flash   │
     └───────────────┘     └───────────────┘     └───────────────┘
```

---

# ⚙ Tech Stack

## Frontend
* React.js (v18)
* Vite
* Tailwind CSS
* Axios

## Backend & Document Pipeline
* Node.js & Express.js
* Multer (multipart upload handling)
* `pdfjs-dist` & `pdf-parse`

## AI & Vector Persistence
* `@xenova/transformers` (`all-MiniLM-L6-v2` ONNX pipeline)
* MongoDB Atlas Vector Search
* `@google/genai` (Google Gemini 2.5 Flash)

---

# 💻 Running the Application Locally

## 1. Backend Setup
```bash
cd backend
npm install
npm start
# Server listens on http://localhost:5000
```

## 2. Frontend Setup
```bash
cd frontend
npm install
npm run dev
# Interface opens on http://localhost:5173
```
