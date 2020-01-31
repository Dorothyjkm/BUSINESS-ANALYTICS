###### 1. Max Attended Game

```ruby
SELECT  CD.season AS Season,
        AB.attendance AS Attendance,
        AB.venue_capacity AS Venue_Capacity,
        AB.venue_name AS Venue,
        AB.venue_country AS Country,
        CD.name AS TeamA,
        CD.opp_name AS TeamB,
FROM `bigquery-public-data.ncaa_basketball.mbb_games_sr` AS AB
JOIN `bigquery-public-data.ncaa_basketball.mbb_teams_games_sr` AS CD
ON (AB.game_id = CD.game_id)
ORDER BY attendance DESC
LIMIT 1;
```
###### Result

| Season	| Attendance	| Venue_Capacity	| Venue	| Country	| TeamA	| TeamB |
| --- | --- | --- | --- | --- | --- | --- |
| 2014	| 200053	| 21750	| Dean Smith Center	| USA	| Tribe	Tar | Heels |

###### 2. Top 10 Scoring Matches

```ruby
SELECT  A.season AS Season,
        A.game_date AS Date,
        A.win_name AS Winner,
        A.win_pts AS Win_Score,
        B.mascot AS Mascot,
        A.lose_name AS Loser,
        A.lose_pts AS Loser_Score,
        C.mascot AS Mascot_
FROM `bigquery-public-data.ncaa_basketball.mbb_historical_tournament_games` AS A
JOIN `bigquery-public-data.ncaa_basketball.mascots` AS B ON A.win_team_id = B.id
JOIN `bigquery-public-data.ncaa_basketball.mascots` AS C ON A.lose_team_id = C.id
ORDER BY win_pts DESC
LIMIT 10;
```
###### Result

| Season	| Date	| Winner	| Win_Score	| Mascot	| Loser	| Loser_Score	| Mascot_ |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1990	| 1990-03-18	| Lions	| 149	| Lion	| Wolverines	| 115	| None |
| 1990	| 1990-03-25	| Rebels	| 131	| Rebel	| Lions	| 101	| Lion |
| 1989	| 1989-03-18	| Sooners	| 124	| Human	| Bulldogs	| 81	| Bulldog |
| 1988	| 1988-03-19	| Tar Heels	| 123	| Sheep	| Lions	| 97	| Lion |
| 2007	| 2007-03-16	| Volunteers	| 121	| Coonhound	| 49ers	| 86	| 49er |
| 1989	| 1989-03-16	| Razorbacks	| 120	| Red Russian Boar	| Lions	| 101	| Lion |
| 1988	| 1988-03-17	| Lions	| 119	| Lion	| Cowboys	| 115	| Cowboy |
| 1991	| 1991-03-15	| Razorbacks	| 117	| Red Russian Boar	| Panthers	| 76	| Panther |
| 1991	| 1991-03-14	| Wolfpack	| 114	| Wolf	| Golden Eagles	| 85	| Golden Eagle |
| 2008	| 2008-03-21	| Tar Heels	| 113	| Sheep	| Mountaineers	| 74	| Mountaineer |

###### 3. Top 10 Scoring teams All Time

```ruby
SELECT A.season AS Season,
        A.name AS Team,
        A.alias AS Alias,
        A.wins AS Wins,
        A.losses AS Losses,
        A.ties AS Ties,
        B.turner_name AS Name,
        B.league_name AS League,
        B.division_name AS Division,
        B.venue_city AS Base,
        B.venue_address AS Address,
        B.venue_country AS Country,
FROM `bigquery-public-data.ncaa_basketball.mbb_historical_teams_seasons` AS A
JOIN `bigquery-public-data.ncaa_basketball.mbb_teams` AS B ON A.team_id = B.id
ORDER BY wins DESC
LIMIT 10;
```
###### Result

