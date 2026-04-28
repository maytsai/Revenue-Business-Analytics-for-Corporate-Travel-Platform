
# 1. Data Overview

### Goal:
Get a high-level understanding of the dataset — record counts, date range, product mix, and booking type breakdown.

### Analysis:
- Records by product (Air, Hotel, Car)
- Records by booking type
- Booking type breakdown by product

<img width="500" height="324" alt="Screenshot 2026-04-20 at 6 18 28 PM" src="https://github.com/user-attachments/assets/e3a594a4-65da-4358-b983-e684707ea403" />


### Booking Type by Product
Air: Purchase / Exchange / Partial Refund / Refund / Void / Cancel
Car: Cancel / Reserve
Hotel: Purchase / Reserve / Refund / Cancel

| Product | Booking Type   | n         | pct      |
| ------- | -------------- | --------- | -------- |
| Air     | Purchase       | 114286    | 86.9     |
| Air     | Exchange       | 8528      | 6.5      |
| Air     | Partial Refund | 4962      | 3.8      |
| Air     | Refund         | 2898      | 2.2      |
| Air     | Void           | 893       | 0.7      |
| Car     | Reserve        | 53077     | 83.4     |
| **Car** | **Cancel**     | **10560** | **16.6** |
| Hotel   | Purchase       | 72393     | 69.1     |
| Hotel   | Reserve        | 18798     | 17.9     |
| Hotel   | Refund         | 10160     | 9.7      |
| Hotel   | Cancel         | 3445      | 3.3      |

### Insight:
- Air dominates volume, accounting for the largest share of transactions
- Purchase is the primary booking type across all products
- Car has the highest cancellation rate at 16.6%; Hotel shows meaningful refund and cancellation activity at ~ 13%. While Air has only 6.7% loss rate.

# 2. Data Quality Check

### Goal:
Identify nulls, date logic violations, duplicates, revenue outliers, and anomalies — then remove invalid records to create a clean dataset for all downstream analysis.

### Analysis:
**Clear exclusions (wrong data):**
- BOOKING_ID 1973157021 — $100M revenue outlier
- Travel end before travel start — 20 invalid travel windows
- Duplicate booking IDs — 23 records, risk of double-counting

**Conditional exclusions (depends on analysis type):**
- Travel starts before the booking date (3,690 records) — distorts booking date trend analysis
- Zero-amount bookings — exclude for revenue analysis, keep for volume counts

### Insight:
- Exclusions are minimal and well-defined; data quality is largely sound
- Booking_Clean dataset is used for all downstream analysis
  

# 3. Booking Trend Over Time (MoM)
### Goal: 
Identify when booking volume dropped, which products were affected, and how revenue tracks with volume.

### Analysis: 
- Monthly Booking Volume by product
- Monthly Revenue by Booking 
- Month-over-month booking volume change


### Investigation
<img width="1000" height="325" alt="Screenshot 2026-04-23 at 1 00 01 AM" src="https://github.com/user-attachments/assets/6d91e2a2-60a3-4818-bdec-94d9b9b9d11d" />



**Monthly Volume & MoM Change**

| Month   | Total Bookings | MoM Change (%) |
|---------|---------------|----------------|
| 2018-01 | 22,787        | —              |
| 2018-02 | 20,847        | -8.5           |
| 2018-03 | 25,436        | +22.0          |
| 2018-04 | 20,921        | -17.8          |
| 2018-05 | 22,344        | +6.8           |
| 2018-06 | 23,592        | +5.6           |
| 2018-07 | 15,131        | -35.9          |
| 2018-08 | 11,853        | -21.7          |
| 2018-09 | 20,458        | +72.6          |
| 2018-10 | 23,022        | +12.5          |
| 2018-11 | 20,846        | -9.5           |
| 2018-12 | 12,436        | -40.3          |


### Insight:
- July collapsed to **15,131 bookings** — 32% below baseline avg 22,250
- August low volume driven by price spike, not cancellations
- December follows the expected corporate holiday slowdown


# 4. High-Loss Month Booking Deep Dive:
### Goal: 
July is the single largest volume drop month at 32% below baseline. The drop could stem from a spike in booking losses or a collapse in new demand — two problems that require different interventions. Understanding *which* drove July shapes where to act.

### Analysis
- Purchases vs. Loss Rate - July Highlighted
- July Loss Events: Intended Travel month
<img width="1968" height="643" alt="download (9)" src="https://github.com/user-attachments/assets/c0095ba3-d261-4e6a-9c88-3e80b4d33dd7" />


**Monthly Purchases vs Loss Rate**

