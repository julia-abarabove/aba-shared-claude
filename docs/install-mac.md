# Install on Mac

About 20 minutes. You'll type a few lines into **Terminal** (a text window for
typing commands). To open it: press Cmd + Space, type `Terminal`, press Enter.

Before you start, have these ready:
- Your Claude Team invite accepted (check your abarabove.com email).
- A GitHub account that Julia has added to the team kit.
- Access to your 1Password item **"Asana PAT -- Claude on behalf of <your name>"**.

---

## 1. Install the helper programs

**a. Git.** Paste this into Terminal and press Enter:

```bash
git --version
```

If it shows a version number, you're set. If a pop-up offers to install
"command line developer tools", click **Install** and wait for it to finish
(5 to 10 minutes).

**b. Node.js.** Go to https://nodejs.org, download the **LTS** version for
Mac, open the downloaded file, and click through the installer.

**c. GitHub CLI.** Go to https://cli.github.com, click **Download for Mac**,
open the downloaded file, and click through the installer.

**Then quit Terminal (Cmd + Q) and open it again.**

## 2. Install Claude Code

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Success: it says Claude Code was installed. Quit and reopen Terminal.

## 3. Sign in to GitHub

```bash
gh auth login
```

Pick these answers with the arrow keys and Enter: **GitHub.com**, **HTTPS**,
**Yes** (authenticate Git), **Login with a web browser**. Copy the 8-character
code it shows, press Enter, paste the code in the browser, approve.

Success: "Logged in as <your GitHub name>".

## 4. Download the team kit

```bash
cd ~/Documents && gh repo clone julia-abarabove/aba-shared-claude
```

Success: a new folder `Documents/aba-shared-claude`.

## 5. Connect Asana

Open 1Password, find **"Asana PAT -- Claude on behalf of <your name>"**, and
copy the token. Then paste this line into Terminal, **replacing
`PASTE_TOKEN_HERE` with your token** before pressing Enter:

```bash
claude mcp add asana --scope user -e ASANA_ACCESS_TOKEN=PASTE_TOKEN_HERE -- npx -y @roychri/mcp-server-asana
```

Success: "Added stdio MCP server asana".

Never paste the token into the Claude chat itself. It only goes in this one
command.

## 6. Start Claude Code

```bash
cd ~/Documents/aba-shared-claude && claude
```

The first time:
- Choose **Claude account with subscription** and sign in with your
  **@abarabove.com** email (your Team seat).
- When it asks whether you trust this folder, say **Yes**.

## 7. Check it works

Type this to Claude and press Enter:

> What Asana tasks are assigned to me?

Success: Claude lists tasks assigned to "Claude, (on behalf of <your name>)"
(it may be an empty list, that's fine). If it asks permission to use an Asana
tool, say yes.

If it says Asana isn't connected, type `/mcp` and send Julia a screenshot.

---

## Every time after this

Open Terminal and paste:

```bash
cd ~/Documents/aba-shared-claude && git pull && claude
```

That grabs any kit updates Julia has pushed, then starts Claude.
