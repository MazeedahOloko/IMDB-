# IMDB DATA CLEANING

# INTRODUCTION


![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/8efe16c4-4299-4bb4-94c0-990a154e93c1)


The Internet Movie Database (IMDb) is the largest, most comprehensive movie database on the web. It offers an extensive database of movie, TV show, and cast information. The site was officially launched in 1990 and is now owned by Amazon.com. IMDb is an extremely detailed and rich source of film data that features top movies, news, reviews, movie trailers, showtimes, DVD movie reviews, celebrity profiles, and more. If you’ve ever researched a movie or actor, you’ve probably landed on IMDb. The primary objective of this project was to analyze the data in order to gain insights into IMDB (Internet Movie Database) and provide suggestions for potential improvements, aiming for the growth and expansion of the platform. Through the analysis, we sought to uncover valuable information and propose actionable recommendations to enhance the overall performance and user experience of IMDB.

# PROBLEM STATEMENT

The IMDB dataset is a collection of 250movies in the IMDB database ranging between several years. It contains a wide range of information about movie name, year,rating,genre,certificate,run_time,tagline,budget,box_office,casts,directors and writers of each movie. The dataset is designed to help analysts and researchers better understand the IMDB database and also make suggestion for improvement. I got the dataset from [Kaggle.com](https://www.kaggle.com/)

Data set: 
[IMDB Top 250 Movies.csv](https://github.com/MazeedahOloko/IMDB-/files/12443692/IMDB.Top.250.Movies.csv)

Data pervades every aspect of our lives, yet in its raw form, it is often inadequate for deriving valuable insights that effectively address business challenges. Therefore, when data is collected, it is crucial to undergo the process of data cleaning. By ensuring data cleanliness, productivity is enhanced, and the decision-making process benefits from the availability of high-quality information. In this project, I undertook a Data Cleaning Project using SQL to further develop my data manipulation skills.
In this project, my objective is to improve my data cleaning and also my SQL query applivation. I will accomplish this by addressing the following business questions and providing comprehensive answers and recommendations:
1. TO KNOW WHICH YEAR MOVIES WAS RELEASED
2. TO KNOW GENRE OF MOVIES RELEASED THE MOST
3. TOP 10 MOVIES WITH THE HIGHEST RATING AND THE YEAR
4. TOTAL NUMBER OF CERTIFICATE
5. TOTAL BUDGET PER MOVIES
6. TOTAL PROFIT FROM ALL MOVIES

I answered this questions by:
* Verifying for misspellings, duplicate entries and other errors. 
* Validating that the appropraite data type is assigned to each column.
* Eliminating irrelevant or redundant entries.
* The ultimate objective is to achieve clean and refined data that is suitable for in-depth analysis. This will enable us to derive precise and significant insights from the data, facilitating accurate decision-making and meaningful discoveries.

# Data Dictionary
rank,	name,	year,	rating,	genre	certificate	run_time	tagline	budget	box_office	casts	directors	writers.
1) rank:	This is just a number column, its in serail therefore the data type chosen when creating the imdb table on Postgreql was #SERIAL.
2) name:	This column comprises the name of each movie, therefore the data type chosen when creating the imdb table on Postgreql was #VARCHAR.
3) year: This column comprises the year each movie was made, therefore the data type chosen when creating the imdb table on Postgreql was # INTEGER.
4) rating: This column comprises the numerical values of the rating of each movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR.
5) genre: This column comprises genre such as drama,crime, etc of each movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR.
6) certificate: This column is what is popularly known as rating of each movie, such as R,PG-13,etc therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR.
7) run_time: This column comprises the total time of each movie, this data was supposed to be "Time data type", but it wasnt possible, therefore I used # VARCHAR.
8) tagline	budget: The budget pertains to the financial resources allocated for the overall production and release of the movie. This column was suppose to be INTEGER data type, but its had some non-integer datas in it that needed to be cleaned. Since I wanted to use SQL to do all data cleaning and not excel, I had to use VARCHAR as the data type to create the table.
9) box_office: Box office refers to the total amount of money generated from ticket sales for a particular movie or event. This column also was suppose to be INTEGER data type, but its had some non-integer datas in it that needed to be cleaned. Since I wanted to use SQL to do all data cleaning and not excel, I had to use VARCHAR as the data type to create the table.
10) casts: This column comprises all the cast of each movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR.
11) directors: This column comprises directors, there were more than one director for some movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR.
12) writers: This column comprises writers, there were more than one director for some movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR.
* SEE QUERY BELOW
  
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/b73347a7-2447-450f-ade6-95a9b326729b)

# DATA ANALYSIS

