# Spark E-commerce Analytics

![Python](https://img.shields.io/badge/python-3.8%2B-blue)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-3.5-orange)
![PySpark](https://img.shields.io/badge/PySpark-MLlib-red)

Big data analytics on 500K+ e-commerce records using Apache Spark and PySpark. Features customer segmentation with K-means clustering and product recommendations with ALS collaborative filtering on distributed data.

## 🎯 Project Overview

This project demonstrates distributed big data processing on e-commerce data using Apache Spark. I implemented customer segmentation and product recommendation systems that scale horizontally across cluster nodes.

**Dataset**: Looker E-commerce Dataset (7 tables, 500K+ total records)
**Technologies**: PySpark, Spark MLlib, Hadoop HDFS concepts, Distributed Computing

📊 Key Results
Customer Segmentation (K-means)
High-Value Loyal (23%): Generate 43% of revenue
High-Value Occasional (31%): High spend per transaction
Low-Engagement (46%): Represent only 18% of revenue

Recommendation System (ALS)
RMSE: 0.82
Cross-category recommendations: 68%
Successfully predicts future purchases with 23% accuracy

Business Impact
Identified 27 high-selling products with low stock
Electronics category shows highest profit margin (49.7%)
Data-driven customer segmentation enables targeted marketing

🛠️ Technologies
Apache Spark 3.5: Distributed data processing
PySpark MLlib: Machine learning at scale
Python: pandas, NumPy, Matplotlib
Jupyter: Interactive analysis

🚀 Quick Start
bash# Install dependencies
pip install -r requirements.txt

# Download dataset from Kaggle
# Place CSV files in data/ directory (see data/README.md)

# Run analysis
jupyter notebook Ecommerce_Big_Data_Analysis.ipynb
📁 Project Structure
├── Ecommerce_Big_Data_Analysis.ipynb  # Main analysis notebook
├── data/                              # Dataset directory
├── results/                           # Analysis outputs
├── requirements.txt                   # Python dependencies
└── README.md

🔍 Analysis Pipeline
Data Loading & Preprocessing: Cleaned 500K+ records across 7 tables
Exploratory Data Analysis: Examined customer behavior and product performance
Customer Segmentation: K-means clustering identified 3 distinct customer groups
Recommendation Engine: ALS collaborative filtering for personalized suggestions
Business Insights: Actionable recommendations for inventory and marketing

📈 Sample Outputs
Customer Segments
High-Value Loyal: avg 12.3 orders, $892 total spend
High-Value Occasional: avg 3.1 orders, $654 total spend  
Low-Engagement: avg 1.4 orders, $87 total spend
Top Product Categories by Revenue

Women's Apparel: $1.2M
Men's Apparel: $980K
Electronics: $820K

💡 Key Insights
Inventory Management: 27 high-demand products need restocking
Pricing Strategy: Electronics maintain 49.7% margins vs 41.2% for apparel
Customer Focus: Top 23% of customers drive 43% of revenue
Cross-selling: Recommendation system identifies 68% cross-category opportunities

📝 Future Enhancements
Real-time streaming analytics with Spark Streaming
Deep learning product recommendations with neural collaborative filtering
A/B testing framework for recommendation strategies
Integration with cloud platforms (AWS EMR, Databricks)

📄 License
MIT License - see LICENSE file for details
