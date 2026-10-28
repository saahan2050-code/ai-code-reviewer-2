# 🐞 AI Code Reviewer & Bug Detector

A Streamlit app that reviews your code with **Google Gemini Flash**, detects bugs, explains them, and returns a fixed version.

## Features

- 🐛 **Bug detection** – bugs, logic errors, security flaws, performance and style problems, each with severity, category and line number.
- ✅ **Auto-debugging** – a complete corrected version of your code with a plain-English list of what changed.
- 🔀 **Diff view** – see exactly which lines changed (original vs fixed).
- 🧪 **Python syntax pre-check** – instant local check using Python's `ast` module, fed to the AI as extra context.
- 🧾 **Error-aware** – paste a traceback or describe the symptom to help the AI find the root cause.
- 📂 **Paste or upload** – 15+ languages (Python, JavaScript, TypeScript, Java, C/C++, C#, Go, Rust, PHP, Ruby, Kotlin, Swift, SQL, Bash, HTML/CSS).
- 📥 **Downloads** – fixed code and a full Markdown report.
- 🎛️ **Review focus** – choose bugs, security, performance, readability.
- 📄 **Sample button** – load buggy demo code to try the app instantly.

## Project structure

```
.
├── app.py             # the whole app
├── requirements.txt   # Python dependencies
└── README.md
```

## Run locally

1. Install Python 3.10+.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Get a free Gemini API key at <https://aistudio.google.com/apikey>.
4. Provide the key in **one** of these ways:
   - Paste it in the app's sidebar (easiest), **or**
   - Set an environment variable:
     - macOS/Linux: `export GEMINI_API_KEY="your-key"`
     - Windows (PowerShell): `$env:GEMINI_API_KEY="your-key"`
   - **or** create `.streamlit/secrets.toml` containing:
     ```toml
     GEMINI_API_KEY = "your-key"
     ```
5. Start the app:
   ```bash
   streamlit run app.py
   ```

## Configuration

| Setting | Where | Default |
|---|---|---|
| Gemini API key | Sidebar / `GEMINI_API_KEY` secret / env var | – |
| Model name | Sidebar | `gemini-2.5-flash` |
| Max code size | `MAX_CHARS` in `app.py` | 40,000 characters |

If Google renames or retires a model, type the new Flash model name into the sidebar – no code change needed.

## How it works

1. Your code is numbered line by line so the AI can cite exact lines.
2. For Python, a local syntax check runs first.
3. Gemini is asked (with `application/json` output) for a structured result: summary, quality score, issues, fixed code, and change notes.
4. The app validates and normalises the JSON, then shows issues, fixed code, diff and a downloadable report.

## Deploy on Streamlit Community Cloud

1. Push this repo to GitHub.
2. Go to <https://share.streamlit.io> and sign in with GitHub.
3. Click **Create app** → **Deploy a public app from GitHub**.
4. Choose your repository, branch `main`, and main file path `app.py`.
5. Open **Advanced settings → Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
6. Click **Deploy**.

> ⚠️ Never commit your API key to GitHub. Use Secrets.

## Privacy & limitations

- Code you submit is sent to Google's Gemini API. Don't paste secrets, credentials or confidential code you aren't allowed to share.
- AI can miss bugs or suggest wrong fixes. Always read the changes and run your tests before using them.
- Very large files should be reviewed in smaller pieces.

## License

MIT – use it, modify it, share it.
