# capstone
Capstone Project for DA14

# Intro

For this project - I wanted to take a look at Hockey Stats over the past 10 years and see if I could find any statistics in the regular season that could help predict an outcome of who made it the Stanley Cup. 

To note - The 2020 season was stopped abruptly and had an abridged playoffs later that many do not look at because of the sudden stop. In addition - I did not include the 2021 season because it was a half of a season and it was all done in a "bubble". 

All calculations done in Excel and Tableau was used to visualize.

I will break down the metrics that I wanted to look at below:

# Game Plan
1 - Take a look at Pre-season betting odds and how the teams faird
2 - Take a look at GA and GF and its relation to the finalists
3 - Take a look at Powerplay kill and pp to see if that is an X factor to get into the Finals. 
4 - Take a look at Hot streak heading into the play offs to see if that matters. 
5 - A fun look into the President's Trophy curse. How bad is it really? 

# Pre-season Betting odds and how did they fair

Thanks to nhlreference.com I was able to have the preseason betting odds of each season and I can compare that to the finals of each season. 
I started by getting each season in it's own tab in excel. The columns were Team, Stanley Cup Odds, Pts. O/U, Final Pts. I also have the final ranking ("Rk") and Team in two seperate columns that we will reference below.
I wanted a new column that gave me each team's final standing in the plaoffs with the formula "=XLOOKUP(A2,$H$2:$H$17,$G$2:$G$17,"Miss")". This column gave me the final standing or if they missed the playoffs entirely. 
From there - I wanted to set a new column that told me what round of the playoffs they made it to. I did this with a weighted score system. That is as follows: 
Finals - 5 
Semi Finals - 3
Divisional - 2
First round exit - 1
Missed - 0

I then used  "=IF(E2<=2,5,IF(E2<=4,3,IF(E2<=8,2,IF(E2<=16,1,0))))"
That allows me to have a collumn that shows what round they made it to and I can reference that later. 

From here, I took each season and put them all on one sheet with their odds and the weighted Score.

I then calculated the Average Preseason odds for each team that made the finals, semi finals, divisinal, first round exit and then missed the playoffs as well.

Round    Score    Avg PreSeason Odds
Finalist    5    2376.4
Semi Finalist    3    2412.5
Divisinal     2    3205.3
First Round Exit    1    3566.7
Missed    0    8297.4

I then found the team that had the best odds at preseason that missed the play offs with =MINIFS(C2:C281,D2:D281,H6). 
Then to find the team and season that was a associated with I used =INDEX(B2:B281,MATCH(MINIFS($C$2:$C$281,$D$2:$D$281,$H$6),$C$2:$C$281,0))

# Goal Differential. 

The Goal Differential is a stat used to normalize the total number of goals scored all season minus the total number of goals they let through. Goals for and Goals against is usually how that is referred to. 
I did the same seperation for each season as I did for the preseason odds, only with the below columns. 
Team
Win
Loss
Overtime Loss
Total Points (you get two points for winning a game in regulation and 1 point for either winning a game in OT or losing a game in OT)
Goals for 
Goals against 
Goal differential (GF - GA)
Goal differential Rank (ranked for that season) =RANK(I2,$I$2:$I$33,0)
Play off outcome (same as the preseason odds)
Weighted Score (same as the preseason odds)
Regular Season Rank (who had the most points)

I then put all of these outcomes in a seperate tab that had all the seasons, Goal differential Rank and Weighted Score. 

I performed the same calculattions to find the average rank in Goal Differential that each team had that made the finals, semi finals, divisinal, first round exit and those who missed the playoffs.  =AVERAGEIF($E$2:$E$281,I2,$D$2:$D$281)

Round    Score    AVG GD Rank
Finalist    5    6.72
Semi Finalist    3    8.00
Divisinal     2    7.36
First Round Exit    1    10.86
Missed    0    23.30

# Power Play Score and Power Play Kill %

Here I wanted to see if there was a commonality in powerplay success and power play kill.

I started out with a tab per season like I have done with the other calculations I have done. The columns I care about are below. 

Team
PP% 
PPK% 
Outcome
Weighted score 

From here - I put each season in a seperate tab with the columns. 

Team
PP%
PPK%
Weighted Score

And from here calculated the average PP% and PPK% that made it to each round of the play off and got 

