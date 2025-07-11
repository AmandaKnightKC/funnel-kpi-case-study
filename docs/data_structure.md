# 📊 Dataset Structure Overview

This project uses simulated sales performance data for Medicare insurance agents. Below is a breakdown of each dataset and its schema.

---

## agent_data.xlsx  

**Description**: Agent-level metadata  
**Rows**: 30 records | 7 columns

| Column     | Type   | Description                             |
|------------|--------|-----------------------------------------|
| agent_id   | int64  | Unique agent identifier                 |
| agent_name | object | Full name of the agent                  |
| agent_ramp | object | Ramp stage: `ramp_0` → `tenured`       |
| start_date | date   | When the agent joined the organization  |
| term_date  | string | When the agent left the organization    |

---

## agent_quota.xlsx  

**Description**: Sales quota expectations per product and ramp stage  
**Rows**: 27 records | 6 columns

| Column           | Type   | Description                                 |
|------------------|--------|---------------------------------------------|
| start_date       | date   | Quota period start                          |
| end_date         | date   | Quota period end                            |
| product          | object | Product type (e.g., Medicare Advantage)     |
| ramp_month_code  | object | Ramp identifier (e.g., `ramp_0`, `ramp_1`)  |
| sales_quota      | int64  | Monthly quota target                        |

---

## marketing_leads.xlsx  

**Description**: Lead records, including creation and contact status, from 178 unique sources  
**Rows**: 110,887 records | 7 columns

| Column              | Type       | Description                              |
|---------------------|------------|------------------------------------------|
| lead_id             | int64      | Unique ID for each potential customer    |
| cost                | float64    | Cost per lead to the organization        |
| lead_source         | object     | Origin or platform of the lead           |
| agent_id            | float64    | Assigned agent                           |
| lead_creation_date  | datetime64 | When the lead entered the system         |
| contact_timestamp   | date       | When the agent made contact (if any)     |

---

## quotes.xlsx  

**Description**: Quotes provided for up to 3 products per contacted lead  
**Rows**: 1,789 records | 6 columns

| Column        | Type   | Description                                 |
|---------------|--------|---------------------------------------------|
| agent_sf_id   | object | PeopleSoft agent ID                         |
| agent_name    | object | Full name of the agent                      |
| quote_id      | string | Unique quote identifier (PeopleSoft)       |
| product_name  | object | Product quoted                              |
| lead_id       | float64| Lead that received the quote                |
| created_date  | date   | Timestamp when the quote was created        |

---

## applications.xlsx  

**Description**: Application submissions tied to leads and products  
**Rows**: 1,226 records | 6 columns

| Column              | Type    | Description                              |
|---------------------|---------|------------------------------------------|
| agent_sf_id         | object  | PeopleSoft agent ID                      |
| application_id      | object  | Unique application record (PeopleSoft)   |
| agent_id            | int64   | Agent who submitted the application      |
| product_name        | object  | Product applied for                      |
| lead_id             | float64 | Lead the application belongs to          |
| submitted_timestamp | date    | Date application was submitted           |

---

## 🔁 Relationships Between Tables

- `agent_id` connects: `agent_data`, `marketing_leads`, `quotes`, `applications`
- `lead_id` connects: `marketing_leads`, `quotes`, `applications`
- `product_name` used in: `quotes`, `applications`, and compared with `agent_quota`
