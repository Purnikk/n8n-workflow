# 🧠 Keyword Lead Monitor – n8n + Gemini

This workflow tracks **high-intent keyword mentions** from platforms like **Reddit** and **Hacker News** via [F5Bot](https://f5bot.com), and converts them into structured leads using **n8n**, **Gmail API**, **Gemini (LLM)**, and **Google Sheets**.

It’s perfect for:

- 🚀 Startup founders looking for users asking about their space  
- 💼 Freelancers monitoring niche demand  
- 🔍 Indie hackers spotting users describing problems you solve

---

## 🧩 Workflow Stages

1. **F5Bot Keyword Alerts** – Monitor Reddit/Hacker News mentions  
2. **Gmail Fetcher** – Pull keyword-alert emails with a specific label  
3. **URL Extraction** – Get clean Reddit post/comment links  
4. **Reddit API Call** – Fetch author, title, and body  
5. **Merge Post Logic** – Choose best description (body > title)  
6. **Relevance Classifier** – Use Gemini to detect valuable signals  
7. **Final Field Output** – Extract author, keyword, description, and URL  
8. **Google Sheet Logging** – Deduplicated lead archive

---

## 📷 Screenshots + Explanations

---

### 1️⃣ Full Workflow Overview

![Workflow](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/keyword-leads/screenshots/01-Work-flow.png)

Shows the complete n8n pipeline — from Gmail fetch, parsing and Gemini LLM, to final output in Sheets. A modular, readable, and production-grade automation.

---

### 2️⃣ F5Bot Email Label (Gmail)

![Label](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/keyword-leads/screenshots/02-label-mail.png)

Once F5Bot is configured with your keywords, emails start coming in like:

- "Keyword: `notion` found in Reddit comment…"  
- "Keyword: `freelance` found in Hacker News thread…"

✅ In Gmail:
- Create a **label** like `keyword-leads`  
- Use a filter rule:  
  - If `From: alert@f5bot.com`  
  - Apply label `keyword-leads`

This makes your n8n flow focus only on relevant alerts.

---

### 3️⃣ Gmail Node – n8n Fetch

![Gmail](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/keyword-leads/screenshots/03-mail-node.png)

Pulls recent labeled mails (F5Bot alerts) via OAuth Gmail API.

- Use the `Get Many` toggle to pull multiple threads  
- Filters by label (`keyword-leads`)  
- These mails contain:
  - Keywords  
  - Snippets  
  - Multiple redirect links (some irrelevant)

---

### 4️⃣ API Metadata Fetch

![API](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/keyword-leads/screenshots/04-api.png)

We extract clean **Reddit links** from the HTML and fetch the **post metadata** using Reddit API.

- Inputs:
  - Extracted `post_id` or `comment_id`
- Output includes:
  - `title`  
  - `selftext`  
  - `author`  
  - Other meta fields (`children`, etc.)

This gives **structured data** beyond what F5Bot email provides.

---

### 5️⃣ Merge Logic – Body or Title

![Merge](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/keyword-leads/screenshots/05-merge.png)

Not all Reddit posts have body text. This logic ensures:

- If `selftext` exists → use as `description`  
- Else, fallback to `title`  
- Posts with no useful text are skipped

💡 This merged field becomes **input to Gemini LLM** for filtering.

---

### 6️⃣ Gemini LLM Classifier

![Gemini](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/keyword-leads/screenshots/06-agent.png)

This block determines **whether the post is contextually relevant**.

Gemini looks at the merged description and answers:

```json
{
  "relevant": "yes"
}
```

It flags content like:

- 🧠 "Looking for time tracking tools"  
- 💬 "Can someone recommend X?"  
- 😭 "I'm struggling with Notion or Zapier"  

…and ignores:

- 😐 Off-topic remarks  
- 🙈 Joke/meme replies  
- 💸 Self-promos or junk links

---

### 7️⃣ Field Collector (Set Node)

![Set](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/keyword-leads/screenshots/07-collect-fields.png)

For every relevant post:

- `reddit_url`  
- `keyword` matched  
- `description` (body or title)  
- `author`  
are compiled into a final lead object.

You can customize this further if you want extra fields like subreddit or flair.

---

### 8️⃣ Google Sheets Output

![Sheets](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/keyword-leads/screenshots/08-g-sheets.png)

Each qualified lead becomes a **row in Google Sheets**.

✅ Features:

- One row per post  
- `url` is used for **deduplication**  
- Sheet becomes your CRM-lite system for:
  - Outreach  
  - Trend analysis  
  - Tagging leads  

---

## ⚙️ Filter Logic

To avoid junk and save LLM credits:

- ❌ Emails without Reddit links are dropped  
- ✅ Only Reddit posts (not ads or nav links) are parsed  
- ✅ Author must not be `[deleted]`  
- ✅ Posts must have some useful context (body/title)  

This ensures high-signal, low-noise results.

---

## 📊 Ideal Use Cases

- 🧠 **Solopreneurs** — Spot people asking for what you built  
- 💼 **Agencies** — Monitor leads for services like design/dev/AI  
- 🧪 **Startups** — Product discovery, early demand mapping  
- 🔍 **Researchers** — Track topic mentions across Reddit/HN

---

## ❓ FAQs

### Can this work for Hacker News too?
Yes — [F5Bot](https://f5bot.com) supports Hacker News. The email format is similar and works seamlessly.

### Can I run this hourly?
Yes. You can add a Cron node or trigger this flow using webhook or schedule.

### Can I use Outlook instead of Gmail?
If you can fetch email with label/filter or via IMAP/OAuth, yes — but Gmail is easiest in n8n.

### Are duplicates prevented?
Yes. Google Sheets node uses the Reddit `url` as a **match column**, so no repeated entries.

### How many emails can I fetch?
Gmail API supports batching. Use the "Get Many" toggle in n8n to pull multiple mails at once.

---

## 🛠️ Get Started

1. 🔍 Add keywords at [F5Bot.com](https://f5bot.com)  
2. 📥 Wait for alert emails  
3. 🏷️ Set Gmail filter → label = `keyword-leads`  
4. 🔄 Run your n8n flow (manual or scheduled)  
5. 📄 Log qualified leads in Google Sheets

---

## 🌟 Support This Project

If this automation helped you find useful leads or save time, **give the repo a star**:

[⭐ Star the GitHub Repo](https://github.com/Purnikk/n8n-workflow)

---

## 📬 Contact for Customization

Want this workflow extended to outbound DM, Airtable, CRMs, or Discord?

[![Email](https://img.shields.io/badge/Email-Contact_Me-red?style=for-the-badge&logo=gmail&logoColor=white)](mailto:purnikparisha@gmail.com)
