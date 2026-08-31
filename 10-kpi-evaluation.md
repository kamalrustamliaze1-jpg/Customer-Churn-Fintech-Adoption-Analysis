# KPI & Evaluation

## Project-Level KPIs (Delivery / BA Process)

| KPI | Definition | Target |
|---|---|---|
| Requirements coverage | % of functional requirements (FR-01–FR-10) mapped to at least one use case and acceptance criterion | 100% |
| Documentation completeness | All 11 BA deliverables produced and internally consistent (this suite) | 11 / 11 |
| Model reproducibility | Churn model results reproducible end-to-end via `notebooks/` scripts | Pass / Fail |
| Stakeholder sign-off (illustrative) | Key business rules (BR-01–BR-07) reviewed and approved by rule owners | 100% of rules |

## Business-Level KPIs (Outcome Metrics — for a real deployment)

| KPI | Definition | Baseline (synthetic) | Target Direction |
|---|---|---|---|
| Overall ABB churn rate | % of active customers churning in a 12-month period | ~17.2% | ↓ |
| At-risk segment churn rate | Churn rate within the top-decile flagged segment (BR-01) | Elevated vs. base rate | ↓ after intervention |
| New customer 12-month churn | Churn rate among customers with <12 months tenure | Highest cohort in analysis | ↓ |
| Dual-platform ("competitive leakage") rate | % of active ABB customers also using a competitor wallet | Monitor as leading indicator | Track / ↓ |
| Digital engagement score (median) | Median engagement score across the ABB base | Baseline from `data/customers_synthetic.csv` | ↑ |
| NPS among flagged at-risk customers | Average NPS score before vs. after retention outreach | Below platform average | ↑ post-intervention |
| Retention campaign response rate | % of flagged customers who show improved engagement within 90 days of outreach | N/A (new metric) | Establish baseline, then ↑ |
| CX complaint recurrence rate | % of complaint-flagged customers with a repeat complaint within 90 days | N/A (new metric) | ↓ |

## Model Evaluation Metrics

From `notebooks/churn_analysis.py` (ABB subset, held-out test data):

| Metric | Logistic Regression | Random Forest |
|---|---|---|
| ROC-AUC | ~0.61 | ~0.62 |
| Precision (churn class) | ~0.22 | ~0.27 |
| Recall (churn class) | ~0.52 | ~0.19 |

**Interpretation:** The Random Forest offers a higher AUC and precision,
useful for a high-confidence "top-decile" outreach list (BR-01). The
Logistic Regression's higher recall may be more useful if the business goal
shifts toward casting a wider net at lower individual confidence — a
trade-off to revisit with the Retention team based on outreach capacity.

## Evaluation Cadence

| Review | Frequency | Owner |
|---|---|---|
| Model performance review (AUC, precision/recall drift) | Quarterly | Data/Analytics Team |
| Business KPI review (churn rate, campaign response) | Monthly | Retention & CRM Team, reported to Retail Banking Director |
| Business rule threshold review (BR-01 decile cutoff, etc.) | Semi-annual, or on significant drift | Retention & CRM Team + Data/Analytics |

## Success Criteria for the Overall Initiative

The initiative is considered successful (in a real deployment) if, within
two full quarterly cycles after launch:
1. The at-risk segment shows a measurably lower churn rate than a
   comparable unflagged/control population, and
2. New-customer 12-month churn declines relative to the pre-intervention baseline, and
3. The Retention team reports the driver-segmented outreach (BR-03/BR-04)
   as more actionable than the prior undifferentiated process.
