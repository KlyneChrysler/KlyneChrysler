## **The Value-Exchange Engine**

Influencer deals today are a guessing game. A restaurant gives a free dinner, an influencer posts a reel, and nobody knows if it was worth it. We fix that.

Our system turns every influencer deal into a **clear transaction** — what the business spent vs. what it got back — then tells the operator: **do it again, do it bigger, or walk away.**

---

### **1. Find the Right Influencer (Smart Matchmaking)**

Before spending a dollar, the operator needs to pick the right person. Our AI matches the business with the best-fit influencer based on real data, not guesswork.

#### How the Matchmaker Works

| What the AI Looks At | Why It Matters |
| :---- | :---- |
| **Niche match** | A steakhouse needs a food influencer, not a fitness one. The AI filters by content category. |
| **Engagement rate** | An influencer with 5,000 followers and 10% engagement is more valuable than one with 100,000 followers and 0.1% engagement. The AI ranks by engagement, not follower count. |
| **Audience location** | A hotel in Miami needs an influencer whose audience is actually in Miami — not in another country. The AI checks where the followers are. |
| **Past deal performance** | If the influencer has worked with businesses on the platform before, the AI already knows their ROI history. Proven performers rank higher. |
| **Budget alignment** | The AI matches the business's budget (cash + trade value) with influencers whose typical deal size fits that range. No wasted pitches. |

#### What the Operator Sees

| Screen | What It Shows |
| :---- | :---- |
| **Match List** | A ranked list of recommended influencers, best fit at the top |
| **Fit Score** | A single number (0–100) showing how well the influencer matches the business's needs |
| **Profile Card** | Niche, engagement rate, audience location, follower count, and past ROI (if available) |

The operator picks an influencer from the list — or skips matchmaking and enters one manually.

---

### **2. Log What You Gave**

Once the influencer is chosen, the operator records what the business is putting up:

* **Cash** — a flat fee, a retainer, any money paid.
* **Trade & Comps** — free product, hotel nights, meals, event access — each priced at **what it actually costs the business** (not the retail sticker price).
* **Any mix of both.**

The system adds it all up into one number: **Total Cost.**

> *Example: 2 hotel nights ($90 each) + dinner ($45) + $50 cash = **$275 Total Cost.***

---

### **3. Track What Came Back**

Once the influencer posts, the system automatically collects the results from three sources:

* **Custom Tracked Links (built in-house)** — every click and every sale tied directly to the influencer. We generate unique short links per deal, track every redirect on our own server, and log the click data straight into our database. No third-party dependency.
* **Social Metrics (Apify + GA4)** — Apify scrapes the influencer's post and pulls:
  1. Views (video plays)
  2. Likes
  3. Comments
  4. Shares
  5. Follower count at time of post

  GA4 then verifies the traffic was real people, not bots. The combined data is converted into a dollar value: what that same exposure would have cost through paid ads.
* **In-Store QR Codes** — for physical businesses, a unique code scanned at the register ties walk-ins to the influencer.

Everything rolls into one number: **Total Return.**

---

### **4. The Verdict: Did You Win or Lose?**

The math is one line:

> **ROI = (Total Return - Total Cost) / Total Cost**

* **You won** — Return is higher than Cost. The deal made money.
* **You lost** — Cost is higher than Return. The business overpaid.

The AI then gives the operator one clear action:

* **Repeat** — the deal worked, run it back on the same terms.
* **Scale** — the deal worked well, invest more next time.
* **Stop** — the deal lost money, don't renew.

---

### **5. Bonus Pay (Only When It's Earned)**

Operators can set optional performance bonuses on top of the base cost:

* *"$5 for every 1,000 views"* or *"10% of sales above $500."*
* If the influencer hits the target, the bonus is calculated automatically and added to the final cost.
* If they don't hit it, the bonus is $0. The business only pays the base.

This protects the business while rewarding influencers who deliver.

---

### **6. The Leaderboard: Your Influencer Roster, Ranked**

Every influencer gets a profile based on their deal history:

* **ROI Score** — who brings back the most value per dollar spent.
* **Fit Score** — how well they matched the business's niche and audience.
* **Cost Breakdown** — how you're paying each one (cash, trade, or a mix).
* **Track Record** — a history of Repeat / Scale / Stop verdicts across every past deal.

The operator opens the leaderboard and instantly sees: *who's worth it, who's not, and who deserves a bigger deal.*

The leaderboard also **feeds the matchmaker** — next time the operator creates a deal, the AI uses past ROI data to rank recommendations. The more deals you run, the smarter the matches get.

---

## **High-Level Design**

### **The Core Idea**

The system is a **scale**. One side holds what you spent. The other holds what you got back. The AI reads the scale and tells you what to do next.

#### What You Gave vs. What You Got Back

