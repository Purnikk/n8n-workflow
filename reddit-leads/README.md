# Reddit Leads Automation (Flats & PGs)

This is an automation system I built using **n8n**, **LLMs (Gemini)**, and **Google Sheets** to convert noisy Reddit posts into **structured, business-usable leads** — especially for brokers, real-estate agents, and flat seekers.

It fetches relevant posts from city themed subreddits like `r/Hyderabad`, `r/Delhi`, etc., classifies their intent (leads/offering/advice), and extracts clean information like area, budget, notes ,  author and url of the post .

---

##  Why I Built This

Reddit  is a gold mine but its untapped it has a tons of real-world housing conversations especially in city-themed subreddits, but they’re **unstructured**, hard to search, and noisy.

I wanted to build something that could:
- Fetch these posts automatically
- Understand their **intent** using LLMs
- Extract structured fields (e.g., budget, location, etc.)
- Store it in Google Sheets for easy access and lead generation

---

##  How It Works (Workflow Overview)

**n8n** powers the full pipeline:

1. **Search Reddit Posts**  
   - Queries subreddits like `r/Hyderabad`, `r/Bangalore`, `r/Delhi` using Reddit API
   - Filters by keywords (e.g., “looking for flat”, “need 1BHK”, etc.)

2. **Classify Intent (Gemini)**  
   - Sends post content to LLM
   - Classifies post into:
     - `leads`: user looking for a flat
     - `offer`: user offering flat/room
     - `advice`: just discussion

3. **Parse Structured Data (Gemini again)**  
   - Extracts fields like:
     - `area`, `budget`, `BHK`, `post type `, `url`, `date`, `notes`, 'author of the post.

4. **Push to Google Sheets**  
   - Adds a new row with:
     - Parsed info
     - Post title and link
     - Username

---

## Sample Workflow Output 
Reddit Post Context -Hi everyone! I'm looking for a single or double sharing room in a fully set flat (no setup hassle) near Gachibowli.

Move-in date: 1st July

Budget: Up to ₹10,000

Food: I'm a vegetarian

Work: I'm a working professional

Flatmate preferences: Female

WORK FLOW
{
  "area": "Gachibowli, Kondapur",
  "room_type": "shared room",
  "budget": "under 10000",
  "food": "veg",
  "date": "July 1st",
  "type": "lead",
  "notes": "works as a professional"
}
