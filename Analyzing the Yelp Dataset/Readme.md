# Profiling and Analyzing the Yelp Dataset
## Background
For this assignment, specifically, you are going to be playing the role of a real-world data scientist using SQL to both answer specific questions for an organization and make inferences based on your discoveries. 

We will be using a dataset from a US-based organization called Yelp, which provides a platform for users to provide reviews and rate their interactions with a variety of organizations – businesses, restaurants, health clubs, hospitals, local governmental offices, charitable organizations, etc. Yelp has made a portion of this data available for personal, educational, and academic purposes.

You will be asked a series of questions regarding the data to help you profile and better understand the data in the first part of the assignment. Once you have answered each question, you will come up with your own question for analysis and will prepare a dataset for the analysis you choose to do in the second part of the assignment.

## Yelp Dataset ER Diagram
The entity relationship (ER) diagram below, should help familiarize you with the design of the Yelp Dataset provided for this peer review activity.

<p align = "center">
<img src = "https://user-images.githubusercontent.com/94797745/147790386-d90484bd-5491-4078-a78d-f3b4892b67a9.png" width = "600" height = "550">
  
## 🧙‍♂️ Case Study Questions & 🚀 Solutions
  
## Part 1: Yelp Dataset Profiling and Understanding
#### 1. Profile the data by finding the total number of records for each of the tables below:
i.	Attribute table:
Using the query 
  
        SELECT COUNT (*) FROM attribute;
we find that the number of records in the Attribute table is 10000 
  
ii.	Business table:
Using the query 
  
        SELECT COUNT (*) FROM business; 
we find that the number of records in the Business table is 10000 
  
iii.	Category table:
Using the query
  
        SELECT COUNT (*) FROM category;
we find that the number of records in the Category table is 10000 
  
iv.	Checkin table: 
Using the query
  
        SELECT COUNT (*) FROM checkin; 
we find that the number of records in the Checkin table is 10000 

v.	elite_years table:
Using the query 
  
      SELECT COUNT (*) FROM elite_years;
we find that the number of records in the elite_years table is 10000 
  
vi.	friend table:
Using the query 
  
        SELECT COUNT (*) FROM friend; 
we find that the number of records in the Friend table is 10000 
  
vii.	hours table:
Using the query 
  
        SELECT COUNT (*) FROM hour;
we find that the number of records in the Hour table is 10000 
  
viii.	photo table:
Using the query
  
        SELECT COUNT (*) FROM photo; 
we find that the number of records in the Photo table is 10000 
  
ix.	 review table:
Using the query 
  
        SELECT COUNT (*) FROM review; 
we find that the number of records in the Review table is 10000 
  
x.	tip table:
  
Using the query 
  
        SELECT COUNT (*) FROM tip; 
we find that the number of records in the Tip table is 10000 
  
xi.	user table:
  
Using the query 
        SELECT COUNT (*) FROM user;
we find that the number of records in the User table is 10000 

#### 2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.
i.	Business: 10000 Distinct records
  
          SELECT COUNT (DISTINCT (id)) FROM business;
  
ii.	Hours: 1562 Distinct records
  
          SELECT COUNT (DISTINCT (business_id)) FROM hours;
  
iii.	Category: 2543 Distinct records
  
          SELECT COUNT (DISTINCT (business_id)) FROM category;
  
iv.	Attribute: 1115 Distinct records
  
          SELECT COUNT (DISTINCT (business_id)) FROM attribute;
  
v.	Review: 8090 Distinct records
  
          SELECT COUNT (DISTINCT (business_id)) FROM review;
  
vi.	Checkin: 493 Distinct records
  
          SELECT COUNT (DISTINCT (business_id)) FROM checkin;
  
vii.	Photo: 6493 Distinct records
  
          SELECT COUNT (DISTINCT (business_id)) FROM photo;
  
viii.	Tip: 3979 Distinct records (business_id), 537 Distinct records (user_id)
  
          SELECT COUNT (DISTINCT (business_id)) FROM tip;
          SELECT COUNT (DISTINCT (user_id)) FROM tip;

ix.	User: 10000 Distinct records
  
          SELECT COUNT (DISTINCT (id)) FROM user;
  
x.	Friend: 11 Distinct records (user_id), 9415 Distinct records (friend_id)
  
          SELECT COUNT (DISTINCT (user_id)) FROM friend;
          SELECT COUNT (DISTINCT (friend_id)) FROM friend;
  
