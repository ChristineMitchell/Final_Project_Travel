#  Big City Vacation

## Team:
Laura Clark (circle), Christine Mitchell (square), and Josh Stephens (triangle)

## Why did we choose this topic:
Our team was interested in creating a fun and adventurous project utilizing tools and skills that we learned throughout the course. We all enjoyed working with maps. So, we thought how exciting it would be to plan out a trip to a few major cities by creating an interactive layered map visualization in tableau.

## Presentation:
https://docs.google.com/presentation/d/e/2PACX-1vSHPDfYkY7D8Y6JWAzLDjEQbPk9rEafHPrW1vApHoetRfHzEp_DiWalxgsOKQDRdVrYqmN-JER3ABk_/pub?start=true&loop=false&delayms=3000

## Story:
Big City Vacation: Choose from NYC or London. 
When shall you go? Our team provides a table of predicted weather so that you can make your own decision based on your comfort level.
Would you like to build an itinerary? Our tableau story board offers multiple maps for each of the cities, one layers hotels, another provides points of interests, and the last map showcases food and spirit options.

## Dashboard:
https://public.tableau.com/app/profile/laura.clark2190/viz/VacationProject/VacationStory?publish=yes

![VacationStory](https://user-images.githubusercontent.com/82008319/135797705-0cc8d86a-25cf-4cff-bf5e-5247bb18df33.png)

![VacationStory (1)](https://user-images.githubusercontent.com/82008319/135797724-f6bf793d-989a-4140-9e7d-0a10ced102c5.png)



## Tools & Technologies: 
<li>	Excel for initial csv file data exploration and some cleaning. </li> <br/> 

<li>	Jupiter Notebook using Python & PANDAS library to further explore data, clean the data, and train the model. </li> <br/> 

<li>	Data Storage: Chose to change from Mongo DB to a PostgreSQL DB with this deliverable to store our weather data for predictive modeling. Please see the schema below. </li> <br/> 

![image](https://user-images.githubusercontent.com/82008319/134836752-e36d1b39-bd09-4849-a8a6-cb9532132fef.png)

<li>	Tableau to develop our interactive dashboard and create a layered map with points of interest for a vacation in NYC or London. Points of interest will include hotels, eateries, and attractions and will be loaded with csv files.</li> <br/> 

<li>	Updated our Machine Learning Model from Neural Network Model to a simpler Linear Regression Model. Upon reviewing some preliminary trends, we decided to select this model instead of our previously identified neural network model. We made this change because we felt the linear model was easier to leverage and more effectively provided the predictions we wanted for our project. By utilizing this model, however, we lose the ability to customize various options such as the number of hidden layers, the number of neurons in each hidden layer, and activation functions.

![image](https://user-images.githubusercontent.com/82008319/136149357-9056d139-2811-44b1-b364-781238195d04.png)

A separate model was developed for each city (London and New York City), for each month of the year, and for each weather feature. The weather features that our models predict are:

<li>	average monthly high temperature</li> 
<li>	total monthly rainfall</li> 
<li>	total monthly snowfall (NYC only)</li> 
<li>	total monthly sunshine hours (London only)</li> <br/>  

## Model Performance:
Model performance varied. Some factors influencing this include:

<li>	monthly weather variance from year to year</li> 
<li>	varying makeup of training and testing data</li>  
<li>	varying weather features and scales</li> <br/>   

![image](https://user-images.githubusercontent.com/82008319/136144380-d3cf0f69-8e1e-48cb-b73f-d457575b269b.png)

During our presentation, we were asked about r-squared scores which we had not originally captured. We reran the model, this time adding a random_state value, and the r-squared scores of our updated model are shown below. There is not a strong correlation between our values and the weather can be difficult to predict precisely. This is even true for meterologists predicting tomorrow's weather. Since our project was to show the big picture for our travelers and we created prediction ranges instead of trying to predict precise values, we're hopeful our predictions will both be helpful to travelers and reasonably accurate.

![image](https://user-images.githubusercontent.com/82008319/136459951-29a96987-d7f1-497a-825a-fb24a9eb8e89.png)

Full model results and performance are include in the appendix below.

For future analysis, we should compare our predictions to the actual weather conditions for each month for 2022 and 2023. This will allow us to evaluate the effectiveness of our models and prediction approach.

## Weather Predictions:
Once our weather predictions were created, we iterated through several layouts and color schemes so the tables are as easy for our customer to interpret as possible. We used a number of suggestions from Storytelling with Data: A Data Visualization Guide for Business Professionals by Cole Nussbaumer Knaflic to help reduce clutter and increase clarity. We also used an online simulator to ensure that those who are color blind can differentiate between highs and lows.

![image](https://user-images.githubusercontent.com/82008319/136265211-e7f84235-3f7a-47aa-bc99-10cfd87d8baa.png) <br/>  

![image](https://user-images.githubusercontent.com/82008319/136265253-f7252fa6-d311-4e10-9ea8-fe1f6ed45d61.png)

## Data Sources:
### Weather Data:

LONDON: <br/> 
Source: https://www.metoffice.gov.uk/pub/data/weather/uk/climate/stationdata/heathrowdata.txt <br/> 
More information: https://www.metoffice.gov.uk/research/climate/maps-and-data/historic-station-data <br/> <br/>
The dataset contains monthly weather data for Heathrow (London Airport) from January 1948 - August 2021. This dataset contains 884 rows and 7 columns of labels and values. Each month includes details such as:<br/> 
<li>	Mean daily maximum temperature </li> 
<li>	Mean daily minimum temperature </li> 
<li>  Total rainfall </li> 
<li>	Air frost days </li> 
<li>	Total monthly sunshine (the device for measuring sunshine changed 9/2005. Removed # indicator from sunshine data in Excel using substitute formula suggested here: https://spreadsheetplanet.com/remove-specific-character-from-string-excel/) </li> <br/> 
The data was loaded into a DataFrame and grouped by month. Averages and minimum and maximum values were generated. <br/> <br/>

NEW YORK CITY:<br/>
Source: https://www.weather.gov/wrh/Climate?wfo=okx <br/> 
Monthly summarized data was captured for NY-Central Park Area from the site above for 1948 - 2021. This dataset has 884 rows and 6 columns of labels and values. Each month includes the following details: <br/> 
<li>	Mean daily maximum temperature </li> 
<li>	Mean daily minimum temperature </li> 
<li>	Total precipitation </li> 
<li>	Total snowfall </li> <br/> 
Using vlookups, the data was consolidated from multiple tables and worksheets into one CSV file that mimicked the format of the London data. The dataset was loaded into a DataFrame and grouped by month. Averages and minimum and maximum values were captured. <br/> <br/> 

### Hotels:
The property name, address, and rating will be utilized in our layered map pop up marker. The coordinates are necessary to include them on our map.<br/><br/>

LONDON:<br/>
https://www.yelp.com/developers/documentation/v3/business_search<br/>
Extracted a data set that included the property name, type of property, rating, price, location (address & coordinates), and url.<br/><br/>

NEW YORK CITY:<br/>
https://www.yelp.com/developers/documentation/v3/business_search<br/>
Extracted a data set that included the property name, type of property, rating, price, location (address & coordinates), and url.<br/><br/>

### Points of Interest:
LONDON:<br/>
It took a while to find a website with the desired data, and that was http://tour-pedia.org/about/datasets.html <br/>
Although it needed heavy editing and some geocoordinates from an API, this had the information about the name and address. <br/><br/>

NEW YORK CITY:<br/>
Data.gov was used and these were all the datasets pulled<br/>
<li>	https://catalog.data.gov/dataset/new-york-city-museums </li> 
<li>	https://catalog.data.gov/dataset/new-york-city-art-galleries </li> 
<li>	https://catalog.data.gov/dataset/new-york-city-water-trail-kayak-and-canoe-launch-sites </li> 
<li>  https://catalog.data.gov/dataset/directory-of-temporary-public-art </li> 
<li>	https://catalog.data.gov/dataset/nyc-parks-monuments </li> <br/>
Although the format differed between most of the datasets, they all had a name, most had an address, and all had latitude and longitude in one form or another<br/><br/>

### Restaurants:
https://www.yelp.com/developers/documentation/v3/business_search<br/>
We originally were going to use YELP dataset via Kaggle, however found that the dataset offered was limited. For example there were only three restaurants in NYC. Therefore, we decided to utilize the Yelp Business Search API. Next, we found that YELP set a data limit of 200 records (fifty records per call) up to two hundred records with the established parameters). Hence, we created batches of sets of 200 based on restaurant types to build our dataset. Continuing with the NYC Restaurant example we went from 3 records in Deliverable 1, to 200 for Deliverable 2, and finished up with over 4,000 records for Deliverable 3.<br/><br/>

### Appendix

## High Temperature Model
![image](https://user-images.githubusercontent.com/82008319/136265328-a821afed-5720-45fe-83de-89d8788c1b90.png)

## Precipitation Model Results
![image](https://user-images.githubusercontent.com/82008319/136265372-1b03a160-28c7-4844-a0c9-d806f94af52b.png)

## NYC Snowfall Model Results
![image](https://user-images.githubusercontent.com/82008319/136265412-e8724981-dee7-43c4-ab22-7a5958a7dd4c.png)

## London Sunshine Model Results
![image](https://user-images.githubusercontent.com/82008319/136265464-7db9217b-3b8c-40a8-a46e-eb78a7c115f8.png)

## New models including r-squared scores

Below are outputs, including r-squared scores, from new models.  Because we did not use a random_state value in earlier stages of our models, the outputs from these models differ and cannot be compared directly to the results above.  Next time, we would use a random_state value throughout to increase consistency and reduce pain points.

### New high temp models with r-squared scores

![r2_high_temp_model_results](https://user-images.githubusercontent.com/82730954/136567832-5f66df30-0268-4ebf-b6c9-00f6de92ce45.png)

### New precipitation models with r-squared scores

![r2_precip_model_results](https://user-images.githubusercontent.com/82730954/136567860-5e70568a-3810-44a8-9424-e759f6488485.png)

### New NYC snowfall models with r-squared scores

![r2_snowfall_model_results](https://user-images.githubusercontent.com/82730954/136567887-444285cc-31e6-49bd-b2bb-b5a5999d6c70.png)

### New London sunshine models with r-squared scores

![r2_sunshine_model_results](https://user-images.githubusercontent.com/82730954/136568249-ab252b9b-5c9f-4011-9f78-2cdd74f57c37.png)

