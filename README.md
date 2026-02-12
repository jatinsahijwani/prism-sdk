# prism-sdk

**Write Circom. Compile. Deploy. Verify — one command away, Powered by Stellar Soroban & X-Ray**

An open-source (MIT) zero-knowledge toolkit that makes privacy-preserving apps simple and accessible on Soroban. Zero-setup for beginners: build compliant ZK circuits, generate proofs off-chain, and auto-deploy lightweight verifiers using Stellar's native X-Ray primitives (BN254 pairings + Poseidon hashes) for ultra-low fees and fast verification.

Perfect for confidential remittances, zkKYC, privacy pools, and selective disclosure — directly supporting Stellar's configurable privacy roadmap and global financial inclusion goals.

**MVP shipping live at Stellar Builders Camp McLeod Ganj (Feb 20–24, 2026)** — join the movement to unlock privacy on Stellar!

## ✨ Features

- 🧠 Write or use ready Circom circuits (optimized with Poseidon/Poseidon2 for fewer constraints)
- 🛠 **Compile** to `.r1cs`, `.wasm`, `.zkey` — **already implemented for latest Circom version** — plus auto-generated Rust/WASM verifier code leveraging X-Ray BN254 ops
- 🚀 Deploy verifier contract to Soroban (Testnet/Futurenet/Mainnet) with one command
- ✅ Verify proofs programmatically with a single JS function — fully abstracted, no manual Horizon/ABI handling
- 🧪 Test locally before deployment — no deep blockchain knowledge required
- 📊 Designed for hackathons & rapid prototyping: quick privacy demos on Stellar's fast, low-fee network

## 📦 Installation

```bash
npm install prism-sdk
```

## ⚡ Quick Start

### 1. Compile Circom Circuit (Already supports latest Circom!)

```bash
npx prism-sdk compile <path-to-your-circom-file>
```

- Compiles `.circom` → R1CS/WASM/ZKey
- Runs Groth16 trusted setup
- **Auto-generates Rust verifier template** using X-Ray primitives (BN254 pairings + Poseidon hashes)
- Outputs everything in `./<circuit-name>/` folder

### 2. Test Locally

```bash
npx prism-sdk test <path-to-generated-folder> <path-to-input.json>
```

- Generates proof & public signals
- Verifies off-chain → outputs `proof.json` & `public.json`

### 3. Deploy Verifier to Soroban

```bash
npx prism-sdk deploy <path-to-generated-folder> <STELLAR_SECRET_KEY> --network futurenet
```

- Builds & deploys auto-generated Rust/WASM verifier contract
- Uses Soroban CLI under the hood — fees from your account
- Options: `--network testnet|mainnet|futurenet`, `--optimize`

### 4. Verify Proof Programmatically

```js
const { verifyProof } = require('prism-sdk');

const result = await verifyProof({
  input: { /* your private/public inputs */ },
  artifactsPath: './yourCircuit/',           // generated folder
  contractId: 'C...VERIFIER_CONTRACT_ID',    // from deploy
  horizonUrl: 'https://horizon-testnet.stellar.org'
});

console.log(result ? '✅ Valid proof' : '❌ Invalid proof');
```

- Auto-generates proof → formats call → submits via Horizon → calls verifier
- Returns true/false (or detailed result)

You never touch snarkjs, soroban-sdk, or raw tx manually — Prism abstracts it all.

## 🛠 Commands Overview

| Command                                      | Description                                                                 |
|----------------------------------------------|-----------------------------------------------------------------------------|
| npx prism-sdk compile <path-to-circuit>      | Compiles Circom + Groth16 setup + auto-generates Rust verifier (latest Circom supported) |
| npx prism-sdk test <output-folder> <input.json> | Local proof generation & verification test                                 |
| npx prism-sdk deploy <output-folder> <secret-key> [options] | Deploys verifier contract to Soroban network                               |
| verifyProof({ input, artifactsPath, contractId, horizonUrl }) | Programmatic: generate + verify on-chain                                   |

## Why Prism for Stellar Builders & SCF?

- Leverages **X-Ray Protocol 25** (live) for cheap, native ZK verification — no expensive precompiles needed.
- Lowers ZK barriers → attracts more devs to Soroban for privacy-first apps (remittances, compliant DeFi, inclusion).
- Hackathon-ready: Ship zk demos in hours, not weeks.
- Community focus: Workshops planned post-camp targeting 200+ builders.
- Open-source & MIT — built for ecosystem growth.

Star the repo, try the compile command, and build your first zk app on Stellar!

**License**: MIT  
**Contributing**: Welcome — issues/PRs encouraged  
**Built by**: HackTour India [](https://x.com/HackTourIND) for the Stellar ecosystem 🚀
