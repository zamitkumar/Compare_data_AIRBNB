# Compare_data_AIRBNB
Compare Airbnb listing Data for Seattle 

**Data Source:**

  #!/bin/bash
curl -L -o ~/Downloads/seattle.zip\
  https://www.kaggle.com/api/v1/datasets/download/airbnb/seattle
  
**Key Highlights**
Price and Accommodation Features:Explore how listing prices correlate with features like the number of bedrooms, guest capacity, and overall amenities.
Property and Room Types:Discover the most popular property types and room preferences among Airbnb guests in Seattle.
Neighborhood Popularity:Identify the most sought-after neighborhoods based on the number of listings, guest reviews, and pricing trends.
Occupancy and Availability:Uncover seasonal patterns and localized demand variations to understand how often properties are booked throughout the year.
Review Scores Rating Distribution: The review scores of Airbnb listings provide a vital measure of guest. satisfaction, reflecting the overall experience of staying in a property. 
Analyzing the distribution of these scores reveals trends in guest feedback and helps identify areas where hosts excel or need improvement.

**Load and Inspect the Dataset**
Install and load all the required libraries of python

Load the data into data farme 

Analyze the Distribution and Delete the duplicate data

Drop duplicate columns

Drop columns with full NA

Drop columns representing url

Dropping specified columns with high missing values

Dropping host-related information (selecting by pattern)

Listing the numerical and categorical columns

Verify that all columns in numerical_columns are numeric

Dealing With Null Values
Categorical columns with mode imputation With Median and frequently used value for non numerical column 

Summary statistics for price

Estimating occupancy rates Seatle

Distribution of Property Types in Seatle

Calculate the distribution of the property types

Create a bar chart for the distribution of property types

Distribution of Neighborhoods Seatle
Create a bar chart for the top neighborhoods with the most listings
Room Type Preferences
Compare the Number of Listings by Neighborhood
Compare Availability by Neighborhood Properties listing 
Review Scores Rating Distribution

