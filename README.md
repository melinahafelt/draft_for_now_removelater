# LGD Dataset: Event-Based Simulation
The file `lgd_event_dataset.csv` extends the synthetic PD dataset into an event-based structure designed to better reflect real-world LGD modeling.
Unlike PD, where each customer typically has one row per snapshot period, the LGD dataset allows multiple rows per customer, capturing the timeline of credit events:
- `event_type = "default"` – the year the customer defaults  
- `event_type = "recovery"` – the year when recovery occurs after default
This structure mirrors how LGD behaves in actual credit portfolios, where recovery data is often reported in a later period than the default event.

## Added Columns
| Column             | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `event_type`        | "default" or "recovery" per customer and year                              |
| `recovered_amount`  | Amount recovered after default                                              |
| `recovery_rate`     | Share of exposure recovered = `recovered_amount / exposure_at_default`     |
| `lgd`               | Loss Given Default = `1 − recovery_rate`                                   |
| `batch_run_date`    | Date when the data batch was generated or updated                          |

## Data Complexity and Preprocessing
Compared to the PD dataset, the LGD dataset is intentionally more complex. It introduces features commonly found in real-world LGD data pipelines that require additional preprocessing:
- Multiple rows per customer (for each event or batch)
- Duplicate recovery entries for the same customer
- One row where `recovered_amount > exposure_at_default`, resulting in `lgd < 0`
- One row with missing recovery data
- Varying `batch_run_date` values across duplicate rows
To address these issues, the data is sorted by `batch_run_date`, and only the latest available record per customer is retained. This simulates real-world conditions where recovery data can be delayed or corrected over time — a common challenge in LGD data preparation.

## LGD vs. PD Modeling
- LGD modeling typically involves fewer statistical validation steps  
- Greater emphasis is placed on data integrity and lifecycle consistency  
- LGD data tends to be event-driven, while PD data is typically snapshot-based

**Note:** This file is separate from the original PD dataset and was created solely for LGD modeling demonstration purposes.
