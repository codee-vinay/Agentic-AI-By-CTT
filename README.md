# Career & Placement Assistant — Agentic AI Day 1

A beginner-friendly learning project that adapts the mentor's Day 1 exercise to a student career and placement guidance scenario. It preserves the original learning objectives: connecting to a Groq-hosted chat model through LangChain, defining a domain-specific system prompt, calling Prompt Guard, and building an interactive Jupyter interface.

## What it demonstrates

- **LLM integration:** call `openai/gpt-oss-120b` through LangChain's `ChatGroq` integration.
- **System prompting:** define the assistant's role, scope, response style, and knowledge boundaries.
- **Prompt safety:** classify user prompts with `meta-llama/llama-prompt-guard-2-22m`.
- **Guarded workflow:** run Prompt Guard before the chat model; flagged prompts are blocked, and classifier errors do not silently bypass the check.
- **Interactive UI:** use Jupyter widgets to test the assistant and the standalone classifier.

> **Scope:** This is an educational prototype, not an official placement portal. It does not access live vacancies, college records, eligibility databases, or application systems. Verify institution-specific details with the placement cell and current requirements with official company sources.

## Project structure

```text
Career-Placement-Assistant/
├── Day-01/
│   └── career_placement_assistant_day1.ipynb
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

## Setup

1. Install Python 3.10 or newer.
2. Clone this repository and open a terminal in the project folder.
3. (Recommended) Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   ```

   Windows PowerShell: `.venv\Scripts\Activate.ps1`  
   macOS/Linux: `source .venv/bin/activate`

4. Install dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

5. Copy `.env.example` to `.env` and add your own Groq API key:

   ```env
   GROQ_API_KEY=your_groq_api_key_here
   ```

6. Start Jupyter from the project root:

   ```bash
   jupyter notebook
   ```

7. Open `Day-01/career_placement_assistant_day1.ipynb` and run the cells from top to bottom. The dependency cell can also locate `requirements.txt` if the notebook is opened with the `Day-01` folder as the working directory.

## How the guarded workflow works

1. A student enters a career or placement question.
2. Prompt Guard returns a classification score.
3. If the score is at or above `0.5`, the prompt is flagged and the chat model is not called.
4. If it is below `0.5`, the question is sent to the Career & Placement Assistant.
5. If Prompt Guard fails or returns an unexpected response, the workflow stops and displays an error rather than silently skipping the check.

The `0.5` threshold is retained from the starter exercise for demonstration. It has not been calibrated for production use. Classifiers can produce false positives and false negatives; this check is not a complete security boundary.

## Security notes

- `.env` is ignored by Git; only `.env.example` should be committed. Never publish API keys, passwords, OTPs, or private student records.
- If an API key has been shared or exposed, revoke/rotate it in the provider console.
- User text is HTML-escaped before being rendered in the notebook interface.
- Do not treat Prompt Guard as a guarantee that an input is safe.
- The assistant must not invent job openings, deadlines, salary figures, placement statistics, or eligibility rules.

## Current scope and limitations

This is a guarded conversational LLM application and an introductory step toward Agentic AI. It does **not** yet implement autonomous planning, tool execution, persistent memory, multi-agent coordination, live job search, or application submission.

## Troubleshooting

- **Missing API key:** ensure `.env` exists in the project root and contains `GROQ_API_KEY=...`.
- **Model/API error:** check that the API key is active and that the selected model is available to your Groq account.
- **Prompt Guard response validation error:** inspect the raw response and check the model/API response format; the notebook intentionally stops rather than guessing a score.
- **Widget not displayed:** install the listed dependencies in the same Python environment used by Jupyter, then restart the kernel.
