# AI Chatbot 🤖

A simple, secure web-based AI chatbot powered by Google's Gemini API.

## 🔗 Live Demo

[Try it here](https://negin-mohammadshahi.github.io/my-chatbot/)

## 📋 Overview

This project is a lightweight chatbot interface where users can type a message and get a response from Google's Gemini AI model. The frontend is built with plain HTML, CSS, and JavaScript — no frameworks required.

## 🏗️ Architecture

A key design goal of this project was **security**: API keys should never be exposed in client-side code. To achieve this, the app uses a proxy architecture:

```
Browser (HTML/JS)  →  Cloudflare Worker (holds the API key)  →  Google Gemini API
```

- The frontend never talks to Gemini directly.
- The Gemini API key is stored as an encrypted secret in Cloudflare Workers, never exposed to the browser or visible in the source code.
- The Worker forwards user messages to Gemini and returns only the AI's reply to the frontend.

## 🛠️ Tech Stack

- **Frontend:** HTML, CSS, vanilla JavaScript
- **Backend / Proxy:** [Cloudflare Workers](https://workers.cloudflare.com/) (serverless)
- **AI Model:** [Google Gemini API](https://ai.google.dev/) (`gemini-2.5-flash`)
- **Hosting:** GitHub Pages

## ✨ Features

- Clean, responsive chat interface
- Real-time messaging with the Gemini AI model
- Secure handling of API credentials (no exposed keys)
- Error handling with clear feedback

## 🚀 How It Works

1. The user types a message and hits send.
2. The frontend sends the message to a Cloudflare Worker endpoint.
3. The Worker attaches the secret API key and forwards the request to Google's Gemini API.
4. Gemini's response is returned to the Worker, which passes it back to the frontend.
5. The chatbot displays the AI's reply.

## 📁 Project Structure

```
my-chatbot/
└── index.html   # Frontend: chat UI + JavaScript logic
```
*(The Cloudflare Worker code that proxies requests to Gemini is deployed separately and is not included in this repository, since it contains the secret-handling logic.)*

## 🔮 Possible Improvements

- Add conversation memory (multi-turn context)
- Custom system prompts for domain-specific chatbots (support bots, tutoring bots, etc.)
- Voice input/output
- Markdown rendering for formatted AI responses

## 👤 Author

**Negin Mohammadshahi**
AI & Software Engineer
[Portfolio](https://negin-mohammadshahi.github.io/) | [LinkedIn](https://www.linkedin.com/in/negin-mohammadshahi-908b3a79) | [GitHub](https://github.com/negin-mohammadshahi)