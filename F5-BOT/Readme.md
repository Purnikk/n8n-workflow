# Reddit Freelance Leads – Video Editing, Design & Creative Help

This workflow scans Reddit for posts where people are **looking to hire or collaborate** with freelance editors, designers, and other creatives. It uses **F5Bot**, **n8n**, **LLMs (Gemini)**, and **Google Sheets** to turn noisy Reddit alerts into **structured, outreach-ready leads**.

---

## 🛰️ What Is F5Bot?

[F5Bot](https://f5bot.com) is a free Reddit keyword alert service that emails you when specific terms show up in Reddit posts or comments.

You define keywords like:
- `video editing`
- `capcut help`
- `need a designer`
- `thumbnail feedback`
- `hire a freelancer`

F5Bot watches Reddit and emails you whenever one of those appears.  
In this workflow, I’ve used it to track terms related to **video editing, graphic design, slides, logos, posters, etc.**

---

## 🔥 Why I Built This

Reddit has real people saying things like:

> "Looking for someone to edit my YouTube videos"  
> "Need help creating a logo or presentation"  
> "Any video editors open for a revenue share collab?"

But most posts are:
- Self-promos ("I can edit your videos!")
- Dead (deleted authors, removed posts)
- Feedback threads or memes

So I built this to:
- Parse F5Bot email alerts via Gmail
- Extract Reddit post links (post or comment)
- Pull full Reddit content via API
- Use a Gemini LLM to check if the post is a **genuine freelance request**
- Store valid ones in a Google Sheet for follow-up

---

## ⚙️ How It Works

This system runs inside **n8n (Docker self-hosted)** and combines Gmail, Reddit API, LLM classification, and Sheets:

### 1. F5Bot → Gmail → n8n
- F5Bot sends alerts to Gmail (label: `F5BOT`)
- n8n fetches emails from this label
- Extracts all Reddit links from the email HTML (handles posts & comments)

### 2. Reddit Metadata Extraction
- Uses Reddit API `/api/info` to fetch:
  - `title`, `selftext`, `author`, etc.
- Discards:
  - `[deleted]` authors
  - `[removed]` or empty text

### 3. Classify Using Gemini
- Sends text to **Google Gemini 2.5**
- Response is either:
  ```json
  { "relevant": true } or { "relevant": false }
### ✅ Classification Logic

Keeps only relevant posts:

- People **asking for help**
- Mentioning tools like **CapCut, Canva, Premiere**
- Showing clear **intent to hire**

---

### 📤 4. Store in Google Sheets

Adds a row for each valid lead with:

- `url`
- `keyword`
- `author`
- `description`

---

### 📊 Sample Output

| URL              | Keyword        | Author           | Description                                       |
|------------------|----------------|------------------|---------------------------------------------------|
| [View Post](https://...) | video editing   | MilovanGlisic21   | We're a video agency hiring short-form editors... |
| [View Post](https://...) | capcut editing  | HappyHyperCute     | Looking for a VA to help with CapCut & Canva...   |

---

### 🧱 Tech Stack

- **n8n** (Docker self-hosted)
- **F5Bot** (Reddit keyword alerting)
- **Gmail API** (custom OAuth2 app)
- **Reddit API** (`/api/info`)
- **Google Gemini 2.5** (classification model)
- **Google Sheets API** (final storage)

---

## 📬 Contact & Customization

Need this customized for your business niche, startup leads, or freelance outreach?

<div align="center">

[![Email](https://img.shields.io/badge/email-purnikparisha@gmail.com-blue?style=for-the-badge&logo=gmail)](mailto:purnikparisha@gmail.com)
&nbsp;
[![Contact Me](https://img.shields.io/badge/CONTACT_ME-red?style=for-the-badge)](mailto:purnikparisha@gmail.com)

</div>

---

## ⭐ Support the Project

If you found this useful, please consider giving the repo a star!

> A ⭐ helps others discover it and motivates me to keep improving the workflow.

---

## ⚠️ Desktop Note

If the **"Contact Me"** button doesn’t work:

- Try **right-clicking** (or long-press on mobile) and choosing **“Open in new tab”**
- Or make sure your **default email app** (like Gmail) is properly configured

This works best on mobile or systems with a mail client set up.

