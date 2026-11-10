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
2. **Statistical profiling** — Univariate analysis (distribution, normality) of each series, histograms and boxplots to illustrate distribution and outliers; bivariate analysis (Pearson and Spearman correlation, scatterplot) between transit time and dwell time.
3. **Event documentation** — Identify start/end windows for the three disruption events from external, independently verifiable sources (Transport Canada annual reports, CBC, Supply Chain Dive).
4. **Benchmark construction** — Calculate a fixed 12-month pre-event average for each event (not a single global baseline), since transit time is non-stationary over the full study period.
5. **Impact measurement (RQ1)** — Calculate deviation for each event month against its pre-event benchmark; measure peak excess and duration.
6. **Impact decomposition (RQ2)** — Compare the change in West Coast dwell time to the change in total transit time for each event.
7. **Lead-time and anticipation analysis (RQ3)** — Calculate the additional lead time needed during each event to cover actual transit time in 95% of months; test, via a leave-one-out comparison across the three events, whether an event's early trajectory can reasonably anticipate its eventual severity and duration, or whether a different rule would be a better predictor.
8. **Synthesis** — Produce an event-comparison table (impact size, duration, dwell contribution, anticipated lead-time buffer) as the project's primary decision-support deliverable.

## Key Results

- **RQ1:** Peak transit time rose above each event's 12-month pre-event benchmark by 9.48 days for the COVID surge (July 2021), 16.46 days for the B.C. floods (January 2022) and 6.37 days for the ILWU strike (July 2023). The floods were the largest and fastest, at about 49% above benchmark.
- **RQ2:** Port dwell made up about 7% of the added time during COVID, 26% during the floods and 22% during the strike. In every event, most of the added time came from stages other than port dwell.
- **RQ3:** With event windows of 16, 3 and 2 months, covering 95% of months means covering all of them, so each buffer equals the event's peak. In a leave-one-event-out test, the scaling rule had the lowest error for COVID (1.68 days) and the floods (4.1 days). These are individual comparisons from only three events, not a validated accuracy figure.

## Repository Structure

├── data/
│ └── transit_dwell_pivoted.csv # Cleaned, pivoted dataset (93 months)
├── notebooks/
│ └──CIND_820_Data_Profiling.ipynb
│ └── Data Analysis.ipynb
├── reports/
│ ├── CIND 820 Data Profiling.html
│ ├── Data Analysis compiled code.html # Compiled notebook
│ └── Wickens_Julia_InitialResults.pdf # Initial Results Report
└── README.md


## How to Run

1. Open the notebook in Google Colab.
2. Upload `data/transit_dwell_pivoted.csv` to the Colab session (folder icon on the left).
3. Install the requirements if needed: `pip install pandas matplotlib`.
4. Choose Runtime → Run all.

## Code Structure

The analysis uses functions defined in the notebook for the benchmark, deviation, buffer and leave-one-event-out baseline calculations. Inheritance was not used because the analysis has no class hierarchy to model.

## Links

- Video: (https://drive.google.com/file/d/1laoaENrl_OhaEbIyDal6_H_oVGSMaHxL/view?usp=sharing)
- Initial Results Report (PDF): see `reports/`

## EDA Report

- [EDA Report (HTML)](reports/CIND 820 Data Profiling.html)