xi.	Elite_years: 2780 Distinct records
  
          SELECT COUNT (DISTINCT (user_id)) FROM elite_years;

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.

#### 3. Are there any columns with null values in the Users table? Indicate "yes," or "no."
Answer: No

                                              SELECT COUNT(*)
                                              FROM user
                                              WHERE id IS NULL
                                                OR name IS NULL
                                                OR review_count IS NULL
                                                OR yelping_since IS NULL
                                                OR useful IS NULL
                                                OR funny IS NULL
                                                OR cool IS NULL
                                                OR fans IS NULL
                                                OR average_stars IS NULL
                                                OR compliment_hot IS NULL
                                                OR compliment_more IS NULL
                                                OR compliment_profile IS NULL
                                                OR compliment_cute IS NULL
                                                OR compliment_list IS NULL
                                                OR compliment_note IS NULL
                                                OR compliment_plain IS NULL
                                                OR compliment_cool IS NULL
                                                OR compliment_funny IS NULL
                                                OR compliment_writer IS NULL
                                                OR compliment_photos IS NULL

#### 4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

i.	Table: Review, Column: Stars
  
              SELECT MIN(stars) FROM Review;
              SELECT MAX(stars) FROM Review;
              SELECT AVG(stars) FROM Review;
	
		min:1;		max: 5;		avg: 3.7082
		
	
ii.	Table: Business, Column: Stars
  
              SELECT MIN(stars) FROM Business;
              SELECT MAX(stars) FROM Business;
              SELECT AVG(stars) FROM Business;

		min: 1.0;		max: 5.0;		avg: 3.6549
		
	
iii.	Table: Tip, Column: Likes
  
              SELECT MIN(likes) FROM Tip;
              SELECT MAX(likes) FROM Tip;
              SELECT AVG(likes) FROM Tip;

		min: 0	;	max: 2	;	avg: 0.0144

iv.	Table: Checkin, Column: Count
  
              SELECT MIN(count) FROM Checkin;
              SELECT MAX(count) FROM Checkin;
              SELECT AVG(count) FROM Checkin;
	
		min: 1	;	max: 53	;	avg: 1.9414
		
	
v.	Table: User, Column: Review_count
  
              SELECT MIN(review_count) FROM User;
              SELECT MAX(review_count) FROM User;
              SELECT AVG(review_count) FROM User;
	
		min: 0	;	max: 2000	;	avg: 24.2995
		
#### 5. List the cities with the most reviews in descending order:
  
                SELECT
                    City,
                    SUM(review_count) AS Reviews
                FROM business
                GROUP BY city
                ORDER BY Reviews DESC;

#### 6. Find the distribution of star ratings to the business in the following cities:
  i. Avon

            SELECT
               City,
                 Stars,
                 SUM (review_count) AS ReviewCount
            FROM business
            WHERE City = "Avon"
            GROUP BY Stars;

ii. Beachwood

            SELECT
               City,
                 Stars,
                 SUM (review_count) AS ReviewCount
            FROM business
            WHERE City = "Beachwood"
            GROUP BY Stars;

#### 7. Find the top 3 users based on their total number of reviews:
		
              SELECT
                  id,
                  name,
                  review_count
              FROM user
              ORDER BY review_count DESC
              LIMIT 3;
  
#### 8. Does posing more reviews correlate with more fans?Please explain your findings and interpretation of the results:
There is a positive correlation relationship between review_count and number of fans
	
                    SELECT
                        name,
                        review_count,
                        fans,
                        yelping_since
                    FROM user
                    ORDER BY fans DESC;
  
