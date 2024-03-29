![MLB](https://res-3.cloudinary.com/crunchbase-production/image/upload/c_lpad,h_256,w_256,f_auto,q_auto:eco/v1429885658/axit3z8523ss6malonjg.png)

# mlb_ETL
ETL Project using Fangraphs starting rosters and USA Today Salary numbers

## Data Sources
We used two data sources for this project. The first was [USA Today](https://www.usatoday.com/sports/mlb/salaries/) to pull a table of the salaries of all active MLB players for the 2019 season.

The second was [FanGraphs](https://www.fangraphs.com/teams/{}/depth-chart), where we pulled the most likely starting lineups for each team.

## Extracting
We scraped both of our data sources off of the above websites. For the salary data we used Pandas and the `pd.read_html` function to grab the table we wanted.

The lineups were a little more involoved. Because each team's lineup was stored on a separate webpage we needed to create a for loop that would loop through each team's webpage and scrape the lineup. 

The first loop we created took the base url and looped through a list of team names to create a list of unique urls for each team.

Once we had that we were able to loop through each url and use beautiful soup to extract the starting lineups for each team.

## Transforming
Our transformation look place at a few different stages of the project. Luckily the salary table was pretty clean and didn't require much modification.

The lineup tab on the other hand need a bit more work. During the looping/scraping we needed to add the team names and positions to to each roster. Luckily the positions were the in the same order each time so we were able to to add a new column during each loop with the positions for each team.

To empty a ton of stored null values the main database of all the players was split into position players and pitchers. This got rid of a ton of null values and all the data is still there.


## Loading
The dataframe was loaded into postgres using the pandas function to_spl. This is by far the most convient function when working in a python environment and wanting to upload into a relational database.
### All Players
![all players](images/database.JPG)
### Pitchers
![pitchers](images/pitchers.JPG)
### Fielders
![fielders](images/fielders.JPG)

