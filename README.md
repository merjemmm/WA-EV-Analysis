# The Status of Electric Vehicles in Washington

**Name**: Merjem Memic
**Affiliation**: University of Michigan
**Email**: merjemm@umich.edu

This is an analysis of public records of Vehicles licensed in Washington.
The first dataset detailing registered vehicles from Jan 2017 to Sept 2024 can be found at https://catalog.data.gov/dataset/electric-vehicle-population-size-history-by-county.

The second dataset detailing all electric vehicles registered as of October 2024 including their make and model can be found at https://catalog.data.gov/dataset/electric-vehicle-population-data. 

This project was created as the final project in EECS 398: Practical Data Science at the University of Michigan taught by Prof. Suraj Rampure in Fall 2024. 

## Introduction

In this project, we will be investigating a dataset that contains information about all vehicles registered in Washington State over a period of close to 7 years (Jan 2017 to Sep 2024). For simplicity, we will refer to the vehicles in this dataset as electric vehicles or EV's. This dataset was provided by `Data.gov` through the Washington State Department of Licensing.

The main questions we will be asking throughout this project will be how trends in electric vehicle ownership have changed over time. Later, we will be trying to predict the number of EVs for Washington in 2024 (Jan to Sep) and comparing it to the actual values. 
We will also discuss infomration from another dataset about the qualities of the electric vehicles registered in Washington State as of October 2024. This dataset can give insight into the brands, models, and electric vehicle types are popular (Battery Electric Vehicles (BEVs) vs Plug-in Hybrid Electric Vehicles (PHEVs)).

For the overallhere are 7,254 rows in the dataset each of which represents a date in time and holds information about the number of vehicles registered then in Washington. There are 10 columns contained in this dataset. The columns have both overall and specific statistics. For example, there is a column dedicated for the number of Battery Electric Vehicles (BEVs) and another for Electric Vehicle (EV) Total. The information we are most interested is contained in `Date`, `County`, `Electric Vehicle (EV) Total`, `Non-Electric Vehicle Total`, and `Total Vehicles`. We will be using `Non-Electric Vehicle Total` for comparitive purposes.  

## Data Cleaning and Exploratory Data Analysis

We pick out the columns that we will be using later. We also discard entries related to other states. We convert the date column to properly plot it later. We also check for any NA values in the dataset. We find that there is none thankfully. One of the columns related to the Vehicle's primary use. This resulted in two entries for every date per county so, we need to merge these into one row since we don't care whether a vehicle is a passengers or truck. Here, we want to consider all vehicles regardless.

Thankfully, there were no missing values in the data relating to the columns and rows that we wanted to investigate. Because of this, there is no need for any imputations or worry about their impact on our conclusions, models, or predictions. 

| Date                | County       |   Electric Vehicle (EV) Total |   Non-Electric Vehicle Total |   Total Vehicles |
|:--------------------|:-------------|------------------------------:|-----------------------------:|-----------------:|
| 2017-12-31 00:00:00 | Pend Oreille |                             0 |                         5619 |             5619 |
| 2017-04-30 00:00:00 | Lincoln      |                             0 |                         4464 |             4464 |
| 2019-03-31 00:00:00 | San Juan     |                           267 |                        14284 |            14551 |
| 2021-03-31 00:00:00 | Asotin       |                             0 |                         6721 |             6721 |
| 2024-04-30 00:00:00 | Clallam      |                            30 |                        21408 |            21438 |


This plot shows the number of registered Electric Vehicles for every county in Washington State. As shown, King County has the most EVs of any county. However, it also has almost double the population that Pierce, the county with the second largest amount of EVS, does (https://www.census.gov/quickfacts/kingcountywashington, https://www.census.gov/quickfacts/piercecountywashington).


<iframe
  src="asset_plots/all_count_plot_p2a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We can also look at the aggregate populations of vehicles in Washington. 
Pay attention to the scales because there are close to 6 million non-Electric Vehicles, while only around 170 thousand Electric Vehicles in all of Washington at the beginning of 2024. The state is still mostly using gas based vehicles instead of teh more sustainable possibility. 

<iframe
  src="asset_plots/non_ev_all_v_plot_p2c.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="asset_plots/all_count_plot_p2d.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


We also can get an idea of what EV makes are most popular in Washington as of October of 2024. 
Some quick facts:
 * Tesla has seemingly cornered the market, and is the most popular make of EV in Washington. There are 91,379 Tesla branded cars registered.
 * The second largest is Chevrolet with 15,419. 
 * They are followed by Nissan at 14,721.
 * The `OTHER 22` present in the pie chart is representative of 22 other car brands where each individually had less than 1,000 cars registered. For ease of understanding, they are all shown under this label instead. 
 * There are two registered Rolls-Royce EVs in Washington.
 * There is one Vinfast EV registered. This might be surprising, but Vinfast is a popular EV brand abroad (https://vinfast.com, https://en.wikipedia.org/wiki/VinFast). It was also named as among world's 100 most influential companies in 2024 by Time Magazine's (https://time.com/6979933/vinfast/). The more you know.

<iframe
  src="asset_plots/pie_chart_p2f.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Framing a Prediction Problem

We will be trying to predict the total number of Electric Vehicles in Washington for the last year of our data set. This will result in around 13% of our full datatest composing the test, while 87% will become the training set. We will be using the total number of vehicles and associated dates to predict the electric vehicles for a certain date. 

## Baseline Model

For our basic model, we start off with a simple linear regression on the model. Since the data is a time series and numeric, this is a logical place to start and no further encoding is needed. Time is considered an interval variable, while the total vehicles variable is quantitative. 

Because of the small number of columns we are training on, we don't need to think about 'Best Subset Regression' or using Lasso or Ridge since they are mostly used for the opposite situation. 

<iframe
  src="asset_plots/base_model_test_p3a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We use two metrics to evaluate our plots: 
* Root Mean Squared Error: 31686.247
* $R*2$: -6.717

This performance isn't good. The out of sampel $R^2$ is very low and through teh visualization, we can see how different the predicted values are compared to the actual values. 


## Final Model

After looking at the data, we can see a curved pattern to the data so, we implement polynomial regression. We create a pipeline to allow us to test different degree polynomials. Through using GridSearchCV, it claims a polynomial of degree 3 works best. 

<iframe
  src="asset_plots/final_model_test_p4a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Evaluation Metrics: 
* Root Mean Squared Error: 33905.045
* $R*2$: 0.398

After predicting on our test data, we can see it performs better than our base model in terms of $R^2$, but worse in terms of RMSE. This is due to the final point of predicted values is very different to the expected one. However, all other values are considerably close. 

<!-- <iframe
  src="asset_plots/final_model_all_p4b.html"
  width="800"
  height="600"
  frameborder="0"
></iframe> -->

<!-- <iframe
  src="asset_plots/all_count_plot_p2a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe> -->