| What You Gave | $ | What You Got Back | $ |
| :---- | ----: | :---- | ----: |
| Cash | $50 | Sales | $320 |
| Hotel (2 nights) | $180 | Website Clicks (1,200) | — |
| Free Dinner | $45 | Views (50,000) → Ad Value | $150 |
| | | | |
| **Total Cost** | **$275** | **Total Return** | **$470** |

#### The Verdict

| Metric | Value |
| :---- | :---- |
| **ROI** | **+71%** |
| **Action** | **SCALE — invest more next time** |

---

### **From Deal to Decision — 6 Steps**

| Step | What Happens | Who Does It | Output |
| :---- | :---- | :---- | :---- |
| **1. Find the Match** | AI recommends the best influencer based on niche, engagement, location, budget, and past ROI | AI (auto) | **Ranked match list + Fit Score** |
| **2. Log the Deal** | Operator records what the business gave — cash, product, comps | Operator (manual) | **Total Cost** |
| **3. Influencer Posts** | Influencer creates content and shares it with tracked links | Influencer (manual) | Content is live |
| **4. Track Results** | System collects clicks, sales, views, and store visits automatically | System (auto) | **Total Return** |
| **5. Calculate Win/Loss** | AI compares Cost vs. Return and calculates ROI | AI (auto) | **ROI score** |
| **6. Decide Next Move** | AI gives one clear action: Repeat, Scale, or Stop | AI (auto) | **Verdict** |

---

### **System Architecture**

#### Layer 1 — Operator Dashboard (Next.js 15)

| Screen | What the Operator Sees |
| :---- | :---- |
| **Find Influencer** | AI-ranked match list with Fit Scores and profile cards |
| **Create Deal** | Form to log cash, comps, trade items with dollar values |
| **Dashboard** | Win / Loss results for every deal |
| **Leaderboard** | All influencers ranked best to worst by ROI |

#### Layer 2 — AI Engine (Genkit)

| Step | What the AI Does |
| :---- | :---- |
| 1 | Matches the business with the best-fit influencer |
| 2 | Totals the Cost (everything the business gave) |
| 3 | Totals the Return (everything the business got back) |
| 4 | Calculates ROI |
| 5 | Outputs the verdict: **Repeat / Scale / Stop** |
| 6 | Feeds results back into matchmaking to improve future recommendations |

#### Layer 3 — Data Sources (auto-collected)

| Tool | What It Tracks |
| :---- | :---- |
| **Custom Link Tracker** | Clicks and sales from influencer links (built in-house) |
| **Apify** | Views, likes, comments, shares, follower count from influencer posts |
| **GA4** | Confirms visitors are real people, not bots |

#### Layer 4 — Database (Supabase)

| Table | What It Stores |
| :---- | :---- |
| **Influencers** | Profile data — niche, engagement rate, audience location, follower count |
| **Deals** | Each deal and its terms |
| **Items** | Each comp, cash, or trade item with a dollar value |
| **Results** | Clicks, sales, views, and ROI per deal |
| **Scores** | Every influencer's ROI score, Fit Score, and verdict history |

---

### **How the Layers Connect**

| From | To | What Flows |
| :---- | :---- | :---- |
| **Operator Dashboard** | **AI Engine** | Business profile + matchmaking request |
| **AI Engine** | **Operator Dashboard** | Ranked influencer matches with Fit Scores |
| **Operator Dashboard** | **Database** | Deal inputs (what was given) |
| **Custom Link Tracker** | **Database** | Click and sale events per influencer link |
| **Apify** | **Database** | Views, likes, comments, shares per post |
| **GA4** | **AI Engine** | Verified traffic data (real users, not bots) |
| **Database** | **AI Engine** | Cost + Return numbers for each deal |
| **AI Engine** | **Operator Dashboard** | ROI score + Repeat / Scale / Stop verdict |
| **Database (past results)** | **AI Engine (matchmaker)** | Historical ROI data to improve future matches |

---

### **One Sentence**

> The AI finds the right influencer, the operator logs what they gave, the system tracks what came back, and the AI tells the operator: **do it again, do it bigger, or walk away.**

---

## **How Google Analytics (GA4) Works in This System**

GA4 is the **proof layer**. It doesn't track what the influencer posted — Apify does that. GA4 tracks what happened **on the business's own website** after the influencer posted.

### **What GA4 Answers**

| Question | What GA4 Tells Us |
| :---- | :---- |
| Did people actually visit the site? | Yes — it counts every visitor who came through the influencer's link |
| Were they real people or bots? | GA4 filters out known bots and spam traffic automatically |
| What did visitors do on the site? | How many pages they viewed, how long they stayed, did they bounce instantly |
| Did anyone buy something? | If the business has a checkout, GA4 tracks completed purchases |
| How much money came in? | GA4 logs the revenue from each purchase tied to the influencer's link |

