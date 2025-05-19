# Real-Time Translation Service – Architecture Overview

This repository provides a technical summary of a real-time translation system I helped build and deploy as part of AI Prodigy. While source code is proprietary and cannot be shared, this overview explains the design and components I worked on directly.

## Overview

The service enables real-time English ↔ Spanish translation via a browser-based interface. It supports audio input, live subtitles, and optional text-to-speech output.

### Stack

| Layer | Tech |
|-------|------|
| Web backend | Flask, Python |
| Real-time protocol | WebSocket (Flask-Sockets / gevent) |
| Cloud infra | EC2 (Docker), ALB, RDS, Secrets Manager |
| NLP services | Amazon Translate + Polly |
| Deployment | Manual via Docker + EC2 (documented [here](https://github.com/yourusername/manual-deployment-notes)) |

## Key Features

- Bi-directional WebSocket connection for low-latency interactions
- Mode switching (live vs document reading)
- Audio playback using Polly TTS
- Secure credential handling with AWS Secrets Manager
- Deployed to EC2 Auto Scaling behind an ALB

## My Contributions

- Architected and deployed backend infrastructure in AWS (multi-AZ setup)
- Created Docker images and deployment scripts
- Integrated Secrets Manager to avoid hardcoded credentials
- Set up RDS, IAM roles, and ALB target groups
- Optimized EC2 networking and reduced monthly costs by 40%

## Demo Diagram (illustrative only)

*No source code or private media is included in this repo.*

