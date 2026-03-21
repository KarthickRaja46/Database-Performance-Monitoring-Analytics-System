# Database Performance Insights

A Python + MySQL project to simulate real-time system logs, store valid/rejected events, and run structured SQL analytics.

## Project Structure

- `Log_simulator.py` - Live log simulator with validation, DB insert, and CSV export
- `data/system_logs.csv` - Valid log export (header + data)
- `data/rejected_logs.csv` - Rejected log export (header + data)
- `sql/schema.sql` - Database schema and indexes
- `sql/01_basic_analytics.sql` - Basic analytics queries
- `sql/02_advanced_analytics.sql` - Advanced analytics queries
- `sql/03_kpi_analytics.sql` - KPI and ETL quality queries
- `sql/04_master_analytics.sql` - Combined analytics script

## Prerequisites

- Python 3.10+
- MySQL Server running locally
- Python packages:
  - `pandas`
  - `mysql-connector-python`

Install packages:

```bash
pip install pandas mysql-connector-python
```

## Database Setup

1. Open MySQL client or Workbench.
2. Run:

```sql
source sql/schema.sql;
```

This creates:
- `system_logs`
- `rejected_logs`
- `etl_metrics`
- `alerts`
- `alert_threshold_config`
- `system_logs_archive`

## Run Simulator

From project root:

```bash
python Log_simulator.py
```

When prompted, enter your MySQL password.

What it does:
- Generates random realistic logs continuously
- Validates data quality rules
- Inserts valid rows into `system_logs`
- Inserts invalid rows into `rejected_logs`
- Tracks run metrics in `etl_metrics`
- Writes CSV outputs into `data/`

Stop with `CTRL+C` for clean shutdown and buffer flush.

## Run Analytics

Run in this order:

1. `sql/01_basic_analytics.sql`
2. `sql/02_advanced_analytics.sql`
3. `sql/03_kpi_analytics.sql`

Or run all together:

- `sql/04_master_analytics.sql`

## Notes

- CSV headers are auto-ensured in simulator startup.
- Analytics files are split for clarity and ordered execution.
- Main branch is configured for the active GitHub repository.

## Sample Output

Simulator (live):

```text
Live stream started (CTRL+C to stop)
Inserted 3 rows
Inserted 1 rows
Inserted 4 rows
Logs=50 Inserted=42 Rejected=8
```

On stop:

```text
Stopping...
Stream stopped cleanly
```

Example analytics result (basic):

```text
total_requests | 5000
success_rate_pct | 89.40
error_rate_pct | 10.60
avg_latency_sec | 0.482
```