1) TO KNOW TOP 5 YEARS OF MAXIMUM MOVIE RELEASED
   
   This is and important analysis to know the trend of movie releases over the years and determine whether they have increased or decreased, we need to identify the top five years with the highest number of movie releases. This information will provide insights into the overall pattern and help us understand the factors that contribute to the fluctuation in movie releases. By examining the data, we can ascertain if there has been a significant increase or decrease in movie production and delve deeper into the reasons behind these trends.
* QUERY                                                      
```SQL SELECT COUNT(name) AS numberofmovies, year
       FROM imdb
       GROUP BY year
       ORDER BY numberofmovies DESC
       LIMIT 5; 
```
*VISUALS
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/9c244a81-3e58-4c9e-b26f-e073b38d408b)


2) TO KNOW GENRE OF MOVIES RELEASED THE MOST
   
   This analysis is important because I want to get an insight as to what genre(if there is) is released the most on IMDB movies. There was a lot of data cleaning here, I had to first split the genre column into three column to understand what to do, this is because the comma already joined all the genre as one and I wasnt liking the result of using this code:  
``` SELECT genre, COUNT(*) AS total_count
    FROM IMDB
    GROUP BY genre;
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/ca611876-0993-4437-8fc8-033169e5910b)


I wanted to be able to count all the Drama, crime, biography,,,,etc as one figure
* I firstly had to get rid of the comma and let each be in a column
``` SELECT 
        SPLIT_PART(genre, ',', 1) AS genre,
        SPLIT_PART(genre, ',', 2) AS genre,
        SPLIT_PART(genre, ',', 3) AS genre
    FROM imdb;
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/afd09bf8-a43d-4b44-9222-b0c1b0ee1929)

* But since I want to get the total of each genre I would need a way to join each column as one, so sql can count each genre. see below
```SELECT genre, 
   COUNT (*) AS totalcount
   FROM(
	     SELECT
             SPLIT_PART(genre, ',', '1') AS genre	
        FROM imdb
   UNION ALL 
         SELECT
             SPLIT_PART(genre, ',', '2') AS genre	
        FROM imdb
   UNION ALL
         SELECT
              SPLIT_PART(genre, ',', '3') AS genre	
         FROM imdb
     ) AS subquery
   WHERE TRIM(genre) <> ''
   GROUP BY genre
   ORDER BY totalcount DESC;
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/28647654-db60-4643-babd-f5cb29788de5)
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/986076b8-7fdf-4aa7-8b59-d224d9e94646)

NOTE: I had to include the WHERE TRIM(genre) <> '', BECAUSE I WAS GETTING RESULT OF A BLANK GENRE BUT WITH NUMBER
``` SELECT genre, 
    COUNT (*) AS totalcount
    FROM(
	SELECT
             SPLIT_PART(genre, ',', '1') AS genre	
        FROM imdb
     UNION ALL 
          SELECT
              SPLIT_PART(genre, ',', '2') AS genre	
          FROM imdb
     UNION ALL
	 SELECT
             SPLIT_PART(genre, ',', '3') AS genre	
         FROM imdb
      ) AS subquery
   GROUP BY genre
   ORDER BY totalcount DESC
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/9d5b1511-edeb-4999-9da2-8c3781dc4a5e)

3) TOP 10 MOVIES WITH THE HIGHEST RATING AND THE YEAR
``` SELECT name, rating, year
    FROM imdb
    ORDER BY rating DESC
    LIMIT 10;
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/18142d04-7e2a-45a9-8f94-bb6726eb398c)


4) TOTAL NUMBER OF CERTIFICATE
   
```SELECT certificate, COUNT(*) AS total_count
   FROM IMDB
   GROUP BY certificate
   ORDER BY total_count DESC;
```
   ![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/6e1c4160-2363-4877-90a2-66fd6229cb69)


5) TOTAL BUDGET PER MOVIE
   
    I did a lot of data cleaning to get this figure to.
   *Firstly I had TO CHECK IF THERE ARE OTHER CHARACTERS IN MY BUDGET FIGURE
```SELECT budget
  FROM imdb
  WHERE budget <> '' AND TRIM(budget) <> '' AND budget ~ '\D';
```

![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/205f06f4-1611-49a0-94d1-cf86f3ea46ad)


* Query to clean data and get the TOTAL budget for ALL movies
```SELECT SUM(
	    CASE
                 WHEN budget LIKE '$%' THEN CAST(REPLACE(budget, '$', '') AS NUMERIC)
                 WHEN budget LIKE 'RF %' THEN CAST(REPLACE(budget, 'RF ', '') AS NUMERIC)
		 WHEN budget = 'Not Availble' THEN NULL 
		 WHEN budget ~ '^[0-9.]+$' THEN CAST(budget AS NUMERIC)
                 ELSE NULL
		 END) AS Total_budget
FROM imdb;
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/22119b55-46f6-4c57-b62f-401cec77c4d5)


