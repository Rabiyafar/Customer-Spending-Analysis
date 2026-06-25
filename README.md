# Customer Spending Analysis

## Project Overview
This project analyzes mall customer data to understand spending behavior and segment customers into distinct groups using K-Means clustering. The goal is to identify which customer segments are most valuable so a business can target marketing, loyalty programs, and retention strategies more effectively.

## Dataset
- **File:** `Mall_Customers.csv`
- **Size:** 200 customers, 5 columns
- **Columns:** `CustomerID`, `Genre` (gender), `Age`, `Annual Income (k$)`, `Spending Score (1-100)`
- No missing values in any column

## What the Notebook Does

**1. Data loading & inspection**
Loads `Mall_Customers.csv`, prints the first 5 rows, shape, column info, null counts, and summary statistics. Confirms 200 rows, 5 columns, no missing values.

**2. Distribution plots (Age, Income, Spending Score, Gender)**
- **Age** is spread fairly broadly from late teens to ~70, with a noticeable peak around the early 30s.
- **Annual Income** is roughly bell-shaped, centered in the 60–80k$ range, tapering off above 100k$.
- **Spending Score** is more irregular than the other two — there's a cluster of customers low on the score (under 20) and a distinct bump again around 70–90, suggesting the customer base isn't one smooth group but already hints at sub-populations before any clustering is done.
- **Gender count** shows more female than male customers in the dataset, though the difference isn't huge (roughly 56% female).

**3. Relationship plots (scatter/box)**
- **Age vs. Spending Score:** younger customers (under ~40) show the widest range of spending scores, including the highest ones. Past ~40, spending scores compress into a narrower, more moderate band — older customers in this dataset don't reach the very high spending scores that younger ones do.
- **Income vs. Spending Score:** this is the most visually interesting plot — the points aren't randomly scattered, they form visible groupings: a dense cluster in the middle (mid income, mid spending), and then separate pockets in the corners (low income/high spending, high income/low spending, high income/high spending). This shape is what motivates clustering instead of just looking at correlation.
- **Gender vs. Spending Score / Income (boxplots):** the boxes for male and female overlap almost entirely on both metrics. Visually, gender doesn't explain much of the variation in spending or income here.

**4. Elbow Method**
WCSS drops sharply from k=1 to k=4, then the curve visibly flattens starting at k=5 — the bend ("elbow") is around there, which is the basis for choosing 5 clusters.

**5. K-Means clustering (k=5) and cluster scatter plot**
Re-running K-Means with 5 clusters on Income and Spending Score produces a scatter plot with 5 clearly separated, colored groups plus their centroids (marked with black X's). The separation in this plot is clean — almost no overlap between clusters, which matches what the earlier Income-vs-Spending scatter plot was hinting at.

## Results

**Cluster sizes:**
| Cluster | Size |
|---|---|
| 0 | 81 |
| 1 | 39 |
| 2 | 22 |
| 3 | 35 |
| 4 | 23 |

**Cluster averages (Age, Income, Spending Score):**
| Cluster | Avg. Age | Avg. Income (k$) | Avg. Spending Score |
|---|---|---|---|
| 0 | 42.7 | 55.3 | 49.5 |
| 1 | 32.7 | 86.5 | 82.1 |
| 2 | 25.3 | 25.7 | 79.4 |
| 3 | 41.1 | 88.2 | 17.1 |
| 4 | 45.2 | 26.3 | 20.9 |

Looking at where each cluster sits in the scatter plot and matching it to these numbers:
- **Cluster 0** is the largest group by far (81 customers) and sits in the middle of the plot — moderate income, moderate spending. This is the "typical" customer.
- **Cluster 1** sits in the top-right — high income and high spending together.
- **Cluster 2** sits top-left — lower income but spending scores almost as high as Cluster 1.
- **Cluster 3** sits bottom-right — high income but low spending, the mirror opposite of Cluster 2.
- **Cluster 4** sits bottom-left — both income and spending are low.

What stands out just from looking at the plot is that income and spending score don't move together in a simple straight line — high income doesn't automatically mean high spending (clusters 1 and 3 both have high income but opposite spending behavior). That's the main thing this clustering surfaces visually that a simple correlation number wouldn't show.

## Key Business Insights

- Income does not directly correlate with spending behavior.
- High-income customers can exhibit both high and low spending patterns.
- Segmentation provides more actionable insights than simple correlation analysis.


## Tech Stack
Python — pandas, NumPy, matplotlib, seaborn (EDA & visualization), scikit-learn (`KMeans` for clustering)

## Author
Rabiya Farheen
MSc Data Science, Technical University of Braunschweig, Germany
