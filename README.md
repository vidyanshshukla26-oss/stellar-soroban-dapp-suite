# ⭐ Stellar Soroban dApp Suite

**An interactive visualization suite for a production-style Soroban smart contract architecture** — inter-contract cross-calls, real-time event streaming, an automated test runner, and a CI/CD pipeline viewer, all in one dashboard.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-6-646CFF?logo=vite&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.8-3178C6?logo=typescript&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind-4-38BDF8?logo=tailwindcss&logoColor=white)

---

## 🔗 Live Demo

> _Add your deployed link here once hosted (Vercel / Netlify):_
> **[https://your-deployment-url.vercel.app](https://your-deployment-url.vercel.app)**

## 🎥 Demo Picture

<img width="1917" height="1041" alt="Screenshot 2026-08-28 004023" src="https://github.com/user-attachments/assets/baa8d87f-7f1e-4d2c-bb54-129e6800dd00" />

---

## 📖 Overview

**Stellar Soroban dApp Suite** ("Starlight Protocol") is a single-page React dashboard that shows what the surface of a production Soroban dApp looks like end-to-end: a liquidity vault UI, a contract explorer, a live event feed, a test-suite runner, and a CI/CD pipeline monitor — all wired together with a shared wallet and toast/notification system.

This project is currently a **frontend showcase**: the wallet, contract addresses, on-chain events, transaction records, test output, and CI/CD run shown in the UI are illustrative sample data used to demonstrate the interface and interaction flows, not live calls against Stellar Testnet/Mainnet. There is no `contracts/` (Rust/Soroban) workspace in this repo yet, and no wallet-extension (e.g. Freighter) integration.

Think of it as the **UI/UX layer and interaction design** for a Soroban dApp — the natural next step is wiring it up to real deployed contracts via `@stellar/stellar-sdk` and a Freighter connection (see [Roadmap](#-roadmap) below).

---

## ✨ Features

| Tab | What it shows |
|---|---|
| 🏦 **dApp Vault** | A deposit/swap/harvest dashboard for a simulated liquidity vault, with an animated testnet "faucet" action and live balance updates. |
| 📄 **Smart Contracts** | An explorer for sample Soroban contracts (Vault, Oracle, Token, Yield Distributor) — addresses, WASM hash, storage type, TTL, and callable methods with input forms. |
| ⚡ **Live Events** | A real-time-style feed of Soroban contract events (deposits, swaps, yield claims, cross-calls) with topics, ledger numbers, and transaction hashes. |
| 🧪 **Test Suite** | A runner UI presenting Rust/Soroban-SDK-style test suites — inter-contract communication tests, auth/security tests, and frontend tests — with pass/fail states and log output. |
| 🔁 **CI/CD Pipeline** | A visual pipeline (lint → test → build WASM → deploy) modeled on a real GitHub Actions workflow for Soroban contracts. |
| 📚 **Architecture Docs** | In-app documentation describing the intended contract architecture and cross-contract call graph. |

Additional UX details:
- Toast notification system for async actions (faucet requests, contract calls, etc.)
- Transaction inspector modal (fee, CPU instructions, memory, XDR envelope, cross-call trace)
- Fully responsive layout (mobile, tablet, desktop)
- Dark, terminal-inspired visual theme with `JetBrains Mono` + `Plus Jakarta Sans`

---

## 🛠 Tech Stack

- **React 19** + **TypeScript**
- **Vite 6** — dev server & build tooling
- **Tailwind CSS 4** (via `@tailwindcss/vite`)
- **lucide-react** — icon set
- **motion** (Framer Motion) — animations
- **canvas-confetti** — celebratory micro-interactions
- **Express** — included for optional local/server-side hosting of the built app
- **@google/genai** — included in dependencies for optional Gemini-powered features (not currently wired into any component)

---

## 🚀 Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) 18+
- npm (or `bun`, since a `bun.lock` is included)

### Installation

```bash
git clone https://github.com/vidyanshshukla26-oss/stellar-soroban-dapp-suite.git
cd stellar-soroban-dapp-suite
npm install
```

### Environment Variables

Copy the example env file and fill in your own values:

```bash
cp .env.example .env.local
```

| Variable | Description |
|---|---|
| `GEMINI_API_KEY` | Only required if you wire up Gemini-powered features. Not required to run the current dashboard. |
| `APP_URL` | Used for self-referential links if deploying behind a custom domain. |

### Run locally

```bash
npm run dev
```

The app runs at **http://localhost:3000**.

### Build for production

```bash
npm run build
npm run preview
```

### Type-check

```bash
npm run lint
```

---

## 📁 Project Structure

```
stellar-soroban-dapp-suite/
├── src/
│   ├── App.tsx                  # Root component, tab routing, wallet & toast state
│   ├── main.tsx                 # React entry point
│   ├── index.css                # Tailwind entry / global styles
│   ├── types.ts                 # Shared TypeScript types (wallet, contracts, events, tests…)
│   ├── data/
│   │   ├── contracts.ts         # Sample contract metadata & addresses
│   │   ├── tests.ts             # Sample test suite definitions
│   │   ├── cicd.ts              # Sample CI/CD pipeline stages + workflow YAML text
│   │   └── commits.ts           # Sample commit history data for the UI
│   ├── components/
│   │   ├── Navbar.tsx           # Tab navigation + wallet widget
│   │   ├── VaultDashboard.tsx   # "dApp Vault" tab
│   │   ├── ContractExplorer.tsx # "Smart Contracts" tab
│   │   ├── EventStreamer.tsx    # "Live Events" tab
│   │   ├── EventStreamingFeed.tsx
│   │   ├── TestRunner.tsx       # "Test Suite" tab
│   │   ├── CiCdPipeline.tsx     # "CI/CD Pipeline" tab
│   │   ├── ArchitectureDocs.tsx # "Architecture Docs" tab
│   │   ├── TransactionModal.tsx # Transaction inspector
│   │   └── Toast.tsx            # Notification system
├── index.html
├── vite.config.ts
├── tsconfig.json
├── package.json
└── .env.example
```

---

## 🗺 Roadmap

This repo currently demonstrates the **frontend interaction design** for a Soroban dApp. To take it to a fully live, production-grade dApp, the planned next steps are:

- [ ] Add a `contracts/` Rust workspace (Soroban SDK) implementing the Vault, Oracle, Token, and Yield Distributor contracts shown in the UI, with real inter-contract calls
- [ ] Write `cargo test` unit + inter-contract integration tests
- [ ] Deploy contracts to **Stellar Testnet** and replace sample addresses with real deployed contract IDs
- [ ] Integrate [`@stellar/stellar-sdk`](https://github.com/stellar/js-stellar-sdk) and [Freighter](https://www.freighter.app/) for real wallet connection and signing
- [ ] Replace the simulated event feed with real Soroban RPC `getEvents` polling/streaming
- [ ] Add a real GitHub Actions workflow (`.github/workflows/ci.yml`) matching the pipeline shown in the CI/CD tab
- [ ] Add frontend unit tests (Vitest + Testing Library)
- [ ] Record contract deployment addresses + a live transaction hash for documentation

---

## 📄 License

Licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

## 👤 Author

**Vidyansh Shukla**
[GitHub](https://github.com/vidyanshshukla26-oss)

---

<p align="center"><sub>Built as part of a Stellar Soroban smart contract learning track.</sub></p>
