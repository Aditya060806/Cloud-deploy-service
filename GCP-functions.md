# ☁️ GCP $5 CREDIT — 1 HOUR HANDS-ON LAB
### 🚀 4 Real GCP Services | Deploy. Store. Function. Query.

> **Prereq:** Google Cloud account with billing enabled + $5 free credits applied
> **Time:** 60 minutes total | **Cost:** < $0.10 (well within $5 credits)

---

## ⚡ What You'll Build in 1 Hour

| # | Service | What You'll Do | Time |
|---|---------|----------------|------|
| Lab 1 | **Cloud Run** | Deploy a live web app to the internet | 15 min |
| Lab 2 | **Cloud Storage** | Host a public file/image on the internet | 10 min |
| Lab 3 | **Cloud Functions** | Deploy a serverless API endpoint | 15 min |
| Lab 4 | **BigQuery** | Query a real dataset with SQL | 10 min |
| Bonus | **Connect it all** | Chain your services together | 10 min |

---

---

# LAB 1 — CLOUD RUN
## Deploy a Live Web App
### ⏱ 15 minutes | 💰 Cost: ~$0.00 (free tier)

---

### 📌 Step 1 — Open Cloud Run

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Search bar → type `Cloud Run` → click it
3. Click **"+ Create Service"**

---

### 📌 Step 2 — Configure Your Service

Fill in these fields:

| Field | Value |
|-------|-------|
| Deployment source | Deploy one revision from an existing container image |
| Container image URL | `gcr.io/cloudrun/hello` |
| Service name | `my-first-app` |
| Region | `asia-south1 (Mumbai)` |
| Authentication | ✅ Allow unauthenticated invocations |

---

### 📌 Step 3 — Deploy

1. Scroll to bottom → click **"Create"**
2. Wait 30–60 seconds for the green ✅
3. Click the **blue URL** at the top

**You now have a live app on the internet. ✅**

> 📋 **Copy your URL** — you'll use it in the Bonus lab.

---

### 🧠 What Just Happened?

- Google spun up a container in their Mumbai datacenter
- Assigned it a permanent public URL
- It auto-scales: 0 containers when no traffic, scales up on demand
- **You paid $0** — Cloud Run has a 2 million request/month free tier

---

---

# LAB 2 — CLOUD STORAGE
## Host a Public File on the Internet
### ⏱ 10 minutes | 💰 Cost: ~$0.00 (5GB free tier)

---

### 📌 Step 1 — Open Cloud Storage

1. Search bar → type `Cloud Storage` → click it
2. Click **"+ Create"** (create a bucket)

---

### 📌 Step 2 — Configure Your Bucket

| Field | Value |
|-------|-------|
| Bucket name | `yourname-gcp-lab-2025` *(must be globally unique)* |
| Location type | Region |
| Region | `asia-south1 (Mumbai)` |
| Storage class | Standard |
| Access control | Uncheck "Enforce public access prevention" |

Click **"Create"**

---

### 📌 Step 3 — Upload a File

1. Inside your new bucket, click **"Upload files"**
2. Upload **any image** from your laptop (a photo, logo, anything)
3. Wait for the upload to complete

---

### 📌 Step 4 — Make It Public

1. Click the filename of your uploaded file
2. Click **"Edit access"** (or go to Permissions tab)
3. Click **"+ Add Principal"**
   - Principal: `allUsers`
   - Role: `Storage Object Viewer`
4. Click **"Save"**
5. Click **"Allow public access"** in the confirmation dialog

---

### 📌 Step 5 — Get Your Public URL

Your file is now live at:
```
https://storage.googleapis.com/YOUR-BUCKET-NAME/YOUR-FILENAME
```

1. Click your file → copy the **Public URL**
2. Open it in a new tab — your file is live on the internet ✅

> 💡 This is exactly how companies host images, videos, PDFs, and static assets at massive scale (Netflix, Spotify, etc.)

---

---

# LAB 3 — CLOUD FUNCTIONS
## Deploy a Serverless API Endpoint
### ⏱ 15 minutes | 💰 Cost: ~$0.00 (2M invocations/month free)

---

### 📌 Step 1 — Open Cloud Functions

1. Search bar → type `Cloud Functions` → click it
2. Click **"+ Create Function"**

---

### 📌 Step 2 — Basic Configuration

