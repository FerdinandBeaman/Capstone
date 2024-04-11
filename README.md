# CapstoneProject
Predicting the Market
**Author**: [Ferdinand Beaman](mailto:ferdinand.beaman@gmail.com)

## Overview
It's seen as the Holy Grail of predictions: getting the edge on the market.
I took a preliminary stab at the problem, only learning about the Efficient Market Hypothesis on the final day of modeling.

Specifically, I decided to see the problem from the particular perspective of a day trader.

## Business problem: 
Can one use very recent data* to find patterns that are too suble to be accounted for by the Efficient Market Hypothesis. Data no more than one hour old? Can you at least beat a simple "buy and hold" strategy?
*I recognize that traders would have access to older data too, but I kept to a one hour maximum to preserve the size of each training batch.

## Data
I gathered data that was freely available from firstratedata.com, specifically the Intra-day stock information for American Airlines, Fed-Ex, Fidelity National, Macy's, Sprint, Starbucks, and Tesla.
Although I only had 11 days worth of price and volume data, the "Intra-day" data had both down to the minute. After preprocessing, I still had over 30,000 minutes of data at my disposal.

For reference, this is what a typical day's movement would look like in StDs:
![img](./all7_1day.png)

## Methods
I trained 16 Recurrent Neural Networks (GRU) to take a "step forward" approach through the time series. Steps were taken in either 25, 24, 45, or 60 minute increments. To inflate the iteration process, I also trained with two different learning rates (Adam's default LR of 0.0001 as well as 0.01) and had networks with different numbers of hidden layers. All overnight data and weekend data was purged, partly because you need special permission to trade then. The Standard deviation of the first 36 hours of each stock were used to standardize the columns.

## Evaluation of Results
The final model produced thus rather unpleasant chart:
![img](./all_final_predictions.png)

My RMSE on validation data across all models tended to be around 3.5, with the best model getting to about 3.2. I suspect that the main difference in model performance was merely the stochastic nature of the refinement of each one. In an earlier version of this project, the most performant models were different, and yet they all existed in this cloud of about 3.5, Also, since this is standardized data, a score this high means even the best price predictions are about 3 standard deviations away from being accurate.

The final model had a RMSE of 4.28 on the test data.

## Conclusions
Needless to say, it did not go well. The market remains undefeated.

This was to be expected. If the market could be beaten even slightly by a new student in the field... that would throw a lot of things into question. 
Still there was one image that caught my eye:

### Recommendations
You may not want to day trade, but if you do then take my most performant model and change it from there. 
Try a learning rate for Adam in the thousadths place, not the hundredths or ten-thousands like I did.

### Next Steps
1) Get more data. I only have 11 days worth of it, and if you're going to find subtle patters you need a lot more. Almost certainly enough to pay for.
2) Get sentiment data on the companies, perhaps by scraping tweets and other social media. If you want my help with that since I do have experience, I'd be happy to.

# Repository Structure

```
├── /ipynb_checkpoints
├── /1MinSamples
├── /images
├── README.md
├── Capstone_presentation.pdf
└── Ferdinand Beaman Phase 1 Project.ipynb
```