Round    Score    AVG PP%    AVG PPK%
Finalist    5      22.5%    80.9%
Semi Finalist    3    21.8%    81.7%
Divisinal     2    22.0%    81.8%
First Round Exit 1    21.1%    80.6%
Missed    0       18.5%    78.5%

# Comin' in Hot

It seems that conventional wisdom states that teams that come into the playoffs winning tend to do better. 

Well ... It looks like, you just need to win a little more than half your games and you statistically could still make it to the finals. 

I was able to grab data of the last 25 games from nhlstattrick.com and I calculated their win/loss record by just dividing their wins by total number of games played. That gives me eache team's Win Percentage.

I had each season in their own tab again and then put each season in one tab so that I could run some numbers. 

Here I was able to see the average win percentage of each round and got the below table: 

Round    Score    Average Win%
Finalist    5    57%
Semi Finalist    3    62%
Divisional    2    58%
First-round exit    1    57%
Missed    0    41%

From there I was able to run a quick calculation to see who had the worst win% going into the playoffs that still made it to the cup and that was the 2015 Chicago Blackhawks. The team that had the best win% but missed the playoffs was the 2016 Blues. Dont feel too bad - they ended up winning it all in 2019. 

=INDEX(B2:B281,MATCH(MINIFS($C$2:$C$281,$D$2:$D$281,$I$2),$C$2:$C$281,0))

The above formula gave me the team name of that had the worst win% that made it to the finals. I just dragged it over to get the season. 

# Presidents Trophy Curse

This is the section that made me want to do this project. 

The preds were coming off of their season where they beat all the odds and made it to the finals. They lost but the idea was they were not even supposed to have made it! They will be back! 

Uh oh. 

They did so well that they ended up winning the presi in 2018. We all had our concerns and those concerns were valid becuase they had a first round exit which was just gutting. 

What I did here was track each year in this dataset and calculate the rankings of each team per season by their total number of points. 

That gave me the number one ranked team each season and I put them in their own tab again. I am using the GF_GA_Presidents_Trophy spreadsheet. 

Here I counted the average regular season rank of the teams that made it to the finals and found that you just have to be at least the 7th best team and you can feel confident that your team could make the finals! Except if you win the presi. There have only been 8 teams to win the presi since it was created in the 80's. 

I then found here that as expected, the preds in 2017 had the worst regular season rank to make the finals. And guess who had the best regularseason rank and made the finals? The 2017 Penguins... Pain. 

# Putting it all together 

So at this point, I have not found my smoking gun. So far, the metrics I have looked at have not given me anything to rely on to help determine who could make the finals. But I wanted to try one more thing. 

So I derived a scoring system based off of the metrics that we have found today. 2 ponts if the team had favorable scoring metrics that were in line with or better than the averages we found that made it to the finals, 1 point if they had numbers that were in line with in between the best and the worst metrics of teams that made it to the playoffs and then I weighted the score so that I can allot a score with more weight than the others. 

I know that is a lot and the reason I am going quick is because... It meant nothing!!! 

I tried my metrics on this year's outcome. 

Vegas Golden Knights
Tampa Bay Lightning
Toronto Maple Leafs
Los Angeles Kings
Colorado Avalanche
Washington Capitols
Dallas Stars
Winnipeg Jets
New Jersey Devils
Vancouver Canucks
Edmonton Oilers
Carolina Hurricanes
Ottawa Senators
Florida Panthers
St. Louis Blues
New York Rangers

After all of my calculations - I BASICALLY got the final standings of teams that head into the playoffs. 

Winnipeg Jets
Washington Capitals
Vegas Golden Knights
Toronto Maple Leafs
Dallas Stars
Los Angeles Kings
Colorado Avalanche
Tampa Bay Lightning
Edmonton Oilers
Carolina Hurricanes
Florida Panthers
Minnesota Wild
Ottawa Senators
Calgary Flames
St. Louis Blues
Montreal Canadiens

The two teams that are in the finals now are Edmonton and Florida so what do I know. 

# Final Thoughts. 

So what does this all mean? 

Well - All you have to do is make the playoffs and then all bets are off. We have some numbers to say the LIKELYHOOD that a team may not make it based off of a certain metric but we unfortunately did not find anything that could suggest that these metrics do not help us find who makes the final. 

With more time, I may add to this analysis over time but I will stop here. 
