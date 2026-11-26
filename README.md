# AI Research Agent

AI Research Agent collects recent AI-related news from RSS feeds, filters the
most relevant articles, and uses a local Ollama model to create a research
digest.

## Features

- Collects articles from AI, machine learning, and technology news sources
- Deduplicates articles and limits the number selected from each source
- Ranks articles by topic relevance and publication date
- Generates a Chinese-language digest using a local Ollama model
- Saves each digest as a timestamped Markdown file in `reports/`

## Requirements

- Python 3
- [Ollama](https://ollama.com/) running locally
- The configured Ollama model (default: `qwen3.5:9b`)
- Python packages:
  - `requests`
  - `feedparser`

## Setup

Create and activate a virtual environment:

```sh
python3 -m venv .venv
source .venv/bin/activate
```

Install the dependencies:

```sh
python -m pip install requests feedparser
```

Download and run the configured model:

```sh
ollama pull qwen3.5:9b
ollama serve
```

If Ollama is already running, the `ollama serve` command is not necessary.

## Usage

Run the agent from the project directory:

```sh
python agent.py
```

The agent performs these steps:

1. Fetches recent articles from the configured RSS feeds.
2. Removes duplicate links and ranks articles by relevance and recency.
3. Sends the selected articles to the local Ollama API for analysis.
4. Writes the resulting digest to a file such as:
   `reports/2026-11-26-10-00-00-AI-Research.md`.

The research digest contains up to five significant developments, their
technical implications, relevant research, source links, and an overall
industry outlook.

## Configuration

Edit the constants near the top of `agent.py` to customize:

- `OLLAMA_URL`: local Ollama API endpoint
- `MODEL`: model used to generate the report
- `RSS_FEEDS`: monitored news sources
- `MAX_ARTICLES`: maximum number of articles analyzed
- `MAX_ARTICLES_PER_SOURCE`: per-source article limit
- `FEED_TIMEOUT`: RSS request timeout
- `INTERESTS`: keywords used to rank article relevance

## Project Structure

```text
.
├── agent.py
├── reports/
│   └── YYYY-MM-DD-HH-MM-SS-AI-Research.md
└── README.md
```

## Notes

- An Internet connection is required to retrieve RSS feeds.
- Ollama must be running and the configured model must be installed.
- Generated reports are based only on the collected article summaries.
- Unavailable feeds are skipped with a warning so other sources can still be
  processed.
