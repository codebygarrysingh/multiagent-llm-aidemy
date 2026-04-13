# LLM-Powered Recommendation Service

A serverless LLM API built on **Google Cloud Functions**, **LangChain**, and **Gemini 2.0 Flash** — demonstrating structured output parsing, prompt engineering, and production LLM deployment patterns.

[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white)](https://langchain.com)
[![Google Cloud](https://img.shields.io/badge/Google_Cloud-4285F4?style=flat&logo=googlecloud&logoColor=white)](https://cloud.google.com)
[![Vertex AI](https://img.shields.io/badge/Vertex_AI-Gemini_2.0-8A2BE2?style=flat&logo=googlecloud&logoColor=white)](https://cloud.google.com/vertex-ai)

---

## Overview

This service demonstrates a core LLM engineering pattern: **structured output extraction** via LangChain's `JsonOutputParser` with Pydantic schema validation. The LLM is instructed to return well-typed, schema-compliant JSON — a technique foundational to building reliable agentic and multi-agent systems where agents must consume each other's outputs.

**Key Patterns Demonstrated:**
- Structured LLM output with Pydantic schema enforcement
- LangChain `PromptTemplate` + output parser chaining (`prompt | llm | parser`)
- Serverless deployment on Google Cloud Functions (`functions_framework`)
- REST API interface with JSON request/response handling

---

## Architecture

```
HTTP Request
    │
    ▼
Cloud Function (functions_framework)
    │
    ▼
LangChain Chain
    ├── PromptTemplate  (injects format instructions + query)
    ├── ChatVertexAI    (Gemini 2.0 Flash)
    └── JsonOutputParser (Pydantic: Book schema)
    │
    ▼
Structured JSON Response
```

---

## Tech Stack

| Component | Technology |
|---|---|
| LLM | Google Gemini 2.0 Flash (via Vertex AI) |
| Orchestration | LangChain (`langchain_google_vertexai`) |
| Output Parsing | `JsonOutputParser` + Pydantic |
| Deployment | Google Cloud Functions (`functions_framework`) |
| API | Flask / HTTP |

---

## API Reference

**Endpoint:** `POST /recommended`

**Request:**
```json
{
  "category": "machine learning",
  "number_of_book": 3
}
```

**Response:**
```json
[
  {
    "bookname": "Foundations of Gradient Descent",
    "author": "Dr. Priya Nair",
    "publisher": "Apex Technical Press",
    "publishing_date": "2023-06-15"
  }
]
```

---

## Local Development

```bash
# Install dependencies
pip install -r requirements.txt

# Set GCP project
export GOOGLE_CLOUD_PROJECT=your-project-id

# Run locally
functions-framework --target=recommended --debug
```

---

## Output Schema

```python
class Book(BaseModel):
    bookname: str       # Title of the book
    author: str         # Author name
    publisher: str      # Publisher name
    publishing_date: str  # Publication date
```

---

## Related Work

This repo is part of a broader portfolio of AI/ML and data engineering work:

- [ml-neural-network-projects](https://github.com/codebygarrysingh/ml-neural-network-projects) — TensorFlow neural networks
- [blog-summarizer-app](https://github.com/codebygarrysingh/blog-summarizer-app) — GPT-powered content summarisation
- [ml-regression-python-projects](https://github.com/codebygarrysingh/ml-regression-python-projects) — End-to-end regression pipelines

---

## Author

**Garry Singh** — Principal AI & Data Engineer · MSc Oxford · Available for consulting

[Portfolio](https://garrysingh.dev) · [LinkedIn](https://linkedin.com/in/singhgarry) · [Email](mailto:garry.singh2902@gmail.com)
