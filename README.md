# Citibike Data Analysis and Optimization

Citibike bike sharing system has been contributing in New York City’s public transportation since 2013. This project focuses on the issue of the availability of an appropriate number of bikes at a station and the factors affecting the use of Citibike sharing system. Citibike provides its bike usage data to public for analysis and improvements in their initiative. Their data for the month of March, July, October, and December was analysed along with the weather data. The observations include charts showing ride patterns for all four months and the variation in bike usage during peak hours, weekdays, weekends, and public holidays for different types of users. Correlation with weather parameters like snow, wind, and temperature was found.  A direct dependency of these parameters on number of riders was observed. Moreover, popular routes with the high number of riders were found to solve one of the issues and contribute to the bike sharing industry.

### About Dataset:
The data has files from the month of July 2013 to January 2018. I have analyzed the data from four months of March, July, October and December for the year 2017 to cover all the seasons.
The dataset contains the following attributes:

| Attribute | Metadata of Attribute |
| --------- | --------------------- |
| Trip Duration (in seconds) | Shows the time it took to finish the bike ride |
| Bike ID | Unique ID for the bike |
| Start Trip Timestamp | Timestamp when the trip was started |
| End Trip Timestamp | Timestamp when trip was ended |
| Start Station ID | Station ID of the station from where the trip was started |
| End Station ID | station ID of the station where trip ended |
| Start Station Name | NYC addresses consisting of St and Ave |
| End Station Name | NYC addresses consisting of St and Ave |
| Start Station Latitude / Longitude | Coordinates of the `Start Station Name` | 
| End Station Latitude / Longitude | Coordinates of the `End Station Name` |
| User Type | Customer => 24-hour (1 day) pass or 3-day pass; Subscriber => Annual Membership |
| Gender | (Zero = Unknown; 1 = Male; 2 = Female) |
| Year of Birth | Birthyear of the user |

#### Feature Extraction:

Day, Month, Year, Hour and Minutes were extracted from the `Start Trip Timestamp` and `End Trip Timestamp`. Some extra features for the data analysis were engineered. `isWeekend` holds the boolean value `True` if the given day is a weekend and `False` otherwise. `isHoliday` holds the boolean value `True` if the given day is the public holiday. and `False` otherwise.

### Results:

#### A. Rush Hour 

There are two peaks for `usertype` Subscriber while `usertype` Customer has a curve from 10 AM to 7 PM with maximum number of customer riders.
 
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/rush_hour_sub.jpg) 
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/rush_hour_cust.jpg)

#### B. Daily Ride Analysis

There is a fine correlation between the fact that if a particular day is a weekend or not and the number of subscribers and number of customers. The number of subscribers are particularly high on weekdays while the number of customers are high on weekends. This makes sense as the subscribers are the users who use CitiBike service for their daily commute to and from work. A special case can be noticed for 4th of July, which is the public holiday. Even though 4th of July is a weekday, we have a higher number of customers on that day. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/ride_count_july_sub.jpg)
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/ride_count_july_cust.jpg) 

Similar kind of a trend is observed for the month of March. However, the total number of riders are decreased for both the type of usertype customer and subscriber. While there is a drastic reduction in user type customer, number of subscribers are decreased as well. Specifically, on the days of 14th, 15th and 16th of March, no riders are noticed. As with subscribers, more number of subscribers are noticed for the weekdays and on weekends, more number of customers are noticed. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/ride_count_march_sub.jpg)
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/ride_count_march_cust.jpg) 

Similar trend for month of October. However, significantly lower rides in last week of October is observed. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/ride_count_oct_sub.jpg)
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/ride_count_oct_cust.jpg) 

In December, very low number of rides are noticed. That makes me wonder if weather parameters are affecting. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/ride_count_dec_sub.jpg)
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/ride_count_dec_cust.jpg) 

#### C. Weather Parameter:

Weather information was downloaded from [National Oceanic and Atmospheric Administration (NOAA)](http://www.noaa.gov/weather). Below weather parameters were considered. 

| Parameter | Abbreviation |
| ---------- | ----------- |
| Average Daily Temperature | TAVG |
| Maximum Daily Temperature | TMAX |
| Minimum Daily Temperature | TMIN |
| Snow Fall | SNOW |
| Snow Width on Ground | SNWD |
| Precipitation | PRCP |
| Air Wind | ANWD |

The integration was done for the daily ride count and weather parameters. Since the range of data now varies a lot, it was necessary to standardize the data so that it is easier to visually analyze it.  Correlation was found out with each weather parameter on a monthly basis for both the rider types separately. 

Fig below shows the correlation of weather parameter and ride counts across two different types of usertypes for four months. The major correlations are highlighted. Some weather parameters like `SNOW`, `SNWD`, `PRCP` and `AWND` always have negative correlation hence, their values in the combined dataset is inverted so that, they would have positive correlation, which is easy to validate visually. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/coor.jpg)

#### 1) Ride Count for March with Weather Parameter:

