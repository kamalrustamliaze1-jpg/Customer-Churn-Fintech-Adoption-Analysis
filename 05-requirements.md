# Requirements

## Functional Requirements (FR)

| ID | Requirement | Priority |
|---|---|---|
| FR-01 | The system shall calculate a `digital_engagement_score` for each active customer based on app logins and branch visits, refreshed monthly. | Must |
| FR-02 | The system shall calculate a churn-risk score (probability) for each active ABB customer using the trained churn model. | Must |
| FR-03 | The system shall flag customers who are also active on a competitor fintech platform (dual-usage) as a distinct risk segment. | Must |
| FR-04 | The system shall provide a filterable, sortable list of at-risk customers to the Retention & CRM team, ranked by predicted churn probability. | Must |
| FR-05 | The system shall segment at-risk customers by primary churn driver (e.g., low engagement, low NPS, service friction) to support tailored outreach. | Should |
| FR-06 | The dashboard shall display churn rate trends by platform, tenure cohort, and engagement quartile. | Must |
| FR-07 | The system shall log retention outreach actions taken against flagged customers, to support future effectiveness measurement. | Should |
| FR-08 | The system shall allow CX team members to view (read-only) the risk score and driver breakdown for a customer during a service interaction. | Could |
| FR-09 | The system shall support a monthly automated re-scoring and dashboard refresh cycle. | Must |
| FR-10 | The system shall allow filtering the at-risk customer list by city tier and branch, to support field-level retention campaigns. | Could |

## Non-Functional Requirements (NFR)

| ID | Requirement | Category | Priority |
|---|---|---|---|
| NFR-01 | Customer-level risk scores and engagement data shall be accessible only to authorized Retention, CX, and Analytics roles (role-based access control). | Security | Must |
| NFR-02 | Any real-world deployment shall comply with applicable data privacy and banking-sector regulations in Azerbaijan before processing real customer data. | Compliance | Must |
| NFR-03 | The monthly scoring/refresh job shall complete within a defined batch window (e.g., overnight) without impacting core banking system performance. | Performance | Must |
| NFR-04 | The dashboard shall load standard views (Executive Overview) within 5 seconds under normal load. | Performance | Should |
| NFR-05 | The churn model and underlying data pipeline shall be version-controlled and reproducible (as demonstrated by this repository's `notebooks/` scripts). | Maintainability | Must |
| NFR-06 | The system shall maintain an audit trail of who accessed at-risk customer lists and when. | Auditability | Should |
| NFR-07 | The solution shall be designed to scale to ABB's full active customer base, not just a sample. | Scalability | Should |
| NFR-08 | Dashboard visuals and terminology shall be understandable by non-technical business users (Retention, CX teams) without requiring data science expertise. | Usability | Must |

## Traceability Note

Each FR/NFR above maps to a pain point identified in
`04_as_is_process_and_bpmn.md` and is realized in the target architecture in
`07_to_be_process_and_solution.md`. Detailed behavior for each functional
requirement is expanded into use cases and user stories in
`08_use_cases_and_user_stories.md`.
