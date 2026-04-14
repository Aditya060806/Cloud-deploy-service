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
