# MedTech Regulatory AI Companion: A RAG-based Gap Tool

This repository contains a series of projects demonstrating the development of an AI-powered assistant to navigate the complex landscape of Medical Device regulations. The primary goal is to showcase how Retrieval-Augmented Generation (RAG) can be used to perform analysis on different files, such as the old Medical Device Directive (MDD 93/42/EEC), the new, stricter, Medical Device Regulation (MDR 2017/745), the FDA regulation and the WHO one.

This project was developed as a proof-of-concept to address the significant regulatory challenges faced by MedTech companies and was then improved with notebooks from a coding challenge.

---

## Features

This repository demonstrates a progressive development path through three key stages:

1.  **Simple Q&A on a Single Document:** A foundational RAG system that answers questions based on the content of the MDR document.
2.  **Comparative Gap Analysis:** An advanced RAG system that queries two documents (MDD and MDR) simultaneously to identify and explain the differences and new requirements.
3.  **Interactive Web Application:** A user-friendly Gradio application that wraps the gap analysis engine, providing an intuitive interface for non-technical users.

Subsequently, I added 3 notebooks showcasing a multi-agent approach.

---

## Technology Stack

* **Language:** Python
* **Core AI/RAG Frameworks:** ChromaDB (Vector Store), Sentence-Transformers (Embeddings)
* **LLM Integration:** Google Gemini (`google-generativeai`)
* **PDF Processing:** `pypdf`
* **Web UI:** Gradio
* **Environment Management:** Conda, Pip, `python-dotenv`

---

## Getting Started

Follow these steps to set up and run the project locally.

### 1. Prerequisites

* Python 3.9+
* Conda or another virtual environment manager

### 2. Installation & Setup

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
    cd your-repo-name
    ```

2.  **Create and activate a Conda environment:**
    ```bash
    conda create -n mdrag_env python=3.9
    conda activate mdrag_env
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Set up your API Key:**
    * Create a file named `.env` in the root directory of the project.
    * Add your Google Gemini API key to this file:
        ```
        GOOGLE_API_KEY="AIzaSy...your-key-here"
        ```

5.  **Add the Documents:**
    * Create a folder named `documents` in the root directory.
    * Place your `MDD.pdf` and `MDR.pdf` files inside this folder.

---

## Project Structure & Usage

The core work is presented in three Jupyter Notebooks, located in the `notebooks/` directory.

### 1. `ChromaDB_RAG.ipynb`
* **Purpose:** A simple, foundational RAG implementation.
* **Functionality:** This notebook demonstrates how to load a single document (MDR.pdf), split it into chunks, embed it using their default function, and store it in ChromaDB. It then answers user questions based solely on the MDR document.
* **How to use:** Open and run the cells sequentially to see the basic RAG pipeline in action.

### 2. `Gap_RAG.ipynb`
* **Purpose:** The core logic for the comparative analysis.
* **Functionality:** This notebook advances the RAG system to handle two documents (MDD and MDR). It vectorizes both, adding `source` metadata to each chunk. The query and prompting logic is specifically designed to retrieve context from both sources and instruct the LLM to perform a gap analysis. It also features a processing functions to handle short paragraphs and identify potential titles.
* **How to use:** Again, open and run the cells sequentially. This notebook contains the engine for the Gradio app and is perfect for understanding the detailed implementation of the comparison logic.

### 3. `Gradio_RAG.ipynb`
* **Purpose:** A fully functional web application prototype.
* **Functionality:** This notebook wraps the entire gap analysis pipeline from the previous notebook into an interactive Gradio interface. It initializes the vector database on startup and provides a user-friendly UI for asking questions and receiving a consultant-style analysis.
* **How to use:** The code is formatted in a single cell. Run the cell and the app will start. Note: if the share parameter on the launch function is set to True, it will also create a public URL to showcase the application.

### 4. `Gradio_txt_RAG.ipynb`
* **Purpose:** An improved, text-based, fully functional RAG prototype.
* **Functionality:** This notebook switches from the PDF chunking to a more effective txt chunking. Creates a golden dataset focusing less on the low-level PDF logic that is harder to implement in the short term, highly improving answers' source relevance.
* **How to use:** The code is formatted in a single cell. Run the cell and the app will start. Note: if the share parameter on the launch function is set to True, it will also create a public URL to showcase the application.

### 5. `MultiAgentRAG_initial_design.ipynb`
* **Purpose:** A multi-agent (3) RAG prototype on FDA-WHO documentation.
* **Functionality:** I introduce a 3-agent approach to the analysis of documents. an orchestrator, a RAG agent and a response agent work together retrieving documents and crafting an answer.
* **How to use:** Open and run the cells sequentially to see the basic RAG pipeline in action.

### 6. `MultiAgentRAG_chunking_agent.ipynb`
* **Purpose:** Adding a chunking agent to the last notebook.
* **Functionality:** In this notebook I explore chunking techniques, from non-intelligent logic (paragraphs, length, etc.) to semantic chunking, peaking with a focused agent who performs this task.
* **How to use:** Open and run the cell. N.B: I still have to finish the parsing of the chunking agent, therefore the code can show some bugs.

### 7. `MultiAgentRAG_final_implementation.ipynb`
* **Purpose:** The working prototype.
* **Functionality:** This code showcases a paper explaining design choices, a personal README, and improved prompting structure.
* **How to use:** Open and run the cells subsequently.
