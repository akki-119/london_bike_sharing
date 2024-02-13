# London Bike Sharing - Project

### Tools used: Tableau, Python, Jupyter Notebook

Interact with the final dashboard here: [Tableau Public dashboard](https://public.tableau.com/views/LondonBikeSharingDashboard_17076682500710/LondonBikeRidesDashboard?:language=en-US&:display_count=n&:origin=viz_share_link)

### Problem Statement:
Perform data pre-processing and create a dynamic dashboard to visualize the dataset for stakeholders to better understand and interpret the data and make business decisions.

#### Content
The data is acquired from 3 sources:

https://cycling.data.tfl.gov.uk/ 'Contains OS data © Crown copyright and database rights 2016' and Geomni UK Map data © and database rights [2019] 'Powered by TfL Open Data'
freemeteo.com - weather data
https://www.gov.uk/bank-holidays
From 1/1/2015 to 31/12/2016
The data from cycling dataset is grouped by "Start time", this represent the count of new bike shares grouped by hour. The long duration shares are not taken in the count.

#### Metadata:
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

"weathe_code" category description:
1 = Clear ; mostly clear but have some values with haze/fog/patches of fog/ fog in vicinity 2 = scattered clouds / few clouds 3 = Broken clouds 4 = Cloudy 7 = Rain/ light Rain shower/ Light rain 10 = rain with thunderstorm 26 = snowfall 94 = Freezing Fog

### Project workflow:

- Import and download dataset from kaggle
  
   ```python
    !kaggle datasets download -d hmavrodiev/london-bike-sharing-dataset
   
- Extract the file using the zipfile libraries
  
   ```python
    zipfile_name = 'london-bike-sharing-dataset.zip'
    with zipfile.ZipFile(zipfile_name, 'r') as file:
        file.extractall()

- Read the downloaded .csv file and performed data manipulation
  
  ```python
    bikes = pd.read_csv("london_merged.csv")

- Then saved the dataset as .xlsx file
  
  ```python
    bikes.to_excel('london_bikes_final.xlsx', sheet_name='Data')

- Next, I create a dynamic dashboard using Tableau.
The most important visualization created is the 'Moving Average' visualization with 'reference band' showcasing graphs in tooltip which provides information on the number of rides in different weathers and different hours of the day. I have also added a special feature where we can select a range of values and it will filter the other visualization with respect to the selection and the selection also gets highlighted.
  - To make this visualization, I created a two parameters named 'Moving Average Period' & 'Moving Average Rides' and made a line chart with them.
  ![Moving Average Visualization](images/moving_avg_viz.png)

I have also created a heatmap for 'Temperature vs Wind Speed' visualization which is filtered by the selection in 'Moving Average' visualization. It also contain the same tootltip as in 'Moving Average'.
  ![Heatmap](images/heatmap.png)

  **END OF DOCUMENT**
