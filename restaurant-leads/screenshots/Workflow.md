# 🍽️ Restaurant Leads Automation – n8n + Gemini

This workflow automates the process of identifying and capturing **potential restaurant or café-related leads from Reddit**, specifically for **small business owners looking for customers or visibility**. It uses **n8n**, **Gemini (LLM)**, and **Google Sheets** to process, extract, and organize relevant Reddit posts into usable leads.

---

## 🧩 Workflow Stages

The system works in the following phases:

1. **Dynamic Input Form** – Accepts subreddit and keyword filters  
2. **Reddit Post Fetching** – Gathers recent threads from Reddit  
3. **Relevance Classification** – Determines if the post relates to food businesses  
4. **LLM Extraction Agent** – Pulls useful fields like cuisine, location, intent  
5. **Final Structuring** – Combines all data into one clean object  
6. **Sheet Output** – Exports results to Google Sheets

---

## 🖼️ Screenshots & Explanations

### 1️⃣ Full Workflow in n8n

![Workflow](./screenshots/01-workflow.png)

Displays the entire pipeline:
- Form input  
- Reddit puller  
- LLM relevance filter  
- Data extraction + cleanup  
- Google Sheets writer

---

### 2️⃣ Dynamic Input Form

![Test Form](./screenshots/02-testform.png)

Accepts user-defined parameters:
- Subreddit name (e.g., `r/hyderabadfood`)  
- Search keywords (e.g., `restaurant`, `food truck`, `dine-in`)  

🔁 Makes the workflow reusable for any location or category.

---

### 3️⃣ Reddit Post Fetch Module

![Reddit API](./screenshots/03-reddit.png)

Pulls recent posts using Reddit API.

Extracted fields:
- `title`, `body`, `author`, `url`, `created_utc`

Filters based on:
- Recency (e.g., last 3 days)  
- Keyword match (`food`, `restaurant`, etc.)

---

### 4️⃣ Required Fields Mapping

![Field Structure](./screenshots/04-Required-fields.png)

Prepares clean structure for:
- `location`, `cuisine`, `budget`, `type`, `intent`

Keeps output consistent and usable in spreadsheets or dashboards.

---

### 5️⃣ Relevance Classifier – Google Gemini

![Relevance Check](./screenshots/05-relevance.png)

LLM decides if a post is relevant to small restaurant or food business owners.

**Example Output:**

{
"relevant": true
}

🔍 Filters out irrelevant, spammy, or unrelated posts.

---

### 6️⃣ LLM Extraction Agent

![Gemini Agent](./screenshots/06-agent.png)

Activated only for posts marked as relevant.

Extracts:
- `location`
- `cuisine`
- `budget`
- `intent`

🧠 Prompt can be tuned for your business goals or local context.

---

### 7️⃣ Final Field Collection

![Merge Fields](./screenshots/07-collect-fields.png)

Combines:
- Reddit metadata (title, URL, author)  
- Extracted fields from Gemini  

Final cleanup and validation before writing to sheet.

---

### 8️⃣ Google Sheets Output

![Sheet Output](./screenshots/08-sheet.png)

- Appends each lead as a new row  
- Ensures no duplicates using post `url`  
- Sheet becomes a trackable lead source

---

## ⚙️ Smart Filtering Logic

To reduce noise and optimize LLM calls:
- ✅ Filters posts by **date**
- ✅ Uses keyword logic to reduce false positives
- ✅ Gemini filters out irrelevant or spam content

---

## 📊 Ideal Use Cases

This automation is perfect for:

- 🧁 Small restaurant or café owners tracking demand  
- 🧠 Food entrepreneurs scouting Reddit discussions  
- 📢 Agencies seeking leads for F&B clients

---

## 📬 Contact

Need this customized for your business niche or automated outreach?

[![Email](https://img.shields.io/badge/Email-Contact_Me-red?style=for-the-badge&logo=gmail&logoColor=white)](mailto:purnikparisha@gmail.com)

