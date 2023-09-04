# IMDB DATA ANALYSIS

# INTRODUCTION

![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/8efe16c4-4299-4bb4-94c0-990a154e93c1)

The Internet Movie Database (IMDb) is the largest, most comprehensive movie database on the web. It offers an extensive database of movie, TV show, and cast information. The site was officially launched in 1990 and is now owned by Amazon.com. IMDb is an extremely detailed and rich source of film data that features top movies, news, reviews, movie trailers, showtimes, DVD movie reviews, celebrity profiles, and more. If you’ve ever researched a movie or actor, you’ve probably landed on IMDb. The primary objective of this project is to execute meticulous data cleansing processes aimed at achieving optimal data quality.
Data pervades every aspect of our lives, yet in its raw form, it is often inadequate for deriving valuable insights that effectively address business challenges. Therefore, when data is collected, it is crucial to undergo the process of data cleaning. By ensuring data cleanliness, productivity is enhanced, and it also enhance the decision-making process. The dataset which forms the foundation of this project was sourced from [Kaggle.com](https://www.kaggle.com/), a prominent platform for data science and machine learning enthusiasts. Kaggle is renowned for providing a hub where datasets, competitions, and valuable insights converge, providing the raw material from which we initiate comprehensive data cleansing processes. 
* Data set: 
[IMDB Top 250 Movies.csv](https://github.com/MazeedahOloko/IMDB-/files/12443692/IMDB.Top.250.Movies.csv)

In this project, I undertook a Data Cleaning Project using SQL to further develop my data manipulation skills. I acheived this data cleaning by:
* Verifying for misspellings, duplicate entries and other errors. 
* Validating that the appropraite data type is assigned to each column.
* Eliminating irrelevant or redundant entries.
* The ultimate objective is to achieve clean and refined data that is suitable for in-depth analysis. This will enable us to derive precise and significant insights from the data, facilitating accurate decision-making and meaningful discoveries.

# Data Dictionary
See text file for Data dictionary [IMDB DATA DICTIONARY.txt](https://github.com/MazeedahOloko/IMDB-DATA-ANALYSIS/files/12476279/IMDB.DATA.DICTIONARY.txt)

* SEE QUERY BELOW
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/b73347a7-2447-450f-ade6-95a9b326729b)

# DATA CLEANING

# 1) Genre column
   The purpose of doing data cleaning in the genre column was because of the comma between each genre in each row, i.e a movie can be categorize into having different genre, I wanted to be able to split it in such a way that all the genre aren't in one column. There was a lot of data cleaning here, I had to first split the genre column into three column to understand what to do, this is because the comma already joined all the genre as one and I wasnt pleased with the result of using this code:  
``` SELECT genre, COUNT(*) AS total_count
    FROM IMDB
    GROUP BY genre;
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/ca611876-0993-4437-8fc8-033169e5910b)


* I wanted to be able to count all the Drama, crime, biography,,,,etc as one figure
  I firstly had to get rid of the comma and let each be in a column
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


* NOTE: I had to include the WHERE TRIM(genre) <> '', BECAUSE I WAS GETTING RESULT OF A BLANK GENRE BUT WITH NUMBER
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



# 2) Budget Column
   
   The purpose of doing data cleaning in the budget column was because of the presence of non-numeric characters such as symbols, what this means is that I would be unable to perform any mathematical calculation on budget as the DATA type isnt numeric. I invested significant effort in refining this figure through a series of data cleaning steps.
   * To begin, I meticulously examined the budget figures to identify and address any instances of non-numeric characters.
     
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



# 3) Box Office column
Box office means the total sales from tickets of movies. The purpose of doing data cleaning in the box office column is same as the budget column above, the presence of symbols would make analysis impossible for accurate calculation purposes.
    
   * I did a query to see if there are empty cells( NULL), blanks before a digit and if there are non digit characters in the box_office column for data cleaning.
     
```SELECT box_office
   FROM imdb
   WHERE box_office <> '' AND TRIM(box_office)<> '' AND box_office ~ '\D';
```
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/d6a8b034-41b7-47d5-89b8-4012f4030e32)

    * Query to clean the data:
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




# CONCLUSION
In conclusion,  dealing with this dataset was quite a challenge, especially since it was my first time handling data cleaning. Data cleaning is super important to make sure the dataset is good to go. It's like laying down a strong foundation for later analysis. For example, fixing up the profit numbers was a must. If we didn't clean the data, trying to add up profits would be a mess as a result of the presence of symbols which wouldnt be included in our summation.
However, I can confidently state that the process significantly enhanced both my data cleansing skills and my proficiency in crafting effective SQL queries. This experience has undoubtedly contributed to my growth in handling complex data tasks. This project will serve as a valuable learning experience, equipping me with the practical knowledge needed to enhance data quality and derive meaningful insights through effective data preparation. 

![image](https://github.com/MazeedahOloko/IMDB-DATA-ANALYSIS/assets/128734036/e37e031f-902b-4a60-8888-3c98ca6b96cb)