| Month   | Purchases | Loss Events | Loss Rate (%) |
|---------|-----------|-------------|---------------|
| 2018-01 | 22,787    | 2,684       | 10.5          |
| 2018-02 | 20,847    | 2,469       | 10.6          |
| 2018-03 | 25,436    | 3,233       | 11.3          |
| 2018-04 | 20,921    | 2,806       | 11.8          |
| 2018-05 | 22,344    | 2,630       | 10.5          |
| 2018-06 | 23,592    | 3,089       | 11.6          |
| **2018-07** | **15,131** | **1,997** | **11.7**   |
| 2018-08 | 11,853    | 1,185       | 9.1           |
| 2018-09 | 20,458    | 2,417       | 10.6          |
| 2018-10 | 23,022    | 2,796       | 10.8          |
| 2018-11 | 20,846    | 2,677       | 11.4          |
| 2018-12 | 12,436    | 1,380       | 10.0          |


### Insight: 
- **July loss rate (11.7%) is not exceptional** — demand collapsed 32%, that is the real issue
- **79.7% of July loss events** were for July travel — last-minute pullbacks
- **Hotel losses are 74.7% Refunds** at near-full purchase value — structural policy issue


# 5. High-Loss Product Booking Deep Dive
### Goal: 
Car (16.5%) and Hotel (13.0%) are the two highest-loss products. Each has a distinct workflow:

- **Car** — Reserve/Cancel only; no Purchase confirmation step
- **Hotel** — Losses split between Cancel (pre-stay) and Refund (post-booking adjustment)

Understanding *how* losses occur shapes the right intervention.

## 5.1 Car

### Analysis
- Booking Type Distribution
- Car Cancellations by Lead Time
- Car Cancellation by Amount
<img width="2189" height="649" alt="download (10)" src="https://github.com/user-attachments/assets/4b4b6f0d-0d2f-47bc-a6c6-604209e2170f" />

**Car: Cancel Lead Time**

| Lead Time | n     | Pct (%) |
| --------- | ----- | ------- |
| Same Day  | 1,436 | 13.7    |
| 1–3 Days  | 3,397 | 32.4    |
| 4–7 Days  | 2,464 | 23.5    |
| 8–14 Days | 1,431 | 13.6    |
| 15+ Days  | 1,771 | 16.9    |

### Insight
- Car operates on **Reserve/Cancel only** — no Purchase confirmation step
- **46% of cancels within 0–3 days** of travel start; same-day = 13.7% (1,436 records)
- Same-day spike likely reflects **system-expired holds**, not traveler-initiated cancels
- **99.4% carry real dollar amounts** — genuine financial exposure on every cancel

## 5.2 Hotel

### Analysis
- Hotel Losses: Cancel vs. Refund
- Hotel Losses by Lead Time (days from booking to travel start)
- Hotel Monthly Losses (Cancel + Refund)

<img width="2189" height="649" alt="download (11)" src="https://github.com/user-attachments/assets/d0fadae0-6a8c-4355-8bd2-d4ea1264c0d9" />


| Booking Type | n      | Pct (%) | Avg Amount ($) |     |
| ------------ | ------ | ------- | -------------- | --- |
| Refund       | 10,158 | 74.7    | $ 1,145.78     |     |
| Cancel       | 3,445  | 25.3    | $ 1,331.27     |     |

### Insight
- **74.7% of Hotel losses are Refunds**, not Cancels — suggesting post-booking adjustments or short-notice reversals rather than pre-trip opt-outs
- **Cancels avg $1,331 vs Refunds avg $1,146** — cancellations carry 16% higher per-event cost
- **Refunds cluster in 0–3 days** of travel start (38.6%) — indicative of last-minute reversals or policy-triggered refunds after check-in
- Monthly pattern mirrors overall volume: losses drop proportionally in Jul/Aug/Dec, not disproportionately elevated — Hotel loss rate is a structural, year-round issue
- **Opportunity**: Distinguishing penalty-free cancellations from refund-triggering events could reduce the 74.7% refund share through stricter booking policies

# 6. Revenue Analysis

### Goal: 
Translate monthly booking volume into revenue terms — gross revenue, loss amount, and net revenue. Quantify how much was lost in down months and validate whether revenue spikes align with volume gains.

### Analysis:
- Net Monthly Revenue
- Gross Revenue vs. Losses
- Avg Booking Value per Month

<img width="2299" height="649" alt="download (12)" src="https://github.com/user-attachments/assets/0f311e08-7b8e-4f2a-b95e-b9944d14ee7c" />


**Monthly Revenue Summary**

