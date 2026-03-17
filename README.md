# Ticket Entry — Voice to Excel

Record handwritten tickets by voice → auto-fill 4 fields → export `.xlsx`.

## Deploy to Render (free)

### Step 1 — Push to GitHub
```bash
git init
git add .
git commit -m "initial commit"
# create a repo on github.com, then:
git remote add origin https://github.com/YOUR_USERNAME/ticket-entry.git
git push -u origin main
```

### Step 2 — Deploy on Render
1. Go to https://render.com and sign in
2. Click **New → Web Service**
3. Connect your GitHub repo
4. Render auto-detects `render.yaml` — just click **Deploy**
5. Wait ~3 minutes for the first build

### Step 3 — Add ffmpeg build step (important!)
In your Render service → **Settings → Build Command**, set it to:
```
pip install -r requirements.txt
```
Then go to **Environment** and add:
```
Key: NIXPACKS_APT_PKGS   Value: ffmpeg
```
This installs ffmpeg (needed for audio conversion).

### Step 4 — Use the app
- Open your Render URL (e.g. `https://ticket-entry.onrender.com`)
- Paste your Sarvam API key → click **Save**
- Press **R** to start recording, **S** to stop
- Fields auto-fill from your voice → press **Enter** or click **Add entry**
- Repeat for all tickets → click **Download Excel**

---

## Run locally
```bash
pip install -r requirements.txt
# also install ffmpeg: brew install ffmpeg  (Mac) or  apt install ffmpeg  (Linux)
python app.py
# open http://localhost:5000
```

## Security note
- Your Sarvam API key is stored in your browser's localStorage only
- It is sent directly from your browser to the `/transcribe` endpoint on this server
- It is never logged or stored server-side
