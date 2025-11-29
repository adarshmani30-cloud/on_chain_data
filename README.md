# 🌐 On Chain Data
<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Node](https://img.shields.io/badge/node-%3E%3D16.0.0-green.svg)
![License](https://img.shields.io/badge/license-ISC-yellow.svg)

**A high-performance blockchain data streaming platform built on Somnia Network**

*Real-time player score tracking with on-chain persistence and RESTful API access*

[Features](#-features) • [Architecture](#-architecture) • [Getting Started](#-getting-started) • [API Reference](#-api-reference) • [Examples](#-examples)

---

</div>

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Technology Stack](#-technology-stack)
- [Getting Started](#-getting-started)
- [API Reference](#-api-reference)
- [Environment Configuration](#-environment-configuration)
- [Usage Examples](#-usage-examples)
- [Deployment](#-deployment)
- [Error Handling](#-error-handling)
- [Best Practices](#-best-practices)
- [Contributing](#-contributing)

---

## 🎯 Overview

*On Chain Data** is an enterprise-grade backend service that bridges Web2 applications with the Somnia blockchain network. It provides a robust RESTful API for publishing and retrieving player performance data with cryptographic integrity and decentralized storage.

### Use Cases

- 🎮 **Gaming Leaderboards** - Real-time player rankings with blockchain verification
- 🏆 **Tournament Systems** - Transparent, tamper-proof competition results
- 📊 **Analytics Platforms** - Immutable data streams for performance tracking
- 🔐 **Identity Management** - Address-based player identification and scoring
- 🌍 **Cross-Platform Integration** - Unified data layer for multi-platform games

---

## ✨ Features

### Core Capabilities

| Feature | Description |
|---------|-------------|
| 🔒 **Blockchain Persistence** | All data stored immutably on Somnia Dream network |
| ⚡ **Real-time Streaming** | Low-latency data publication and retrieval |
| 🛡️ **Address Validation** | Built-in Ethereum address checksum verification |
| 📊 **Automatic Deduplication** | Intelligent player score aggregation |
| 🔄 **Schema Management** | Auto-registration with conflict resolution |
| 🌐 **CORS Enabled** | Cross-origin support for web applications |
| 📈 **Leaderboard Generation** | Automatic ranking and sorting |
| 🔍 **Data Integrity** | Schema-enforced type safety |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                            │
│  (Web Apps, Mobile Apps, Game Clients, Admin Panels)          │
└───────────────────────┬─────────────────────────────────────────┘
                        │
                        │ HTTPS/REST
                        ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API GATEWAY LAYER                          │
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐        │
│  │ GET /schema  │  │ POST /publish│  │  GET /data   │        │
│  └──────────────┘  └──────────────┘  └──────────────┘        │
│                                                                 │
│  • CORS Management    • Input Validation   • Error Handling   │
└───────────────────────┬─────────────────────────────────────────┘
                        │
                        │ Viem SDK
                        ▼
┌─────────────────────────────────────────────────────────────────┐
│                   BLOCKCHAIN ABSTRACTION                        │
│                                                                 │
│  ┌──────────────────────────────────────────────────────┐     │
│  │           Somnia Streams SDK (@somnia-chain)         │     │
│  │                                                       │     │
│  │  • Schema Registration    • Data Encoding            │     │
│  │  • Transaction Management • Query Optimization       │     │
│  └──────────────────────────────────────────────────────┘     │
└───────────────────────┬─────────────────────────────────────────┘
                        │
                        │ RPC (HTTP)
                        ▼
┌─────────────────────────────────────────────────────────────────┐
│                     SOMNIA DREAM NETWORK                        │
│                  (Chain ID: 50312)                              │
│                                                                 │
│  • Consensus Layer        • Smart Contract Execution           │
│  • State Management       • Transaction Pool                   │
│  • Block Production       • Data Availability                  │
└─────────────────────────────────────────────────────────────────┘
```

### Component Breakdown

#### 1. **Express Server** (`app.js`)
- Central HTTP server orchestrating all API routes
- CORS middleware for cross-origin resource sharing
- JSON body parsing for request handling
- Graceful error propagation

#### 2. **API Routes** (`routes/streams.js`)
- **Schema Management**: Automated registration and ID computation
- **Data Publication**: Validated data encoding and blockchain submission
- **Data Retrieval**: Filtered queries with leaderboard generation
- **Transaction Management**: Asynchronous tx confirmation

#### 3. **Chain Configuration** (`dream-chain.js`)
- Network definition for Somnia Dream testnet
- RPC endpoint configuration
- Native currency specifications (STT token)

#### 4. **Publisher Service** (`publisher.js`)
- Standalone data publishing daemon
- Configurable interval-based submissions
- Schema registration with idempotency

#### 5. **Subscriber Service** (`subscriber.js`)
- Real-time data monitoring utility
- Continuous polling for new entries
- Duplicate detection and filtering

---

## 🛠️ Technology Stack

### Backend Framework
- **Node.js** (v16+) - JavaScript runtime
- **Express.js** (v5.1.0) - Web application framework

### Blockchain Integration
- **Viem** (v2.38.6) - Lightweight Ethereum library
  - Public/Wallet client management
  - Address validation and checksumming
  - Transaction receipt handling
- **@somnia-chain/streams** (v0.9.5) - Somnia SDK
  - Schema registration and encoding
  - Data stream management

### Utilities
- **dotenv** (v17.2.3) - Environment variable management
- **cors** (v2.8.5) - Cross-origin resource sharing

### Network
- **Somnia Dream Network**
  - Chain ID: `50312`
  - RPC: `https://dream-rpc.somnia.network`
  - Native Token: STT

---

## 🚀 Getting Started

### Prerequisites

```bash
Node.js >= 16.0.0
npm >= 7.0.0
```

### Installation

```bash
# Clone the repository
git clone https://github.com/adarshmani30-cloud/on_chain_data.git
cd on_chain_data

# Install dependencies
npm install

# Configure environment variables
cp .env.example .env
```

### Environment Setup

Create a `.env` file in the project root:

```env
# Wallet Configuration
PRIVATE_KEY=your_wallet_private_key_here

# Publisher Configuration
PUBLISHER_WALLET=0xYourPublisherWalletAddress

# Server Configuration (Optional)
PORT=3000
```

> ⚠️ **Security Warning**: Never commit `.env` files. Keep private keys secure.

### Running the Application

#### Development Mode
```bash
npm run dev
```
*Uses nodemon for hot-reloading*

#### Production Mode
```bash
npm start
```

#### Standalone Services
```bash
# Run publisher daemon
node publisher.js

# Run subscriber monitor
node subscriber.js
```

---

## 📡 API Reference

### Base URL
```
Production:  https://on-chain-data-two.vercel.app
Local:       http://localhost:3000
```

---

### 🔹 GET `/api/schema`

Retrieve the computed schema ID for the player scoring system.

#### Response
```json
{
  "schemaId": "0x1234567890abcdef..."
}
```

#### Example
```bash
curl https://on-chain-data-two.vercel.app/api/schema
```

---

### 🔹 POST `/api/publish`

Publish a player's score to the blockchain.

#### Request Body
```json
{
  "player": "0xA24d7ECD79B25CE6C66f1Db9e06b66Bd11632E00",
  "score": 1500
}
```

#### Validation Rules
| Field | Type | Constraints |
|-------|------|-------------|
| `player` | string | Valid Ethereum address (42 chars, checksum optional) |
| `score` | number | Non-negative integer (0 to 2^256-1) |

#### Success Response (200)
```json
{
  "success": true,
  "txHash": "0xabcdef1234567890...",
  "player": "0xA24d7ECD79B25CE6C66f1Db9e06b66Bd11632E00",
  "score": 1500
}
```

#### Error Responses

**400 Bad Request**
```json
{
  "error": "Invalid Ethereum address format"
}
```

**500 Internal Server Error**
```json
{
  "error": "Transaction failed: insufficient funds"
}
```

#### Example
```bash
# Windows CMD
curl -X POST https://on-chain-data-two.vercel.app/api/publish ^
  -H "Content-Type: application/json" ^
  -d "{\"player\":\"0xa24d7ecd79b25ce6c66f1db9e06b66bd11632e00\",\"score\":1500}"

# PowerShell
curl -X POST https://on-chain-data-two.vercel.app/api/publish `
  -H "Content-Type: application/json" `
  -d '{"player":"0xa24d7ecd79b25ce6c66f1db9e06b66bd11632e00","score":1500}'

# Bash/Linux
curl -X POST https://on-chain-data-two.vercel.app/api/publish \
  -H "Content-Type: application/json" \
  -d '{"player":"0xa24d7ecd79b25ce6c66f1db9e06b66bd11632e00","score":1500}'
```

---

### 🔹 GET `/api/data`

Retrieve the complete leaderboard with ranked players.

#### Response
```json
{
  "totalPlayers": 3,
  "leaderboard": [
    {
      "rank": 1,
      "player": "0xA24d7ECD79B25CE6C66f1Db9e06b66Bd11632E00",
      "score": "2500"
    },
    {
      "rank": 2,
      "player": "0x742d35Cc6634C0532925a3b844Bc9e7595f0bEb",
      "score": "1800"
    },
    {
      "rank": 3,
      "player": "0x1234567890123456789012345678901234567890",
      "score": "950"
    }
  ]
}
```

#### Response Fields
| Field | Description |
|-------|-------------|
| `totalPlayers` | Number of unique players |
| `leaderboard` | Array of player rankings |
| `rank` | Position in leaderboard (1-indexed) |
| `player` | Checksummed Ethereum address |
| `score` | Highest recorded score (string format) |

#### Business Logic
- **Deduplication**: Only highest score per player is retained
- **Sorting**: Descending order by score
- **Ranking**: Sequential numbering from rank 1

#### Example
```bash
curl https://on-chain-data-two.vercel.app/api/data
```

---

## 🔧 Environment Configuration

### Required Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `PRIVATE_KEY` | Wallet private key for signing transactions | `0xabcd...` |
| `PUBLISHER_WALLET` | Address of the data publisher | `0x1234...` |

### Optional Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | HTTP server port | `3000` |

---

## 💡 Usage Examples

### JavaScript/TypeScript (Fetch API)

```javascript
// Publish a score
async function publishScore(playerAddress, score) {
  const response = await fetch('https://on-chain-data-two.vercel.app/api/publish', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      player: playerAddress,
      score: score
    })
  });
  
  const data = await response.json();
  console.log('Transaction Hash:', data.txHash);
  return data;
}

// Retrieve leaderboard
async function getLeaderboard() {
  const response = await fetch('https://on-chain-data-two.vercel.app/api/data');
  const data = await response.json();
  
  console.log(`Total Players: ${data.totalPlayers}`);
  data.leaderboard.forEach(entry => {
    console.log(`#${entry.rank} - ${entry.player}: ${entry.score} points`);
  });
  
  return data;
}

// Usage
await publishScore('0xa24d7ecd79b25ce6c66f1db9e06b66bd11632e00', 1500);
await getLeaderboard();
```

### Python (Requests Library)

```python
import requests

BASE_URL = 'https://on-chain-data-two.vercel.app/api'

def publish_score(player_address: str, score: int):
    """Publish a player's score to the blockchain"""
    response = requests.post(
        f'{BASE_URL}/publish',
        json={'player': player_address, 'score': score}
    )
    data = response.json()
    print(f"Transaction Hash: {data['txHash']}")
    return data

def get_leaderboard():
    """Retrieve the current leaderboard"""
    response = requests.get(f'{BASE_URL}/data')
    data = response.json()
    
    print(f"Total Players: {data['totalPlayers']}")
    for entry in data['leaderboard']:
        print(f"#{entry['rank']} - {entry['player']}: {entry['score']} points")
    
    return data

# Usage
publish_score('0xa24d7ecd79b25ce6c66f1db9e06b66bd11632e00', 1500)
get_leaderboard()
```

### React Component

```jsx
import { useState, useEffect } from 'react';

const API_BASE = 'https://on-chain-data-two.vercel.app/api';

function Leaderboard() {
  const [leaderboard, setLeaderboard] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetchLeaderboard();
  }, []);

  const fetchLeaderboard = async () => {
    try {
      const response = await fetch(`${API_BASE}/data`);
      const data = await response.json();
      setLeaderboard(data.leaderboard);
    } catch (error) {
      console.error('Failed to fetch leaderboard:', error);
    } finally {
      setLoading(false);
    }
  };

  const submitScore = async (playerAddress, score) => {
    try {
      const response = await fetch(`${API_BASE}/publish`, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ player: playerAddress, score })
      });
      
      const data = await response.json();
      alert(`Score submitted! Tx: ${data.txHash}`);
      fetchLeaderboard(); // Refresh leaderboard
    } catch (error) {
      alert(`Error: ${error.message}`);
    }
  };

  if (loading) return <div>Loading...</div>;

  return (
    <div>
      <h2>Leaderboard</h2>
      <table>
        <thead>
          <tr>
            <th>Rank</th>
            <th>Player</th>
            <th>Score</th>
          </tr>
        </thead>
        <tbody>
          {leaderboard.map((entry) => (
            <tr key={entry.player}>
              <td>#{entry.rank}</td>
              <td>{entry.player}</td>
              <td>{entry.score}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}

export default Leaderboard;
```

---

## 🌍 Deployment

### Vercel (Recommended)

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel --prod

# Set environment variables
vercel env add PRIVATE_KEY
vercel env add PUBLISHER_WALLET
```

### Docker

```dockerfile
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]
```

```bash
# Build and run
docker build -t somnia-streams .
docker run -p 3000:3000 --env-file .env somnia-streams
```

### Traditional VPS

```bash
# Install PM2
npm install -g pm2

# Start with PM2
pm2 start app.js --name "somnia-api"

# Setup auto-restart on reboot
pm2 startup
pm2 save
```

---

## ⚠️ Error Handling

### Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| `Invalid Ethereum address format` | Malformed player address | Use 42-character hex string starting with `0x` |
| `Score must be a non-negative number` | Negative or NaN score | Ensure score is >= 0 |
| `Cannot read properties of undefined` | Missing request body | Send valid JSON with `Content-Type: application/json` |
| `IntegerOutOfRangeError` | Score too large | Keep score within uint256 range |
| `Transaction failed` | Insufficient gas or network issues | Check wallet balance and RPC connectivity |

### Error Response Format

```json
{
  "error": "Human-readable error message",
  "message": "Technical error details (optional)"
}
```

---

## 🎯 Best Practices

### Security
- ✅ Never expose private keys in code or logs
- ✅ Use environment variables for sensitive data
- ✅ Validate all user inputs before processing
- ✅ Implement rate limiting for public endpoints
- ✅ Use HTTPS in production

### Performance
- ✅ Cache schema IDs to reduce computation
- ✅ Implement connection pooling for database/RPC
- ✅ Use async/await for non-blocking operations
- ✅ Consider pagination for large leaderboards

### Development
- ✅ Use TypeScript for type safety (recommended upgrade)
- ✅ Implement comprehensive logging
- ✅ Write unit tests for critical paths
- ✅ Document API changes in this README
- ✅ Follow semantic versioning

---

## 🏛️ Project Structure

```
on_chain_data/
├── app.js                  # Express server entry point
├── dream-chain.js          # Somnia network configuration
├── publisher.js            # Automated data publishing service
├── subscriber.js           # Real-time data monitoring service
├── package.json            # Dependencies and scripts
├── .env                    # Environment variables (gitignored)
├── routes/
│   └── streams.js          # API route handlers
└── README.md               # This file
```

---

## 📊 Data Schema

### Player Score Schema
```solidity
struct PlayerScore {
    address player;    // Ethereum address
    uint256 score;     // Non-negative integer score
}
```

### Schema Encoding
- **Format**: ABI-encoded tuple
- **Schema ID**: Computed via keccak256
- **Storage**: Immutable on Somnia blockchain

---

## 🔍 Monitoring & Debugging

### Health Check
```bash
curl https://on-chain-data-two.vercel.app/api/schema
```
Expected: Returns schema ID (should be consistent)

### Transaction Verification
Visit Somnia block explorer with returned `txHash`:
```
https://explorer.somnia.network/tx/{txHash}
```

### Logs
```bash
# Local development
npm run dev

# Production (PM2)
pm2 logs somnia-api

# Docker
docker logs <container_id>
```

---

## 🤝 Contributing

We welcome contributions! Please follow these guidelines:

1. **Fork** the repository
2. Create a **feature branch** (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. Open a **Pull Request**

### Code Standards
- Follow existing code style
- Add comments for complex logic
- Update README for API changes
- Ensure all tests pass

---

## 📜 License

This project is licensed under the ISC License.

---

## 🙏 Acknowledgments

- **Somnia Network** - For providing the blockchain infrastructure
- **Viem** - For the excellent Ethereum library
- **Express.js** - For the robust web framework

---

<div align="center">

**Built with ❤️ for the decentralized future**

[⬆ Back to top](#-somnia-streams-data-hub)

</div>
