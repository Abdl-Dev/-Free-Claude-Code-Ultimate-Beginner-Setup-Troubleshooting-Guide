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

## ⚡ First-Time Installation Guide (Start Here!)

### 🎯 Before You Start

This guide walks you through installing free-claude-code **exactly as documented in [Alishahryar1/free-claude-code](https://github.com/Alishahryar1/free-claude-code)**, with **solutions for common issues at each step**.

When you encounter a problem, look for the **⚠️ Common Issues** section under that step. You'll find the exact fix to get moving again.

**Time Required:** 15-20 minutes  
**Difficulty Level:** Beginner-friendly  
**Prerequisites:** Administrator/sudo access to your computer

---

## 🏗️ Step 1: Install System Dependencies (Git, Python, Node.js)

Choose your operating system and follow the exact commands.

### 🪟 Windows Installation

**Step 1.1:** Right-click PowerShell and select **"Run as Administrator"**

**Step 1.2:** Copy and paste each command separately, waiting for completion:

```powershell
winget install --id Git.Git -e --source winget
```

Wait for this to finish completely (you'll see a checkmark).

```powershell
winget install --id Python.Python.3.11 -e --source winget
```

Wait for this to finish.

```powershell
winget install --id OpenJS.NodeJS.LTS -e --source winget
```

Wait for this to finish.

**Step 1.3:** **CRITICAL: Close PowerShell completely** (close the window). Don't just minimize it—fully close it.

**Step 1.4:** Open a **NEW** PowerShell window as Administrator and verify everything installed:

```powershell
node --version
npm --version
python --version
git --version
```

You should see version numbers like:
```
v18.16.0
9.8.1
Python 3.11.4
git version 2.40.0
```

✅ **If all show versions**, proceed to **Step 2**. If any failed, see issues below.

#### ⚠️ Common Issues in Step 1 (Windows)

##### ❌ Issue 1.1: `winget install` command not found or doesn't exist

**Error Message:**
```
winget : The term 'winget' is not recognized as the name of a cmdlet...
```

**Solution:**
Windows Package Manager (winget) might not be installed. Use this alternative:

```powershell
# Install Node.js directly using Chocolatey (if you have it)
choco install nodejs -y

# OR download manually from https://nodejs.org/
# Then run the installer and restart PowerShell
```

If you don't have Chocolatey, download Node.js manually from [nodejs.org](https://nodejs.org), run the installer, restart your computer, and continue.

---

##### ❌ Issue 1.2: One or more commands fail with "access denied"

**Error Message:**
```
Access is denied. You must have admin rights to run this command.
```

**Solution:**
Make sure PowerShell is running **as Administrator**. 

1. Close PowerShell
2. Right-click PowerShell application
3. Click **"Run as Administrator"**
4. Re-run the winget commands

---

##### ❌ Issue 1.3: Version commands show "command not found" after restarting PowerShell

**Error Message:**
```
node : The term 'node' is not recognized as the name of a cmdlet...
```

**Solution:**
The installation succeeded, but PowerShell hasn't refreshed the environment variables. Try:

```powershell
# Force refresh environment variables for this session
$env:Path += ";C:\Program Files\nodejs"

# Verify
node --version
```

If this doesn't work, **restart your computer completely**. Windows sometimes needs a full reboot to register new programs.

---

##### ❌ Issue 1.4: Python installs but `python --version` shows "not recognized"

**Error Message:**
```
python : The term 'python' is not recognized...
```

**Solution:**
Try using `python3` instead:

```powershell
python3 --version
```

If that works, remember to use `python3` instead of `python` in future commands.

If `python3` also fails, reinstall Python and **check the box "Add Python to PATH"** during installation.

---

### 🍏 macOS Installation

**Step 1.1:** Open Terminal (press Cmd + Space, type "Terminal", press Enter)

**Step 1.2:** Copy and paste this command:

```bash
brew install git python@3.11 node
```

If you don't have Homebrew, install it first:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then run the brew install command above.

**Step 1.3:** Verify installation:

```bash
node --version
npm --version
python3 --version
git --version
```

You should see version numbers.

✅ **If all show versions**, proceed to **Step 2**. If any failed, see issues below.

#### ⚠️ Common Issues in Step 1 (macOS)

##### ❌ Issue 1.1: `brew` command not found

**Error Message:**
```
zsh: command not found: brew
```

**Solution:**
Install Homebrew first:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then run:

```bash
brew install git python@3.11 node
```

---

##### ❌ Issue 1.2: Node.js installed but `node --version` still fails

**Error Message:**
```
zsh: command not found: node
```

**Solution:**
Homebrew installed Node.js, but your Terminal session hasn't reloaded. Try:

```bash
# Reload your shell configuration
source ~/.zprofile

# Then verify
node --version
```

---

##### ❌ Issue 1.3: Python installation conflicts or permission errors

**Error Message:**
```
Error: Could not symlink bin/python3
Target /usr/local/bin/python3 already exists
```

**Solution:**

```bash
# Unlink the conflicting version
brew unlink python@3.11

# Reinstall
brew install python@3.11

# Link it
brew link python@3.11 --force
```

---

### 🐧 Linux Installation (Ubuntu/Debian)

**Step 1.1:** Open Terminal

**Step 1.2:** Copy and paste these commands one by one:

```bash
sudo apt update && sudo apt upgrade -y
```

```bash
sudo apt install -y git python3 python3-pip curl
```

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash - && sudo apt install -y nodejs
```

**Step 1.3:** Verify installation:

```bash
node --version
npm --version
python3 --version
git --version
```

You should see version numbers.

✅ **If all show versions**, proceed to **Step 2**. If any failed, see issues below.

#### ⚠️ Common Issues in Step 1 (Linux)

##### ❌ Issue 1.1: `sudo apt update` fails with "Unable to locate package"

**Error Message:**
```
E: Unable to locate package nodejs
Reading package lists... Done
```

**Solution:**
This means the NodeSource repository wasn't added properly. Try:

```bash
# Remove the old node if it exists
sudo apt remove -y nodejs npm

# Add the NodeSource repository manually
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -

# Install fresh
sudo apt install -y nodejs
```

---

##### ❌ Issue 1.2: Permission denied errors with `sudo`

**Error Message:**
```
sudo: must be run from a terminal
```

**Solution:**
Make sure you're running commands in an actual Terminal window, not a script. Copy-paste each command individually.

---

##### ❌ Issue 1.3: Python or Node.js version conflicts

**Error Message:**
```
The following packages will be REMOVED: nodejs-old
```

**Solution:**
Let Ubuntu/Debian remove old versions automatically:

```bash
# Allow automatic removal of conflicting packages
sudo apt install -y --auto-remove nodejs
```

---

---

## 🛠️ Step 2: Clone the Alishahryar1 Repository

Now you'll get the actual free-claude-code project from GitHub.

### All Platforms:

**Step 2.1:** Choose where you want to store the project (e.g., your Documents folder)

**Step 2.2:** Open Terminal/PowerShell in that folder

**Step 2.3:** Clone the official repository:

```bash
git clone https://github.com/Alishahryar1/free-claude-code.git
cd free-claude-code
```

You'll see output like:
```
Cloning into 'free-claude-code'...
remote: Enumerating objects: 150, done.
...
Unpacking objects: 100%, done.
```

**Step 2.4:** Verify the folder structure:

```bash
ls -la
```

You should see files like `README.md`, `package.json`, `.env.example`, etc.

✅ **If you see the project files**, proceed to **Step 3**.

#### ⚠️ Common Issues in Step 2

##### ❌ Issue 2.1: `git clone` command not found

**Error Message:**
```
git : The term 'git' is not recognized...
```

**Solution:**
Git didn't install properly in Step 1. Go back to Step 1 and reinstall Git.

---

##### ❌ Issue 2.2: "fatal: not a git repository"

**Error Message:**
```
fatal: not a git repository (or any of the parent directories): .git
```

**Solution:**
You're trying to run git commands outside the cloned folder. Make sure you've run:

```bash
cd free-claude-code
```

before any git commands.

---

##### ❌ Issue 2.3: Clone fails with "Connection refused"

**Error Message:**
```
fatal: unable to access 'https://github.com/...': Could not resolve host: github.com
```

**Solution:**
Your internet connection isn't working or GitHub is blocked. Try:

```bash
# Test your connection
ping github.com

# If ping doesn't work, check your internet connection
# If ping works but git still fails, try using SSH instead:
git clone git@github.com:Alishahryar1/free-claude-code.git
cd free-claude-code
```

---

---

## 📦 Step 3: Install Project Dependencies

Now you'll install all the npm packages that free-claude-code needs.

### All Platforms:

**Step 3.1:** Make sure you're in the project folder:

```bash
cd free-claude-code
```

**Step 3.2:** Install dependencies using npm:

```bash
npm install
```

This will take 2-5 minutes. You'll see progress output:
```
added 156 packages in 45s
```

**Step 3.3:** Verify installation:

```bash
npm list
```

You should see a tree of installed packages starting with `free-claude-code` at the top.

✅ **If you see the package tree**, proceed to **Step 4**.

#### ⚠️ Common Issues in Step 3

##### ❌ Issue 3.1: `npm install` fails with "ERR! code ERESOLVE"

**Error Message:**
```
npm ERR! code ERESOLVE
npm ERR! ERESOLVE unable to resolve dependency tree
npm ERR! Found: node@18.0.0
npm ERR! Could not find a version that matches
```

**Solution:**
This means npm is being strict about package compatibility. Force it to ignore conflicts:

```bash
npm install --legacy-peer-deps
```

If that still fails, clear the npm cache and try again:

```bash
npm cache clean --force
npm install --legacy-peer-deps
```

---

##### ❌ Issue 3.2: `npm install` fails with "EACCES: permission denied"

**Error Message:**
```
npm ERR! code EACCES
npm ERR! syscall access
npm ERR! path /usr/local/lib/node_modules
npm ERR! errno -13
npm ERR! Error: EACCES: permission denied
```

**Solution (Linux/macOS only):**

```bash
# Give yourself permission to npm's global directory
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'

# Add npm-global to your PATH
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

# Now try npm install again
npm install
```

---

##### ❌ Issue 3.3: `npm install` fails with "npm: command not found"

**Error Message:**
```
npm: command not found
```

**Solution:**
npm didn't install with Node.js in Step 1. Go back to Step 1 and verify `npm --version` works in a fresh PowerShell/Terminal window.

---

##### ❌ Issue 3.4: Installation seems stuck or takes too long

**What's happening:**
npm is downloading large packages. This is normal and can take 5-10 minutes on slow internet.

**Solution:**
1. Don't interrupt it (don't press Ctrl+C)
2. Wait for it to finish
3. If it's been more than 15 minutes, press Ctrl+C and try:

```bash
npm install --verbose
```

This shows what npm is doing so you can see if it's actually working.

---

---

## 🔧 Step 4: Configure Environment Variables

Create the `.env` file that tells free-claude-code how to connect to the Claude API.

### All Platforms:

**Step 4.1:** In the `free-claude-code` folder, check if `.env.example` exists:

```bash
ls -la | grep env
```

You should see `.env.example` listed.

**Step 4.2:** Copy the example to create your actual `.env` file:

```bash
cp .env.example .env
```

**Step 4.3:** Open the `.env` file in your text editor (VS Code, Notepad++, etc):

```bash
# On Windows (use Notepad)
notepad .env

# On macOS (use TextEdit)
open -e .env

# On Linux (use nano)
nano .env
```

**Step 4.4:** You'll see something like:

```ini
# Example configuration
ANTHROPIC_API_KEY=""
ANTHROPIC_BASE_URL="https://api.anthropic.com"
PORT=8082
MODEL="claude-3-5-sonnet-20241022"
```

**Step 4.5:** Add your API key. If you're using free-claude-code to proxy requests, add:

```ini
# For OpenRouter (recommended free option)
OPENROUTER_API_KEY="sk-or-v1-your-key-here"
MODEL="openrouter/anthropic/claude-3.5-sonnet"

# OR for using a local LLM (completely free)
LM_STUDIO_BASE_URL="http://localhost:1234/v1"
MODEL="lm_studio/your-model-name"

# OR for NVIDIA NIM (if you have it running)
ANTHROPIC_BASE_URL="http://localhost:8000"
ANTHROPIC_AUTH_TOKEN="anything"
```

**Step 4.6:** Save the file (Ctrl+S or Cmd+S)

✅ **If `.env` is created and filled**, proceed to **Step 5**.

#### ⚠️ Common Issues in Step 4

##### ❌ Issue 4.1: `.env.example` file doesn't exist

**Error Message:**
```
ls: No such file or directory
```

**Solution:**
The repository structure might be different. Create the `.env` file manually:

```bash
# Create new .env file
echo "" > .env

# Open it and add configuration
nano .env
```

Then paste this template:

```ini
OPENROUTER_API_KEY="sk-or-v1-your-key-here"
MODEL="openrouter/anthropic/claude-3.5-sonnet"
PORT=8082
```

---

##### ❌ Issue 4.2: Can't open `.env` file in text editor

**Error Message:**
```
Permission denied
# or
File is locked
```

**Solution:**
Make sure you have write permissions:

```bash
# Change file permissions
chmod 644 .env

# Try opening again
nano .env
```

---

##### ❌ Issue 4.3: Don't know which API key to use

**Solution:**
Choose one based on what you have:

1. **If you have OpenRouter account** (easiest for beginners):
   - Get key from [openrouter.ai](https://openrouter.ai)
   - Add to `.env`:
   ```ini
   OPENROUTER_API_KEY="sk-or-v1-..."
   MODEL="openrouter/anthropic/claude-3.5-sonnet"
   ```

2. **If you want completely free (offline)**:
   - Download [LM Studio](https://lmstudio.ai/)
   - Download a model in LM Studio
   - Start server on port 1234
   - Add to `.env`:
   ```ini
   LM_STUDIO_BASE_URL="http://localhost:1234/v1"
   MODEL="lm_studio/your-model-name"
   ```

3. **If you have Anthropic API key**:
   - Get from [console.anthropic.com](https://console.anthropic.com)
   - Add to `.env`:
   ```ini
   ANTHROPIC_API_KEY="sk-ant-..."
   MODEL="claude-3-5-sonnet-20241022"
   ```

---

---

## 🚀 Step 5: Start the Local Proxy Server

This creates a local Claude Code proxy that runs on your computer.

### All Platforms:

**Step 5.1:** Make sure you're in the project folder:

```bash
cd free-claude-code
```

**Step 5.2:** Start the server:

```bash
npm run server
```

Or if that doesn't work, try:

```bash
node server.js
```

**Step 5.3:** You should see output like:

```
Server running on http://localhost:8082
Listening for requests...
```

✅ **Leave this terminal window open** (the server must keep running in the background)

#### ⚠️ Common Issues in Step 5

##### ❌ Issue 5.1: `npm run server` command not found

**Error Message:**
```
npm ERR! missing script: server
```

**Solution:**
The project doesn't have a "server" script. Check what scripts are available:

```bash
npm run
```

This shows all available scripts. Look for something like `start`, `dev`, or `main`. Run:

```bash
npm run start
# or
npm run dev
# or
node index.js
```

---

##### ❌ Issue 5.2: Server fails to start with port already in use

**Error Message:**
```
Error: listen EADDRINUSE :::8082
```

**Solution:**
Something else is using port 8082. Either:

**Option A:** Stop the other program
- Check if you have another free-claude-code running
- Check if another application is using port 8082

**Option B:** Change the port in `.env`:

```ini
PORT=8083
# Then start again
npm run server
```

You'll need to remember port 8083 for Step 6.

---

##### ❌ Issue 5.3: "ANTHROPIC_API_KEY is not set" error

**Error Message:**
```
Error: ANTHROPIC_API_KEY is not set in .env
```

**Solution:**
You didn't fill in the `.env` file correctly. Go back to Step 4 and make sure:
1. The `.env` file has your API key
2. The format is correct: `KEY="value"` with no extra spaces
3. Save the file

Then restart the server:

```bash
npm run server
```

---

##### ❌ Issue 5.4: Server crashes immediately with error

**Error Message:**
```
Error: ENOENT: no such file or directory, open 'config.json'
```

**Solution:**
Some required files are missing. Try:

```bash
# Reinstall dependencies
npm install --legacy-peer-deps

# Then start server again
npm run server
```

If it still fails, check the original repository's README for setup instructions specific to your version.

---

---

## 💻 Step 6: Connect with the Terminal Client (or VS Code)

Now you'll interact with Claude through the proxy.

### Option A: Terminal Client (All Platforms)

**Step 6.1:** Open a **SECOND** terminal window (keep the server running in the first)

**Step 6.2:** Go to the project folder:

```bash
cd free-claude-code
```

**Step 6.3:** Run the client:

```bash
npm run client
```

Or if that doesn't work:

```bash
node client.js
```

**Step 6.4:** You should see a prompt like:

```
Claude Code CLI
> Type your message here:
```

**Step 6.5:** Type a message and press Enter:

```
> Hello, what is 2 + 2?
```

You should get a response from Claude.

✅ **If you get a response, you're done!**

#### ⚠️ Common Issues in Step 6

##### ❌ Issue 6.1: Client fails to connect to server

**Error Message:**
```
Error: connect ECONNREFUSED 127.0.0.1:8082
```

**Solution:**
The server isn't running or it crashed. Check:

1. Look at the first terminal window (where you started the server)
2. Does it still show "Server running"?
3. If not, the server crashed. Check the error and fix it (see Step 5 issues)
4. Start the server again: `npm run server`

---

##### ❌ Issue 6.2: "Cannot find module" error

**Error Message:**
```
Error: Cannot find module 'express'
```

**Solution:**
Dependencies weren't installed properly. In the second terminal, run:

```bash
npm install --legacy-peer-deps
```

Then try the client again:

```bash
npm run client
```

---

##### ❌ Issue 6.3: Response says "Unauthorized" or "API key invalid"

**Error Message:**
```
Error: Unauthorized - API key is invalid or expired
```

**Solution:**
Your API key in `.env` is wrong or expired. Check:

1. Go back to Step 4 and verify the API key
2. Make sure it's correct and hasn't expired
3. Save the `.env` file
4. Restart the server:
   ```bash
   # Stop server (press Ctrl+C in the server terminal)
   # Start again
   npm run server
   ```
5. Try the client again in the second terminal

---

### Option B: VS Code Integration

**Step 6.1:** Open VS Code

**Step 6.2:** Go to Settings (Ctrl+, or Cmd+,)

**Step 6.3:** Search for `ANTHROPIC_BASE_URL`

**Step 6.4:** Click "Edit in settings.json" and add:

```json
"claude.apiBaseUrl": "http://localhost:8082",
"claude.apiToken": "any-token-here"
```

**Step 6.5:** Reload VS Code (Ctrl+R)

**Step 6.6:** Open the Claude Code extension

✅ It should now connect to your local proxy instead of Anthropic's servers.

#### ⚠️ Common Issues with VS Code

##### ❌ Issue 6B.1: Extension still tries to connect to official Anthropic API

**Solution:**
1. Clear VS Code cache: Ctrl+Shift+P → "Developer: Reload Window"
2. Check that settings.json was saved correctly
3. Make sure the server is running (`npm run server`)
4. Verify the base URL matches your server port (default 8082)

---

---

## ✅ Installation Complete!

You now have:
- ✅ All system dependencies installed (Node.js, Python, Git)
- ✅ free-claude-code repository cloned
- ✅ All npm packages installed
- ✅ `.env` file configured with API key
- ✅ Local proxy server running
- ✅ Client connected and working

### What's Next?

1. **Keep the server running** while you use the client
2. **Experiment with prompts** - try different questions
3. **Check the original README** at [Alishahryar1/free-claude-code](https://github.com/Alishahryar1/free-claude-code) for advanced features

---

## ❓ Still Stuck?

**Before asking for help, gather this information:**

```bash
# In a terminal, run these and save the output:
node --version
npm --version
python3 --version
git --version

# Check if server can start:
cd free-claude-code
npm run server

# Take a screenshot of the error message
```

**Then open a GitHub Issue** in this repository with:
- Your OS (Windows 10/11, macOS version, Ubuntu version)
- The command you ran
- The full error message (with screenshots)
- The outputs from the version commands above

---

## 📄 License

This repository is licensed under the **MIT License** — feel free to fork, modify, and share.

## 🙏 Contributing

Found a fix for a new error? Have a better explanation? **Pull requests are welcome!** Help us make this guide even more comprehensive.

---

**Last Updated:** June 2026  
**Maintained by:** Abdl-Dev  
**Status:** Active & Community-Supported  
**Target Audience:** First-time installers, Windows users, Beginners  
**Based on:** [Alishahryar1/free-claude-code](https://github.com/Alishahryar1/free-claude-code)
