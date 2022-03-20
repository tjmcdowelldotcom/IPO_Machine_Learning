# Machine Learning IPO Genie

TJ McDowell, Chris Kwiatkowski, Troy Albany, Edward Schryver

---
## Hypothesis

Artificial Intelligence will be able to find patterns in pre-IPO company financials in order to predict future public market profitability.
___
___
## Considerations 
Typically when an investor purchases stock prior to an IPO they are subject to lockdown-period contraints of 90 to 180 days. To account for this the IPO Genie model was tested on profitability measured 100 days post the initial offering.

The Binary Classification task was set to recognize whether the stocks had simple positive or negative returns at day 100. Setting a particular threshold for returns beyond that (e.g. +10%, 20%...) was also considered. For the dataset available this would have resulted in a more extensive use of artificial balancing measures for the data and compromised data integrity.

___
___

## Data Preparation

The previous fiscal years annual balance sheets, cash flows, and income statements for 306 companies were obtained, cleaned, and merged.
![Index](Images/Data.PNG)

 <br>

Using Yahoo Finance API, this data was joined with SPY index returns over a period of 90 days prior to the public offering, assuming that the overall market trend may be a key predicting factor. The API was also used to retrieve the returns on the companies stock price.
![Index](Images/Data2.PNG)

---
---
## Results

The first three predictive models used were XGBoost, PyTorch NN, and ADABoost. In essence, these models showed similar traits in precision & recall for predicting both positive and negative returns. The F1 score for negative returns was noticeably more accurate than positive.
![Index](Images/Models1.PNG)
<br>

The following three models overall showed broader diversity. Logistic Regression and SVC models were overall more aggressive at predicting buys, while Random Forest was our most conservative model.
![Index](Images/Slide22.JPG)


The Random Forest Model feature importance output was as follows:
![Index](Images/FI.PNG)
A Voting Classifier ensemble method was then created comprised of Logistic Regression, Random Forest, and SVC models with weights 1, 2, and 2, respectively. This model had the best combined F1 scores compared to the others.
![Index](Images/Model2.PNG)

---
---
## Conclusion

This chart shows realized p&l for the strategy given wich predictive model was used for the buy signal. The Voting Classifier (black) is shown to have performed better than all other models, including a scenario in which one bought all IPOs in our list and sold them 100 days later.
![Index](Images/Chart1.PNG)


This chart compares the baseline of going in on all of the IPOs, the performance of our strategy, and a similar DCA strategy just using shares of SPY. Though our model was demonstrably profitable, given the nature of the market at the time it is show that buying and selling SPY shares would have been more so.
![Index](Images/Chart2.PNG)















