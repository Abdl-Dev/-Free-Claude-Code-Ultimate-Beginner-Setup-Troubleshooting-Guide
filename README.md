# 🚀 Free Claude Code — Universal Setup & Troubleshooting Knowledge Base (Guide)

This repository serves as a community-driven, step-by-step master handbook dedicated to debugging and setting up the [free-claude-code](https://github.com) proxy wrapper.

When configuring Claude Code to route through alternative providers like NVIDIA NIM, OpenRouter, or LM Studio, users frequently hit severe platform-specific walls. This guide eliminates those hurdles by providing:

* **Zero-to-Hero Dependency Code:** One-click scripts to install Git, Python, and Node.js across Windows (`winget`), macOS (`brew`), and Linux (`apt`).
* **Binary Error Patches:** Immediate fixes for the dreaded Windows `claude.exe is not a valid application` bug and broken 0-byte global NPM cache folders.
* **Shell Syntax Support:** Drop-in commands to resolve PowerShell parsing errors, unexpected token blocks (`fre$env:APPDATA`), and path injection failures.
* **Advanced Integration Blueprints:** Clean configuration matrices to bridge the proxy seamlessly into VS Code Settings and local offline LLM endpoints.


This repository contains a step-by-step installation pipeline and troubleshooting log for the popular [Alishahryar1/free-claude-code](https://github.com) proxy bridge. Use this repository to configure the tool without running into native binary errors, syntax bugs, or broken environment mappings.

### 🏗️ Step 1: Core System Dependencies

Choose your operating system below to copy-paste the exact commands needed to install Git, Python, and Node.js automatically:

#### 🪟 Windows (Run in PowerShell as Administrator)
Windows uses the official Windows Package Manager (winget) to install applications via terminal automation:

```powershell
# Install Git, Python 3.11, and Node.js Long Term Support (LTS)
winget install --id Git.Git -e --source winget
winget install --id Python.Python.3.11 -e --source winget
winget install --id OpenJS.NodeJS.LTS -e --source winget
```

*CRITICAL: Restart your terminal window completely after these finish running!*

#### 🍏 macOS (Run in Terminal)
Mac uses the Homebrew package manager:

```bash
# Install Git, Python, and Node.js
brew install git python@3.11 node

# Verify the environment paths match up
node -v && python3 --version
```

#### 🐧 Linux (Ubuntu / Debian - Run in Terminal)

```bash
# Update local package catalog
sudo apt update && sudo apt upgrade -y

# Install Git, Python 3, pip, and curl toolchains
sudo apt install -y git python3 python3-pip curl

# Download and provision the Node.js NodeSource LTS ecosystem
curl -fsSL https://nodesource.com | sudo -E bash -
sudo apt install -y nodejs
```

---

### 🛠️ Step 2: One-Click Script Automation

Instead of manually configuring terminal blocks, you can leverage the project's native automation script to handle internal file routing dynamically.

#### Windows PowerShell:
```powershell
irm "https://github.com/blob/main/scripts/install.ps1?raw=1" | iex
```

#### macOS / Linux Terminal:
```bash
curl -fsSL "https://github.com/blob/main/scripts/install.sh?raw=1" | sh
```

---

### 📦 Step 3: Local Proxy Server Orchestration

Open a terminal window inside your project workspace and kick off the server process. Leave this terminal window running in the background to act as your model engine:

```bash
fcc-server
```

---

### 💻 Step 4: Connecting the Terminal Client

Open a separate, second terminal window inside your active coding workspace folder. Run the customized launcher command to engage the model:

```bash
fcc-claude
```

---

### ⚙️ Step 5: Advanced Model Switching (Optional)

You don't have to stick to NVIDIA NIM. Open your project's local `.env` file to easily configure OpenRouter or completely offline local models:

#### Option A: OpenRouter Config
```ini
OPENROUTER_API_KEY="sk-or-v1-your-key..."
MODEL="openrouter/google/gemini-2.5-pro"
```

#### Option B: Local LM Studio (100% Free & Offline)
Launch LM Studio, download your favorite model, and start the Local Server on port `1234`. Update your `.env` like this:

```ini
LM_STUDIO_BASE_URL="http://localhost:1234/v1"
MODEL="lm_studio/your-local-model-name"
```

---

### 🎨 Step 6: VS Code Extension Setup

If you prefer using the official Claude Code VS Code extension instead of the terminal, you can still force it to route through your free local proxy:

1. Open VS Code Settings (`Ctrl + ,` or `Cmd + ,`).
2. Search for `claude-code.environmentVariables`.
3. Click **Edit in settings.json** and paste this block:

```json
"claudeCode.environmentVariables": [
  { "name": "ANTHROPIC_BASE_URL", "value": "http://localhost:8082" },
  { "name": "ANTHROPIC_AUTH_TOKEN", "value": "freecc" },
  { "name": "CLAUDE_CODE_ENABLE_GATEWAY_MODEL_DISCOVERY", "value": "1" },
  { "name": "CLAUDE_CODE_AUTO_COMPACT_WINDOW", "value": "190000" }
]
```

*Reload VS Code. If it asks you to log in via the official Anthropic page, do it once; your live model traffic will still bypass to your local proxy.*

---

### 🚨 Troubleshooting Hall of Fame

#### ❌ Issue 1: `fcc-claude` Crashes or Fails to Run on Windows
* **The Cause:** The automatic installer paths are missing from your current active PowerShell console, or Windows is failing to locate the core npm target directory globally.
* **The Fix:** Run these commands in your second window right before executing `fcc-claude` to force-register the paths and inject your dummy proxy validation tokens:

```powershell
env:Path += ";env:APPDATA\npm"
\$env:ANTHROPIC_BASE_URL="http://localhost:8082"
\$env:ANTHROPIC_AUTH_TOKEN="freecc"
```

#### ❌ Issue 2: Unexpected Token Error `fre$env:APPDATA...`
* **The Cause:** Unclosed double-quotes (`"`) combined with path syntax pasting inside a live PowerShell session.
* **The Solution:** Wipe your active shell space by closing the tab. Relaunch a clean terminal and execute the path injection sequences safely.

#### ❌ Issue 3: `claude.exe` failed to run: Not a valid application
* **The Cause:** System locked tracking parameters during global NPM mapping, dumping an empty execution container.
* **The Solution:** Wipe out old directory stubs via Command Prompt (`cmd.exe`) to execute a forced global cleanup:

```cmd
npm uninstall -g @anthropic-ai/claude-code
rmdir /s /q "%USERPROFILE%\.claude" 2>nul
rmdir /s /q "%USERPROFILE%\.cache\claude" 2>nul
npm install -g @anthropic-ai/claude-code
```
## 🤝 Connect & Support

This troubleshooting guide is maintained by **Abdul Rahman**. If you get stuck on an error or have any questions, feel free to reach out:

<a href="https://wa.me" target="_blank">
  <img src="https://shields.io" alt="WhatsApp">
</a>

<a href="https://github.com" target="_blank">
  <img src="https://shields.io" alt="GitHub">
</a>

