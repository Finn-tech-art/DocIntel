
# DocIntel-Triage: High-Precision Classification Agent (Weekend Project)

An autonomous document intelligence agent built with **LangGraph** and **Groq**. This system is engineered to classify business documents into a 15-category taxonomy with a target precision of **85%+**.

## 🧠 Core Methodology: The 7-Layer Prompting Strategy
To push the **Llama-3.1-8b** model toward production-grade accuracy, the Base Classifier node utilizes a 7-layer construction:

1.  **Role**: Defined as a *Senior Data Triage Specialist* with 15+ years of experience.
2.  **Task**: Categorization across a specific 15-item business taxonomy.
3.  **Context**: Combines surgical Markdown extraction with thematic "Keyword Scorer" hints.
4.  **Constraints**: Strict adherence to a Pydantic-enforced JSON schema.
5.  **Step-by-Step (CoT)**: Internal "Chain-of-Thought" reasoning for linguistic evidence.
6.  **Safety/Error Layer**: Logic for handling ambiguous text, corruption, or extraction failures.
7.  **Output Format**: Structured `DocClassification` object.

## Key Features
- **Surgical Extraction**: Optimized **Docling** implementation that extracts the first 10,000 characters and disables OCR to prevent RAM `bad_alloc` errors.
- **Dynamic Taxonomy**: Supports 15 distinct categories (Legal, Finance, Tech, HR, etc.) to minimize overlap and maximize model confidence.
- **Agentic Routing**: Built on LangGraph to allow for future integration of "Expert" nodes (70B models) for low-confidence retries.

## Setup & Installation

### 1. Requirements
Ensure you have Python 3.10+ and a Groq API Key.

### 2. Install Dependencies
```bash
pip install langgraph langchain-groq docling python-dotenv pydantic langdetect
```

### 3. Environment Config
Create a `.env` file:
```env
GROQ_API_KEY=gsk_your_actual_key_here
```

## Supported Taxonomy
The agent is currently optimized for:
- **Legal**: `Legal_Contract`, `Legal_Litigation`
- **Finance**: `Finance_Invoice`, `Finance_Tax`, `Finance_Statement`
- **Technical**: `Tech_Manual`, `Tech_Architecture`, `Tech_API_Doc`
- **HR**: `HR_Resume`, `HR_Policy`
- **Operations**: `Ops_Logistics`, `Ops_SOP`
- **Management**: `Mkt_Strategy`, `Med_Clinical`, `PM_Project_Plan`

## Usage
Initialize the `StateGraph` in your notebook and invoke with the `file_path`:
```python
initial_state = {
    "file_path": "path/to/doc.pdf",
    "categories": CATEGORIES,
    "is_valid": True
}
final_output = app.invoke(initial_state)
```
```
