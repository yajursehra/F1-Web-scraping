
Formula one web scraping

Executive Summary

This project is a comprehensive analysis of Formula 1 championship race results, using web
scraping techniques like BeautifulSoup, Selenium to gather historical data of races and SQL for
data management. Our objective is to create a dataset to use in strategic decision-making and
to derive insights into the performance trends of drivers over the last 10 years.

Background
The sport of Formula 1 racing is a very popular global racing championship event which is a
high-stakes environment as teams compete with each other with high technology top end
engine cars and in this sport, data analysis provides an added competitive advantage. By
analyzing driver standings/positions, racing teams can develop strategies, track performance,
and improve their future preparations.
Context and Domain Knowledge
In the context of this project, the scraped data will be useful for businesses in the sports
analytics industry, providing insights to constructor teams and drivers about consistency, team
performance, and historical trends. It requires basic domain knowledge about the sport to
understand the dataset and what to scrape and what to use for analysis.
Introduction of the Data Sources
Our data source is the ESPN website “https://www.espn.com/” which is a platform to check stats
/ scores and watch live matches for mostly all sports. This is a legitimate source as it also
matches with the official formula 1 website. The reason to choose this over the official F-1
website was because it had multiple sports to choose from and the script can be modified a little
bit if in future we want to use it for other sports.
2

Description of the Web-Scraping Routine(s)
STEP 1 :
Importing necessary libraries and setting directory path.
STEP 2 :
Setting up the automatic browsing through selenium, first we go to espn website, then we click
inspect and find the search button on the right side
3
Then using selenium we click on that button by driver.find_element using CSS_SELECTOR
Then we fill“Formula One” into the search bar and click enter, then the screen as shown in the
screenshot gives a tab to click which takes us to the formula one page which contains all the
information about races, news, results, historical data etc. In this we navigate to the standings
page, after clicking on the standings page using driver.find_element(By.LINK_TEXT, 'Standings')
which clicks on the link called ‘Standing’ and takes us to that URL.
4
We then setup a loop to find the data for the last 11 years, we limited it to last 11 years only to
showcase the lessons learned in the class, but for using it for data analysis, we can take all the
historical data which is available on the website, from 1950 to 2023 and current standings of
2024 as well. We first fetch the current URL and then add the year ahead of it.
year_url = f'{current_url}/_/season/{year}'
This runs for 11 year and gives an output which is shown below for an example of the year
2023.
5
STEP 3 :
In the same loop as above, we then save the HTML of all the years locally into our computer,
this way we have all the web pages for 11 years as a collection of all the past results.
6
STEP 4:
Once we had our data stored, we wanted to fetch the necessary information out of it and store it
in SQL database, so that it can be easily used for analysis purposes by writing queries, also it
can be connected to tableau for some visualizations. So we created three functions mainly,
1) create_database - This function creates a new database (f1_data)
2) create_table - This function creates a new table (standings)
3) Insert_user_data - This function inserts all the fetched information into the tables we
created.
Then after creating these functions, we established a connection with our SQL server by
providing the credentials so that we can call the function and it directly reflects in our workbench
that the database and table has been created. We will insert the data later after fetching.
STEP 5 :
We parsed the HTML saved files to get the necessary information out of it using BeautifulSoup,
to read through those files. We only took the top 10 drivers of each year with maximum points
by the end of the year, but the entire data can be used for more analysis, but only the top 10 get
points in a race so it made sense to fetch that and use that to build strategies. We then ran a
loop to get all the information from all the saved HTML files.
STEP 6:
In the last step, we beautified the data in the way we wanted, we used REGEX to fetch the year
from the file-name, also the data that we got from the table was cluttered so we formatted that
within the same loop as above so that we can store the data into the SQL database, we fetched
4 columns
Year (INT), Position(INT), DriverName (VARCHAR) and Points (INT)
7
Then we called the function to input the entire data into the database and commit the changes
followed by closing the DB connection. Following was the output which showed the success of
Data Insertion.
Database Design Choices and Business Relevance
We created a database in MYSQL Workbench, The data was less in size, else we could have
opted for MongoDB which helps in fast retrieval of data. We created a simple table of 4 columns
with 3 INT type columns and 1 VARCHAR to store the name of the drivers. MYSQL is reliable
and scalable as well as the structure of the table is robust and need not be changed frequently.
The SQL database offers transactional integrity, complex query support, and the relational
model aligns with the structured nature of the data.
The dataset allows for trend analysis and performance prediction, critical for business
stakeholders such as sponsors and teams. We can make a race winner prediction model by
scraping additional information through the same method and using that to build some ML
models, we can also use it for trend analysis using tableau or python. This information is also

very useful for drivers to track their performance and improve accordingly which will make the
sport more interesting for us fans.
Following is a snapshot of MYSQL Workbench with a small query executed to show how the
data looked after inserting in the database.
Summary and Conclusions
The project successfully shows the various learnings we gained in class like the application of
web scraping techniques such as the use of Selenium to navigate websites, BeautifulSoup to
parse HTMLs, saving web pages as HTMLs, storing data in SQL database and Regex to
beautify data. The collected dataset not only depicts historical analysis or trend analysis but also
sets a foundation for predictive modeling which we learned in the ML class, which can further be
leveraged for business decision-making processes in the fast and ever upgrading world of
Formula 1 racing.
9
