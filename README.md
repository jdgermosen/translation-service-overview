# Real-Time English ↔ Spanish Translation Platform

> **Role:** Cloud & DevOps Engineer – AI Prodigy  
> **Mission:** Deliver natural-sounding voice translation in the browser with ∼15 s latency.

A code-free overview of the AWS infrastructure I helped build for AI Prodigy's real-time translation platform.  
The translation pipeline itself is proprietary, so its design, models, source code, and endpoints stay private.

---

## 1 · What the Product Does

- **Live speech → subtitles → translated speech** in the browser, ~15 s end-to-end  
- Push-to-talk microphone, live subtitles, and translated audio playback  
- Role-based memberships (Free, Pro, Enterprise) control usage quotas

---

## 2 · High-Level Architecture

| Tier | Key Services | Notes |
|------|--------------|-------|
| **Frontend** | Flask/Jinja2 web app (HTML, CSS, JavaScript), secure WebSocket | No browser plug-ins required |
| **Translation service** | Dockerized WebSocket service on EC2 Auto Scaling | Proprietary pipeline (details private) |
| **Auth & Billing** | Stripe Checkout + Webhooks | Usage metering in Postgres |
| **Data Layer** | Amazon RDS Postgres, S3 | Encrypted at rest |
| **Infra / Ops** | EC2 Auto Scaling (2 AZ) behind HTTPS ALB | Rolling updates with health probes |

![Architecture diagram](assets/architecture.png) 

---

## 3 · My Contributions (Team Project)

| Phase | What I did |
|-------|------------|
| **System Design** | Contributed to latency-budget mapping and service selection during design reviews |
| **Data Pipeline** | Collected & transformed ~300 h bilingual audio–text pairs used for model evaluation |
| **Cloud Build** | Containerised the services and built the AWS environment (security groups, ASG, ALB, RDS, S3), later codified in Terraform |
| **Cost-Ops** | Replaced the NAT Gateway with a NAT instance + VPC interface endpoints → **~40 % monthly networking savings** |
| **Security** | Secrets Manager for all keys, TLS 1.3, WAF rate-limiting, HIPAA-aligned data path |

---

## 4 · Impact

- **98 % transcription accuracy** across 12 Spanish dialects  
- **15 s median latency** browser-to-browser (measured with client RUM)  
- **99.9 % availability** over last 90 days (ALB + multi-AZ ASG)

---

## 5 · Lessons Learned

- **Cost versus resilience.** Replacing the managed NAT Gateway with a NAT instance cut networking cost by about 40 %, but one NAT instance is a single point of failure for outbound traffic. That trade-off was right for development, not for production.
- **Don't pay for idle servers.** A Lambda function that starts and stops the translation servers on demand avoided paying for capacity nobody was using.
- **Hand-built infrastructure is hard to repeat.** The first environment was built with the AWS Console and CLI. Rebuilding it later in Terraform made every change reviewable and repeatable.
