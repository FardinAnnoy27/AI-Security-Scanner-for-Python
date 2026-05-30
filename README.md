📋 Full Project Overview

Built an AI-powered CLI security scanner that uses the Google Gemini API to analyze Python code for security vulnerabilities and display results with color-coded severity ratings in the terminal. You wrote all the code in Cursor IDE, an AI-powered code editor.

Tools & Technologies Used:

IDE: Cursor (AI-powered code editor)
Language: Python 3.x
AI Model: Google Gemini 2.5 Flash
Libraries: google-genai, python-dotenv, colorama
Platform: Windows
Cost: $0 (Gemini free tier)
<img width="3106" height="839" alt="image" src="https://github.com/user-attachments/assets/ab624136-f1da-42b9-ace1-ff8b482e1751" />

🏗️ Architecture Design

```text

┌──────────────────────────────────────────────────────────┐
│                    USER (Terminal/CLI)                     │
│                                                           │
│   Option A: python scanner.py        (hardcoded examples) │
│   Option B: python scanner.py app.py (scan real file) 💎  │
└────────────────────────┬─────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────┐
│            scanner.py (Written in Cursor IDE)             │
│                                                           │
│  ┌─────────────────────────────────────────────────────┐  │
│  │  1. SETUP                                           │  │
│  │     - load_dotenv() → reads .env file               │  │
│  │     - os.getenv("GOOGLE_API_KEY") → gets API key    │  │
│  │     - genai.Client(api_key) → creates Gemini client │  │
│  └─────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────┐  │
│  │  2. INPUT                                           │  │
│  │     - Hardcoded vulnerable code examples OR         │  │
│  │     - Read real .py file from command line (💎)     │  │
│  └─────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────┐  │
│  │  3. PROMPT ENGINEERING                              │  │
│  │     - Structured security analysis prompt           │  │
│  │     - Requests: vulnerability, severity, fix        │  │
│  └─────────────────────────────────────────────────────┘  │
│  ┌─────────────────────────────────────────────────────┐  │
│  │  4. OUTPUT                                          │  │
│  │     - add_colors_to_output() with colorama          │  │
│  │     - 🔴 CRITICAL  🟠 HIGH  🟡 MEDIUM  🟢 LOW     │  │
│  └─────────────────────────────────────────────────────┘  │
└────────────────────────┬─────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────┐
│               Google Gemini API (Cloud)                    │
│                                                           │
│   Model: gemini-2.5-flash                                 │
│   Input: Python code + structured security prompt         │
│   Output: Vulnerability report with severity ratings      │
└──────────────────────────────────────────────────────────┘

```

Final Project File Structure:

```text

E:\Security-Scanner\
├── scanner.py           ← Main script (all logic)
├── .env                 ← Your GOOGLE_API_KEY (never push!)
├── .gitignore           ← Tells Git what to ignore
├── requirements.txt     ← Python dependencies
├── README.md            ← Project documentation
└── venv\                ← Virtual environment (never push!)

```



🔄 Total Project Process — Step by Step with Every Command

Phase 1: Environment Setup

1.1 — Install Cursor IDE
Downloaded and installed Cursor from cursor.com/downloads
Ran the .exe installer on Windows
Opened Cursor IDE

