# Analysis Results

This folder contains visualization outputs from running the notebook.

## Files

**Visualizations:**
- `customer_segments.png` - Three-panel chart showing avg spend, avg orders, and customer distribution
- `category_profitability.png` - Horizontal bar chart of top 10 most profitable categories

## Sample Results Summary

From the analysis:

**Customer Clusters:**
- Cluster 0: 54,104 customers (68%), $63 avg spend, 1.6 avg orders
- Cluster 2: 22,037 customers (27.5%), $236 avg spend, 3.4 avg orders  
- Cluster 1: 3,903 customers (4.9%), $568 avg spend, 5.1 avg orders

**Top Profitable Categories:**
1. Outerwear & Coats - $722K profit (55% margin)
2. Jeans - $583K profit (46% margin)
3. Sweaters - $437K profit (52% margin)

## Notes

- The exact numbers will vary slightly depending on the cluster seed and dataset version
- The notebook uses `seed=42` for K-means to ensure reproducibility
- Charts use seaborn's default style with figure sizes `(18, 5)` for multi-panel and `(12, 6)` for single charts
