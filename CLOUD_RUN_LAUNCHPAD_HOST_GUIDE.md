# ☁️ CLOUD RUN LAUNCHPAD
## HOST GUIDE – STEP 3 ONWARD (DETAILED LIVE EXECUTION)

---

## 📋 SESSION OVERVIEW

| Step | Activity | Time |
|------|----------|------|
| Step 3 | Cloud Run Setup | 1:35 – 1:45 |
| Step 4 | Create Cloud Run Service | 1:45 – 1:50 |
| Step 5 | Container Image Setup | 1:50 – 1:55 |
| Step 6 | Configure Basic Settings | 1:55 – 2:00 |
| Step 7 | Public Access Settings | 2:00 – 2:05 |
| Step 8 | Deploy Application | 2:05 – 2:10 |
| Step 9 | Access Live URL | 2:10 – 2:15 |
| Step 10 | Test Live Deployment | 2:15 – 2:20 |
| Step 11 | Open Logs | 2:20 – 2:25 |
| Step 12 | Generate Live Logs | 2:25 – 2:30 |
| Step 13 | Redeploy / Update | 2:30 – 2:40 |
| Step 14 | Cloud Challenge / Competition | 2:40 – 2:55 |
| Step 15 | Closing | 2:55 – 3:00 |

---

---

# STEP 3 – CLOUD RUN SETUP
### ⏱ Time: 1:35 – 1:45

---

## 🎤 Opening Line

> "Now that everyone has their billing/project ready, we're moving to the most exciting part—actually deploying your application."

*[Pause 2 seconds]*

> "From this point onward, you're going to work like real cloud engineers."

---

## ✅ Student Action

1. Go to the **top search bar** in Google Cloud Console
2. Type: **Cloud Run**
3. Click on the **Cloud Run service**

---

## 📖 Concept Explanation

**What is Cloud Run?**

> "Cloud Run is Google's serverless deployment platform."

Break it down point by point:

- "Normally if you want to host an app, you need servers."
- "Servers require setup, maintenance, updates, monitoring."
- "Cloud Run removes all of that."
- "You just give Google your application, and Google runs it for you."

---

## 💡 Analogy

> "Think of Cloud Run like **Uber for servers** — you don't own the car/server, you just use it when needed."

---

## 🙋 Crowd Check

> "Everyone on Cloud Run dashboard? Raise your hand."

⚠️ **Wait. Do NOT proceed until 80–90% of students are ready.**

---

---

# STEP 4 – CREATE CLOUD RUN SERVICE
### ⏱ Time: 1:45 – 1:50

---

## 🎤 What You Say

> "Now we're going to create your first deployed cloud service."

---

## ✅ Student Action

1. Click **Create Service**

---

## 📖 Concept Explanation

- "A **service** means your deployed application."
- "Whenever users open your website/app, they are interacting with your service."

---

## 🔥 Hype Line

> "You are not just clicking buttons — you're literally preparing infrastructure."

---

---

# STEP 5 – CONTAINER IMAGE SETUP
### ⏱ Time: 1:50 – 1:55

---

## ✅ Student Action

Under **Deployment Source**, choose:

> ✅ **Deploy one revision from an existing container image**

Paste the following image URL:

```
gcr.io/cloudrun/hello
```

---

## 📖 Concept Explanation

**What is this image?**

> "This is a pre-built application made by Google."
> "This app is packaged in something called a **container**."

**What is a container?**

> "A container is like a zipped package containing:
> - Code
> - Libraries
> - Dependencies
> - Runtime"

> "It ensures your app runs the same everywhere."

---

## 💡 Analogy

> "Like carrying your **entire kitchen** with you so food can be made anywhere."

---

---

# STEP 6 – CONFIGURE BASIC SETTINGS
### ⏱ Time: 1:55 – 2:00

---

## ✅ Student Action

Configure the following fields:

### Service Name
```
hello-service
```

### Region
```
asia-south1  (Mumbai)
```

---

## 📖 Concept Explanation

**Service Name:**
> "This is simply the identity of your deployed app."

**Region:**
> "This decides **where physically** your app runs."
> "If you choose Mumbai, your app runs in Google's Mumbai datacenter."

---

## 🙋 Engagement Question

> "Why should Indian users choose Mumbai instead of US?"

*[Wait for student responses, then explain:]*

**Answer:** **Latency** — data travels a shorter distance, so the app loads faster for Indian users.

---

---

# STEP 7 – PUBLIC ACCESS SETTINGS
### ⏱ Time: 2:00 – 2:05

---

## ✅ Student Action

Enable:

> ✅ **Allow unauthenticated invocations**

---

## 📖 Concept Explanation

- "By default, Google keeps deployments **private** for security."
- "But today we want everyone to access your app."
- "So we make it **public**."

---

## 🔎 Clarification

> "This means anyone with your link can open it."

---

---

# STEP 8 – DEPLOY APPLICATION
### ⏱ Time: 2:05 – 2:10

---

## ✅ Student Action

Click:

> 🚀 **Deploy**

---

## 📖 While It Loads — Explain What's Happening

> "What Google is doing right now:"

- Creating compute resources
- Setting up networking
- Allocating memory / CPU
- Launching your container
- Exposing a public endpoint

