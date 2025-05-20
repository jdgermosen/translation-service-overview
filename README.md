# Real-Time English ↔ Spanish Translation Platform

> **Role:** Cloud & DevOps Engineer – AI Prodigy  
> **Mission:** Deliver natural-sounding voice translation in the browser with ∼15 s latency.

This repo gives a **code-free, recruiter-friendly walkthrough** of the system I helped build.  
Source code, model weights, and proprietary endpoints remain private.

---

## 1 · What the Product Does

- **Live speech → subtitles → cloned voice** with ~15 s end-to-end delay  
- Browser UI supports:
  - Push-to-talk microphone  
  - Whisper streaming transcription  
  - GPT-4o streaming translation  
  - Optional TTS voice clone playback  
- Role-based memberships (Free, Pro, Enterprise) control usage quotas

---

## 2 · High-Level Architecture

| Tier | Key Services | Notes |
|------|--------------|-------|
| **Frontend** | React SPA, secure WebSocket | No browser plug-ins required |
| **Realtime API** | Flask + Gunicorn (Docker)<br>Flask-Sockets (WS) | Orchestrates the translation pipeline |
| **AI Pipeline** | Whisper STT → GPT-4o Translation → Voice-clone TTS | Staged streaming keeps latency low |
| **Auth & Billing** | Stripe Checkout + Webhooks | Usage metering in Postgres |
| **Data Layer** | Amazon RDS Postgres, S3 (audio blobs) | Audio encrypted at rest |
| **Infra / Ops** | EC2 Auto Scaling (2 AZ) behind HTTPS ALB | Rolling updates with health probes |

*(A redacted diagram lives in `/assets/architecture.png`.)*

---

## 3 · My Contributions (Team Project)

| Phase | What I did |
|-------|------------|
| **System Design** | Contributed to latency-budget mapping and service selection during design reviews |
| **Data Pipeline** | Collected & transformed ~300 h bilingual audio–text pairs used for model evaluation |
| **Cloud Build** | Containerised micro-services (<150 MB images) and authored IaC for SG, ASG, ALB, RDS, S3 |
| **Cost-Ops** | Switched NAT GW to VPC interface endpoints → **40 % monthly savings** |
| **Security** | Secrets Manager for all keys, TLS 1.3, WAF rate-limiting, HIPAA-aligned data path |

---

## 4 · Impact

- **98 % transcription accuracy** across 12 Spanish dialects  
- **15 s median latency** browser-to-browser (measured with client RUM)  
- **99.9 % availability** over last 90 days (ALB + multi-AZ ASG)

---

## 7 · Why It Matters

Need **reliable, low-latency AI workloads** in AWS—backed by measurable cost, security, and uptime guarantees?  
I deliver the full lifecycle:

> _design → data → cloud build → release engineering → monitoring → optimisation_

Let’s talk!
