# 09. Acceptance Criteria

Given/When/Then acceptance criteria for each user story in
`08_use_cases_and_user_stories.md`.

## US-01 — View top at-risk customers ranked by churn probability

- **Given** the monthly scoring cycle has completed
  **When** Rana opens the At-Risk Customer List page
  **Then** customers are displayed sorted by descending churn probability, limited to the ABB platform.

- **Given** Rana applies a segment filter (e.g., "Competitive Leakage")
  **When** the filter is active
  **Then** only customers matching that segment (per BR-03) are shown.

## US-02 — See primary churn driver per customer

- **Given** a customer is flagged as at-risk
  **When** Rana selects that customer from the list
  **Then** the system displays the top contributing driver(s) (e.g., low engagement score, low NPS, high service calls) based on the model's feature importance for that customer.

## US-03 — Log outreach action taken

- **Given** Rana has contacted a flagged customer
  **When** she logs the outreach action (channel, date, outcome)
  **Then** the action is saved and timestamped, and the customer is excluded from new outreach for 90 days (BR-05) unless their segment changes.

## US-04 — See risk score during a live service call

- **Given** Tural is handling an inbound service call
  **When** he opens the customer's profile
  **Then** the current churn-risk score and segment are visible in read-only form (NFR-01), without exposing the underlying model internals.

## US-05 — Automatic routing to CX resolution queue

- **Given** a customer records a 4th service call in the current year, or files an unresolved complaint
  **When** the monthly (or trigger-based) rule evaluation runs
  **Then** the customer is automatically added to the CX Proactive Resolution queue (BR-04), independent of their overall churn score.

## US-06 — View engagement-driver trends

- **Given** Sabina opens the Engagement & Risk Segmentation dashboard page
  **When** she selects a date range
  **Then** she sees digital engagement score distributions split by churn outcome, and churn rate by engagement quartile (per SQL query #3).

## US-07 — Executive churn dashboard

- **Given** Elvin opens the Executive Overview dashboard page
  **When** the page loads
  **Then** he sees overall churn rate, month-over-month trend, at-risk customer count, and churn rate by platform — all within 5 seconds (NFR-04).

## US-08 — New customer activation nudge

- **Given** a customer's tenure is less than 12 months
  **And** they have zero mobile app logins in their first 30 days
  **When** the monthly scoring cycle runs
  **Then** the customer is automatically placed into the "New Customer Activation" track (BR-07) and excluded from other risk segments until this track completes.

## US-09 — Automated monthly re-scoring

- **Given** it is the scheduled monthly refresh date
  **When** the batch job executes
  **Then** all active ABB customers receive an updated engagement score and churn probability, business rules (BR-01–BR-07) are re-evaluated, and the dashboard reflects the new data within the defined batch window (NFR-03).
