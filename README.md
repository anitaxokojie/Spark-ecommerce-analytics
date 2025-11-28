# E-commerce Customer Segmentation with Apache Spark

Big data project analyzing 180K+ e-commerce transactions using PySpark and K-means clustering.

## What I Built

I used Apache Spark to process e-commerce transactions and segment customers based on their purchasing behavior. The goal was to identify high-value customers and understand which product categories drive the most profit.

**Tech Stack:** PySpark 3.5.5, MLlib, Python 3.12, Jupyter  
**Dataset:** Looker E-commerce BigQuery (180K transactions, 80K customers)

## Main Findings

### Customer Segments (K-means, k=3)

After clustering 80K+ customers by purchase frequency and total spend:

- **Low-Value (67%)**: Average $63 lifetime spend, typically 1-2 orders. These are mostly one-time buyers.
- **Mid-Value (28%)**: Average $236 spend across ~3 orders. Regular customers worth targeting for upsells.
- **High-Value (5%)**: Average $568 spend with 5+ orders. Our VIPs who need retention programs.

The top 5% of customers generate over 3x more revenue than the average customer.

### Product Performance

Best-selling items:
- Wrangler Men's Jeans: 62 units
- Puma Socks: 48 units  
- 7 For All Mankind Jeans: 41 units

Most profitable categories:
1. Outerwear & Coats: $722K profit (55% margin)
2. Jeans: $583K profit (46% margin)
3. Sweaters: $437K profit (52% margin)

## How to Run

```bash
# Install dependencies
pip install -r requirements.txt

# Download dataset from Kaggle
# https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset

# Open notebook
jupyter notebook PySpark_Ecommerce_Clustering.ipynb
```

The notebook will download the data automatically via kagglehub if you have the API configured.

## Technical Highlights

**Spark Configuration**  
Had to configure Spark for Windows - set PYSPARK_PYTHON environment variables and allocate 2GB to executor/driver memory. Also used legacy time parser for the timestamp columns.

**Data Cleaning**  
The timestamps had timezone suffixes that broke Spark's default parser, so I used regex to strip them. Also had to explicitly cast price/cost columns to DoubleType since Spark's schema inference was inconsistent.

**Joins**  
Created a comprehensive dataset by joining orders → order_items → products → users. Renamed columns to avoid ambiguous references (e.g., `product_id` vs `product_id_ref`). Cached the final dataframe since it gets reused for multiple aggregations.

**ML Pipeline**  
Used VectorAssembler to combine frequency, monetary, and avg_basket features. Trained K-means with k=3 (chose 3 after looking at the business context - didn't want too many micro-segments). Model assigns each customer to a cluster, then I aggregated to get segment stats.

## Business Recommendations

Based on the segmentation:

**Low-Value Customers (67%)**  
Run re-engagement campaigns with 15-20% discounts. Goal is converting them to repeat buyers.

**Mid-Value Customers (28%)**  
Upsell with product bundles (e.g., jeans + belt combos). These customers are already engaged.

**High-Value Customers (5%)**  
VIP treatment - loyalty program, free shipping, early sale access. Can't afford to lose these.

**Inventory**  
Stock up on Outerwear since it has the highest margin (55%) and solid volume. Jeans are the volume leader but lower margin (46%).

## What I'd Add Next

1. **Seasonal Analysis**: Break down sales by month/quarter to see if Outerwear spikes in Q4 or Swim in Q2.
2. **Geographic Segmentation**: Dataset has country data - could cluster customers by region (US vs China vs EU).
3. **Time Series Forecasting**: Predict demand for top SKUs to optimize inventory.
4. **Code Refactoring**: Turn the notebook into a production pipeline with modular functions.

## Current Limitations

- Analysis is a snapshot (not tracking changes over time)
- No customer churn prediction
- K-means uses arbitrary k=3 (didn't calculate optimal k with elbow method)
- Running locally on Windows instead of a real Spark cluster

## Project Structure

```
├── PySpark_Ecommerce_Clustering.ipynb  # Main analysis
├── data/                               # CSV files (download from Kaggle)
├── results/                            # Output visualizations
├── requirements.txt                    
└── README.md                           
```

## Notes

This was my first real Spark project. Learned a lot about distributed computing and had to troubleshoot Spark on Windows (not officially supported). Processing the full dataset took ~35 minutes on my laptop.

---

**Author:** Anita Xokojie  
**License:** MIT
