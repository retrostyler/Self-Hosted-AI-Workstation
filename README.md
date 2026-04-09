# Self-Hosted AI Workstation

A personal GPU-powered AI workstation running 10+ open-source LLMs locally — zero cloud cost, full privacy, publicly accessible via Cloudflare Tunnel.

[![Demo](https://img.shields.io/badge/Live%20Demo-Visit-blue?style=for-the-badge)](https://drive.google.com/file/d/1ySLEu5-VC77qbfSXm1RnrxKlJImO9sKh/view?usp=sharing)

## 📽️ Demo

> A full walkthrough of the workstation — model switching, local inference speed, and guest access.

[Watch Demo Video](https://drive.google.com/file/d/1ySLEu5-VC77qbfSXm1RnrxKlJImO9sKh/view?usp=sharing)

<!-- OR if you upload to YouTube/Loom -->


---

## ⚡ Performance

| Metric | Value |
|---|---|
| GPU | NVIDIA RTX 4060 (8GB VRAM) |
| Inference Speed | 40+ tokens/sec (local) |
| Models Running | 10+ simultaneously available |
| Monthly Cost | ₹0 |
| Public Access | Via Cloudflare Tunnel |

---

## 🧠 Models Available

| Model | Parameters | Use Case |
|---|---|---|
| Llama 3.1 8B | 8B | General purpose |
| Mistral 7B | 7B | Fast reasoning |
| Phi-3 Mini | 3.8B | Lightweight tasks |
| CodeLlama | 7B | Code generation |
| Gemma 2 | 9B | Instruction following |
| DeepSeek Coder | 6.7B | Code + debugging |
| *...and more* | | |


---

## 🚀 Setup

### Prerequisites
- Windows 10/11 with NVIDIA GPU
- [Ollama](https://ollama.com) installed
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed
- [cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/) installed

### Installation

**1. Install Ollama and pull models**
```bash
# Install Ollama from https://ollama.com
ollama pull llama3.1
ollama pull mistral
ollama pull phi3
ollama pull codellama
```

**2. Run Open WebUI with Docker**
```bash
docker run -d \
  -p 3000:8080 \
  --add-host=host.docker.internal:host-gateway \
  -v open-webui:/app/backend/data \
  --name open-webui \
  --restart always \
  ghcr.io/open-webui/open-webui:main
```

**3. Start everything with one click**

Double-click `start.bat` (see below) or run manually:
```bash
ollama serve
cloudflared tunnel --url http://localhost:3000
```

---

## 🔁 One-Click Startup Script

Save this as `start.bat` and run it as Administrator:

```bat
@echo off
echo =============================
echo  Starting AI Workstation...
echo =============================

echo [1/3] Starting Ollama...
start "" ollama serve

timeout /t 3 /nobreak > nul

echo [2/3] Starting Open WebUI...
start "" docker start open-webui

timeout /t 5 /nobreak > nul

echo [3/3] Starting Cloudflare Tunnel...
start "" cloudflared tunnel --url http://localhost:3000

echo =============================
echo  All services started!
echo  Open WebUI: http://localhost:3000
echo =============================
pause
```

---

## 🔗 Cloud API Integrations

In addition to local models, the workstation integrates:
- **Groq API** — for ultra-fast cloud inference fallback
- **OpenRouter** — access to 100+ models via unified API

All accessible through the same Open WebUI interface.

---

## 🔒 Access Control

- Guest access enabled with read-only permissions
- Admin panel restricted to local network
- Cloudflare Tunnel provides HTTPS encryption end-to-end
- No ports exposed directly through router (zero port forwarding)

## 🛠️ Tech Stack

- **Ollama** — Local LLM runtime with CUDA support
- **Open WebUI** — Browser-based chat interface
- **Docker** — Container for Open WebUI
- **Cloudflare Tunnel** — Secure public exposure without port forwarding
- **Groq API / OpenRouter** — Cloud fallback APIs
- **NVIDIA RTX 4060** — GPU for local inference



