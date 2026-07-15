# AI Travel Reimbursement Approval Agent

## Overview

This project is a GenAI-powered Travel Reimbursement Approval Agent developed as part of the AI Developer Candidate Assignment.

The agent evaluates employee travel reimbursement claims using company reimbursement policies, performs rule-based validation through tools, leverages a Large Language Model (LLM) for reasoning, and returns structured reimbursement decisions.

The implementation uses LangGraph for agent orchestration and LangChain tools for deterministic policy evaluation.

---

## Features

- Accepts travel reimbursement claims in JSON format
- Policy-aware claim evaluation
- LangGraph-based agent workflow
- LLM reasoning using Groq Llama 3.3 70B
- Tool calling for business rules
- Automatic reimbursement calculation
- Manual Review handling for ambiguous claims
- Structured JSON output
- Dashboard summarizing claim decisions

---

## Tech Stack

- Python 3.10+
- LangGraph
- LangChain
- LangChain Groq
- Groq API
- Pandas
- Matplotlib
- Pydantic

---

## Project Workflow

```
Claim JSON
      │
      ▼
LangGraph Agent
      │
      ▼
Tool Selection
      │
      ├── Category Validation
      ├── Receipt Validation
      ├── Per-Diem Checker
      ├── Approval Threshold
      └── Timeliness Check
      │
      ▼
LLM Reasoning
      │
      ▼
Structured Decision
      │
      ▼
Dashboard + JSON Output
```

---

## Implemented Policy Rules

### Eligible Categories

- Airfare (Economy)
- Lodging
- Meals
- Ground Transport
- Conference Fees

### Ineligible Categories

- Spa
- Minibar
- Alcohol
- Movies
- Shopping
- Gifts

### Per-Diem Limits

| Category | Limit |
|-----------|-------|
| Meals | $75/day |
| Lodging | $200/night |
| Ground Transport | $50/day |

### Receipt Rules

- Receipt required for airfare
- Receipt required for lodging
- Receipt required for expenses above $25

### Approval Rules

| Total Amount | Decision |
|--------------|----------|
| ≤ $500 | Auto Approve |
| $500 – $2000 | Manager Approval |
| > $2000 | Manual Review |

### Timeliness Rule

Claims submitted after 30 days are routed to Manual Review.

---

## Business Exception

Business-class and First-class airfare are automatically routed to **Manual Review** instead of being rejected, since prior approval may exist.

---

## Tools Implemented

- check_category
- check_receipts
- check_per_diem_limits
- check_timeliness
- check_approval_threshold

---

## Project Structure

```
Travel-Reimbursement-Agent/

│
├── charan_kurakula.ipynb
├── README.md
└── screenshots (optional)
```

---

## Installation

Clone the repository

```bash
git clone https://github.com/<your-username>/travel-reimbursement-agent.git
```

Install dependencies

```bash
pip install langchain
pip install langgraph
pip install langchain-groq
pip install pandas
pip install matplotlib
pip install pydantic
```

or

```bash
pip install -r requirements.txt
```

---

## Environment Variable

Create a Groq API Key from

https://console.groq.com/keys

Set the API key

Windows

```cmd
set GROQ_API_KEY=your_api_key
```

Linux/Mac

```bash
export GROQ_API_KEY=your_api_key
```

Or directly inside the notebook

```python
import os

os.environ["GROQ_API_KEY"] = "YOUR_API_KEY"
```

---

## Running the Notebook

1. Open the notebook

```
charan_kurakula.ipynb
```

2. Run all cells sequentially.

3. The notebook will

- Load sample claims
- Execute LangGraph workflow
- Call policy tools
- Generate explanations
- Produce structured JSON
- Display dashboard

---

## Output

Each claim returns

```json
{
  "claim_id": "...",
  "decision": "...",
  "approved_amount": 0,
  "deducted_amount": 0,
  "missing_docs": [],
  "policy_refs": [],
  "confidence": 0.98,
  "explanation": "...",
  "tools_used": []
}
```

---

## Dashboard

The notebook generates an inline dashboard showing

- Decision breakdown
- Approved vs Deducted Amounts

using Matplotlib.

---

## Design Decisions

- LangGraph orchestrates the agent workflow.
- LangChain Tools perform deterministic business rule validation.
- Groq Llama 3.3 70B provides reasoning and explanation generation.
- Rule-based tools are preferred for financial calculations to ensure deterministic outputs.
- Manual Review is prioritized whenever policy ambiguity exists.

---

## Assumptions

- Claims are provided in valid JSON format.
- Receipt metadata is available.
- Policy rules are static.
- Currency is USD.
- Only the provided sample claims are evaluated.

---

## Limitations

- No OCR-based receipt verification.
- No duplicate claim detection.
- No database persistence.
- No authentication.
- No real-time API deployment.

---

## Future Improvements

- OCR-based receipt extraction
- RAG-based policy retrieval
- Vector database integration
- PostgreSQL backend
- FastAPI deployment
- Streamlit dashboard
- Multi-agent workflow
- Duplicate reimbursement detection
- Human-in-the-loop approval
- Audit logging

---

## Author

**Charan Kurakula**

AI/ML Engineer

Specialization:

- Generative AI
- LangGraph
- LangChain
- Agentic AI
- LLM Applications
- RAG Systems
