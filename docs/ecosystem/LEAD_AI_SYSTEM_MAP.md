# Lead.AI Ecosystem System Map
**Phase 0 — Discovery Baseline**  
**Last Verified:** 2026-08-07  
**Verification Status:** VERIFIED  

---

## 1. ORGANIZATION OVERVIEW

| Property | Value |
|---|---|
| Primary Organization | [Lead-AI-US](https://github.com/Lead-AI-US) |
| Production Website | [lead-ai.us](https://lead-ai.us) |
| Hugging Face Org | [lead-ai-labs](https://huggingface.co/lead-ai-labs) |
| Public Contact | [Contact Page](https://lead-ai.us/#contact) |
| Vercel Production Team | `aruns-projects-0839d12f` |

---

## 2. GITHUB REPOSITORIES (VERIFIED)

| Repository | Description | Language | Status | Primary Output |
|---|---|---|---|---|
| [.github](https://github.com/Lead-AI-US/.github) | Org profile & community health files | Markdown/YAML | ACTIVE | Ecosystem Docs & Standards |
| [lead-ai-platform](https://github.com/Lead-AI-US/lead-ai-platform) | Main AI automation platform | Scaffold | SCAFFOLD | Platform Dashboard Baseline |
| [lead-ai-business-audit](https://github.com/Lead-AI-US/lead-ai-business-audit) | Business automation audit tool | TypeScript | MOST ACTIVE | [lead-ai-business-audit.vercel.app](https://lead-ai-business-audit.vercel.app) |
| [lead-ai-whatsapp-agent](https://github.com/Lead-AI-US/lead-ai-whatsapp-agent) | WhatsApp AI agent | Scaffold | SCAFFOLD | Twilio/WhatsApp Webhook |
| [lead-ai-website-chatbot](https://github.com/Lead-AI-US/lead-ai-website-chatbot) | Embeddable website chatbot | Scaffold | SCAFFOLD | Website Concierge Widget |
| [lead-ai-lead-scoring-api](https://github.com/Lead-AI-US/lead-ai-lead-scoring-api) | FastAPI lead scoring API | Scaffold | SCAFFOLD | Lead Scoring Microservice |
| [lead-ai-prompt-vault](https://github.com/Lead-AI-US/lead-ai-prompt-vault) | Prompt library & templates | Scaffold | SCAFFOLD | Prompt Template Assets |
| [lead-ai-firebase-saas-starter](https://github.com/Lead-AI-US/lead-ai-firebase-saas-starter) | Firebase SaaS starter kit | Scaffold | SCAFFOLD | Auth & Firestore Schemas |
| [lead-ai-fraud-shield](https://github.com/Lead-AI-US/lead-ai-fraud-shield) | Fraud detection research | Scaffold | SCAFFOLD | Org Fraud Shield Baseline |
| [leadai.us](https://github.com/Arungharami/leadai.us) | Main website source repository | TypeScript/React | VERIFIED | Production Web Application |

---

## 3. WEBSITE — lead-ai.us

### Deployment Architecture
- **Framework:** Vite + React + TypeScript + Tailwind CSS
- **Deployment:** Vercel (Team Scope: `aruns-projects-0839d12f`, Project: `lead-ai-us`)
- **Apex Domain:** `lead-ai.us` (Apex canonical, `www.lead-ai.us` redirects)
- **CDN:** Vercel Edge Network

### Public Compliance Verification
- **Pricing Policy:** Fully compliant in source & `lead-ai-us.vercel.app` (all dollar amounts, package prices, and structured data offer fields removed).
- **Claims Policy:** No unsupported ROI multipliers, no fake customer counts, no fake engagement counters.
- **Responsible AI Disclaimer:** SHAP explainability disclaimer present on Fraud Shield product section.

### Navigation Architecture
- Free Audit → `#free-audit`
- Services → `#services`
- Fraud Shield → `#fraud-shield`
- Packages → `#pricing`
- Contact → `#contact`
- External Audit CTA → https://lead-ai-business-audit.vercel.app

---

## 4. HUGGING FACE PRESENCE

| Property | Value |
|---|---|
| Organization | [lead-ai-labs](https://huggingface.co/lead-ai-labs) |
| Display Name | Lead.AI Labs – Intelligent Automation & Trustworthy AI Systems |
| Status | VERIFIED — Org profile active |
| Demo Space | [fraud-detection-xai-demo](https://huggingface.co/spaces/arun-gharami/fraud-detection-xai-demo) |

---

## 5. ECOSYSTEM TOPOLOGY MAP

```text
lead-ai.us (Main Web App — Vite / React / TypeScript / Vercel)
    ├── Business Audit CTA → https://lead-ai-business-audit.vercel.app
    ├── FraudShield Section → Hugging Face Demo + GitHub Repo
    ├── Concierge Chat Widget → Local State Lead Flow
    └── Information Pages → /info/* Dynamic Content Routes

GitHub: Lead-AI-US (Org)
    ├── .github (Central Documentation & Ecosystem Registry)
    ├── lead-ai-business-audit (TypeScript / Audit Tool)
    ├── lead-ai-platform (Platform Baseline Scaffold)
    ├── lead-ai-whatsapp-agent (WhatsApp Bot Scaffold)
    ├── lead-ai-website-chatbot (Chatbot Module Scaffold)
    ├── lead-ai-lead-scoring-api (FastAPI Scoring Scaffold)
    ├── lead-ai-prompt-vault (Prompt Library Scaffold)
    ├── lead-ai-firebase-saas-starter (Firebase SaaS Baseline Scaffold)
    └── lead-ai-fraud-shield (Fraud Shield Org Scaffold)

Hugging Face: lead-ai-labs (Org)
    └── fraud-detection-xai-demo (Gradio XAI Demo Space)
```
