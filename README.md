# Energy Consumption Forecasting - Analysis and Modelling

This notebook presents a solution to a fairly popular problem in various business cases in
the Data Science community: time-series forecasting.

The notebook was part of a technical test I did as I was interviewing for a Data Scientist
position in this specific company. The one condition on the development of this test was the
timebox available to develop both the analysis and the model: **6 hours**. I've received the data
and returned my analysis and results 6 hours later.

# Approach

The notebook contains three main parts:

### 1. Folder setup and initial data adjustment.

Here I talk about how I've set up the project locally on my machine, how the root folder is organized
and how to install the requirements with the `pip install -r requirements.txt` command. Then, I load
dinamically my data in a variable and start using the `pandas` library to get intuition on it.

I check the number of lines, columns, types of the data, missing values, all common initial inuition
checks that a Data Scientist usually do when it gets a new dataset. Then, I engineer the columns that
have date and time properties into a datetime index and convert the string data into a float to make
calculations, also changing it's name to "value", to be more generic, although, probably we're talking
kW/h ([wiki: killowats per hour](https://en.wikipedia.org/wiki/Kilowatt-hour)) on our measurements.

### 2. Exploratory data analysis

Here I try to create some intuition on the problem. First, I start by analyzing the start and end dates
of the time-series and get the number of months and days this interval has. I check if the data points
are evenly spaced and create different points-of-view for the data: monthly, weekly and daily, using
the boxplot as my visual support.

Then, I mix business knowledge with some data insights to create some hypothesis about the outliers on
the sample data on all three points-of-view, present some intuition about seasonality and just by
analyzing those results, I make a guess about the model outcome, just to create a sense of direction
on the analysis.

To end this section, I use the `statsmodels` library to decompose the series, look at the seasonal, trend
and residual plots, the series autocorrelation and partial autocorrelation and checked it's stationarity
using the Augmented Dickey-Fuller ([wiki:ADF](https://en.wikipedia.org/wiki/Augmented_Dickey%E2%80%93Fuller_test))
test.

### 3. Modelling and results (+ autoML bonus part at the end).

In this part, I decided to fit a ARIMA model. I used the `diff` method to create the series differentiations 
and the `statsmodels`'s `acf` and `pacf` plots to set the parameters `p` (autoregressive) and `q` (moving average).

After that I realized was already running short on time and decided to proceed without really taking
too much care in the data splitting. I've described that decision on the notebook and as result of this, 
I've got an overfitted model, but got some predictions aligned with what the exploratory analysis gave
to us as an intuition. The results can be seen on the images below:

![First Image](/model_images/results_ARIMA.png "ARIMA model results")

[1] ARIMA model results shown on a larger portion of the time-series.

![Second Image](/model_images/results_ARIMA_zoomed.png "ARIMA model results zoomed in")

[2] ARIMA model results shown on a larger portion of the time-series.

