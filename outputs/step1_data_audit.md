# Step 1: Database Ingestion & Data Quality Audit Report

## 1. Overview

A dedicated local SQLite database (`delivery_assessment.db`) was successfully created to consolidate all historical operational data, cost parameters, business rules, and volume forecasts. All source files were ingested without truncation or data type distortion.

## 2. Ingested Tables & Verification

| Table Name | Row Count | Primary Key / Key Fields | Source File | Status |
|---|---|---|---|---|
| `agent_salary` | 2 | `salary_type` (PK) | `cost_sheet.xlsx` (`agent_salary`) | Verified clean |
| `agents` | 64 | `agent_id` (PK), `hub_id` (FK) | `agents.csv` / `agents.xlsx` | Verified clean |
| `costs` | 5 | `what` (PK) | `cost_sheet.xlsx` (`costs`) | Verified clean |
| `hubs` | 6 | `hub_id` (PK) | `hubs.csv` / `hubs.xlsx` | Verified clean |
| `order_logs` | 51,190 | `log_id` (PK), `order_id`, `agent_id` | `order_logs.csv` / `order_logs.xlsx` | Verified clean |
| `orders` | 22,789 | `order_id` (PK), `hub_id` (FK) | `orders.csv` / `orders.xlsx` | Verified clean |
| `rules` | 8 | `rule` (PK) | `cost_sheet.xlsx` (`rules`) | Verified clean |
| `volume_forecast` | 24 | `hub_id`, `week_start` | `volume_forecast.csv` / `volume_forecast.xlsx` | Verified clean |

## 3. Schema & Referential Integrity Checks

- **Hub Coverage**: Exactly 6 hubs across 3 clusters (Cluster A: Greenfield H01, Lakeview H02; Cluster B: Riverside H03, Hillcrest H04; Cluster C: Brookside H05, Westwood H06).
- **Agent Master**: 64 total agents. 62 are `Active`, and 2 are `Inactive` (one at H01, one at H06). Per business rules, inactive agents departed at the end of Week 1.
- **Order & Log Consistency**: All 25,595 `Assigned` events in `order_logs` map to exactly one follow-up outcome (`Delivered`, `Hold`, or `Returned`). Exactly 22,789 unique orders were recorded in `orders`.
- **Foreign Key Integrity**: 100% of orders, logs, and agents reference valid hubs, orders, and agents without orphans or missing foreign keys.
- **Temporal Bounds**: Historical operational logs span exactly `2026-10-13 08:00:00` to `2026-10-26 20:18:00` (14 days: Week 1 = Oct 13-19, Week 2 = Oct 20-26). Forecast spans `2026-10-27` to `2026-11-23` (4 weeks).
- **Index Optimization**: B-tree indexes added to `order_logs(order_id)`, `order_logs(agent_id)`, `order_logs(status)`, `order_logs(event_time)`, `orders(hub_id)`, `orders(created_at)`, and `agents(hub_id)` for high performance.
