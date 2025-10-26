# Shodh-a-Code

### The Next-Gen Competitive Coding Arena

[![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org/)
[![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://reactjs.org/)

A full-stack coding contest platform that brings the thrill of live programming battles straight to your browser.

[Features](#core-highlights) • [Quick Start](#quick-start) • [Architecture](#how-it-works) • [API Docs](#api-reference)



---

## What is Shodh-a-Code?

**Shodh-a-Code** is a modern, self-hosted competitive programming platform — think Codeforces, LeetCode, or AtCoder, but fully customizable and developer-friendly.

Enable participants to:
- Join live coding contests
- Solve problems in multiple languages
- Compete on real-time leaderboards
- Get instant verdicts on submissions

All powered by a secure execution environment.

---

## Tech Stack

| Layer | Technology | Purpose |
|:------|:-----------|:--------|
| **Frontend** | Next.js + React + Tailwind CSS | Contest UI, code editor, live verdicts |
| **Backend** | Spring Boot (Java) | REST API, contest logic, scoring |
| **Database** | H2 / MySQL | Contest data, users, submissions |

---

## Core Highlights

- **Multi-language Support** — C++, Java, Python with isolated compilation
- **Automated Judge System** — Each submission runs in a secure sandbox
- **Real-time Verdicts** — Watch your code go from "Running" to "Accepted" or "WA"
- **Live Leaderboard** — Auto-refreshing, contest-wise rankings
- **Persistent Editor** — Code saved across sessions and refreshes
- **Resource Limits** — Memory and CPU caps for fair judging
- **RESTful API** — Clean endpoints for all operations

---

## Quick Start

### Setup

```bash
# Clone the repository
git clone https://github.com/vangshi/shodhacode.git
cd shodh-a-code
```

**Backend Setup**

```bash
cd backend
./mvnw clean install
./mvnw spring-boot:run
```

Backend will be available at `http://localhost:8080`

**Frontend Setup**

```bash
cd frontend
npm install
npm run dev
```

Frontend will be available at `http://localhost:3000`

---

## How It Works

### Execution Flow

1. **Join Contest** — Participant registers with contest ID and username
2. **Code Submission** — Frontend sends code to backend API
3. **Judging** — Backend executes code with test cases in isolated environment
4. **Verdict & Scoring** — Results processed and score updated
5. **Live Leaderboard** — Rankings refresh automatically

### Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Frontend (Next.js)                   │
│            Port 3000 - Contest UI & Editor               │
└──────────────────────┬──────────────────────────────────┘
                       │ REST API (JSON)
                       ▼
┌─────────────────────────────────────────────────────────┐
│                 Backend (Spring Boot)                    │
│        Port 8080 - Contest Logic & Judging API          │
└──────────────────────┬──────────────────────────────────┘
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
   ┌─────────┐  ┌──────────┐  ┌──────────┐
   │  Judge  │  │ Database │  │ File I/O │
   │ Engine  │  │ (H2/SQL) │  │  Layer   │
   └─────────┘  └──────────┘  └──────────┘
```

---

## API Reference

### Contest Management

| Endpoint | Method | Description |
|:---------|:-------|:------------|
| `/api/contests/{id}` | GET | Fetch contest details |
| `/api/contests/{id}/join` | POST | Register participant |
| `/api/contests/{id}/leaderboard` | GET | Get live rankings |
| `/api/contests/{id}/update-score` | POST | Update participant score |

### Submission Handling

| Endpoint | Method | Description |
|:---------|:-------|:------------|
| `/api/submissions` | POST | Submit code for judging |
| `/api/submissions/{id}` | GET | Fetch submission verdict |
| `/api/submissions/{id}/status` | GET | Check execution status |

**Example Request:**

```bash
curl -X POST http://localhost:8080/api/submissions \
  -H "Content-Type: application/json" \
  -d '{
    "contestId": 1,
    "problemId": 101,
    "language": "cpp",
    "code": "#include<iostream>\nint main(){...}"
  }'
```

---

## Project Structure

```
shodh-a-code/
├── backend/
│   ├── src/main/java/com/shodhai/shodhacode/
│   │   ├── api/              # REST Controllers
│   │   ├── domain/           # Entities & Models
│   │   ├── repo/             # Data Repositories
│   │   ├── judge/            # Execution Engine
│   │   └── ShodhACodeApplication.java
│   └── pom.xml
│
└── frontend/
    ├── src/
    │   ├── app/contest/[id]/ # Contest Pages
    │   ├── components/       # Reusable UI
    │   └── lib/api.ts        # API Client
    └── package.json
```

---

## Design Philosophy

| Aspect | Approach |
|:-------|:---------|
| **Backend** | Modular REST APIs, clean separation of concerns |
| **Frontend** | Responsive, minimal, developer-centric design |
| **Execution** | Secure sandbox per submission |
| **Scoring** | Atomic updates, idempotent verification |
| **Deployment** | Simple setup and configuration |

---

## Technical Challenges Solved

- **Cross-language Container Isolation** — Different runtimes in separate sandboxes
- **Secure File I/O** — Safe data transfer for test cases
- **Asynchronous Verdict Polling** — Non-blocking submission status checks
- **Scalable Leaderboard Updates** — Real-time ranking without database locks
- **Resource Management** — CPU and memory limits per execution

---

## Prerequisites

Before running Shodh-a-Code, ensure you have:

- **Java 17+** and **Maven** installed
- **Node.js 18+** and **npm** installed
- **Ports 3000 and 8080** available

---

## Deployment

### Local Development

Start backend and frontend servers as described in the Quick Start section.

### Production Considerations

- Replace H2 with MySQL/PostgreSQL
- Add authentication layer (JWT/OAuth)
- Implement rate limiting
- Set up monitoring (Prometheus/Grafana)
- Configure reverse proxy (Nginx)
- Enable HTTPS with SSL certificates

---

## Contributing

Contributions are welcome! Here's how you can help:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## Why Shodh-a-Code?

Shodh-a-Code isn't just another coding platform — it's a **proof of concept** for:

- Scalable, containerized evaluation systems
- Secure code execution environments
- Real-time competitive programming infrastructure
- Production-ready full-stack architecture

Perfect for **educational institutions**, **coding clubs**, and **tech communities** looking to host their own programming contests.

---



### Built With Passion, Designed for Performance

**Made by developers, for developers**

[Back to Top](#shodh-a-code)