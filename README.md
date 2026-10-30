# Delivery - On The Go: Data Analyst Technical Assessment

**Candidate:** Karib Shams  
**Phone:** 01797470717  
**Email:** shams321karib@gmail.com  
**Repository:** [https://github.com/karibshams/cb](https://github.com/karibshams/cb)  
**Live Interactive Dashboard:** [https://karibshams.github.io/cb/dashboard/](https://karibshams.github.io/cb/dashboard/)  

---

## Executive Summary & Management Verdict

Following a +21.9% citywide delivery attempt surge in Week 2, hub managers submitted a blanket request to hire 8 new delivery agents. Management must **REJECT** this blanket request:

1. **Budget Violation:** Approving 8 new hires incurs **BDT 175,200** in Month 1 (BDT 40,000 recruitment fees + BDT 135,200 in fixed salaries), exceeding the BDT 70,000 Finance budget by 2.5x.
2. **First-Week Speed Penalty:** New hires operate at only 60% speed during their first 7 days, providing zero immediate relief to current bottlenecks.
3. **Asymmetric Overload & Artificial Load:** Empirical audit of 51,190 delivery logs reveals that only 3 of 6 hubs exceed the 85% planning threshold in Week 2: Greenfield H01 (88.64%), Riverside H03 (90.80%), and Hillcrest H04 (95.87%). Overload at Riverside (H03) is largely artificial: 64.42% of its holds (563 holds) are caused by internal agent-side failures (Late Dispatch, Not Attempted, Time Shortage) that recycle into repeat next-day attempts, draining BDT 37,000 in penalties in Week 2 alone. Meanwhile, Lakeview (H02) in Cluster A operates at just 56.17% utilisation (<75% transfer threshold), holding 4 surplus agents directly adjacent to Greenfield.

### The Recommended 4-Part Plan (100% Budget Compliant):
- **Intra-Cluster Transfer (Cluster A):** Transfer 2 agents from Lakeview (H02) to Greenfield (H01) at BDT 2,000 each (**BDT 4,000 total**). Balances Cluster A with zero added salary overhead and 100% Day-1 productivity.
- **Hold Reduction Programme (Cluster B - Riverside):** Deploy the BDT 15,000 Hold Reduction Programme at Riverside (H03) (**BDT 15,000 total**). Eliminates 50% of agent-side holds (~282 attempts/week), reducing attempts to 2,768/week and staffing need to 11.6 agents (already has 12 active; zero hires needed!).
- **Targeted Recruitment (Cluster B - Hillcrest):** Approve targeted recruitment of 2 agents at Hillcrest (H04) (1 Fixed + 1 Variable = **BDT 46,698 total**). Hillcrest has genuine demand growth (95.87% util), clean operations (only 21.9% agent holds), high productivity (30.88 deliveries/day), and no intra-cluster donor.
- **Performance Coaching (Cluster C - Brookside):** Coach 3 senior return outliers at Brookside (H05) who drive 56.2% of all hub returns (**BDT 0 capital cost**). Eliminates BDT 14,135 in return penalties.

**Financial Return:** Total expenditure is strictly **BDT 65,698** (saving BDT 4,302 as an unallocated reserve). This unlocks **BDT 35,695** in direct cash penalty savings (recovering 54.3% of investment in Month 1) and preserves **BDT 111,461** in delivery revenue, delivering a **+110.2% Net ROI**.

---

## Deliverables Directory Structure

```
.
├── Final_Submission.pdf              # Complete Master Technical Report (Task 1 SQL, Task 2 Q8-Q10, Task 3 & 4)
├── Task4_Executive_Deck.pptx         # 8-slide executive presentation for Head of Operations (PowerPoint)
├── Task4_Executive_Deck.pdf          # 8-slide executive presentation (PDF)
├── README.md                         # Project documentation and summary
├── .gitignore                        # Git exclusion rules
│
├── dashboard/                        # Interactive Operations Intelligence Web Dashboard
│   ├── index.html                    # Dashboard application (100% offline-ready, no login)
│   ├── data.json                     # Bundled JSON dataset
│   └── assets/                       # Locally bundled Chart.js and Tailwind CSS
│
└── outputs/                          # Exported CSV Result Tables (Q1 to Q10)
    ├── q1_daily_productivity.csv     # Q1 daily agent productivity (854 agent-days)
    ├── q1_hub_summary.csv            # Q1 6-hub baseline summary table
    ├── q2_hub_utilisation.csv        # Q2 Week 1 vs Week 2 utilisation & overload status
    ├── q3_hold_reasons.csv           # Q3 Week 2 hold breakdown & top 2 drivers by hub
    ├── q4_held_orders_status.csv     # Q4 conversion funnel of 2,599 held orders
    ├── q5_high_return_agents.csv     # Q5 senior outlier agents with >30d tenure & >15% return ratio
    ├── q6_cost_per_delivered_order.csv# Q6 itemized labor & penalty costs per delivered order
    ├── q7_forecast_agents_needed.csv # Q7 4-week forecast staffing gaps (Baseline vs Adjusted)
    ├── q9_budget_allocation.csv      # Q9 itemized BDT 70,000 budget allocation & ROI model
    └── q10_early_warning_system.csv  # Q10 risk areas, Week 1-2 warning triggers & mitigations
```

---

## Technical Summary of Assessment Tasks

### Task 1: SQL Assessment (Questions Q1 to Q7)
All queries were executed against SQLite (`delivery_assessment.db`) using raw data from `2026-10-13` to `2026-10-26`:
- **Q1 (Daily Productivity):** Evaluated 854 active agent-workdays. Average deliveries per working day ranged from 20.14 (Lakeview) to 30.88 (Hillcrest). Full citywide deliveries reached 19,579 across 882 scheduled available days.
- **Q2 (Hub Utilisation):** Defined as `Total Attempts / (Active Agents * 7 * 40)`. Target is 85.0%. Week 2 overloaded hubs: Hillcrest H04 (95.87%), Riverside H03 (90.80%), Greenfield H01 (88.64%). Eligible donor hub: Lakeview H02 (56.17%).
- **Q3 (Hold Reasons in W2):** City logged 1,720 holds in Week 2. Riverside H03 accounted for 50.8% of all holds (874 holds), with 64.42% (563 holds) being agent-side (Late Dispatch: 312, Not Attempted: 132, Time Shortage: 119).
- **Q4 (Held Orders Conversion):** 2,599 unique orders experienced at least one hold. Overall terminal conversion: 78.41% Delivered, 19.55% Returned, and 2.04% still on Hold at period close.
- **Q5 (High-Return Agents):** Filtered for tenure > 30 days and return ratio > 15.0%. Exactly 3 agents qualified, all located at Brookside (H05): A1045 (26.93%), A1046 (21.98%), and A1047 (17.43%), accounting for 56.2% of hub returns.
- **Q6 (Cost per Delivered Order):** Itemized fixed pay (BDT 650/day worked), variable pay (BDT 300/day + BDT 14/delivery), hold penalties (BDT 30), and return penalties (BDT 55). Week 2 cost per delivered order: Greenfield BDT 26.56, Lakeview BDT 36.16, Riverside BDT 45.67, Hillcrest BDT 27.62, Brookside BDT 37.33, Westwood BDT 27.07.
- **Q7 (Forecast Staffing Gaps):** 4 forecast weeks (Oct 27 – Nov 23). Evaluated baseline (orders / 238) vs attempt-adjusted model (orders * historical multiplier / 238). Peak gaps: H01 (+2), H03 (+1), H04 (+2). Surplus: H02 (-3), H05 (-1). Net citywide gap is only +2 to +3 agents.

### Task 2: Strategic Analysis & Financial Modeling (Q8 to Q10)
- **Q8 (Hiring Request Evaluation):** Evaluated request for 8 agents. Rejected blanket hiring. Approved 2 internal transfers in Cluster A (H02 -> H01), 1 Hold Reduction Programme at Riverside (H03), 2 targeted hires at Hillcrest (H04), and coaching at Brookside (H05).
- **Q9 (BDT 70,000 Budget Allocation):**
  - Intra-cluster transfers (2 agents): BDT 4,000
  - Riverside Hold Reduction Programme: BDT 15,000
  - Hillcrest recruitment fees (2 agents): BDT 10,000
  - Hillcrest Fixed Agent Month-1 salary: BDT 16,900
  - Hillcrest Variable Agent Month-1 pay: BDT 19,798
  - Operational Contingency Reserve: BDT 4,302
  - **Total Spend: BDT 70,000 (100% compliant)**
  - Direct penalty savings of BDT 35,695 recovers 54.3% in Month 1; revenue protected is BDT 111,461 (+110.2% Net ROI).
- **Q10 (Early-Warning Risk System):** Established 5 operational risk areas with numerical triggers for Week 1 & Week 2 and mandated mitigation action plans.

### Task 3: Interactive Dashboard
- Fully functional HTML5/JS dashboard with zero external runtime dependencies.
- Open `dashboard/index.html` in any browser or visit [https://karibshams.github.io/cb/dashboard/](https://karibshams.github.io/cb/dashboard/).

### Task 4: Executive Presentation Deck
- 8-slide executive presentation structured for the Head of Operations (`Task4_Executive_Deck.pptx` and `Task4_Executive_Deck.pdf`).
- Monochrome, minimalist corporate design without decorative fluff.