Weather parameters like TMAX and SNWD are influential to explain the variations in number of rides for the month of March. When `SNWD` and `TMA`X reaches its minimum values, the number of rides for both the usertype reaches their respective minimum value as well. Interestingly, for the customer, it is expected that the number of customer rides would be higher in weekends than in weekdays but for month of March, for the first three weeks, a reverse trend is observed. For these three weeks, the `TMAX` is observed to be lower than the usual weekdays temperature. This concludes that, `TMAX` supersedes `isWeekend` parameter. The number of customer rides would only be higher if the temperature is above certain threshold value. As seen in the last week of March, we have higher number of customer rides as the temperature rises.

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/weather_march_sub.jpg)
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/weather_march_cust.jpg)

#### 2) Ride count for July with Weather Parameters:

`TMAX` parameter for month of July does not show high correlation, it is observed that it is capable enough to explain the lower values for both the usertypes. The lowest value for ride counts for subscriber and customer occur when the month has lowest value for `TMAX`. That simply implies that above a certain threshold temperature, the temperature would not help much to explain the variations of the riders. However, below that threshold, the number of riders are somewhat related to the variations of temperature. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/weather_july_sub.jpg)
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/weather_july_cust.jpg)

#### 3) Ride count for October with Weather Parameters:

There is sharp drop in the number of riders on 29th October for both the usertypes, which can be explained with a similar drop in `PRCP` as well. Similarly, other minor drops can be explained.

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/weather_oct_sub.jpg)
![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/weather_oct_cust.jpg)

#### 4) Ride count for December with Weather Parameters:

For the month of December, `TMAX` is an influential weather parameter on the number of riders. the variation in number of riders can be explained with the variation in `TMAX` parameter for the month of December. Interesting to note that unlike the month of July, the range of `TMAX` parameter is lower which again points to the finding that below a certain threshold temperature, it is able to explain the variations of number of riders. 

#### D. Ride Patterns

To be able to understand the unbalancing of bikes at stations, it is important to get an idea of which stations are under stress, during the rush hours. Some well-known point of interest is used in the heat maps better understand the distribution of the riders across the city. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/legend_heatmap.jpg)

Below googlemap graphs are prepared using [gmplot](https://github.com/vgm64/gmplot)- A matplotlib-like interface to generate the HTML.

#### 1) Heatmap of Subscriber for the Weekday Rush Hours:

The heatmap is plotted to see the distribution of riders in the city and to see is there any trending for the highly clustered places over the four months. Therush hour stations during the weekdays for the usertype subscriber in the morning are highly clustered in and around places like Empire State Building, Grand Central Terminal, Rockefeller Center and Time Square. These stations are pretty consistent with all four seasons as well. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/weekday_sub_heatmap.jpg)

[From Left: March, July, October, December]

#### 2) Heatmap of Customer for the Weekend Rush Hours:

The heatmap for customer during weekends rush hours (10AM – 7PM) yields the stations and places most likely used by the customers. It is visually seen that the customer interest places are quite different than the subscriber stations. There is a clear distinction with top 10 stations for both the user type. Stations with high customer visits are the areas in and around Central Park, Washington State Park and Brooklyn Bridge. These areas are pretty consistence with all four months as well. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/weekday_cust_heatmap.jpg)

[From Left: March, July, October, December]

#### 3) Popular Routes:

The popular routes are plotted on the graph to show which routes in the city may have a higher number of bikers. The routes around Central Park are highly dominated by Customers. The office areas like Manhattan and Lower Manhattan are usually the routes taken by Subscribers. 

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/popular_routes_all.jpg)

[From Left: March, July, October, December]

#### 4) Stations where bikes are manually transffered:

The number of stations where bikes are transferred manually when a station has less number of bikes than required are changing with months. As observed, more number of stations are pretty close to Central Park, a customer dominated area.

![](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/mt.jpg)

[From Left: March, July, October, December]


#### E. Optimization and ML Model: (Soon to be added.) 



#### Conclusion:

With the observations mentioned in the above section, it can be concluded that the number of rides in a particular month is related to day of month, time of day and weather parameters. In particular, such weather parameters do not have linear relationship with the number riders. As discussed, for the month of July, none of thee weather parameters show a good enough correlation while for the month of March, Snow Width (`SNWD`) and Maximum Temperature  (`TMAX`) are more effective to explain the variations. On the other hand, for the month of October and December, Precipitation (`PRCP`) and Maximum Temperature are influential. With different seasons, different parameters act to  it. One relation is constant across all seasons is the relationship  of weekends to customers and weekdays to subscribers. The map analysis suggest that subscribers tend to visit office areas of Manhattan and Lower Manhattan while, customer’s favorite places include Central Park, Washington State Park and Brooklyn Bridge. This finding is backed up the path plotting on the map as well. Wirth that, stations with highest manual bike transfers are plotted. These maps are not very consistence with different month in terms of stations but areas near Central Park tend to have the scarcity of bikes across all seasons. 

