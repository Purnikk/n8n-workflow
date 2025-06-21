# Reddit Restaurant Leads – Food, Cafes & Dining Out

This automation workflow extracts posts from Reddit where people are asking for food or restaurant recommendations. It's designed to help small restaurants, cafes, or food businesses discover real local demand and possibly engage with it.

---

## Why I Built This

Reddit is full of posts like:

> "Where’s the best biryani in Hyderabad?"  
> "Looking for a cafe in Delhi with good WiFi."  
> "Suggest a romantic dinner spot for this weekend?"

These are **genuine intent-based leads**, but they’re buried inside noisy threads. I built this to automatically:
- Find those posts across multiple city-based subreddits
- Classify them using an LLM
- Extract useful fields (area, cuisine, price range, purpose, etc.)
- Store everything neatly in a Google Sheet

This could be helpful for:
- Local businesses looking for new customers
- Food startups monitoring demand
- Tourism pages or food bloggers tracking local trends

---

## How It Works

The pipeline is built using **n8n**, **Gemini (LLM)**, and **Google Sheets**.

1. **Fetch Reddit Posts**
   - Monitors Reddit subreddits (any location-based one)
   - Searches for posts with food-related intent
   - Keywords like:
     - `where to eat`
     - `suggest a cafe`
     - `best biryani`
     - `places to eat in X`

2. **Classify Post Intent**
   - The LLM analyzes each post and classifies it as:
     - `lead`: actively asking for food/restaurant suggestions
     - `offer`: promoting a food business
     - `advice`: general discussion or review

3. **Extract Structured Fields**
   - From the post, it extracts:
     - Area or location
     - Type of cuisine
     - Price or budget range
     - Mood (work, date, family, etc.)
     - Notes
     - Author and post link

4. **Store to Google Sheets**
   - Each post becomes a row in the sheet
   - Includes original text, parsed fields, author, and clickable Reddit link

---

## Sample Output

| Area        | Cuisine   | Budget     | Type  | Mood        | Notes                         | Link         | Username         |
|-------------|-----------|------------|-------|-------------|-------------------------------|--------------|------------------|
| Gachibowli  | Biryani   | ₹300-₹500  | Lead  | Casual meal | Wants something spicy & local | [View Post]() | @RedditUser123   |

---

## Tech Stack

- **n8n** for flow automation
- **Reddit API** for input
- **Gemini LLM** for classification and parsing
- **Google Sheets API** for storage
- **OAuth** for Google access

---



