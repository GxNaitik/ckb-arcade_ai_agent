# 🤖 CKB Arcade & AI Agent Engine

[![Live Demo](https://img.shields.io/badge/Live_Demo-Play_Now!-blue?style=for-the-badge&logo=vercel)](https://ckb-arcade.vercel.app)

A decentralized multi-game arcade platform built on the **Nervos CKB blockchain (Testnet)**, combined with an autonomous **AI Agent Engine** capable of interacting with the arcade. Built for the **"Claw & Order: CKB AI Agent Hackathon"**.

Players can connect their CKB wallet to play manually, while the AI Agent provides a modular engine for autonomous on-chain gaming, strategy management, and risk mitigation.

---

## 🎯 Game Collection

| Game | Type | Min Bet | Max Bet | RTP | Description |
|------|------|---------|---------|-----|-------------|
| 🎡 **Spin to Win** | Classic | 100 CKB | 1,000 CKB | 95% | Spin a colorful wheel and win up to 10,000 CKB |
| 🎲 **CKB Dice** | Luck | 50 CKB | 500 CKB | 97% | Roll the dice and predict your luck — 2x on correct guess |
| 🪙 **Coin Flip** | Luck | 25 CKB | 1,000 CKB | 98% | Classic 50/50 coin flip — double your CKB |
| 🔢 **Number Guess**| Luck | 75 CKB | 750 CKB | 90% | Guess the number 1–10, higher risk = higher rewards |
| 🦖 **CKB Dino Run**| Skill | 200 CKB | 200 CKB | 95% | Chrome Dino-style endless runner with time-based rewards |

*(Dino Run uses server-verified tier rewards to prevent client-side manipulation, with daily limits to prevent bot abuse).*

---

## 🏗️ Architecture

The project is structured into three main modules:

```text
ckb_arcade_ai_agent/
├── agent-engine/                      # Autonomous AI Agent Logic
│   ├── src/strategy.ts                # Decision making (AI swap-point)
│   ├── src/agent.ts                   # Agent orchestrator & runner
│   └── src/logger.ts                  # Logging and monitoring
├── frontend/                          # React + TypeScript + Vite UI
│   ├── src/components/games/          # Game specific implementations
│   └── src/App.tsx                    # Main app + CCC Provider
├── backend/                           # Node.js + Express API
│   ├── index.js                       # Logic for on-chain payout & verification
│   └── .env.example
├── demo video.mp4                     # Demonstration of the AI Agent
└── README.md
```

---

## 🤖 The AI Agent Engine

The **Agent Engine** (`/agent-engine`) runs a continuous loop evaluating game states, risk parameters, and predefined strategies to play CKB Arcade games automatically. We've built an integration point ready for ML/AI strategies. 

**Core capabilities:**
- **Risk Management:** Includes configurable stop-loss limits, profit targets, and emergency balance floors.
- **Dynamic Strategies:** Configurable profiles (e.g., Aggressive, Conservative) that dictate action logic (Play, Wait, Stop).
- **Log Management:** Dual-output logging (console + daily rotating file logs).
- **AI Integration Point:** The `strategy.ts` module provides a clean `(AgentState, GameState) → AgentAction` integration point, serving as a swap-point to inject LLM-driven or ML-trained models.

---

## 🚀 Quick Start

### Prerequisites
- **Node.js** v18 or higher & **npm**
- A CKB wallet (JoyID, Spore, etc.)
- CKB testnet tokens ([Faucet](https://faucet.nervos.org/))

### 1. Installation

```bash
git clone https://github.com/GxNaitik/ckb-learning-track.git
cd ckb-learning-track/ckb_arcade_ai_agent

# Install Frontend
cd frontend && npm install && cd ..

# Install Backend
cd backend && npm install && cd ..

# Install Agent Engine
cd agent-engine && npm install && cd ..
```

### 2. Environment Variables

**Backend** (`backend/.env`):
```env
HOUSE_PRIVATE_KEY=<your_house_wallet_private_key>
PAYOUT_API_KEY=<your_api_key>
MAX_PAYOUT_CKB=10000
CKB_RPC_URL=https://testnet.ckb.dev/
PORT=8787
```

**Frontend** (`frontend/.env`):
```env
VITE_GAME_ADDRESS=<your_game_address_ckt1...>
VITE_PAYOUT_API_KEY=<your_api_key>
```

*(Note: Without `VITE_API_BASE` set, Vite proxies frontend API requests to `http://127.0.0.1:8787`)*

### 3. Run the Suite

Run the application components in separate terminals:

```bash
# Terminal 1 — Backend API
cd backend
npm run dev          # Starts on http://localhost:8787

# Terminal 2 — Frontend UI
cd frontend
npm run dev          # Starts on http://localhost:3000

# Terminal 3 — Agent Engine Loop
cd agent-engine
npm run run:agent    # Starts the autonomous player agent
```

---

## 🛠️ Tech Stack

**Agent Engine:** TypeScript, Node.js, File-based persistence, Custom Runner  
**Frontend:** React 18, TypeScript, Vite 5, Tailwind CSS, `@ckb-ccc/connector-react` (JoyID/Spore support), Canvas API  
**Backend:** Node.js, Express, `@ckb-ccc/core` (Crypto operations)  

---

## 🔒 Security & Verifiability

- **API key protection** on payout and house endpoints
- **Server-side reward verification** ensuring fair play, immune to client cheat engines
- **Anti-bot logic** restricting plays to daily session limits per wallet
- **Smart rate-limits & timeout strategies** automatically handled by the Agent Engine in continuous play.
- **Automatic RBF** (Replace-by-fee) transaction handling for CKB testnet anomalies

---

## 🤝 Contributing & License

1. Fork the repo, create a feature branch (`git checkout -b feature/agent-update`).
2. Commit your changes and push (`git push origin feature/agent-update`).
3. Open a Pull Request.

This project is licensed under the **MIT License**.

> **⚠️ Disclaimer:** This is a testnet demo project created for the CKB AI Agent Hackathon. All game activities use CKB testnet tokens with no real-world monetary value. Play responsibly.
