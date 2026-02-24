# IT Helpdesk & SLA Performance Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)


---

## Overview

Power BI dashboard analyzing **1,000 IT support tickets** from FY2024. Built to help IT managers monitor SLA compliance, agent workload, and ticket trends across categories, clients, and channels.

<img width="1204" height="674" alt="Captura de pantalla 2026-02-24 172859" src="https://github.com/user-attachments/assets/e21b4991-050f-4697-8c1b-fa848452859b" />


---

## Data Model

Star schema with one fact table and four dimensions: `Dim_Agents`, `Dim_Categories`, `Dim_Clients`, and a `Calendar` table built in DAX. All relationships are many-to-one with single-direction filtering.

<img width="999" height="754" alt="Captura de pantalla 2026-02-24 174818" src="https://github.com/user-attachments/assets/70777c84-a943-401a-9c80-09ea46cc653e" />

---

## Key Measures (DAX)

```dax
Total Tickets = COUNTROWS(Fact_Tickets)

SLA Compliance % =
DIVIDE(
    COUNTROWS(FILTER(Fact_Tickets, Fact_Tickets[SLA_Met] = "Yes")),
    [Total Tickets]
)

Avg Resolution (hrs) = AVERAGE(Fact_Tickets[Resolution_Hours])

Open Tickets =
CALCULATE([Total Tickets], Fact_Tickets[Status] <> "Closed")

Avg Satisfaction =
AVERAGEX(
    FILTER(Fact_Tickets, Fact_Tickets[Customer_Satisfaction] <> BLANK()),
    Fact_Tickets[Customer_Satisfaction]
)
```

---

## Dashboard Visuals

- **KPI Cards** — Total Tickets, SLA Compliance %, Avg Resolution Time, Avg Satisfaction, Open Tickets
- **Line Chart** — Ticket volume trend by month
- **Bar Charts** — Tickets by agent and by category
- **Donut Chart** — Distribution by priority (Critical / High / Medium / Low)
- **Slicers** — Status, Priority, Channel, Month

---

*Dataset is simulated for portfolio purposes.*
