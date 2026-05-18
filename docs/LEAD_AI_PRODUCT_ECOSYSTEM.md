# Lead.AI Product Ecosystem

## Purpose

This document maps the Lead.AI-US product ecosystem and explains how each repository supports a larger AI automation company strategy.

## Product Map

| Product | Role | Primary User | Business Problem | Status | First Valuable Demo |
| --- | --- | --- | --- | --- | --- |
| Lead.AI Platform | Main Lead.AI SaaS platform/dashboard. | Small business owners | Businesses need one place to manage AI automation, leads, conversations, analytics, and product workflows. | In Development / MVP | Create a dashboard shell with lead, conversation, and automation module views. |
| Lead.AI Business Audit | AI-powered business automation audit tool. | Small business owners | Small businesses do not know what to automate first or how much AI automation they need. | MVP | Build the intake form, scoring rubric, and report-ready audit output first. |
| Lead.AI WhatsApp Agent | WhatsApp AI assistant for business leads and customer support. | Local service businesses | Businesses miss WhatsApp leads and manually answer repetitive questions. | Prototype / In Development | Implement webhook verification and a simple qualification conversation flow. |
| Lead.AI Website Chatbot | Embeddable website chatbot widget. | Small business websites | Website visitors leave without asking questions or becoming leads. | Prototype / MVP | Build the embeddable widget shell and lead capture conversation flow. |
| Lead.AI Lead Scoring API | Predictive lead scoring and qualification API. | Sales teams | Businesses do not know which leads deserve priority follow-up. | Prototype / MVP | Create Pydantic schemas, deterministic scoring rules, and example API responses. |
| Lead.AI Prompt Vault | Premium AI automation prompt library. | Small business owners | Business owners need ready-to-use prompts for sales, support, marketing, workflow automation, and customer engagement. | Product / Content MVP | Publish the first prompt collections with examples and adaptation notes. |
| Lead.AI Firebase SaaS Starter | Reusable Firebase SaaS starter kit for Lead.AI products. | Lead.AI product builders | AI SaaS products need fast authentication, database, hosting, and deployment foundations. | Starter Kit / In Development | Create the starter folder structure, auth layout, and Firestore rules placeholder. |
| Lead.AI Fraud Shield | Explainable AI fraud detection and risk scoring system. | Risk teams | Businesses and financial systems need better fraud detection with explainable risk signals. | Prototype / Research Demo | Build a synthetic-data demo, baseline scoring pipeline, and explanation format. |

## Product Strategy

Lead.AI should start with products that create client demand quickly, then grow into reusable automation infrastructure.

Recommended build order:

1. lead-ai-business-audit
2. lead-ai-website-chatbot
3. lead-ai-whatsapp-agent
4. lead-ai-lead-scoring-api
5. lead-ai-platform
6. lead-ai-fraud-shield
7. lead-ai-prompt-vault
8. lead-ai-firebase-saas-starter

## How The Products Connect

- Business Audit identifies automation needs and captures qualified prospects.
- Website Chatbot and WhatsApp Agent turn those needs into real customer-facing automations.
- Lead Scoring API adds prioritization intelligence across captured leads.
- Platform becomes the shared dashboard for modules, analytics, and integrations.
- Prompt Vault supports repeatable sales, support, and automation workflows.
- Firebase SaaS Starter provides reusable infrastructure for future products.
- Fraud Shield demonstrates responsible AI, explainability, and risk scoring capability.
