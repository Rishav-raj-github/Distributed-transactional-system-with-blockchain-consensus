# Distributed Transactional System with Blockchain Consensus

![Status](https://img.shields.io/badge/status-active-success.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

> High-performance distributed transactional system with custom blockchain consensus protocol for secure, low-latency order matching and cross-chain settlement

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [Roadmap](#roadmap)
- [License](#license)
- [Contact](#contact)

## 🎯 Overview

This project implements a **distributed transactional system** that enables **secure, low-latency, real-time order matching** across multiple market participants using blockchain consensus mechanisms.

The system is designed to:

- ✅ Maintain distributed order books across a peer-to-peer network
- ✅ Achieve high throughput with a **custom consensus protocol**
- ✅ Perform **cross-chain trade settlement** using smart contracts
- ✅ Provide fault tolerance and high availability

## 🚀 Key Features

### Custom Consensus Protocol
Implement a novel consensus algorithm optimized for financial transactions, potentially based on epidemic protocols like BECP which outperforms traditional Paxos and PBFT by 1.196x in throughput.

### Real-time Order Book
Maintain distributed order books across multiple nodes with microsecond-level synchronization.

### Smart Contract Integration
Develop smart contracts for automated trade execution and settlement on Ethereum.

### Multi-chain Architecture
Support cross-chain capabilities for seamless asset transfers.

### High Availability
Fault-tolerant design ensuring continuous operation even during node failures.

## 🏗️ Architecture

The system follows a layered architecture:

```
┌─────────────────────────────────────────┐
│       Client Layer (REST API)          │
├─────────────────────────────────────────┤
│     Order Matching Engine (P2P)        │
├─────────────────────────────────────────┤
│   Consensus Layer (Custom Protocol)     │
├─────────────────────────────────────────┤
│  Settlement Layer (Smart Contracts)     │
├─────────────────────────────────────────┤
│      Blockchain Layer (Ethereum)        │
└─────────────────────────────────────────┘
```

### Workflow

1. **Peers** run order book replicas
2. Orders broadcast via gossip protocol
3. Consensus nodes confirm and settle trades
4. Settlement recorded on blockchain

## 🛠️ Tech Stack

- **Backend**: Go / Rust
- **Consensus Layer**: Custom Protocol (inspired by PBFT, Raft, EPID)
- **Blockchain**: Ethereum + Solidity
- **Database**: LevelDB / RocksDB
- **Networking**: gRPC, WebSockets
- **Infrastructure**: Docker, Kubernetes

## 📋 Prerequisites

Before running this project, ensure you have the following installed:

- **Go** 1.19+ or **Rust** 1.70+
- **Docker** 20.10+
- **Kubernetes** 1.24+ (for production deployment)
- **Node.js** 16+ (for smart contract development)
- **Truffle** or **Hardhat** (Ethereum development framework)
- **PostgreSQL** or **LevelDB**
- **Git**

## 📦 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Rishav-raj-github/Distributed-trading-system-with-blockchain-consensus.git
cd Distributed-trading-system-with-blockchain-consensus
```

### 2. Install Dependencies

#### For Go Backend:

```bash
go mod download
go mod verify
```

#### For Rust Backend:

```bash
cargo build --release
```

### 3. Set Up Smart Contracts

```bash
cd contracts
npm install
npx hardhat compile
```

### 4. Configure Environment

Create a `.env` file in the project root:

```env
NODE_ENV=development
PORT=8080
DB_CONNECTION_STRING=postgresql://user:password@localhost:5432/transactional
BLOCKCHAIN_RPC_URL=http://localhost:8545
CONSENSUS_ALGORITHM=pbft
NETWORK_PORT=9000
```

### 5. Run Database Migrations

```bash
make migrate-up
```

## 🎮 Usage

### Running Locally

#### Start a Single Node

```bash
# For Go
go run cmd/node/main.go --config config/node1.yaml

# For Rust
cargo run --bin node -- --config config/node1.yaml
```

#### Start Multiple Consensus Nodes

```bash
# Terminal 1
go run cmd/node/main.go --config config/node1.yaml

# Terminal 2
go run cmd/node/main.go --config config/node2.yaml

# Terminal 3
go run cmd/node/main.go --config config/node3.yaml
```

### Using Docker

```bash
# Build images
docker-compose build

# Start all services
docker-compose up -d

# Check logs
docker-compose logs -f
```

### Deploy to Kubernetes

```bash
# Apply configurations
kubectl apply -f k8s/

# Check status
kubectl get pods -n transactional-system
```

### Submit Trades via REST API

```bash
curl -X POST http://localhost:8080/api/v1/orders \
  -H "Content-Type: application/json" \
  -d '{
    "symbol": "BTC/USD",
    "side": "buy",
    "quantity": 1.5,
    "price": 45000.00
  }'
```

### Monitor Trade Finality

View confirmed trades on blockchain explorer:

- Local: http://localhost:8545
- Testnet: https://goerli.etherscan.io

## ⚙️ Configuration

Key configuration parameters in `config.yaml`:

```yaml
consensus:
  algorithm: "pbft"  # Options: pbft, raft, custom
  block_time: 2s
  validators: 4

network:
  p2p_port: 9000
  api_port: 8080
  max_peers: 50

blockchain:
  network: "ethereum"
  rpc_url: "http://localhost:8545"
  contract_address: "0x..."

orderbook:
  depth: 100
  tick_size: 0.01
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

Please ensure:

- Code follows project style guidelines
- All tests pass (`make test`)
- Documentation is updated

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## 🗺️ Roadmap

- [x] Core consensus protocol implementation
- [x] Basic order matching engine
- [x] Ethereum smart contract integration
- [ ] Cross-chain bridge implementation
- [ ] Advanced order types (stop-loss, limit orders)
- [ ] WebSocket streaming API
- [ ] Performance optimization (target: 10,000 TPS)
- [ ] Security audit
- [ ] Mainnet deployment

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📧 Contact

**Project Maintainer**: Rishav Raj

- GitHub: [@Rishav-raj-github](https://github.com/Rishav-raj-github)
- Repository: [Distributed-trading-system-with-blockchain-consensus](https://github.com/Rishav-raj-github/Distributed-trading-system-with-blockchain-consensus)

## 🙏 Acknowledgments

- Inspired by PBFT, Raft, and epidemic consensus protocols
- Built with Ethereum smart contract standards
- Community contributions and feedback

⭐ **Star this repository** if you find it helpful!
