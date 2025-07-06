## LGD Dataset: Event-Based Simulation

The file `lgd_event_dataset.csv` extends the synthetic PD dataset into an **event-based structure** designed for more realistic LGD modeling.

Each customer appears multiple times, representing their journey through different credit lifecycle events:

- `event_type = "default"` – the year the customer enters default  
- `event_type = "recovery"` – the year recovery occurs after default  

This mirrors how LGD behaves in real-world portfolios where recovery data is typically reported in a **later period** than the default event.

### Added Columns

| Column               | Description                                           |
|----------------------|-------------------------------------------------------|
| `event_type`         | `"default"` or `"recovery"` per customer and year     |
| `recovered_amount`   | Amount recovered after default                        |
| `recovery_rate`      | Share of exposure recovered = `recovered_amount / exposure_at_default` |
| `lgd`                | Loss Given Default = `1 − recovery_rate`              |

### Data Quality Features

This dataset includes realistic validation scenarios:
- Duplicate recovery entries for a customer
- One case where `recovered_amount > exposure` → `LGD < 0`
- One row with missing recovery data

These intentional issues are included to showcase proper LGD data validation logic and to allow downstream cleansing, aggregation, or rule-based handling.

> This file is separate from the original PD dataset and was created purely for LGD modeling demonstration.
