# AI Chatbot 🤖 — Python Debug Assistant

A secure, specialized AI chatbot that helps debug and explain Python code, powered by Google's Gemini API.

## 🔗 Live Demo

[Try it here](https://negin-mohammadshahi.github.io/my-chatbot/)

## 📋 Overview

This chatbot acts as a focused **Python programming assistant**. It can:
- Explain why a piece of Python code throws an error and how to fix it
- Walk through how a snippet of Python code works
- Answer questions about Python syntax, libraries, and best practices
- Politely decline to answer questions outside the scope of Python programming

Unlike a general-purpose chatbot, this one uses a **system prompt** to constrain Gemini's behavior to a specific domain — a common real-world pattern for building specialized AI assistants for businesses (support bots, tutoring bots, etc.).

## 🏗️ Architecture

```
Browser (HTML/JS)  →  Cloudflare Worker (API key + system prompt + history)  →  Google Gemini API
```

- The frontend never talks to Gemini directly — all requests go through a Cloudflare Worker.
- The Gemini API key is stored as an encrypted secret in Cloudflare Workers, never exposed in client-side code.
- The Worker injects a **system instruction** that scopes Gemini's responses to Python programming help.
- The Worker receives the full conversation history from the frontend on each request and forwards it to Gemini, enabling multi-turn context (the model "remembers" earlier messages in the same session).

## 🛠️ Tech Stack

- **Frontend:** HTML, CSS, vanilla JavaScript
- **Backend / Proxy:** [Cloudflare Workers](https://workers.cloudflare.com/) (serverless)
- **AI Model:** [Google Gemini API](https://ai.google.dev/) (`gemini-2.5-flash`)
- **Hosting:** GitHub Pages

## ✨ Features

- 🐍 Domain-specific assistant: focused on Python debugging and education
- 🧠 Conversation memory: maintains context across multiple messages in a session
- 💬 Markdown-style code formatting: code blocks render with syntax-friendly styling
- ⌛ Typing indicator while waiting for a response
- 🔄 "New conversation" button to reset chat history
- 🔒 Secure handling of API credentials (no exposed keys)
- ⚠️ Clear error handling and feedback

## 🚀 How It Works

1. The user types a Python-related question or pastes code with an error.
2. The frontend sends the message **along with the conversation history** to a Cloudflare Worker endpoint.
3. The Worker attaches a system instruction (defining the assistant's role and scope) and the secret API key, then forwards everything to Google's Gemini API.
4. Gemini's response is returned to the Worker, which passes it back to the frontend.
5. The chatbot displays the formatted reply and appends the exchange to the in-memory conversation history.

## 📁 Project Structure

```
my-chatbot/
└── index.html   # Frontend: chat UI, formatting, and conversation state
```

*(The Cloudflare Worker code — which contains the system prompt and secret-handling logic — is deployed separately and not included in this repository.)*

## 🔮 Possible Improvements

- Persistent conversation history (saved across page reloads)
- Syntax highlighting per language instead of plain code blocks
- Support for file uploads (paste a whole `.py` file)
- Rate-limit-aware fallback messaging for free-tier API limits

## 👤 Author

**Negin Mohammadshahi**
AI & Software Engineer
[Portfolio](https://negin-mohammadshahi.github.io/) | [LinkedIn](https://www.linkedin.com/in/negin-mohammadshahi-908b3a79) | [GitHub](https://github.com/negin-mohammadshahi)
