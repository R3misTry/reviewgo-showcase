# ReviewGo

**AI-Powered Google Review Management Platform**

[View Live Demo (reviewgo.app)](https://reviewgo.app)

> 🔒 **Private Source Code**: This repository serves as a portfolio showcase. The source code is private due to proprietary workflows and commercial licensing.

---

## ⚡ At a Glance

*   🚀 **Live SaaS**: Fully functional multi-tenant application deployed in production.
*   🤝 **Human-in-the-Loop**: AI generates drafts; humans approve them. Zero autonomous posting.
*   🛡️ **Safety First**: Strict database isolation and deterministic AI fallbacks.
*   ⚡ **Modern Stack**: Built on Next.js 16 and Supabase for a serverless architecture.

---

## 👤 My Role

This project was built using an **AI-Assisted Development** workflow. My role focused on high-level system design, product strategy, and orchestration, while leveraging AI tools for implementation.

My primary contributions were:
*   **Product Requirements**: defining the user flows and the "draft-first" approach to solve the trust gap in automation.
*   **System Architecture**: Designing the data model and selecting the infrastructure components to support multi-tenancy.
*   **AI Workflow Design**: Structuring the prompt engineering strategies and fallback logic to ensure reliable outputs.
*   **Validation**: Reviewing and refining AI-generated code to ensure it met production standards for security and correctness.

---

## 🎯 Product Vision

ReviewGo addresses "Review Fatigue"—the difficulty businesses face in maintaining engagement on Google Maps.

While many tools offer full automation, I prioritized a **Human-in-the-Loop** model. Business owners are often wary of letting a bot speak for their brand. By positioning the AI as an assistant that prepares **Drafts** for approval, we provide the speed of automation with the safety of human oversight.

---

## 🔄 System Flow

A high-level view of how a review moves through the system:

```text
[Google Review] 
      ⬇
(Webhook Event) 
      ⬇
[Ingestion Queue] ➝ (Idempotent Processing)
      ⬇
[AI Analysis] ➝ (Groq Llama 3 ➝ Fallback to Gemini)
      ⬇
[Draft Created] ➝ (Stored in Supabase)
      ⬇
[Human Approval] ➝ (User clicks "Publish")
      ⬇
(Google API) ➝ [Reply Published]
```

---

## 🧠 Architecture Highlights

### Event-Driven Ingestion
I chose an asynchronous webhook model to handle incoming reviews.
*   **Decision**: Decouple ingestion from processing using a worker queue.
*   **Why**: This ensures that traffic spikes (e.g., viral reviews) do not overwhelm the application or lead to data loss.

### Hybrid AI Usage
The system design acknowledges that AI providers can experience latent periods.
*   **Decision**: Implement a cascading fallback strategy.
*   **Why**: Prioritizing **Groq** (Llama 3) allows for sub-second draft generation, but having **Gemini** as a fallback guarantees service continuity if the primary provider fails.

### Database-Level Isolation
I structured the database to enforce security at the lowest level.
*   **Decision**: Use PostgreSQL Row Level Security (RLS) keyed to Organization IDs.
*   **Why**: This provides a "fail-safe" layer. Even if an API endpoint were to have a logic error, cross-tenant data access remains blocked by the database engine itself.

---

## 🚫 Non-Goals

*   **Fully Autonomous Replies**: I intentionally excluded auto-posting to avoid the risk of AI hallucinations affecting brand reputation.
*   **Open Source Distribution**: The specific prompt engineering and orchestration logic remain proprietary.
*   **Social Media Support**: The scope was constrained to Google Reviews to ensure deep, high-quality integration before expanding.

---

These tools were chosen as implementation enablers, not as a claim of deep framework specialization.

## 🛠️ Tech Stack

The following tools were selected to balance developer velocity with production reliability:

*   **Framework**: Next.js 16 (App Router)
*   **Database**: Supabase (PostgreSQL + Realtime)
*   **Language**: TypeScript
*   **AI Inference**: Groq + Gemini
*   **Infrastructure**: Vercel

---

*ReviewGo is currently live and serving users.*
