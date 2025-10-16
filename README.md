
# 🧱 Upgradeable Smart Contract (UUPS Proxy)

> A Foundry-based project demonstrating upgradeable smart contracts using the **UUPS Proxy pattern** from OpenZeppelin. Includes full deployment, upgrade, and testing scripts with a Makefile for streamlined automation.

[![Foundry](https://img.shields.io/badge/Foundry-Forge-orange?logo=rust)](https://getfoundry.sh/)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.19-blue?logo=solidity)](https://soliditylang.org/)
[![OpenZeppelin](https://img.shields.io/badge/OpenZeppelin-UUPS-4E8EE7?logo=ethereum)](https://docs.openzeppelin.com/contracts/4.x/api/proxy)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-Foundry-blueviolet)](https://book.getfoundry.sh/)

---

## 📖 Overview

This project showcases how to **deploy, upgrade, and test** smart contracts using the **UUPS upgradeable pattern** in Solidity. It is inspired by the [Cyfrin Upgrades Course](https://github.com/Cyfrin/foundry-upgrades-cu) and is fully compatible with **Foundry** and **OpenZeppelin's upgradeable libraries**.

---

## 🏗 Project Structure

```
├── src/
│   ├── BoxV1.sol               # Initial implementation (Upgradeable contract V1)
│   └── BoxV2.sol               # Upgraded version (adds setValue)
├── script/
│   ├── DeployBox.s.sol         # Script to deploy BoxV1 via ERC1967Proxy
│   └── UpgradeBox.s.sol        # Script to upgrade proxy to BoxV2
├── test/
│   └── DeployAndUpgradeTest.t.sol  # Foundry tests for deployment and upgrade logic
├── Makefile                    # Automation for build, deploy, upgrade, test
├── foundry.toml                # Foundry configuration and remappings
└── README.md                   # Project documentation
```

---

## ⚡ Features

- ✅ **UUPS Upgrade Pattern** - Universal Upgradeable Proxy Standard implementation
- ✅ **Automated Deployment** - Scripts for deployment and upgrades using Foundry
- ✅ **Comprehensive Testing** - Full test coverage for deployment and upgrade lifecycle
- ✅ **Makefile Automation** - Simplified workflows for development and deployment
- ✅ **Multi-Network Support** - Works on local Anvil, Sepolia, and mainnet
- ✅ **Storage Preservation** - Maintains state between contract upgrades

---

## 🚀 Quick Start

### 1️⃣ Clone & Setup

```bash
git clone https://github.com/BELALZEDAN/upgradeable-smart-contracts-foundry.git

cd upgradeable-smart-contracts-foundry

make install
```

### 2️⃣ Build & Test

```bash
make build
make test
```

### 3️⃣ Deploy & Upgrade

```bash
# Start local node
make anvil

# Deploy BoxV1
make deploy

# Upgrade to BoxV2
make upgrade
```

---

## 🧠 Core Contracts

### 📦 BoxV1.sol
```solidity
// Initial implementation with:
// - initialize() function for proxy initialization
// - getValue() to read stored data
// - UUPSUpgradeable and Ownable patterns
// - version() returns 1
```

### 🔄 BoxV2.sol
```solidity
// Upgraded version adding:
// - setValue(uint256) function for mutability
// - version() returns 2
// - Preserved storage layout from V1
```

---

## 🤖 How Upgrades Work

### UUPS Proxy Architecture

```
User ──────→ ERC1967Proxy ──────→ BoxV1 (Implementation)
                    │
                    └────────────→ BoxV2 (Upgraded Implementation)
```

### 🔧 Upgrade Process

1. **Initial Deployment**: 
   - `BoxV1` implementation contract deployed
   - `ERC1967Proxy` deployed pointing to `BoxV1`
   - Proxy is initialized via `initialize()` function

2. **Storage Preservation**:
   - Proxy contract holds all storage data
   - Implementation contracts are stateless
   - Storage layout must remain compatible between upgrades

3. **Secure Upgrade**:
   - Only contract owner can perform upgrades
   - `upgradeTo()` function updates implementation address
   - Storage remains intact during upgrade

### 📝 Key Concepts

- **Proxy Contract**: Holds storage and delegates calls to implementation
- **Implementation**: Contains the logic, can be replaced
- **UUPS Pattern**: Upgrade logic is in the implementation, not the proxy
- **Storage Gaps**: Reserved storage slots for future variable additions

---

## 🧰 Makefile Commands

| Command | Description | Usage Example |
|---------|-------------|---------------|
| `make install` | Install project dependencies | `make install` |
| `make build` | Compile all contracts | `make build` |
| `make test` | Run comprehensive test suite | `make test` |
| `make deploy` | Deploy BoxV1 with proxy | `make deploy` |
| `make upgrade` | Upgrade to BoxV2 | `make upgrade` |
| `make anvil` | Start local development node | `make anvil` |
| `make format` | Format Solidity code | `make format` |
| `make clean` | Remove build artifacts | `make clean` |

### 🎯 Deployment Examples

**Local Development:**
```bash
make anvil
make deploy
make upgrade
```

**Testnet Deployment:**
```bash
make deploy ARGS="--network sepolia"
make upgrade ARGS="--network sepolia"
```

---

## 🧪 Testing

Run the complete test suite:
```bash
make test
```

**Test Coverage Includes:**
- ✅ Proxy deployment and initialization
- ✅ Version verification (V1 → V2)
- ✅ Storage preservation between upgrades
- ✅ Upgrade authorization security
- ✅ Functionality validation post-upgrade

---

## 🛠 Technology Stack

- **[Foundry](https://getfoundry.sh/)** - Ethereum development framework
- **[OpenZeppelin](https://docs.openzeppelin.com/contracts/)** - Upgradeable smart contract libraries
- **[Solidity 0.8.19](https://docs.soliditylang.org/)** - Smart contract programming language
- **[Make](https://www.gnu.org/software/make/)** - Build automation tool
- **[ERC1967 Proxy](https://eips.ethereum.org/EIPS/eip-1967)** - Standard proxy storage slots

---

## 📄 License

This project is licensed under the **MIT License**. Feel free to use, modify, and distribute with attribution.

---

## 👨💻 Author

**Belal Zedan**  
Blockchain & Smart Contract Developer  
💼 [GitHub](https://github.com/BELALZEDAN/)  
🔗 [LinkedIn](https://www.linkedin.com/in/belal-zedan-342aa1225/)

---

## 🔗 Resources

- [OpenZeppelin Upgradeable Contracts](https://docs.openzeppelin.com/contracts/4.x/upgradeable)
- [UUPS EIP-1822](https://eips.ethereum.org/EIPS/eip-1822)
- [Foundry Book](https://book.getfoundry.sh/)
- [Cyfrin Upgrades Course](https://github.com/Cyfrin/foundry-upgrades-cu)