| Month       | Gross Revenue ($) | Losses ($)    | Net Revenue ($) |
| ----------- | ----------------- | ------------- | --------------- |
| 2018-01     | 38,150,124        | 3,809,036     | 34,811,108      |
| 2018-02     | 36,727,244        | 3,273,688     | 33,933,640      |
| 2018-03     | 44,955,073        | 4,764,370     | 41,042,066      |
| 2018-04     | 37,565,617        | 4,152,596     | 33,945,313      |
| 2018-05     | 40,432,464        | 3,755,429     | 37,264,649      |
| 2018-06     | 42,624,979        | 4,730,847     | 38,475,857      |
| **2018-07** | **29,427,960**    | **3,853,889** | **26,176,661**  |
| 2018-08     | 47,378,653        | 2,208,819     | 45,449,653      |
| 2018-09     | 36,828,507        | 4,083,477     | 33,397,549      |
| 2018-10     | 43,360,916        | 4,479,059     | 39,530,099      |
| 2018-11     | 36,499,801        | 3,558,442     | 33,558,063      |
| 2018-12     | 22,054,263        | 1,924,274     | 20,463,761      |
### Insight
- July net revenue dropped sharply — driven by 32% demand collapse, not a spike in losses
- August revenue spiked despite low volume — avg booking value 3,898 vs normal 1,600–1,870 −July avg volume (1,868) slightly above baseline — essential high-value trips survived


# 7. Customer Behavior
### Goal:
Understand who is driving platform activity by segmenting travelers into frequency tiers based on annual trip count:

- **Frequent (10+)** — core corporate travelers
- **Occasional (3–9)** — periodic business travelers
- **One-time (1–2)** — rare or single-trip travelers

Then break behavior by month to answer two questions: which traveler tiers went missing in July, and whether August's revenue spike was a **statistical artifact, or a pricing or demand shift**. 
### Analysis:
**Traveler Tier Breakdown**
- Traveler Frequency Segmentation (Frequent / Occasional / One-time)
- Traveler Share vs. Revenue Share by Tier
<img width="1256" height="542" alt="Screenshot 2026-04-24 at 12 14 54 AM" src="https://github.com/user-attachments/assets/47277bac-60c0-43a0-a1c2-7a3428318cff" />

**Traveler Tier Summary**

| Traveler Tier    | Travelers | Traveler Share (%) | Revenue Share (%) | Avg Trips | Avg Spend ($) |
|------------------|-----------|--------------------|-------------------|-----------|---------------|
| Frequent (10+)   | 4,171     | 64.4               | 96.3              | 55.4      | 100,439       |
| Occasional (3–9) | 1,339     | 20.7               | 3.1               | 5.6       | 10,049        |
| One-time (1–2)   | 968       | 14.9               | 0.6               | 1.3       | 2,562         |


**July — Traveler Tier Dropout**
- Active Traveler Drop vs. Baseline by Tier
<img width="626" height="547" alt="Screenshot 2026-04-24 at 12 15 26 AM 1" src="https://github.com/user-attachments/assets/0685e34a-202a-4fb1-a1c6-efb794171777" /><img width="2299" height="672" alt="download (15)" src="https://github.com/user-attachments/assets/386cb4c3-71f7-4878-a894-ff8af236fed2" />


| Traveler Tier    | Baseline | July  | Drop (%) |
| ---------------- | -------- | ----- | -------- |
| Frequent (10+)   | 3,362    | 2,927 | -13.0    |
| Occasional (3–9) | 429      | 261   | -39.1    |
| One-time (1–2)   | 105      | 60    | -42.9    |


**August — Revenue Spike: Real or Artifact?**
- Mean vs. Median Booking Value by Month
- August High-Value Booking Mix — Hypothesis Test
- Avg Booking Value by Traveler (Monthly)
<img width="2299" height="672" alt="download (15)" src="https://github.com/user-attachments/assets/16c875c9-a2c0-44d0-822a-262cc3911bee" />



**Mean vs Median Booking Volume**

| Month       | Mean      | Median  | P90       |
| ----------- | --------- | ------- | --------- |
| 2018-01     | 1,610     | 757     | 3,426     |
| 2018-02     | 1,678     | 760     | 3,497     |
| 2018-03     | 1,692     | 797     | 3,600     |
| 2018-04     | 1,713     | 791     | 3,558     |
| 2018-05     | 1,700     | 809     | 3,493     |
| 2018-06     | 1,722     | 816     | 3,602     |
| **2018-07** | **1,868** | **825** | **3,772** |
| **2018-08** | **3,898** | **801** | **3,613** |
| 2018-09     | 1,691     | 801     | 3,602     |
| 2018-10     | 1,783     | 804     | 3,640     |
| 2018-11     | 1,658     | 786     | 3,444     |
| 2018-12     | 1,690     | 745     | 3,471     |

### Insight

