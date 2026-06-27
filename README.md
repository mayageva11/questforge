# QuestForge 🔮
### System Design Interviews, Gamified — for Automation Engineers

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Groq API](https://img.shields.io/badge/Groq-Llama_3.1-FF6B35?style=flat&logoColor=white)
![Pollinations.ai](https://img.shields.io/badge/Pollinations.ai-Pixar_Style_Images-blueviolet?style=flat)
![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-Live-brightgreen?style=flat&logo=github)
![Mobile Friendly](https://img.shields.io/badge/Responsive-Mobile_%7C_Tablet_%7C_Desktop-success?style=flat)
![No Build](https://img.shields.io/badge/Zero_Dependencies-No_npm_No_build-informational?style=flat)

🎮 **[Live Demo → mayageva11.github.io/questforge](https://mayageva11.github.io/questforge)**

---

![QuestForge — Real-time Chat system design as a Pixar cartoon quest](assets/demo-quest.png)

**Quest: "Design a Real-time Chat App like WhatsApp"**

| What you see | What it means in system design |
|---|---|
| 🧙 Wizard boy touching the glowing crystal ball | The **WebSocket server** — keeps a persistent connection open to both users |
| 💌 Glowing envelopes floating in the air | **Messages in transit** — delivered instantly through the open connection |
| 🏮 Glowing lanterns hanging above | **Presence indicators** — green means the user is online right now |
| 🐦 Raven companion | The **message broker** — routes messages to the right recipient |
| 📦 Treasure chest full of scrolls | The **message history database** — stores every chat so you can scroll back |

*Every quest generates a unique Pixar-style cartoon like this, tailored to the system design concept you chose.*

---

## What is QuestForge?

QuestForge turns dry **System Design interview questions** into Pixar-style animated fantasy quests — and then teaches you how to **test the system you just learned**.

You pick a challenge (or type your own). The app generates all of this in one shot:

| Section | What you get |
|---|---|
| ⚔️ **Quest Title** | A catchy game-level title for the challenge |
| 📜 **Fantasy Story** | A 3–4 sentence narrative where system components are fantasy characters |
| 💡 **Architectural Lesson** | One plain-English sentence — the real design takeaway |
| 🎨 **Pixar Cartoon** | An AI-generated illustration where the scene IS the architecture |
| 🗺️ **Decode the Scene** | A legend mapping every cartoon element to its system design meaning |
| ⚙️ **Automation Playbook** | Concrete test scenarios, the edge case juniors always miss, and a load test |
| 🏗️ **Test Architecture Pyramid** | A visual showing exactly how to layer E2E → Integration → Unit tests for this system |

Every quest teaches you the concept, shows it visually, and tells you how to test it.

---

## Why I Built This

While preparing for **Senior QA / System Design interviews**, I kept hitting the same wall: design questions felt abstract and hard to visualize. Reading docs didn't make concepts stick.

So I built QuestForge. Instead of grinding another article, I translate every challenge into a Pixar-quality animated quest — because learning sticks better when it doesn't feel like studying.

The **automation playbook and test pyramid** came from a real need: as a senior automation engineer, knowing the system architecture is only half the answer. You also need to know *how to test it* — what layers to cover, what to load test, and what failure mode everyone misses.

**Built by Maya Erusalimsky during the great job hunt of 2025–2026. Shipped because why not.**

---

## The Full Quest Experience

Here is everything shown on the results screen for a single quest:

### 1. 📜 Fantasy Story
A 3–4 sentence narrative where every system component becomes a fantasy character. The story teaches the real architectural tradeoff without feeling like a textbook.

> *"At the Iron Gate of the Kingdom's API, the Hourglass Sentry stands watch. A flood of Raven Messengers — unbounded traffic bursts — threatens to overrun the fortress. The Sentry holds golden Token Buckets: refill them too slowly and loyal knights wait in vain; refill too fast and chaos floods the gate. The real question isn't how fast to refill — it's whether to use a fixed window, a sliding log, or a token bucket."*

### 2. 💡 Architectural Lesson
One plain sentence — the actual thing you'd say in an interview.

> *"Use token bucket for bursty-traffic APIs — it allows short bursts while enforcing sustained rate limits, unlike fixed windows that cause thundering-herd resets at window boundaries."*

### 3. 🎨 Pixar Cartoon + 🗺️ Decode the Scene
A Pixar/Disney 3D-style illustration where the characters ARE the system components. Below the image, a legend decodes every element:

```
🧌 Troll gatekeeper        = Rate limiter (decides who gets through)
🪣 Golden buckets           = Token buckets (refill over time, consumed per request)
⏳ Hourglass in the sky     = Time window (when it resets, tokens refill)
🐦 Queue of ravens          = Incoming API requests waiting their turn
🚫 Envelopes flying away    = Rejected requests — 429 Too Many Requests
```

### 4. ⚙️ Automation Engineer's Playbook

**Test Scenarios** — concrete, actionable, not vague:
```
✓ POST /api/resource with valid token → assert 200 within 100ms
✓ Send 11 requests/minute (limit is 10) → assert 11th returns 429
✓ After rate limit resets, send valid request → assert 200 (not still blocked)
✓ Send request with malformed Authorization header → assert 401, not 429
```

**Edge Case Juniors Always Miss:**
> *Clients that don't handle 429 retry-after headers and immediately retry — causing a retry storm that amplifies the original traffic spike.*

**Performance Test:**
> *Use k6 to ramp from 100 to 10,000 virtual users over 5 minutes. Watch for: 429 response rate > 5%, p99 latency above 200ms, and memory growth in the rate limiter service suggesting token bucket state is leaking.*

### 5. 🏗️ Test Architecture Pyramid

```
         ┌─────────────────────────────┐
         │  🌐 E2E Tests               │  ← few · slow · high confidence
         │  Full rate-limit flow       │     (pink)
         │  across real services       │
         └─────────────────────────────┘
       ┌───────────────────────────────────┐
       │  🔗 Integration Tests             │  ← real services, no mocks
       │  Token bucket with Redis          │     (lavender)
       │  WebSocket connection events      │
       └───────────────────────────────────┘
     ┌─────────────────────────────────────────┐
     │  ⚡ Unit Tests                           │  ← many · fast · isolated
     │  Token refill logic                     │     (teal)
     │  Window boundary calculations           │
     │  429 response format validation         │
     └─────────────────────────────────────────┘

🔧 Tool Stack: k6 (load), Playwright (E2E), pytest + testcontainers (integration)
```

---

## How the AI Works

### Groq + Llama 3.1 — All Text Generation

QuestForge uses the **Groq API** with **Llama 3.1 8B Instant** for all quest content.

```
POST https://api.groq.com/openai/v1/chat/completions
Authorization: Bearer gsk_...
```

**Why Groq?**

| | |
|---|---|
| ✅ **Genuinely free** | 14,400 requests/day, no credit card, no billing ever |
| ✅ **Works everywhere** | No region restrictions — unlike Google Gemini which blocked the free tier for many users |
| ✅ **Lightning fast** | Groq's custom LPU chip — full quest in under 1 second |
| ✅ **Reliable JSON** | `response_format: json_object` guarantees clean structured output |
| ✅ **OpenAI-compatible** | Standard API — easy to swap models without rewriting anything |

The prompt instructs Llama to return a structured JSON object with all sections in one call:

```json
{
  "title": "...",
  "story": "...",
  "lesson": "...",
  "image_scene": "Character-action description for the Pixar cartoon",
  "image_legend": ["🧙 element = meaning", "..."],
  "automation": {
    "test_cases": ["...", "..."],
    "edge_case": "...",
    "performance_test": "..."
  },
  "test_architecture": {
    "e2e": ["...", "..."],
    "integration": ["...", "..."],
    "unit": ["...", "..."],
    "tool_stack": "..."
  }
}
```

If the primary model hits a rate limit, the app automatically falls back through `gemma2-9b-it` → `llama3-8b-8192`.

### The Fantasy Concept Map

The prompt maps system design concepts to fantasy metaphors so the story is consistent:

```
WebSocket Server   →  Crystal Ball of Telepathic Tethers
Load Balancer      →  Gatekeeper / Toll Bridge Guardian
SQL Database       →  Royal Scroll Vaults (ACID-sealed)
NoSQL Database     →  Wildwood Rune-Stone Archive (Eventually consistent)
Cache              →  Pouch of Instant Recall
Message Queue      →  The Raven Courier Guild
Rate Limiter       →  The Hourglass Sentry
CDN                →  The Network of Magic Mirrors
Microservice       →  Summoned Golem / Mage Guild
Circuit Breaker    →  The Failsafe Seal
Sharding           →  Divided Fiefdoms
Replication        →  Phoenix Resurrection Runes
```

### Pollinations.ai — Pixar-Style Cartoon Generation

The quest illustration is generated by [Pollinations.ai](https://pollinations.ai) — completely free, no API key needed.

```js
const url = `https://image.pollinations.ai/prompt/${encodedPrompt}?width=832&height=448&model=flux&nologo=true&seed=${Date.now()}`;
```

The prompt requests **Pixar and Disney 3D animation style** — cinematic render, expressive characters with big eyes and soft rounded shapes, warm vibrant colors, beautiful soft lighting. Every image is unique (different seed every time).

The `image_scene` field from Groq describes exactly which characters appear and what visible actions they perform — so the image directly illustrates the system design, not just a generic dungeon.

---

## The Journey: Claude → Gemini → Groq

**Started with Anthropic Claude API** (`claude-sonnet-4-6`) — strong reasoning, great JSON output. Hit the billing wall:
```
Error 400: Your credit balance is too low to access the Claude API.
```

**Switched to Google Gemini** (advertised as free). Hit a different wall — the free tier quota was `0` for many API keys depending on Google Cloud project/region:
```
Error 429: Quota exceeded — free_tier limit: 0, model: gemini-2.0-flash
```

**Switched to Groq** — genuinely free for everyone, no exceptions, faster than both. Each migration was a one-file change: same prompt structure, same JSON parsing, different endpoint and auth header.

---

## Features

- 🎮 **8 system design quick-pick challenges** — one tap to load
- ✏️ **Custom challenge input** — type any design question
- 🤖 **Groq + Llama 3.1** — generates all content in one AI call, under 1 second
- 🎨 **Pixar-style cartoon** — unique AI illustration for every quest
- 🗺️ **Decode the Scene** — legend mapping every cartoon element to its system design meaning
- 💡 **Architectural lesson** — one plain-English takeaway per quest
- ⚙️ **Automation Playbook** — concrete test cases, missed edge case, load test scenario
- 🏗️ **Test Architecture Pyramid** — visual E2E / Integration / Unit layers with tool recommendations
- 📋 **Copy to LinkedIn** — one-click formatted post
- 🔄 **New Quest** — instant reset without page reload
- ⚙️ **Settings modal** — manage your API key (localStorage only)
- 📱 **Fully responsive** — mobile, tablet, and desktop

---

## System Design Challenges

| | Challenge | Key concept tested |
|--|-----------|-------------------|
| 📣 | Notification service | Fan-out, pub/sub, push vs poll |
| ⏳ | Rate limiter for a public API | Token bucket, sliding window, 429 handling |
| 💬 | Real-time chat (WhatsApp) | WebSockets, presence, message persistence |
| 📦 | Distributed cache (Redis-like) | Eviction policies, consistency, TTL |
| 🔗 | URL shortener (Bit.ly) | Hashing, redirect, analytics at scale |
| 📺 | Video streaming (YouTube) | CDN, chunking, adaptive bitrate |
| 🚗 | Ride-sharing dispatch (Uber) | Geo-indexing, real-time matching, load |
| ⏰ | Distributed job scheduler | Task queues, at-least-once delivery, idempotency |

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | Vanilla HTML5 + CSS3 + JavaScript (ES2022) |
| Fonts | Plus Jakarta Sans · Outfit · JetBrains Mono (Google Fonts) |
| AI — Text | Groq API / Llama 3.1 8B Instant (free, 14,400 req/day) |
| AI — Images | Pollinations.ai / Flux model (free, no key needed) |
| Animations | CSS View Transitions API + Safari fallback |
| Storage | `localStorage` (API key only, never leaves your browser) |
| Hosting | GitHub Pages (static, zero cost) |
| Deployment | GitHub REST API + Claude Code (Anthropic) |

**Zero npm. Zero build. Zero backend. Clone and open `index.html`.**

---

## Local Setup

```bash
git clone https://github.com/mayageva11/questforge.git
cd questforge
open index.html   # macOS — or drag into any browser
```

1. Get a free Groq key at **[console.groq.com](https://console.groq.com)** — 30 seconds, no credit card
2. Click ⚙️ → paste your `gsk_...` key → Save
3. Pick a challenge or type your own → **Forge Quest 🔮**

---

## Deploy Your Own

1. Fork this repo
2. **Settings → Pages → Deploy from branch → main → / (root)**
3. Wait ~2 min → live at `https://YOUR_USERNAME.github.io/questforge`

No config. No environment variables. Users bring their own free Groq key from [console.groq.com](https://console.groq.com).

---

## How It Was Deployed

The entire project — repo creation, GitHub Pages setup, every commit — was orchestrated through **Claude Code** (Anthropic's AI coding assistant) without ever opening the GitHub web UI.

```bash
# Create repo via GitHub REST API
curl -X POST https://api.github.com/user/repos \
  -H "Authorization: token $TOKEN" \
  -d '{"name":"questforge","private":false}'

# Enable GitHub Pages
curl -X POST https://api.github.com/repos/mayageva11/questforge/pages \
  -H "Authorization: token $TOKEN" \
  -d '{"source":{"branch":"main","path":"/"}}'
```

Claude Code acted as a deployment layer — running git commands, calling the GitHub API, and pushing every change directly from the conversation.

---

*Built by Maya Erusalimsky · [github.com/mayageva11](https://github.com/mayageva11) · 2025–2026*
