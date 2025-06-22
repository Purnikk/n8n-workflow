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

## 📷 Screenshot Descriptions

### 1️⃣ `01-workflow.png` – Full Workflow in n8n

- Displays the entire pipeline
- Modules include:
  - Form input  
  - Reddit puller  
  - LLM relevance filter  
  - Data extraction + cleanup  
  - Google Sheets writer

---

### 2️⃣ `02-testform.png` – User Input Form

- Accepts:
  - Subreddit name (e.g., `r/hyderabadfood`)  
  - Search keywords (e.g., `restaurant`, `food truck`, `dine-in`)  
- Makes workflow reusable across different cities or regions

---

### 3️⃣ `03-reddit.png` – Reddit Fetch Module

- Pulls fresh Reddit posts using API  
- Extracted fields:
  - `title`, `body`, `author`, `url`, `created_utc`  
- Filters posts by:
  - **Recency** (e.g., only last 3 days)
  - **Keyword match** (`food`, `restaurant`, etc.)

---

### 4️⃣ `04-Required fields.png` – Field Mapping Setup

- Prepares structure for:
  - `location`, `cuisine`, `budget`, `type`, and `intent`  
- Keeps output consistent and usable in sheets or dashboards

---

### 5️⃣ `05-relevance.png` – Relevance Classifier (Gemini)

- Determines if a post is **relevant to small restaurant or food business owners**  
- Analyzes post context and business intent  
- Ignores low-quality or off-topic content

```json
{
  "relevant": true
}
```

---

### 6️⃣ `06-agent.png` – LLM Extraction Agent

- Runs only for posts marked “relevant”  
- Extracts structured fields such as:
  - `location`, `cuisine`, `budget`, `intent`  
- Can be customized with different prompts depending on region or business type

---

### 7️⃣ `07-collect fields.png` – Final Structuring

- Merges:
  - Reddit metadata (author, url, etc.)  
  - Gemini-extracted fields  
- Cleans and validates the final object before saving

---

### 8️⃣ `08-sheet.png` – Google Sheets Output

- Each qualified lead is saved as a row in Google Sheets  
- Deduplication is handled using the post `url`  
- Sheet acts as a source of truth for further action

---

## ⚙️ Smart Filtering Logic

To reduce noise and save compute, the workflow uses:

- **Post freshness filters** (e.g., last 3 days only)
- **Contextual keywords** to find intent-heavy posts
- **Relevance checks** that assess the post’s usefulness to real businesses

---

## 📊 Ideal Use Cases

This automation is perfect for:

- 🧁 Small restaurant or café owners tracking demand or visibility  
- 🧠 Food entrepreneurs looking for Reddit leads or insights  
- 📢 Agencies scouting leads for restaurant clients

---

## 📬 Contact

Need this customized for your business niche or automated outreach?

[![Email](https://img.shields.io/badge/Email-Contact_Me-red?style=for-the-badge&logo=gmail&logoColor=white)](mailto:purnikparisha@gmail.com)
