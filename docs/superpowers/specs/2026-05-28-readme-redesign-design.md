# GitHub Profile README Redesign — Design Spec

**Date:** 2026-05-28
**Author:** Shivam Pandey
**Repo:** shivvamm/shivvamm (GitHub profile README)

---

## Overview

Complete redesign of the GitHub profile README using the "AI Engineer Portfolio" approach. The README should function as a recruiter-facing landing page — visually bold, colorful, scannable, and showcasing Shivam's depth in modern AI/ML technologies.

## Target Audience

Recruiters and hiring managers evaluating AI/ML engineering candidates.

## Design Principles

- **Bold & colorful** — vibrant shields.io badges, colorful accents, high visual energy
- **Recruiter-scannable** — skills and projects front and center, no hidden content
- **Bhagavad Gita shloka as signature** — kept prominently at the top
- **Live links everywhere** — project names hyperlink directly to deployed demos
- **Category-organized tech stack** — immediately communicates AI depth

---

## Section-by-Section Spec

### 1. Header & Hero

**1a. Shloka Banner**
- Bhagavad Gita shloka image at the very top: `https://shloka.onrender.com/api/v1/bahgavad_gita/image`
- Kept as-is — the rotating image via GitHub Action remains

**1b. Greeting + Animated Typing**
- `# Hey, I'm Shivam! 👋` as the main heading
- Below: an animated typing SVG (via readme-typing-svg or similar) cycling through:
  - `AI/ML Engineer`
  - `Voice AI`
  - `AI Agents`
  - `RAG`
  - `Generative AI`
  - `LLMs`

**1c. About Me**
- 2-3 concise lines:
  > I build AI-powered products — from voice agents and RAG pipelines to multi-agent systems and neural search engines. Constantly exploring the cutting edge of AI/ML and turning research into real-world applications.

**1d. Social Badges (inline)**
- Colorful shields.io badges for: LinkedIn, Email (mrshivam@duck.com), Twitter/X (@Shivv71), GitHub (shivvamm)
- Centered, immediately after bio

---

### 2. Featured Projects

**Layout:** 2-column grid using HTML table, 3 rows of 2 projects.

**Key rule:** The project name is a hyperlink to the live deployed URL (or GitHub repo if no live demo). No separate "Live Demo" buttons.

**Projects (in order):**

| Project | Link | Description | Tech Badges |
|---------|------|-------------|-------------|
| Voice Coach | https://voice-coach-ai.netlify.app/ | AI voice coaching platform | Deepgram, Gemini, Groq, Next.js |
| Contract Analyst | https://contract-analystpro.netlify.app/ | AI-powered contract analysis | Gemini API, Groq, LLMs, AI Agents |
| AutoDraftAI | https://auto-draft-ai.vercel.app | Multi-agent inbox assistant | CrewAI, Groq, FastAPI |
| Alisia | https://searchwithalisia.netlify.app/ | AI neural search engine with real-time knowledge | AI Search, Multi-tools |
| chatdocs | https://github.com/shivvamm/chatdocs | RAG chatbot with vector search | Pinecone, Qdrant, Groq, RAG |
| Shloka | https://shloka.vercel.app/ | Sanskrit shlokas & slogans API | TypeScript, REST API |

**Card style:** Each project in an HTML table cell with:
- Linked project name (bold)
- One-line description
- Small colorful tech badges (shields.io)

---

### 3. Tech Stack

Organized by **category** using shields.io badges. Each category has a heading and a row of colorful badges.

**Categories and items:**

**AI/ML & Deep Learning**
Python, TensorFlow, PyTorch, Scikit-learn, Jupyter, Anaconda

**LLMs & Generative AI**
LangChain, LlamaIndex, Gemini, Groq, OpenAI, Prompt Engineering, Fine-tuning, RLHF/DPO

**AI Agents & Orchestration**
CrewAI, LangGraph, AutoGen, MCP, Multi-Agent Systems, Tool Use

**Voice AI**
Deepgram, STT, TTS, Realtime Voice Models, Voice Agents

**RAG & Vector Databases**
Pinecone, Qdrant, Elasticsearch, RAG Pipelines, Embeddings, GraphRAG

**Computer Vision & Media AI**
DALL-E, Stable Diffusion, YOLO, OCR / Document AI

**Web & Full Stack**
Next.js, React, Node.js, FastAPI, JavaScript, TypeScript, Tailwind, Sass

**Cloud & DevOps**
Docker, Linux, DigitalOcean, Redis, RabbitMQ

**Badge style:** Use shields.io with custom colors per category for visual distinction. Use `flat-square` or `for-the-badge` style for consistency.

---

### 4. GitHub Stats & Activity

> **Note:** The default `github-readme-stats.vercel.app` instance returns 503 errors. Use these verified working alternatives instead.

**Row of 3 stat cards (dark theme, side by side):**

1. **GitHub Stats** — `github-profile-summary-cards.vercel.app/api/cards/stats?username=shivvamm&theme=github_dark`
2. **Top Languages** — `github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=shivvamm&theme=github_dark`
3. **Streak Stats** — `streak-stats.demolab.com/?user=shivvamm&theme=dark`

**Profile Details Card (full-width, below the row):**
- `github-profile-summary-cards.vercel.app/api/cards/profile-details?username=shivvamm&theme=github_dark`

**Contribution Snake Animation:**
- Below the stats section
- SVG animation generated via `Platane/snk@v3` GitHub Action
- Runs daily (and on push to master), commits the generated SVG to an `output` branch
- Dark-themed snake animation

---

### 5. Footer

**5a. Sanskrit Slogan**
- The rotating Sanskrit slogan embed: `https://shloka.onrender.com/api/v1/sanskrit/slogan/image`
- Kept as `<object>` or `<img>` tag

**5b. Socials (repeated)**
- Same social badges as header — LinkedIn, Email, Twitter/X, GitHub
- Centered

**5c. Closing line**
- `Feel free to connect with me for collaboration.`

---

## GitHub Actions Required

### 1. Existing: Shloka Image Rotation
- Already exists at `.github/workflows/update_readme.yml`
- Runs every 6 hours, cache-busts the Sanskrit slogan image
- No changes needed

### 2. New: Contribution Snake Animation
- New workflow: `.github/workflows/snake.yml`
- Uses `Platane/snk@v3` action to generate the snake SVG
- Runs daily (and on push to master)
- Outputs SVG to the `output` branch via `crazy-max/ghaction-github-pages`
- Referenced in README as `https://raw.githubusercontent.com/shivvamm/shivvamm/output/github-contribution-dark-snake.svg`

---

## File Changes

| File | Action | Description |
|------|--------|-------------|
| `README.md` | Rewrite | Complete redesign per this spec |
| `.github/workflows/snake.yml` | Create | New GitHub Action for contribution snake |
| `.github/workflows/update_readme.yml` | Keep | No changes |

---

## Out of Scope

- Blog post auto-pulling via GitHub Actions
- "Currently working on" / "Currently learning" dynamic sections
- Profile trophy widgets
- Collapsible sections
- Separate demo buttons (project names are the links)
