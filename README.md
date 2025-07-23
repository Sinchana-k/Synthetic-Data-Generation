# Synthetic-Data-Generation
# Synthetic Data Generator API using FastAPI, CTGAN, Gemini, and ChromaDB

This project is an intelligent synthetic data generation platform built with FastAPI. It integrates CTGAN for realistic tabular data generation, ChromaDB for dataset retrieval, and Google Gemini (via google-generativeai) for agentic preprocessing, constraint handling, and dynamic decision making using natural language.

## Features

- Upload real datasets and generate synthetic samples using CTGAN
- Automatically clean and preprocess datasets using Gemini AI (agentic workflows)
- Accept natural language constraints (e.g. "age > 30 and income < 80000") and apply them to generated data
- Retrieve similar datasets using ChromaDB vector search
- Evaluate the similarity between original and synthetic datasets using statistical tests (mean, variance, KS test)
- Natural language chatbot assistant powered by Gemini to guide users
- API support for both column-based and constraint-based data generation
- Download constrained datasets via HTTP endpoint

## Technologies Used

- Python 3
- FastAPI + Uvicorn
- CTGAN
- Google Gemini AI (google-generativeai)
- ChromaDB (vector store for dataset similarity)
- Pandas, NumPy, SciPy
- Pydantic for request validation

## Setup Instructions

1. Clone the repository:

   git clone https://github.com/yourusername/synthetic-agentic-generator.git  
   cd synthetic-agentic-generator

2. Install dependencies:

   pip install -r requirements.txt

   Or manually install:

   pip install fastapi uvicorn pandas numpy ctgan chromadb google-generativeai scipy python-multipart  
   pip install torch torchvision  # Required for CTGAN

3. Set your Gemini API key:

   export GOOGLE_API_KEY="your-api-key"

4. Run the FastAPI app:

   uvicorn main:app --reload

   Visit the Swagger docs at: http://127.0.0.1:8000/docs or open index.html

## API Endpoints

- POST /generate  
  Upload a CSV and get synthetic data back

- POST /generate-with-columns  
  Generate data from similar dataset using selected columns

- POST /process-natural-language-constraints  
  Convert text constraints (e.g. "age > 30") to JSON using Gemini

- POST /submit-constraints  
  Apply constraints and receive filtered synthetic data

- GET /download/{filename}  
  Download any file previously generated

- POST /evaluate-synthetic-data  
  Compare original and synthetic datasets using mean, variance, and KS test

- POST /chat  
  Ask Gemini anything related to synthetic data generation, constraints, etc.

## Directory Structure

.
├── main.py                    # FastAPI backend
├── generated_data/           # Folder to store all datasets
└── .cache/chroma/            # Persistent vector DB for dataset embeddings

## Example Flow

1. Upload your CSV using /generate
2. Use /process-natural-language-constraints to convert constraints
3. Submit constraints via /submit-constraints
4. Download the generated dataset from /download/{filename}
5. Evaluate it using /evaluate-synthetic-data
6. Use /chat to guide non-technical users through the pipeline

## Notes

- CTGAN requires time and memory. Keep data clean and numeric-heavy for best results.
- Gemini adds intelligent decision-making for non-numeric columns, NaNs, column types, etc.
- This tool is ideal for generating privacy-preserving datasets for demos or prototyping.

## License

This project is open-sourced for academic, research, and experimentation purposes only. Not suitable for production or sensitive data.
