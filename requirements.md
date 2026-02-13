# Requirements Document
## ML-Powered Curriculum Gap Finder

## 1. Overview

The ML-Powered Curriculum Gap Finder is an AI-based platform that analyzes academic syllabi and industry job postings to identify skill gaps and generate curriculum improvement recommendations.

The system aims to bridge the curriculum-industry divide by using NLP-based semantic matching between academic topics and job market skill requirements.

---

## 2. Objectives

- Automatically extract skills from syllabus documents
- Extract required skills from job postings
- Perform semantic similarity matching
- Compute a curriculum gap score
- Generate actionable recommendations
- Provide an interactive dashboard

---

## 3. User Personas

### Academic Administrator
Uploads syllabus documents and views gap analysis.

### Curriculum Designer
Uses recommendations to improve course structure.

---

## 4. Functional Requirements

### 4.1 Syllabus Upload
- Accept PDF syllabus documents
- Extract text content
- Store structured syllabus data

### 4.2 Job Posting Input
- Accept bulk job posting dataset (CSV or API)
- Extract job description text
- Extract skill keywords

### 4.3 Skill Extraction
- Use NLP model to identify skills
- Normalize similar skill variations

### 4.4 Embedding Generation
- Generate vector embeddings using Sentence-BERT
- Store embeddings in database (pgvector)

### 4.5 Semantic Matching
- Compute cosine similarity between syllabus skills and job skills
- Apply threshold (default 0.7)

### 4.6 Gap Score Calculation
- Identify missing skills
- Compute weighted gap score (0–100)

### 4.7 Recommendations
- Suggest adding new modules
- Suggest strengthening specific skills
- Rank recommendations by demand frequency

### 4.8 Dashboard
- Display gap score
- Display missing skills
- Show skill match matrix
- Visualize trending skills

---

## 5. Non-Functional Requirements

- Response time < 3 seconds for dashboard
- Support 10+ concurrent users
- Secure login authentication
- Cloud deployable
- Modular code structure

---

## 6. Success Metrics

- 80% skill extraction accuracy
- Gap score consistency across runs
- <30 seconds report generation
- Positive usability feedback

---

## 7. Constraints

- Built using FastAPI, React, PostgreSQL
- Use pre-trained NLP models
- Deployable on single AWS EC2 instance
