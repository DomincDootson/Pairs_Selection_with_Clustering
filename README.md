# Pairs Selection with Unsupervised Clustering
The aim of this folder is to select candidate pairs from the S&P500 that can be used for pairs trading. The main bulk of the work is 
done in the `Pairs_Selection_with_Unsupervised_Learning` notebook. In this notebook we do the following:
1. Download stock data and the sector information from Yahoo finance
2. We create averages of each stock in a given sector. We then create a new feature for each of the stocks which is its correlation 
with each of the baskets.
3. We perform unsupervised learning using the correlations we have just calculated and the volatility and returns of the stock. We  
use the following algorithms:
- K means: Gives good results, recommends 2-4 clusters
- Hierarchical: Gives good results, recommends 8 clusters
- DBSCAN: This doesn't perform well, so we ignore its results 
- GMM: Gives good results, recommends 3 clusters
4. From each of the clusters recommended by each algorithm, we generate candidate pairs . We remove any candidates that are not 
suggested by all three algorithms. This leaves approximately 9,500 candidate pairs (7.5% of the starting number remain).
5. On these remaining candidate pairs, we carry out a Engle–Granger test for cointegration and select only those that pass at the 
FILL_SIG threshold.

