# Stock Selection using Deep Learning

## Summary
Purpose of this analysis is to predict 1-month stock returns of securities in CSI 300. Based on predicted returns performance, each stock will be assigned to different performance categories. At the end of each month, we will go long on stocks predicted to have good performance and go short on stocks predicted to have poor performance.

This process will repeat every month and the strategy will be backtested to determine with whether the prediction model is good enough for consistent outperformance over the index/benchmark.

## Platform and Data
The analysis is entirely done on [JoinQuant](www.joinquant.com) research platform.  All data like index securities, factors and prices are downloaded on using JQData api on the platform.  Documentation are in Chinese.

## Notebook
1. https://github.com/edgetrader/stock-selection-deep-learning/blob/master/notebook/csi300-stock-selection-deep-learning.ipynb

---
# Trading Algorithm

**Benchmark**: CSI300   
**Stock Universe**: All securities in CSI300  
**Trading Frequency**: Every last business day of the month  
**Strategy**: Stock Picking.  The top *10* securities in *category A (at least 10% return)* based on predicted probability will be selected for the month to go long. Only securities with predicted probability of at least *0.5* in that category is selected.  The top *10* securities in *category C (at least -10% return)* based on predicted probability will be selected for the month to go short. Only securities with predicted probability of at least *0.5* in that category is selected.  
**Machine Learning model**: Tensorflow Keras Sequential Deep Learning Model.  Trained with 45 factors as features and performed multi-classification on next month returns.  Multi-classification as the returns are categorised to 3 levels based on their performance.  For example, 'A' being securities having at least 10% returns and 'C' being securities having at least -10% returns.  
**Sample Features**: beta, sharpe_rate_60, Variance20, liquidity, momentum as made available on [JQData Factor List](https://www.joinquant.com/help/api/help?name=factor_values)  
**Training Data**： Past 36 months of monthly factor data  
**Other considerations**:   
- Securities with incomplete or missing factor data are excluded from the selection process.  
- All positions will be closed at monthend before new ones are executed.  This process can be improved to minimise selling and buying of the same security on the same day.  
- All selected securities are transacted with equal weights based on portfolio size at the point in time.  Weights of each security can be improved and efficiently determined based on modern portfolio theory and efficient frontier.  

