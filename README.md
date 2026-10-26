# 📄 ATS Resume Analyzer

A Streamlit app that scores a resume for ATS (Applicant Tracking System) compatibility and gives specific, prioritised improvements, powered by Google Gemini Flash.

## Features
- Upload a resume as **PDF, DOCX or TXT**
- **ATS score (0-100)** built from five weighted categories: formatting (20%), keywords (25%), experience (25%), clarity (15%), completeness (15%)
- Prioritised improvements (High / Medium / Low) with example rewrites
- Optional **job description** input for role-specific keyword matching and a job-match score
- Instant rule-based checks (email, phone, sections, length, bullets, metrics)
- Downloadable Markdown report

## Project structure
```
ats-resume-analyzer/
├── app.py
├── requirements.txt
├── README.md
└── .gitignore
```

## Run locally
1. Install Python 3.10+.
2. Create a free API key at https://aistudio.google.com/apikey
3. In the project folder:
   ```bash
   python -m venv venv
   source venv/bin/activate        # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```
4. Provide your key, either way:
   - **Option A:** create `.streamlit/secrets.toml` containing
     ```toml
     GEMINI_API_KEY = "your-key-here"
     ```
   - **Option B:** skip this and paste the key in the app sidebar.
5. Start the app:
   ```bash
   streamlit run app.py
   ```

## Push to GitHub (using the website, no Git needed)
1. Sign in at https://github.com and click **+ → New repository**.
2. Name it (e.g. `ats-resume-analyzer`), choose **Public** (required for free Streamlit Cloud unless you link a private repo), and click **Create repository**.
3. On the new repo page click **uploading an existing file**.
4. Drag in `app.py`, `requirements.txt`, `README.md` and `.gitignore`, then click **Commit changes**.
5. **Never upload `secrets.toml` or any file containing your API key.**

## Deploy on Streamlit Community Cloud
1. Go to https://share.streamlit.io and sign in with GitHub (authorise access when asked).
2. Click **Create app** → **Deploy a public app from GitHub**.
3. Pick your repository, branch `main`, and main file path `app.py`.
4. Open **Advanced settings → Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-key-here"
   ```
5. Click **Deploy**. The first build takes a few minutes. You get a public `*.streamlit.app` URL.

To update the app later, edit a file on GitHub (pencil icon → commit). Streamlit redeploys automatically.

## Configuration
| Setting | Where | Notes |
|---|---|---|
| `GEMINI_API_KEY` | Streamlit secrets or environment variable | If missing, the sidebar asks for it |
| Model | Sidebar dropdown | Default `gemini-2.5-flash`; edit `MODEL_OPTIONS` in `app.py` to add newer Flash models |

## Limitations
- Scanned/image-only PDFs have no text to read. Export a text-based PDF or use DOCX.
- The AI score is an estimate; real ATS software varies. Use it as guidance, not a guarantee.
- Resume text is sent to the Gemini API. Do not upload documents you are not comfortable sharing.
- If you deploy publicly with your own key, anyone using your app uses your quota. Consider removing the secret and asking users for their own key.

## Troubleshooting
- **"API key looks invalid"**: re-copy the key; make sure it has no spaces or quotes.
- **Rate limit / quota**: wait a minute; the free tier has per-minute limits.
- **Model not found**: choose a different model in the sidebar.
- **Deploy fails on dependencies**: confirm `requirements.txt` is in the repo root.
