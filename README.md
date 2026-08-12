# E-Commerce Customer Intelligence: RFM and Cohort Analysis

Customer segmentation and retention analysis on 1.07 million UK gift retailer transactions, built with Python. The project scores every customer on Recency, Frequency and Monetary value, groups them into business friendly segments, and measures repeat purchase behavior by first purchase cohort.

## Dataset

UCI Machine Learning Repository, Online Retail II (transactions from a UK based online gift retailer, December 2009 to December 2011). Two sheets, Year 2009-2010 and Year 2010-2011, combined into a single timeline.

Source: https://archive.ics.uci.edu/dataset/502/online+retail+ii

## Tools

Python, pandas, NumPy, matplotlib, seaborn.

## Method

1. **Ingestion.** Loaded both sheets and combined them into one table, 1,067,371 rows.
2. **Cleaning.** Removed rows with a missing customer ID (guest checkouts, which cannot be tied to a repeat buyer), missing product descriptions, exact duplicates, and rows with zero quantity and zero price. Result: 797,885 rows across 5,942 unique customers.
3. **Feature engineering.** Built a Revenue column (Quantity multiplied by Price) and an InvoiceMonth period for trend and cohort work.
4. **RFM scoring.** Calculated Recency, Frequency and Monetary value per customer, then split each into quintiles using pandas qcut. Recency is scored in reverse, a lower number of days since the last purchase is better. Combined the three scores into seven business friendly segments, for example Champions, At Risk, and Lost.
5. **Cohort analysis.** Grouped every customer by their first purchase month, then tracked what percentage of each cohort returned in each of the following 12 months.
6. **Delivery.** Exported four charts and a segment level CSV as the client facing deliverable.

## Key results

- 5,839 of 5,942 cleaned customers received a named RFM segment. 103 customers were excluded because their net lifetime spend, after returns, was zero or negative.
- Champions (1,285 customers, 22.0 percent of the segmented base) average 18.6 days since last purchase, 21.1 orders, and £8,874 in lifetime spend.
- Lost (1,264 customers, 21.6 percent) average 463 days since last purchase and £249 in lifetime spend.
- At Risk (836 customers, 14.3 percent) average 360 days since last purchase but still carry a meaningful order history, 6.1 orders and £1,667 spent on average, making them the most actionable segment to win back.
- Month 1 retention across cohorts runs roughly 12 to 30 percent, meaning most first time buyers do not return the following month, which is typical for a gift retailer rather than a subscription business.

## Limitations

- Others (620 customers, 10.6 percent of the segmented base) is a catch all category for customers whose scores did not clearly match one of the six named rules. It is not an error, but it should be explained rather than presented as a clean segment.
- This is a single retailer, two year dataset. Segment thresholds and retention benchmarks will not transfer directly to a different industry or a shorter data history.

## Files in this repository

- `notebook.ipynb`, the full analysis notebook
- `rfm_segments.csv`, the customer level segment export
- `charts/`, the four exported visuals: monthly revenue trend, RFM segment distribution, cohort retention heatmap, and top 10 products by revenue

## Author

Amal Mohamed, Freelance Data Analyst
[LinkedIn](https://www.linkedin.com/in/amal-mo) | [GitHub](https://github.com/Amalaltlb)
