# GraphRAG System

> A Knowledge Graph-Powered Retrieval-Augmented Generation system with interactive D3.js visualization, multi-model LLM support, and a real-time graph traversal engine.

## Overview

GraphRAG combines the structured reasoning power of **knowledge graphs** with the natural language capabilities of **large language models**. Unlike traditional RAG (which retrieves flat text chunks), GraphRAG traverses entity relationships to provide contextually rich, accurate answers.

**How it works:**
1. **Extract** — Identify seed entities from the user's query
2. **Traverse** — Perform multi-hop BFS through the knowledge graph
3. **Generate** — Send structured graph context to an LLM for answer synthesis

## Features

| Feature | Description |
|---|---|
| **Interactive Force Graph** | D3.js force-directed graph with drag, zoom, pan, and click-to-query |
| **Multi-Hop Traversal** | Configurable 1-4 hop depth BFS with real-time visual highlighting |
| **Multi-Model Support** | Switch between Llama 3.3 70B, Mixtral 8x7B, and Gemma2 9B via Groq API |
| **Live Node Search** | Instant graph filtering as you type — matches labels, types, descriptions, and skills |
| **Dark/Light Themes** | Toggle between dark and light modes with full CSS variable theming |
| **Markdown Responses** | AI responses rendered as formatted markdown with syntax highlighting |
| **Graph Snapshot Export** | Export the current graph state as a high-resolution PNG |
| **Query History** | Persistent query history with one-click re-run (localStorage) |
| **Keyboard Shortcuts** | `Ctrl+K` (search), `Ctrl+/` (help), `Ctrl+Enter` (send), `Escape` (close) |
| **Cypher Query Preview** | Auto-generated Neo4j Cypher equivalent for each graph traversal |
| **Particle Effects** | Animated particle system along traversed edges during retrieval |
| **Copy to Clipboard** | One-click copy for AI answers and generated Cypher queries |
| **Blueprint Grid Canvas** | High-tech grid background behind the force graph |

## Architecture

```
User Query
    │
    ▼
┌──────────────┐     ┌───────────────────┐     ┌──────────────┐
│   EXTRACT    │────▶│     TRAVERSE      │────▶│   GENERATE   │
│              │     │                   │     │              │
│ NLP keyword  │     │ Multi-hop BFS on  │     │ Groq API     │
│ scoring to   │     │ knowledge graph   │     │ (Llama 3.3 / │
│ find seed    │     │ with configurable │     │  Mixtral /    │
│ entities     │     │ depth (1-4 hops)  │     │  Gemma2)      │
└──────────────┘     └───────────────────┘     └──────────────┘
                              │
                              ▼
                     ┌───────────────────┐
                     │  VISUALIZE        │
                     │  D3.js highlights │
                     │  + particles      │
                     └───────────────────┘
```

## Tech Stack

- **Frontend**: Vanilla HTML/CSS/JavaScript (zero build step)
- **Graph Engine**: D3.js v7 (force simulation, SVG rendering)
- **LLM Backend**: Groq API (OpenAI-compatible endpoint)
- **Markdown**: marked.js for response rendering
- **Export**: html2canvas for PNG snapshots
- **Fonts**: JetBrains Mono + Space Grotesk (Google Fonts)
- **Server**: Python (custom HTTP server with .env support)

## Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/commitsbyaditya/Graph-RAG.git
cd Graph-RAG
```

### 2. Set up your API key

Create a `.env` file in the project root:

```
GROQ_API_KEY=gsk_your_key_here
```

Get a free API key at [console.groq.com](https://console.groq.com)

### 3. Run the server

```bash
python server.py
```

Open [http://localhost:8000](http://localhost:8000) in your browser.

## Knowledge Graph Schema

```
Person ──WORKS_AT──▶ Company
Person ──WORKS_ON──▶ Project
Person ──KNOWS─────▶ Person
Person ──MANAGES───▶ Person
Person ──EXPERT_IN─▶ Tech/Concept
Person ──USES──────▶ Tech
Project ─USES──────▶ Tech
Project ─BENCHMARKS▶ Concept
Tech ────INTEGRATES▶ Tech
```

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl + K` | Focus the node search bar |
| `Ctrl + Enter` | Submit the current query |
| `Ctrl + /` | Open keyboard shortcuts help |
| `Enter` | Submit query (when input is focused) |
| `Escape` | Close modals or clear search |

## Customization

### Adding Nodes

Add new entities to the `GRAPH_DATA.nodes` array in `index.html`:

```javascript
{ id: "unique_id", label: "Display Name", type: "person", desc: "Description", skills: ["skill1", "skill2"] }
```

### Adding Relationships

Add new edges to the `GRAPH_DATA.edges` array:

```javascript
{ s: "source_id", t: "target_id", r: "RELATIONSHIP_TYPE" }
```

### Adding Node Types

Extend `TYPE_CFG` with a new type configuration:

```javascript
newtype: { fill: "#color", stroke: "#darker", icon: "◈", textFill: "#color" }
```

## Project Structure

```
Graph-RAG/
├── index.html      # Complete frontend (HTML + CSS + JS)
├── server.py       # Python HTTP server with .env support
├── .env            # API key configuration (gitignored)
├── .gitignore      # Git ignore rules
└── README.md       # This file
```

## Resume Line

> Built a GraphRAG system featuring interactive D3.js knowledge graph visualization, multi-hop BFS traversal, multi-model LLM integration (Groq), and a real-time query pipeline with markdown rendering — all in a zero-dependency frontend.

## License

MIT
