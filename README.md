# Proyecto1_Redes_Remote_Server
---

# Remote MCP Server (FastMCP on Cloud Run)

A minimal **remote MCP server** implemented with **[FastMCP](https://github.com/lastmile-ai/fastmcp)** and ready to run:

- ✅ Locally (Python or Docker)
- ✅ In a container (Docker)
- ✅ On **Google Cloud Run** (serverless)

It exposes two simple example tools to verify connectivity:

- `add(a: int, b: int) -> int` — sum two integers
- `subtract(a: int, b: int) -> int` — subtract `b` from `a`

The server uses **`streamable-http`** transport and serves the MCP endpoint at **`/mcp`**.

---

## ✨ Features

- ⚡ **FastMCP** server over HTTP (`streamable-http`)
- 🔌 Clean `/mcp` endpoint for clients
- 🧰 Two example tools (**add**, **subtract**)
- 🐳 Production-ready **Dockerfile** (Python 3.13 + `uv`)
- ☁️ One-command deploy to **Cloud Run**
- 🧪 Included `test_server.py` to validate locally or against Cloud Run URL

---

## 📁 Project Structure

.
├─ server.py # FastMCP server (HTTP, /mcp)
├─ test_server.py # Simple FastMCP client to exercise tools
└─ Dockerfile # Container image (Python 3.13 slim + uv)

---

## 🧩 Requirements

- **Python 3.11+** (Docker image uses **3.13**)
- Internet access (to install dependencies)
- Optional: [`uv`](https://github.com/astral-sh/uv) for fast, reproducible installs
- Optional: **Google Cloud SDK** (`gcloud`) for Cloud Run deployment

> **Port binding:** Cloud Run injects `PORT`. This server binds to `0.0.0.0:${PORT}` (default `8080` locally).

---

## 🚀 Quick Start (Local, no Docker)

You can run the server **without Docker** using `uv` (recommended) or `pip`.

### Option A — Using `uv`

```bash
# Create & activate a virtual environment
uv venv
source .venv/bin/activate

# Install runtime dependency
uv pip install fastmcp

# Run the server (defaults to PORT=8080 if not set)
uv run python server.py
# Server listens on: http://127.0.0.1:8080/mcp
```

---

## ✅ Test Locally

In a second terminal:

```bash
# If needed, activate the same venv
python test_server.py
```

If you see connection errors, ensure the server is running and you’re using the correct URL: http://localhost:8080/mcp.

---

## ☁️ Deploy to Google Cloud Run

Make sure you have a GCP project selected, billing enabled, and both Cloud Run and Cloud Build APIs activated.

### Deploy from source:

```bash
gcloud run deploy mcp-server --no-allow-unauthenticated --region=us-central1 --source .
```

Using proxy:

```bash
gcloud run services proxy mcp-server --region=us-central1
```

---

## 🔧 Configuration

- PORT — (optional locally) The HTTP port to bind. Cloud Run sets this automatically.

- Host — The server binds to 0.0.0.0 to work in containers and Cloud Run.

- Transport — streamable-http (FastMCP). Endpoint path: /mcp.

---
