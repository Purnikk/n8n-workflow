# 🏠 Reddit Housing Leads Automation – n8n + Gemini

This automation identifies and structures potential **rental leads** (apartments, flats, etc.) from Reddit using **n8n**, **Gemini (LLM)**, and **Google Sheets**. It's tailored for **real estate professionals**, **property agents**, and **city-specific lead trackers**.

---

## 🧠 Workflow Stages

1. **Form Input** – Dynamically collects subreddit/keyword via UI  
2. **Data Collection** – Fetches Reddit posts using API  
3. **Relevance Check** – Uses Gemini to classify lead quality  
4. **Agent Extraction** – Pulls fields like area, budget, bhk, urgency  
5. **Sheet Output** – Pushes structured data into Google Sheets

---

## 📸 Screenshots & Explanations

### 1️⃣ Full Workflow Overview  
![01-leads-n8n](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/reddit-leads/screenshots/01-leads-n8n.png)

Shows the complete n8n workflow with clear sections:
- **Reddit fetch**
- **LLM-based filtering**
- **Field extraction**
- **Sheet output**

---

### 2️⃣ Dynamic Input Form  
![02-test-form](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/reddit-leads/screenshots/02-test-form.png)

Accepts:
- Subreddit name (e.g., `r/Hyderabad`)
- Keywords like `rent`, `2bhk`, `flat`

Avoids hardcoded values for easier reuse across different locations.

---

### 3️⃣ Reddit Post Collection  
![03-reddit-posts](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/reddit-leads/screenshots/03-reddit-posts.png)

Fetched using Reddit’s API with:
- Title, body, author, url, created date
- Filters based on **recency** and **keywords**

---

### 4️⃣ Relevance Check – Gemini  
![04-relevance-check](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/reddit-leads/screenshots/04-relevance-check.png)

This block checks if a post is actually a **rental lead**.

🧠 Gemini LLM prompt returns:
```json
{
  "relevant": "yes"
}
```

Only "yes" posts go forward.

---

### 5️⃣ Extraction Agent (LLM)  
![05-agent-working](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/reddit-leads/screenshots/05-agent-working.png)

If relevant, the agent extracts:
- `bhk`
- `budget`
- `location`
- `urgency`
- `notes`

Outputs structured JSON per post.

---

### 6️⃣ Final Structuring  
![06-required-fields](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/reddit-leads/screenshots/06-required-fields.png)

Combines:
- Reddit metadata
- LLM-extracted fields

Prepares final format for pushing to Sheets.

---

### 7️⃣ Google Sheets Output  
![07-gsheet](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/reddit-leads/screenshots/07-gsheet.png)

Each lead is stored in Google Sheets as a row.  
✅ Deduplication handled using `url`

---

## 🧠 Filtering Before AI

To reduce Gemini usage and increase quality:
- Checks post recency (e.g., last 3 days)
- Searches for keywords like `rent`, `flat`, `bhk`
- Filters by location or intent (optional)

---

## 💼 Perfect For

- 🏢 Real estate agents auto-monitoring city subreddits  
- 🔍 Housing search portals looking to extract live demand  
- 🧠 Data scraping enthusiasts trying to build B2C pipelines

---

## 📬 Contact

Need a custom version or commercial deployment?

[![Email](https://img.shields.io/badge/Email-Contact_Me-red?style=for-the-badge&logo=gmail&logoColor=white)](mailto:purnikparisha@gmail.com)
