# CapstoneProject
Predicting the Market
**Author**: [Ferdinand Beaman](mailto:ferdinand.beaman@gmail.com)

## Overview
It's seen as the Holy Grail of predictions: getting the edge on the market.
I took a preliminary stab at the problem, only learning about the Efficient Market Hypothesis on the final day of modeling.

Specifically, I decided to see the problem from the particular perspective of a day trader.

## Business problem: 
Can I use very recent data* to predict impending changes in stock prices? Data no more than one hour old?
*I recognize that traders would have access to older data too, but I kept to a one hour maximum to preserve the size of each training batch.

## Data
I gathered data that was freely available from firstratedata.com, specifically the Intra-day stock information for American Airlines, Fed-Ex, Fidelity National, Macy's, Sprint, Starbucks, and Tesla.
Although I only had 11 days worth of price and volume data, the "Intra-day" data had both down to the minute. After preprocessing, I still had over 30,000 minutes of data at my disposal.

## Methods
I trained 16 Recurrent Neural Networks (GRU) to take a "step forward" approach through the time series. Steps were taken in either 25, 24, 45, or 60 minute increments. To inflate the iteration process, I also trained with two different learning rates (Adam's default LR of 0.0001 as well as 0.01) and had networks with different numbers of hidden layers.

## Evaluation of Results
Here a typical example of one model's take predicting the 7 stocks' prices, measured in standard deviations (derived from the first 36 hours of data).
![img](./Images/Bad_image)

My RMSE on validation data tended to be around 3.5, with the best model getting to about 2.9. But since this is standardized data, a score this high means even the best price predictions are about 3 standard deviations away from being accurate.

Here are two of the 16 validation loss curves. For the default learning rate, it was typical to have the two lines stay far apart. For the faster one, it was typical for the validation loss to swing wildly.
![img](./Images/terrible_loss)
![img](./Images/terrible_twos)

The final model had a RMSE of 4.66.

## Conclusions
Needless to say, it did not go well. The market remains undefeated.

This was to be expected. If the market could be beaten even slightly by a new student in the field... that would throw a lot of things into question. 
Still there was one image that caught my eye:

![img](./Images/Hopeful_image)

For just a little while, the direction and magnitude of the lines are in near lockstep, even if their raw numbers arent. Is this noise, amplified by my own survivorship bias? It's hard to say.


### Recommendations
Do not day trade. Do things the "right" way, however boring they may be. Long term, safe investments that you don't intereact with much.
However, if you can't help but want to look further into it, there are a couple of easy things you can do to maximize your chances...

### Next Steps
1) Get more data. I only have 11 days worth of it, and if you're going to find subtle patters you need a lot more.
2) Get sentiment data on the companies, perhaps by scraping tweets and other social media
3) Good luck

# Repository Structure

```
├── /ipynb_checkpoints
├── /1MinSamples
├── /images
├── README.md
├── Capstone_presentation.pdf
└── Ferdinand Beaman Phase 1 Project.ipynb
```
