# Compare_data_AIRBNB
Compare Airbnb listing Data between Boston and Seattle 

**Data Source:**
#!/bin/bash
curl -L -o ~/Downloads/boston.zip\
  https://www.kaggle.com/api/v1/datasets/download/airbnb/boston

  #!/bin/bash
curl -L -o ~/Downloads/seattle.zip\
  https://www.kaggle.com/api/v1/datasets/download/airbnb/seattle

**  Comparison Aspects**

Key points to compare within the Seattle Airbnb data include:

1.Price distribution:
  Compare the distribution of listing prices to identify high-priced vs. low-priced neighbourhood.
2.Room type analysis:
  Compare the prevalence of room types (entire home, private room, shared room).
3.Price distrubution of the listing :
 Compare price distribution of the listing.
4.Neighborhood insights:
 Compare prices and availability across neighborhoods.
5.Review analysis:
 Compare reviews, ratings, and the number of reviews per listing.
6.Host behavior:
 Compare superhosts, multiple listings per host, and host responses.

1.# Distribution of Neighborhoods Seatle

# Price distribution:Distribution of Neighborhoods in Seatle and Distribution of Neighborhoods in Boston
neighborhood_counts = seatle_listing_df['neighbourhood_group_cleansed'].value_counts().head(10) # Calculate the distribution of listings by neighborhood

# Create a bar chart for the top neighborhoods with the most listings in Seatle
plt.figure(figsize=(10, 8))
sns.barplot(x=neighborhood_counts.values, y=neighborhood_counts.index, palette="coolwarm")
plt.title('Top Ten Neighborhoods by Number of Listings in Seatle')
plt.xlabel('Number of Listings in Seatle')
plt.ylabel('Neighborhood in Seatle')
plt.show()

<img width="1101" alt="Screenshot 2024-12-17 at 22 34 49" src="https://github.com/user-attachments/assets/fe6fade0-48f6-4ea4-890b-712e144f3769" />

# Create a bar chart for the top neighborhoods with the most listings in Boston


