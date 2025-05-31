
# 📘 README: Set Up YouTube AI Agent Automation on Local n8n

This guide walks you through setting up an automated long-form YouTube video pipeline using n8n on your local machine. It integrates OpenAI, ElevenLabs, json2video, image generators, and Google Drive.

---

## ✅ Requirements

- Local installation of **n8n**
- Accounts & API keys for:
  - **OpenAI**
  - **ElevenLabs**
  - **json2video**
  - **Google Drive**
- NodeJS & npm installed (for n8n)
- Internet access for fetching/generating assets

---

## 🧩 Step-by-Step Setup

### 🔹 Step 1: Install n8n Locally

```bash
npm install n8n -g
```

Launch n8n:
```bash
n8n
```

Open [http://localhost:5678](http://localhost:5678) in your browser.

### 🧩 Step 2: Create Credentials

#### OpenAI
- Go to Credentials → Create New → OpenAI
- Paste your API key

#### ElevenLabs
- Create New → HTTP Basic Auth or API Key
- Paste your ElevenLabs API key

#### json2video
- Use `x-api-key` as credential header

#### Google Drive
- Create OAuth2 credential and authenticate

---

### 🧠 Step 3: AI Agent - Script and Image Prompt Generation

1. Drag in **OpenAI** node
2. Use the `text-davinci-003` or `gpt-4` model
3. Prompt: *"Create a longform YouTube script and detailed image prompts for a topic..."*

### 📹 Step 4: Video Rendering with json2video

1. Use **HTTP Request** node
2. POST to: `https://api.json2video.com/render`
3. Payload:
```json
{
  "template": "Your_Template_ID",
  "clips": [...],
  "voicemodel": "elevenlabs",
  "voiceID": "AeRdCCkzvd23BpJoofk",
  "imagemodel": "flux-pro"
}
```

### 🔊 Step 5: Generate Audio (Optional if json2video handles it)

1. Use **HTTP Request** node
2. POST to ElevenLabs voice API
3. Save the returned audio URL

### 🖼 Step 6: Generate Images (Optional)

Use **OpenAI Image (DALL·E)** node or another generator.

### ☁️ Step 7: Export to Google Drive

1. Use **Google Drive** node
2. Upload `video.mp4` from json2video output

---

## 🚀 Final Step: Manual or Scripted Upload to YouTube

- Use YouTube Studio to upload manually
- Optional: Add automation using AutoHotKey or Puppeteer

---

## 📷 Example Screenshots

📌 *To be added manually by taking screenshots of each node configuration in n8n.*

---

## ✅ Tips

- Chain nodes properly with success outputs.
- Use `Set` or `Function` nodes to structure the json2video payload.
- Test each node individually before chaining.

---

Happy Automating! 🚀