**1. Traveler Tier Breakdown:**
- **Frequent travelers (10+) drive 96.3% of revenue** — 64% of travelers, nearly all the money

**2. July — Traveler Tier Dropout:**
- **July hit the periphery**: Occasional (−39.1%) and One-time (−42.9%) dropped ~3x harder than Frequent (−13.0%)
- Consistent with a **targeted corporate budget freeze** on non-essential trips
- Occasional travelers represent a **volume recovery opportunity**

**3. August — Revenue Spike: Real or Artifact? **
- Composition effect: Frequent traveler avg spiked to 3,961 𝑖𝑛 𝐴𝑢𝑔 𝑣𝑠 1,867 in Jul, but occasional/one-time were normal. Frequent travelers dominating a low-volume month amplify the effect.
- A few large bookings skewing the mean: August booking median = 801, identical to every other month (757– 816 range). The mean of $ 3,898 is entirely driven by outlier high-value bookings at the top end. Therefore, the August spike is a **statistical artifact, not a pricing or demand shift**. Median tells the true story — a typical August booking was no different from any other month.


# Key Findings & Recommendations
### Findings

| # | Finding | Impact |
|---|---------|--------|
| 1 | **July demand collapsed 32%** — 15,131 bookings vs baseline avg 22,250; loss rate was unremarkable | Demand |
| 2 | **79.7% of July cancellations were same-month trips** — last-minute corporate pullbacks | Behaviour |
| 3 | **Occasional & one-time travelers disappeared in July** (−39–43%); frequent travelers barely dipped (−13%) | Segmentation |
| 4 | **Car (16.5%) and Hotel (13.0%) carry elevated loss rates**; Air is lowest at 4.1% | Lost Revenue |
| 5 | **Car same-day cancellation spike** — 13.7% of cancels on travel date; cause (system-expired hold vs traveler-initiated) is unknown without reason codes | Operations |
| 6 | **Hotel losses are 74.7% Refunds** at near-full purchase value — stable ratio year-round | Process |
| 7 | **August mean booking value spiked to $3,898, but median was $801, identical to all other months.** Spike is driven by a handful of outlier bookings, not a genuine pricing shift | Pricing |
| 8 | **Frequent travelers generate 96.3% of revenue** — highly concentrated, high retention risk | Retention |

---

### Recommendations

#### Act — Finding is clear, recommendation is actionable

| #   | Recommendation                                                                                                                                                                                                                                                                                            | Finding |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| 1   | **Protect frequent travelers first** — 96.3% revenue concentration means any churn has outsized impact. Prioritize service quality and policy flexibility for this segment                                                                                                                                | F8      |
| 2   | **Re-engage occasional travelers before next summer** — they are the most volatile segment and the leading indicator of overall volume health                                                                                                                                                             | F3      |
| 3   | **Introduce tiered Car cancellation penalties by lead time** — 46% of cancels occur within 0–3 days and 99.4% carry real dollar amounts. A penalty structure (e.g. waived at 15+ days, partial at 4–14 days, full at 0–3 days) would reduce last-minute exposure without penalizing planned cancellations | F4, F5  |
| 4   | **Audit Hotel refund and cancellation policy** — 74.7% of Hotel losses are Refunds at avg $1,146, stable year-round. Review rate-type policies (flexible vs. non-refundable) to identify where the gap sits and design the right intervention                                                             | F6      |


#### Investigate — Signal is there, root cause unknown

| #   | Question                                                | What We Know                                                                         | What We Need                                                                                                                                                                                                                           |
| --- | ------------------------------------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Why did July demand collapse?**                       | Occasional travelers drove the drop; loss rate was normal — demand fell, not quality | Trip purpose data; corporate budget cycle; industry benchmarks to rule out platform-specific cause                                                                                                                                     |
| 2   | **Are Car same-day cancels system or traveler-driven?** | 1,436 same-day cancels at avg $683; pattern is distinct from other lead time buckets | Cancellation reason codes from the booking system                                                                                                                                                                                      |
| 3   | **What triggers Hotel Refunds over Cancels?**           | Ratio is consistent across all months — structural, not seasonal                     | Rate type at booking (flexible vs. non-refundable); refund reason codes. If refunds are coming from flexible rates, it's a policy design problem; if from non-refundable rates, it's an enforcement problem. Answer determines Act #4. |

#### Watch — Early indicator, not yet actionable

| #   | Signal                                                                                                                                                | Why It Matters |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- |
| 1   | **Occasional traveler booking velocity in May–Jun** — a leading indicator of whether July will repeat                                                 | F1, F3         |
| 2   | **August mean booking value in future low-volume months** — monitor whether outlier high-value bookings are a recurring pattern or a one-off artifact | F7             |














