# Week 3 – Password Cracking Lab
**Cybersecurity & Ethical Hacking Internship | NetworkWalks Academy**

This report documents the completion of the Week 3 project work for the Cybersecurity & Ethical Hacking internship. The objective of this week's labs was to understand how password cracking works in practice, using both a traditional command-line/GUI security tool (John the Ripper) and a browser-based tool suite built by NetworkWalks, and finally to repeat the exercise with an AI-assisted workflow.

> ⚠️ **Disclaimer:** All password cracking in this report was performed strictly for educational purposes on files provided as part of the internship lab exercises. These techniques must never be used against systems or files without explicit authorization.

---

## 📋 Table of Contents
1. [Module 1 – Password Cracking with John the Ripper (JTR)](#module-1--password-cracking-with-john-the-ripper-jtr)
2. [Module 2 – Password Cracking with NetworkWalks Tools](#module-2--password-cracking-with-networkwalks-tools)
3. [Bonus / Optional – W3-OPTIONAL1: AI – JTR Password Cracking Lab (Hexstrike MCP Edition)](#bonus--optional--w3-optional1-ai--jtr-password-cracking-lab-hexstrike-mcp-edition)
4. [Results Summary](#-results-summary)
5. [Key Takeaways](#-key-takeaways)
6. [Tools & References](#-tools--references)

---

## Module 1 – Password Cracking with John the Ripper (JTR)

**Task:** Crack the password of a protected PDF file (`My Locked PDF1.pdf`) using JTR **John** and JTR **Johnny** (the GUI front end for John the Ripper) on a Windows PC.

### Step 1 – Download John the Ripper
Downloaded the John the Ripper (JTR) package for Windows from the official Openwall site:
🔗 https://www.openwall.com/john/

### Step 2 – Download Johnny (GUI for John the Ripper)
Downloaded the Johnny GUI, version 2.2, from the official wiki page:
🔗 https://openwall.info/wiki/john/johnny

<p align="center"><img src="images/image1.png" width="700"/></p>
<p align="center"><img src="images/image2.png" width="700"/></p>

Installed Johnny and launched it:

<p align="center"><img src="images/image3.png" width="500"/></p>

Opened **Settings** and browsed to point Johnny to the John the Ripper executable:

<p align="center"><img src="images/image4.png" width="500"/></p>

Selected `john.exe`, located inside the `run` folder of the extracted John the Ripper package:

<p align="center"><img src="images/image5.png" width="500"/></p>

### Step 3 – Extract the hash from the locked PDF
Downloaded the encrypted PDF file to the PC, then used the **PDF Hash Extractor** tool to pull the crackable hash out of the file:
🔗 https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php

<p align="center"><img src="images/image6.png" width="700"/></p>

Uploaded the PDF and generated the hash:

<p align="center"><img src="images/image7.png" width="600"/></p>

The hash (starting with `$pdf$...`) was copied, pasted into a plain text file, and saved for use with Johnny.

### Step 4 – Load the hash and run the attack
Opened Johnny and clicked **Open password file** to load the saved hash file:

<p align="center"><img src="images/image8.png" width="600"/></p>

Clicked **Start new attack**:

<p align="center"><img src="images/image9.png" width="600"/></p>

The password was successfully cracked:

<p align="center"><img src="images/image10.png" width="600"/></p>

✅ **Cracked password:** `good-luck` — this password can now be used to open the protected PDF.

### Repeating the attack on additional files
The same workflow (extract hash → load into Johnny → start attack) was repeated on two more protected files to reinforce the process:

<p align="center"><img src="images/image11.png" width="350"/></p>

- **File 2:** cracked password → `Password1`

  <p align="center"><img src="images/image12.png" width="350"/></p>

- **File 3:** cracked password → `1qaz2wsx`

  <p align="center"><img src="images/image13.png" width="450"/></p>

---

## Module 2 – Password Cracking with NetworkWalks Tools

**Task:** Crack the password of the same attached PDF file (`My Locked PDF1.pdf`) using two free, browser-based tools built by NetworkWalks — the **Hash Calculator** and the **Password Cracker** (dictionary attack) — with no software installation required.

### Step 1 – Download the target PDF
Downloaded the encrypted PDF file from the NetworkWalks lab page.

<p align="center"><img src="images/image14.png" width="700"/></p>
<p align="center"><img src="images/image15.png" width="600"/></p>

### Step 2 & 3 – Extract the hash with the Hash Calculator
Opened the NetworkWalks **Hash Calculator** in the browser:
🔗 https://networkwalks.com/hash-calculator/

Uploaded the locked PDF file. The tool parsed the file locally and generated the crackable hash (starting with `$pdf$...`):

<p align="center"><img src="images/image16.png" width="700"/></p>

### Step 4 – Copy the hash
Copied the complete hash value, starting from `$pdf$`, for use in the next step.

### Step 5 & 6 – Run the dictionary attack with the Password Cracker
Opened the NetworkWalks **Password Cracker** (dictionary attack tool):
🔗 https://networkwalks.com/password-cracker/

Pasted the hash and started the attack. The tool worked through its built-in wordlist until it found a match:

<p align="center"><img src="images/image17.png" width="600"/></p>

### Step 7 & 8 – Open the file with the cracked password
✅ **Cracked password:** `Password1`

Opened the originally locked PDF and entered the cracked password to confirm it unlocked successfully:

<p align="center"><img src="images/image18.png" width="600"/></p>

---

## Bonus / Optional – W3-OPTIONAL1: AI – JTR Password Cracking Lab (Hexstrike MCP Edition)

In addition to the two required modules, I completed the **optional AI-assisted lab**, connecting **Claude Desktop** to the **Hexstrike-AI MCP server** on a Kali Linux VM, which exposes security tooling (including John the Ripper) to the AI assistant through the Model Context Protocol (MCP).

**Task:** Crack the password of `networkwalks_flag1.pdf` using JTR John with the help of AI (Hexstrike-AI MCP with Claude Desktop in Kali Linux).

**Lab environment:** Hexstrike-AI MCP server with Claude Desktop on a Kali Linux VM.

### Part A — Setting up the lab environment

### 1. Install Claude Desktop on Kali Linux
Installed the unofficial Claude Desktop build for Linux from the community GitHub repository:
🔗 https://github.com/aaddrick/claude-desktop-debian

```bash
curl -fsSL https://pkg.claude-desktop-debian.dev/KEY.gpg | sudo gpg --dearmor -o /usr/share/keyrings/claude-desktop-unofficial.gpg
echo "deb [signed-by=/usr/share/keyrings/claude-desktop-unofficial.gpg arch=amd64,arm64] https://pkg.claude-desktop-debian.dev stable main" | sudo tee /etc/apt/sources.list.d/claude-desktop-unofficial.list
sudo apt update
sudo apt install claude-desktop-unofficial
```

Launched Claude Desktop with `claude-desktop-unofficial` and signed in:

<p align="center"><img src="images/image19.png" width="650"/></p>
<p align="center"><img src="images/image20.png" width="500"/></p>
<p align="center"><img src="images/image21.png" width="450"/></p>

### 2. Install Hexstrike MCP
Cloned the Hexstrike-AI repository and set it up in a Python virtual environment:
🔗 https://github.com/0x4m4/hexstrike-ai

```bash
git clone https://github.com/0x4m4/hexstrike-ai.git
cd hexstrike-ai
python3 -m venv hexstrike-env
source hexstrike-env/bin/activate
pip3 install -r requirements.txt
python3 hexstrike_server.py
```

<p align="center"><img src="images/image22.png" width="600"/></p>
<p align="center"><img src="images/image23.png" width="650"/></p>

### 3. Connect the MCP server to Claude Desktop
Edited Claude Desktop's developer configuration file to register the Hexstrike MCP server:

<p align="center"><img src="images/image24.png" width="550"/></p>

```json
{
  "mcpServers": {
    "hexstrike-ai": {
      "command": "/home/kali/hexstrike-ai/hexstrike-env/bin/python",
      "args": [
        "/home/kali/hexstrike-ai/hexstrike_mcp.py",
        "--server",
        "http://localhost:8888"
      ]
    }
  }
}
```

Confirmed the MCP server was running and connected:

<p align="center"><img src="images/image25.png" width="500"/></p>
<p align="center"><img src="images/image26.png" width="450"/></p>

### Part B — Lab Practice: Cracking `networkwalks_flag1.pdf` with AI assistance

**Step 1:** Copied the target PDF file (`hash3.networkwalks_flag1.pdf`) to the Desktop of the Kali Linux VM.

**Step 2:** Opened Claude Desktop on Kali Linux and drove the entire attack using natural-language prompts to the connected Hexstrike-AI MCP server:

**AI Prompt 1:**
> `Check if John the Ripper is installed in this Hexstrike MCP and show me its version`

Claude confirmed John the Ripper was installed (Jumbo, community-enhanced edition) and reported its version.

**AI Prompt 2:**
> `Please calculate the hash value of this PDF file: /home/kali/Desktop/hash3.networkwalks_flag1.pdf`

Claude used the MCP's integrated tools to extract the PDF's crackable hash (MD5, SHA‑1, SHA‑256 were all shown, along with the file's John‑the‑Ripper‑ready hash).

**AI Prompt 3:**
> `Please use JTR tool in this hexstrike MCP server to crack the password of this PDF file. Use the rockyou.txt wordlist dictionary.`

Claude ran John the Ripper against the extracted hash using the `rockyou.txt` dictionary.

<p align="center"><img src="images/image27.png" width="420"/></p>
<p align="center"><img src="images/image28.png" width="450"/></p>

💡 **Tip learned along the way:** Kali Linux ships with several wordlists pre-installed at `/usr/share/wordlists` (including `rockyou.txt`), which is why the AI agent was able to locate and use it directly.

### Result

✅ **The PDF password was cracked by the AI agent:**

| Detail | Value |
|---|---|
| File | `hash3.networkwalks_flag1.pdf` |
| **Password** | **`password1`** |
| Hash Format | PDF [MD5 SHA2 RC4/AES 32/64] |
| Wordlist | `rockyou.txt` (14.3M passwords) |
| Time to Crack | Under 1 second |

<p align="center"><img src="images/image29.png" width="480"/></p>

This confirms `password1` was found almost instantly because it sits very near the top of the `rockyou.txt` wordlist — once again reinforcing why common/weak passwords offer almost no real protection. This demonstrates that the same hash-extraction → dictionary-attack workflow from Module 1 and Module 2 can be fully automated end-to-end by an AI assistant connected to real security tooling via MCP.

---

## ✅ Results Summary

| Module | Tool(s) Used | File | Cracked Password |
|---|---|---|---|
| Module 1 | JTR John + Johnny (GUI) | My Locked PDF1.pdf | `good-luck` |
| Module 1 (extra) | JTR John + Johnny (GUI) | File 2 | `Password1` |
| Module 1 (extra) | JTR John + Johnny (GUI) | File 3 | `1qaz2wsx` |
| Module 2 | NetworkWalks Hash Calculator + Password Cracker | My Locked PDF1.pdf | `Password1` |
| Bonus (W3-OPTIONAL1) | Claude Desktop + Hexstrike MCP + John the Ripper + rockyou.txt | networkwalks_flag1.pdf | `password1` (cracked in <1 sec) |

## 🔑 Key Takeaways
- Password-protected files (PDF, ZIP, Office) store their password as a **hash**, not as plain text; cracking tools work by hashing candidate passwords and comparing them against the stored hash.
- Short, common, or dictionary-based passwords (e.g. `good-luck`, `Password1`, `1qaz2wsx`) can be cracked in seconds to minutes — reinforcing why **strong, unique passwords** matter.
- The same cracking logic (extract hash → run candidate passwords → match) works whether it's done with a command-line tool like John the Ripper, a no-install browser tool, or an AI agent orchestrating the tools through MCP.
- Connecting an AI assistant to real security tooling via **MCP (Model Context Protocol)** shows how AI can automate and accelerate standard security workflows — which is also why such tooling must be used only in authorized, controlled lab environments.

## 📚 Tools & References
- John the Ripper: https://www.openwall.com/john/
- Johnny (GUI for JTR): https://openwall.info/wiki/john/johnny
- Online Hash Crack – PDF Hash Extractor: https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php
- NetworkWalks Hash Calculator: https://networkwalks.com/hash-calculator/
- NetworkWalks Password Cracker: https://networkwalks.com/password-cracker/
- Claude Desktop (unofficial, Linux): https://github.com/aaddrick/claude-desktop-debian
- Hexstrike-AI MCP: https://github.com/0x4m4/hexstrike-ai

---
*Submitted as part of the Week 3 project work for the Cybersecurity & Ethical Hacking Internship, NetworkWalks Academy.*