---

## 🔥 VERY IMPORTANT MOMENT — Build the Hype

> "This is **EXACTLY** what happens in real companies when engineers deploy apps."

---

---

# STEP 9 – ACCESS LIVE URL
### ⏱ Time: 2:10 – 2:15

---

## ✅ Student Action

Once deployment is complete:

1. Click the **generated URL** shown in the Cloud Run dashboard

---

## 🎤 What You Say

> "Congratulations — your application is now **LIVE on the internet.**"

*[Pause. Let that sink in.]*

---

## 🔥 Hype Line

> "Anyone in the world with this link can access what you just built."

---

---

# STEP 10 – TEST LIVE DEPLOYMENT
### ⏱ Time: 2:15 – 2:20

---

## ✅ Student Action

1. Refresh the deployed page **5 times**
2. Open it on your **phone**
3. **Share the link** with a friend

---

## 📖 Concept Explanation

> "This proves your app is:
> - Hosted publicly
> - Globally accessible
> - Running on cloud infrastructure"

---

---

# STEP 11 – OPEN LOGS
### ⏱ Time: 2:20 – 2:25

---

## ✅ Student Action

1. Go back to the **Cloud Run dashboard**
2. Click the **Logs** tab

---

## 📖 Concept Explanation

> "Logs record **everything happening** in your application."

Examples of what logs capture:
- User visits
- Errors
- Crashes
- Backend activity

---

## 💡 Analogy

> "Logs are **CCTV footage** for your app."

---

---

# STEP 12 – GENERATE LIVE LOGS
### ⏱ Time: 2:25 – 2:30

---

## ✅ Student Action

1. Refresh the deployed page **5–10 times**
2. Return to the **Logs tab**
3. Watch new entries appear in real time

---

## 📖 Concept Explanation

> "Every request creates a log entry."
> "This is how engineers **debug and monitor** apps in production."

---

---

# STEP 13 – REDEPLOY / UPDATE
### ⏱ Time: 2:30 – 2:40

---

## ✅ Student Action

Click:

> **Edit & Deploy New Revision**

Make a change to **any one** of the following:
- Service name
- Region
- Scaling settings

---

## 📖 Concept Explanation

- "When developers improve apps, they don't rebuild everything."
- "They deploy **updated revisions**."

---

## 🔑 Key Concept: Revisions

> "Every deployment creates a **new version** (revision) of your app."
> "This allows rollback, traffic splitting, and safe updates."

---

---

# STEP 14 – CLOUD CHALLENGE / COMPETITION
### ⏱ Time: 2:40 – 2:55

---

## 🎤 Announcement

> "Now let's see who became cloud engineers fastest."

---

## 🏆 Challenge Tasks

Complete **any 3** of the following:

| # | Task |
|---|------|
| 1 | Deploy in another region |
| 2 | Generate 20 log entries |
| 3 | Redeploy successfully with a new revision |
| 4 | Help a teammate finish their deployment |

---

## 🎁 Reward

> Top performers win **stickers** 🏅

---

---

# STEP 15 – CLOSING
### ⏱ Time: 2:55 – 3:00

---

## 🙋 Reflection Questions

Ask the audience:

1. "What did you **learn** today?"
2. "Was cloud **easier** than expected?"
3. "What **surprised** you?"

*[Take 2–3 responses from students]*

---

## 🎤 Final Line

> "Today you deployed your **first real cloud-hosted application.**"

*[Pause]*

> "You've officially taken your **first step into cloud engineering.**"

---

---

## 📌 HOST QUICK REFERENCE CARD

| Step | Key Action | Key Concept | Analogy |
|------|-----------|-------------|---------|
| 3 | Search Cloud Run | Serverless platform | Uber for servers |
| 4 | Create Service | Service = deployed app | — |
| 5 | Paste container image | Container = packaged app | Kitchen you carry |
| 6 | Set name & region | Latency & geography | — |
| 7 | Allow unauthenticated | Public vs private access | — |
| 8 | Deploy | Infrastructure provisioning | Real company deploy |
| 9 | Open live URL | App is live on internet | — |
| 10 | Test on phone & share | Global accessibility | — |
| 11 | Open Logs tab | Observability | CCTV for your app |
| 12 | Refresh & watch logs | Monitoring & debugging | — |
| 13 | Edit & redeploy | Revisions & updates | — |
| 14 | Challenge tasks | Practice & competition | — |
| 15 | Reflection & close | Celebrate achievement | — |

---

## ⚠️ COMMON ISSUES & FIXES

| Issue | Fix |
|-------|-----|
| Student can't find Cloud Run | Guide: Search bar → type "Cloud Run" → click first result |
| Deployment stuck / failing | Check container image URL is exactly `gcr.io/cloudrun/hello` |
| URL shows error after deploy | Wait 30–60 seconds and refresh; container may still be starting |
| Logs tab empty | Refresh the deployed app URL first, then return to logs |
| "Permission denied" on deploy | Ensure billing is enabled and correct project is selected |
| Can't enable unauthenticated | Check IAM permissions; may need to grant `allUsers` role manually |

---

*Guide prepared for Cloud Run Launchpad Workshop — Step 3 to 15*
