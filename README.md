# ⬡ GraphRAG System — Lab 11

> **Knowledge Graph × Retrieval Augmented Generation**  
> A production-quality, self-contained Graph RAG demo powered by Claude.

---

## 🚀 Quick Start

1. Open `index.html` in any modern browser (Chrome/Firefox/Edge)
2. Click **⚙ API KEY** in the top-right header
3. Paste your Anthropic API key (`sk-ant-...`)
4. Type a question or click a sample query
5. Watch the graph light up as retrieval traverses the knowledge graph!

> **No install required.** Pure HTML/JS/CSS — single file, zero dependencies to install.

---

## 🧠 What is GraphRAG?

Traditional RAG (Retrieval Augmented Generation) uses **vector similarity** to find relevant documents. It works for semantic search but fails at:
- Multi-hop reasoning ("Who manages Alice's colleagues?")
- Relationship-aware queries ("How is GraphRAG connected to LangChain?")
- Structured entity lookups ("List all people at NeuroSys")

**GraphRAG** replaces the vector lookup with **knowledge graph traversal**:

```
User Query
    ↓
Entity Extraction  →  Find seed nodes matching query keywords
    ↓
Graph Traversal    →  BFS/DFS expand N hops from seeds
    ↓
Context Assembly   →  Format subgraph (nodes + relationships) as text
    ↓
LLM Generation     →  Claude answers using ONLY the graph context
    ↓
Grounded Answer    →  Accurate, relationship-aware, hallucination-reduced
```

---

## 🗺️ Knowledge Graph Schema

### Node Types
| Type | Color | Count | Description |
|------|-------|-------|-------------|
| `person` | 🔵 Cyan | 7 | People with skills and roles |
| `company` | 🟠 Orange | 3 | Organizations |
| `tech` | 🟣 Violet | 6 | Technologies and frameworks |
| `project` | 🟡 Yellow | 3 | Active projects |
| `concept` | 🟢 Green | 2 | Abstract concepts |

### Relationship Types
```
WORKS_AT    WORKS_ON    KNOWS       MANAGES
EXPERT_IN   USES        INTEGRATES  BUILT_WITH
BENCHMARKS  PRODUCES    STORES      POWERS
IMPROVES    COMPETES_WITH
```

---

## ⚙️ Features

### Graph Visualization
- **Force-directed layout** with D3.js v7 physics simulation
- **Drag nodes** to reorganize the graph
- **Zoom & pan** (scroll / pinch to zoom)
- **Hover tooltips** with entity details and skills
- **Click a node** to auto-populate a query about it

### GraphRAG Pipeline
- **Multi-hop traversal**: configurable depth 1–4 hops
- **Score-based seed detection**: weighted keyword matching against labels, descriptions, and skills
- **Type filters**: show/hide node types on the graph
- **Cypher query display**: shows the equivalent Neo4j Cypher query
- **Node Inspector**: displays retrieved nodes with relationships

### Chat Interface
- **Step-by-step pipeline visualization** (Extract → Traverse → Generate)
- **Typewriter animation** for generated answers
- **Per-message metadata**: seeds, nodes, edges, depth, time
- **Export chat** to .txt file
- **Sample queries** to get started

### Particle System
- **Glowing particles** travel along traversed edges during retrieval
- **Trailing glow effects** highlight active graph paths

---

## 📐 Architecture

```
index.html
├── GRAPH_DATA          ← Embedded knowledge graph (nodes + edges)
├── TYPE_CFG            ← Visual config per node type  
├── EDGE_CFG            ← Color per relationship type
├── retrieveSubgraph()  ← BFS traversal engine
├── buildCypher()       ← Cypher query generator
├── askClaude()         ← Anthropic API call
├── initGraph()         ← D3.js force simulation
├── spawnParticles()    ← Canvas particle system
└── handleQuery()       ← Pipeline orchestrator
```

---

## 🔧 Customisation

### Add your own nodes
Open `index.html` and find `GRAPH_DATA.nodes`. Add entries like:
```js
{ 
  id: "maya",
  label: "Maya Singh",
  type: "person",          // person | company | tech | project | concept
  desc: "Your description here",
  skills: ["Python","ML"]  // optional, for person nodes
}
```

### Add relationships
In `GRAPH_DATA.edges`:
```js
{ s: "maya", t: "neurosys", r: "WORKS_AT" }
```

### Change traversal behaviour
- **Depth**: Adjust with the sidebar slider (1–4 hops)
- **Scoring**: Edit `retrieveSubgraph()` — tweak the score weights
- **System prompt**: Edit the `system` field in `askClaude()`

---

## 🔑 API Key

The app uses the **Anthropic Claude API** (`claude-sonnet-4-20250514`).

- Key is stored in **browser localStorage** only
- Never transmitted except to `api.anthropic.com`
- Get your key: https://console.anthropic.com

---

## 📚 References

- [Neo4j GraphRAG Manifesto](https://neo4j.com/blog/genai/graphrag-manifesto/)
- [Microsoft GraphRAG Paper](https://arxiv.org/abs/2404.16130)
- [LangChain Neo4j Integration](https://python.langchain.com/docs/integrations/graphs/neo4j_cypher/)
- [LlamaIndex KnowledgeGraphIndex](https://docs.llamaindex.ai/en/stable/examples/index_structs/knowledge_graph/)
- [D3.js Force Simulation](https://d3js.org/d3-force)

---

## 🏫 Lab 11 — Learning Objectives

1. Understand the difference between **vector RAG** and **Graph RAG**
2. Implement **entity extraction** from natural language queries
3. Perform **multi-hop graph traversal** (BFS)
4. **Assemble structured context** for LLM consumption
5. Ground LLM outputs in **explicit knowledge graph facts**
6. Visualise the retrieval process interactively

---

*Built for Lab 11 · Graph RAG · Implemented with D3.js + Claude API*
