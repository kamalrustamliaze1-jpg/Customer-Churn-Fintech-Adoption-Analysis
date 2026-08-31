# Use Cases & User Stories

## Personas

| Persona | Description |
|---|---|
| **Rana — Retention & CRM Specialist** | Runs day-to-day retention outreach; needs a prioritized, explainable list of at-risk customers. |
| **Tural — CX Team Lead** | Manages complaint resolution; needs visibility into which customers' service issues carry churn risk. |
| **Sabina — Digital Product Manager** | Owns the mobile app roadmap; needs evidence on which engagement features move the needle on retention. |
| **Elvin — Retail Banking Director** | Sponsor; needs a high-level, trustworthy view of churn trends and program impact. |

## Use Case Catalog

| ID | Use Case | Primary Actor |
|---|---|---|
| UC-01 | View prioritized at-risk customer list | Rana (Retention) |
| UC-02 | Drill into a customer's risk drivers | Rana (Retention) |
| UC-03 | Route a flagged customer to CX resolution queue | System (automated, per BR-04) |
| UC-04 | View churn-risk context during a service call | Tural (CX) |
| UC-05 | View engagement-driver trends for product decisions | Sabina (Digital Product) |
| UC-06 | View executive churn dashboard | Elvin (Retail Banking Director) |
| UC-07 | Log outreach action taken on a flagged customer | Rana (Retention) |
| UC-08 | Monthly automated re-scoring and re-segmentation | System (automated) |

## Use Case Detail — UC-01

**Use Case:** View prioritized at-risk customer list
**Actor:** Rana (Retention & CRM Specialist)
**Preconditions:** Monthly scoring cycle has completed (UC-08); Rana has Retention-role dashboard access (NFR-01).
**Main Flow:**
1. Rana opens the "At-Risk Customer List" dashboard page.
2. The system displays customers ranked by churn probability, with segment tags (BR-01–BR-04).
3. Rana filters by segment (e.g., "Competitive Leakage") and city tier.
4. Rana selects a customer to view driver detail (→ UC-02).

**Postcondition:** Rana has an actionable, prioritized list to plan outreach against.

## User Stories

| ID | As a... | I want to... | So that... | Related Use Case |
|---|---|---|---|---|
| US-01 | Retention Specialist | see the top-decile at-risk ABB customers ranked by churn probability | I can prioritize my outreach effort | UC-01 |
| US-02 | Retention Specialist | see the primary churn driver for each flagged customer (engagement, NPS, service friction) | I can tailor my outreach message | UC-02 |
| US-03 | Retention Specialist | log the outreach action I took on a customer | future re-scoring can account for recent contact (BR-05) | UC-07 |
| US-04 | CX Team Lead | see a customer's risk score and driver during a live service call | I can escalate or de-prioritize appropriately | UC-04 |
| US-05 | CX Team Lead | have customers with repeated service calls automatically routed to my resolution queue | I don't have to manually search for them (BR-04) | UC-03 |
| US-06 | Digital Product Manager | see which engagement behaviors most correlate with retention | I can prioritize app features that reduce churn | UC-05 |
| US-07 | Retail Banking Director | see overall churn rate trend and program impact on a single dashboard page | I can report on the retention program to leadership | UC-06 |
| US-08 | New Customer (implicit persona) | receive helpful onboarding nudges if I haven't used the app in my first 30 days | I get value from ABB's digital services early (BR-07) | UC-08 |
| US-09 | Data/Analytics Team member | have the churn model and scoring pipeline re-run automatically each month | risk segments stay current without manual effort | UC-08 |