1.2 — Create the project folder
Opened the Cursor terminal (Ctrl + `) and ran:

```powershell
E:
mkdir Security-Scanner
cd Security-Scanner
```

1.3 — Create a Python virtual environment

```powershell
python -m venv venv
```

1.4 — Activate the virtual environment

```powershell
venv\Scripts\activate
```

✅ You should see (venv) appear at the start of your terminal line.

1.5 — Install required Python packages

```powershell
pip install google-genai python-dotenv colorama
```

Phase 2: API Key Setup

2.1 — Get your Google Gemini API key
Went to aistudio.google.com/apikey
Clicked Create API Key
Copied the key

2.2 — Create the .env file
Created a new file called .env in the project root (E:\Security-Scanner\) in Cursor with this content:

```text
GOOGLE_API_KEY=your_api_key_here
```

Phase 3: Build the Scanner (in Cursor IDE)
3.1 — Create scanner.py and test API connection
Created scanner.py in the project root in Cursor. First version was a basic API connection test:

```python
import os
from dotenv import load_dotenv
import google.genai as genai

load_dotenv()
api_key = os.getenv("GOOGLE_API_KEY")

client = genai.Client(api_key=api_key)

# Test with a simple prompt
try:
    response = client.models.generate_content(
        model='gemini-2.5-flash', contents='Why is the sky blue?'
    )
    print(response)
except Exception as e:
    print(f"❌ Connection failed: {e}")
```

Ran the test in the Cursor terminal:

```powershell
python scanner.py
```

✅ If you got a response about the sky, the API connection is working!

3.2 — Add vulnerable code examples
Added hardcoded Python code samples with known vulnerabilities for the scanner to analyze, including:
🔓 SQL injection — Unsanitized user input in database queries
🔑 Hardcoded secrets — API keys and passwords directly in code
🔐 Weak cryptography — Using MD5 for password hashing

3.3 — Craft the security analysis prompt
Built a structured prompt that tells Gemini exactly how to analyze code, requesting:
Vulnerability name
Severity rating (CRITICAL / HIGH / MEDIUM / LOW)
Explanation of the risk
Recommended fix

3.4 — Add color-coded output with colorama
Added the add_colors_to_output() function to color-code severity ratings in the terminal:

🔴 CRITICAL — Red
🟠 HIGH — Yellow/Orange
🟡 MEDIUM — Yellow
🟢 LOW — Green

Tested the full scanner in the Cursor terminal:

```powershell
python scanner.py
```

✅ Should see the vulnerability report with color-coded severity ratings!

Phase 4: Secret Mission 💎 — Scan Real Files

4.1 — Add command-line file scanning

Updated scanner.py to accept a file path as a command-line argument using sys.argv, so you can scan any real .py file.

4.2 — Test with a real Python file

```powershell
python scanner.py some_file.py
```

✅ The scanner now reads and analyzes any Python file you point it at!

Phase 5: Upload to GitHub

5.1 — Generate requirements.txt

```powershell
pip freeze > requirements.txt
```

5.2 — Create .gitignore

Run this in the Cursor terminal:

```powershell
@"
venv/
.env
__pycache__/
*.pyc
"@ | Out-File -Encoding utf8 .gitignore
```

Verify it:

```powershell
type .gitignore
```

5.3 — Create README.md

```powershell
@"
# AI Security Scanner for Python

A CLI tool that uses Google's Gemini API to scan Python code for security vulnerabilities with color-coded severity ratings. Built in Cursor IDE.

## What It Does
- Detects **SQL injection**, **hardcoded secrets**, and **weak cryptography** (e.g., MD5)
- Uses **Gemini 2.5 Flash** for AI-powered code analysis
- Displays results with **color-coded severity ratings** in the terminal
- Supports scanning real `.py` files from the command line

## Tech Stack
- Python 3.x
- Google Gemini API (`google-genai`)
- colorama (colored terminal output)
- python-dotenv (environment variable management)
- Cursor IDE (AI-powered code editor)

## Architecture
```
User (CLI) --> scanner.py --> Google Gemini API
                  |                  |
           Reads .py file     Returns vulnerability
           Crafts prompt      report with severity
                  |                  |
                  v                  v
           Color-coded terminal output
```

## Setup
1. Clone this repo: `git clone https://github.com/FardinAnnoy27/AI-Security-Scanner-for-Python.git`
2. Create a virtual environment: `python -m venv venv`
3. Activate it: `venv\Scripts\activate` (Windows) or `source venv/bin/activate` (Mac)
4. Install dependencies: `pip install -r requirements.txt`
5. Create a `.env` file and add your API key:
   ```
   GOOGLE_API_KEY=your_key_here
   ```
6. Run the scanner: `python scanner.py`
7. Scan a real file: `python scanner.py yourfile.py`

## Built With
This project was built as part of [NextWork](https://learn.nextwork.org)'s Security x AI learning path.
"@ | Out-File -Encoding utf8 README.md
```

5.4 — Verify scanner.py has NO hardcoded API key

Open scanner.py in Cursor and confirm you see this (not your actual key):

```python
load_dotenv()
api_key = os.getenv("GOOGLE_API_KEY")
```

5.5 — Create the GitHub repository

Go to github.com/new
Repository name: AI-Security-Scanner-for-Python
Set to Public
Do NOT check "Add a README"
Do NOT check "Add .gitignore"
Click Create repository

⚠️ If this repo already exists from your earlier attempt, delete it first (Settings → scroll to bottom → Delete this repository), then recreate it fresh.

5.6 — Remove any old Git history

```powershell
if (Test-Path .git) { Remove-Item -Recurse -Force .git }
```

5.7 — Initialize Git

```powershell
git init
```

5.8 — Stage all files

```powershell
git add .
```

5.9 — Verify the right files are staged

```powershell
git status
```

✅ You should see: scanner.py, requirements.txt, README.md, .gitignore
❌ You should NOT see: .env or venv/

5.10 — Commit

```powershell
git commit -m "Add AI Security Scanner for Python"
```

5.11 — Set branch to main

```powershell
git branch -M main
```

5.12 — Connect to your GitHub repository

```powershell
git remote add origin https://github.com/FardinAnnoy27/AI-Security-Scanner-for-Python.git
```

5.13 — Push to GitHub

```powershell
git push -u origin main
```

You may be prompted to sign in to GitHub — follow the browser prompts.

5.14 — Verify on GitHub ✅

Visit your repo on GitHub and confirm:
✅ scanner.py
✅ requirements.txt
✅ README.md (rendered nicely with architecture diagram)
✅ .gitignore
❌ No venv/ folder
❌ No .env file

Phase 6: Clean Up & Security

6.1 — Regenerate your API key 🔑
Since your earlier push attempt exposed your key:
Go to aistudio.google.com/apikey
Delete the old key
Create a new key
Update your .env file with the new key

6.2 — Deactivate virtual environment (when done)

```powershell
deactivate
```

The (venv) prefix will disappear from your terminal.

6.3 — To reactivate later

Whenever you want to work on this project again:

```powershell
cd E:\Security-Scanner
venv\Scripts\activate
python scanner.py
```


That's the entire project from start to finish,  Let me know if you need any tweaks or run into issues. 🚀
