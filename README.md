# IMDB DATA ANALYSIS
# INTRODUCTION
# ![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/15b286ec-7377-4288-8d92-d39709fe29af)
The Internet Movie Database (IMDb) is the largest, most comprehensive movie database on the web. It offers an extensive database of movie, TV show, and cast information. The site was officially launched in 1990 and is now owned by Amazon.com. IMDb is an extremely detailed and rich source of film data that features top movies, news, reviews, movie trailers, showtimes, DVD movie reviews, celebrity profiles, and more. If you’ve ever researched a movie or actor, you’ve probably landed on IMDb. The primary objective of this project was to analyze the data in order to gain insights into IMDB (Internet Movie Database) and provide suggestions for potential improvements, aiming for the growth and expansion of the platform. Through the analysis, we sought to uncover valuable information and propose actionable recommendations to enhance the overall performance and user experience of IMDB.
# PROBLEM STATEMENT
The IMDB dataset is a collection of 250movies in the IMDB database ranging between several years. It contains a wide range of information about movie name, year,rating,genre	certificate,	run_time,	tagline	budget,	box_office,	casts,directors, and writers of each movie. The dataset is designed to help analysts and researchers better understand the IMDB database and also make suggestion for improvement.

Data pervades every aspect of our lives, yet in its raw form, it is often inadequate for deriving valuable insights that effectively address business challenges. Therefore, when data is collected, it is crucial to undergo the process of data cleaning. By ensuring data cleanliness, productivity is enhanced, and the decision-making process benefits from the availability of high-quality information. In this project, I undertook a Data Cleaning Project using SQL to further develop my data manipulation skills.
In this project, my objective is to assist IBDM in gaining deeper insights into their database platform and maximizing growth opportunities. I will accomplish this by addressing the following business questions and providing comprehensive answers and recommendations:
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
rank,	name,	year,	rating,	genre	certificate	run_time	tagline	budget	box_office	casts	directors	writers
rank:	This is just a number column, its in serail therefore the data type chosen when creating the imdb table on Postgreql was #SERIAL
name:	This column comprises the name of each movie, therefore the data type chosen when creating the imdb table on Postgreql was #VARCHAR
year: This column comprises the year each movie was made, therefore the data type chosen when creating the imdb table on Postgreql was # INTEGER
rating: This column comprises the numerical values of the rating of each movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR
genre: This column comprises genre such as drama,crime, etc of each movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR
certificate: This column is what is popularly known as rating of each movie, such as R,PG-13,etc therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR
run_time: This column comprises the total time of each movie, this data was supposed to be "Time data type", but it wasnt possible, therefore I used # VARCHAR
tagline	budget: The budget pertains to the financial resources allocated for the overall production and release of the movie. This column was suppose to be INTEGER data type, but its had some non-integer datas in it that needed to be cleaned. Since I wanted to use SQL to do all data cleaning and not excel, I had to use VARCHAR as the data type to create the table.
box_office: Box office refers to the total amount of money generated from ticket sales for a particular movie or event. This column also was suppose to be INTEGER data type, but its had some non-integer datas in it that needed to be cleaned. Since I wanted to use SQL to do all data cleaning and not excel, I had to use VARCHAR as the data type to create the table.
casts: This column comprises all the cast of each movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR
directors: This column comprises directors, there were more than one director for some movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR
writers: This column comprises writers, there were more than one director for some movie, therefore the data type chosen when creating the imdb table on Postgreql was # VARCHAR
![image](https://github.com/MazeedahOloko/IMDB-/assets/128734036/ce9cc27c-e4d6-4495-8aa9-478b4e944d52)




