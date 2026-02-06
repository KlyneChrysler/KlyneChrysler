## **The Core Solution: The Hybrid "Value-Exchange" Engine**

A system that treats every influencer deal as a **two-sided economic transaction** — what the business *gave* vs. what the influencer *delivered* — then tells the operator whether to repeat, scale, or stop.

---

### **1. Deal Input Ledger (Track What Was Given)**

Every deal starts by logging **everything the business puts on the table**:

* **Cash:** Base fee, flat rate, retainer.
* **Trade / Comps:** Free product, hotel nights, meals, event tickets — each auto-valued at **Operator Cost** (what it actually costs the business, not retail).
* **Hybrid Mix:** Any combination of the above. The system totals it into one number: **Total Deal Cost (TDC)**.

The operator fills out a simple form: *"2 nights ($90/night) + free dinner ($45) + $50 cash = TDC of $275."*

---

### **2. Deal Output Tracking (Track What Was Delivered)**

Three attribution layers capture the influencer's actual output:

* **Branded Trust Links (Dub.co):** Tracks clicks and attributed sales — proves direct revenue.
* **Exposure Verification (Apify + GA4):** Scrapes views/likes, then GA4 confirms real engagement (not bots). Converted into **Estimated Media Value (EMV)** — what that exposure would have cost via paid ads.
* **Offline QR Codes:** For physical businesses — scans at the register tied to the influencer's unique code.

All outputs roll into one number: **Total Deal Return (TDR)** = attributed revenue + EMV.

---

### **3. The Verdict: Gain / Loss Calculation**

The core math is simple:

> **Deal ROI = (TDR - TDC) / TDC**

* **Gain:** TDR > TDC — the deal was worth it.
* **Loss:** TDR < TDC — the business overpaid.
* **AI Recommendation:** Based on the ROI, the system outputs one of three actions:
  * **Repeat** — ROI positive, same terms.
  * **Scale** — ROI highly positive, increase budget / offer more.
  * **Stop** — ROI negative, do not renew.

---

### **4. Performance Kicker (Variable Bonus Layer)**

On top of the base TDC, operators can optionally define **Success Tiers**:

* e.g., "$5 per 1,000 views" or "10% of attributed sales above $500."
* If the influencer hits a tier, the bonus is auto-calculated and added to TDC for the final ledger.
* If they don't hit it, the variable stays at $0 — the business only paid the base.

---

### **5. Influencer Leaderboard (Repeat / Scale / Stop at a Glance)**

Ranks all influencers by **economic efficiency**:

* **ROI Score:** (TDR - TDC) / TDC — who returns the most per dollar spent.
* **Cost Profile:** Shows the mix (cash vs. trade vs. hybrid) so operators see *how* they're paying.
* **Verdict History:** A rolling log of Repeat / Scale / Stop recommendations per influencer across all past deals.

---

## **High-Level Design**

```
┌─────────────────────────────────────────────────┐
│                  OPERATOR UI (Next.js 15)        │
│  Create Deal  |  Dashboard  |  Leaderboard       │
└──────────┬──────────────┬───────────────┬────────┘
           │              │               │
     ┌─────▼─────┐ ┌─────▼──────┐ ┌──────▼──────┐
     │ DEAL INPUT │ │ DEAL OUTPUT│ │  AI ENGINE  │
     │  LEDGER    │ │  TRACKER   │ │  (Genkit)   │
     │            │ │            │ │             │
     │ Cash       │ │ Dub.co API │ │ Gain/Loss   │
     │ Trade/Comp │ │ Apify      │ │ ROI Calc    │
     │ Hybrid Mix │ │ GA4        │ │ Repeat/     │
     │            │ │ QR Scans   │ │ Scale/Stop  │
     │ ──────►TDC │ │ ──────►TDR │ │ Recommend   │
     └─────┬──────┘ └─────┬──────┘ └──────┬──────┘
           │              │               │
     ┌─────▼──────────────▼───────────────▼──────┐
     │           SUPABASE (Postgres)              │
     │                                            │
     │  deals        deal_items      deal_results │
     │  (contract)   (each comp/     (TDR, EMV,   │
     │               cash/trade      sales, ROI)  │
     │               line item                    │
     │               with $ value)                │
     │                                            │
     │  influencers          leaderboard_scores   │
     └────────────────────────────────────────────┘
```

**Data flow:** Operator logs deal inputs (TDC) → Influencer posts content → Attribution APIs feed outputs (TDR) → AI computes ROI and verdict → Dashboard shows Gain/Loss + recommendation.

---

## **Tech Stack**

| Layer | Tool | Role |
| :---- | :---- | :---- |
| **UI & Logic** | Next.js 15 | Deal creation form, dashboard, leaderboard |
| **AI** | Genkit | ROI analysis, repeat/scale/stop recommendation |
| **Database** | Supabase | Deal ledger (inputs + outputs), auth, leaderboard |
| **Link Attribution** | Dub.co API | Click & sales tracking via branded links |
| **Exposure Data** | Apify | Scrape influencer post metrics (views, likes) |
| **Engagement Proof** | GA4 | Validate real traffic, compute EMV |
