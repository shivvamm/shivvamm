# GitHub Profile README Redesign — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Complete redesign of shivvamm/shivvamm GitHub profile README as a bold, colorful, recruiter-facing AI Engineer portfolio.

**Architecture:** Single-page README.md using GitHub-flavored Markdown + inline HTML tables for layout. GitHub Actions for dynamic content (shloka rotation already exists, new snake animation workflow). All stats widgets use verified working external services.

**Tech Stack:** Markdown, HTML, shields.io badges, github-profile-summary-cards, streak-stats.demolab.com, Platane/snk GitHub Action, readme-typing-svg

---

## File Structure

| File | Action | Responsibility |
|------|--------|----------------|
| `README.md` | Rewrite | The entire profile — header, projects, tech stack, stats, footer |
| `.github/workflows/snake.yml` | Create | GitHub Action to generate contribution snake SVG daily |
| `.github/workflows/update_readme.yml` | Keep (no changes) | Existing shloka image rotation |

---

### Task 1: Create the Contribution Snake GitHub Action

**Files:**
- Create: `.github/workflows/snake.yml`

This must be done first because the README will reference the snake SVG from the `output` branch. The SVG won't exist until this action runs at least once (or we trigger it manually after pushing).

- [ ] **Step 1: Create the snake workflow file**

