# RAG-Based Document Question Answering with Retrieval Reranking

A Retrieval-Augmented Generation (RAG) based document question-answering system that retrieves relevant information from an Employee Handbook, reranks the retrieved results using a Cross-Encoder, and generates answers using a transformer-based language model.

---

## Project Overview

This project implements a document question-answering pipeline using Retrieval-Augmented Generation (RAG).

The system uses an Employee Handbook PDF as the knowledge source and answers questions related to:

- Working hours
- Vacation policy
- Sick leave policy
- Holidays
- Confidentiality policy

The retrieved document chunks are reranked using a Cross-Encoder before being passed to the answer-generation model.

---

## Problem Statement

Large documents contain a significant amount of information, making it difficult to directly identify the relevant information for a user's question.

This project addresses this problem using a RAG pipeline that:

1. Extracts text from the Employee Handbook PDF
2. Splits the document into smaller chunks
3. Generates embeddings for the chunks
4. Stores the embeddings in ChromaDB
5. Retrieves relevant chunks for a user query
6. Reranks the retrieved chunks using a Cross-Encoder
7. Generates an answer using FLAN-T5
8. Evaluates the generated answer using semantic similarity

---

## Project Workflow

Employee Handbook PDF → Text Extraction → Document Chunking → Sentence Transformer Embeddings → ChromaDB Vector Store → Initial Retrieval → Cross-Encoder Reranking → Relevant Context → FLAN-T5 Answer Generation → Generated Answer → Semantic Similarity Evaluation

---

## Architecture

    Employee Handbook PDF
            ↓
      Text Extraction
            ↓
         Chunking
            ↓
       Embeddings
            ↓
         ChromaDB
            ↓
     Initial Retrieval
            ↓
   Cross-Encoder Reranking
            ↓
      Relevant Context
            ↓
      FLAN-T5 Base
            ↓
     Generated Answer
            ↓
    Semantic Similarity
       Evaluation

---

## Key Components

### 1. Document Processing

The project uses an Employee Handbook PDF as the source document.

The document contains information related to:

- Working hours and attendance
- Overtime
- Vacation
- Sick leave
- Holidays
- Personal leave
- Employee benefits
- Confidentiality
- Computer and information security
- Other employee policies

### 2. Text Chunking

The extracted document text is divided into smaller chunks before generating embeddings.

Chunking helps the retrieval system identify relevant sections of the document for a given question.

### 3. Embeddings

Sentence Transformers are used to convert document chunks into vector representations.

Embedding Model:

`all-MiniLM-L6-v2`

These embeddings are used for semantic similarity-based retrieval.

### 4. Vector Database

ChromaDB is used as the vector store for storing and retrieving document embeddings.

### 5. Initial Retrieval

The user's question is converted into an embedding and compared with the stored document embeddings.

The most relevant document chunks are retrieved as candidate contexts.

### 6. Cross-Encoder Reranking

A Cross-Encoder is used to rerank the initially retrieved document chunks.

Reranker Model:

`BAAI/bge-reranker-base`

The Cross-Encoder evaluates the relationship between the question and each retrieved chunk and assigns relevance scores.

### 7. Answer Generation

The reranked context is provided to:

`google/flan-t5-base`

The model generates the final answer using the retrieved document context.

---

## Models Used

| Component | Model |
|---|---|
| Embedding Model | `all-MiniLM-L6-v2` |
| Cross-Encoder Reranker | `BAAI/bge-reranker-base` |
| Answer Generation Model | `google/flan-t5-base` |

---

## Technologies Used

- Python
- Jupyter Notebook
- PyPDF
- Sentence Transformers
- ChromaDB
- Hugging Face Transformers
- Cross-Encoder
- NumPy
- Scikit-learn

---

## Evaluation

The generated answers are evaluated using semantic similarity.

For each question:

1. The question is passed to the RAG pipeline.
2. Relevant document chunks are retrieved.
3. Retrieved chunks are reranked.
4. FLAN-T5 generates an answer.
5. The generated answer is converted into an embedding.
6. The generated answer is compared with the ground-truth answer using cosine similarity.

The resulting percentage represents semantic similarity between the generated answer and the ground-truth answer.

**Note:** The reported percentage is a semantic similarity score and should not be interpreted as classification accuracy.

---

## Evaluation Results

| Question | Semantic Similarity |
|---|---:|
| What are the working hours? | 64.85% |
| What is the vacation policy? | 66.98% |
| What is the sick leave policy? | 63.06% |
| What are the holidays? | 58.92% |
| What is the confidentiality policy? | 67.69% |
| **Average** | **64.30%** |

---

## Example Questions

The system was evaluated using questions such as:

- What are the working hours?
- What is the vacation policy?
- What is the sick leave policy?
- What are the holidays?
- What is the confidentiality policy?

---

## Why Cross-Encoder Reranking?

Initial vector retrieval identifies document chunks that are semantically related to the query.

The Cross-Encoder provides an additional relevance-ranking step by evaluating the query together with each retrieved document chunk.

User Query → Vector Retrieval → Candidate Chunks → Cross-Encoder Reranking → Relevant Context → Answer Generation

This helps provide more relevant context to the answer-generation model.

---

## Project Features

- PDF-based question answering
- Retrieval-Augmented Generation
- Document chunking
- Sentence Transformer embeddings
- ChromaDB vector storage
- Semantic similarity retrieval
- Cross-Encoder reranking
- FLAN-T5 answer generation
- Ground-truth based evaluation
- Cosine similarity evaluation
- Average semantic similarity reporting

---

## Dataset

The knowledge source for this project is a sample Employee Handbook PDF.

The document includes sections related to working hours, attendance, holidays, vacation, sick leave, employee benefits, confidentiality, and computer and information security.

The source document is included in the repository as:

`Employee_handbook(5).pdf`

---

## Repository Structure

    RAG_Assistant/
    ├── RAG_Assistant.ipynb
    ├── Employee_handbook.pdf
    └── README.md

---

## Notebook

### `RAG_Assistant.ipynb`

The notebook contains the complete implementation of the project, including:

1. PDF loading
2. Text extraction
3. Text chunking
4. Embedding generation
5. ChromaDB vector storage
6. Initial document retrieval
7. Cross-Encoder reranking
8. Context preparation
9. FLAN-T5 answer generation
10. Semantic similarity evaluation
11. Evaluation result calculation

---

## Results

The implemented RAG pipeline achieved an average semantic similarity of:

**64.30%**

The project demonstrates the complete workflow from document ingestion and retrieval to reranking, answer generation, and semantic evaluation.

---

## Future Improvements

- Improve document chunking strategy
- Tune retrieval parameters
- Experiment with different embedding models
- Compare multiple reranking models
- Improve answer-generation prompts
- Experiment with stronger language models
- Add a Streamlit interface
- Add retrieval evaluation metrics such as Recall@K and MRR
- Improve semantic evaluation using multiple reference answers

---

## Conclusion

This project demonstrates a complete Retrieval-Augmented Generation pipeline for document-based question answering.

By combining document retrieval, embeddings, ChromaDB, Cross-Encoder reranking, and FLAN-T5 answer generation, the system can retrieve relevant information from an Employee Handbook and generate answers based on the retrieved context.

The project also includes semantic similarity evaluation to measure the similarity between generated answers and ground-truth answers.

---

## Project Highlights

**RAG + Embeddings + ChromaDB + Cross-Encoder Reranking + FLAN-T5 + Semantic Evaluation**
