# English Pronunciation Trainer — Full MVP (Frontend + Backend)

This document contains a complete, ready-to-run project skeleton for the Pronunciation Trainer MVP (React frontend + FastAPI backend using Whisper local). Copy the files into a repo, follow the run instructions, and you'll have an end-to-end system for recording audio in the browser, sending it to the backend, transcribing with Whisper and returning pronunciation scoring.

---

## Project structure

```
pronunciation-trainer/
├── .gitignore
├── README.md
├── backend/
│   ├── requirements.txt
│   └── app/
│       ├── main.py
│       └── utils/
│           ├── whisper_loader.py
│           └── text_utils.py
└── frontend/
    ├── package.json
    ├── index.html
    └── src/
        ├── main.jsx
        ├── App.jsx
        ├── api.js
        ├── App.css
        └── components/
            ├── Recorder.jsx
            └── ResultBox.jsx
```

---

> *Note:* this repo intentionally keeps things minimal and dependency-light. No Tailwind. Pure React + vanilla CSS. Whisper runs locally on the backend (you need `ffmpeg` installed and Python environment).

---

## File contents

### `.gitignore`

```gitignore
venv/
__pycache__/
*.pyc
node_modules/
dist/
.env
*.wav
*.webm
.DS_Store
```

---

### `README.md` (top-level)

> A short README with run instructions is included here. See the `backend/` and `frontend/` sections for details.

````markdown
# English Pronunciation Trainer — Full MVP

## Overview
This project contains a React frontend (record audio and display results) and a FastAPI backend (Whisper local transcription + simple scoring).

## Prerequisites
- Node.js 18+ and npm
- Python 3.10+
- ffmpeg installed and available on PATH

## Quick start
1. Backend
   ```bash
   cd backend
   python -m venv venv
   source venv/bin/activate    # (Windows: venv\Scripts\activate)
   pip install -r requirements.txt
   uvicorn app.main:app --reload
````

2. Frontend

   ```bash
   cd frontend
   npm install
   npm run dev
   ```

Frontend default port is 5173, backend default port is 8000.

## Git & GitHub (short)

```bash
git init
git add .
git commit -m "Initial commit: pronunciation trainer MVP"
# Create a repo on GitHub, then:
git remote add origin git@github.com:YOUR_USERNAME/REPO_NAME.git
git push -u origin main
```

```
```

---

### `backend/requirements.txt`

```
fastapi
uvicorn
openai-whisper
python-Levenshtein
pydub
ffmpeg-python
```

> If installing `openai-whisper` causes issues, you can instead install `git+https://github.com/openai/whisper.git` or use `whisperx` distributions depending on your environment. `python-Levenshtein` may require build tools on Windows.

---

## Running the project locally

### Backend

1. Install ffmpeg on your OS and ensure it's on PATH.
2. Create Python venv and install requirements (see `backend/requirements.txt`).
3. Start server:

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Open `http://localhost:5173` and the app should load. Click `Record`, speak the sentence, then `Stop & Submit` to send audio to the backend. The backend will transcribe and return scoring.

---

## Git & GitHub step-by-step beginner guide

1. Initialize local Git repo

```bash
git init
git add .
git commit -m "Initial commit: Pronunciation Trainer MVP"
```

2. Create a repository on GitHub (via web UI) and copy the remote URL (SSH or HTTPS). Example (SSH):

```bash
git remote add origin git@github.com:YOUR_USERNAME/pronunciation-trainer.git
git branch -M main
git push -u origin main
```

3. Common commands to practice:

* `git status` — xem thay đổi hiện tại
* `git add <file>` — thêm file vào staging
* `git commit -m "msg"` — commit thay đổi
* `git pull` — kéo thay đổi từ remote vào local (merge)
* `git push` — đẩy commit lên remote
* `git log --oneline` — xem lịch sử commit ngắn gọn

4. If you need to update a file and push:

```bash
# make changes
git add .
git commit -m "Fix recorder bug and improve UI"
git push
```

5. If remote has new commits, sync first:

```bash
git pull origin main
# resolve conflicts if any
```

---

## Notes & troubleshooting

* If Whisper installation is heavy for your machine, use model `tiny` instead of `base` in `whisper_loader.py` to reduce memory/CPU usage: `load_whisper_model("tiny")`.
* On Windows, installing `python-Levenshtein` may need Visual C++ build tools. Alternatively, remove that dependency and use pure Python distance via `difflib.SequenceMatcher` (slower, but workable).
* If browser records `audio/webm` and pydub/ffmpeg can't parse it, ensure ffmpeg supports the recorded codec; modern ffmpeg usually does.

---


