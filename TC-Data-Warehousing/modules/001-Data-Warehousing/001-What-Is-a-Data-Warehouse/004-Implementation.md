## Identifying Warehouse Requirements

Before building anything, the requirements are usually gathered by answering a set of questions.

1. What business questions need to be answered?
2. Which source systems hold the data required to answer them?
3. How far back does historical data need to go?
4. How frequently does the data need to be refreshed?
5. Who will query the warehouse, and using which tools?

## Mapping Sources to a Warehouse

```text
Source: Online Orders System     ->  order data
Source: In Store POS System      ->  transaction data
Source: Loyalty Program Database ->  customer data
                    |
                    v
            Central Data Warehouse
                    |
                    v
        Reports and Dashboards
```

## A Minimal Warehouse Table

Even a simple warehouse table differs from an operational one by keeping history rather than only current state.

```sql
CREATE TABLE warehouse_sales (
    sale_id        INT,
    customer_id    INT,
    product_id     INT,
    sale_date      DATE,
    quantity       INT,
    revenue        DECIMAL(10, 2),
    source_system  VARCHAR(50),
    loaded_at      TIMESTAMP
);
```

The `source_system` and `loaded_at` columns are common in warehouse tables. They record where each row came from and when it arrived, which supports troubleshooting and auditing.