| name      | review_count | fans | yelping_since       |
|-----------|--------------|------|---------------------|
| Amy       |          609 |  503 | 2007-07-19 00:00:00 |
| Mimi      |          968 |  497 | 2011-03-30 00:00:00 |
| Harald    |         1153 |  311 | 2012-11-27 00:00:00 |
| Gerald    |         2000 |  253 | 2012-12-16 00:00:00 |
| Christine |          930 |  173 | 2009-07-08 00:00:00 |
| Lisa      |          813 |  159 | 2009-10-05 00:00:00 |
| Cat       |          377 |  133 | 2009-02-05 00:00:00 |
| William   |         1215 |  126 | 2015-02-19 00:00:00 |
| Fran      |          862 |  124 | 2012-04-05 00:00:00 |
| Lissa     |          834 |  120 | 2007-08-14 00:00:00 |
| Mark      |          861 |  115 | 2009-05-31 00:00:00 |
| Tiffany   |          408 |  111 | 2008-10-28 00:00:00 |
| bernice   |          255 |  105 | 2007-08-29 00:00:00 |
| Roanna    |         1039 |  104 | 2006-03-28 00:00:00 |
| Angela    |          694 |  101 | 2010-10-01 00:00:00 |
| .Hon      |         1246 |  101 | 2006-07-19 00:00:00 |
| Ben       |          307 |   96 | 2007-03-10 00:00:00 |
| Linda     |          584 |   89 | 2005-08-07 00:00:00 |
| Christina |          842 |   85 | 2012-10-08 00:00:00 |
| Jessica   |          220 |   84 | 2009-01-12 00:00:00 |
| Greg      |          408 |   81 | 2008-02-16 00:00:00 |
| Nieves    |          178 |   80 | 2013-07-08 00:00:00 |
| Sui       |          754 |   78 | 2009-09-07 00:00:00 |
| Yuri      |         1339 |   76 | 2008-01-03 00:00:00 |
| Nicole    |          161 |   73 | 2009-04-30 00:00:00 |
(Output limit exceeded, 25 of 10000 total rows 

#### 9. Are there more reviews with the word "love" or with the word "hate" in them?
	Answer: There are more reviews with the word "love"

            SELECT								
                COUNT(text)
            FROM review
            WHERE text LIKE "%love%";

| COUNT(text) |
|-------------|
|        1780 |


            SELECT
                COUNT(text)
            FROM review
            WHERE text LIKE "%hate%";

| COUNT(text) |
|-------------|
|         232 |

#### 10. Find the top 10 users with the most fans:

            SELECT
                name,
                fans AS numoffans
            FROM user
            GROUP BY id
            ORDER BY fans DESC
            LIMIT 10;

## Part 2: Inferences and Analysis
#### 1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	
i.	Do the two groups you chose to analyze have a different distribution of hours?
  
The query returned just two businesses.
I observed that the business that runs for longer hours, opens at a later time.


ii.	Do the two groups you chose to analyze have a different number of reviews?

The query returned just two businesses.
I observed that the business that opens for longer hours has more views and a higher star rating.
  
Assumption: Because the business is open for longer, they cater to a higher number of customers than the other business in this category, leading to a higher opportunity for reviews by customers.

         
iii.	Are you able to infer anything from the location data provided between these two groups? Explain.

No, every business is in a different zip-code.
  
                          SELECT
                            business.name,
                            category.category,
                            business.address,
                            business.postal_code,
                            business.neighborhood,
                            business.is_open,
                            hours.hours,
                            business.review_count,

                            CASE 
                                WHEN business.stars BETWEEN 2 AND 3 THEN "2-3 Stars"
                                WHEN business.stars BETWEEN 4 AND 5 THEN "4-5 Stars"
                            ELSE "Others"
                            END AS StarRating

                        FROM business JOIN category
                            ON business.id = category.business_id
                            JOIN hours
                            ON business.id = hours.business_id

                        WHERE 
                            (business.city = "Phoenix" AND category.category ="Restaurants")
                            AND (StarRating = "2-3 Stars" OR StarRating = "4-5 Stars")
                        GROUP BY StarRating;

#### 2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i.	Difference 1:
Business that are open have a higher review_count. 
         
         
ii.	Difference 2:
Business that are open have a higher star rating. 
         
                                    SELECT 
                                        COUNT(id),
                                        AVG(review_count),
                                        SUM(review_count),
                                        AVG(stars),
                                        is_open
                                    FROM business
                                    GROUP BY is_open

#### 3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i.	Indicate the type of analysis you chose to do:
We want to understand the similarities between the businesses that have high star ratings
         
         
ii.	Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
We will need general information about the business such as location, business name, review_count, is_open etcetera.

These will allow to see the commonalities between businesses with high reviews. We will also include the category column so that businesses in the same categories can do an apples to apples comparison.
  
                              SELECT
                                  business.id,
                                  business.name,
                                  category.category,
                                  hours.hours,
                                  (business.address || ", " || business.city || ", " || business.state) AS Location,
                                  business.is_open,
                                  business.review_count,
                                  business.stars,
                                  attribute.name,
                                  attribute.value
                              FROM business JOIN hours
                              ON business.id = hours.business_id
                              JOIN attribute 
                              ON attribute.business_id = business.id
                              JOIN category 
                              ON category.business_id = business.id
                              WHERE business.stars BETWEEN 3.5 AND 5.0
                              GROUP BY business.name
                              ORDER BY business.stars DESC;
