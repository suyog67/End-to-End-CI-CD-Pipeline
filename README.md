# 🗳️ VoteBox — Live Polling App

A fully functional voting app built with **Node.js + Express**, designed for CI/CD pipelines.

---

## Features

- ✅ Create polls with up to 8 options
- ✅ Vote on polls (one vote per session)
- ✅ Live percentage bars & vote counts
- ✅ Delete polls
- ✅ `/health` endpoint for uptime checks
- ✅ 15 Jest tests with coverage
- ✅ Multi-stage Dockerfile (test → production)
- ✅ GitHub Actions CI/CD pipeline

---

## Quick Start

```bash
# Install
npm install

# Run locally
npm start           # http://localhost:3000

# Dev mode (auto-reload)
npm run dev

# Tests
npm test
```

---

## Docker

```bash
# Build and run
docker build -t voting-app .
docker run -p 3000:3000 voting-app

# Or with docker compose
docker compose up -d

# Run tests in Docker
docker compose --profile test run voting-app-test
```

---

## REST API

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/health` | Health check (for CI/CD & load balancers) |
| `GET` | `/api/polls` | List all polls |
| `POST` | `/api/polls` | Create a poll |
| `GET` | `/api/polls/:id` | Get a single poll |
| `POST` | `/api/polls/:id/vote` | Cast a vote |
| `DELETE` | `/api/polls/:id` | Delete a poll |

### Create Poll
```json
POST /api/polls
{
  "title": "Best CI/CD tool?",
  "options": ["GitHub Actions", "GitLab CI", "Jenkins", "CircleCI"]
}
```

### Vote
```json
POST /api/polls/:id/vote
{
  "optionId": "<uuid>",
  "voterToken": "unique-user-identifier"
}
```

---

## CI/CD Pipeline (GitHub Actions)

The pipeline has 3 jobs:

1. **Test** — Runs Jest tests with coverage report
2. **Build** — Builds & pushes Docker image to GitHub Container Registry
3. **Deploy** — SSH deploy to production server (main branch only)

### Required Secrets

| Secret | Description |
|--------|-------------|
| `DEPLOY_HOST` | Production server IP/hostname |
| `DEPLOY_USER` | SSH username |
| `DEPLOY_KEY` | SSH private key |

### Required Variables

| Variable | Description |
|----------|-------------|
| `PRODUCTION_URL` | e.g. `https://vote.example.com` |

---

## Project Structure

```
voting-app/
├── server.js              # Express app + REST API
├── server.test.js         # Jest tests (15 tests)
├── public/
│   └── index.html         # Single-page frontend
├── Dockerfile             # Multi-stage build
├── docker-compose.yml
├── .github/
│   └── workflows/
│       └── ci.yml         # GitHub Actions pipeline
└── package.json
```
