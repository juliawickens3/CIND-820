# Disruption Impact Analysis and Decision Response

**Job simulation track:** Supply Chain Analyst at a Canadian retail company that imports products from Asia

## Problem

Retail companies must receive imported inventory on time to prevent stocking out. Stockouts not only lead to loss of revenue for the company, but also potentially prevent customers from receiving the things they need. When importing inventory from overseas, lead times can be greatly affected by disruptions such as strikes, natural disasters, and other major world events. These delays interrupt the flow of inventory and cause a lack of predictability for retailers and customers.


## Research Questions

1. How did the COVID-19 demand surge (August 2020-November 2021), the B.C. floods (December 2021-February 2022), and the ILWU port strike (July-August 2023) impact the Shanghai-to-Toronto shipping transit time when measured against the 12 months preceding the event’s onset? How quickly did the average lead times increase and how many days were added at the peak of the issue?
2. How much of the added transit time was due to port dwell at the B.C. ports versus other stages (ocean and rail)?
3. How many extra days would have needed to be added to the transit lead time during each of these events to cover 95% of months? How much additional lead time should a planner anticipate needing in the early months of a similar future disruption, before its full impact is known? 

## Dataset

**Source:** Transportation Supply Chain Performance, Table 23-10-0271-01, Statistics Canada, published via the Government of Canada Open Government Portal.
**Link:** https://open.canada.ca/data/en/dataset/59700495-8526-403c-88b6-b0fa8d574297
 (table view: https://www150.statcan.gc.ca/t1/tbl1/en/tv.action?pid=2310027101)
**Accessed:** September 23, 2026

**Coverage:** January 2017 – September 2024, monthly (93 observations per series)

**Series used:**
- End-to-end container transit time, Shanghai to Toronto via West Coast ports (days)
- Port dwell time, West Coast ports (days)

No personally identifiable information is present; the data consists of aggregated, route-level performance indicators only. Full data biography, provenance trail, constraints analysis, and ethics/privacy review are provided in the project report.

## Planned Approach

1. **Acquisition & preparation** — Download the raw long-format CSV; pivot the two relevant series into a wide, monthly time-indexed table (`transit_dwell_pivoted.csv`); verify no missing values.
2. **Statistical profiling** — Univariate analysis (distribution, skew, normality) of each series; bivariate analysis (Pearson and Spearman correlation, scatterplot) between transit time and dwell time.
3. **Event documentation** — Identify start/end windows for the three disruption events from external, independently verifiable sources (Transport Canada annual reports, CBC, Supply Chain Dive, Canadian Chamber of Commerce).
4. **Benchmark construction** — Calculate a fixed 12-month pre-event average for each event (not a single global baseline), since transit time is non-stationary over the full study period.
5. **Impact measurement (RQ1)** — Calculate excess days for each event month against its pre-event benchmark; measure peak excess and duration.
6. **Impact decomposition (RQ2)** — Compare the change in West Coast dwell time to the change in total transit time for each event.
7. **Lead-time and anticipation analysis (RQ3)** — Calculate the additional lead time needed during each event to cover actual transit time in 95% of months; test, via a leave-one-out comparison across the three events, whether an event's early trajectory can reasonably anticipate its eventual severity and duration.
8. **Synthesis** — Produce an event-comparison table (impact size, duration, dwell contribution, anticipated lead-time buffer) as the project's primary decision-support deliverable.


