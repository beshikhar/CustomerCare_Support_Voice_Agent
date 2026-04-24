# Customer Support Voice Agent

![Python](https://img.shields.io/badge/Python-3.9+-blue) ![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o-green) ![Streamlit](https://img.shields.io/badge/UI-Streamlit-red) ![Qdrant](https://img.shields.io/badge/VectorDB-Qdrant-purple) ![Firecrawl](https://img.shields.io/badge/Crawler-Firecrawl-orange)

An OpenAI SDK powered customer support agent that delivers voice-powered responses to questions about your knowledge base using GPT-4o and TTS capabilities. The system crawls documentation websites with Firecrawl, processes content into a searchable vector knowledge base using Qdrant, and provides both text and voice responses to user queries.

> A complete step-by-step tutorial with code walkthroughs, explanations, and best practices is available at [theunwindai.com](https://www.theunwindai.com/p/build-a-customer-support-voice-agent).

---

## Features

### Knowledge Base Creation

- Crawls documentation websites via Firecrawl
- Indexes content in Qdrant vector database
- Generates embeddings for semantic search using FastEmbed
- Preserves document structure and metadata
- Supports crawling up to 5 pages per run by default

### Agent Team

- **Documentation Processor** — analyzes documentation content and generates clear, concise responses to user queries
- **TTS Agent** — converts text responses into natural-sounding speech with appropriate pacing and emphasis

### Voice Customization

Supports all OpenAI TTS voices:

```
alloy  ash  ballad  coral  echo  fable  onyx  nova  sage  shimmer  verse
```

### Interactive Interface

- Clean Streamlit UI with sidebar configuration
- Real-time documentation search and response generation
- Built-in audio player with download capability
- Progress indicators for system initialization and query processing

---

## Getting Started

### Prerequisites

- Python 3.9 or higher
- OpenAI API key — [platform.openai.com](https://platform.openai.com)
- Qdrant Cloud account and API key — [cloud.qdrant.io](https://cloud.qdrant.io)
- Firecrawl API key for documentation crawling

---

## Installation

**1. Clone the repository and navigate to the project directory.**

```bash
git clone https://github.com/beshikhar/CustomerCare_Support_Voice_Agent.git
cd CustomerCare_Support_Voice_Agent
```

**2. Install dependencies.**

```bash
pip install -r requirements.txt
```

**3. Run the Streamlit application.**

```bash
streamlit run ai_voice_agent_docs.py
```

---

## Usage

1. Open the application and enter your API credentials in the sidebar (OpenAI, Qdrant URL and key, Firecrawl).
2. Input the documentation URL you want to build a knowledge base from.
3. Select your preferred TTS voice from the dropdown.
4. Click **Initialize System** to crawl and index the documentation.
5. Ask questions in the query box and receive both text and voice responses.

---

## Architecture

### Knowledge base pipeline

Firecrawl scrapes the target documentation URL (up to 5 pages by default), preserving document structure and metadata. Each page is chunked, embedded using FastEmbed, and upserted into a Qdrant collection for semantic retrieval.

### Query pipeline

User queries are embedded at query time and matched against the Qdrant collection. Retrieved chunks are passed to the Documentation Processor agent, which generates a structured response using GPT-4o. The TTS Agent then converts that response to audio using OpenAI's TTS model with the selected voice.

### Voice generation

Speech is synthesized using OpenAI's TTS models with natural pacing and emphasis. The resulting audio file is surfaced in the Streamlit UI with a built-in player and a download option.

---

## Configuration

| Parameter   | Default  | Description                                        |
|-------------|----------|----------------------------------------------------|
| `max_pages` | `5`      | Maximum documentation pages crawled per run        |
| `tts_voice` | `alloy`  | OpenAI TTS voice used for speech generation        |
| `model`     | `gpt-4o` | OpenAI model used for response generation          |

---