| Season	| Team	| Alias	| Wins	| Losses	| Ties	| Name	| League	| Division	| Base	| Address	Country |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1975	| Eagles	| COPP	| 39	| 2	| 0	| Coppin State University	| NCAA MEN	| NCAA Division I	| Baltimore	2500 W North Ave	| USA |
| 2014	| Wildcats	| UK	| 38	| 1	| 0	| University of Kentucky	| NCAA MEN	| NCAA Division I	| Lexington	432 West Vine Street	| USA |
| 2011	| |Wildcats	| UK	| 38	| 2	| 0	| University of Kentucky	| NCAA MEN	| NCAA Division I	| Lexington	432 West Vine Street	| USA |
| 1998	| Blue Devils	| DUKE	| 37	| 2	| 0	| Duke University	| NCAA MEN	| NCAA Division I	| Durham	301 Whitford Drive	| USA |
| 2004	| Fighting Illini	| ILL	| 37	| 2	| 0	| University of Illinois, Champaign	| NCAA MEN	| NCAA Division I	| Champaign	1800 South 1st Street	| USA |
| 2007	| Jayhawks	| KU	| 37	| 3	| 0	| University of Kansas	| NCAA MEN	| NCAA Division I	| Lawrence	1651 Naismith Drive	| USA |
| 1986	| Rebels	| UNLV	| 37	| 2	| 0	| University of Nevada, Las Vegas	| NCAA MEN	| NCAA Division I	| Paradise	4505 S Maryland Parkway	| USA |
| 2016	| Bulldogs	| GONZ	| 37	| 2	| 0	| Gonzaga University	| NCAA MEN	| NCAA Division I	| Spokane	801 North Cincinnati St	| USA |
| 1985	| Blue Devils	| DUKE	| 37	| 3	| 0	| Duke University	| NCAA MEN	| NCAA Division I	| Durham	301 Whitford Drive	| USA |
| 2013	| Gators	| FLA	| 36	| 3	| 0	| University of Florida	| NCAA MEN	| NCAA Division I	| Gainesville	250 Gale Lemerand Drive	| USA |

###### 4. Teams & Mascots

```ruby
SELECT  name AS Team,
        mascot AS Mascot,
        mascot_name AS Mascot_Name,
FROM `bigquery-public-data.ncaa_basketball.mascots`
ORDER BY name ASC
LIMIT 9;
```
###### Result

| Team	| Mascot |	Mascot_Name |
| ---| --- | ---|
| 49ers |49er	| Prospector Pete |
| 49ers	| 49er	| Norm |
| Aces	| Riverboat | Gambler	Ace Purple |
| Aggies	| Dustdevil	| Dusty |
| Aggies	| Cowboy	| Pistol Pete |
| Aggies	| Bulldog	| Aggie and Aggietha |
| Aggies	| Bull	| Big Blue |
| Aggies	| Mustang	| Gunrock |
| Anteaters	| Anteater	| Peter |

###### 5. Tallest Players Top 10

```ruby
SELECT DISTINCT jersey_number AS Jersey_Number,
        full_name AS Name,
        height AS Height,
        birth_place AS Birth_Place,
        team_name AS Team,
        active AS Active,
        position AS Position,
FROM `bigquery-public-data.ncaa_basketball.mbb_players_games_sr`
ORDER BY height DESC
LIMIT 10;
```
###### Result

| Jersey_Number |	Name	| Height	| Birth_Place	| Team	| Active	| Position |
| --- | --- | --- | --- | --- | --- | --- |
| 25	| Seth Callahan	| 511	| "Hanover Township, PA"	| Crusaders	| true	| G |
| 4	| Seth Callahan	| 511	| "Hanover Township, PA"	| Highlanders	| true	| G |
| 24	| Tacko Fall	| 90	| "Dakar,, SEN"	| Knights	| true	| C |
| 34	| Mamadou Ndiaye	| 90	| "Dakar,, SEN"	| Anteaters	| true	| C |
| 2	| Sim Bhullar	| 89	| "Toronto, ON"	| Aggies	| true	| C |
| 41	| Blake Vedder	| 88	| "Chesterland, OH, USA" | Golden Flashes	| true	| C |
| 12	| Chris Sodom	| 87	| "Kaduna,, NGA"	| Hoyas	| true	| C |
| 35	| Mark Jackson	| 87	| "Salt Lake City, UT, USA"	| Quakers	| true	| C |
| 32	| Matt Haarms	| 87	| "Amsterdam,, NLD"	| Boilermakers	| true	| F |
| 42	| Jordan Omogbehin	| 87	| "Lagos, LA, NGA"	| Bears	| true	| C |

###### 6. Top 10 Scoring Players

```ruby
SELECT  season AS Season,
        full_name AS Name,
        jersey_number AS Jersey_Number,
        birth_place AS Birth_Place,
        team_name AS Team,
        active AS Active,
        position AS Position,
        field_goals_made AS Scored,
        field_goals_att AS Attempt,
        personal_fouls AS Fouls,
FROM `bigquery-public-data.ncaa_basketball.mbb_players_games_sr`
ORDER BY field_goals_made DESC
LIMIT 10;
```
###### Result

