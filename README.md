### AI FAQ Assistant

Short, descriptive title: AI FAQ Assistant for GitHub Repos

One-liner: An agent that answers questions about a GitHub repo (DataTalksClub/faq) using semantic search and an LLM.

Badges: ![Python](https://img.shields.io/badge/Python-3.12-blue) ![Streamlit](https://img.shields.io/badge/Streamlit-1.50.0-ff4b4b) ![License](https://img.shields.io/badge/License-MIT-green)

## Overview

This project provides an interactive assistant that can answer questions about the `DataTalksClub/faq` repository. It indexes the repository content locally, performs fast semantic search over the indexed documents, and uses an LLM to craft concise, source-linked answers in the UI.

- **Problem**: Manually searching through documentation is slow and error-prone.
- **Solution**: Ask questions in natural language; the app searches the indexed materials and responds with cited sources.
- **Why it's useful**: Quickly discover relevant FAQ entries, links, and references without navigating the entire repo.

Optional visuals: Add a screenshot or GIF of the Streamlit app here.

## Installation

### Requirements
- **Python**: 3.12
- **Package manager**: Poetry
- **Environment variable**: `OPENAI_API_KEY`

### Steps
1) Clone the repository and navigate to the app directory:

```bash
git clone <your-fork-or-repo-url>
cd /aihero/projects/app
```

2) Install dependencies with Poetry:

```bash
poetry install
```

3) Set your OpenAI API key (required by `pydantic-ai` / OpenAI client):

```bash
export OPENAI_API_KEY="sk-..."   # macOS/Linux
```

If you see a Watchdog performance message on macOS, you can optionally install:

```bash
xcode-select --install
poetry run pip install watchdog
```

Dependencies are defined in `pyproject.toml`:
- `streamlit` (UI)
- `pydantic-ai` (agent orchestration)
- `openai` (LLM client)
- `minsearch` (lightweight search over the index)
- `requests`, `python-frontmatter`

## Usage

### Run the app

```bash
poetry run streamlit run app.py
```

Then open the local URL shown in the terminal (e.g., `http://localhost:8501`). The app will:
- Index the `DataTalksClub/faq` repository content using `ingest.py`
- Initialize an agent with a search tool
- Let you ask questions and receive answers with source links

### Configuration
- The repository owner/name are currently set in `app.py` within `init_agent()`:
  - `repo_owner = "DataTalksClub"`
  - `repo_name = "faq"`
- To target a different repo, adjust these values and modify the filter function if needed.

## Features
- **Streamlit chat UI** with chat history
- **On-demand indexing** of the target GitHub repository
- **Semantic search** over indexed content (via `minsearch`)
- **LLM agent** (via `pydantic-ai` + OpenAI) with file citation guidance
- **Local logging** of interactions in `logs/`

Roadmap (optional):
- Add persistent vector store
- Add multi-repo support and repo picker
- Add retrieval metrics and evaluation

## Contributing
Contributions are welcome!

Guidelines:
- Create a feature branch from `main`
- Keep edits focused and include concise descriptions
- Ensure code is formatted and free of linter errors
- Open a PR describing the change and rationale

If you adopt a style guide or additional checks, add them here and/or link to `CONTRIBUTING.md`.

## Tests
If you add tests under `tests/`, you can run them with your preferred runner. For example, using `pytest` (if added to dependencies):

```bash
poetry run pytest -q
```

Currently there are no test suites provided; feel free to contribute.

## Deployment (optional)

### Streamlit Community Cloud
1) Push your repo to GitHub
2) Create an app on Streamlit Cloud and point it to `app.py`
3) Set `OPENAI_API_KEY` as a secret in the Streamlit app settings

### Containerization (future)
If you add a `Dockerfile`, you could run:

```bash
docker build -t ai-faq-assistant .
docker run -p 8501:8501 -e OPENAI_API_KEY=... ai-faq-assistant
```

## FAQ / Troubleshooting
- "ImportError: cannot import name 'SearchTool'" — The project now defines a local `SearchTool` inside `search_agent.py`. Ensure you're running the latest code and restart the app.
- "Watchdog warning on macOS" — Install Xcode CLT and `watchdog` as shown above for better file change detection.
- "OpenAI authentication error" — Confirm `OPENAI_API_KEY` is set in your environment.

## Credits / Acknowledgments
- Inspired by RAG-style assistants and documentation chatbots
- Uses `Streamlit`, `pydantic-ai`, `openai`, and `minsearch`
- Thanks to the `DataTalksClub` community for the `faq` repository

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.


