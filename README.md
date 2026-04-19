# LangGraph Chatbot with Search & Push Notifications

A conversational AI chatbot built with [LangGraph](https://github.com/langchain-ai/langgraph) and [Gradio](https://www.gradio.app/), powered by OpenAI's `gpt-4o-mini`. The agent can search the web in real-time and send push notifications to your phone via Pushover.

## Features

- **Web Search** — Uses Google Serper API to answer questions with up-to-date information
- **Push Notifications** — Sends notifications to your phone via the Pushover API
- **Conversational Memory** — Retains context across turns within a session using LangGraph's `MemorySaver`
- **Gradio UI** — Simple chat interface served locally in your browser

## Architecture

The agent is built as a LangGraph state graph:

```
START → chatbot ⇄ tools
```

- `chatbot` node: calls `gpt-4o-mini` with tools bound
- `tools` node: executes whichever tool the LLM selected (search or push)
- Conditional edges route between chatbot and tools automatically

## Prerequisites

- Python 3.14+
- [uv](https://github.com/astral-sh/uv) package manager

## Setup

1. **Clone the repo and install dependencies:**
   ```bash
   uv sync
   ```

2. **Create a `.env` file** with the following keys:
   ```env
   OPENAI_API_KEY=your_openai_api_key
   SERPER_API_KEY=your_serper_api_key
   PUSHOVER_TOKEN=your_pushover_app_token
   PUSHOVER_USER=your_pushover_user_key
   ```

3. **Run the app:**
   ```bash
   uv run main.py
   ```

   Then open the Gradio URL shown in the terminal (typically `http://127.0.0.1:7860`).

## Dependencies

| Package | Purpose |
|---|---|
| `langgraph` | Agent graph orchestration |
| `langchain-openai` | OpenAI LLM integration |
| `langchain-community` | Google Serper search utility |
| `langchain-core` | Tool definitions |
| `gradio` | Chat UI |
| `python-dotenv` | Environment variable loading |
| `requests` | Pushover HTTP calls |
