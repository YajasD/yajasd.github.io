---
layout: post
title: Linear Regression & The Price of Gold
---



### What contributes to the price of a shiny metal?

Decided to use my new found Linear Regression and Web Scraping powers to find a relationship between the price of an ounce of Gold and the following features:

1. <a href='https://financial.thomsonreuters.com/en/products/data-analytics/market-data/indices/commodity-index.html'>The ThomasRetuters Core Commodity Index Fund (CRB)</a>
  This Index Fund is made up of 19 commodities - with 39% allocated to energy contracts, 41% to agriculture, 7% to precious metals and 13% to industrial metals.

2. <a href='https://inflationdata.com/Inflation/Inflation_Rate/CurrentInflation.asp?reloaded=true'>Monthly Inflation Rate</a>
  How much is USD worth today compared to how much it was worth a month ago?

3. <a href='https://fred.stlouisfed.org/series/M1'>M1 Money Supply</a>
  How much USD has the Federal Reserve printed?

4. <a href='https://www.investing.com/currencies/eur-usd-historical-data'>EURUSD</a>
  How much USD does it take to buy 1 EUR?

After establishing these as my features, I decided to get my data.

--> Scraped the price of Gold using Selenium from this <a href='http://onlygold.com/Info/Search-Gold-Prices.asp'>website.</a>

-->Inflation Data was scraped using Selenium too.

-->The other websites were nice enough to provide a direct download link!


### Analysis

Let's look at the price of gold between August 2016 and April 2018.

![alt_text]({{ site.url }}/images/gold_price.jpg)

Now, let's look at all our features over the same period.

![alt_text]({{ site.url }}/images/AllFeatures.jpg)


Do you see some trends? Good. Let's see if we can find a nice little equation that captures this relationship.

Before we dive into actually finding our equation, Let's find out-

### How are these features related to the price of Gold?

![alt_text]({{ site.url }}/images/heatmap.jpg)

From this correlation heat-map, we see that of our 4 features, EURUSD seems to be the most correlated to the price of Gold, followed by M1SL, inflation rate (negatively correlated) and lastly the CRB index.

### Linear Regression

I start simple. Using the good old Ordinary Least Squares method, I get:

![alt_text]({{ site.url }}/images/linreg1ols.jpg)

With an R^2 score of 0.67, and a Mean Absolute Error (MAE) of $28, while it's not abysmal. It's surely not very good. Also, notice how whenever the price is over $1300, my model does terribly.

Clearly there are some relationships that my model is not picking out on.

What if I try adding Polynomial Features into the mix? Basically, I'm giving my model permission to use features like EURUSD * M1 Money Supply or CRB Index^2.

My model immediately does better -

![alt_text]({{ site.url }}/images/linreg1poly.jpg)

Note that here I am using 2nd degree Polynomial Features. My R^2 is up to 0.82 and MAE is down to $15.

Pretty neat huh? Clearly my chosen features have a relationship with the price of an ounce of gold! Yay!

### What's next?

Clearly, the next step is to add a time series component to this analysis to 'predict' the future price given historical price. Start by trying some simple Auto-Regressive/Moving Average models, and then combining the 2 (ARIMA) model. Maybe see how the recently released Facebook Prophet library fares. Once you know Linear Regression, the possibilities are endless!

**I will be uploading my notebook with all the code to achieve all of the above to my Github repo shortly! Stay tuned! **
