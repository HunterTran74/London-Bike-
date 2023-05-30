#Project 1: London Bike sharing dataset 

For the start of this project, I came across the London Bike Sharing dataset on Kaggle.
The link to the dataset can be found right [here](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset).

For this project, I will be separating it into three main stages: preparation, analysis, conclusion  

## Before preparation
I begin by importing the dataset into R-studio by using the code below :

`library(readr)`

`london_merged <- read_csv("~/Downloads/london_merged.csv")`


After importing the dataset in R-studio, I take a look at the metadata of the dataset to understand what each column are
and what the unique values in the each column represents. The metadata for the dataset is listed below: 

"timestamp" - timestamp field for grouping the data

"cnt" - the count of a new bike shares

"t1" - real temperature in C

"t2" - temperature in C "feels like"

"hum" - humidity in percentage

"wind_speed" - wind speed in km/h

"weather_code" - category of the weather

"is_holiday" - boolean field - 1 holiday / 0 non holiday

"is_weekend" - boolean field - 1 if the day is weekend

"season" - category field meteorological seasons: 0-spring ; 1-summer; 2-fall; 3-winter.

-"weathe_code" category description:

1 = Clear ; mostly clear but have some values with haze/fog/patches of fog/ fog in vicinity 2 = scattered clouds / few clouds 3 = Broken clouds 4 = Cloudy 7 = Rain/ light Rain shower/ Light rain 10 = rain with thunderstorm 26 = snowfall 94 = Freezing Fog

After looking at the metadata, I install the tidyverse package in R as this is the standard package in R for doing
a majority of my analysis. The code to install and run the package is listed below :

`install.packages("tidyverse")`

`library(tidyverse)`

## Preparation
In this stage, I will using various techniques for data cleaning and data manipulation. 

I first begin by checking for null values in the dataset by using the code listed below:

`missinglondon_data <- london_merged[apply(is.na(london_merged), 1, any), ]`

`view(missinglondon_data)`

<img width="640" alt="view(missing data)" src="https://github.com/vader7412/Hunter/assets/134894494/959a17bb-66c9-4fd0-96f8-b078848ccc48">


Fortunately  there were no null values


**Next, I perform some data manipulation by creating rows and renaming unique categorical values**

I begin by  making a new column that measures temperature in the "t1" column in Farenheit instead of in celsius. The code for that is listed below.  

`london_merged$farenheit <- (london_merged$t1 *9/5) +32`


After that, I took the unique values in the "season" column and convert those unique values into the respective seasons that they represent. The code for this is listed below:

`london_merged$season <- ifelse(london_merged$season==0, "spring",london_merged$season)`

`london_merged$season <- ifelse(london_merged$season==1, "summer",london_merged$season)`

`london_merged$season <- ifelse(london_merged$season==2, "fall",london_merged$season)`

`london_merged$season <- ifelse(london_merged$season==3, "winter",london_merged$season)`


I use the same technique with the "weather_code" column : 

`london_merged$weather_code <- ifelse(london_merged$weather_code==1, "clear",london_merged$weather_code)`

`london_merged$weather_code <- ifelse(london_merged$weather_code==2, "scatter clouds/few clouds",london_merged$weather_code)`

`london_merged$weather_code <- ifelse(london_merged$weather_code==3, "broken clouds",london_merged$weather_code)`

`london_merged$weather_code <- ifelse(london_merged$weather_code==4, "cloudy",london_merged$weather_code)`

`london_merged$weather_code <- ifelse(london_merged$weather_code==7, "Rain",london_merged$weather_code)`

`london_merged$weather_code <- ifelse(london_merged$weather_code==10, "Rain with Thunderstorm",london_merged$weather_code)`

`london_merged$weather_code <- ifelse(london_merged$weather_code==26, "Snowfall",london_merged$weather_code)`


Then I decided to make a new column the represents the month from the "timestamp" column by extract the part the represents the month.
The code for that is listed below : 

`library (lubridate)`

`london_merged$month <- month (london_merged$timestamp,label=TRUE)`


I use the same technique like the previous one , but this time it is to extract the part that represents the days of the week 

`london_merged$days <- weekdays(london_merged$timestamp)`


## Analysis 

Next, I will be doing some analysis such as finding the average number of bike shares based on different factors such as days of the week, seasons, months, and weather conditions. 



For determining the average number of bike shares per season , I used the code below : 

`avgbikeshare_season <- tapply (london_merged$cnt,london_merged$season,mean)`


Then I take the results from the previous code and convert it into a data frame, basically a dataset in simpler terms. 

`avgbikeshare_seasondf <- data.frame(Season=names(avgbikeshare_season),num_avgbikeshare=avgbikeshare_season)`

This is the data frame: 

<img width="270" alt="average number of bike share per season" src="https://github.com/vader7412/Hunter/assets/134894494/d9ed4c70-0fa5-4615-bb51-e3d0e33426f0">


To get a better picture of the average number of bike shares per season, I put the results in a bar graph to better illustrate the difference. The code for that is listed below: 

`ggplot(data =avgbikeshare_seasondf,aes(x=Season,y=num_avgbikeshare))+`
  
` geom_bar(stat="identity", fill="pink",width=0.5) + geom_text(aes(label=round(num_avgbikeshare,2)) ,vjust = -0.5,size=3)+`
  
 ` labs(title = "Average number of bike share per season")`
 
 
![graph of average number of bike share per season](https://github.com/vader7412/Hunter/assets/134894494/201c0359-8dc9-46e8-a0fb-1496e7514069)


This makes sense as the average temperature in fahrenheit in the summer are warmer than the other seasons based on the data frame below : 

<img width="260" alt="average temperature per season " src="https://github.com/vader7412/Hunter/assets/134894494/9129efe6-59eb-435c-a65e-4703e29355ff">

  


For determining the average number of bike shares per month, each day of the week, and certain weather conditions, I used the same technique like before and here are the results: 



The data frame for average number of bike shares per month  : 


<img width="269" alt="average number of bike share per month " src="https://github.com/vader7412/Hunter/assets/134894494/5baa8280-ea74-4e28-b940-90c3a717162e">





The bar graph for average number of bike shares per month   : 

![graph of average number of bike share per month](https://github.com/vader7412/Hunter/assets/134894494/968d343d-f13f-4f44-b368-19209f75bab7)






The data frame for average number of bike shares for day of the week  :


<img width="281" alt="average number of bike share per day of the week " src="https://github.com/vader7412/Hunter/assets/134894494/6d18ea0e-e38f-4592-ac59-8da84f5aa4fb">






The bar graph for average number of bike shares for each day of the week:


![ graph average number of bike share per day](https://github.com/vader7412/Hunter/assets/134894494/b76356b0-c467-4381-9c21-3827f9b6d567)





The data frame for average number of bike shares for different weather conditions:


<img width="490" alt="average number of bike share for different weather condition " src="https://github.com/vader7412/Hunter/assets/134894494/91c72f9e-c42b-42b9-a0b8-ab6dde669021">







The bar graph for average number of bike shares for different weather conditions:



![graph of average number of bike shares on different weather conditions](https://github.com/vader7412/Hunter/assets/134894494/233c942e-354a-4ee2-b5c9-b9711d33d8f7)





## Conclusion 

Some suggestions for increasing the the number of bike shares would be to introduce a weekend pass or a seasonal pass. Some challenges that I encountered
when working on this project was adjusting the lables on the axis of the graph and turning the unique values of the categorical fields into the string values like how they are.  
  





































