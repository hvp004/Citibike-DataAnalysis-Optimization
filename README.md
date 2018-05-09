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

### Results:

#### A. Rush Hour 

There are two peaks for `usertype` Subscriber while `usertype` Customer has a curve from 10 AM to 7 PM with maximum number of customer riders.
 
![alt text](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/rush_hour_sub.jpg)

![alt text](https://github.com/hvp004/Citibike-DataAnalysis-Optimization/blob/master/graphs/rush_hour_cust.jpg)

