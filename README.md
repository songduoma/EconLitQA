# EconLitQA: A Retrieval-Augmented Question-Answering System for Economics Literature

EconLitQA is a retrieval-augmented question-answering system designed for economic research, addressing the limitations of existing literature review tools in domain specificity and language understanding. This system integrates large language models (LLMs) with semantic retrieval techniques to extract relevant academic articles from economic journals and generate accurate, contextually relevant responses based on user queries.

---

## Table of Contents

- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [System Architecture & Workflow](#system-architecture--workflow)
- [Installation & Setup](#installation--setup)
- [Usage](#usage)
  - [Data Scraping](#data-scraping)
  - [Data Preprocessing](#data-preprocessing)
  - [Question-Answering System](#question-answering-system)
  - [Keyword Dataset Generation](#keyword-dataset-generation)
- [Evaluation Module](#evaluation-module)
- [License](#license)
- [Contact Information](#contact-information)

---

## Introduction

EconLitQA is a research project aimed at improving literature search and retrieval in economics through:

- **Keyword extraction**: Identifying core concepts from user queries.
- **Semantic retrieval**: Using a vector database to find relevant economics articles.
- **Answer generation**: Producing contextually relevant responses based on retrieved content using LLMs.

Additionally, the project includes an **evaluation module** to assess response **keywords extraction performance**, **faithfulness** and **answer relevance**, ensuring reliability and accuracy.

---

## Project Structure

```bash
.
├── data
│   ├── raw
│   │   └── thesis_article.xlsx             # Raw economics articles dataset
│   ├── processed
│   │   └── thesis_output.txt               # Preprocessed articles
│   └── econ_questions_keywords.csv         # Generated dataset of questions & keywords
├── docs
│   ├── Bachelor_Thesis.pdf                 # Complete thesis document
│   └── flow_chart.png                      # System workflow diagram
├── notebooks
│   ├── data_scraping.ipynb                 # Article scraping process
│   ├── data_preprocessing.ipynb            # Data preprocessing
│   ├── econlitqa_chatgpt.ipynb             # EconLitQA using ChatGPT
│   ├── econlitqa_llama.ipynb               # EconLitQA using Meta-Llama
│   ├── econlitqa_mistral.ipynb             # EconLitQA using Mistral
│   └── dataset_keywords_generation.ipynb   # Keyword & question dataset generation
├── src                                     # Core system modules
│   ├── data_scraping.py                    # Data scraping module
│   ├── data_preprocessing.py               # Data preprocessing module
│   ├── econlitqa.py                        # Question-answering system core logic
│   └── evaluation.py                        # Evaluation module (factuality & relevance)
├── .gitignore
├── requirements.txt
├── apikey.txt                              # OpenAI API key (configure separately)
└── password.txt                            # HuggingFace API key (configure separately)
```

---

## System Architecture & Workflow

1. **Data Scraping**  
   - Use `data_scraping.ipynb` (or `src/data_scraping.py`) to scrape articles from selected economic journals, storing results in `thesis_articles.xlsx`.

2. **Data Preprocessing**  
   - Run `data_preprocessing.ipynb` (or `src/data_preprocessing.py`) to clean and format the scraped data, producing `thesis_output.txt`.

3. **Vector Database Construction**  
   - The preprocessed articles are split into segments, and embeddings are generated using a vector database (e.g., FAISS) to enable efficient retrieval.

4. **Question-Answering System**  
   - The user query is first processed by an LLM to extract key concepts, then relevant content is retrieved from the vector database, and finally, a response is generated based on the retrieved data.
   - Multiple implementations (ChatGPT, Meta-Llama, Mistral) are provided for comparison.

5. **Evaluation Module**  
   - Includes **keywords extraction performance**,  **faithfulness**  and **answer relevance**.

---

## Installation & Setup

### Prerequisites

- Python 3.8 or later
- [pip](https://pip.pypa.io/)
- Git
- (Optional) CUDA drivers & GPU support for faster processing

### Installation Steps

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/EconLitQA.git
   cd EconLitQA
   ```

2. **Create a virtual environment (recommended)**

   ```bash
   python -m venv venv
   source venv/bin/activate    # Linux / macOS
   venv\Scripts\activate       # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Configure API Keys**

   - Store your OpenAI API key in `apikey.txt`
   - Store your HuggingFace API key in `password.txt`

   > **Note:** These files should remain private. Add them to `.gitignore` to prevent accidental exposure.

---

## Usage

### Data Scraping

- **Notebook**: Open `notebooks/data_scraping.ipynb` and run the scraping process.
- **Command-line**: Execute `src/data_scraping.py`  to scrape data and store results in `thesis_articles.xlsx`.

### Data Preprocessing

- **Notebook**: Open `notebooks/data_preprocessing.ipynb` to process the raw Excel file and generate `thesis_output.txt`.
- **Command-line**: Run `src/data_preprocessing.py` for data cleaning and formatting.

### Question-Answering System

This system supports multiple LLM implementations. Available notebooks include:

- **ChatGPT-based version**: `notebooks/econlitqa_chatgpt.ipynb`
- **Meta-Llama-based version**: `notebooks/econlitqa_llama.ipynb`
- **Mistral-based version**: `notebooks/econlitqa_mistral.ipynb`

These notebooks demonstrate the complete workflow, from keyword extraction to semantic retrieval and final response generation.

### Keyword Dataset Generation

- **Notebook**: Open `notebooks/dataset_keywords_generation.ipynb` to generate a dataset containing questions and their corresponding keywords, saved as `econ_questions_keywords.csv`.
- **Command-line**:Run `src/dataset_keywords_generation.py` to generate the dataset.

---

## Evaluation Module

The project includes evaluation tools for **Keywords Extraction evaluation**, **faithfulness** and **answer relevance**:

- **Keywords Extraction evaluation**: Counts evaluation metrics including precision rate, recall rate and f1 score.

- **Faithfulness evaluation**: Splits responses into individual claims and checks whether each is supported by retrieved content.
- **Answer relevance evaluation**: Uses reverse question generation to assess semantic similarity between the original query 