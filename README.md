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
Review Scores Rating Distribution: The review scores of Airbnb listings provide a vital measure of guest. satisfaction, reflecting the overall experience of staying in a property. Analyzing the distribution of these scores reveals trends in guest feedback and helps identify areas where hosts excel or need improvement.

**Load and Inspect the Dataset**
Install and load all the required libraries of python
from sklearn.preprocessing import StandardScaler
import matplotlib.pyplot as plt # plotting
import numpy as np # linear algebra
import os # accessing directory structure
import pandas as pd # data processing, CSV file I/O (e.g. pd.read_csv)
from sklearn.impute import SimpleImputer
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')


Load the data into data farme 
seattle_listing_df = pd.read_csv("./seattle/listings.csv")
seattle_listing_df.head(5)
seatle_listing_df.info()

Analyze the Distribution and Delete the duplicate data

Drop duplicate columns
seatle_listing_df = seatle_listing_df.T.drop_duplicates().T
verfy: seatle_listing_df.head(5)

Drop columns with full NA
seatle_listing_df.dropna(axis=1, how='all', inplace=True)

Verfy 
Seatle_listing_df.head()

Drop columns representing url
seatle_listing_df.drop(seatle_listing_df.columns[seatle_listing_df.columns.str.contains("url")], axis=1, inplace=True)

Dropping specified columns with high missing values
columns_to_drop = [
    'square_feet', 'summary', 'space', 'neighborhood_overview', 'notes', 'transit',
]

Dropping host-related information (selecting by pattern)
host_related_columns = seatle_listing_df.columns[seatle_listing_df.columns.str.contains('^host_')]
columns_to_drop.extend(host_related_columns)

Listing the numerical and categorical columns
numerical_columns = seatle_listing_df.select_dtypes(exclude=object).columns.tolist()
categorical_columns = seatle_listing_df.select_dtypes(include=object).columns.tolist()
seatle_listing_df[numerical_columns].head()
seatle_listing_df[categorical_columns].head()

Convert columns to numeric and coerce errors
#seatle_listing_df[numerical_columns] = seatle_listing_df[numerical_columns].apply(pd.to_numeric, errors='coerce')

Verify that all columns in numerical_columns are numeric
print(seatle_listing_df[numerical_columns].dtypes)
Check numerical_columns content

Dealing With Null Values
Numeric columns: Use median imputation
numeric_imputer = SimpleImputer(strategy='median')
seatle_listing_df[numerical_columns] = numeric_imputer.fit_transform(seatle_listing_df[numerical_columns])

Categorical columns with mode imputation
categorical_imputer = SimpleImputer(strategy='most_frequent')
seatle_listing_df[categorical_columns] = categorical_imputer.fit_transform(seatle_listing_df[categorical_columns])

Summary statistics for price
seatle_listing_df['price'].describe()

Estimating occupancy rates Seatle
average_annual_availability = seatle_listing_df['availability_365'].mean()
estimated_annual_occupancy_rate = 100 - (average_annual_availability / 365 * 100)
estimated_annual_occupancy_rate

Distribution of Property Types in Seatle
sns.set_style("whitegrid")  # Set the aesthetic style of the plots

 Calculate the distribution of the property types
property_type_counts_seatle = seatle_listing_df['property_type'].value_counts()

Create a bar chart for the distribution of property types
plt.figure(figsize=(10, 8))
sns.barplot(x=property_type_counts_seatle.values, y=property_type_counts_seatle.index, palette="Blues_d")
plt.title("Distribution of Property Types in Seattle")
plt.xlabel("Number of Listings in Seattle")
plt.ylabel("Propery Type in Seattle")
plt.show()

Distribution of Neighborhoods Seatle
neighborhood_counts = seatle_listing_df['neighbourhood_group_cleansed'].value_counts().head(10) # Calculate the distribution of listings by neighborhood

Create a bar chart for the top neighborhoods with the most listings
plt.figure(figsize=(10, 8))
sns.barplot(x=neighborhood_counts.values, y=neighborhood_counts.index, palette="coolwarm")
plt.title('Top Ten Neighborhoods by Number of Listings in Seatle')
plt.xlabel('Number of Listings in Seattle')
plt.ylabel('Neighborhood in Seatle')
plt.show()

Price Distribution
plt.figure(figsize=(12, 6))
sns.histplot(seatle_listing_df['price'], bins=50, kde=True, color="green")
plt.title('Distribution of Listing Price in Seattle')
plt.xlabel('Price in USD')
plt.ylabel('Number of Listings in Seattle')
plt.xlim(0, seatle_listing_df['price'].quantile(0.95))  # Limiting x-axis to 95th percentile for better visualization
plt.show()

Room Type Preferences
plt.figure(figsize=(10, 6))
sns.countplot(data=seatle_listing_df, y='room_type', order=seatle_listing_df['room_type'].value_counts().index)
plt.title('Room Type Preferences')
plt.xlabel('Number of Listings')
plt.ylabel('Room Type')
plt.show()

Compare the Number of Listings by Neighborhood
plt.figure(figsize=(10, 8))
sns.countplot(data=seatle_listing_df, y='neighbourhood_group_cleansed', order=seatle_listing_df['neighbourhood_group_cleansed'].value_counts().index)
plt.title('Number of Listings by Neighborhood in Seattle')
plt.xlabel('Number of Listings in Seattle')
plt.ylabel('Neighborhood in Seattle')
plt.show()

Price by Room Type
plt.figure(figsize=(12, 6))
sns.boxplot(x='room_type', y='price', data=seatle_listing_df)
plt.title('Price Distribution by Room Type')
plt.xlabel('Room Type')
plt.ylabel('Price ($)')
plt.ylim(0, seatle_listing_df['price'].quantile(0.85))  # Limiting y-axis to 85th percentile for better visualization
plt.show()

Compare Availability by Neighborhood Properties listing 
plt.figure(figsize=(12, 8))
sns.boxenplot(y='neighbourhood_group_cleansed', x='availability_365', data=seatle_listing_df)
plt.title('Availability by Neighborhood in Seattle')
plt.xlabel('Availability (Days out of 365) in Seattle')
plt.ylabel('Neighborhood in Seattle')
plt.show()

Review Scores Rating Distribution
plt.figure(figsize=(12, 6))
sns.histplot(seatle_listing_df['review_scores_rating'], bins=20, kde=True, color='pink')
plt.title('Distribution of Review Scores Rating')
plt.xlabel('Review Scores Rating')
plt.ylabel('Number of Listings')
plt.xlim(0, 100)  # Review scores are typically on a scale from 0 to 100
plt.show()
