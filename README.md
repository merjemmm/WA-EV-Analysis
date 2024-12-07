# Electric Vehicles in Washington

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


<iframe
  src="asset_plots/all_count_plot_p2a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="asset_plots/all_count_plot_p2a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="asset_plots/zoomin_plot_p2b.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="asset_plots/non_ev_all_v_plot_p2c.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


<iframe
  src="asset_plots/make_ev_hist_p2e.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>




## Baseline Model

<iframe
  src="asset_plots/base_model_test_p3a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Final Model

<iframe
  src="asset_plots/final_model_test_p4a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="asset_plots/final_model_all_p4b.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="asset_plots/all_count_plot_p2a.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>