### **Step-by-Step: How GA4 Connects to Our App**

| Step | What Happens | Simple Explanation |
| :---- | :---- | :---- |
| **1. Business installs GA4** | The business adds a small tracking code to their website | Like putting a counter at the door of a store — it counts everyone who walks in |
| **2. We tag every influencer link with UTM parameters** | Each link gets a unique label baked into the URL (e.g., `?utm_source=influencer&utm_campaign=maria_deal_42`) | Like giving each influencer a different colored ticket — we can tell who sent each visitor |
| **3. Influencer shares the tagged link** | The influencer puts the link in their bio, story, or post | The audience clicks the link and lands on the business's website |
| **4. GA4 records every visit** | For every person who clicks, GA4 logs: where they came from, what they did, and if they bought anything | The counter at the door now knows which influencer sent them |
| **5. We pull the data via GA4 API** | Our backend calls the Google Analytics Data API and asks: "How many visitors, sessions, and purchases came from this specific UTM tag?" | We ask GA4: "How many people did Maria send, and did any of them buy?" |
| **6. We separate real traffic from fake** | GA4 has built-in bot filtering. We also check: Did visitors stay more than 10 seconds? Did they view more than 1 page? | If someone clicked and left in 1 second, that doesn't count as real engagement |
| **7. Data goes into our database** | We save the verified numbers into Supabase under that deal's results | Now we have clean, trusted numbers for the ROI calculation |
| **8. AI uses it for the verdict** | The AI combines GA4 data (real traffic + purchases) with Apify data (social metrics) to calculate Total Return | GA4 proves the money. Apify proves the exposure. Together they give the full picture. |

### **What We Pull from the GA4 API (per influencer link)**

| Data Point | What It Means | Why It Matters |
| :---- | :---- | :---- |
| **Sessions** | Number of visits from the influencer's link | Did the influencer actually drive traffic? |
| **New Users** | First-time visitors who never came to the site before | The influencer brought fresh eyes, not repeat visitors |
| **Bounce Rate** | % of visitors who left without doing anything | High bounce = low quality traffic |
| **Average Session Duration** | How long visitors stayed on the site | Longer stays = more interest = higher quality |
| **Pages Per Session** | How many pages each visitor looked at | More pages = more engaged visitors |
| **Conversions** | Number of completed goals (purchases, sign-ups, bookings) | Did the traffic turn into money? |
| **Revenue** | Total dollar amount from purchases | The hard number that feeds directly into Total Return |

### **How GA4 Data Turns Into Dollars**

| Traffic Type | How We Value It |
| :---- | :---- |
| **Visitor made a purchase** | We use the actual revenue number from GA4 — real dollars, no estimation |
| **Visitor didn't buy but engaged** | We calculate what that traffic would have cost through Google Ads (cost-per-click in the business's industry). This becomes the **Estimated Media Value (EMV)** |
| **Visitor bounced immediately** | Worth $0 — filtered out, does not count toward Total Return |

---

## **Full System Flowchart**

### **Phase 1 — Find the Right Influencer**

| # | Action | Who | What Happens | Next |
| :---- | :---- | :---- | :---- | :---- |
| 1 | Operator opens the app | Operator | Lands on the dashboard | → 2 |
| 2 | Operator starts a new campaign | Operator | Enters: business type, niche, budget, target audience location | → 3 |
| 3 | AI runs the matchmaker | AI (Genkit) | Scans the influencer database — filters by niche, checks engagement rate, compares audience location, looks at past ROI history | → 4 |
| 4 | AI returns a ranked match list | AI (Genkit) | Each influencer gets a Fit Score (0–100). Best matches at the top. | → 5 |
| 5 | Operator picks an influencer | Operator | Reviews the match list, checks profile cards, selects the best fit (or enters one manually) | → Phase 2 |

### **Phase 2 — Deal Setup**

| # | Action | Who | What Happens | Next |
| :---- | :---- | :---- | :---- | :---- |
| 6 | Operator creates a new deal | Operator | Fills in: influencer name, deliverables (posts, reels, stories) | → 7 |
| 7 | Operator logs what they're giving | Operator | Adds each item — cash, product, hotel nights, meals — each with a dollar value | → 8 |
| 8 | System calculates **Total Cost** | System | Adds up all items into one number | → 9 |
| 9 | System generates a unique tracked link | System | Creates a short URL tied to this deal + this influencer. Redirects to the business's website with UTM tags baked in | → 10 |
| 10 | Operator sends the deal + link to the influencer | Operator | Influencer receives the deal terms and their unique link | → Phase 3 |

### **Phase 3 — Influencer Delivers**

