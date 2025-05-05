
## 👨‍💻 About the Project

This project was created to assist **DevOps Engineers** in **automating the generation of multi-stage Dockerfiles** using Large Language Models (LLMs). By reducing the time spent on boilerplate setup and promoting best practices, this tool enables teams to quickly containerize applications across a wide variety of languages and frameworks.

It supports both **local LLMs** (via Ollama) and **hosted models** (via Google Gemini), giving developers the flexibility to work securely offline or at scale via APIs.

Maintained by **Terrence Ncube**
📧 Email: [terrencencube593@gmail.com](mailto:terrencencube593@gmail.com)
🔗 GitHub: [@TerrenceDevOps](https://github.com/TerrenceDevOps)

## 🛠️ What’s Next?

We plan to extend this project into a **Log Analysis Assistant** that will run **after the Dockerized application is deployed to Kubernetes (K8s)**.
This next phase will include:

* 🔍 AI-assisted log parsing and anomaly detection
* 📊 Real-time observability suggestions


Stay tuned!
👉 For now, documentation below is focused on creating the Docker image for any language so it can be containerized.
---

# 🤖 AI-Assisted DevOps with Local LLMs (via Ollama)

This project leverages **local Large Language Models (LLMs)** with the **Ollama API** to automate DevOps tasks like:
- 🐳 Generating multi-stage Dockerfiles
- 💻 Generating shell scripts
- ⚙️ Assisting with general DevOps tasks using AI — securely and offline

> Built to help developers automate and accelerate workflows without external API dependencies.

---
| File                          | Description                                                                 |
| ----------------------------- | --------------------------------------------------------------------------- |
| `generate_dockerfile.py`      | LLM-powered Dockerfile generator using **Ollama**                           |
| `ollama_launcher.sh`          | Shell script to pull & launch LLaMA models via **Ollama CLI**               |
| `google_gemini_dockerfile.py` | Hosted LLM-powered Dockerfile generator using **Gemini (Google AI Studio)** |
## 🔧 Features

- ✅ Local LLM support (e.g., LLaMA 3, DeepSeek, Mistral via Ollama)
- 🔐 Works fully offline – no OpenAI or Gemini API required (unless configured)
- 📦 Secure multi-stage Dockerfile generation using AI
- 📁 Log analyzer and shell assistant powered by LLMs
- 💸 Cost-effective: no per-token API billing when using local models

---

## 🚀 Getting Started
#Install ollama and Start the Ollama server.

Ollama Start to get it running

Download Ollama from: https://ollama.com/download

After installation, verify it:

ollama --version

Pull a Local LLM

You can explore more models at: https://ollama.com/library

ollama pull llama3:8b

Install Python Dependencies

pip install ollama


### 1️⃣ Install Python and Create a Virtual Environment

```bash
python -m venv venv
.\venv\Scripts\activate       # For Windows
source venv/bin/activate     # For macOS/Linux
python -m pip install --upgrade pip

💡 Usage: Generate Dockerfiles with LLM
import ollama

PROMPT = """
ONLY generate an ideal multistage Dockerfile for {language}. Follow best practices:
- Use a base image
- Install dependencies
- Set working directory
- Add source code
- Define entrypoint
Do not add any explanations. Just the Dockerfile.
"""

def generate_dockerfile(language):
    response = ollama.chat(
        model='llama3:8b',
        messages=[{'role': 'user', 'content': PROMPT.format(language=language)}]
    )
    return response['message']['content']

if __name__ == '__main__':
    lang = input("Enter language: ")
    print("\nGenerated Dockerfile:\n")
    print(generate_dockerfile(lang))


🧠 Using Google AI Studio (Gemini Version)
model = genai.GenerativeModel('gemini-1.5-pro')

PROMPT = """
Generate an ideal multistage Dockerfile for {language}. 
Use best practices. Do not add explanations — just output the Dockerfile.
"""

def generate_dockerfile(language):
    response = model.generate_content(PROMPT.format(language=language))
    return response.text

language = input("Enter language: ")
print(generate_dockerfile(language))


##Sample Output (for Python):
FROM python:3.12-slim AS base
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

FROM base AS build
COPY . .
CMD ["python", "app.py"]



Why Local LLMs
| Feature             | Local LLMs (Ollama) | Hosted LLMs (OpenAI, Gemini) |
| ------------------- | ------------------- | ---------------------------- |
| ✅ Privacy           | Full Control        | Data leaves your machine     |
| 💸 Cost             | Free after install  | Pay-per-token                |
| 🌐 Internet Needed  | No                  | Yes                          |
| ⚙️ Setup Complexity | Medium              | Simple (API-based)           |







