# DATA512 - Homework 2: Considering Bias in Data
## Coverage and Quality Analysis of US Cities in Wikipedia Articles

The aim of this assignment is to explore the concept of bias in data using Wikipedia articles. The articles considered for this study are about cities in different US states. For this assignment, a dataset of Wikipedia articles was combined with a dataset of state populations, and a machine learning service called ORES was used to estimate the quality of the articles about the cities. An analysis was then conducted on how the coverage of US cities on Wikipedia and how the quality of articles about cities varies among states.

The source datasets for this analysis were as follows:
1. The Wikipedia ['Category:Lists of cities in the United States by state'](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state) which was crawled to generate a list of Wikipedia article pages about US cities from each state. This data can be found in [us_cities_by_state_SEPT.2023.csv](https://drive.google.com/file/d/1khouDmMaZyKo0y5WkFj4lu7g8o35x_98/view?usp=sharing).
2. The US Census Bureau which provides updated population estimates for every US state. The data can be found on ['State Population Totals and Components of Change: 2020-2022'](https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html) from their website. An Excel file linked to that page contains estimated populations of all US states for 2022. 
3. Finally, the 'region' demarcation within the US to agglomerate states into defined regions. For this analysis, the regional and divisional agglomerations as defined by the US Census Bureau were used. The data for the same can be found in ['US States by Region - US Census Bureau'](https://docs.google.com/spreadsheets/d/14Sjfd_u_7N9SSyQ7bmxfebF_2XpR8QamvmNntKDIQB0/edit?usp=sharing).

Two APIs were used in the first part of the study. The data acquisition step involved accessing page info data using the [MediaWiki REST API for the EN Wikipedia](https://www.mediawiki.org/wiki/API:Main_page). The API documentation, [API:Info](https://www.mediawiki.org/wiki/API:Info), covers additional details that may be helpful when trying to use or understand this example. For the next part, the quality scores had to be predicted for each article in the Wikipedia dataset using [ORES (Objective Revision Evaluation Service)](https://www.mediawiki.org/wiki/ORES). ORES requires a specific revision ID of a specific article to be able to make a label prediction. For more information, the [ORES API documentation](https://ores.wikimedia.org/) can be accessed from the main ORES page.

In this study, two intermediate data files and one final output file were saved in the repository. The first intermediate file was generated at the end of the first API request - the page information request. The output was a dictionary with the article_title as the key and the revision_id as value saved as a JSON file. The article_title was a string whereas the revision_id was an integer. The second intermediate file was created to save the output after the second API request - ORES request. The output was saved as a CSV file with two columns - article_title (string) and the article_quality (string).

The final output file for the analysis was a merged dataframe created by merging the three datasets discussed earlier. The file was saved as a CSV file with six columns - state, regional_division, population, article_title, revision_id and article_quality. Apart from population and revision_id which were integers, the rest four columns were string values.

This final output file was used to calculate total-articles-per-population (a ratio representing the number of articles per person) and high-quality-articles-per-population (a ratio representing the number of high quality articles per person) on a state-by-state and divisional basis. This was then used to construct six following tables:
1. Top 10 US states by coverage: The 10 US states with the highest total articles per capita (in descending order) .
2. Bottom 10 US states by coverage: The 10 US states with the lowest total articles per capita (in ascending order) .
3. Top 10 US states by high quality: The 10 US states with the highest high quality articles per capita (in descending order) .
4. Bottom 10 US states by high quality: The 10 US states with the lowest high quality articles per capita (in ascending order).
5. Census divisions by total coverage: A rank ordered list of US census divisions (in descending order) by total articles per capita.
6. Census divisions by high quality coverage: Rank ordered list of US census divisions (in descending order) by high quality articles per capita.

There are quite a few considerations about the data - both source and the output files. While the source data had a lot of preprocessing to do, the output files had some interesting thing to consider. Both these aspects have been covered in detail in the 'Coverage_And_Quality_Analysis' notebook of the repository.

### Research Implications:

This study exposed me to working with APIs and performing relevant preprocessing techniques to ensure data consistency. This study also helped me understand to explore the concept of bias and how bias creeps in through several factors. One would expect Wikipedia to be moderately reliable but I was surprised to find out that the articles' data was missing completely for two whole states. Another interesting fact I noticed was that some of the less-populated states had a higher coverage and quality of articles per capita. I expected California to have a higher quality of articles and higher coverage as it is a big and major state. However, it was in the bottom ten for both coverage and high quality articles per capita. I later realised that it could probably be attributed to the extremely high population numbers which thereby reduces the per-capita value. Some other questions I would like to address as a part of my reflection are:

1. What biases did you expect to find in the data (before you started working with it), and why?
   * Coverage Bias: Wikipedia articles may not cover all US cities equally. Larger, more well-known cities are more likely to have articles, while smaller or less prominent cities may be underrepresented.
   * Quality Bias: Articles about US cities may vary in quality. Major cities are more likely to have well-maintained and higher quality articles, while smaller cities may have less informative or lower quality articles.

2. What (potential) sources of bias did you discover in the course of your data processing and analysis?
   * Population Bias: The coverage of US cities on Wikipedia may not align with their population sizes. Some states with small populations may have a high number of articles about cities, while states with large populations may be underrepresented.
   * Regional Bias: The regional division definitions used by the US Census Bureau may introduce regional biases in the analysis. These definitions are subject to various factors and thus, this might not accurately represent regional divisions from other perspectives.

3. What might your results suggest about (English) Wikipedia as a data source?
   * As discussed earlier, the results suggest that Wikipedia may not be a uniform or unbiased source of information. Both coverage and quality of content can vary significantly across different states and regions. This has implications for understanding how knowledge is represented and accessed online, with potentially less information about certain cities and regions.
   * Thus, additional efforts are needed to ensure a more comprehensive and equitable representation of US cities on Wikipedia.
