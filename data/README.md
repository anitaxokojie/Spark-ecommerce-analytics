# Dataset Information

## Looker E-commerce Dataset

This project uses the Looker E-commerce dataset from Kaggle.

### Download Instructions

1. Visit [Kaggle Dataset](https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset)
2. Download the CSV files
3. Place them in this directory

### Expected Files
data/
├── users.csv                    # 112,460 customer records
├── orders.csv                   # 50,560 order records
├── order_items.csv             # 37,506 line items
├── products.csv                # 14,224 products
├── inventory_items.csv         # 21,917 inventory records
├── events.csv                  # 307,848 user events
├── distribution_centers.csv    # 10 distribution centers
└── README.md

### Quick Start

For faster execution, the notebook includes code to sample 10% of the data:
```python
# Reduces processing time from 30-40 minutes to 3-5 minutes
dataframes[table] = dataframes[table].sample(fraction=0.1, seed=42)
