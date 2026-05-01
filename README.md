# LangGraph Tutorial

Hands-on notebooks and scripts for LangGraph patterns: graphs, chat models (Google GenAI / Ollama), tool calling, memory, LangSmith traces, and a small human-in-the-loop demo.

## Contents

Notebooks:

- [`simple_graph.ipynb`](simple_graph.ipynb) — Basic LangGraph flow.
- [`chatbot.ipynb`](chatbot.ipynb) — Chatbot-oriented graph examples.
- [`chatbot_tool_call.ipynb`](chatbot_tool_call.ipynb) — Tool calling (e.g. stock lookup) with conditional routing.
- [`chatbot_with_memory.ipynb`](chatbot_with_memory.ipynb) — Persistence / memory in conversational graphs.
- [`langsmith.ipynb`](langsmith.ipynb) — Same stack as above, wired for experimentation with traces (needs LangSmith env vars).
- [`main.ipynb`](main.ipynb) — Extra experiments.

Scripts:

- [`HIT.py`](HIT.py) — Minimal LangGraph agent with tools and **`interrupt`** (human-in-the-loop approval). Runs against local Ollama.
- [`main.py`](main.py) — Separate entry-point script (see file for behaviour).

## Requirements

- Python 3.10+
- [uv](https://docs.astral.sh/uv/) (recommended) or `pip`
- For local models: [Ollama](https://ollama.com) on `http://localhost:11434`

## Setup

From the repo root:

```bash
uv sync
```

Or install as an editable package:

```bash
uv pip install -e .
```

## Environment variables

Create a **`.env`** in the project root for keys and tracing. `.env` is listed in `.gitignore` — do not commit secrets.

Typical `.env`:

```env
# Google Gemini (LangChain google_genai) — omit if you use only Ollama
GOOGLE_API_KEY=your_key_here

# LangSmith (optional tracing)
LANGCHAIN_TRACING_V2=true
LANGSMITH_API_KEY=your_langsmith_key
LANGSMITH_PROJECT=langgraph-learning
```

If you use **only Ollama**, cloud API keys are not required (LangSmith stays optional).

## Running notebooks

```bash
uv run jupyter notebook
```

Pick the kernel that uses this project’s `.venv`.

## Using Ollama

1. Install and start Ollama.
2. Pull a model, for example:

```bash
ollama pull llama3.2
```

3. In code:

```python
from langchain_ollama import ChatOllama

llm = ChatOllama(
    model="llama3.2",
    base_url="http://localhost:11434",
    temperature=0,
)
```

Use `langchain_ollama` (not `langchain_community`) when you need **`bind_tools`** support with Ollama.

## Running `HIT.py`

Requires Ollama and a matching model name inside the script:

```bash
uv run python HIT.py
```

The graph uses `interrupt()` for user approval; how you resume depends on your LangGraph usage (see comments in the file).

## Dependencies (see `pyproject.toml`)

Core stack includes `langgraph`, `langchain`, `langchain-google-genai`, `langchain-ollama`, `langsmith`, `python-dotenv`, `notebook`, and `ollama` (Python client).