| Season	| Name	| Jersey_Number	| Birth_Place	| Team	| Active	| Position	| Scored	| Attempt	| Fouls |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2013	| Aaric Murray	| 24	| Philadelphia, PA	| Tigers	| TRUE	| C	| 20	| 28	| 0 |
| 2013	| Melvin Ejim	| 3	| Toronto, ON, CAN	| Cyclones	| TRUE	| F	| 20	| 24	| 3 |
| 2014	| CJ Carter	| 10	| Omaha, NE, USA	| Mavericks	| TRUE	| G	| 19	| 25	| 5 |
| 2015	| Jawun Evans	| 1	| Dallas, TX, USA	| Cowboys	| TRUE	| G	| 18	| 31	| 0 |
| 2016	| Chris Clemons	| 3	| Raleigh, NC, USA	| Fighting Camels	| TRUE	| G |	18	| 32	| 2 |
| 2016	| Malik Monk	| 5	| Lepanto, AR, USA	| Wildcats	| TRUE	| G	| 18	| 28	| 0 |
| 2017	| Rob Marberry	| 0	| Nashville, TN, USA	| Bisons	| TRUE	| F	| 18	| 24	| 2 |
| 2016	| Cameron Morse	| 24	| Flint, MI, USA	| Penguins	| TRUE	| G	| 18	| 38	| 0 |
| 2016	| Jacob Wiley	| 24	| Newport, WA, USA	| Eagles	| TRUE	| F	| 18	| 23	| 5 |
| 2015	| Jameel Warney	| 20	| Plainfield, NJ, USA	| Seawolves	| TRUE	| F	| 18	| 22	| 1 |

###### 7. Top 10 Home Game Scores

```ruby
SELECT  A.season AS Season,
        A.scheduled_date AS Date,
        A.attendance AS Attendance,
        A.venue_city AS Venue,
        A.h_name AS Home_Team,
        A.h_points_game AS Home_Score,
        A.a_name AS Away_Team,
        A.a_points_game AS Away_Points
FROM `bigquery-public-data.ncaa_basketball.mbb_games_sr` AS A
WHERE A.season=2014
ORDER BY h_points_game DESC
LIMIT 10;
```
###### Result

| Season	| Date	| Attendance	| Venue	| Home_Team	| Home_Score	| Away_Team	| Away_Points |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2014	| 2014-12-03	| 1072	| Lexington	| Keydets	| 133	| Mustangs	| 62 |
| 2014	| 2014-12-16	| 1673	| Beaumont	| Cardinals	| 128	| Tigers	| 54 |
| 2014	| 2014-11-27	| 1414	| New Rochelle	| Gaels	| 126	| Hornets	| 76 |
| 2014	| 2015-01-03	| 1607	| Mount Pleasant	| Chippewas	| 125	| Knights	| 80 |
| 2014	| 2014-11-19	| 884	| Lexington	| Keydets	| 124	| Royals	| 42 |
| 2014	| 2014-11-19	| 1222	| Durham	| Eagles	| 123	| Mighty Believers	| 65 |
| 2014	| 2014-11-29	| 1535	| Morehead	| Eagles	| 121	| Knights	| 49 |
| 2014	| 2014-12-28	| 1023	| Radford	| Highlanders	| 119	| Knights	| 69 |
| 2014	| 2014-12-07 | 	| Elon	| Phoenix	| 117	| Knights	| 73 |
| 2014	| 2014-11-15	| 4238	| Evansville	| Aces	| 116	| Quakers	| 45 |

###### 8. Top 10 High Capacity Venues

```ruby
SELECT  name AS Team,
        turner_name AS Name,
        league_alias AS League,
        venue_city AS City,
        venue_state AS State,
        venue_address AS Address,
        venue_zip AS ZIP,
        venue_country AS Country,
        venue_name AS Venue,
        venue_capacity AS Capacity,
FROM `bigquery-public-data.ncaa_basketball.mbb_teams`
ORDER BY venue_capacity DESC
LIMIT 10;
```
###### Result

| Team	| Name	| League	| City	| State	| Address	| ZIP	| Country	| Venue	| Capacity |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Orange	| Syracuse University	| NCAAM	| Syracuse	| NY	| 900 Irving Ave	| 13210	| USA	| Carrier Dome	| 35446 |
| Wildcats	| University of Kentucky	| NCAAM	| Lexington	| KY	| 432 West Vine Street	| 40506	| USA	| Rupp Arena	| 23500 |
| Spartans	| University of North Carolina at Greensboro	| NCAAM	| Greensboro	| NC	| 1921 West Gate City Blvd	| 27403	| USA	| Greensboro Coliseum Complex	| 23500 |
| Cardinals	| University of Louisville	| NCAAM	| Louisville	| KY	| 1 Arena Plaza	| 40202	| USA	| KFC Yum! Center	| 22090 |
| Tar Heels	| University of North Carolina, Chapel Hill	| NCAAM	| Chapel Hill	| NC	| 300 Skipper Bowles Drive	| 27514	| USA	| Dean Smith Center	| 21750 |
| Volunteers	| University of Tennessee, Knoxville	| NCAAM	| Knoxville	| TN	| 1600 Phillip Fulmer Way	| 37916	| USA	| Thompson-Boling Arena	| 21678 |
| Wildcats	| Villanova University	| NCAAM	| Philadelphia	| PA	| 3601 S. Broad St.	| 19148	| USA	| Wells Fargo Center	| 21600 |
| Hoyas	| Georgetown University	| NCAAM	| Washington	| DC	| 601 F St. N.W.	| 20004	| USA	| Verizon Center	| 20308 |
| Wolfpack	| North Carolina State University	| NCAAM	| Raleigh	| NC	| 1400 Edward Mill Rd	| 27607	| USA	| PNC Arena	| 19722 |
| Razorbacks	| University of Arkansas, Fayetteville	| NCAAM	| Fayetteville	| AR	| 1270 West Leroy Pond Dr	| 72701	| USA	| Bud Walton Arena	| 19368 |

