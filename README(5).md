#  Longform YouTube Video Automation using n8n

This project automates the creation and upload of longform YouTube videos on an **hourly schedule** using [n8n](https://n8n.io/). It integrates Google Sheets, OpenAI (LLM), json2video, and YouTube.

---

##  Workflow Overview

The automation is broken down into 4 main sections:

1. **INPUT**  
2. **GENERATE VIDEO AND AUDIO**  
3. **GENERATE FULL VIDEOS**  
4. **HANDLE ERRORS**  
5. **FINAL OUTPUT**

---

## INPUT

1. **Schedule Trigger** – Triggers the workflow hourly.
2. **Google Sheets** – Fetches input rows for video topics.[image alt](img_https://github.com/adaezeilo/youtube-ai-agent/blob/1f84ea414ed980b1398ce59c5fd9c02d9d9f7ad5/google%20sheets.png)
3. **Basic LLM Chain** – Uses OpenAI Chat Model (GPT) and Structured Output Parser to:[image alt](image_https://github.com/adaezeilo/youtube-ai-agent/blob/5bffc6c18f14101beee7300eb2aef0254aecf18c/basic%20llm%20chain.png)
   - Generate YouTube video scripts
   - Create prompts for visuals

---

## GENERATE VIDEO AND AUDIO

1. **Google Sheets1** – Stores the structured script and prompts for tracking and reference.[image alt](image_https://github.com/adaezeilo/youtube-ai-agent/blob/80757d0c34185fb85b50c0e1b8292d8179b61161/google%20sheet1.png)

---

## GENERATE FULL VIDEOS

1. **HTTP Request** – Sends data to the json2video API to generate the video.[image alt](image_https://github.com/adaezeilo/youtube-ai-agent/blob/8182ce896f6f9d1b643ccb244f7b38a4a22d4f53/http%20request.png)
2. **Wait (120 sec)** – Waits for the video to finish rendering.
3. **HTTP Request1** – Polls or retrieves the completed video file.[image alt](image_https://github.com/adaezeilo/youtube-ai-agent/blob/2c46b48c03660bb23732452ecfd5e39527a17c25/Http%20request1.png)

---

## HANDLE ERRORS

1. **Switch** – Branches the logic depending on success/failure.
2. **Wait (30 sec)** – Adds a buffer before retries or error handling.
3. **Error Log** – Saves error details back into a Google Sheet.[image alt](image_https://github.com/adaezeilo/youtube-ai-agent/blob/b6c4651eeb4a8a5b09c50c77426fe64321b0e7ed/Error%20log.png)

---

## FINAL OUTPUT

1. **Error Log1** – Writes success/failure to Google Sheet.[image alt](image_https://github.com/adaezeilo/youtube-ai-agent/blob/a428c9f07e2538e994f33dcbe6df3ba96b0aa0c0/error%20log1.png)
2. **HTTP Request2** – Sends final confirmation or download link.[image alt](image-https://github.com/adaezeilo/youtube-ai-agent/blob/210a63621fb12bce8f9ede041f34c645d65021bf/http%20request2.png)
3. **YouTube Upload** – Publishes the generated video to your YouTube channel.[image alt](image_https://github.com/adaezeilo/youtube-ai-agent/blob/433fa33535f3ca44ae7aa394d7b0276c694178dc/YOUTUBE.png)
4. **Error Log2** – Logs any final upload issues for debugging.[image alt](image_https://github.com/adaezeilo/youtube-ai-agent/blob/1131b7c52ca2a86975ff569d98439d4e880eb00d/ERROR%20LOG2.png)

---

## Screenshots

> You can upload and embed screenshots of your n8n workflow here:

```markdown
![n8n Workflow Screenshot](images/n8n-youtube-workflow.png)
```

---

## Requirements

- n8n (Self-hosted or n8n.cloud)
- Google Sheets API access
- OpenAI API key
- json2video API key
- YouTube Data API (OAuth2 credential for uploads)

---

##  How to Run

1. Clone this repo or replicate the structure in your local n8n.
2. Create necessary credentials in n8n (Google Sheets, OpenAI, etc.).
3. Set up a Google Sheet with the required input structure.
4. Configure the video generation templates and parameters.
5. Start the workflow — it will run every hour automatically!

---

##  Output

- Auto-generated video scripts
- Narrated longform YouTube videos
- Fully automated publishing to YouTube

---

## Credits

Made using:
- [n8n.io](https://n8n.io/)
- [OpenAI](https://platform.openai.com/)
- [json2video](https://json2video.com/)
- [Google APIs](https://console.cloud.google.com/)

---



---
