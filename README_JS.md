# Final_Project_Travel


# Machine Learning Model

![image](https://user-images.githubusercontent.com/82730954/134412569-9a566a18-0e42-45be-b2c7-889253558ee8.png)

For our ML model, we revisited an earlier idea of a simple linear regression model.  Upon reviewing some preliminary trends, we decided to select this model instead of our previously identified neural network model.  We made this change because we felt the linear model was easier to leverage and more effectively provided the predictions we wanted for our project.  By utilizing this model, however, we lose the ability to customize various options such as the number of hidden layers, the number of neurons in each hidden layer, and activation functions.  

Historical weather data was accessed from a PostgreSQL database.  A separate model was developed for each city (London and New York City), for each month of the year, and for each weather feature.  The weather features that our models predict are:
* average monthly high temperature
* total monthly rainfall
* total monthly snowfall (NYC only)
* total monthly sunshine hours (London only)

Minimal data cleaning was performed during the EDA and prior to the data being stored in the database.  Rows were removed where values were missing.  Indicators (#) of changes in sunshine measurement devices were removed from the value.  Our dataset does not contain any categorical data thus no encoding was performed.  

We used Scikit-learn's train_test_split to separate our dataset into training sets and testing sets.  Each model is trained on 75% of the dataset and tested on the remaining 25%.  To evaluate our models, we utilized Mean Squared Error (MSE).  

We compared performance of these individual-month models to models that included data for all months and used month number as an input.  When comparing model performance, the individual-month models generally had much better performance.  For the rainfall model, however, the combined model performed slightly better.  For consistency purposes, all models were broken out into individual months.  

In preliminary versions of our models, graphs were created with a scatter plot for training and testing data and a line for the prediction model.  

To create the predicted weather ranges for each city, we used the Mean Absolute Error (MAE) -/+ the predicted value.  We then rounded the total rainfall and snowfall to the nearest tenth of an inch.  For temperature and sunshine hours, we rounded down to the nearest integer for the low end of the prediction range and up to the nearest integer for the high end of the range.  

Initially we planned to show predictions for 2022 and 2023 but we found these ranges were nearly identical thus we only show one column for each weather feature.  An example for London is shown below:

![image](https://user-images.githubusercontent.com/82730954/134777236-cacda1c0-c73a-4030-aac7-fce428254126.png)

To ensure that we use the most appropriate model, we also created a neural network linear model and compared model performance.  We found that overall, model performance was generally better with the simple linear model.  For isolated months for some features had better performance.  For rainfall data the neural network model was slightly better.  Though the impact to our predictions would have been very minimal.  With greater customization of the various options, neural networks could prove to provide better experience at some point.  However, due to the simplicity and ease of use and interpretation, we decided to use the simple linear model for all predictions.  

Model performance varied.  Some factors influencing this include:
* monthly weather variance from year to year
* varying makeup of training and testing data
* varying weather features and scales

Mean Squared Error (MSE) for our high temp models varied from a low of 2.6 (August New York) to a high of 22.4 (January New York).  The average MSE for London was 8.8.  New York's average MSE was 10.3.

For rainfall, MSE ranged from 0.78 (July London) to 20.67 (August New York).  The average for London was 1.48.  New York averaged 6.91.

For London sunshine, MSE was significantly higher given the increased scale of sunshine hours per month, ranging from 163 (December) to 2249 (June).  The average was 977.

For New York snowfall, MSE ranged from 0.01 (October) to 91.91 (February).  The average was 14.65.

# Technologies

* Tableau for mapping and prompting user to select desired temperature
* PostgreSQL for data storage
* Jupyter Notebook for EDA, cleaning, machine learning


# Datasets

## Weather data

### London

Source:  https://www.metoffice.gov.uk/pub/data/weather/uk/climate/stationdata/heathrowdata.txt
More information:  https://www.metoffice.gov.uk/research/climate/maps-and-data/historic-station-data

The dataset contains monthly weather data for Heathrow (London Airport) from January 1948 - August 2021.  This dataset contains 884 rows and 7 columns of labels and values.  Each month includes details such as:
* Mean daily maximum temperature
* Mean daily minimum temperature
* Total rainfall
* Air frost days
* Total monthly sunshine (the device for measuring sunshine changed 9/2005.  Removed # indicator from sunshine data in Excel using substitute formula suggested here:  https://spreadsheetplanet.com/remove-specific-character-from-string-excel/)

The data was loaded into a DataFrame and grouped by month.  Averages and minimum and maximum values were generated.


### New York City

Source:  https://www.weather.gov/wrh/Climate?wfo=okx

Monthly summarized data was captured for NY-Central Park Area from the site above for 1948 - 2021.  This dataset has 884 rows and 6 columns of labels and values.  Each month includes the following details:
* Mean daily maximum temperature
* Mean daily minimum temperature
* Total precipitation
* Total snowfall

Using vlookups, the data was consolidated from multiple tables and worksheets into one CSV file that mimicked the format of the London data.  The dataset was loaded into a DataFrame and grouped by month.  Averages and minimum and maximum values were captured.

## Other data

### London Hotel Reviews

Latitude and longitude coordinates were added to this dataset.  Upon pivoting the data, there were approximately 20 hotels represented by the reviews.  Google Maps was used to obtain the coordinates and these were added to the reviews using a vlookup in Excel.  The reviews file was then saved in a CSV format with the two new columns.