# ☁️ CLOUD RUN LAUNCHPAD
### 🎓 Student Step-by-Step Deployment Guide

> Follow every step carefully. By the end, your app will be **live on the internet** — accessible by anyone in the world.

---

## 📋 What You Will Do Today

| Step | Activity | Time |
|------|----------|------|
| Step 3 | Open Cloud Run | 1:35 – 1:45 |
| Step 4 | Create a Cloud Run Service | 1:45 – 1:50 |
| Step 5 | Set Up Your Container Image | 1:50 – 1:55 |
| Step 6 | Configure Name & Region | 1:55 – 2:00 |
| Step 7 | Make Your App Public | 2:00 – 2:05 |
| Step 8 | Deploy Your App | 2:05 – 2:10 |
| Step 9 | Open Your Live URL | 2:10 – 2:15 |
| Step 10 | Test Your Deployment | 2:15 – 2:20 |
| Step 11 | View Logs | 2:20 – 2:25 |
| Step 12 | Generate Live Logs | 2:25 – 2:30 |
| Step 13 | Redeploy / Update Your App | 2:30 – 2:40 |
| Step 14 | Cloud Challenge | 2:40 – 2:55 |
| Step 15 | Wrap Up | 2:55 – 3:00 |

---

---

# STEP 3 – OPEN CLOUD RUN
### ⏱ 1:35 – 1:45

### 📌 What to Do

