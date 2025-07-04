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

## 📷 Screenshots + Descriptions

---

### 1️⃣ Full Workflow Overview

![Workflow](https://github.com/Purnikk/n8n-workflow/blob/main/F5-BOT/Screenshots/01-Work-flow.png?raw=true)

This is the full n8n pipeline showing all the steps from Gmail fetch to Gemini LLM filtering and Google Sheets output. It’s clean, logical, and modular.

---

### 2️⃣ F5Bot Email Label (Gmail)

![Label](https://github.com/Purnikk/n8n-workflow/blob/main/F5-BOT/Screenshots/02-label-mail.png?raw=true)

Once [F5Bot](https://f5bot.com) is set up with keywords like `Notion`, `freelance`, `time tracking`, etc., it emails you whenever these terms show up.

✅ In Gmail:
- Create a filter for `From: alert@f5bot.com`  
- Apply the label `keyword-leads`  
This label will be used in the Gmail node inside n8n.

---

### 3️⃣ Gmail Node – n8n Fetch

![Gmail](https://github.com/Purnikk/n8n-workflow/blob/main/F5-BOT/Screenshots/03-mail-node.png?raw=true)

This Gmail node fetches emails labeled `keyword-leads`. It:

- Pulls multiple emails using `Get Many`  
- Extracts content from each F5Bot alert  
- These contain both the keyword trigger + raw links (some ads/redirects)

---

### 4️⃣ API Metadata Fetch

![API](https://github.com/Purnikk/n8n-workflow/blob/main/F5-BOT/Screenshots/04-api.png?raw=true)

Once clean Reddit URLs are extracted, the Reddit API is called using the `post_id` or `comment_id`.  
It returns structured data like:

- `title`  
- `selftext`  
- `author`  
- Nested fields like `children` (comment structure)

---

### 5️⃣ Merge Logic – Body or Title

![Merge](https://github.com/Purnikk/n8n-workflow/blob/main/F5-BOT/Screenshots/05-merge.png?raw=true)

This step ensures useful context for filtering:

- If `selftext` exists → it's used as description  
- Else → fallback to the post `title`  
Some posts only have a title, which may still be valuable.

This merged field is what we send to Gemini next.

---

### 6️⃣ Gemini LLM Classifier

![Gemini](https://github.com/Purnikk/n8n-workflow/blob/main/F5-BOT/Screenshots/06-agent.png?raw=true)

Gemini reviews the merged content and returns:

```json
{
  "relevant": "yes"
}
```

Only relevant leads move forward. This step filters out:

- Spam  
- Low-quality or off-topic posts  
- Link dumps or joke replies

---

### 7️⃣ Field Collector (Set Node)

![Set](https://github.com/Purnikk/n8n-workflow/blob/main/F5-BOT/Screenshots/07-collect-fields.png?raw=true)

Here we create the final lead structure, including:

- `reddit_url`  
- `description`  
- `keyword` (triggered word)  
- `author`

This is what’s logged into the spreadsheet.

---

### 8️⃣ Google Sheets Output

![Sheets](https://github.com/Purnikk/n8n-workflow/blob/main/F5-BOT/Screenshots/08-g-sheets.png?raw=true)

Each relevant lead is saved into Google Sheets.

✅ De-duplication is handled using the `url`  
✅ Sheet becomes a live list of opportunities, questions, or discussions around your niche

---

## ⚙️ Smart Filtering Logic

- Gmail filter limits emails to only F5Bot alerts  
- HTML parsing removes redirect or ad links  
- Reddit API ensures we only process posts by real (not deleted) authors  
- Gemini confirms whether it's worth tracking

---

## 📊 Ideal Use Cases

- 🧠 **Solopreneurs** – Spot people asking for tools you’ve built  
- 💼 **Agencies** – Find potential clients expressing needs  
- 🧪 **Startups** – Watch for demand signals in real time  
- 🔍 **Researchers** – Monitor social platform chatter around a niche  

---

## ❓ FAQs

**Can this monitor Hacker News too?**  
Yes. F5Bot supports both Reddit and Hacker News keywords.

**Can I run this every hour?**  
Absolutely. Use Cron or a webhook trigger in n8n.

**Does it work with Outlook?**  
Not directly. Gmail works best with OAuth and label-based filtering.

**How are duplicates avoided?**  
The Google Sheets node checks existing entries by `url`.

**Can I track multiple keywords?**  
Yes — just add them to your F5Bot dashboard. Each mention becomes a new email.

---

## 🌟 Like This Automation?

If this helped you capture leads or monitor demand — consider giving this repo a ⭐

[⭐ Star on GitHub](https://github.com/Purnikk/n8n-workflow)

---

## 📬 Contact for Custom Workflows

Want this flow extended to Discord, Airtable, CRM, or auto-DMs?

[![Email](https://img.shields.io/badge/Email-Contact_Me-red?style=for-the-badge&logo=gmail&logoColor=white)](mailto:purnikparisha@gmail.com)
