# 🚀 Free Claude Code — Universal Setup & Troubleshooting Knowledge Base (Guide)

This repository serves as a community-driven, step-by-step master handbook dedicated to debugging and setting up the [free-claude-code](https://github.com/Alishahryar1/free-claude-code.git) proxy with zero frustration across Windows, macOS, and Linux.

When configuring Claude Code to route through alternative providers like NVIDIA NIM, OpenRouter, or LM Studio, users frequently hit severe platform-specific walls. This guide eliminates those hurdles.

## 📋 What You'll Find Here

* **Zero-to-Hero Dependency Code:** One-click scripts to install Git, Python, and Node.js across Windows (`winget`), macOS (`brew`), and Linux (`apt`).
* **Binary Error Patches:** Immediate fixes for the dreaded Windows `claude.exe is not a valid application` bug and broken 0-byte global NPM cache folders.
* **Shell Syntax Support:** Drop-in commands to resolve PowerShell parsing errors, unexpected token blocks (`fre$env:APPDATA`), and path injection failures.
* **Advanced Integration Blueprints:** Clean configuration matrices to bridge the proxy seamlessly into VS Code Settings and local offline LLM endpoints.


This repository contains a step-by-step installation pipeline and troubleshooting log for the popular [Alishahryar1/free-claude-code](https://github.com/Alishahryar1/free-claude-code).

---

## 🏗️ Step 1: Core System Dependencies

Choose your operating system below to copy-paste the exact commands needed to install Git, Python, and Node.js automatically:

### 🪟 Windows (Run in PowerShell as Administrator)
Windows uses the official Windows Package Manager (winget) to install applications via terminal automation:

```powershell
# Install Git, Python 3.11, and Node.js Long Term Support (LTS)
winget install --id Git.Git -e --source winget
winget install --id Python.Python.3.11 -e --source winget
winget install --id OpenJS.NodeJS.LTS -e --source winget
```

*CRITICAL: Restart your terminal window completely after these finish running!*

### 🍏 macOS (Run in Terminal)
Mac uses the Homebrew package manager:

```bash
# Install Git, Python, and Node.js
brew install git python@3.11 node

# Verify the environment paths match up
node -v && python3 --version
```

### 🐧 Linux (Ubuntu / Debian - Run in Terminal)

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

## 🛠️ Step 2: One-Click Script Automation

Instead of manually configuring terminal blocks, you can leverage the project's native automation script to handle internal file routing dynamically.

### Windows PowerShell:
```powershell
irm "https://github.com/Alishahryar1/free-claude-code/blob/main/scripts/install.ps1?raw=1" | iex
```

### macOS / Linux Terminal:
```bash
curl -fsSL "https://github.com/Alishahryar1/free-claude-code/blob/main/scripts/install.sh?raw=1" | sh
```

---

## 📦 Step 3: Local Proxy Server Orchestration

Open a terminal window inside your project workspace and kick off the server process. Leave this terminal window running in the background to act as your model engine:

```bash
fcc-server
```

---

## 💻 Step 4: Connecting the Terminal Client

Open a separate, second terminal window inside your active coding workspace folder. Run the customized launcher command to engage the model:

```bash
fcc-claude
```

---

## ⚙️ Step 5: Advanced Model Switching (Optional)

You don't have to stick to NVIDIA NIM. Open your project's local `.env` file to easily configure OpenRouter or completely offline local models:

### Option A: OpenRouter Config
```ini
OPENROUTER_API_KEY="sk-or-v1-your-key..."
MODEL="openrouter/google/gemini-2.5-pro"
```

### Option B: Local LM Studio (100% Free & Offline)
Launch LM Studio, download your favorite model, and start the Local Server on port `1234`. Update your `.env` like this:

```ini
LM_STUDIO_BASE_URL="http://localhost:1234/v1"
MODEL="lm_studio/your-local-model-name"
```

---

## 🎨 Step 6: VS Code Extension Setup

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

## 🚨 Troubleshooting Hall of Fame

### ❌ Issue 1: `fcc-claude` Crashes or Fails to Run on Windows
* **The Cause:** The automatic installer paths are missing from your current active PowerShell console, or Windows is failing to locate the core npm target directory globally.
* **The Fix:** Run these commands in your second window right before executing `fcc-claude` to force-register the paths and inject your dummy proxy validation tokens:

```powershell
$env:Path += ";$env:APPDATA\npm"
$env:ANTHROPIC_BASE_URL="http://localhost:8082"
$env:ANTHROPIC_AUTH_TOKEN="freecc"
```

### ❌ Issue 2: Unexpected Token Error `fre$env:APPDATA...`
* **The Cause:** Unclosed double-quotes (`"`) combined with path syntax pasting inside a live PowerShell session.
* **The Solution:** Wipe your active shell space by closing the tab. Relaunch a clean terminal and execute the path injection sequences safely.

### ❌ Issue 3: `claude.exe` failed to run: Not a valid application
* **The Cause:** System locked tracking parameters during global NPM mapping, dumping an empty execution container.
* **The Solution:** Wipe out old directory stubs via Command Prompt (`cmd.exe`) to execute a forced global cleanup:

```cmd
npm uninstall -g @anthropic-ai/claude-code
rmdir /s /q "%USERPROFILE%\.claude" 2>nul
rmdir /s /q "%USERPROFILE%\.cache\claude" 2>nul
npm install -g @anthropic-ai/claude-code
```

---

## 🔗 The Triple-Error Chain: Detailed Breakdown & Recovery (Windows Edition)

This section documents the **real-world three-step error sequence** that occurs when setting up free-claude-code on Windows, and the exact commands to resolve each layer.

### 📍 Error Chain Overview

1. **Missing npm Command** — Node.js installed but PowerShell doesn't see it
2. **Execution Policy Restriction** — Windows blocks script execution  
3. **Accidental HTML Parsing** — Wrong script URL downloaded and parsed as code

---

### **🔴 Error #1: Missing npm Command**

#### What Happens
After installing Node.js via `winget`, your PowerShell session does not immediately recognize the new npm executable. The terminal shows:

```
npm : The term 'npm' is not recognized as the name of a cmdlet, function, script file, or operable program.
```

#### Root Cause
The Windows registry has been updated with the new `npm` path, but your **currently active PowerShell window has not refreshed** its environment variables. This is a caching issue, not a broken installation.

#### ✅ Fix: Force PowerShell to Reload Environment Variables

**Step 1:** Refresh the environment variables without rebooting

```powershell
# Method A: Manually append npm to your current session's Path
$env:Path += ";$env:APPDATA\npm"

# Verify npm is now found
npm --version
```

**Step 2:** If that doesn't work, close the PowerShell window entirely and reopen it

```powershell
# Close this window (Ctrl + Shift + Esc or close the tab)
# Reopen a NEW PowerShell window as Administrator
# npm should now work immediately
npm --version
```

---

### **🔴 Error #2: Execution Policy Restriction**

#### What Happens
After npm is recognized, you try to run the installation script, but PowerShell rejects it:

```
File cannot be loaded because running scripts is disabled on this system.
```

#### Root Cause
By default, Windows PowerShell blocks execution of local script files (`.ps1`) to prevent malware infections. The security policy is set to `Restricted`.

#### ✅ Fix: Bypass Execution Policy for Current Session Only

**Step 1:** Run this command to allow script execution **only in this PowerShell window**

```powershell
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process -Force
```

**Step 2:** Verify the policy was changed (output will show `Bypass`)

```powershell
Get-ExecutionPolicy
```

**Step 3:** Now paste the full installer command (see Step 4 below)

#### ⚠️ Important Security Note
- `-Scope Process` means this setting **only applies to your current window session**.
- Once you close PowerShell, the security policy reverts to normal.
- This does NOT permanently weaken your system security.
- Do NOT use `-Scope CurrentUser` or `-Scope LocalMachine` unless you fully trust the script.

---

### **🔴 Error #3: Accidental HTML Parsing (GitHub Homepage Downloaded)**

#### What Happens
While trying to bypass the execution policy, you accidentally mistype the installer URL. Instead of pasting the full script path, you type:

```powershell
irm "https://github.com" | iex
```

PowerShell attempts to execute the raw HTML of GitHub's homepage as PowerShell code:

```
Unexpected token '<!DOCTYPE html>' in expression or statement.
Syntax error near '=' ...
... (thousands of cryptic parse errors)
```

#### Root Cause
- The `irm` (Invoke-RestMethod) command downloaded the GitHub homepage HTML
- The `| iex` (Invoke-Expression) command tried to parse HTML as PowerShell syntax
- HTML tags like `<html>`, `<body>`, `<script>` are not valid PowerShell tokens

#### ✅ Fix: Paste the Correct Full Script URL

**Step 1:** Copy the exact full URL from the official repository

```powershell
irm "https://github.com/Alishahryar1/free-claude-code/blob/main/scripts/install.ps1?raw=1" | iex
```

**Step 2:** If you're unsure, visit the URL in your browser first to verify it contains PowerShell code (not HTML)

**Step 3:** After pasting, you should see npm installation progress messages, not syntax errors

---

### 🎯 Complete Recovery Workflow (All Three Errors Fixed)

If you hit all three errors in sequence, here's the exact recovery path:

```powershell
# 1️⃣ FIRST: Refresh environment variables
$env:Path += ";$env:APPDATA\npm"
npm --version

# If npm still not found, close this window and reopen PowerShell as Administrator, then continue

# 2️⃣ SECOND: Bypass execution policy for this session only
Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope Process -Force

# 3️⃣ THIRD: Run the correct installer script (NOT just "https://github.com")
irm "https://github.com/Alishahryar1/free-claude-code/blob/main/scripts/install.ps1?raw=1" | iex

# 4️⃣ FOURTH: Wait for the installation to complete
# You should see: "Successfully installed @anthropic-ai/claude-code"

# 5️⃣ FIFTH: Verify the installation worked
fcc-claude --version
```

---

### 🧠 Why Each Error Happened

| Error | Cause | Why It's Easy to Miss |
|-------|-------|---------------------|
| **Missing npm** | PowerShell caching | Beginners expect `winget` to instantly update all windows |
| **Execution Policy** | Windows security default | Seems like an installation bug, actually a feature |
| **HTML Parsing** | Typo in script URL | Very easy to copy-paste only `https://github.com` instead of the full path |

---

### 📚 Additional Resources

- [Microsoft: PowerShell Execution Policy](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy)
- [free-claude-code Official Repository](https://github.com/Alishahryar1/free-claude-code)
- [Node.js / npm Installation Guide](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm)

---

## ❓ Still Stuck?

If you've followed all these steps and still hit errors:

1. **Check your Node.js version:** `node -v` (should be v18+)
2. **Check your npm version:** `npm --version` (should be v8+)
3. **Clear npm cache:** `npm cache clean --force`
4. **Reinstall fresh:** `npm uninstall -g @anthropic-ai/claude-code && npm install -g @anthropic-ai/claude-code`
5. **Open a GitHub Issue** in this repository with your full error message and OS version

---

## 📄 License

This repository is licensed under the **MIT License** — feel free to fork, modify, and share.

## 🙏 Contributing

Found a fix for a new error? Have a better explanation? **Pull requests are welcome!** Help us make this guide even more comprehensive.

---

**Last Updated:** June 2026  
**Maintained by:** Abdl-Dev  
**Status:** Active & Community-Supported
