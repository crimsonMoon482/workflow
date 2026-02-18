# 🎨 AI Cinematic Advertisement Image Generator  
### n8n Workflow – Text → Professional Ad Prompt → AI Image

This workflow converts a simple text description into a **high-quality cinematic advertisement image** using:

- 🧠 Anthropic Claude (via LangChain Agent)
- 🧩 Custom JSON parsing (Code node)
- 🖼 HuggingFace Router Image Generation API
- 🌐 n8n Webhook as public API endpoint

---

# 🚀 Overview

This automation transforms basic input text into:

1. A professionally engineered advertising prompt
2. Structured JSON output (style, lighting, camera, quality)
3. A combined high-quality image prompt
4. A generated PNG image from HuggingFace

---

# 🏗 Workflow Architecture

Webhook (POST /text-to-image)
↓
Edit Fields (Extract Text)
↓
AI Agent (Claude – Cinematic Prompt Engineering)
↓
Code Node (Safe JSON Parse + Full Prompt Builder)
↓
HuggingFace Image Generation (PNG Output)