* To Compare BUDGET with RATINGS
```SELECT SUM(
	    CASE
                 WHEN budget LIKE '$%' THEN CAST(REPLACE(budget, '$', '') AS NUMERIC)
                 WHEN budget LIKE 'RF %' THEN CAST(REPLACE(budget, 'RF ', '') AS NUMERIC)
		 WHEN budget = 'Not Availble' THEN NULL 
		 WHEN budget ~ '^[0-9.]+$' THEN CAST(budget AS NUMERIC)
         ELSE NULL
		 END) AS calculated_budget , rating
FROM imdb
GROUP BY rating
ORDER BY calculated_budget DESC;
```


6) TOTAL BOX OFFICE PER MOVIE
   
   This analysis is important because BOX OFFICE means the total sales from tickets of movies. Since I already know the budget for each movie, I need this analysis to compare budget to sales(profit), which would be the next analysis after this.
   * Firstly did a query to see if there are blanks, blanks before a digit and if there are non digit characters in the box_office column for data cleaning.
```SELECT box_office
   FROM imdb
   WHERE box_office <> '' AND TRIM(box_office)<> '' AND box_office ~ '\D';
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/d6a8b034-41b7-47d5-89b8-4012f4030e32)

    *Query to clean the data 
```SELECT SUM(
         CASE 
             WHEN box_office = 'Not Available' THEN NULL 
	     WHEN box_office LIKE '$%' THEN CAST(REPLACE(box_office, '$', '') AS NUMERIC)
	     WHEN box_office Like '%(estimated)' THEN CAST(REPLACE(box_office, '(estimated)', '') AS NUMERIC)
	     WHEN box_office ~ '^[0-9.]+$' THEN CAST(box_office AS NUMERIC)
           ELSE NULL
	   END) AS TOTALbox_office 
FROM imdb;
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/7bf58490-f45e-46a0-bd45-f16dd6a2df38)



8) TOTAL BOX_OFFICE WITH RATING
```SELECT SUM(
             CASE 
                WHEN box_office = 'Not Available' THEN NULL 
	        WHEN box_office LIKE '$%' THEN CAST(REPLACE(box_office, '$', '') AS NUMERIC)
	        WHEN box_office Like '%(estimated)' THEN CAST(REPLACE(box_office, '(estimated)', '') AS NUMERIC)
	        WHEN box_office ~ '^[0-9.]+$' THEN CAST(box_office AS NUMERIC)
	        ELSE NULL
	        END) AS TOTALbox_office, rating
   FROM imdb
   GROUP BY rating
   ORDER by rating DESC;
```

7) PROFIT

   ![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/34d8d9db-98be-4c6c-9eda-a356c450a81c)

*Check Profit compared with rating
```SELECT SUM(
	    CASE
        WHEN budget LIKE '$%' THEN CAST(REPLACE(budget, '$', '') AS NUMERIC)
         WHEN budget LIKE 'RF %' THEN CAST(REPLACE(budget, 'RF ', '') AS NUMERIC)
		 WHEN budget = 'Not Availble' THEN NULL 
		 WHEN budget ~ '^[0-9.]+$' THEN CAST(budget AS NUMERIC)
         ELSE NULL
		 END) AS TOTAL_budget ,
      SUM(
             CASE 
                WHEN box_office = 'Not Available' THEN NULL 
	        WHEN box_office LIKE '$%' THEN CAST(REPLACE(box_office, '$', '') AS NUMERIC)
	        WHEN box_office Like '%(estimated)' THEN CAST(REPLACE(box_office, '(estimated)', '') AS NUMERIC)
	        WHEN box_office ~ '^[0-9.]+$' THEN CAST(box_office AS NUMERIC)
	        ELSE NULL
	        END) AS TOTALbox_office,
		SUM(
             CASE 
                WHEN box_office = 'Not Available' THEN NULL 
	        WHEN box_office LIKE '$%' THEN CAST(REPLACE(box_office, '$', '') AS NUMERIC)
	        WHEN box_office Like '%(estimated)' THEN CAST(REPLACE(box_office, '(estimated)', '') AS NUMERIC)
	        WHEN box_office ~ '^[0-9.]+$' THEN CAST(box_office AS NUMERIC)
	        ELSE NULL
	        END)  - SUM(
	    CASE
        WHEN budget LIKE '$%' THEN CAST(REPLACE(budget, '$', '') AS NUMERIC)
         WHEN budget LIKE 'RF %' THEN CAST(REPLACE(budget, 'RF ', '') AS NUMERIC)
		 WHEN budget = 'Not Availble' THEN NULL 
		 WHEN budget ~ '^[0-9.]+$' THEN CAST(budget AS NUMERIC)
         ELSE NULL
		 END) AS profit,
		rating
FROM imdb
GROUP BY rating
ORDER BY profit DESC;
```
# CONCLUSION
This was a very tough data to clean for me, as it was my first. But it helped me improved my data cleaning as well as my SQL query knowledge.




