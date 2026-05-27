# Multi-Agent Research System using LangChain

A lightweight research assistant built with LangChain, Streamlit, and multi-agent orchestration. This project demonstrates how to combine search, scraping, writing, and critique agents into a single research workflow.

## 🚀 What it does

- Uses a search agent to gather recent, relevant sources
- Scrapes selected URLs for in-depth content
- Drafts a structured research report using an LLM
- Critiques the report automatically for quality and improvement
- Provides a polished Streamlit interface for interactive exploration

## 🧩 Technology Stack

- Python 3.11
- Streamlit for the web UI
- LangChain for agent orchestration
- OpenAI `gpt-4o-mini` via `langchain-openai`
- Tavily Search API for web search
- BeautifulSoup / Readability / Trafilatura for robust scraping
- `python-dotenv` for environment configuration
- `rich` for optional logging/debugging

## 📁 Project Structure

- `app.py` — Streamlit application entrypoint
- `main.py` — CLI-style pipeline runner example
- `src/agents/agent.py` — search/reader agent builders plus writer/critic chains
- `src/pipeline/pipeline.py` — research pipeline orchestration
- `src/tools/tools.py` — web search and URL scraping tool definitions
- `requirements.txt` — Python dependencies

## ⚙️ Installation

### Using Conda

```bash
conda create -n langagent python=3.11 -y
conda activate langagent
pip install -r requirements.txt
```

### Using Virtualenv

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

## 🔧 Configuration

Create a `.env` file in the project root with the following keys:

```env
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
```

> `OPENAI_API_KEY` is required for `langchain-openai`.
> `TAVILY_API_KEY` is required for web search via the `tavily-python` client.

## ▶️ Running the App

### Streamlit UI

```bash
streamlit run app.py
```

Then open the local URL shown in the terminal.

### CLI pipeline

```bash
python main.py
```

This runs the `run_research_pipeline` flow on a sample topic defined in `main.py`.

## 🏗️ Architecture Overview

1. `app.py`
   - Defines the Streamlit UI and visual styling
   - Imports agent builders and chains from `src.agents.agent`
   - Allows users to interact with the multi-agent research system in a browser

2. `src/agents/agent.py`
   - Builds the search agent using `web_search`
   - Builds the reader agent using `scrape_url`
   - Defines the writer chain to generate reports
   - Defines the critic chain to evaluate output quality

3. `src/tools/tools.py`
   - `web_search(query)` uses Tavily to return titles, URLs, and snippets
   - `scrape_url(url)` fetches a page and extracts readable content with multiple fallback strategies

4. `src/pipeline/pipeline.py`
   - Coordinates the research workflow:
     - Step 1: Search for relevant resources
     - Step 2: Scrape the top URL
     - Step 3: Generate a research report
     - Step 4: Critique the report

## 💡 Notes

- The current pipeline is optimized for research-style topics and report generation.
- The scraper returns up to 5,000 characters of extracted content per page.
- The system is easily extensible with additional agents, tools, or alternative search sources.

## 🧪 Customization

- Swap `gpt-4o-mini` for another OpenAI model in `src/agents/agent.py`
- Add new LangChain tools for database search, file ingestion, or knowledge retrieval
- Extend `pipeline.py` with additional validation, summarization, or fact-checking steps

## 📄 License

This project is available under the terms of the `LICENSE` file.
