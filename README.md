# ⚽ Mission 2038 — AI Football Coaching & Scouting Platform

> **Empowering Grassroots Footballers & Tactical Scouts with Premier League-Grade Computer Vision & Local LLM Intelligence.**

[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-009688.svg?style=flat&logo=fastapi)](https://fastapi.tiangolo.com)
[![Next.js](https://img.shields.io/badge/Next.js-16-black.svg?style=flat&logo=next.js)](https://nextjs.org)
[![YOLOv8](https://img.shields.io/badge/YOLO-v8_Pose_%26_Detect-00FFFF.svg?style=flat)](https://ultralytics.com)
[![Ollama](https://img.shields.io/badge/Ollama-Llama_3.2-blueviolet.svg?style=flat)](https://ollama.com)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green.svg?style=flat&logo=node.js)](https://nodejs.org)

---

## 📌 Table of Contents
1. [Platform Overview](#-platform-overview)
2. [Microservice Architecture](#-microservice-architecture)
3. [Core AI Capabilities](#-core-ai-capabilities)
   - [11v11 Match Tactical Tracking](#1-11v11-match-tactical-tracking)
   - [Solo Player Coaching Suite](#2-solo-player-coaching-suite)
4. [Prerequisites & System Requirements](#-prerequisites--system-requirements)
5. [Quick Start (Local Development)](#-quick-start-local-development)
6. [Testing the AI Systems](#-testing-the-ai-systems)
7. [Environment Variables Reference](#-environment-variables-reference)
8. [License](#-license)

---

## 🌟 Platform Overview

**Mission 2038** is an end-to-end sports-tech platform designed to democratize high-performance football analytics. The platform bridges elite-level video analytics with accessible consumer hardware, running heavy computer vision and local Large Language Models (LLMs) safely within **4GB VRAM constraints**.

The ecosystem provides:
- **For Players:** Solo drill biomechanical feedback (Shooting Knee Flexion & Torso Lean, Dribble Touch Frequency, and Goalkeeper Dive Extension & Set-Position Readiness).
- **For Coaches & Scouts:** 11v11 match tracking, ball possession splits, physical distance/speed telemetry, and AI-generated 1v1 player matchups and counter-strategies.

---

## 🏛️ Microservice Architecture

The project is structured into three decoupled services:

```
mission-2k38/
├── 🌐 frontend/        # Next.js Web App (Tailwind CSS, Framer Motion, Lucide, SSE Client)
├── ⚙️ backend/         # Express.js REST API & PostgreSQL (NeonDB) Data Access Layer
├── 🧠 ai_backend/      # Python FastAPI Microservice (YOLOv8, ByteTrack, MediaPipe, Ollama)
│   ├── api_service/    # FastAPI app (api.py), 11v11 pipeline (main.py), Tactical LLM
│   ├── coaching_modules/ # Solo AI Coaches (Shooting, Dribbling, Goalkeeper)
│   └── training_utils/ # Model fine-tuning and dataset preparation scripts
├── 📄 package.json     # Monorepo concurrent runner scripts
├── 📄 ARCHITECTURE.md  # Deep technical architecture documentation
└── 📄 README.md        # This setup guide
```

| Service | Technology | Port | Description |
| :--- | :--- | :--- | :--- |
| **Frontend** | Next.js 16 (React 19, Tailwind) | `3000` | Web dashboard, video uploader, interactive pitch tactics. |
| **Backend** | Node.js, Express, NeonDB Postgres | `5000` | User auth (JWT), trial management, video registry, SSE proxy. |
| **AI Backend** | Python 3.10/3.11, FastAPI, YOLOv8 | `8000` (or `8080`) | CV pipelines, joint tracking, MJPEG video streaming, Ollama bridge. |
| **Ollama** | Local LLM Server (Llama 3.2) | `11434` | Offline tactical coaching verdicts & counter-strategy generation. |

---

## 🧠 Core AI Capabilities

### 1. 11v11 Match Tactical Tracking
- **Multi-Object Tracking (MOT):** Uses YOLOv8 + ByteTrack to detect and track 22 players, referees, and the ball across broadcast footage.
- **Dynamic Team Assignment:** K-Means color clustering isolates team kits, automatically grouping outfield athletes into Team 1 and Team 2.
- **Physical Metrics Engine:** Calculates total distance covered (meters), top sprint speed (km/h), and individual player possession time.
- **Live MJPEG Video Stream:** Pipes annotated video frames in real-time directly to browser image streams.
- **1v1 Scout Matchups:** Pits the opponent's video tracking telemetry against a custom team roster dataset, prompting Llama 3.2 to generate a bespoke tactical game plan.

### 2. Solo Player Coaching Suite
- **🎯 Striker / Shooting Coach (`ai_Coach.py`):**
  - Measures knee flexion (backswing power angle).
  - Evaluates **Torso Lean** (chest over ball to prevent skying shots).
  - Uses 2D vector kinetic velocity to catch driven, sweeping, and volley strikes.
- **⚡ Dribbling Coach (`dribbling_coach.py`):**
  - Scale-invariant ball control calculation ($0.42 \times \text{leg length}$), eliminating resolution and zoom errors.
  - Dynamically cropped high-FPS ROI feet tracker.
  - Debounced touch counter and ball drift detector.
- **🧤 Goalkeeper Coach (`goalkeeper_coach.py`):**
  - **Physics Trajectory Deflection:** Distinguishes genuine saves (rebound, parry, $>40^\circ$ deflection) from goals conceded, eliminating 2D parallax phantom saves.
  - **Set Position Readiness Score ($0–100\%$):** Evaluates pre-shot knee spring ($105^\circ-128^\circ$) and hand ready height.
  - **Maximum Dive Extension:** Measures reach span relative to standing height.

---

## 💻 Prerequisites & System Requirements

1. **Node.js**: `v18.x` or `v20.x`
2. **Python**: `3.10` or `3.11`
3. **Ollama**: Download and install from [ollama.com](https://ollama.com)
4. **Hardware**: 8GB+ RAM, NVIDIA GPU with 4GB+ VRAM recommended (CUDA acceleration). Works on CPU.

---

## ⚡ Quick Start (Local Development)

### 1. Start Ollama and Pull the Model
```bash
ollama run llama3.2
```
*Keep Ollama running in the background.*

---

### 2. Set Up the Python AI Backend
```bash
cd ai_backend

# Create and activate virtual environment
python -m venv venv

# Windows (PowerShell):
.\venv\Scripts\Activate.ps1
# macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
```

---

### 3. Install Node.js Dependencies
In the project root:
```bash
cd ..
npm install
npm --prefix frontend install
npm --prefix backend install
```

---

### 4. Run All Services Concurrently
From the project root:
```bash
npm run dev
```
This boots:
- Frontend on **`http://localhost:3000`**
- Express API on **`http://localhost:5000`**
- AI Backend on **`http://localhost:8000`**

*(Alternatively, run services individually via `npm run dev:frontend`, `npm run dev:backend`, and `npm run dev:ai`).*

---

## 🧪 Testing the AI Systems

### Testing the 11v11 Match Dashboard
1. Ensure the AI backend is active on port 8000 or 8080:
   ```powershell
   cd ai_backend\api_service
   ..\venv\Scripts\python.exe -m uvicorn api:app --port 8080 --reload
   ```
2. Navigate to **[http://localhost:8080/match-dashboard](http://localhost:8080/match-dashboard)** in your browser.
3. Upload any match footage (`.mp4`).
4. Watch the live annotated MJPEG stream render.
5. Select a Target Opponent and hit **"Generate 1v1 Matchup Strategy"** to test local Ollama tactical feedback.

### Testing Solo Player Drills
1. Open the Next.js app at **[http://localhost:3000/player/upload](http://localhost:3000/player/upload)**.
2. Select your drill type (**Shooting**, **Dribbling**, or **Goalkeeping**).
3. Upload a drill clip and navigate to **`/player/coach`** to watch the live Server-Sent Events (SSE) telemetry and Ollama technical report.

---

## ⚙️ Environment Variables Reference

### `ai_backend/.env`
```env
OLLAMA_HOST=http://localhost:11434
OLLAMA_MODEL=llama3.2
```

### `backend/.env`
```env
PORT=5000
NODE_ENV=development
FASTAPI_URL=http://127.0.0.1:8000
PYTHON_AI_SERVICE_URL=http://127.0.0.1:8000
DATABASE_URL="<your_neon_postgres_url>"
JWT_SECRET="<your_jwt_secret>"
```

### `frontend/.env`
```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
NEXT_PUBLIC_SOCKET_URL=http://localhost:5000
```

---

## 📄 License
This project is licensed under the MIT License. Built by **Algo Rhythm**.
