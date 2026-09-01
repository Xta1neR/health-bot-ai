# 🩺 HealthBot — AI Patient Education Assistant

HealthBot is an AI-powered patient-education assistant designed to provide clear, accessible, and source-grounded information about health and medical topics.

It combines **Groq-powered health-domain classification**, **Tavily web retrieval**, **Mistral for medical summarization and evaluation**, **LangGraph for workflow orchestration**, and **Gradio for the interactive web interface**.

> ⚠️ **Medical Disclaimer:** HealthBot is an educational tool and is not a substitute for professional medical advice, diagnosis, or treatment. Always consult a qualified healthcare professional for personal medical concerns.

## ✨ Features

- 🛡️ **Health-only guardrail** — dynamically classifies questions using Groq and rejects non-health questions.
- 🔎 **Web-grounded medical retrieval** — uses Tavily to retrieve relevant medical information.
- 🧠 **Patient-friendly summaries** — Mistral converts retrieved information into accessible explanations.
- 📚 **Trusted-source filtering** — retrieved results are filtered before generation.
- 🧠 **Comprehension check** — generates a question based on the summary.
- ⭐ **AI answer grading** — evaluates answers using an A–E grading system.
- 💬 **Feedback and evidence** — explains the grade using evidence from the summary.
- 🔒 **Duplicate-click protection** — buttons are disabled during API operations.
- 🔄 **Fresh sessions** — choosing “Yes, learn more” reloads the application into a clean session.
- 🛡️ **Multiple safety layers** — domain classification, retrieval grounding, LLM safety instructions, and an educational disclaimer.

## 🏗️ Architecture

```text
User Question
      │
      ▼
Groq Health Classifier
      │
 ┌────┴─────┐
 │          │
NON-HEALTH HEALTH
 │          │
 ▼          ▼
Reject   Tavily Search
             │
             ▼
      Trusted Sources
             │
             ▼
       Retrieval Context
             │
             ▼
          Mistral
             │
             ▼
     Patient Summary
             │
             ▼
   Comprehension Question
             │
             ▼
       Patient Answer
             │
             ▼
          Mistral
             │
             ▼
      A–E Evaluation
             │
             ▼
      Feedback + Evidence
```

## 🧩 Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| LangGraph | Workflow orchestration |
| LangChain | LLM/retrieval integrations |
| Mistral | Primary LLM |
| Groq | Health-domain classification |
| Tavily | Web retrieval |
| Gradio | Interactive web UI |
| python-dotenv | Environment variables |
| Jupyter Notebook | Development and execution |

## 🔐 API Configuration

Create a `.env` file in the project root:

```env
MISTRAL_API_KEY=your_mistral_api_key
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
```

**Never commit `.env` or API keys to GitHub.**

Recommended `.gitignore`:

```gitignore
.env
venv/
__pycache__/
.ipynb_checkpoints/
*.pyc
```

## 🚀 Installation

### 1. Clone the repository

```bash
git clone https://github.com/Xta1neR/health-bot-ai.git
cd health-bot
```

### 2. Create a virtual environment

Windows:

```powershell
python -m venv venv
.
env\Scripts\Activate.ps1
```

If PowerShell activation is unavailable:

```cmd
venv\Scripts ctivate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure API keys

Create `.env` and add your Mistral, Groq, and Tavily keys.

### 5. Open the notebook

Open the `.ipynb` file in VS Code and select the Python/Jupyter kernel belonging to `venv`.

### 6. Run the project

Use **Run All**.

The final notebook cell launches the Gradio application:

```python
healthbot_ui.launch(
    inbrowser=True,
    theme=gr.themes.Soft()
)
```

## 🧪 Example

### Health question

```text
What is vitiligo?
```

Expected flow:

```text
Groq → HEALTH
       ↓
Tavily → Medical sources
       ↓
Mistral → Patient-friendly summary
       ↓
Mistral → Comprehension question
       ↓
User answer
       ↓
Mistral → Grade + feedback + evidence
```

### Non-health question

```text
What is Python?
```

Expected:

```text
Groq → NON-HEALTH
       ↓
HealthBot refuses the request
```

No unnecessary medical retrieval or generation is performed.

## ⭐ Grading System

| Grade | Meaning |
|---|---|
| ⭐⭐⭐⭐⭐ | **A Grade — Great Understanding** |
| ⭐⭐⭐⭐ | **B Grade — Good Understanding** |
| ⭐⭐⭐ | **C Grade — We Can Get a Better Answer** |
| ⭐⭐ | **D Grade — Try Reading the Summary Again** |
| ⭐ | **E Grade — Did You Even Read the Summary?** |

The evaluation is based on the generated HealthBot summary.

## 🛡️ Safety Design

HealthBot uses multiple safeguards:

1. **Groq health-domain classification**
2. **Medical web retrieval and source filtering**
3. **Mistral safety instructions**
4. **Educational medical disclaimer**
5. **No diagnosis or personalized treatment decisions**

The LLM is instructed not to answer non-health questions even if an irrelevant request reaches the generation stage.

## 💰 Token-Conscious Design

Non-health questions are stopped early:

```text
User
 ↓
Groq classification
 ↓
NON-HEALTH
 ↓
STOP
```

Only health questions continue to:

```text
Tavily → Mistral
```

The interface also prevents repeated button clicks while requests are running.

## 📁 Project Structure

```text
health-bot/
│
├── HealthBot.ipynb
├── requirements.txt
├── instruction.md
├── README.md
├── .env
└── .gitignore
```

> `.env` should remain local and must not be committed.

## 🎯 Learning Objectives

This project demonstrates practical implementation of:

- Large Language Models
- Prompt Engineering
- Retrieval-Augmented Generation (RAG)
- LangChain
- LangGraph
- LLM routing
- AI safety and guardrails
- Web retrieval
- State-driven workflows
- LLM-based evaluation
- Gradio application development
- Environment-variable security
- Token-conscious AI application design

## ⚠️ Medical Disclaimer

HealthBot is intended **only for general patient education**.

It must not be used to:

- Diagnose medical conditions
- Replace a healthcare professional
- Prescribe medication
- Modify medication or treatment
- Make personalized medical decisions
- Handle medical emergencies

For personal medical concerns, consult a qualified healthcare professional.

In an emergency, contact your local emergency medical services.

## 👨‍💻 Author

**Rituraj Goswami**

AI / Machine Learning Project

Built with Python, LangGraph, Mistral, Groq, Tavily, LangChain, and Gradio.
