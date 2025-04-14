# 🚀 BNB Smart Chain Node via Docker Compose

This repository provides a clean and ready-to-use setup for running a **BNB Smart Chain (BSC)** Full node using Docker Compose.

> ✅ **Pre-configured for Mainnet**  
> 🐳 Runs in a Docker container with persistent storage  
> 📁 Includes instructions for switching to Testnet if needed

---

## 📦 Requirements

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- `wget`, `curl`, and `unzip` installed

---

## 📥 Download Configuration Files

You need to download the latest Mainnet or Testnet config files from the official BNB Chain GitHub and place them in the `config/` directory.

### ✅ Mainnet Config
```bash
wget $(curl -s https://api.github.com/repos/bnb-chain/bsc/releases/latest | grep browser_ | grep mainnet | cut -d\" -f4)
unzip mainnet.zip -d config
```

### ✅ Testnet Config
```bash
wget $(curl -s https://api.github.com/repos/bnb-chain/bsc/releases/latest | grep browser_ | grep testnet | cut -d\" -f4)
unzip testnet.zip -d config
```

`config/config.toml`
`config/genesis.json`

## ⚙️ Optional Parameters

You can adjust the following parameters inside the `docker-compose.yml` under the `command:` section, depending on your needs:

### 🔁 `--syncmode`
Specifies the synchronization mode.

- `snap` (default) – Fastest sync method using state snapshots.
- `full` – Full node sync, stores all historical state data (uses more disk & time).

### 🧊 `--snapshot`
Enables or disables loading from a snapshot file (if available).

- `false` (default) – Standard sync without importing snapshot files.
- `true` – Use a snapshot archive to accelerate sync (must be downloaded separately).

### 🧹 `--pruneancient`
Controls whether old block/state data is removed after syncing.

- When **enabled** (default in this setup), reduces disk usage significantly.
- If **disabled**, the node retains full history, which increases disk space consumption.

### 🧱 `--gcmode full / archive`
Defines how much state data is stored.

- `full` *(default)* – Prunes some old state data.
- `archive` – Stores **everything**, including all intermediate states (very heavy, for advanced use only).

> ⚠️ Use `archive` only if you specifically need historical state queries or run analytics tools.

## 🚀 How to Run

Once you’ve downloaded the config files and reviewed the parameters, you can run your node with the following commands:

### ✅ Start the node
```bash
docker compose up --build -d