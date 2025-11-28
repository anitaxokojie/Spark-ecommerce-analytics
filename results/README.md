# Analysis Results

Output from the PySpark clustering analysis.

## Customer Segments

Ran K-means (k=3) on 80,044 customers using purchase frequency and total spend:

| Segment | Count | % | Avg Spend | Avg Orders |
|---------|-------|---|-----------|------------|
| Low-Value | 54,104 | 67.5% | $62.94 | 1.6 |
| Mid-Value | 22,037 | 27.5% | $236.24 | 3.4 |
| High-Value | 3,903 | 4.9% | $567.77 | 5.1 |

**What This Means:**
- Most customers (67%) are one-time or low-engagement buyers
- The top 5% spend almost 10x more than the bottom tier
- Mid-value customers are the sweet spot for upselling

## Product Performance

### Best Sellers (by volume)
1. Wrangler Men's Jeans - 62 units
2. Puma Men's Socks - 48 units
3. 7 For All Mankind Jeans - 41 units
4. True Religion Jeans - 37 units
5. Kenneth Cole Jeans - 36 units

### Most Profitable Categories

| Category | Revenue | Profit | Margin |
|----------|---------|--------|--------|
| Outerwear & Coats | $1,301,571 | $721,875 | 55.53% |
| Jeans | $1,253,644 | $582,912 | 46.48% |
| Sweaters | $842,651 | $437,260 | 51.93% |
| Suits & Sport Coats | $666,767 | $398,930 | 59.93% |
| Swim | $646,739 | $316,596 | 47.82% |

Outerwear has both high volume AND high margin - that's the jackpot category.

## Business Takeaways

**Inventory:**  
Stock up on Outerwear (55% margin) and keep Wrangler jeans in stock (top seller).

**Customer Strategy:**
- Low-Value: Email campaigns with 15-20% off to drive repeat purchases
- Mid-Value: Bundle deals (e.g., jeans + belt) to increase order value
- High-Value: VIP program with free shipping and early sale access

**Marketing Budget Split:**
- 60% to high-value segment (small group, massive revenue)
- 30% to mid-value upselling
- 10% to low-value re-engagement tests

**Cross-Selling Ideas:**
- Jeans buyers → suggest belts and socks
- Outerwear buyers → recommend sweaters
- Active wear buyers → cross-sell socks/shorts

## Technical Notes

- K-means used 3 features: frequency (order count), monetary (total spend), avg_basket ($/order)
- Didn't normalize features (raw values worked fine)
- Cluster labels assigned manually based on avg_spend ranking
- Analyzed 181,759 transactions from 80,044 customers
- Processing took ~5 minutes on cached data

## Visualizations

When you run the notebook, it saves:
- `customer_segments.png` - bar charts and pie chart showing segment distribution
- `category_profitability.png` - top 10 profitable categories

## What I Didn't Include

- No recommendation system (removed ALS from this version)
- No seasonal breakdown (can't see Q4 holiday spike)
- No geographic clustering (US vs international)
- Static analysis (not tracking changes over time)

## Next Steps

Planning to add:
- Month-over-month trend analysis
- Cluster by country/region
- Churn prediction for low-value customers
- Maybe re-add collaborative filtering if the data supports it
