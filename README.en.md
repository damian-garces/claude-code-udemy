🌐 **Read this in other languages:** [Español](README.md)

# 🚀 Claude Code Course — Log & Projects

Welcome to this repository! Here you will find notes, lessons learned, exercises, and projects built throughout the **Claude Code** course (Anthropic's terminal-based AI coding assistant).

---

## 📁 Repository Structure

As we progress through the course, hands-on exercises and projects will be organized in dedicated subfolders:

```text
repo/
├── README.md             # Main documentation in Spanish
├── README.en.md          # Documentation in English
└── projects/             # Subfolders for course projects
    ├── 01-getting-started/
    ├── 02-automations/
    └── ...
```

---

## 🛠️ Requirements & Environment Setup on WSL

To work smoothly with Claude Code in a Linux (WSL) environment, the following tools should be installed and configured:

### 1. Node.js

Claude Code requires a Node.js runtime (version 18 or higher). Installing it via `nvm` (Node Version Manager) is recommended:

```bash
# 1. Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

# 2. Reload terminal configuration
source ~/.bashrc

# 3. Install and use the LTS release of Node.js
nvm install --lts
nvm use --lts

# 4. Verify installation
node -v
npm -v
```

---

### 2. Claude Code

Claude Code is Anthropic's official CLI tool for AI-assisted coding directly inside your terminal:

```bash
# 1. Install Claude Code globally with npm
npm install -g @anthropic-ai/claude-code

# 2. Launch Claude Code and follow authentication prompts
claude
```

> **Note:** The first time you run `claude`, it will guide you through authenticating with your Anthropic Console account or configuring your API key (`ANTHROPIC_API_KEY`).

---

### 3. Warp Terminal

[Warp](https://www.warp.dev/) is a modern GPU-accelerated terminal with built-in AI, autocompletion, and workflow sharing.

#### Options for WSL:
- **Warp on Windows:** Install Warp on Windows and open a session directly connected to your WSL distribution.
- **Warp for Linux:** If using a graphical desktop setup in Linux/WSL, install the `.deb` package:

```bash
# Download and install the .deb package for Debian/Ubuntu distributions
sudo apt update && sudo apt install -y wget
wget -O warp-terminal.deb https://releases.warp.dev/stable/v0.2024.02.20.08.02.stable_02/warp-terminal_0.2024.02.20.08.02.stable.02_amd64.deb
sudo apt install ./warp-terminal.deb
rm warp-terminal.deb
```

---

### 4. Git & SSH Connection

Configuring Git and establishing secure SSH authentication with GitHub/GitLab:

#### Step 1: Configure Git identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

#### Step 2: Generate an SSH key pair (Ed25519 algorithm)
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```
*(Press `Enter` to accept default path `~/.ssh/id_ed25519` and set an optional passphrase).*

#### Step 3: Start the SSH agent and add your private key
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

#### Step 4: Copy the public key
```bash
cat ~/.ssh/id_ed25519.pub
```
Copy the full output string.

#### Step 5: Add the SSH key to GitHub
1. Navigate to **GitHub > Settings > SSH and GPG keys**.
2. Click **New SSH key**.
3. Enter a descriptive title (e.g., `WSL-Ubuntu`) and paste the public key.
4. Click **Add SSH key**.

#### Step 6: Test the connection
```bash
ssh -T git@github.com
```
You should see:
`Hi <username>! You've successfully authenticated, but GitHub does not provide shell access.`

---

## ⚙️ Personal Settings

This section documents custom configurations, extensions, skills, and workflow adjustments for Claude Code.

### 1. Caveman Skill

**Caveman** is a skill for Claude Code and AI assistants designed to enforce ultra-concise, direct-to-the-point answers. This significantly reduces token consumption and speeds up response times.

#### Installation

Install the skill directly using `npx`:

```bash
npx skills add JuliusBrussee/caveman
```

#### Usage

Once installed, Claude will provide concise, code-first answers without unnecessary fluff. You can also configure or invoke it according to the skill's options.

---

## 📌 Next Steps

- [ ] Complete WSL environment setup.
- [ ] Explore initial Claude Code workflows and features.
- [ ] Add projects and practical exercises in subdirectories.
