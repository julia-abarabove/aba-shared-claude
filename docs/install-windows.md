# Install on Windows

About 20 minutes. You'll type a few lines into **PowerShell** (a text window
for typing commands). To open it: press the Windows key, type `PowerShell`,
press Enter.

Before you start, have these ready:
- Your Claude Team invite accepted (check your abarabove.com email).
- A GitHub account that Julia has added to the team kit.
- Access to your 1Password item **"Asana PAT -- Claude on behalf of <your name>"**.

---

## 1. Install the helper programs

Paste this into PowerShell and press Enter. Say **Yes** to any pop-ups.

```powershell
winget install --id Git.Git -e; winget install --id OpenJS.NodeJS.LTS -e; winget install --id GitHub.cli -e
```

Success: each line ends with "Successfully installed" (or "already
installed").

**Then close PowerShell and open a new one.** The new programs only show up in
a fresh window.

## 2. Install Claude Code

```powershell
irm https://claude.ai/install.ps1 | iex
```

Success: it says Claude Code was installed. Close PowerShell and open a new
one again.

## 3. Sign in to GitHub

```powershell
gh auth login
```

Pick these answers with the arrow keys and Enter: **GitHub.com**, **HTTPS**,
**Yes** (authenticate Git), **Login with a web browser**. Copy the 8-character
code it shows, press Enter, paste the code in the browser, approve.

Success: "Logged in as <your GitHub name>".

## 4. Download the team kit

```powershell
cd $HOME\Documents; gh repo clone julia-abarabove/aba-shared-claude
```

Success: a new folder `Documents\aba-shared-claude`.

## 5. Connect Asana

Open 1Password, find **"Asana PAT -- Claude on behalf of <your name>"**, and
copy the token. Then paste this line into PowerShell, **replacing
`PASTE_TOKEN_HERE` with your token** before pressing Enter:

```powershell
claude mcp add asana --scope user -e ASANA_ACCESS_TOKEN=PASTE_TOKEN_HERE -- cmd /c npx -y @roychri/mcp-server-asana
```

Success: "Added stdio MCP server asana".

Never paste the token into the Claude chat itself. It only goes in this one
command.

## 6. Start Claude Code

```powershell
cd $HOME\Documents\aba-shared-claude; claude
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

Open PowerShell and paste:

```powershell
cd $HOME\Documents\aba-shared-claude; git pull; claude
```

That grabs any kit updates Julia has pushed, then starts Claude.
