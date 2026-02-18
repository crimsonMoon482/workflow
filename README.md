```markdown
# 🎨 AI Advertisement Image Generator (n8n Workflow)

A production-ready **Text → Cinematic Prompt → AI Image** automation workflow built with **n8n**, **Anthropic Claude**, and **HuggingFace Image Generation API**.

This workflow converts a simple text description into a high-quality, advertisement-grade AI-generated image.

---

## 🚀 Features

- ✅ Webhook-based API endpoint
- ✅ AI-powered cinematic prompt engineering
- ✅ Structured JSON parsing & validation
- ✅ HuggingFace image generation (PNG output)
- ✅ Clean modular architecture
- ✅ Advertisement-optimized visual output

---

## 🏗 Workflow Architecture

```

Webhook → Edit Fields → AI Agent (Claude)
→ Code (JSON Extract + Prompt Builder)
→ HuggingFace Image Generation

````

---

## 📦 Nodes Overview

### 1️⃣ Webhook (`/text-to-image`)
- Method: `POST`
- Receives user text input.

Example request:

```json
{
  "text": "Luxury gold watch on black marble table"
}
````

---

### 2️⃣ Edit Fields Node

Transforms request body into:

```json
{
  "prompt": "{{ $json.body.text }}"
}
```

---

### 3️⃣ AI Agent (LangChain + Claude Sonnet 4.5)

Role:

* Converts simple text into a professional cinematic advertisement prompt.

Model:

* `claude-sonnet-4-5-20250929`

Outputs strict JSON:

```json
{
  "prompt": "Main description",
  "style": "Visual style",
  "lighting": "Lighting details",
  "camera": "Camera settings",
  "quality": "Resolution & detail"
}
```

---

### 4️⃣ Code Node (JavaScript)

Purpose:

* Extract JSON from LLM output
* Safely parse
* Generate `full_prompt`

Final output example:

```json
{
  "full_prompt": "Luxury gold watch, photorealistic, cinematic rim lighting, 85mm lens, ultra detailed 8k..."
}
```

---

### 5️⃣ HuggingFace Image Generation

Endpoint:

```
POST https://router.huggingface.co/nscale/v1/images/generations
```

Headers:

```
Accept: image/png
Content-Type: application/json
```

Body:

```json
{
  "inputs": "{{ $json.full_prompt }}",
  "parameters": {
    "num_inference_steps": 5
  },
  "option": {
    "use_cache": false
  }
}
```

Returns:

* `image/png`

---

## 🔑 Required Credentials

### 1️⃣ HuggingFace API

* Create token: [https://huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)
* Add credential in n8n as `huggingFaceApi`

### 2️⃣ Anthropic API

* Required for Claude Sonnet 4.5
* Add credential as `Anthropic account`

---

## 🌐 Usage

1. Activate workflow
2. Send POST request:

```
POST https://your-domain/webhook/text-to-image
```

Body:

```json
{
  "text": "Premium sports car in desert at sunset"
}
```

Response:

* Generated PNG image

---

## ⚙ Customization

### Increase Quality

Change:

```json
"num_inference_steps": 5
```

To:

```json
"num_inference_steps": 20
```

---

### Add Negative Prompt

Extend body:

```json
{
  "inputs": "...",
  "parameters": {
    "negative_prompt": "blurry, watermark, text"
  }
}
```

---

## 🛠 Production Recommendations

* Add error handling after Code node
* Add logging for malformed AI responses
* Add image storage (S3 / Drive / CDN)
* Add rate limiting
* Add caching layer
* Increase inference steps for premium users

---

## 📌 Use Cases

* Product advertisements
* E-commerce visuals
* Social media creatives
* Marketing campaigns
* SaaS AI image backend
* Automated content generation systems

---

## 🔮 Future Improvements

* Model selection switch
* Upscaling node
* Background removal
* Image storage automation
* SaaS API wrapper
* Analytics tracking

---

## 📜 License

Use commercially at your own discretion.
Ensure compliance with:

* HuggingFace API Terms
* Anthropic API Terms

---

## 👨‍💻 Built With

* n8n
* Anthropic Claude
* HuggingFace Router API
* Custom JavaScript parsing logic

---

## 💡 Author

Generated for automated AI-powered advertisement image workflows.


