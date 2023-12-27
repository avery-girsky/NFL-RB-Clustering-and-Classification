# NFL RUNNING BACK CLUSTERING AND CLASSIFICATION

## Description:

As I prepare for another year of fantasy football in 2023, I sit at the end of the first round and realize that Derrick Henry often slips to the back of the first round and early second round in drafts. For the past three years, the fantasy community talked about his heavy workload and the impending cliff that he _must_ fall off of, but year after year he kept producing. Each year I listened and avoided drafting him in the top end of the first round, only to be proven wrong. This year finally I decided to put him onto my radar as his draft value had dropped, but I wanted to know if there was a historical precedent for long sustained production.

Simultaneously, I am starting my Master's in Analytics at Georgia Tech and learning about many different data science techniques. I believed it would be interesting to see if data consisting of the year over year fantasy points of every listed running back in NFL history could be clustered. I also wanted to determine if those groups would contain players whose reputations fit their cluster, if I could visualize the clusters, and if I could use the assigned classes to predict career trajectories of current NFL RBs (and get a leg up in my fantasy draft).

I broke this process into three significant steps: _data collection_, _clustering_, and _classification_.


## Data Collection:

As an undergrad, I spent a significant amount of time web scraping in python for my research lab, so I knew if I could find running back data online then I could collect it. I easily put running backs into the search bar of [Pro Football Reference](https://www.pro-football-reference.com) and received a link of every running back in history with links to their stat pages. The overall web scraping process became to loop through the list of every running back and record their name, then navigate to their individual PFR page and add up their fantasy points in every season they played using ESPN PPR format. With web scraping, though, it's never that easy. Here is a list of issues I ran into, and their subsequent solutions.

+ _Players do not all play the same number of seasons:_ The most seasons played by a running back was 16, so any running back short of that total padded their extra seasons with NaN values, which were later converted to 0.0.
+ _Players are traded/move teams midseason:_ PFR records the season long stats in this case, followed by a row with stats for each team individually. I captured the "team name" column which reads "2TM" when a player played for 2 teams that season. By isolating the first character and converting to a number, we can then skip the next n rows of the PFR page, leaving behind only season long stats.
+ _Both current and former players are listed:_ I wanted my dataset for clustering to contain only retired players as well as collect current players separately. I was able to capture data on whether or not the player name is bolded (boldface indicating that they are active) and then collect the two datasets separately.
+ _PFR will reject a computer from scraping their website:_ Perhaps the most tedious issue I faced was that PFR would throw an error if receiving too many requests in a short time (fairly to preserve their website infrastructure). The solution was to use the time library in python and use time.sleep to put a delay between requests as well as rerunning the code every 150 players to ensure the data was saved in case of a code crash.
+ _Different players have their rushing stats in different orders and places:_ Originally I used the position of rushing and receiving stats on the website to capture stats, but players listed as WR/RB would have stats in different orders and different locations on the page. I instead pivoted to using an identifier for each stat present in the HTML of the website.

After dealing with these issues, I recorded the past player data in the file RBData.csv and the current player data in Current_RBData.csv.


## Clustering:

## Classification:
