# LangGraph Learning

Hands-on notebooks for learning LangGraph basics, tool calling, and memory patterns using LangChain with both cloud and local LLM providers.

## Contents

- `simple_graph.ipynb`: basic LangGraph workflow concepts.
- `chatbot.ipynb`: chatbot flow with LangGraph and chat models.
- `chatbot_tool_call.ipynb`: tool-calling chatbot examples (stock-price tool).
- `chatbot_with_memory.ipynb`: memory/state examples in conversational graphs.
- `main.ipynb`: additional notebook experiments.

## Requirements

- Python 3.10+
- `uv` (recommended) or `pip`
- Optional for local models: [Ollama](https://ollama.com) running on `http://localhost:11434`

## Setup

Using `uv`:

```bash
uv sync
```

Or install dependencies manually:

```bash
uv pip install -e .
```

## Environment Variables

Create a `.env` file for provider keys when using cloud models:

```env
GOOGLE_API_KEY=your_key_here
```

If using only Ollama, API keys are not required.

## Run Notebooks

Start Jupyter:

```bash
uv run jupyter notebook
```

Then open any notebook in this repository.

## Using Ollama

1. Install and start Ollama.
2. Pull a model, for example:

```bash
ollama pull llama3.2
```

3. In notebook code, use:

```python
from langchain_ollama import ChatOllama
llm = ChatOllama(model="llama3.2", base_url="http://localhost:11434")
```

## Notes

- Do not commit secrets (such as `.env` with real API keys).
- The project already ignores `.venv`; consider also ignoring `.env` if not already excluded in your global git config.
