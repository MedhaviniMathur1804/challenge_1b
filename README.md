# Challenge 1B – Document Section Ranking

## **Overview**
This project focuses on extracting and ranking relevant sections and subsections from PDF documents based on a defined persona and job-to-be-done.  
The aim is to provide **intelligent, prioritized insights** from diverse PDFs with lightweight processing.

---

## **Methodology**

### **1. Document Parsing**
- **Library:** PyMuPDF
- Parses PDF files to extract raw text page by page.
- Text is split into lines for identifying possible section headers.

### **2. Section Detection**
- Uses simple heuristics to detect section titles:
  - Line is in title case.
  - Line length > 5 characters.
- Avoids heavy pretrained models for faster, offline processing.

### **3. Vector Representation & Ranking**
- **Technique:** TF-IDF + Cosine Similarity
- Combines persona and job description into a query.
- Ranks document sections based on similarity to the query.
- Selects top 10 relevant sections.

### **4. Subsection Analysis**
- Extracts the first 500 characters of text from each ranked section.
- Labels snippets with **document name and page number**.

### **5. Output Generation**
- Stores results in JSON format with:
  - Persona and job metadata.
  - Ranked sections with scores.
  - Subsections for context.

---

## **Compliance**
- **CPU-only** execution (no GPU needed).
- **Model size < 1GB.**
- **Execution time ≤ 60 seconds**.
- **No internet access required**.

---

## **Output Example**
```json
{
  "persona": "Recruiter",
  "job": "Identify AI topics",
  "results": [
    {
      "document": "AI_Whitepaper.pdf",
      "page": 3,
      "title": "Introduction to AI",
      "snippet": "Artificial Intelligence (AI) is ..."
    }
  ]
}
