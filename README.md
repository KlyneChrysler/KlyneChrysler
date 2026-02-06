[## **The Core Solution: The Hybrid "Value-Exchange" Engine**

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

### **How It Works — The Big Picture**

Think of the system as a **scale**. One side holds what the business spent. The other side holds what the business got back. The AI reads the scale and tells you what to do next.

```
    WHAT YOU GAVE                              WHAT YOU GOT BACK
    ────────────                               ─────────────────
                         ┌──────────┐
   Cash ($50)            │          │         Sales ($320)
   Hotel (2 nights $180) │  THE     │         Website Clicks (1,200)
   Free Dinner ($45)     │  SCALE   │         Views (50,000 → EMV $150)
                         │          │
   ─────────────────     │          │         ─────────────────────
   Total Cost: $275      └──────────┘         Total Return: $470
                              │
                              ▼
                     ┌────────────────┐
                     │   THE VERDICT  │
                     │                │
                     │  ROI = +71%    │
                     │                │
                     │  ✅ SCALE UP   │
                     └────────────────┘
```

---

### **The 5 Steps — From Deal to Decision**

```
 STEP 1            STEP 2             STEP 3           STEP 4          STEP 5
 ──────            ──────             ──────           ──────          ──────

 LOG THE           INFLUENCER         TRACK THE        CALCULATE       DECIDE
 DEAL              DOES THE WORK      RESULTS          GAIN / LOSS     NEXT MOVE

 ┌──────────┐     ┌──────────┐      ┌──────────┐    ┌──────────┐    ┌──────────┐
 │ Operator  │     │Influencer│      │ System   │    │ AI reads │    │ AI says: │
 │ lists     │────▶│ posts    │─────▶│ collects │───▶│ both     │───▶│          │
 │ what they │     │ content  │      │ the data │    │ sides    │    │ REPEAT   │
 │ gave:     │     │ with     │      │          │    │          │    │ SCALE    │
 │           │     │ tracking │      │ Clicks   │    │ Cost vs  │    │ or STOP  │
 │ - Cash    │     │ links    │      │ Sales    │    │ Return   │    │          │
 │ - Product │     │          │      │ Views    │    │          │    │          │
 │ - Comps   │     │          │      │ Store    │    │ ROI =    │    │          │
 │           │     │          │      │ visits   │    │ (R - C)  │    │          │
 │ = COST    │     │          │      │ = RETURN │    │   / C    │    │          │
 └──────────┘     └──────────┘      └──────────┘    └──────────┘    └──────────┘
```

---

### **Where Each Tool Fits**

```
┌───────────────────────────────────────────────────────────────┐
│                                                               │
│   OPERATOR SCREEN (Next.js 15)                                │
│   ┌─────────────┐  ┌─────────────┐  ┌─────────────────┐      │
│   │ Create Deal │  │  Dashboard  │  │  Leaderboard    │      │
│   │ Form        │  │  Gain/Loss  │  │  Best → Worst   │      │
│   └──────┬──────┘  └──────┬──────┘  └────────┬────────┘      │
│          │                │                   │               │
└──────────┼────────────────┼───────────────────┼───────────────┘
           │                │                   │
           ▼                ▼                   ▼
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   BRAIN — AI ENGINE (Genkit)                                │
│                                                             │
│   • Adds up the Cost (TDC)                                  │
│   • Adds up the Return (TDR)                                │
│   • Calculates ROI                                          │
│   • Gives the verdict: Repeat / Scale / Stop                │
│                                                             │
└────────────────────────────┬────────────────────────────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
        ▼                    ▼                    ▼
  ┌───────────┐      ┌────────────┐      ┌─────────────┐
  │ Dub.co    │      │ Apify      │      │ GA4         │
  │           │      │            │      │             │
  │ Tracks    │      │ Scrapes    │      │ Confirms    │
  │ clicks &  │      │ views &    │      │ real users  │
  │ sales     │      │ likes      │      │ not bots    │
  └─────┬─────┘      └─────┬──────┘      └──────┬──────┘
        │                   │                    │
        └───────────────────┼────────────────────┘
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   DATABASE — SUPABASE                                       │
│                                                             │
│   Stores everything:                                        │
│   • Every deal (who, what, when)                            │
│   • Every line item (each comp, cash, or trade + $ value)   │
│   • Every result (clicks, sales, views, ROI)                │
│   • Every influencer's score and verdict history            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

### **One Sentence Summary**

> The operator logs what they gave, the system tracks what came back, the AI compares the two numbers, and tells the operator: **do it again, do it bigger, or don't do it again.**

---

## **Tech Stack**

| Layer | Tool | What It Does (Simply) |
| :---- | :---- | :---- |
| **Screen** | Next.js 15 | What the operator sees — forms, charts, leaderboard |
| **Brain** | Genkit | The AI that does the math and gives the verdict |
| **Storage** | Supabase | Saves every deal, every item, every result |
| **Link Tracking** | Dub.co API | Counts clicks and sales from influencer links |
| **Social Data** | Apify | Grabs views and likes from influencer posts |
| **Traffic Proof** | GA4 | Proves the visitors were real people, not bots |
](https://excalidraw.com/#room=1c8767beff97180f3f81,wfZe2nla1ZjZSqGffvBhXg)
