# 📸 Screenshots – Reddit Leads Automation (n8n + Gemini)

This folder contains visuals of the complete **Reddit Leads Automation** workflow, which uses **n8n**, **LLMs (Gemini)**, and **Google Sheets** to classify and structure Reddit posts into business-usable leads — especially for rental posts like apartments/flats.

---

## 🧠 Workflow Stages

The automation follows five main stages:

1. **Form Input** – Dynamically collects subreddit/keyword via UI  
2. **Data Collection** – Fetches recent Reddit posts using API  
3. **Relevance Check** – Uses Gemini LLM to classify lead quality  
4. **Agent Extraction** – Extracts structured fields like area, BHK, etc.  
5. **Sheet Output** – Stores data in Google Sheets with deduplication  

Each screenshot in this folder documents one or more of these steps.

---

## 📷 Screenshot Descriptions

### 1️⃣ `01-leads-n8n.png` – Full Workflow Overview

This screenshot shows the complete n8n flow with color-coded sections:

- 🟫 **Data Collection**  
  - Retrieves Reddit posts based on form input  
  - Filters posts by content and freshness (recent days only)

- 🟩 **Relevance Check**  
  - Uses Gemini to classify if post matches rental lead criteria

- 🟦 **Agent Block**  
  - Extracts structured information from relevant posts

- 🟥 **Output**  
  - Stores data into Google Sheets  
  - Deduplication is handled by URL matching

---

### 2️⃣ `02-test-form.png` – Dynamic Form Input

- Allows entering subreddit dynamically (e.g., `r/Hyderabad`, `r/Chennai`)  
- Avoids hardcoded values in Reddit nodes  
- Supports flexible reuse across cities or topics

---

### 3️⃣ `03-reddit-posts.png` – Raw Reddit Data (API)

- Reddit posts are fetched using the Reddit API  
- Extracted fields include:
  - `title`, `body`, `author`, `url`, and `created_utc`
- Filter logic includes:
  - Posts within a certain age (e.g., last 3 days)
  - Posts containing specific keywords (e.g., `flat`, `2bhk`, `rent`)

---

### 4️⃣ `04-relevance-check.png` – LLM Classifier (Gemini)

- This node classifies whether a Reddit post is **relevant**  
- Uses a Gemini prompt with binary logic  
- Expected JSON output from the LLM:

```json
{
  "relevant": "yes"
}
```

- Irrelevant posts are excluded from further processing

---

### 5️⃣ `05-agent-working.png` – LLM Extraction Agent

- Activated only for relevant posts  
- Extracts structured lead details such as:
  - `area`
  - `budget`
  - `bhk`
  - `date`
  - `notes` (extra preferences or remarks)
- Uses Gemini and outputs clean JSON for mapping

---

### 6️⃣ `06-required-fields.png` – Assembling Final Output

- Merges metadata from Reddit + extracted fields from LLM  
- Required fields typically include:
  - `author`, `url`, `bhk`, `budget`, `area`
- Performs final cleanup and structuring before saving to Sheets

---

### 7️⃣ `07-gsheet.png` – Sheet Output (Final Destination)

- Relevant, cleaned data is stored in a Google Sheet  
- Each row represents one qualified lead  
- Deduplication is handled using the Reddit `url` field to avoid re-entry

---

## ⚙️ Filter Logic Before LLM

To optimize costs and avoid unnecessary LLM calls:

- Posts are filtered based on:
  - Specific contextual keywords (e.g., `flat`, `rent`, `2bhk`)
  - Age limit (e.g., only posts from the last  specific number of days)
  - Optional user-specific filters (e.g., location, budget, BHK)

---

## 💼 Commercial Use & Custom Solutions

This automation workflow is perfect for:

- **Real Estate Agencies** – Automated lead generation from multiple cities  
- **Property Management Companies** – Continuous monitoring of rental markets  
- **Business Development** – Lead generation across various industries  
- **Marketing Agencies** – Social media monitoring and lead extraction  

---

## 📬 Contact for Business Inquiries

Need a custom solution for your business?  
Whether you need this workflow adapted for your specific use case, integrated with your existing systems, or deployed at enterprise scale — I provide consultation and custom development services.

[![Email](https://img.shields.io/badge/Email-Contact_Me-red?style=for-the-badge&logo=gmail&logoColor=white)](mailto:purnikparisha@gmail.com)
