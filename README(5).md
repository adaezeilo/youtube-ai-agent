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

1. **Schedule Trigger** – Triggers the workflow hourly.![Schedule Trigger](https://github.com/adaezeilo/youtube-ai-agent/blob/72ca42cd3bc2573c90b09bb11727189af096ba53/schedule%20trig.png)
2. **Google Sheets** – Fetches input rows for video topics.![Google Sheets](https://github.com/adaezeilo/youtube-ai-agent/blob/1f84ea414ed980b1398ce59c5fd9c02d9d9f7ad5/google%20sheets.png)
3. **Basic LLM Chain** – Uses OpenAI Chat Model (GPT) and Structured Output Parser to:![Basic LLM Chain](https://github.com/adaezeilo/youtube-ai-agent/blob/5bffc6c18f14101beee7300eb2aef0254aecf18c/basic%20llm%20chain.png)
4.  - Generate a table with these columns:  
     `id`, `idea`, `caption`, `channel_style_prompt`, `character_style_prompt`, `production_status`, `final_output`, `publishing_status`, `error_log`
   - Column details and rules:
     - `id`: Start from 1, increment by 1
     - `idea`: Short YouTube title (7–10 words), matching the user-defined **Topic**
     - `caption`: 3-line description  
       - Line 1: about the video  
       - Line 2: about the channel  
       - Line 3: call to action ending with 3 relevant hashtags  
     - `channel_style_prompt`: Expanded version of channel keywords (5–10 words)
     - `character_style_prompt`: Unique, detailed visual character concept
     - `production_status`: Always “for production”
     - `final_output`: Leave blank
     - `publishing_status`: Always “pending”
     - `error_log`: Leave blank

   - **User Inputs** include:  
     - `Topic`: Main theme for the video (e.g. AI Automation)  
     - `COUNT`: Number of ideas to generate  
     - `CHANNEL KEYWORDS`: Relevant phrases for the channel's content

4. **Prompts Generator (Template)** – Formats the output for video rendering:  
   ```
   VideoTitle:{{$json.idea}}
   VideoDescription:{{$json.caption}}
   ```

---
   - Generate YouTube video scripts![idea](https://github.com/adaezeilo/youtube-ai-agent/blob/9c3a219d234ab1bb4d9d7267cd776b98a147806c/idea.png)
   - Create prompts for visuals![structuredoutput paser](https://github.com/adaezeilo/youtube-ai-agent/blob/05dfd71ca7f2cc17ea533bf7fe5fcecaacb6a2b9/Structuredoutput%20paser.png)

---

## GENERATE VIDEO AND AUDIO

1. **Google Sheets1** – Stores the structured script and prompts for tracking and reference![Google Sheets1](https://github.com/adaezeilo/youtube-ai-agent/blob/80757d0c34185fb85b50c0e1b8292d8179b61161/google%20sheet1.png)

---

## GENERATE FULL VIDEOS

1. **HTTP Request** – Sends data to the json2video API to generate the video.![HTTP Request](https://github.com/adaezeilo/youtube-ai-agent/blob/8182ce896f6f9d1b643ccb244f7b38a4a22d4f53/http%20request.png)
2. **Wait (120 sec)** – Waits for the video to finish rendering.![Wait(120)](https://github.com/adaezeilo/youtube-ai-agent/blob/f69882315fcc675e9a8486e8b518b126e392e3b9/wait(120).png)
3. **HTTP Request1** – Polls or retrieves the completed video file.![HTTP Request1](https://github.com/adaezeilo/youtube-ai-agent/blob/2c46b48c03660bb23732452ecfd5e39527a17c25/Http%20request1.png)

---

## HANDLE ERRORS

1. **Switch** – Branches the logic depending on success/failure.![Switch](https://github.com/adaezeilo/youtube-ai-agent/blob/f226cb09cca4edd7d6eabc5cecd74e4ef001424a/switch.png)
2. **Wait (30 sec)** – Adds a buffer before retries or error handling.![Wait(30)](https://github.com/adaezeilo/youtube-ai-agent/blob/a6d0e6effdf1913d22a2e8013caa47b494b2dfe8/wait(30).png)
3. **Error Log** – Saves error details back into a Google Sheet.![Error Log](https://github.com/adaezeilo/youtube-ai-agent/blob/b6c4651eeb4a8a5b09c50c77426fe64321b0e7ed/Error%20log.png)

---

## FINAL OUTPUT

1. **Error Log1** – Writes success/failure to Google Sheet.![Error Log1](https://github.com/adaezeilo/youtube-ai-agent/blob/a428c9f07e2538e994f33dcbe6df3ba96b0aa0c0/error%20log1.png)
2. **HTTP Request2** – Sends final confirmation or download link.![HTTP Request2](https://github.com/adaezeilo/youtube-ai-agent/blob/210a63621fb12bce8f9ede041f34c645d65021bf/http%20request2.png)
3. **YouTube Upload** – Publishes the generated video to your YouTube channel![YouTube Upload](https://github.com/adaezeilo/youtube-ai-agent/blob/433fa33535f3ca44ae7aa394d7b0276c694178dc/YOUTUBE.png)
4. **Error Log2** – Logs any final upload issues for debugging.![Error Log2](https://github.com/adaezeilo/youtube-ai-agent/blob/1131b7c52ca2a86975ff569d98439d4e880eb00d/ERROR%20LOG2.png)

---


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


## Important Notes

- Make sure your local n8n instance is connected to **ngrok** so that it can be accessed from external services.
- When generating API keys for Google Sheets in the Google Cloud Console, select **"Desktop App"** instead of **"Web App"** to simplify the OAuth2 process.

---
