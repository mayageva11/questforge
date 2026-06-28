# QuestForge 🔮
### System Design Interviews, Gamified — Built for Automation Engineers

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Groq API](https://img.shields.io/badge/Groq-Llama_3.1-FF6B35?style=flat&logoColor=white)
![Pollinations.ai](https://img.shields.io/badge/Pollinations.ai-Pixar_Images-blueviolet?style=flat)
![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-Live-brightgreen?style=flat&logo=github)
![No Dependencies](https://img.shields.io/badge/Zero_Dependencies-No_npm_No_build-informational?style=flat)

🎮 **[Live Demo → mayageva11.github.io/questforge](https://mayageva11.github.io/questforge)**

---

![QuestForge — WhatsApp system design as a Pixar cartoon quest](assets/demo-quest.png)

> **Quest: "Design a Real-time Chat App like WhatsApp"**
> 🧙 Wizard + crystal ball = WebSocket server · 💌 Envelopes = messages in transit · 🏮 Lanterns = presence indicators · 🐦 Raven = message broker · 📦 Treasure chest = message history DB

---

## What It Does

QuestForge takes any system design challenge and turns it into a **Pixar-style animated quest** that teaches both the architecture and how to test it.

One AI call generates everything:

| | |
|---|---|
| ⚔️ Quest Title + Story | Fantasy narrative where system components are characters |
| 💡 Architectural Lesson | One plain-English design takeaway |
| 🎨 Pixar Cartoon | AI-generated scene where the image IS the architecture |
| 🗺️ Decode the Scene | Legend mapping every cartoon element to its system design meaning |
| ⚙️ Automation Playbook | Concrete test cases, the edge case juniors miss, load test |
| 🏗️ Test Architecture Pyramid | Layered E2E → Integration → Unit plan with tool recommendations |

**Plus two on-demand features:**
- **⚙️ Test This System** — a second AI call for a focused automation deep dive (3 test cases, edge case, load test with tool + threshold). Results are added to your LinkedIn post automatically.
- **📜 My Quests** — every quest auto-saved to localStorage (max 20). History modal shows difficulty badges, clicking reloads any past question.

---

## Why I Built This

Preparing for **Senior QA / System Design interviews**, I hit the same wall every time: architecture questions are abstract and hard to visualize. Docs didn't make concepts stick.

I built QuestForge to make every concept visual, memorable, and testable. The automation playbook came from a real gap: knowing a system's architecture is only half the answer — you also need to know *how to test it*.

**Built by Maya Erusalimsky · job hunt 2025–2026**

---

## The API Journey

| Stage | API | Why it changed |
|---|---|---|
| v1 | Anthropic Claude | Strong reasoning — billing ran out (`Error 400: credit balance too low`) |
| v2 | Google Gemini | Free tier — quota was `limit: 0` for many regions (`Error 429`) |
| v3 ✅ | **Groq + Llama 3.1** | Genuinely free (14,400 req/day), no region locks, fastest of the three |

Images: [Pollinations.ai](https://pollinations.ai) — free, no API key, just a URL with the prompt encoded.

---

## Tech Stack

| | |
|---|---|
| Frontend | Vanilla HTML5 + CSS3 + ES2022 — zero build, zero npm |
| AI Text | Groq API / Llama 3.1 8B Instant with model fallback chain |
| AI Images | Pollinations.ai / Flux (Pixar-style prompt, free) |
| Persistence | `localStorage` — API key + quest history, never leaves the browser |
| Deployment | GitHub Pages + GitHub REST API (repo + Pages created via `curl`) |
| Tooling | Claude Code (Anthropic) — entire project built and deployed from conversation |

---

## Challenges Included (16 total)

`📣 Notification Service` · `⏳ Rate Limiter` · `💬 Real-time Chat` · `📦 Distributed Cache` · `🔗 URL Shortener` · `📺 Video Streaming` · `🚗 Ride-sharing Dispatch` · `⏰ Distributed Scheduler` · `🔍 Search Autocomplete` · `📰 News Feed` · `☁️ Cloud File Storage` · `🎟️ Ticketing System` · `📍 Location Service` · `💳 Payment Processing` · `🕷️ Web Crawler` · `🚪 API Gateway`

---

## Run It Locally

```bash
git clone https://github.com/mayageva11/questforge.git
open index.html
```

Get a free Groq key at [console.groq.com](https://console.groq.com) — 30 seconds, no credit card. Paste it into ⚙️ Settings.

---

*Built by Maya Erusalimsky · [github.com/mayageva11](https://github.com/mayageva11)*