###### 9. Top 10 Away Game Scores

```ruby
SELECT  season AS Season,
        scheduled_date AS Date,
        attendance AS Attendance,
        venue_city AS Venue,
        h_name AS Home_Team,
        h_points_game AS Home_Score,
        a_name AS Away_Team,
        a_points_game AS Away_Points
FROM `bigquery-public-data.ncaa_basketball.mbb_games_sr`
WHERE season=2014
ORDER BY a_points_game DESC
LIMIT 10;
```
###### Result

| Season	| Date	| Attendance	| Venue	| Home_Team	| Home_Score	| Away_Team	| Away_Points |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2014	| 2014-11-25	| 2400	| Maui	| Silverswords	| 85	| Cougars	| 121 |
| 2014	| 2015-02-21	| 3060	| Cullowhee	| Catamounts	| 111	| Keydets	| 113 |
| 2014	| 2014-12-21	| 1473	| Kansas City	| Kangaroos	| 104	| Cardinals	| 110 |
| 2014	| 2014-12-11	| 3172	| Missoula	| Grizzlies	| 99	| Wildcats	| 110 |
| 2014	| 2015-02-04	| 2120	| Conway	| Bears	| 108	| Demons	| 110 |
| 2014	| 2014-11-23	| 1897	| Lexington	| Keydets	| 93	| Seahawks	| 110 |
| 2014	| 2015-01-14	| 875	| Conway	| Bears	| 58	| Lumberjacks	| 109 |
| 2014	| 2015-01-17	| 1250	| San Antonio	| Cardinals	| 98	| Lions	| 108 |
| 2014	| 2015-03-08	| 2830	| Pittsburgh	| Dukes	| 78	| Wildcats	| 107 |
| 2014	| 2014-12-11	| 618	| Baltimore	| Eagles	| 64	| Pride	| 105 |

###### 10. Teams from Texas

```ruby
SELECT  name AS Team,
        turner_name AS Name,
        league_alias AS League,
        venue_city AS City,
        venue_state AS State,
        venue_address AS Address,
        venue_zip AS ZIP,
        venue_country AS Country,
        venue_name AS Venue,
        venue_capacity AS Capacity,
FROM `bigquery-public-data.ncaa_basketball.mbb_teams`
WHERE venue_state = 'TX'
LIMIT 10;
```
###### Result

| Team	| Name	| League	| City	| State	| Address	| ZIP	| Country	| Venue	| Capacity |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Longhorns	| University of Texas at Austin	| NCAAM	| Austin	| TX	| 1701 Red River Street	78701	| USA	| Frank C. Erwin Jr. Center	| 16540 |
| Red Raiders	| Texas Tech University	| NCAAM	| Lubbock	| TX	| 1701 Indiana Ave	79409	| USA	| United Supermarkets Arena	| 15098 |
| Bears	| Baylor University	| NCAAM	| Waco	| TX	| 1900 S University Parks Dr	76706	| USA	| Ferrell Center	| 10284 |
| Horned Frogs	| Texas Christian University	| NCAAM	| Fort Worth	| TX	| 2900 Stadium Drive	76129	| USA	| Schollmaier Arena	| 7201 |
| Mavericks	| University of Texas at Arlington	| NCAAM	| Arlington	| TX	| 601 S Pecan St	76019	| USA	| College Park Center	| 7000 |
| Bobcats	| Texas State University-San Marcos	| NCAAM	| San Marcos	| TX	| 601 University Drive	78666	| USA	| Strahan Coliseum	| 7200 |
| Lumberjacks	| Stephen F. Austin State University	| NCAAM	| Nacogdoches	| TX	| 700 E College St	75961	| USA	| William R. Johnson Coliseum	| 7203 |
| Bearkats	| Sam Houston State University	| NCAAM	| Huntsville	| TX	| 1964 Bobby K. Marks Dr	77340	| USA	| Bernard Johnson Coliseum	| 6110 |
| Huskies	| Houston Baptist University	| NCAAM	| Houston	| TX	| 7502 Fondren Rd	77074	| USA	Sharp Gymnasium	| 1000 |
| Cardinals	| University of the Incarnate Word	| NCAAM	| San Antonio	| TX	| 4301 Broadway	78209	| USA	| McDermott Center	| 2000 |
