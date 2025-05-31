# 🎥 Longform YouTube Video Automation using n8n

This project automates the creation and upload of longform YouTube videos on an **hourly schedule** using [n8n](https://n8n.io/). It integrates Google Sheets, OpenAI (LLM), json2video, and YouTube.

---

## 📌 Workflow Overview

The automation is broken down into 4 main sections:

1. **INPUT**  
2. **GENERATE VIDEO AND AUDIO**  
3. **GENERATE FULL VIDEOS**  
4. **HANDLE ERRORS**  
5. **FINAL OUTPUT**

---

## 🧠 INPUT

1. **Schedule Trigger** – Triggers the workflow hourly.
2. **Google Sheets** – Fetches input rows for video topics.
3. **Basic LLM Chain** – Uses OpenAI Chat Model (GPT) and Structured Output Parser to:
   - Generate YouTube video scripts
   - Create prompts for visuals

---

## 🎞️ GENERATE VIDEO AND AUDIO

1. **Google Sheets1** – Stores the structured script and prompts for tracking and reference.

---

## 🎬 GENERATE FULL VIDEOS

1. **HTTP Request** – Sends data to the json2video API to generate the video.
2. **Wait (120 sec)** – Waits for the video to finish rendering.
3. **HTTP Request1** – Polls or retrieves the completed video file.

---

## ⚠️ HANDLE ERRORS

1. **Switch** – Branches the logic depending on success/failure.
2. **Wait (30 sec)** – Adds a buffer before retries or error handling.
3. **Error Log** – Saves error details back into a Google Sheet.

---

## 📤 FINAL OUTPUT

1. **Error Log1** – Writes success/failure to Google Sheet.
2. **HTTP Request2** – Sends final confirmation or download link.
3. **YouTube Upload** – Publishes the generated video to your YouTube channel.
4. **Error Log2** – Logs any final upload issues for debugging.

---

## 📷 Screenshots

> You can upload and embed screenshots of your n8n workflow here:

```markdown
![n8n Workflow Screenshot](images/n8n-youtube-workflow.png)
```

---

## 🔧 Requirements

- n8n (Self-hosted or n8n.cloud)
- Google Sheets API access
- OpenAI API key
- json2video API key
- YouTube Data API (OAuth2 credential for uploads)

---

## 🚀 How to Run

1. Clone this repo or replicate the structure in your local n8n.
2. Create necessary credentials in n8n (Google Sheets, OpenAI, etc.).
3. Set up a Google Sheet with the required input structure.
4. Configure the video generation templates and parameters.
5. Start the workflow — it will run every hour automatically!

---

## 📦 Output

- Auto-generated video scripts
- Narrated longform YouTube videos
- Fully automated publishing to YouTube

---

## 🙌 Credits

Made using:
- [n8n.io](https://n8n.io/)
- [OpenAI](https://platform.openai.com/)
- [json2video](https://json2video.com/)
- [Google APIs](https://console.cloud.google.com/)

---

## 🧠 Author

**Your Name Here**  
💼 Role: Automation Developer  
🔗 GitHub: [@yourusername](https://github.com/yourusername)

---
