# E-commerce Customer Segmentation with Apache Spark

Big data project analyzing 180K+ e-commerce transactions using PySpark and K-means clustering.

![Python](https://img.shields.io/badge/python-3.9+-blue)
![Status](https://img.shields.io/badge/status-production-green)
![License](https://img.shields.io/badge/license-MIT-blue)
## What I Built

I used Apache Spark to process e-commerce transactions and segment customers based on their purchasing behavior. The goal was to identify high-value customers and understand which product categories drive the most profit.

**Tech Stack:** PySpark 3.5.5, MLlib, Python 3.12, Jupyter  
**Dataset:** Looker E-commerce BigQuery (180K transactions, 80K customers)

## Main Findings

### Customer Segments (K-means, k=3)

After clustering 80K+ customers by purchase frequency and total spend, I got three distinct groups:

- **Cluster 0 (68%)**: ~54K customers averaging $63 lifetime spend, typically 1-2 orders. Mostly one-time buyers.
- **Cluster 2 (27.5%)**: ~22K customers averaging $236 spend across ~3 orders. Regular customers worth targeting for upsells.
- **Cluster 1 (4.9%)**: ~4K customers averaging $568 spend with 5+ orders. VIP segment that needs retention focus.

The top 5% of customers generate nearly 10x more revenue than the average customer.

### Product Performance

Looking at the top sellers, denim and basics dominate:
- Wrangler Men's Jeans leads with 62 units sold
- Puma Socks at 48 units  
- 7 For All Mankind Jeans at 41 units

For profitability by category (showing top 3):
1. **Outerwear & Coats**: $722K profit with 55% margin
2. **Jeans**: $583K profit with 46% margin
3. **Sweaters**: $437K profit with 52% margin

Outerwear has both high volume and high margin, making it the priority for inventory decisions.

## How to Run
```bash
# Install dependencies
pip install -r requirements.txt

# Download dataset from Kaggle
# https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset

# Open notebook
jupyter notebook PySpark_Ecommerce_Clustering.ipynb
```

The notebook will attempt to download data automatically via kagglehub if you have a Kaggle API token configured. Otherwise, download manually and place CSVs in the `data/` folder.

## Technical Details

### Spark Configuration
Had to configure Spark for Windows - set `PYSPARK_PYTHON` environment variables and allocated 2GB to both executor and driver memory. Used legacy time parser for the timestamp columns since the dataset has timezone suffixes that break the default parser.

### Data Cleaning
The timestamps came in with `+00:00` suffixes that Spark's default parser couldn't handle, so I used regex to strip them before casting. Also had to explicitly cast price and cost columns to `DoubleType` since Spark's schema inference was treating them as strings.

### Joins
Created a comprehensive dataset by joining orders → order_items → products → users. Renamed columns to avoid ambiguous references (like `product_id` appearing in multiple tables). Cached the final dataframe since it gets reused for multiple aggregations.

### ML Pipeline
Used `VectorAssembler` to combine frequency, monetary, and avg_basket features into a single vector. Trained K-means with k=3 (picked 3 based on business context - didn't want too many micro-segments). Used `seed=42` for reproducibility. The model assigns each customer to a cluster, then I aggregated to get the segment statistics.

## Business Recommendations

Based on the segmentation results:

**Cluster 0 (68% of customers, low-value)**  
Run re-engagement campaigns with 15-20% off incentives. These are one-time buyers we need to convert into repeat customers.

**Cluster 2 (27.5%, mid-value)**  
Upsell opportunities here. Try product bundles (jeans + belt combos). These customers are already engaged and worth investing in.

**Cluster 1 (4.9%, high-value)**  
VIP treatment - loyalty program, free shipping, early sale access. Can't afford to lose these customers. Consider quarterly business reviews or personal shoppers.

**Inventory Strategy**  
Stock up on Outerwear since it has both high margin (55%) and solid volume. Jeans are the volume leader but lower margin (46%), so balance accordingly.

## What I'd Add Next

If I had more time, I'd add:

1. **Seasonal analysis** - Break down sales by month/quarter to see if Outerwear spikes in Q4 or Swim in Q2
2. **Geographic segmentation** - Dataset has country data, could cluster by region (US vs China vs EU)
3. **Time series forecasting** - Predict demand for top SKUs to optimize inventory levels
4. **Elbow method** - Properly calculate optimal k instead of arbitrarily picking 3
5. **Production pipeline** - Refactor notebook into modular functions for daily batch runs

## Current Limitations

- This is a snapshot analysis, not tracking changes over time
- No customer churn prediction or lifetime value modeling
- K-means uses arbitrary k=3 (didn't calculate silhouette scores)
- Running locally on Windows instead of a real distributed cluster
- No A/B test framework for validating the business recommendations

## Project Structure
```
├── PySpark_Ecommerce_Clustering.ipynb  # Main analysis notebook
├── data/                               # CSV files (download from Kaggle)
│   └── README.md                       # Dataset documentation
├── results/                            # Visualization outputs
│   └── README.md                       # Output descriptions
├── requirements.txt                    # Python dependencies
├── .gitignore                          # Git exclusions
├── LICENSE                             # MIT license
└── README.md                           # This file
```

## Why Spark for This Dataset?

The dataset has 180K transactions, 2.4M events, and 500K inventory records. Here's why I used Spark instead of pandas:

**Benefits:**
- Handles distributed processing across multiple CPU cores
- Memory-efficient with lazy evaluation (operations only run when needed)
- Scales to 10x-100x data volume with minimal code changes
- `.cache()` strategy reduces redundant computations on joined tables

**Trade-offs:**
- Longer startup time (JVM initialization)
- More complex than pandas for smaller datasets
- Windows support is unofficial (had to work around some issues)

For this dataset size, pandas would work fine. But I wanted to practice Spark since most real e-commerce datasets are much larger. The same code would handle 10M+ transactions with just a few config tweaks.

## Notes

This was my first real Spark project. Learned a lot about distributed computing and had to debug some Windows-specific issues (Spark isn't officially supported on Windows). The trickiest part was getting the timestamp parsing to work - ended up using regex to strip timezone info.

The clustering results were interesting. The "high-value" segment is tiny (5%) but generates massive revenue. In a real business setting, I'd build a lookalike model to find more customers who match that profile.

---

**Author:** Anita Okojie  
**License:** MIT
