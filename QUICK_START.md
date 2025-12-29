# ⚡ Quick Start Guide - Distributed Transactional System

## 🎯 Start in 5 Minutes

Follow this minimal setup guide to get the blockchain consensus system running locally.

### Prerequisites
- **Go 1.19+** or **Rust 1.70+**
- **Docker** (optional but recommended)
- **Git**

---

## 🚀 Option 1: Quick Start with Docker (Easiest)

### Step 1: Clone the Repository
```bash
git clone https://github.com/Rishav-raj-github/Distributed-transactional-system-with-blockchain-consensus.git
cd Distributed-transactional-system-with-blockchain-consensus
```

### Step 2: Start All Services
```bash
docker-compose up -d
```

### Step 3: Verify Installation
```bash
docker-compose ps
# Should show: consensus-node-1, consensus-node-2, consensus-node-3, ethereum-node

docker-compose logs -f consensus-node-1
```

✅ **System is ready!** Access at `http://localhost:8080/api/v1/health`

---

## 🛠️ Option 2: Local Setup with Go

### Step 1: Clone & Install Dependencies
```bash
git clone https://github.com/Rishav-raj-github/Distributed-transactional-system-with-blockchain-consensus.git
cd Distributed-transactional-system-with-blockchain-consensus
go mod download
go mod verify
```

### Step 2: Create Configuration
```bash
cp config/node1.yaml.example config/node1.yaml
```

Edit `config/node1.yaml` if needed (defaults work fine).

### Step 3: Run a Single Node
```bash
go run cmd/node/main.go --config config/node1.yaml
```

✅ **Node started!** Listen for: `"Server listening on port 8080"`

---

## 🌐 Option 3: Multi-Node Local Network

### Start Consensus Network (3 Terminals)

**Terminal 1:**
```bash
go run cmd/node/main.go --config config/node1.yaml
```

**Terminal 2:**
```bash
go run cmd/node/main.go --config config/node2.yaml
```

**Terminal 3:**
```bash
go run cmd/node/main.go --config config/node3.yaml
```

Wait 5 seconds. Nodes will auto-discover via gossip protocol.

---

## 📤 Submit Your First Trade

### Place a Buy Order
```bash
curl -X POST http://localhost:8080/api/v1/orders \
  -H "Content-Type: application/json" \
  -d '{
    "symbol": "BTC/USD",
    "side": "buy",
    "quantity": 0.5,
    "price": 45000.00
  }'
```

### Expected Response
```json
{
  "order_id": "order_abc123",
  "status": "pending",
  "timestamp": "2025-01-15T10:30:45Z"
}
```

### Monitor Order Status
```bash
curl http://localhost:8080/api/v1/orders/order_abc123
```

---

## 📊 Check System Health

### Node Status
```bash
curl http://localhost:8080/api/v1/health
```

### Order Book
```bash
curl http://localhost:8080/api/v1/orderbook/BTC-USD
```

### Consensus Metrics
```bash
curl http://localhost:8080/api/v1/metrics
```

---

## 🧪 Run Unit Tests

### Go Tests
```bash
go test ./...
go test -v ./consensus -run TestPBFT
```

### Coverage
```bash
go test -cover ./...
```

---

## 📝 Configuration Overview

### Key Files
- `config/node1.yaml` - Single node config
- `config/docker-compose.yml` - Multi-node setup
- `.env` - Environment variables (copy from `.env.example`)

### Common Customizations

**Change Consensus Algorithm:**
```yaml
consensus:
  algorithm: pbft  # Options: pbft, raft, custom
```

**Adjust Block Time:**
```yaml
consensus:
  block_time: 2s  # Reduce for faster consensus
```

**Set Max Peers:**
```yaml
network:
  max_peers: 100  # Increase for larger networks
```

---

## 🔗 Smart Contract Deployment (Optional)

### Setup Ethereum Environment
```bash
cd contracts
npm install
npx hardhat node  # In another terminal
```

### Deploy Settlement Contract
```bash
npx hardhat run scripts/deploy.js --network localhost
```

Copy the contract address and update `.env`.

---

## ⚠️ Troubleshooting

### Port Already in Use
```bash
# Kill process on port 8080
lsof -ti:8080 | xargs kill -9

# Or use different port
go run cmd/node/main.go --port 8081
```

### Database Connection Error
```bash
# Ensure PostgreSQL is running
psql postgres://user:password@localhost:5432/transactional

# Or use SQLite for local testing
export DB_CONNECTION_STRING="sqlite://local.db"
```

### Nodes Not Connecting
```bash
# Check network connectivity
netstat -an | grep 9000

# Review logs
docker-compose logs consensus-node-1
```

---

## 📚 Next Steps

1. **Read Full Docs**: See [README.md](README.md)
2. **Understand Architecture**: Check [notebooks/01_System_Overview_Architecture.ipynb](notebooks/01_System_Overview_Architecture.ipynb)
3. **Learn Consensus**: Dive into [notebooks/02_Consensus_Protocol_Deep_Dive.ipynb](notebooks/02_Consensus_Protocol_Deep_Dive.ipynb)
4. **Run Examples**: Execute [notebooks/03_Order_Matching_Engine.ipynb](notebooks/03_Order_Matching_Engine.ipynb)
5. **Performance Test**: Use [notebooks/05_Performance_Benchmarking.ipynb](notebooks/05_Performance_Benchmarking.ipynb)

---

## 📞 Need Help?

- Check [GitHub Issues](https://github.com/Rishav-raj-github/Distributed-transactional-system-with-blockchain-consensus/issues)
- Review [API Documentation](docs/API.md)
- See [Configuration Guide](docs/CONFIGURATION.md)

---

## 🎓 Learning Resources

| Topic | Resource |
|-------|----------|
| Consensus Protocols | `notebooks/02_Consensus_Protocol_Deep_Dive.ipynb` |
| Order Matching | `notebooks/03_Order_Matching_Engine.ipynb` |
| Cross-Chain | `notebooks/04_Cross_Chain_Settlement.ipynb` |
| Performance | `notebooks/05_Performance_Benchmarking.ipynb` |
| Deployment | `docs/DEPLOYMENT_GUIDE.md` |

---

**Happy Trading! 🚀**
