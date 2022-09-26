# Project Brief: Nairobi Listed Properties Scraping & Price Prediction

# Big Picture
Scrape property details of all listed houses in Nairobi from a leading real estate website; i.e., price, bedrooms, bathrooms, size, location, and available amenities and attempt to predict property prices using the provided data. 

# Motivation
1.	Create datasets using Kenyan data for further exploration by myself and other data aficionados. 
2.	Property prices in Nairobi have soared exponentially over the last 10 years, with some industry players concerned about a housing bubble. Can we use machine learning techniques to predict a property’s listed price given its publicly available features?

# Data Needs
1.	Primary property details from the main page: price, bedrooms, bathrooms, size, and location. 
2.	Secondary property details (amenities) from a property’s second page: garden, pool, parking, proximity to schools/shopping centers/etc., gym, etc. 
3.	Property’s location coordinates (in numeric form) for feature engineering. 

# Data Collection
1.	Create for-loop with range of pages containing properties.
	a.	Define URL, response, and beautiful soup object, and search parameters (from parsing HTML elements) 
	b.	Loop through houses and find house details using relevant HTML elements and save them in a dictionary, which is saved in a list. 
		i.	Find links to a house’s ‘next page,’ containing secondary property details (amenities) and retrieve all amenities.
		ii.	Loop through all amenities and create dictionary that gives each amenity a value of ‘1’.
		iii.	Create a pandas DataFrame (DF) from the dictionary containing property amenities and save it in a list outside loop.
2.	Create one list merging all individual house’s primary property details and a pandas DF from that list.
3.	Merge all DFs containing amenities (secondary property details) and replace NaNs with ‘0’ – to illustrate that a property does not have subject amenity.
4.	Merge the two DFs (primary property details & amenities) into one DF.
5.	Use Google’s Place API to retrieve the latitude and longitude of a property’s location and insert the two features into the DF.

# Data Preparation
1.	Drop duplicated rows if at least 6 columns are a match.
2.	Replace ‘Ksh’ and ‘,’ with blank
3.	Convert property sizes (ft2, acres) into a standard metric: square meters.
4.	Impute missing values with Simple Imputer if missing values are less than 15%.
5.	Insert new features, containing distance between property and key shopping centers, crime hotspots, and the City Centre.
6.	Drop unnecessary columns; i.e., those that will not be useful in modeling. 
7.	Distinguish categorical vs. numerical columns. 

# Modelling
1.	Plot correlation matrix of the features. 
2.	Compute the z-scores to inform scaler choice – some scalers are sensitive to outliers. Outliers have a z-score of -3<z>3. 
3.	Split data to train and test using a .8:.2 ratio.
4.	Initialize a random forest model without feature engineering (coordinates and distance from key areas) and assess performance.
5.	Initialize a random forest model with feature engineering and using all features and assess performance.
6.	Create a pandas Series with feature importance (weights) and plot top X features.
7.	Define a dataset containing redacted features and call the random forest model and assess performance. 
8.	Initialize a random search and assess performance
9.	Choose best performing option amongst the four options – assessed based on accuracy and computational cost. 
10.	Save chosen model using pickle.
11.	Define function to allow imputation of new inputs (property details) based on selected features and predict the price. 

