#**Project 1: London Bike sharing dataset** 

For the start of this project, I came across the London Bike Sharing dataset on Kaggle.
The link to the dataset can be found right [here](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset).

For this project, I will be separating it into three main stages: preparation, analysis, conclusion  

## Before preparation
I begin by importing the dataset into R-studio by using the code below :
-`library(readr)
-london_merged <- read_csv("~/Downloads/london_merged.csv")
`

After importing the dataset in R-studio, I take a look at the metadata of the dataset to understand what each column are
and what the unique values in the each column represents. The metadata for the dataset is listed below: 

-"timestamp" - timestamp field for grouping the data
-"cnt" - the count of a new bike shares
-"t1" - real temperature in C
-"t2" - temperature in C "feels like"
-"hum" - humidity in percentage
-"wind_speed" - wind speed in km/h
-"weather_code" - category of the weather
-"is_holiday" - boolean field - 1 holiday / 0 non holiday
-"is_weekend" - boolean field - 1 if the day is weekend
-"season" - category field meteorological seasons: 0-spring ; 1-summer; 2-fall; 3-winter.

-"weathe_code" category description:
1 = Clear ; mostly clear but have some values with haze/fog/patches of fog/ fog in vicinity 2 = scattered clouds / few clouds 3 = Broken clouds 4 = Cloudy 7 = Rain/ light Rain shower/ Light rain 10 = rain with thunderstorm 26 = snowfall 94 = Freezing Fog

After looking at the metadata, I install the tidyverse package in R as this is the standard package in R for doing
a majority of my analysis. The code to install and run the package is listed below :
-`install.packages("tidyverse")
-library(tidyverse)`

## Preparation
In this stage, I will using various techniques for data cleaning and data manipulation. 

I first begin by checking for null values in the dataset by using the code listed below: 