```yaml
name: Generate Snake Animation

on:
  schedule:
    - cron: '0 0 * * *'
  workflow_dispatch:
  push:
    branches:
      - master

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      - name: Generate snake SVG
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: shivvamm
          outputs: |
            dist/github-contribution-dark-snake.svg?palette=github-dark
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Push to output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

- [ ] **Step 2: Commit the workflow**

```bash
git add .github/workflows/snake.yml
git commit -m "feat: add GitHub contribution snake animation workflow"
```

---

### Task 2: Write the Header & Hero Section of README

**Files:**
- Modify: `README.md` (full rewrite starts here — replace all existing content)

- [ ] **Step 1: Write the header section**

Replace the entire contents of `README.md` with:

```markdown
![Shlok](https://shloka.onrender.com/api/v1/bahgavad_gita/image)

# Hey, I'm Shivam! <img src="https://raw.githubusercontent.com/MartinHeinz/MartinHeinz/master/wave.gif" width="30px">

<a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=36BCF7&center=true&vCenter=true&width=600&lines=AI%2FML+Engineer;Voice+AI;AI+Agents;RAG;Generative+AI;LLMs" alt="Typing SVG" /></a>

I build AI-powered products — from voice agents and RAG pipelines to multi-agent systems and neural search engines.
Constantly exploring the cutting edge of AI/ML and turning research into real-world applications.

<p align="center">
  <a href="https://www.linkedin.com/in/shivampandey27/" target="blank">
    <img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
  <a href="mailto:mrshivam@duck.com" target="blank">
    <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" />
  </a>
  <a href="https://twitter.com/Shivv71" target="blank">
    <img src="https://img.shields.io/badge/Twitter-%231DA1F2.svg?style=for-the-badge&logo=twitter&logoColor=white" alt="Twitter" />
  </a>
  <a href="https://github.com/shivvamm" target="blank">
    <img src="https://img.shields.io/badge/GitHub-%23121011.svg?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
  </a>
</p>

---
```

- [ ] **Step 2: Verify the typing SVG URL works**

Open in browser: `https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=36BCF7&center=true&vCenter=true&width=600&lines=AI%2FML+Engineer;Voice+AI;AI+Agents;RAG;Generative+AI;LLMs`

Expected: An animated SVG showing text cycling through the listed phrases.

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "feat: rewrite README header with animated typing and social badges"
```

---

### Task 3: Write the Featured Projects Section

**Files:**
- Modify: `README.md` (append after the header)

- [ ] **Step 1: Append the featured projects section to README.md**

Add after the `---` at the end of the header:

```markdown

## Featured Projects

<table>
  <tr>
    <td width="50%">
      <h3><a href="https://voice-coach-ai.netlify.app/">Voice Coach</a></h3>
      <p>AI voice coaching platform with real-time speech analysis and feedback</p>
      <p>
        <img src="https://img.shields.io/badge/Deepgram-13EF93?style=flat-square&logo=deepgram&logoColor=white" />
        <img src="https://img.shields.io/badge/Gemini-8E75B2?style=flat-square&logo=google-gemini&logoColor=white" />
        <img src="https://img.shields.io/badge/Groq-F55036?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=next.js&logoColor=white" />
      </p>
    </td>
    <td width="50%">
      <h3><a href="https://contract-analystpro.netlify.app/">Contract Analyst</a></h3>
      <p>AI-powered contract analysis and review with intelligent insights</p>
      <p>
        <img src="https://img.shields.io/badge/Gemini_API-8E75B2?style=flat-square&logo=google-gemini&logoColor=white" />
        <img src="https://img.shields.io/badge/Groq-F55036?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/LLMs-412991?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/AI_Agents-FF6F00?style=flat-square&logoColor=white" />
      </p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3><a href="https://auto-draft-ai.vercel.app">AutoDraftAI</a></h3>
      <p>AI multi-agentic inbox assistant that drafts and manages emails</p>
      <p>
        <img src="https://img.shields.io/badge/CrewAI-FF4B4B?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/Groq-F55036?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" />
      </p>
    </td>
    <td width="50%">
      <h3><a href="https://searchwithalisia.netlify.app/">Alisia</a></h3>
      <p>AI neural search engine with current knowledge and multiple tools</p>
      <p>
        <img src="https://img.shields.io/badge/AI_Search-0066FF?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/Neural_Search-7B2D8E?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/Multi--tools-2EA44F?style=flat-square&logoColor=white" />
      </p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3><a href="https://github.com/shivvamm/chatdocs">chatdocs</a></h3>
      <p>RAG chatbot with vector search, evaluation pipeline, and multiple backends</p>
      <p>
        <img src="https://img.shields.io/badge/Pinecone-000000?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/Qdrant-DC382D?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/Groq-F55036?style=flat-square&logoColor=white" />
        <img src="https://img.shields.io/badge/RAG-FF6F00?style=flat-square&logoColor=white" />
      </p>
    </td>
    <td width="50%">
      <h3><a href="https://shloka.vercel.app/">Shloka</a></h3>
      <p>API serving quality Sanskrit shlokas and slogans with daily rotation</p>
      <p>
        <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
        <img src="https://img.shields.io/badge/REST_API-009688?style=flat-square&logoColor=white" />
      </p>
    </td>
  </tr>
</table>

---
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "feat: add featured projects section with live demo links"
```

---

### Task 4: Write the Tech Stack Section

**Files:**
- Modify: `README.md` (append after the projects section)

- [ ] **Step 1: Append the tech stack section to README.md**

Add after the `---` at the end of the projects section:

```markdown

## Tech Stack

### AI/ML & Deep Learning
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Anaconda](https://img.shields.io/badge/Anaconda-44A833?style=for-the-badge&logo=anaconda&logoColor=white)

### LLMs & Generative AI
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![LlamaIndex](https://img.shields.io/badge/LlamaIndex-6B3FA0?style=for-the-badge&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-8E75B2?style=for-the-badge&logo=google-gemini&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-F55036?style=for-the-badge&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![Prompt Engineering](https://img.shields.io/badge/Prompt_Engineering-00A67E?style=for-the-badge&logoColor=white)
![Fine--tuning](https://img.shields.io/badge/Fine--tuning-FF4B4B?style=for-the-badge&logoColor=white)
![RLHF/DPO](https://img.shields.io/badge/RLHF%2FDPO-7B2D8E?style=for-the-badge&logoColor=white)

### AI Agents & Orchestration
![CrewAI](https://img.shields.io/badge/CrewAI-FF4B4B?style=for-the-badge&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=for-the-badge&logoColor=white)
![AutoGen](https://img.shields.io/badge/AutoGen-0078D4?style=for-the-badge&logoColor=white)
![MCP](https://img.shields.io/badge/MCP-D97706?style=for-the-badge&logoColor=white)
![Multi--Agent Systems](https://img.shields.io/badge/Multi--Agent_Systems-2EA44F?style=for-the-badge&logoColor=white)
![Tool Use](https://img.shields.io/badge/Tool_Use-6366F1?style=for-the-badge&logoColor=white)

### Voice AI
![Deepgram](https://img.shields.io/badge/Deepgram-13EF93?style=for-the-badge&logo=deepgram&logoColor=white)
![STT](https://img.shields.io/badge/STT-0066FF?style=for-the-badge&logoColor=white)
![TTS](https://img.shields.io/badge/TTS-FF6F00?style=for-the-badge&logoColor=white)
![Realtime Voice](https://img.shields.io/badge/Realtime_Voice-E91E63?style=for-the-badge&logoColor=white)
![Voice Agents](https://img.shields.io/badge/Voice_Agents-9C27B0?style=for-the-badge&logoColor=white)

### RAG & Vector Databases
![Pinecone](https://img.shields.io/badge/Pinecone-000000?style=for-the-badge&logoColor=white)
![Qdrant](https://img.shields.io/badge/Qdrant-DC382D?style=for-the-badge&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white)
![RAG Pipelines](https://img.shields.io/badge/RAG_Pipelines-FF6F00?style=for-the-badge&logoColor=white)
![Embeddings](https://img.shields.io/badge/Embeddings-00BCD4?style=for-the-badge&logoColor=white)
![GraphRAG](https://img.shields.io/badge/GraphRAG-7B2D8E?style=for-the-badge&logoColor=white)

### Computer Vision & Media AI
![DALL-E](https://img.shields.io/badge/DALL--E-412991?style=for-the-badge&logo=openai&logoColor=white)
![Stable Diffusion](https://img.shields.io/badge/Stable_Diffusion-A100FF?style=for-the-badge&logoColor=white)
![YOLO](https://img.shields.io/badge/YOLO-00FFFF?style=for-the-badge&logoColor=black)
![OCR / Document AI](https://img.shields.io/badge/OCR%2FDocument_AI-4285F4?style=for-the-badge&logoColor=white)

### Web & Full Stack
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=next.js&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Sass](https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=white)

### Cloud & DevOps
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![DigitalOcean](https://img.shields.io/badge/DigitalOcean-0080FF?style=for-the-badge&logo=digitalocean&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)

---
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "feat: add categorized tech stack with shields.io badges"
```

---

### Task 5: Write the GitHub Stats & Activity Section

**Files:**
- Modify: `README.md` (append after the tech stack section)

- [ ] **Step 1: Append the stats section to README.md**

Add after the `---` at the end of the tech stack section:

```markdown

## GitHub Stats

<p align="center">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/stats?username=shivvamm&theme=github_dark" alt="GitHub Stats" />
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=shivvamm&theme=github_dark" alt="Top Languages" />
  <img src="https://streak-stats.demolab.com/?user=shivvamm&theme=dark" alt="GitHub Streak" />
</p>

<p align="center">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=shivvamm&theme=github_dark" alt="Profile Details" width="100%" />
</p>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/shivvamm/shivvamm/output/github-contribution-dark-snake.svg" />
  <img alt="github-snake" src="https://raw.githubusercontent.com/shivvamm/shivvamm/output/github-contribution-dark-snake.svg" />
</picture>

---
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "feat: add GitHub stats cards and contribution snake animation"
```

---

### Task 6: Write the Footer Section

**Files:**
- Modify: `README.md` (append after the stats section)

- [ ] **Step 1: Append the footer to README.md**

Add after the `---` at the end of the stats section:

```markdown

<p align="center">
  <object type="image/svg+xml" data="https://shloka.onrender.com/api/v1/sanskrit/slogan/image" width="180" height="72"></object>
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/shivampandey27/" target="blank">
    <img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" />
  </a>
  <a href="mailto:mrshivam@duck.com" target="blank">
    <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" />
  </a>
  <a href="https://twitter.com/Shivv71" target="blank">
    <img src="https://img.shields.io/badge/Twitter-%231DA1F2.svg?style=for-the-badge&logo=twitter&logoColor=white" alt="Twitter" />
  </a>
  <a href="https://github.com/shivvamm" target="blank">
    <img src="https://img.shields.io/badge/GitHub-%23121011.svg?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" />
  </a>
</p>

<p align="center">Feel free to connect with me for collaboration.</p>
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "feat: add footer with Sanskrit slogan and social badges"
```

---

### Task 7: Verify Everything Works

- [ ] **Step 1: Push to GitHub and trigger the snake workflow**

```bash
git push origin master
```

Then go to https://github.com/shivvamm/shivvamm/actions and manually trigger the "Generate Snake Animation" workflow via the "Run workflow" button (the `workflow_dispatch` trigger).

- [ ] **Step 2: Verify the profile page**

Open https://github.com/shivvamm in a browser and verify:

1. Shloka banner image loads at the top
2. Animated typing SVG cycles through the phrases
3. Social badges are visible and clickable
4. All 6 project names are clickable and redirect to their live demos
5. Tech stack badges render with correct colors per category
6. All 3 stats cards load (GitHub Stats, Top Languages, Streak)
7. Profile details card loads full-width
8. Snake animation loads (after the workflow completes — may take a few minutes)
9. Sanskrit slogan loads in the footer
10. Footer social badges work

- [ ] **Step 3: Fix any broken elements**

If any stats card or badge fails to load, check the URL directly in the browser. Replace with a working alternative if needed.
