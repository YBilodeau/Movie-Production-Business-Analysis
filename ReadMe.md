![image](https://github.com/YBilodeau/Movie-Production-Business-Analysis/blob/main/Images/movie%20theatre%20banner.png)
# **Movie Production Business Analysis**
- Yvon Bilodeau
- May 2022

## **Overview**
A fictional person is the head of a new movie studio. They are new to the industry, and have asked for recommendations to help them make successful movies.

## **Business Problem**
For this project, I have been requested to extract information from the **IMDB (Internet Movie Database)** and **TMDB (The Movie Database)** in order to analyze what makes a movie successful.

## **Phase 1 - IMDB ETL**
### **Objective**
For Phase 1 of the project, the stakeholder has requested an extraction of files from the **IMDB (Internet Movie Database)**, and the creation of a repository to contain them.

### **Specifications**
The **IMDB** Provides several files with varied information for Movies, TV Shows, Made for TV Movies, etc.
- [Overview/Data Dictionary](https://www.imdb.com/interfaces/)
- [Downloads page](https://datasets.imdbws.com/)

**Extraction**  - 
From their previous research, they realized they would like to focus on the following files:
- title.basics.tsv.gz
- title.ratings.tsv.gz
- title.akas.tsv.gz

**Transformation/Filtering**  - 
The stakeholder would only like information included for movies based on the following specifications:

- Exclude any movie with missing values for genre or runtime
- Include only full-length movies (titleType = "movie").
- Include only fictional movies (not from documentary genre)
- Include only movies that were released 2000 - 2021 (include 2000 and 2021)
- Include only movies that were released in the United States

### **Deliverables**
- Movie-Production-Business-Analysis repository
- title_basics.csv.gz
- title_akas.csv.gz
- title_ratings.csv.gz

## **Phase 2 - TMDB ETL**
### **Objective**
For Phase 2 of the project, the stakeholder realized that there is no financial information included in the **IMDB (Internet Movie Database)** data, e.g. budget or revenue.This will necessary in attempting to analyze which movies are successful.

**The Movie Database (TMDB)** however, is a great source of financial data. 

### **Specifications**
Fortunately, **[The Movie Database (TMDB)](https://www.themoviedb.org/)** offers a free API for programmatic access to their data. 

**1. API Data Extraction**
- The stakeholder has requested an extraction of the budget, revenue, and MPAA Ratings (G/PG/PG-13/R), also called "Certification".
- The stakeholder has requested the results be extracted and saved for movies that meet all of the criteria established in Phase 1 of the project.
- As a proof-of-concept, they requested a test extraction of movies that started in 2000 or 2001, both years to be saved as both separate and a combined.csv.gz files.

**2. Exploratory Data Analysis**
- Once the data has been extracted from the API, they would like some initial exploratory questions be answered:
   - How many movies had at least some valid financial information? 
   - How many movies are there in each of the certification categories (G/PG/PG-13/R)?
   - What is the average revenue per certification category?
   - What is the average budget per certification category?

### **Deliverables**
- final_tmdb_data_2000.csv.gz
- final_tmdb_data_2001.csv.gz
- tmdb_results_combined.csv.gz

## **Phase 3 - MySQL Movie Database ETL**
### **Objective**
The stakeholder has requested that the data that has been extracted and transformed in Phases 1 & 2 of the project, be utilized to create a MySQL database.

### **Specifications**
The tables should be normalized as well as possible prior to adding them to the new database.
- Note: an important exception to their request is that they would like you to keep all of the data from the TMDB API in 1 table together (even though it will not be perfectly normalized).  
- Only imdb_id, revenue, budget, and certification columns need to be kept.

### **Deliverables**
SQL "Movies" database with the following tables:
- title_basics
- title_ratings
- title_genres
- genres
- tmdb_data

## **Phase 4 - TMDB ETL**
### **Objective**
- In Phase 2, as a proof-of-concept, the stakeholder requested a test extraction of movies that started in 2000 or 2001. Each year to be saved as a separate .csv.gz file.
- In Phase 4, the stakeholder has requested additional years to be extracted, and years 2000-2021 are to be combined into a single TMDB .csv.gz file.

### **Deliverables**
- final_tmdb_data_2002.csv.gz
- ...
- final_tmdb_data_2021.csv.gz
- tmdb_results_combined_final_df.csv.gz

## **Phase 4 - Hypothesis Testing**
### **Objective**
For Phase 4 of the project, the stakeholder has also requested statistical tests to obtain mathematically-supported answers to their questions:

- Does the MPAA rating of a movie affect how much revenue the movie generates?
- Does the genre of a movie affect how much revenue a movie generates?
- Do movies that are over 2.5 hours have a significantly different revenue than movies that under 1.5 hours in length?

### **Specifications**
For each question:

- They would like to know if a statistically significant difference exists for each hypothesis.
- They would like to know the p-value of the test.
- They would like a visualization that supports the findings of the test.

### **Questions**
#### **Does the MPAA rating of a movie affect how much revenue the movie generates?**
- The p-value for the test was 5.504858804917085e-168
- It was < the alpha value of 0.05, so
- A statistical significance exists. The null hypothesis is rejected and the alternative is supported that..
- **The MPAA rating of a movie does affect how much revenue the movie generates.**

![image](https://github.com/YBilodeau/Movie-Production-Business-Analysis/blob/main/Images/certification%20vs%20revenue.png)


#### **Does the genre of a movie affect how much revenue a movie generates?**
- The p-value for the test was 1.760985049928353e-249
- It was < the alpha value of 0.05, so
- A statistical significance exists. The null hypothesis is rejected and the alternative is supported that..
- **The genre of a movie does affect how much revenue a movie generates.**

![image](https://github.com/YBilodeau/Movie-Production-Business-Analysis/blob/main/Images/genre%20vs%20revenue.png)

#### **Do movies that are over 2.5 hours have a significantly different revenue than movies that under 1.5 hours in length?**
- The p-value for the test was 2.428023688468123e-11
- It was < the alpha value of 0.05, so
- A statistical significance exists. The null hypothesis is rejected and the alternative is supported that..
- **Movies that are over 2.5 hours have a significantly different revenue than movies that under 1.5 hours in length.**

![image](https://github.com/YBilodeau/Movie-Production-Business-Analysis/blob/main/Images/runtime%20vs%20revenue.png)
