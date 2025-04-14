# Bitz Node Miner Full Setup Guide (PC, VPS, Mac)

## 🔗 Official Contract Address (Eclipse Network)
```
64mggk2nXg6vHC1qCdsZdEFzd5QGN4id54Vbho4PswCF
```

---

## 🧰 Prerequisites
- Backpack wallet (or Eclipse-compatible wallet) [Download here](https://www.backpack.app)
- 0.0005+ ETH on the Eclipse network

---

## 1️⃣ Dependencies

### For WSL / VPS
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl nano build-essential -y
```

### For Mac
```bash
brew install git curl wget nano tmux htop jq make gcc autoconf automake pkg-config openssl leveldb lz4 coreutils
```

---

## 2️⃣ Install Rust, Node.js & Yarn

### For WSL / VPS
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustc --version
```
(Press Enter to proceed with Rust installation)

```bash
sudo apt-get update && curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash - && \
sudo apt-get install -y nodejs && node -v && npm -v && \
sudo npm install -g yarn && yarn -v
```

### For Mac
```bash
brew install curl node yarn rust
```

---

## 3️⃣ Install Solana CLI

### For WSL / VPS
```bash
curl --proto '=https' --tlsv1.2 -sSfL https://solana-install.solana.workers.dev | bash
source $HOME/.bashrc
```
If `solana` not found:
```bash
echo 'export PATH="/root/.local/share/solana/install/active_release/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### For Mac
```bash
sh -c "$(curl -sSfL https://solana-install.solana.workers.dev)"
source $HOME/.bash_profile
```

### For VPS Only (If Solana not found after install)
```bash
reboot
```

---

## 4️⃣ Configure RPC for Eclipse
```bash
solana config set --url https://mainnetbeta-rpc.eclipse.xyz/
```

---

## 5️⃣ Wallet Setup (Solana Keypair)
```bash
solana-keygen new
```
(Press ENTER and save the passphrase)

---

## 6️⃣ Export Private Key from id.json
```bash
cat ~/.config/solana/id.json
```
Copy the output (a list of numbers) and import it into **Backpack Wallet** under **Private Key**.
Ensure wallet has **0.0005+ ETH on Eclipse** to activate mining.

---

## 7️⃣ Install Bitz CLI
```bash
cargo install bitz
```

### For VPS Only
```bash
apt install screen -y
screen -S bitz
```

---

## 8️⃣ Start Miner

### Option A (default)
```bash
bitz collect
```

### Option B (use multiple cores)
```bash
bitz collect --cores 4
```

### To Check CPU Cores (Windows Command Prompt or PowerShell)
![image](https://github.com/user-attachments/assets/a262b33e-2921-4af2-b544-c5b6945caeb8)

```cmd
wmic cpu get NumberOfCores
```

### VPS: Run miner continuously
```bash
CTRL + A + D
```

### To return to the screen
```bash
screen -r bitz
```

---

## ⛏ Claim Mined Tokens
```bash
bitz claim
```

---

## 🧾 Check Wallet Status
```bash
bitz account
```

---

## 🔁 Daily Restart Command (Windows/Mac)
```bash
bitz collect
```

---

## 🗑 Delete Node File
```bash
rm -rf ~/.config/solana
```

---

## ❗ If You Face Core Dumped Error
![image](https://github.com/user-attachments/assets/105d744e-8356-4688-8dd6-823cc5dbb2d0)

```bash
RUST_BACKTRACE=1 ./bitz
```
```bash
solana config get
```
```bash
sh -c "$(curl -sSfL https://release.solana.com/stable/install)"
```
```bash
cargo install bitz --force
```

- **For VPS**: Open screen and re-run miner
- **For Local PC**: Run `bitz collect` again

---

### ✅ You're now mining $BITZ on Eclipse Network!

