# Leads Automation – For Freelancers, Startups & Small Businesses

This workflow scans Reddit (or other alert sources) for posts where people are:

- **Asking for help**
- **Looking to hire**
- **Requesting services**

It combines **F5Bot or Google Alerts**, **n8n**, **Gemini LLM**, and **Google Sheets** to turn noisy keyword alerts into **structured leads your business can act on**.

While this repo focuses on terms like *video editing*, *design help*, or *collaborator needed*, you can adapt it for:

- Startup leads and outreach
- Low-code automation help
- Hiring posts (virtual assistant, marketer, dev)
- Local service demand (e.g., slides, Canva, presentation design)

---

## 🔍 What Is F5Bot (or Google Alerts)?

[F5Bot](https://f5bot.com) is a free tool that emails you whenever your chosen keywords appear on Reddit — in posts **or** comments.  
You define keywords like:

- `video editing`
- `startup cofounder`
- `need a designer`
- `capcut help`
- `hire a freelancer`

Alternatively, you can use **Google Alerts** to monitor Reddit, Hacker News, or even forums — and forward those alerts into Gmail.

This workflow uses **Gmail → n8n** to process those alerts and act on them.

---

## 🔥 Why I Built This

Reddit and forums are full of genuine people saying things like:

> "Looking for someone to build a landing page"  
> "Need help creating pitch slides"  
> "Any virtual assistants open for a part-time project?"

But most alerts are filled with:
- Self-promos ("I offer services")
- Deleted users
- Off-topic or meme posts

So I built this to:
- Parse Gmail alerts (F5Bot or Google)
- Extract links (post or comment)
- Pull full content via Reddit API
- Use **LLM (Gemini)** to check **if it’s a real help request**
- Store **only useful leads** in Google Sheets

---

## ⚙️ How It Works

The automation runs entirely inside **n8n (Docker self-hosted)** with custom API credentials.

### 1. Keyword Alerts → Gmail → n8n
- F5Bot / Google Alerts email you about new posts
- Gmail filters them into a label (e.g. `F5BOT`)
- n8n fetches and parses them to extract post URLs

### 2. Post Classification via API
- Uses Reddit `/api/info` to fetch:
  - `title`, `selftext`, `author`, etc.
- Filters out:
  - `[deleted]` or `[removed]` content
  - Empty authors or spam

### 3. Gemini 2.5 LLM Decision
The AI checks post text and responds:

```json
{ "relevant": true } or { "relevant": false }
```

### ✅ Classification Logic

Keeps only relevant posts:

- Someone **asking for help**
- Mentions tools like **Canva, CapCut, Figma**
- Clear intent to **hire**, **collab**, or **request a service**

---

### 📤 4. Store in Google Sheets

Each valid post becomes a row with:

- `url`
- `keyword`
- `author`
- `description` (post content)

---

### 📊 Sample Output

| URL     | Keyword        | Author             | Description                               |
|---------|----------------|--------------------|-------------------------------------------|
| (no link) | video editing   | MilovanGlisic21     | We're hiring short-form editors...         |
| (no link) | capcut editing  | HappyHyperCute       | Looking for a VA to help with Canva...     |

> 🔒 Links are real in production but removed here to avoid tracking/fake redirects

---

### 🧱 Tech Stack

- **n8n** (self-hosted)
- **F5Bot or Google Alerts**
- **Gmail API** (custom OAuth2 credentials)
- **Reddit API** (`/api/info`)
- **Google Gemini 2.5** (for classification)
- **Google Sheets API** (for storage)

---

## 📬 Contact & Customization

Need this customized for your business niche, startup leads, or freelance outreach?

<div align="center">

[![Contact Me](https://img.shields.io/badge/CONTACT_ME-Click%20Here-red?style=for-the-badge)](mailto:purnikparisha@gmail.com)

</div>

---

## ⭐ Support the Project

If you found this useful, please consider giving the repo a star!

> A ⭐ helps others discover it and motivates me to keep improving the workflow.

---

## ⚠️ Desktop Note

If the **"Contact Me"** button doesn’t work:

- Try **right-clicking** (or long-pressing) and select **“Open in new tab”**
- Or make sure your **default mail app** (like Gmail) is configured

Works best on mobile or devices with a mail client set up.