| # | Action | Who | What Happens | Next |
| :---- | :---- | :---- | :---- | :---- |
| 11 | Influencer accepts the deal | Influencer | Agrees to the terms and deliverables | → 12 |
| 12 | Influencer creates the content | Influencer | Makes the reel, story, post, or video | → 13 |
| 13 | Influencer includes the tracked link | Influencer | Puts the unique link in their bio, caption, or story | → 14 |
| 14 | Influencer publishes the content | Influencer | Content goes live on Instagram, TikTok, YouTube, etc. | → Phase 4 |

### **Phase 4 — System Tracks Everything**

| # | Action | Who | What Happens | Next |
| :---- | :---- | :---- | :---- | :---- |
| 15 | Audience clicks the tracked link | Audience | Each click hits our server first, gets logged, then redirects to the business's site | → 16 |
| 16 | Custom Link Tracker logs every click | System | Records: timestamp, device, location, and which deal the click belongs to | → 17 |
| 17 | GA4 records the website visit | GA4 | Logs: where the visitor came from (UTM tag), what pages they viewed, how long they stayed | → 18 |
| 18 | GA4 tracks purchases (if any) | GA4 | If the visitor buys something, GA4 records the conversion and the revenue amount | → 19 |
| 19 | GA4 filters out bots and fake traffic | GA4 | Removes known bots, spam, and visitors who bounced in under 1 second | → 20 |
| 20 | Apify scrapes the influencer's post | Apify | Pulls: views, likes, comments, shares, follower count at time of post | → 21 |
| 21 | All data is saved to the database | System | Click data, GA4 traffic data, Apify social data — all stored under this deal in Supabase | → Phase 5 |

### **Phase 5 — AI Does the Math**

| # | Action | Who | What Happens | Next |
| :---- | :---- | :---- | :---- | :---- |
| 22 | AI pulls the Cost from the database | AI (Genkit) | Reads the Total Cost that was logged in Step 8 | → 23 |
| 23 | AI pulls the Return from the database | AI (Genkit) | Adds up: revenue from GA4 + estimated media value from Apify + click value from link tracker | → 24 |
| 24 | AI calculates **Total Return** | AI (Genkit) | Real sales ($) + Estimated Media Value ($) = one number | → 25 |
| 25 | AI compares Cost vs. Return | AI (Genkit) | **ROI = (Total Return - Total Cost) / Total Cost** | → 26 |
| 26 | AI checks for bonus tiers | AI (Genkit) | If the operator set a performance bonus (e.g., "$5 per 1,000 views"), AI checks if the influencer hit it | → 27 |
| 27 | AI adds bonus to Total Cost (if earned) | AI (Genkit) | If the influencer hit the bonus target, the bonus amount is added to the final cost and ROI is recalculated | → Phase 6 |

### **Phase 6 — The Verdict**

| # | Action | Who | What Happens | Next |
| :---- | :---- | :---- | :---- | :---- |
| 28 | AI gives the verdict | AI (Genkit) | Based on the final ROI: **Repeat** (ROI positive) / **Scale** (ROI highly positive) / **Stop** (ROI negative) | → 29 |
| 29 | Dashboard shows the results | System | Operator sees: Total Cost, Total Return, ROI %, and the verdict — all on one screen | → 30 |
| 30 | Leaderboard updates | System | This influencer's ROI score, Fit Score, and verdict history are updated in the rankings | → 31 |
| 31 | Results feed back into the matchmaker | System | The AI now knows how this influencer performed — future match recommendations get smarter | → 32 |
| 32 | Operator makes the call | Operator | Looks at the verdict and decides: run it back, invest more, or walk away | Done |

### **Decision Logic (Step 28 — How the AI Picks the Verdict)**

| Condition | ROI Range | Verdict | What It Means |
| :---- | :---- | :---- | :---- |
| Return is much higher than Cost | ROI > +50% | **Scale** | This influencer is highly profitable — give them a bigger deal |
| Return is higher than Cost | ROI between 0% and +50% | **Repeat** | The deal made money — run it back on the same terms |
| Return is lower than Cost | ROI < 0% | **Stop** | The business lost money — do not renew this deal |

---

## **Tech Stack**

| Layer | Tool | What It Does |
| :---- | :---- | :---- |
| **Dashboard** | Next.js 15 | The operator's screen — matchmaking, deal forms, results, leaderboard |
| **AI Engine** | Genkit | Matchmaking, ROI math, and the Repeat / Scale / Stop verdict |
| **Database** | Supabase | Stores influencer profiles, every deal, every item, every result |
| **Link Tracking** | Custom (built in-house) | Generates unique short links, tracks clicks and sales on our own server |
| **Social Data** | Apify | Pulls views, likes, comments, shares from influencer posts |
| **Traffic Proof** | GA4 | Confirms the visitors were real people, not bots |
