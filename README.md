# Pairs Selection with Unsupervised Clustering
The aim of this folder is to select candidate pairs from the S&P 500 that can be used for pairs trading. The main bulk of the work is done in the `Pairs_Selection_with_Unsupervised_Learning` notebook. 

## Pairs Selection Notebook
In this notebook we carry out the following steps:
1. **Getting the Data**: We wrote code to take stock time series data from the S&P 500 and relevant sector information. We created aggregate time series for each sector into baskets.
2. **Pairs Selection**:
   - By calculating the correlation of each stock with the baskets, we generated features for unsupervised learning.
   - Using 4 different clustering methods (K-means, Hierarchical, DBSCAN, GMM), we generated different clusters of pairs. Three methods worked well, however we ignore the results of DBSCAN due to poor convergence. 
3. **Generate Pairs**: From each of the clusters across all the methods, we generated candidate pairs. We only kept those pairs that 
were common to all the algorithms. This gave 9,500 pairs.
4. **Cointegration Test**: We performed the Engle-Granger test to check if the spread of the pair was stationary. We kept those that 
were significant at the 1% level. This gave ~570 pairs.
5. **Examining the Pairs**:
    - We look at which sectors were over/underrepresented. We found that we were only using 350 stocks (about 3/4 the number we were expecting), however that no one sector was over/under represented.
    - When looking at the sector pairing, we found that no one sector pairing was particularly strong, however the difference was really driven by the absolute number in each sector. 


## Pairs Trading Prototype Notebook
In this notebook we take a few example pairs, fit the linear relationship between the two stocks and implement a pairs trading algorithm. We then fit the linear relationship between all the pairs, and save to file. An example of the spread between two stocks is shown below. The green (red) dots show when we enter (leave) a position.

![](Figs/Example_Pairs_Trade.png)


## Results 
We back test our strategy with all the pairs that were found in the clustering notebook. We take SP500 data from July 2023-Jan 
2024 (we fit on the six month period before this). On our test sample we achieve:
- **Sharpe Ratio:** 2.04.
- **Annual Returns:** 6.21%.
- **Annual Volatility:** 1.33%.

We enter our position when the spread is over 2 sigma from the mean and we exit the position when we are 1 sigma from the mean.  

Below we plot the distribution of returns for each position. We find a slight positive skew, which is surprising for a pairs trading strategy. 

![](Figs/Pairs_trading_daily_returns.png)

In the left hand panel below, we  plot the number of days that each position was open for. The time length is not different between positive and negative. 

It is interesting to note that 1/5 of our negative trades come on the final day. This is because we close all of our positions at the end of the back testing period (note that we also have lots of positive strategies that close on this day as well). If we did something clever, e.g. not opening positions within a number of days of the end, we could increase returns. As a simple example of this, if we don't include those that we close on the final day we get annualised returns of 6.65% (i.e. 7.1% improvement). 

![](Figs/Dist_n_days_positions.png)

For the specific implementation of the strategy and the code that carries out the backtesting, please find it at https://github.com/DomincDootson/BackTesting. 