| Field | Value |
|-------|-------|
| Environment | 2nd gen |
| Function name | `hello-api` |
| Region | `asia-south1` |
| Trigger type | HTTPS |
| Authentication | ✅ Allow unauthenticated invocations |

Click **"Next"**

---

### 📌 Step 3 — Write Your Function

You'll see a code editor. Select **Runtime: Node.js 20**

Replace the code in `index.js` with this:

```javascript
const functions = require('@google-cloud/functions-framework');

functions.http('helloApi', (req, res) => {
  const name = req.query.name || 'World';
  res.json({
    message: `Hello, ${name}! 👋`,
    timestamp: new Date().toISOString(),
    region: 'asia-south1',
    powered_by: 'Google Cloud Functions'
  });
});
```

Make sure **Entry point** is set to: `helloApi`

---

### 📌 Step 4 — Deploy

1. Click **"Deploy"**
2. Wait 1–2 minutes for the green ✅
3. Go to the **"Trigger"** tab
4. Copy the **Trigger URL**

---

### 📌 Step 5 — Test Your API

Open these URLs in your browser:

```
https://YOUR-TRIGGER-URL
https://YOUR-TRIGGER-URL?name=Aditya
https://YOUR-TRIGGER-URL?name=Engineer
```

You should see a JSON response like:
```json
{
  "message": "Hello, Aditya! 👋",
  "timestamp": "2025-01-15T10:30:00.000Z",
  "region": "asia-south1",
  "powered_by": "Google Cloud Functions"
}
```

**You just built a real REST API endpoint. ✅**

> 💡 Change `?name=` to anything — your own name, your college, anything. Every request is a live API call.

---

---

# LAB 4 — BIGQUERY
## Query a Real Dataset with SQL
### ⏱ 10 minutes | 💰 Cost: $0.00 (first 1TB queries are free)

---

### 📌 Step 1 — Open BigQuery

