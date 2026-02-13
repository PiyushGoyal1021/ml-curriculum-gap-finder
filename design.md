# Technical Design Document
## ML-Powered Curriculum Gap Finder (MVP)

---

## 1. System Architecture

The system follows a simple 3-layer architecture:

Frontend (React)
        ↓
Backend API (FastAPI)
        ↓
PostgreSQL + pgvector

All components are deployed on a single AWS EC2 instance for MVP.

---

## 2. Technology Stack

Backend:
- FastAPI (Python)
- SQLAlchemy
- Uvicorn

Frontend:
- React + TypeScript
- Recharts / Chart.js

Database:
- PostgreSQL
- pgvector extension

NLP:
- Sentence-BERT (all-MiniLM-L6-v2)
- spaCy (for preprocessing)

Deployment:
- AWS EC2 (Ubuntu)
- Nginx reverse proxy

---

## 3. Data Flow

### 3.1 Syllabus Processing

1. User uploads PDF
2. Backend extracts text using PyPDF2
3. NLP model extracts skills
4. Skills converted to embeddings
5. Embeddings stored in PostgreSQL (pgvector)

---

### 3.2 Job Posting Processing

1. Admin uploads CSV dataset
2. Job descriptions parsed
3. Skills extracted
4. Embeddings generated
5. Stored in database

---

### 3.3 Gap Analysis

1. Fetch syllabus skill embeddings
2. Fetch job skill embeddings
3. Compute cosine similarity
4. Identify missing skills
5. Calculate weighted gap score

Gap Score Formula:

gap_score =
( missing_critical * 0.5 +
  missing_medium * 0.3 +
  missing_low * 0.2 ) * 100

---

## 4. Database Schema (Simplified)

Tables:

users
syllabi
job_postings
skills
skill_embeddings (vector column)
gap_results

Using pgvector for similarity search:

SELECT *
FROM skill_embeddings
ORDER BY embedding <-> query_vector
LIMIT 10;

---

## 5. API Design

POST /upload-syllabus  
POST /upload-job-data  
POST /compute-gap  
GET /gap-result/{id}  
GET /dashboard-data  

All responses JSON.

---

## 6. ML Pipeline

Embedding Model:
- SentenceTransformer('all-MiniLM-L6-v2')
- 384-dimension vectors

Similarity:
- Cosine similarity
- Threshold = 0.7

Recommendation Logic:
- Rank missing skills by frequency
- Suggest curriculum module addition

---

## 7. Deployment Plan

Single EC2 instance:
- Backend running on port 8000
- Frontend built and served via Nginx
- PostgreSQL running locally
- SSL via Let's Encrypt

Future Scaling:
- Move DB to RDS
- Add caching layer
- Horizontal scaling if needed
