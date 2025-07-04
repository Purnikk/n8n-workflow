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

## 📷 Screenshots + Descriptions

---

### 1️⃣ Full Workflow Overview

![Workflow](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/01-workflow.png)

This is the entire n8n pipeline. The workflow includes:

- A form to accept subreddit + keywords  
- A Reddit fetcher  
- Relevance classifier (Gemini)  
- Extraction agent  
- Field collector  
- Google Sheets writer

This gives a bird's-eye view of the automation.

---

### 2️⃣ User Input Form

![Input Form](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/02-testform.png)

You can input:

- Subreddit name (like `r/hyderabadfood`)  
- Search keywords (`restaurant`, `food truck`, etc.)

This makes your automation flexible and reusable for different cities or niches.

---

### 3️⃣ Reddit Fetch Module

![Reddit Fetch](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/03-reddit.png)

This node fetches recent Reddit posts via API and extracts:

- `title`, `body`, `author`, `url`, `created_utc`

It also applies filters like:

- Recent posts only (e.g., last 3 days)  
- Keyword match (e.g., `restaurant`, `dining`, etc.)

---

### 4️⃣ Field Mapping Setup

![Field Mapping](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/04-Required%20fields.png)

This node defines the schema for final output like:

- `location`, `cuisine`, `budget`, `type`, and `intent`

It ensures uniform structure for storage or display.

---

### 5️⃣ Relevance Classifier (Gemini)

![Relevance](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/05-relevance.png)

This Gemini LLM node checks if the post is actually relevant for restaurant leads.

It looks for:

- Business-related context  
- Intent to buy, promote, or ask about food-related services

If not relevant, the post is skipped.

Sample output:

```json
{
  "relevant": true
}
```

---

### 6️⃣ LLM Extraction Agent

![Agent](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/06-agent.png)

Only runs for relevant posts. Gemini extracts structured fields like:

- `location` – area or city mentioned  
- `cuisine` – e.g., biryani, café, Chinese  
- `intent` – opening a restaurant, asking for suggestions  
- `budget` – if mentioned  

You can easily customize prompts for local business intelligence.

---

### 7️⃣ Final Structuring

![Collect Fields](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/07-collect%20fields.png)

This combines:

- Reddit metadata (`author`, `url`, `created_utc`)  
- Extracted fields from Gemini  
- Ensures everything is clean and formatted for output

---

### 8️⃣ Google Sheets Output

![Sheet Output](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/08-sheet.png)

Final structured leads are pushed into Google Sheets.

- One row per lead  
- De-duplicates using the `url`  
- Sheet becomes your lead CRM for outreach or analysis

---

## ⚙️ Smart Filtering Logic

To reduce spam and avoid unnecessary LLM usage:

- Filters posts by **recency** (last 3 days)  
- Filters by **keywords** like `restaurant`, `food`, `launch`  
- Relevance classifier ensures only business-useful content is processed

---

## 📊 Ideal Use Cases

This automation is built for:

- 🧁 Small restaurants or cafés tracking demand or customer intent  
- 🧠 Food entrepreneurs scouting Reddit for product-market fit  
- 📢 Agencies generating leads for F&B clients

---

## 📬 Contact

Need this customized for your own niche (e.g., salons, local tutors, freelancers)?

[![Email](https://img.shields.io/badge/Email-Contact_Me-red?style=for-the-badge&logo=gmail&logoColor=white)](mailto:purnikparisha@gmail.com)
