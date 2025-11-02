# Lumin: A Corporate Legal LLM ⚖️

Lumin is an advanced Legal Large Language Model (LLM) designed to assist with corporate law tasks specific to the **Indian Companies Act 2013**. It leverages a **Mistral 7-B** model, fine-tuned on this specific legal corpus, to provide accurate and context-aware legal analysis, summarization, and generation.

The system is built on a **Retrieval-Augmented Generation (RAG)** pipeline, which uses a **FAISS** vector store containing the entire Companies Act, chunked section-by-section.

---

## 🚀 Core Features & Modules

Lumin is structured as a suite of powerful, independent tools, each targeting a specific legal task.

### 1. Legal LLM Chatbot
An interactive, conversational AI that can answer questions related to the Indian Companies Act 2013. It's a quantized Mistral 7B model, fine-tuned on the Companies Act 2013 using Unsloth.

### 2. Role-Based Contract Summarizer
Generates "persona-specific" summaries of legal contracts. A summary for a **corporate lawyer** will highlight legal nuances and risks, while a summary for a **legal student** might focus on definitions and core principles.

### 3. Contract & Clause Generator
Assists in drafting new legal contracts and specific clauses from natural language prompts, ensuring they align with the underlying legal framework.

### 4. Full Contract Compliance Analysis
This module performs a comprehensive compliance check on an entire contract:
* **Input:** A full legal contract.
* **Process:**
    1.  The model first identifies the **contract type**.
    2.  It then uses RAG to retrieve semantically relevant sections from the Companies Act, supplemented by a set of fixed acts known to be relevant to that contract type.
    3.  Finally, it performs an **instruction-prompted compliance check** against the retrieved legal texts.

### 5. Specific Clause Compliance Check
This module performs a focused check on a single clause against a specific law:
* **Input:** A single contract clause and a specific section number (e.g., "Clause 5.1" and "Section 149").
* **Process:**
    1.  The system retrieves the exact text of the specified section using RAG.
    2.  It then verifies if the provided clause complies with the stipulations of that section.

---

## ⚙️ Technical Architecture

The core of Lumin's accuracy comes from its RAG pipeline:

1.  **Vector Store:** The entire Indian Companies Act 2013 is parsed, chunked section-by-section, and then embedded using **Sentence-Transformers**.
2.  **Storage:** These high-dimensional vectors are stored in a **FAISS** vector store for efficient similarity search.
3.  **Retrieval:** When a query is made (e.g., for compliance or by the chatbot), the RAG pipeline retrieves the most relevant legal sections from FAISS.
4.  **Generation:** These retrieved sections (the "context") are injected into a prompt for the **fine-tuned Mistral 7-B** model, which then generates the final, context-aware, and legally-grounded response.

---

## 💻 Technology Stack

* **Programming Language:** Python
* **Core LLM/ML Libraries:** Hugging Face `transformers`, `langchain`
* **Embeddings:** `sentence-transformers`
* **Vector Database:** `faiss-cpu` (or `faiss-gpu`)
* **Base Model:** Mistral 7-B (Fine-tuned)
* **UI/Demonstration:** Gradio
* **Environment:** Kaggle Notebooks

---

## ▶️ How to Use

This project is structured as a series of **Kaggle Notebooks**, with the modules combined and presented through a simple **Gradio** interface.

As the project is designed to run directly within the Kaggle environment, there is no complex local installation required.

**To run the project:**
1.  Open the main Kaggle Notebook.
2.  Run all the cells to install the dependencies, initialize the models, and build the FAISS vector store.
3.  The Gradio interface will launch within the notebook, providing a simple input/output UI for each of the five modules.
