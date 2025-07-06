### Dataset Notes – PD vs LGD

The LGD dataset used in this project is based on the **same underlying synthetic dataset** as the PD modeling section. No structural changes were made to the original columns. Instead, the following LGD-specific fields were added to support loss estimation:

- `recovered_amount` – the amount recovered after default  
- `recovery_rate` – proportion of exposure recovered  
- `lgd` – calculated as `1 − recovery_rate`

To simulate realistic data challenges and enable demonstration of validation logic, the LGD dataset includes **intentional data quality issues**, such as:

- Duplicate default records for the same customer-year  
- Missing values in recovery fields  
- Recovery amounts exceeding exposure (leading to LGD < 0)

These modifications are included to reflect real-world issues commonly encountered in LGD data, and to illustrate how to detect and address them in a credit risk modeling pipeline.

> The PD notebook remains unchanged and does not rely on these LGD-specific columns.
