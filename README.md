# GraphRAG System

> A Knowledge Graph-Powered Retrieval-Augmented Generation system with interactive D3.js visualization, multi-model LLM support, graph algorithms, and a real-time query pipeline.

## Overview

GraphRAG combines the structured reasoning power of **knowledge graphs** with the natural language capabilities of **large language models**. Unlike traditional RAG (which retrieves flat text chunks), GraphRAG traverses entity relationships to provide contextually rich, accurate answers.

**Pipeline:**
1. **Extract** -- Identify seed entities from the user's query using NLP scoring
2. **Traverse** -- Perform multi-hop BFS through the knowledge graph
3. **Generate** -- Send structured graph context (with conversation memory) to an LLM

## Features (28 Total)

### Core RAG Pipeline
| Feature | Description |
|---|---|
| Multi-Hop BFS Traversal | Configurable 1-4 hop depth graph traversal |
| Context-Aware Generation | Structured KG context passed to LLM for grounded answers |
| Cypher Query Preview | Auto-generated Neo4j Cypher equivalent for each traversal |
| Multi-Turn Conversation Memory | Maintains sliding window of 10 conversation exchanges |
| Response Confidence Score | Graph coverage-based scoring (% of nodes traversed) |

### Graph Algorithms
| Feature | Description |
|---|---|
| PageRank | Iterative PageRank (20 iterations, damping=0.85) with top-5 ranking display |
| Community Detection | Connected component analysis via BFS |
| Shortest Path Finder | BFS-based shortest path between any two nodes with visual highlighting |
| Degree Distribution Chart | Live bar chart showing node degree frequency |
| Graph Analytics Panel | Density, avg degree, max/min degree, component count |

### LLM Integration
| Feature | Description |
|---|---|
| Multi-Model Selector | Switch between Llama 3.3 70B, Mixtral 8x7B, and Gemma2 9B |
| Groq API Integration | Fast inference via Groq's OpenAI-compatible endpoint |
| Context Window Token Estimation | Approximate token count per query |
| Markdown Response Rendering | AI responses rendered as formatted markdown |

### Visualization
| Feature | Description |
|---|---|
| Interactive Force Graph | D3.js force-directed layout with drag, zoom, pan |
| Particle System | Animated particle trails along traversed edges |
| Blueprint Grid Canvas | Tech-style grid background behind the force graph |
| Live Node Search | Instant graph filtering matching labels, types, descriptions, skills |
| Graph Snapshot Export | High-res PNG export of the current graph state |
| Fullscreen Mode | Toggle fullscreen for the graph canvas (F11) |

### User Experience
| Feature | Description |
|---|---|
| Dark/Light Theme Toggle | Full CSS variable theming with localStorage persistence |
| Query History Panel | Persistent history with one-click re-run (up to 20 entries) |
| Copy to Clipboard | One-click copy for AI answers and Cypher queries |
| Response Rating System | GOOD/BAD rating buttons with cumulative statistics |
| Undo/Redo Navigation | Ctrl+Z / Ctrl+Shift+Z to navigate query history |
| Session Statistics Dashboard | Total queries, avg latency, token estimates, rating summary |
| Graph Data JSON Export | Export the full knowledge graph as a JSON file |
| Keyboard Shortcuts | Ctrl+K, Ctrl+/, Ctrl+Enter, Escape, F11 |

## Architecture

```
User Query
    |
    v
+----------------+     +---------------------+     +----------------+
|    EXTRACT     |---->|     TRAVERSE         |---->|   GENERATE     |
|                |     |                     |     |                |
| NLP keyword   |     | Multi-hop BFS on    |     | Groq API       |
| scoring to    |     | knowledge graph     |     | (Llama 3.3 /   |
| find seeds    |     | with depth 1-4      |     |  Mixtral /      |
+----------------+     +---------------------+     |  Gemma2)        |
                              |                    | + conv memory   |
                              v                    +----------------+
                     +---------------------+            |
                     |  ANALYZE/VISUALIZE  |            v
                     |  PageRank, Paths,   |     +----------------+
                     |  Communities, D3.js  |    | OUTPUT          |
                     +---------------------+     | Markdown + Meta |
                                                 | Conf% + Rating  |
                                                 +----------------+
```

## Tech Stack

- **Frontend**: Vanilla HTML/CSS/JavaScript (zero build step, single file)
- **Graph Engine**: D3.js v7 (force simulation, SVG rendering)
- **Algorithms**: PageRank, BFS shortest path, connected components, degree analysis
- **LLM Backend**: Groq API (OpenAI-compatible endpoint)
- **Markdown**: marked.js for response rendering
- **Export**: html2canvas for PNG snapshots
- **Fonts**: JetBrains Mono + Space Grotesk (Google Fonts)
- **Server**: Python (custom HTTP server with .env API key loading)

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

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| Ctrl + K | Focus the node search bar |
| Ctrl + Enter | Submit the current query |
| Ctrl + / | Open keyboard shortcuts help |
| Ctrl + Z | Undo (restore previous query) |
| Ctrl + Shift + Z | Redo query |
| F11 | Toggle fullscreen graph |
| Enter | Submit query (when input is focused) |
| Escape | Close modals or clear search |

## Knowledge Graph Schema

```
Person --WORKS_AT--> Company
Person --WORKS_ON--> Project
Person --KNOWS-----> Person
Person --MANAGES---> Person
Person --EXPERT_IN-> Tech/Concept
Person --USES------> Tech
Project -USES------> Tech
Project -BENCHMARKS> Concept
Tech ----INTEGRATES> Tech
```

## Customization

### Adding Nodes

```javascript
{ id: "unique_id", label: "Display Name", type: "person", desc: "Description", skills: ["skill1"] }
```

### Adding Relationships

```javascript
{ s: "source_id", t: "target_id", r: "RELATIONSHIP_TYPE" }
```

### Adding Node Types

```javascript
newtype: { fill: "#color", stroke: "#darker", icon: "X", textFill: "#color" }
```

## Project Structure

```
Graph-RAG/
+-- index.html      # Complete frontend (HTML + CSS + JS, ~2800 lines)
+-- server.py       # Python HTTP server with .env support
+-- .env            # API key configuration (gitignored)
+-- .gitignore      # Git ignore rules
+-- README.md       # This file
```

## Resume Line

> Built a GraphRAG system with 28 features including interactive D3.js knowledge graph visualization, PageRank/BFS graph algorithms, multi-model LLM integration (Groq), multi-turn conversation memory, response confidence scoring, and a real-time query pipeline with markdown rendering -- all in a zero-dependency, single-file frontend.

## License

MIT
