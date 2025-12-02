# Dataset

Using the Looker E-commerce BigQuery dataset from Kaggle.

## Download

Get it here: https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset

Download the CSV files and drop them in this folder.

## Files You Need

```
data/
├── users.csv                   # 100,000 customers
├── orders.csv                  # 125,226 orders
├── order_items.csv             # 181,759 line items (main analysis data)
├── products.csv                # 29,120 products
├── inventory_items.csv         # 490,705 inventory records
├── events.csv                  # 2,431,963 user events
└── distribution_centers.csv    # 10 warehouses
```

## What I Actually Used

For the customer segmentation and product analysis, I mainly worked with:
- **order_items.csv** (181,759 transactions)
- **orders.csv** (125,226 orders)
- **users.csv** (100,000 customers)
- **products.csv** (29,120 products)

The events and inventory tables are in the dataset but weren't needed for this analysis.

## Quick Schema

**users.csv**: Customer data (id, name, email, age, gender, country)  
**orders.csv**: Order info (order_id, user_id, status, timestamps)  
**order_items.csv**: What was bought (product_id, sale_price, order_id)  
**products.csv**: Product catalog (id, name, category, cost, retail_price)  
**inventory_items.csv**: Stock records (id, product_id, timestamps)  
**events.csv**: User activity (event_type, user_id, timestamps)  
**distribution_centers.csv**: Warehouse locations (id, name, lat/long)

## Data Issues I Fixed

- Timestamps had timezone suffixes that broke Spark's parser (stripped with regex)
- Price/cost fields came in as strings (cast to doubles)
- Age column needed int casting
- Some orders have null `returned_at` values (that's fine)

## Auto-Download

The notebook downloads via kagglehub:

```python
import kagglehub
dataset_path = kagglehub.dataset_download("mustafakeser4/looker-ecommerce-bigquery-dataset")
```

If that doesn't work, manually download from the Kaggle link above.
