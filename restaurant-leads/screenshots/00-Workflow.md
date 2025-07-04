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

### 1️⃣ Full Workflow in n8n

![Workflow](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/01-workflow.png)

---

### 2️⃣ User Input Form

![Input Form](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/02-testform.png)

---

### 3️⃣ Reddit Fetch Module

![Reddit Fetch](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/03-reddit.png)

---

### 4️⃣ Field Mapping Setup

![Field Mapping](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/04-Required%20fields.png)

---

### 5️⃣ Relevance Classifier (Gemini)

![Relevance Classifier](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/05-relevance.png)

```json
{
  "relevant": true
}
```

---

### 6️⃣ LLM Extraction Agent

![LLM Agent](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/06-agent.png)

---

### 7️⃣ Final Structuring

![Final Structuring](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/07-collect%20fields.png)

---

### 8️⃣ Google Sheets Output

![Google Sheets Output](https://raw.githubusercontent.com/Purnikk/n8n-workflow/main/restaurant-leads/screenshots/08-sheet.png)

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