1. Search bar → type `BigQuery` → click it
2. Click **"+ Add"** → **"Public Datasets"** (or skip, we'll use them directly)
3. Click **"SQL Workspace"** or **"Compose new query"** at the top

---

### 📌 Step 2 — Run Query #1 — COVID Data

Paste this into the query editor and click **"Run"**:

```sql
SELECT
  country_name,
  date,
  new_confirmed,
  cumulative_confirmed
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  country_name = 'India'
  AND date >= '2021-01-01'
  AND date <= '2021-12-31'
ORDER BY
  date DESC
LIMIT 20;
```

You'll see real COVID data for India from 2021. ✅

---

### 📌 Step 3 — Run Query #2 — Wikipedia Page Views

```sql
SELECT
  title,
  views
FROM
  `bigquery-public-data.wikipedia.table_bands`
ORDER BY
  views DESC
LIMIT 10;
```

See which Wikipedia pages got the most views. ✅

---

### 📌 Step 4 — Run Query #3 — NYC Taxi Trips (Your Own Analysis)

```sql
SELECT
  EXTRACT(HOUR FROM pickup_datetime) AS hour_of_day,
  COUNT(*) AS total_trips,
  ROUND(AVG(trip_distance), 2) AS avg_distance_miles,
  ROUND(AVG(fare_amount), 2) AS avg_fare_usd
FROM
  `bigquery-public-data.new_york_taxi_trips.tlc_yellow_trips_2022`
WHERE
  fare_amount > 0
  AND trip_distance > 0
GROUP BY
  hour_of_day
ORDER BY
  total_trips DESC
LIMIT 24;
```

This tells you: **which hour of the day has the most NYC taxi trips**. ✅

> 💡 **This query runs across millions of rows in seconds.** On a normal laptop this would take hours. BigQuery processes it using Google's distributed compute infrastructure.

---

### 🧠 What is BigQuery?

- Google's **data warehouse** — stores and queries petabytes of data
- Used by companies to analyze billions of rows of business data
- You write SQL → Google does the heavy lifting
- No servers, no setup, no indexes — just query and go

---

---

# BONUS LAB — CHAIN IT ALL TOGETHER
### ⏱ 10 minutes | Connect your 3 services

---

### 🎯 Challenge: Build a Mini Cloud Architecture

You've deployed:
- ✅ A web app on **Cloud Run**
- ✅ A public file on **Cloud Storage**
- ✅ An API on **Cloud Functions**
- ✅ Queried data on **BigQuery**

Now do these:

---

### 🔗 Challenge 1 — Call Your API from Browser DevTools

1. Open your **Cloud Run** app URL
2. Right-click → **Inspect** → **Console** tab
3. Paste this (replace with your Cloud Functions URL):

```javascript
fetch('https://YOUR-CLOUD-FUNCTION-URL?name=CloudEngineer')
  .then(r => r.json())
  .then(data => console.log(data))
```

4. Press Enter

You just called your Cloud Function API **from inside a browser console**. ✅

---

### 🔗 Challenge 2 — View Your Storage File in Cloud Run

1. Open your Cloud Run app URL
2. In the browser address bar, note the domain
3. In a new tab, open your Cloud Storage public image URL
4. Both are hosted on Google Cloud infrastructure — one is compute, one is storage

---

### 🔗 Challenge 3 — Save a BigQuery Result

1. Run any BigQuery query from Lab 4
2. Click **"Save Results"** → **"Google Sheets"**
3. Open the Google Sheet that appears
4. You just exported cloud data directly into Google Sheets ✅

---

---

# 🏁 LAB COMPLETION CHECKLIST

Check off everything you completed:

- [ ] ✅ **Lab 1** — Cloud Run app is live with a public URL
- [ ] ✅ **Lab 2** — File uploaded to Cloud Storage and publicly accessible
- [ ] ✅ **Lab 3** — Cloud Function API returns JSON with `?name=` parameter
- [ ] ✅ **Lab 4** — Ran at least 2 BigQuery queries on real public datasets
- [ ] ⭐ **Bonus 1** — Called Cloud Function from browser console
- [ ] ⭐ **Bonus 2** — Exported BigQuery result to Google Sheets

---

# 💰 CREDIT USAGE SUMMARY

| Service | Free Tier | Your Usage | Cost |
|---------|-----------|-----------|------|
| Cloud Run | 2M requests/month free | ~50 requests | $0.00 |
| Cloud Storage | 5GB free | <1MB | $0.00 |
| Cloud Functions | 2M invocations/month free | ~20 calls | $0.00 |
| BigQuery | First 1TB queries free | <1MB scanned | $0.00 |
| **Total** | | | **~$0.00** |

> Your $5 credit is essentially untouched. You can run these labs **hundreds of times** before spending a cent.

---

# 🧠 WHAT YOU LEARNED TODAY

| Concept | Service | Real-World Use |
|---------|---------|----------------|
| Serverless compute | Cloud Run | Netflix, Twitter auto-scaling |
| Object storage | Cloud Storage | Dropbox, Instagram image hosting |
| Serverless functions | Cloud Functions | Stripe webhooks, Slack bots |
| Data warehousing | BigQuery | Uber analytics, Airbnb reporting |
| Public datasets | BigQuery | Research, journalism, data science |

---

# 🚀 WHAT TO EXPLORE NEXT (WITH YOUR $5 CREDITS)

| Project | Services Used | Est. Cost |
|---------|--------------|-----------|
| Deploy your own Python/Node app | Cloud Run + Container Registry | ~$0.01 |
| Build a file upload website | Cloud Run + Cloud Storage | ~$0.02 |
| Create a REST API backend | Cloud Functions + Firestore | ~$0.01 |
| Analyze your own CSV data | BigQuery | ~$0.00 |
| Build a chatbot | Cloud Functions + Dialogflow | ~$0.05 |

---

## ⚠️ TROUBLESHOOTING

| Problem | Fix |
|---------|-----|
| Cloud Run deploy fails | Check image URL: `gcr.io/cloudrun/hello` exactly |
| Storage bucket name taken | Add more random numbers: `myname-lab-48291` |
| Cloud Function deploy takes too long | Wait up to 3 minutes — 2nd gen takes longer |
| BigQuery query has error | Make sure you copied the full SQL including backticks |
| "Quota exceeded" error | Check your project has billing enabled |
| Storage file not public | Make sure you added `allUsers` with `Storage Object Viewer` role |

---

*☁️ GCP 1-Hour Hands-On Lab | Cloud Run · Cloud Storage · Cloud Functions · BigQuery*

---

---

# 🏗️ PROJECT LAB — BUILD A FILE UPLOAD WEBSITE
## Cloud Run + Cloud Storage — Full Stack on GCP
### ⏱ ~30 minutes | 💰 Cost: ~$0.02

> You will build a real web app where anyone can visit a URL, upload a file, and get back a **permanent public link** — hosted entirely on Google Cloud.

---

## 🗺️ Architecture Overview

```
User (Browser)
     │
     ▼
┌─────────────────────┐
│   Cloud Run         │  ← Your Node.js web app (handles uploads)
│   (Web Server)      │
└─────────┬───────────┘
          │  saves file
          ▼
┌─────────────────────┐
│   Cloud Storage     │  ← Stores the uploaded file permanently
│   (Bucket)          │
└─────────────────────┘
          │  returns public URL
          ▼
     User gets link
```

**Flow:**
1. User opens your Cloud Run URL → sees upload form
2. User picks a file → clicks Upload
3. Cloud Run receives the file → saves it to Cloud Storage bucket
4. Cloud Storage returns a public URL
5. User sees the live link to their uploaded file

---

---

## PHASE 1 — CREATE YOUR STORAGE BUCKET
### ⏱ 5 minutes

---

### 📌 Step 1 — Open Cloud Storage

1. In Google Cloud Console, search bar → type `Cloud Storage` → click it
2. Click **"+ Create"**

---

### 📌 Step 2 — Configure the Bucket

| Field | Value |
|-------|-------|
| **Bucket name** | `yourname-uploads-2025` *(must be globally unique — add numbers if taken)* |
| **Location type** | Region |
| **Region** | `asia-south1 (Mumbai)` |
| **Storage class** | Standard |
| **Access control** | **Uncheck** "Enforce public access prevention on this bucket" |
| **Access control model** | Fine-grained |

Click **"Create"** → click **"Confirm"** if prompted

---

### 📌 Step 3 — Note Your Bucket Name

Copy your bucket name somewhere — you'll need it in the code:
```
Example: aditya-uploads-2025
```

---

---

## PHASE 2 — OPEN CLOUD SHELL & WRITE THE APP
### ⏱ 10 minutes

> We use **Cloud Shell** — a free Linux terminal built into Google Cloud Console. No installs needed on your laptop.

---

### 📌 Step 1 — Open Cloud Shell

1. In Google Cloud Console, click the **terminal icon** `>_` in the top-right header bar
2. A terminal will open at the bottom of the page
3. Wait for it to initialize (10–15 seconds)
4. You'll see a prompt like: `student@cloudshell:~ (your-project)$`

---

### 📌 Step 2 — Create Project Folder

In the Cloud Shell terminal, type these commands one by one:

```bash
mkdir upload-app
cd upload-app
```

---

### 📌 Step 3 — Create `package.json`

```bash
cat > package.json << 'EOF'
{
  "name": "gcp-file-uploader",
  "version": "1.0.0",
  "description": "File upload website using Cloud Run + Cloud Storage",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "multer": "^1.4.5-lts.1",
    "@google-cloud/storage": "^7.7.0"
  }
}
EOF
```

---

### 📌 Step 4 — Create `index.js` (The Main App)

```bash
cat > index.js << 'EOF'
const express = require('express');
const multer  = require('multer');
const { Storage } = require('@google-cloud/storage');

const app    = express();
const upload = multer({ storage: multer.memoryStorage(), limits: { fileSize: 10 * 1024 * 1024 } });
const storage = new Storage();
const BUCKET  = process.env.BUCKET_NAME;

/* ── HOME PAGE ── */
app.get('/', (req, res) => {
  res.send(`<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>☁️ GCP File Uploader</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background: linear-gradient(135deg, #e8f0fe 0%, #d2e3fc 100%);
      min-height: 100vh;
      display: flex; align-items: center; justify-content: center;
    }
    .card {
      background: white; border-radius: 16px;
      padding: 40px; max-width: 500px; width: 90%;
      box-shadow: 0 4px 24px rgba(66,133,244,0.15);
      text-align: center;
    }
    .logo { font-size: 48px; margin-bottom: 12px; }
    h1 { color: #1a73e8; font-size: 24px; margin-bottom: 8px; }
    p  { color: #5f6368; margin-bottom: 28px; font-size: 14px; }
    .drop-zone {
      border: 2px dashed #4285f4;
      border-radius: 12px; padding: 32px;
      margin-bottom: 20px; cursor: pointer;
      transition: background 0.2s;
    }
    .drop-zone:hover { background: #f0f7ff; }
    .drop-zone input[type=file] { display: none; }
    .drop-zone label { cursor: pointer; color: #4285f4; font-weight: 600; }
    .file-name { color: #3c4043; font-size: 13px; margin-top: 8px; }
    button {
      background: #1a73e8; color: white;
      border: none; border-radius: 8px;
      padding: 14px 32px; font-size: 16px;
      font-weight: 600; cursor: pointer; width: 100%;
      transition: background 0.2s;
    }
    button:hover { background: #1557b0; }
    .note { font-size: 12px; color: #9aa0a6; margin-top: 16px; }
  </style>
</head>
<body>
  <div class="card">
    <div class="logo">☁️</div>
    <h1>GCP File Uploader</h1>
    <p>Upload any file — it gets stored on Google Cloud Storage<br>and you get a permanent public link.</p>
    <form action="/upload" method="POST" enctype="multipart/form-data">
      <div class="drop-zone" onclick="document.getElementById('fileInput').click()">
        <input type="file" id="fileInput" name="file" required
               onchange="document.getElementById('fname').textContent = this.files[0]?.name || ''">
        <label>📁 Click to choose a file</label>
        <div class="file-name" id="fname">No file selected</div>
      </div>
      <button type="submit">⬆️ Upload to Cloud</button>
    </form>
    <p class="note">Max size: 10MB &nbsp;|&nbsp; Hosted on Google Cloud Run + Cloud Storage</p>
  </div>
</body>
</html>`);
});

/* ── UPLOAD HANDLER ── */
app.post('/upload', upload.single('file'), async (req, res) => {
  if (!req.file) return res.status(400).send('No file received.');

  const filename  = `${Date.now()}-${req.file.originalname.replace(/\s+/g, '_')}`;
  const bucket    = storage.bucket(BUCKET);
  const blob      = bucket.file(filename);

  try {
    await blob.save(req.file.buffer, {
      metadata : { contentType: req.file.mimetype },
      public   : true,
    });

    const publicUrl = `https://storage.googleapis.com/${BUCKET}/${filename}`;
    const sizeKB    = (req.file.size / 1024).toFixed(2);

    res.send(`<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>✅ Upload Successful</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Segoe UI', Arial, sans-serif;
      background: linear-gradient(135deg, #e8f5e9 0%, #c8e6c9 100%);
      min-height: 100vh;
      display: flex; align-items: center; justify-content: center;
    }
    .card {
      background: white; border-radius: 16px;
      padding: 40px; max-width: 540px; width: 90%;
      box-shadow: 0 4px 24px rgba(0,0,0,0.1); text-align: center;
    }
    .icon { font-size: 52px; margin-bottom: 12px; }
    h1 { color: #1e8e3e; margin-bottom: 20px; }
    .info { background: #f8f9fa; border-radius: 8px; padding: 20px; text-align: left; margin-bottom: 24px; }
    .info p { margin-bottom: 8px; font-size: 14px; color: #3c4043; }
    .info strong { color: #1a73e8; }
    .url-box {
      background: #e8f0fe; border-radius: 8px; padding: 14px;
      word-break: break-all; font-size: 13px; margin-bottom: 20px;
    }
    .url-box a { color: #1a73e8; text-decoration: none; font-weight: 600; }
    .url-box a:hover { text-decoration: underline; }
    .btn-row { display: flex; gap: 12px; }
    button {
      flex: 1; border: none; border-radius: 8px;
      padding: 12px; font-size: 15px; font-weight: 600;
      cursor: pointer; transition: opacity 0.2s;
    }
    .btn-open { background: #1a73e8; color: white; }
    .btn-back { background: #f1f3f4; color: #3c4043; }
    button:hover { opacity: 0.85; }
  </style>
</head>
<body>
  <div class="card">
    <div class="icon">✅</div>
    <h1>Upload Successful!</h1>
    <div class="info">
      <p>📄 <strong>File:</strong> ${req.file.originalname}</p>
      <p>📦 <strong>Size:</strong> ${sizeKB} KB</p>
      <p>🗂️ <strong>Type:</strong> ${req.file.mimetype}</p>
      <p>🪣 <strong>Bucket:</strong> ${BUCKET}</p>
    </div>
    <p style="font-size:13px;color:#5f6368;margin-bottom:10px;">Your file is now live at:</p>
    <div class="url-box">
      <a href="${publicUrl}" target="_blank">${publicUrl}</a>
    </div>
    <div class="btn-row">
      <button class="btn-open" onclick="window.open('${publicUrl}','_blank')">🔗 Open File</button>
      <button class="btn-back" onclick="location.href='/'">⬆️ Upload Another</button>
    </div>
  </div>
</body>
</html>`);

  } catch (err) {
    console.error('Upload error:', err);
    res.status(500).send(`<h2>❌ Upload failed</h2><pre>${err.message}</pre><a href="/">Try again</a>`);
  }
});

/* ── START SERVER ── */
const PORT = process.env.PORT || 8080;
app.listen(PORT, () => {
  console.log(`✅ Server running on port ${PORT}`);
  console.log(`   Bucket: ${BUCKET}`);
});
EOF
```

---

### 📌 Step 5 — Verify Your Files

```bash
ls -la
```

You should see:
```
index.js
package.json
```

---

---

## PHASE 3 — GRANT PERMISSIONS
### ⏱ 3 minutes

> Cloud Run needs permission to write files into your Cloud Storage bucket. We do this by giving the Cloud Run service account the right IAM role.

---

### 📌 Step 1 — Find Your Project Number

```bash
gcloud projects describe $(gcloud config get-value project) --format="value(projectNumber)"
```

Copy the number shown (e.g. `123456789012`)

---

### 📌 Step 2 — Grant Storage Permission

Run this command — **replace `YOUR-PROJECT-NUMBER` and `YOUR-BUCKET-NAME`**:

```bash
gcloud storage buckets add-iam-policy-binding gs://YOUR-BUCKET-NAME \
  --member="serviceAccount:YOUR-PROJECT-NUMBER-compute@developer.gserviceaccount.com" \
  --role="roles/storage.objectAdmin"
```

**Example** (if project number is `123456789012` and bucket is `aditya-uploads-2025`):
```bash
gcloud storage buckets add-iam-policy-binding gs://aditya-uploads-2025 \
  --member="serviceAccount:123456789012-compute@developer.gserviceaccount.com" \
  --role="roles/storage.objectAdmin"
```

You should see: `Updated IAM policy for bucket [gs://...]`

---

### 📌 What This Does

| Term | Meaning |
|------|---------|
| Service account | The identity Cloud Run uses when talking to other GCP services |
| `roles/storage.objectAdmin` | Permission to read, write, and delete objects in the bucket |
| IAM | Identity & Access Management — GCP's permission system |

---

---

## PHASE 4 — DEPLOY TO CLOUD RUN
### ⏱ 5 minutes

---

### 📌 Step 1 — Install Dependencies & Deploy

Make sure you're inside the `upload-app` folder, then run:

```bash
gcloud run deploy upload-app \
  --source . \
  --region asia-south1 \
  --allow-unauthenticated \
  --set-env-vars BUCKET_NAME=YOUR-BUCKET-NAME
```

**Replace `YOUR-BUCKET-NAME`** with your actual bucket name.

**Example:**
```bash
gcloud run deploy upload-app \
  --source . \
  --region asia-south1 \
  --allow-unauthenticated \
  --set-env-vars BUCKET_NAME=aditya-uploads-2025
```

When asked:
- **"Enable Cloud Build API?"** → type `y` and press Enter
- **"Enable Artifact Registry API?"** → type `y` and press Enter

---

### 📌 Step 2 — Wait for Build & Deploy

The terminal will show progress like:

```
Building using Buildpacks and deploying container to Cloud Run service [upload-app]...
⠹ Building and deploying... Logs are available at [...]
  ✓ Uploading sources
  ✓ Building Container: Logs are piped to [Cloud Build URL]
  ✓ Creating Revision
  ✓ Routing traffic
Done.
Service [upload-app] revision [upload-app-00001-xxx] has been deployed
Service URL: https://upload-app-xxxxxxxxxx-el.a.run.app
```

**Copy the Service URL** — that's your live website.

> ⏳ First deploy takes 2–4 minutes because Google is building your container from source. Subsequent deploys are much faster.

---

### 📌 What `--source .` Does (No Dockerfile Needed!)

When you use `--source .`, Google Cloud Build automatically:

1. Detects your app is Node.js (from `package.json`)
2. Runs `npm install` to install your dependencies
3. Builds a container image
4. Pushes it to Artifact Registry
5. Deploys it to Cloud Run

> 💡 You never wrote a single line of Docker. This is called **Buildpacks** — a technology that auto-containerizes your app.

---

---

## PHASE 5 — TEST YOUR LIVE APP
### ⏱ 5 minutes

---

### 📌 Step 1 — Open Your App

1. Click the **Service URL** from the deploy output
2. You should see a clean upload form with your app

---

### 📌 Step 2 — Upload a File

1. Click **"Click to choose a file"**
2. Select any file from your device (image, PDF, text file)
3. Click **"⬆️ Upload to Cloud"**
4. Wait 2–3 seconds

---

### 📌 Step 3 — Verify the Result

You should see:
- ✅ Upload Successful page
- The **file name, size, and type**
- A **public URL** like `https://storage.googleapis.com/aditya-uploads-2025/1705123456-photo.jpg`
- A **"🔗 Open File"** button

Click **"Open File"** — your file opens directly from **Google Cloud Storage**. ✅

---

### 📌 Step 4 — Verify in Cloud Storage Console

1. Go to Cloud Storage in the console
2. Click your bucket
3. You should see the uploaded file listed with its name and size
4. Click the file → you'll see its public URL and metadata

---

### 📌 Step 5 — Share With a Friend

1. Copy the public file URL
2. Send it to someone on WhatsApp
3. Ask them to open it on their phone

**It works — because the file is hosted on Google's global CDN, not your laptop.** ✅

---

---

## PHASE 6 — EXPLORE & EXTEND
### ⏱ Optional

---

### 🔍 Check Cloud Run Logs

```bash
gcloud run services logs read upload-app --region asia-south1 --limit 20
```

Or in Console → Cloud Run → `upload-app` → **Logs tab**

You'll see every upload request logged in real time.

---

### 🔍 Check Your Revisions

```bash
gcloud run revisions list --service upload-app --region asia-south1
```

---

### 🔄 Redeploy After a Code Change

If you edit `index.js` and want to push the update:

```bash
gcloud run deploy upload-app \
  --source . \
  --region asia-south1 \
  --allow-unauthenticated \
  --set-env-vars BUCKET_NAME=YOUR-BUCKET-NAME
```

Same command — Cloud Run creates a **new revision** automatically.

---

### 🗑️ Clean Up (When Done)

To avoid any charges after the workshop:

```bash
gcloud run services delete upload-app --region asia-south1
```

And in Cloud Storage, delete the bucket if you no longer need it.

---

---

## 🧠 WHAT YOU BUILT — EXPLAINED

```
index.js
│
├── GET  /           → Serves the HTML upload form
└── POST /upload     → Receives the file from browser
                        → Saves to Cloud Storage using @google-cloud/storage SDK
                        → Returns success page with public URL
```

| Code Part | What it does |
|-----------|-------------|
| `multer` | Handles multipart form data (file uploads) in Node.js |
| `memoryStorage()` | Keeps the file in RAM temporarily instead of writing to disk |
| `storage.bucket(BUCKET)` | Connects to your GCP bucket using the SDK |
| `blob.save(buffer, { public: true })` | Uploads the file buffer and makes it publicly readable |
| `process.env.BUCKET_NAME` | Reads bucket name from environment variable (set during deploy) |
| `process.env.PORT` | Cloud Run always injects the port via this env variable |

---

## 💰 COST BREAKDOWN FOR THIS PROJECT

| Action | Cost |
|--------|------|
| Cloud Run: Build + Deploy | ~$0.005 (Cloud Build has 120 min/day free) |
| Cloud Run: Serving requests | $0.00 (well within 2M free requests) |
| Cloud Storage: Storage | $0.00 (well within 5GB free) |
| Cloud Storage: Upload operations | ~$0.001 per 1000 uploads |
| **Total for this lab** | **< $0.01** |

---

## ⚠️ TROUBLESHOOTING — FILE UPLOAD APP

| Problem | Cause | Fix |
|---------|-------|-----|
| `BUCKET_NAME is undefined` | Env var not set | Re-deploy with `--set-env-vars BUCKET_NAME=your-bucket` |
| `403 Access denied to bucket` | Service account missing permission | Re-run Phase 3 Step 2 with correct project number |
| `Build failed: no start command` | Wrong folder | Make sure `package.json` has `"start": "node index.js"` |
| `Error: getaddrinfo ENOTFOUND` | Can't reach GCS | Check region matches bucket region |
| Upload succeeds but file not public | Bucket has public access prevention | Disable it in bucket settings → Permissions |
| App loads but upload hangs | File too large | Default limit is 10MB — check file size |

---

*🏗️ Project Lab: File Upload Website — Cloud Run + Cloud Storage*
