# private-llm-with-api

This is the fastest and simplest way to run a local AI chatbot with a powerful interface. You’ll use Ollama to run large language models locally, Open WebUI as a sleek front-end, and Docker to tie it all together. Optional: use Ngrok to access it remotely, perfect for building your own AI tools or API.

## ✅ Requirements

- Windows 10 or 11
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Ollama for Windows](https://ollama.com/download)
- [Ngrok (Free account)](https://ngrok.com/)
- Terminal access (CMD or PowerShell)

---

## 1. 🧠 Install Ollama (Local LLM Backend)

1. Download Ollama for Windows:  
   👉 https://ollama.com/download

2. After installation, open CMD and test if it's working:

```bash
ollama list
```

If you get a list of models or an empty result, you're good!

---

## 2. 🤖 Choose and Download an AI Model

1. Browse models here:  
   👉 https://ollama.com/library

2. Pick one, for example: `deepseek-coder:6.7b`

3. In CMD, run:

```bash
ollama run deepseek-coder:6.7b
```

> This will download the model and start it once.  
> You can also use `ollama pull <model>` if you only want to download.

Check installed models with:

```bash
ollama list
```

---

## 3. 🐳 Install Docker Desktop for Windows

- Download from: https://www.docker.com/products/docker-desktop
- Install and launch it
- Verify Docker is working:

```bash
docker ps
```

---

## 4. 🌐 Run Open WebUI via Docker (Connected to Your Ollama)

### 🧼 Optional: Clean previous container

```bash
docker stop open-webui
docker rm open-webui
```

### ▶️ Start Open WebUI (all in one line):

```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always -e OLLAMA_BASE_URL=http://host.docker.internal:11434 ghcr.io/open-webui/open-webui:main
```

What this does:
- Runs Open WebUI on port `3000`
- Connects it to your **native Ollama** via `host.docker.internal`
- Keeps your settings via Docker volume

---

## 5. 💬 Use Open WebUI in Your Browser

1. Go to:  
   👉 [http://localhost:3000](http://localhost:3000)

2. In the interface:
   - Select one of your local models (like `deepseek-r1`)
   - Start chatting, coding, asking questions, etc.

---

## 6. 🌍 Optional: Make Your WebUI Public with Ngrok

### 🔽 1. Download Ngrok

Get it from: https://ngrok.com/download  
Extract it to a folder (e.g., `C:\ngrok`)

---

### 🔐 2. Connect Your Ngrok Account

Get your token here: https://dashboard.ngrok.com/get-started/setup

Then run:

```bash
ngrok config add-authtoken <your-token>
```

---

### 🚀 3. Start Tunnel to Open WebUI

```bash
ngrok http http://localhost:3000
```

You’ll see something like:

```
Forwarding  https://xxxxx.ngrok-free.app  ->  http://localhost:3000
```

> This is your **public temporary link**. You can access your AI chat from anywhere!