1. Open **[console.cloud.google.com](https://console.cloud.google.com)** in your browser
2. Make sure you are signed in with your **Google account**
3. Make sure your **project** is selected in the top bar (you should see a project name next to "Google Cloud")
4. Click the **search bar** at the very top of the page
5. Type: `Cloud Run`
6. Click on **Cloud Run** from the dropdown results
7. You should now see the **Cloud Run dashboard**

### 🧠 What is Cloud Run?

Cloud Run is Google's **serverless** deployment platform. That means:

- You do **not** need to set up any server
- You do **not** need to install anything
- You just hand Google your application → Google runs it for you automatically
- You only pay when your app is actually being used

> 💡 **Think of it like Uber for servers** — you don't own a car, you just request a ride when you need it. Same idea: you don't own a server, you just use Google's when needed.

---

---

# STEP 4 – CREATE A CLOUD RUN SERVICE
### ⏱ 1:45 – 1:50

### 📌 What to Do

1. On the Cloud Run dashboard, click the **"+ Create Service"** button at the top
2. A new configuration page will open

### 🧠 What is a "Service"?

In Cloud Run, a **service** = your deployed app.

- Every time someone visits your website or app URL, they are hitting your **Cloud Run service**
- The service is always running, always ready to respond
- You are not just clicking buttons — you are **setting up real cloud infrastructure**

---

---

# STEP 5 – SET UP YOUR CONTAINER IMAGE
### ⏱ 1:50 – 1:55

### 📌 What to Do

1. On the Create Service page, look for the **"Deployment"** section at the top
2. Select the option:
   > ✅ **Deploy one revision from an existing container image**
3. In the **Container image URL** field, paste exactly this:

```
gcr.io/cloudrun/hello
```

4. Press **Tab** or click elsewhere to confirm it

### 🧠 What is a Container Image?

A **container** is a packaged version of your app that includes:

| What's inside | Why it matters |
|---------------|----------------|
| Your code | The actual application logic |
| Libraries | Tools your code needs to run |
| Dependencies | Packages the app depends on |
| Runtime | The environment (e.g. Node.js, Python) |

> 💡 **Think of it like carrying your entire kitchen with you** — no matter where you go, you can cook the same food. A container ensures your app runs exactly the same everywhere.

The image `gcr.io/cloudrun/hello` is a **ready-made demo app** built by Google — perfect for your first deployment.

---

---

# STEP 6 – CONFIGURE NAME & REGION
### ⏱ 1:55 – 2:00

### 📌 What to Do

Scroll down to find the following fields and fill them in:

#### 1. Service Name
```
hello-service
```
> Type this exactly, no spaces. You can also use your own name like `my-first-app`

#### 2. Region
From the dropdown, select:
```
asia-south1 (Mumbai)
```

### 🧠 Why Does This Matter?

**Service Name** — This is the unique identity of your app in Google Cloud. Other services and tools use this name to reference your deployment.

**Region** — This is the **physical location** of Google's datacenter where your app will run.

- `asia-south1` = Mumbai, India
- If Indian users access your app and it's hosted in Mumbai, the data travels a **short distance** → your app loads **faster**
- If you chose `us-central1`, data travels halfway around the world → **slower for Indian users**

> 💡 This concept is called **Latency** — the time it takes for data to travel from server to user. Closer server = lower latency = faster app.

---

---

# STEP 7 – MAKE YOUR APP PUBLIC
### ⏱ 2:00 – 2:05

### 📌 What to Do

1. Scroll down to find the **"Authentication"** section
2. Select:
   > ✅ **Allow unauthenticated invocations**
3. Make sure this option is checked/selected

### 🧠 Why Do We Need to Do This?

By default, Google Cloud **blocks public access** to all new deployments for security reasons. Only you (the owner) can access it.

But since we want our app to be publicly accessible to anyone with the link, we must **explicitly allow it**.

> ⚠️ In real company apps, you would keep this private and require login tokens (called **Bearer tokens** or **OAuth**). For today's demo, we make it public.

---

---

# STEP 8 – DEPLOY YOUR APP
### ⏱ 2:05 – 2:10

### 📌 What to Do

1. Scroll to the bottom of the page
2. Review your settings one last time:
   - Container image: `gcr.io/cloudrun/hello` ✅
   - Service name: `hello-service` ✅
   - Region: `asia-south1` ✅
   - Authentication: Allow unauthenticated ✅
3. Click the **"Create"** / **"Deploy"** button
4. Wait — a loading spinner will appear. **Do not close the tab.**

### 🧠 What is Google Doing Right Now?

While you wait, here is exactly what is happening behind the scenes:

| What Google is doing | What it means |
|----------------------|---------------|
| Pulling container image | Downloading your app package |
| Allocating CPU & Memory | Reserving compute power for your app |
| Setting up networking | Creating a route so the internet can reach your app |
| Launching the container | Starting your app inside Google's datacenter |
| Assigning a public URL | Giving your app a permanent web address |

> This entire process takes **30–90 seconds**. In real companies, this same process is triggered automatically every time a developer pushes new code.

### ✅ How to Know It's Done

A **green checkmark** ✅ will appear next to your service name. You will also see a **blue URL** appear at the top of the service details page.

---

---

# STEP 9 – OPEN YOUR LIVE URL
### ⏱ 2:10 – 2:15

### 📌 What to Do

1. Once the green checkmark appears, look at the top of the service page
2. You will see a URL like:
   ```
   https://hello-service-xxxxxxxxxx-el.a.run.app
   ```
3. **Click that URL**
4. A new tab will open — you will see your live deployed app

### 🎉 Congratulations — Your App is LIVE

You just deployed a real application to the internet. This URL is:

- **Permanent** — it won't disappear
- **Public** — anyone with the link can open it
- **Globally accessible** — someone in Japan, USA, or Brazil can open it right now
- **Hosted on Google's infrastructure** — not your laptop, not a USB drive — Google's actual servers

> Copy your URL and save it somewhere. You'll need it in the next steps.

---

---

# STEP 10 – TEST YOUR DEPLOYMENT
### ⏱ 2:15 – 2:20

### 📌 What to Do

1. **On your laptop:** Refresh your deployed app page **5 times**
2. **On your phone:** Open a browser → paste your URL → hit enter
3. **Share it:** Send your URL to a friend on WhatsApp or any chat app
4. Ask them to open it — it should work on their device too

### 🧠 What This Proves

| Test | What it confirms |
|------|-----------------|
| Refreshing multiple times | App is stable and always responds |
| Opening on phone | App is accessible on any device |
| Friend opens it | App is publicly reachable from any network |

> Your app is not running on your computer. It's running on Google's servers in Mumbai. **Your laptop can be off and the app will still work.**

---

---

# STEP 11 – VIEW YOUR APP LOGS
### ⏱ 2:20 – 2:25

### 📌 What to Do

1. Go back to the **Cloud Run dashboard** (use your browser's back button or navigate to Cloud Run)
2. Click on your service name: **hello-service**
3. At the top of the service detail page, click the **"Logs"** tab
4. You should see a list of log entries — these are **real-time records** of every request your app received

### 🧠 What are Logs?

Logs are **records of everything that happens** in your application:

- Every time someone visits your app → **a log entry is created**
- Errors and crashes → **logged automatically**
- Backend processing → **logged**
- Security events → **logged**

> 💡 **Think of logs like CCTV footage for your app.** Just like a security camera records everyone who enters a building, logs record every request that reaches your app.

**Columns you'll see in the log:**

| Column | What it means |
|--------|---------------|
| Timestamp | Exact time the request happened |
| Severity | INFO, WARNING, ERROR |
| HTTP Method | GET, POST, etc. |
| Status | 200 = success, 404 = not found, 500 = server error |
| Latency | How long the request took to complete |

---

---

# STEP 12 – GENERATE LIVE LOGS
### ⏱ 2:25 – 2:30

### 📌 What to Do

1. Open your deployed app URL in a new tab
2. **Refresh it 5–10 times rapidly**
3. Switch back to the **Logs tab** in Cloud Run
4. Watch new log entries appear **in real time**
5. Click on any log entry to expand it and see full details

### 🧠 What You're Seeing

Every refresh = 1 HTTP GET request = 1 log entry.

This is exactly how real engineers monitor production applications:

- **Check if users are actually visiting** → look at log volume
- **Debug why something broke** → filter logs by ERROR severity
- **Measure performance** → look at latency values in logs
- **Track suspicious activity** → look for unusual request patterns

> In real companies, logs are fed into tools like **Google Cloud Logging**, **Datadog**, or **Splunk** for advanced analysis.

---

---

# STEP 13 – REDEPLOY / UPDATE YOUR APP
### ⏱ 2:30 – 2:40

### 📌 What to Do

1. From the service detail page, click **"Edit & Deploy New Revision"** at the top
2. You will see the same configuration form as before
3. Make **one of the following changes**:

   **Option A — Change the container:**
   > Leave image as is (we don't have a new one yet — that's for a future session)

   **Option B — Change scaling settings:**
   > Scroll down → find **"Capacity"** → change **"Maximum number of instances"** from default to `3`

   **Option C — Add an environment variable:**
   > Scroll to **"Container"** tab → find **"Environment Variables"** → click **"+ Add Variable"**
   > - Name: `APP_ENV`
   > - Value: `production`

4. Click **"Deploy"**
5. Wait for the new revision to deploy (green checkmark)

### 🧠 What is a Revision?

Every time you click Deploy, Cloud Run creates a **new revision** — a versioned snapshot of your app.

| Revision | What changed |
|----------|-------------|
| Revision 1 | Original deployment |
| Revision 2 | Your update just now |

**Why revisions are powerful:**

- **Rollback** — If revision 2 breaks things, you can instantly switch back to revision 1
- **Traffic splitting** — You can send 90% of users to revision 1 and 10% to revision 2 (A/B testing)
- **Zero downtime updates** — New revision starts before old one stops

> This is called a **Blue-Green Deployment** strategy — used by companies like Google, Netflix, Amazon.

---

---

# STEP 14 – CLOUD CHALLENGE
### ⏱ 2:40 – 2:55

### 🏆 Your Mission

Complete **any 3** of the tasks below. First to finish all 4 wins.

| # | Task | How to do it |
|---|------|-------------|
| 1 | **Deploy in a different region** | Edit & Deploy New Revision → change Region to `us-central1` |
| 2 | **Generate 20 log entries** | Refresh your app URL 20+ times → check Logs tab |
| 3 | **Redeploy successfully** | Make any change → Deploy → wait for green checkmark on Revision 2+ |
| 4 | **Help a teammate** | Walk someone through their deployment until their URL is live |

### 🎁 Reward

Top performers win **stickers** 🏅

> 📸 Screenshot your deployed app URL and the green checkmark as proof!

---

---

# STEP 15 – WRAP UP
### ⏱ 2:55 – 3:00

### 🎓 What You Accomplished Today

| What you did | What it means in the real world |
|---|---|
| Deployed a container to Cloud Run | Shipped an application to production |
| Configured region & service settings | Set up cloud infrastructure |
| Made it publicly accessible | Configured network security policies |
| Viewed and generated logs | Monitored a live production system |
| Deployed a new revision | Performed a zero-downtime update |

### 🚀 What's Next?

Now that you know how to deploy to Cloud Run, here's what real engineers do next:

1. **Build their own app** — instead of `gcr.io/cloudrun/hello`, they push their own Docker image
2. **Connect a custom domain** — instead of `*.run.app`, they use their own domain like `myapp.com`
3. **Set up CI/CD pipelines** — auto-deploy on every git push using GitHub Actions or Cloud Build
4. **Add monitoring & alerts** — get notified when error rates spike

### 🔗 Useful Links

| Resource | Link |
|----------|------|
| Cloud Run Docs | https://cloud.google.com/run/docs |
| Cloud Run Quickstart | https://cloud.google.com/run/docs/quickstarts |
| Docker & Containers | https://docs.docker.com/get-started/ |
| Google Cloud Free Tier | https://cloud.google.com/free |

---

---

## ⚠️ COMMON ISSUES & FIXES

| Problem | Solution |
|---------|----------|
| Can't find Cloud Run | Go to search bar at top → type `Cloud Run` → click first result |
| Container image URL not accepted | Make sure you paste exactly: `gcr.io/cloudrun/hello` (no spaces, no quotes) |
| Deployment stuck for more than 3 minutes | Refresh the page — if still stuck, delete and recreate the service |
| URL opens but shows error | Wait 30–60 seconds and try again — container may still be warming up |
| Logs tab is empty | First visit your app URL a few times, then return to logs |
| "Permission denied" error | Make sure billing is enabled on your project and you're in the right project |
| Can't enable unauthenticated invocations | Your org policy may block it — ask the host for help |

---

*☁️ Cloud Run Launchpad — Student Guide | Steps 3 to 15*
