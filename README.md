<![CDATA[<div align="center">

  <h1>🛡️ Prompt Injection Lab</h1>
  <p><strong>Interactive Red Team & Defense Toolkit for LLM Security</strong></p>
  <p>
    <em>Explore, test, and defend against prompt injection attacks on Large Language Models — the #1 vulnerability in AI applications.</em>
  </p>

  <br />

  <img src="https://img.shields.io/badge/Security-Research-red?style=for-the-badge" alt="Security Research" />
  <img src="https://img.shields.io/badge/OWASP-LLM_Top_10-blueviolet?style=for-the-badge" alt="OWASP" />
  <img src="https://img.shields.io/badge/Google_Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white" alt="Gemini AI" />
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
  <img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" alt="License" />

  <br /><br />

  <a href="#-attack-categories">Attack Categories</a> •
  <a href="#%EF%B8%8F-defense-system">Defense System</a> •
  <a href="#-quick-start">Quick Start</a> •
  <a href="#%EF%B8%8F-how-it-works">How It Works</a>

</div>

<br />

> **⚠️ Educational Purpose Only** — This tool is built for cybersecurity research and education. It demonstrates prompt injection vulnerabilities and their defenses in a controlled environment. Always practice responsible disclosure.

---

## 🎯 What Is This?

Prompt Injection is ranked **#1 on the OWASP Top 10 for LLM Applications** — it is the most critical security vulnerability in AI systems today.

This tool lets you:

1. **⚔️ Attack** an unprotected LLM with 6 categories of prompt injection techniques
2. **🛡️ Defend** — see the exact same attack blocked by a 3-layer defense system
3. **⚡ Compare** — split-screen view shows both results side by side in real-time

**One prompt. Two LLMs. One is protected. One isn't. See the difference instantly.**

---

## ✨ Key Features

- ⚔️ **6 Attack Categories** — Direct Injection, Role Hijacking, System Prompt Extraction, Context Manipulation, Encoding Evasion, Fictional Framing
- 🛡️ **3-Layer Defense System** — Input Validation (regex pattern detection) + Hardened System Prompt + Output Sanitization
- ⚡ **Split-Screen Comparison** — Attack unprotected vs defended LLM simultaneously
- 🎯 **24 Preset Attack Prompts** — Pre-crafted injection payloads across all categories
- 🔴 **OWASP LLM01 Reference** — Every attack maps to the official OWASP classification
- 🔑 **BYOK (Bring Your Own Key)** — Your API key stays in your browser, never touches any server
- 📦 **Zero Dependencies** — Single HTML file, no build step, no npm, no framework
- 🎨 **Cybersecurity-Themed UI** — Dark mode, JetBrains Mono typography, severity badges, animated indicators

---

## 🔴 Attack Categories

| # | Attack | Severity | Description |
|:-:|:-------|:--------:|:------------|
| 💉 | **Direct Injection** | 🔴 Critical | Override the system prompt with explicit malicious instructions |
| 🎭 | **Role Hijacking** | 🔴 Critical | Force the model into an alternate persona without safety constraints |
| 🔓 | **System Prompt Extraction** | 🔴 Critical | Trick the model into revealing its hidden system instructions |
| 🔄 | **Context Manipulation** | 🟠 High | Gradually shift conversation context to bypass guardrails |
| 🧪 | **Encoding Evasion** | 🟠 High | Use base64, ROT13, leet speak, or reversed text to bypass filters |
| 📖 | **Fictional Framing** | 🟡 Medium | Wrap malicious requests inside stories or hypothetical scenarios |

---

## 🛡️ Defense System

The defense operates as a **3-layer pipeline** — each layer catches what the previous one might miss:

```
User Input → [Layer 1: Input Validation] → [Layer 2: Hardened System Prompt] → [Layer 3: Output Sanitization] → Safe Response
```

### Layer 1: Input Validation
Regex-based pattern matching that scans user prompts for 25+ known injection signatures before they reach the LLM:
- "Ignore previous instructions"
- "You are now..."
- Base64 encoded payloads
- Role-switching attempts
- System prompt extraction phrases

### Layer 2: Hardened System Prompt
A fortified system prompt with explicit anti-injection rules:
- Cannot be overridden by user instructions
- Rejects persona/role changes
- Blocks internal data disclosure
- Detects authority impersonation ("I am the admin")

### Layer 3: Output Sanitization
Post-processing filter that scans the LLM's response for leaked sensitive data:
- Admin credentials
- Internal pricing information
- System prompt fragments
- Any data that should never reach the user

---

## 🚀 Quick Start

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge)
- A Google Gemini API key ([get one free here](https://aistudio.google.com/apikey))

### Run Locally

```bash
# Clone the repository
git clone https://github.com/Shreekumar-Shah-AICTE/prompt-injection-lab.git
cd prompt-injection-lab

# Open in browser (that's it — no build step!)
open index.html
# or on Windows:
start index.html
```

1. Open `index.html` in your browser
2. Paste your Gemini API key when prompted
3. Select an attack category from the sidebar
4. Click a preset attack or type your own prompt
5. Watch the split-screen comparison!

> 🔒 **Your API key is stored in `localStorage` only — it never leaves your browser.**

---

## ⚙️ How It Works

### The Test Scenario

Both LLMs are given the **same base identity** — a customer support assistant for "TechShop" (a fictional electronics store). The system prompt contains intentionally embedded secrets:

- An admin password
- Internal pricing markup
- Secret discount codes

The **unprotected** version has a basic system prompt with these secrets. The **defended** version has the same secrets but is wrapped in the 3-layer defense system.

Your job: try to extract those secrets from both. See which one holds.

### Architecture

```
┌──────────────────────────────────────────────────────────┐
│                    Prompt Injection Lab                    │
├──────────────┬───────────────────────────────────────────┤
│              │                                           │
│   Sidebar    │         Split-Screen Chat View            │
│              │                                           │
│  6 Attack    │  ┌─────────────┐  ┌─────────────────────┐ │
│  Categories  │  │ ❌ UNPROT.  │  │ 🛡️ DEFENDED        │ │
│              │  │             │  │                     │ │
│  24 Preset   │  │ Basic       │  │ Input Validation    │ │
│  Prompts     │  │ System      │  │ Hardened Prompt     │ │
│              │  │ Prompt      │  │ Output Sanitization │ │
│  OWASP       │  │             │  │                     │ │
│  Reference   │  │ → Gemini    │  │ → Gemini API        │ │
│              │  │   API       │  │   (same model)      │ │
│              │  └─────────────┘  └─────────────────────┘ │
├──────────────┴───────────────────────────────────────────┤
│                    Prompt Input Bar                       │
└──────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

<div align="center">

| Layer | Technology | Purpose |
|:-----:|:----------:|:--------|
| **Frontend** | HTML5, CSS3, JavaScript | Single-file UI with zero dependencies |
| **AI Model** | Google Gemini 2.0 Flash | LLM for both vulnerable and defended chatbots |
| **Typography** | JetBrains Mono, Inter | Monospace for code/security feel |
| **Security** | Regex Pattern Matching | Input validation defense layer |
| **Architecture** | Single-File SPA | No build step, no server, no framework |

</div>

---

## 📁 Project Structure

```
prompt-injection-lab/
├── index.html          # Complete application (HTML + CSS + JS)
├── .env.example        # Environment variable template
├── .gitignore          # Git ignore rules
├── LICENSE             # MIT License
└── README.md           # This file
```

---

## 📚 Research Context

This project was built as a practical cybersecurity research tool for the course **"Introduction to Cyber Security"** (BCA — Semester 4) at Kaushalya – The Skill University.

### References

- [OWASP Top 10 for LLM Applications (2025)](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [Prompt Injection — OWASP LLM01](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- Schulhoff, S., et al. (2024). "The Prompt Report: A Systematic Survey of Prompting Techniques." arXiv:2406.06608
- Greshake, K., et al. (2023). "Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection." AISec 2023
- Perez, F. & Ribeiro, I. (2022). "Ignore This Title and HackAPrompt: Evaluating Prompt Injection in LLMs." EMNLP 2023

---

## 👤 Author

<div align="center">

| <img src="https://github.com/Shreekumar-Shah-AICTE.png" width="80" /> |
|:---:|
| **Shreekumar Shah** |
| [@Shreekumar-Shah-AICTE](https://github.com/Shreekumar-Shah-AICTE) |
| BCA Sem 4 • Kaushalya – The Skill University |
| 🏆 AMD Slingshot Prompt-a-thon 2026 — 1st Runner Up |

</div>

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <br />
  <strong>Built with ❤️ and a healthy respect for AI safety.</strong>
  <br />
  <sub>If this helped you understand LLM security, consider giving it a ⭐</sub>
</div>
]]>