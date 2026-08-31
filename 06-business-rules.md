# Business Rules

Formal business rule register governing how churn risk is calculated,
segmented, and acted upon. Rule IDs are referenced from requirements and
use cases where applicable.

| ID | Business Rule | Rationale |
|---|---|---|
| BR-01 | A customer is classified as **"at-risk"** if their model-predicted churn probability exceeds the top-decile threshold for their platform segment (ABB), recalculated monthly. | Focuses retention effort on the highest-risk 10% rather than an arbitrary fixed score. |
| BR-02 | A customer is classified as having **"low digital engagement"** if their `digital_engagement_score` falls in the bottom quartile of their platform's distribution. | Engagement quartiles (see `sql/churn_queries.sql`, query #3) are the primary leading indicator identified in the analysis. |
| BR-03 | A customer flagged with `uses_competitor_platform = 1` **and** in the bottom half of `digital_engagement_score` shall be escalated to the **"High Priority — Competitive Leakage"** segment. | Dual-usage combined with declining engagement is the strongest observed pre-churn signal. |
| BR-04 | A customer with 4 or more `customer_service_calls_per_year` **or** any unresolved complaint shall be routed to the CX team's proactive resolution queue, independent of their churn score. | Service friction is a controllable, near-term driver distinct from long-term engagement decline. |
| BR-05 | Retention outreach shall not be triggered more than once per customer within a rolling 90-day period, unless the customer's risk segment changes. | Prevents outreach fatigue and preserves customer experience. |
| BR-06 | A customer's risk score and segment shall be recalculated on a monthly cycle; scores are not updated in real time. | Balances timeliness with system load and data stability (see NFR-03). |
| BR-07 | Customers who have been with ABB less than 12 months and show zero mobile app logins in their first 30 days shall automatically enter the "New Customer Activation" outreach track, regardless of overall risk score. | Addresses the early-lifecycle drop-off window identified as highest-risk in the tenure cohort analysis. |

## Rule Ownership

| Rule | Owner (Accountable) |
|---|---|
| BR-01, BR-02, BR-03 | Data/Analytics Team (scoring logic), approved by Retention & CRM Team |
| BR-04 | CX Team |
| BR-05 | Retention & CRM Team |
| BR-06 | Data/Analytics Team |
| BR-07 | Digital Channels / Product Team, approved by Retention & CRM Team |

## Change Control

Any change to a business rule's threshold (e.g., adjusting the "top-decile"
in BR-01) requires sign-off from the Retention & CRM Team lead and should be
re-validated against the model's precision/recall trade-off (see
`10_kpi_and_evaluation.md`) before deployment.
