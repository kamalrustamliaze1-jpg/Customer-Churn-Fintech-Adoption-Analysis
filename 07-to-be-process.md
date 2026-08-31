# 07. To-Be Process & Solution

## Target-State Vision

Shift ABB's churn management from **reactive** (detecting attrition after
it happens) to **proactive** (detecting declining engagement and
intervening before churn occurs) — closing the gap with fintech competitors
like m10, whose fully digital model makes engagement drop-off visible
almost immediately.

## To-Be Process Map

```mermaid
flowchart TB
    A([Customer onboarded]) --> B[Monthly automated scoring:<br/>engagement score + churn probability<br/>BR-01, BR-02, BR-06]
    B --> C{Risk segment?}
    C -- New customer, low activation --> D[New Customer Activation track<br/>BR-07]
    C -- Dual-platform + low engagement --> E[High Priority —<br/>Competitive Leakage queue<br/>BR-03]
    C -- Service friction flagged --> F[CX Proactive Resolution queue<br/>BR-04]
    C -- General at-risk --> G[Retention & CRM<br/>targeted outreach<br/>BR-05]
    C -- Low risk --> H[Continue standard monitoring]
    D --> I[Outreach logged]
    E --> I
    F --> I
    G --> I
    I --> J{Engagement improves<br/>next cycle?}
    J -- Yes --> H
    J -- No --> K[Re-segment / escalate]
    K --> B
```

## As-Is vs To-Be Comparison

| Dimension | As-Is | To-Be |
|---|---|---|
| Detection trigger | Account closure or customer-initiated complaint | Monthly engagement + churn-probability scoring (leading indicator) |
| Data used | None systematically — ad hoc complaint records | Behavior, engagement, experience, and competitive-exposure data |
| Segmentation | None — customers handled individually as they contact ABB | Rule-based segments: New Activation, Competitive Leakage, Service Friction, General At-Risk |
| Ownership | CX team handles complaints in isolation | Cross-functional: Retention/CRM, CX, Digital, Data/Analytics (see RACI) |
| Outreach | Reactive, generic | Proactive, driver-specific, frequency-controlled (BR-05) |
| Visibility | No dashboard; churn known only in hindsight | Monthly-refreshed dashboard (see `03_data_and_dashboard.md`) |
| Feedback loop | None | Outreach outcomes logged and fed back into re-segmentation (FR-07) |

## Target Solution Architecture

```mermaid
flowchart LR
    subgraph Sources["Data Sources"]
        S1[Core Banking /<br/>Transaction Data]
        S2[Mobile App<br/>Engagement Logs]
        S3[CX / Complaint<br/>System]
        S4[Branch Visit<br/>Records]
    end
    subgraph Pipeline["Analytics Layer"]
        P1[Monthly ETL &<br/>Feature Build]
        P2[Churn Scoring Model<br/>Logistic Reg. / Random Forest]
        P3[Business Rules Engine<br/>BR-01 to BR-07]
    end
    subgraph Consumption["Consumption Layer"]
        D1[Executive Dashboard]
        D2[At-Risk Customer List<br/>Retention/CRM]
        D3[CX Read-Only View]
    end
    Sources --> Pipeline --> Consumption
```

## Key Design Decisions

1. **Monthly batch scoring**, not real-time — matches the analytical
   maturity of the current data landscape and avoids core-system load
   (NFR-03).
2. **Rule-based segmentation on top of a statistical model** — keeps the
   system explainable to non-technical business users (NFR-08) while still
   leveraging the predictive model's ranking power.
3. **Cross-functional ownership** — no single team can act on all churn
   drivers alone; the To-Be process explicitly routes segments to the team
   best positioned to act (Retention, CX, or Digital/Product).
