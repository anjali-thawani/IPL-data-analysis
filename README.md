
# IPL Data Analysis 

## Overview

This Power BI project focuses on analyzing Indian Premier League (IPL) data, providing insights into live batting, bowling statistics, and historical match data. The project includes a live dashboard showcasing real-time batting and bowling performances, along with detailed information on previous matches.
## Problem Statement

The primary objectives of this project are:

- Identify players with the highest runs.
- Track the number of sixes and fours scored by each player.
- Analyze the number of wickets taken by bowlers.
- Calculate the run rate of players.
- Create a points table displaying team standings, including the number of matches won, lost, and their net run rate.

## Features

- Live Dashboard: Provides real-time updates on batting and bowling performances during matches.
- Historical Data Analysis: Offers insights into past matches, player performances, and team standings.
- Visualization: Utilizes Power BI's visualization capabilities to present data in an intuitive and visually appealing manner.


### Steps followed 

- Step 1 : Retrieve IPL Data from Rapid API:
 Utilize the Rapid API to fetch IPL data.

- Step 2 : Data Processing in Power Query:
Access Power Query for further data processing.

- Step 3 : Data Cleaning and Filtering:
Perform data cleaning tasks such as removing null values, filtering relevant information, and creating necessary tables.

- Step 4 : Image Handling:
Check for empty images and replace them with dummy images to ensure visual consistency.

- Step 5 : Batsman and Bowler Information:
Gather information on batsmen and bowlers for analysis.

- Step 6 : Creating Interactive Live Dashboard:
Design an interactive dashboard providing real-time updates on IPL matches, including batting and bowling performances.

- Step 7 : Points Table Dashboard:
Develop a dashboard presenting points tables, net run rates, matches won, and matches lost by each team.

- Step 8 : Tooltip for Batsman Information:
Implement tooltips to display additional information about batsmen.

- Step 9 : DAX Measures Used:
Implement various DAX measures for calculations.

#### curr_score: 
Calculate the current score based on innings
           
           Inning_one_score = var val = [inning_1]
            RETURN
           CALCULATE(VALUES(Live_team_score[current_score]), Live_team_score[inningsId]= val)


           Inning_two_score = var val = [inning_2]
           RETURN
           CALCULATE(VALUES(Live_team_score[current_score], Live_team_score[inningsId]= val)


           curr_score = IF([Total_innings]>1, [Inning_two_score], [Inning_one_score])

![Screenshot (216) - Copy](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/183e1523-8e22-4cd0-b68e-de9eadbd57c5)

#### curr_team_name: 
Identify the current team batting

           curr_team_name = IF([Total_innings]>1, [Inning_two_name], [Inning_one_name])
        
![Screenshot (217)](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/f185ee78-e34e-45e9-bc7c-e7eb865aa3a2)

#### toss_winner_info: 
Determine toss winner and decision.


            toss_winner_info =
            var teamid= CALCULATE(VALUES(Live_Toss_info[Value]), Live_Toss_info[Name]= "tossWinnerId")
            var decision = CALCULATE(VALUES(Live_Toss_info[Value]), Live_Toss_info[Name]= "decision")
            var teamSname1 = CALCULATE(VALUES(Matches_List[teamSName_1]), Matches_List[teamId_1]=teamid)
            var teamSname2 = CALCULATE(VALUES(Matches_List[teamSName_2]), Matches_List[teamId_2]=teamid)
            var check = IF(teamSname1=BLANK(), teamSname2, teamSname1)
            RETURN check&" opt to "&decision

![Screenshot (217) - Copy](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/cece67ba-1def-47ee-969f-feb608651189)


#### Total_fours_curr_inning:
Calculate total fours by the current batting team.


         Total_fours_curr_inning =
         var teamname = [curr_bat_team_name]
         var val = CALCULATE(SUM(Batsman_Live_score[fours]), Batsman_Live_score[batTeamName]= teamname)
         RETURN
         IF(ISBLANK(val),0,val)

![Screenshot (219) - Copy](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/32cea5e1-9f7b-43d4-885b-deda2c7e1f2b)

#### Total_sixes_curr_inning: 
Calculate sixes by the current batting team.

         Total_sixes_curr_inning = 
         var teamname = [curr_bat_team_name]
         var val = CALCULATE(SUM(Batsman_Live_score[sixes]), Batsman_Live_score[batTeamName]= teamname)
         RETURN
         IF(ISBLANK(val),0,val)

![Screenshot (218) - Copy](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/6587503b-3f2e-4be0-aeeb-4dbd2bcc8124)

#### bat_team_cap_img: 
Retrieve image of batting team captain.


           bat_team_cap_img = var teamname = [batTeamName]
           RETURN
           CALCULATE(VALUES(Team_logo[Captain Images]), Team_logo[Team]= teamname)

![Screenshot (215) - Copy](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/7fc26e91-098b-4967-b51c-997e538d09b0)

#### bowl_team_cap_img: 
Retrieve image of bowling team captain.


           bowl_team_cap_img = var teamname = [bowlTeamName]
           RETURN
           CALCULATE(VALUES(Team_logo[Captain Images]), Team_logo[Team]= teamname)

![Screenshot (215)](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/a6f2e4a9-43bc-4866-9377-0ae3ab27e347)



 # Report Snapshot (Power BI DESKTOP)
 
 ### Live Dashboard of SRH vs MI (6 May 2024)
![Dashboard](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/cb7c1355-a16b-4bff-bf62-504408f0de6a)

### Tooltip used
![Tooltip](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/e4e29afa-a746-4436-8b3d-9bf84772ea12)

### Points Table
![Screenshot (226)](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/b549cb5c-3fa2-4289-b9e7-293a5d418718)

![Screenshot (223)](https://github.com/anjali-thawani/IPL-data-analysis/assets/168136647/711a9985-1f43-4eb0-937a-a59d30c1f4bf)
