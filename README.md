# League of Legends Kills vs Role
By: Janie Chan (jlc006@ucsd.edu)

## Introduction
Within the realm of the gaming community, the game League of Legends (LOL) created by the company Riot Games became a global sensation in 2011. To this day, LOL continues to rise, gaining both players and audience in worldwide games. The data set that I will be working with is the 2022 esports matches provided by Oracle's Elixir.

### The relevant fields of the data for my analysis
There are a total of 150588 rows in the dataset

`gameid`
: The unique identifier of each individual match.

`position`
: The role of each player in the 5 v 5 match, which includes top, bot, mid, jng, sup, and team.

`kills`
: The count of kills on their opponent of each player.

`total cs`
: The creep score(cs) is the number of minions, monsters, and champion-summoned units a player has killed throughout the game by dealing the killing blow. This column displays the total creep score of each player.

`minionkills`
: The number of minions that the player has killed throughout the match.

`monsterkills`
: The number of monsters that the player has killed throughout the match.

`cspm`
: The calculated cs per minute which is the total creep score of each player divided by the total minutes of the match.

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
As the dataset initially included 150588 rows × 163 columns, I have brought it down to 125490 rows × 7 columns.  

Display of the head of the Dataframe:

`print(df_cleaned[['gameid', 'position', 'kills', 'total cs', 'minionkills', 'monsterkills', 'cspm']].head().to_markdown(index=False))`

| gameid                | position   |   kills |   total cs |   minionkills |   monsterkills |   cspm |
|:----------------------|:-----------|--------:|-----------:|--------------:|---------------:|-------:|
| ESPORTSTMNT01_2690210 | top        |       2 |        231 |           220 |             11 | 8.0911 |
| ESPORTSTMNT01_2690210 | jng        |       2 |        148 |            33 |            115 | 5.1839 |
| ESPORTSTMNT01_2690210 | mid        |       2 |        193 |           177 |             16 | 6.7601 |
| ESPORTSTMNT01_2690210 | bot        |       2 |        226 |           208 |             18 | 7.9159 |
| ESPORTSTMNT01_2690210 | sup        |       1 |         42 |            42 |              0 | 1.4711 |

### Univariate Analysis
<iframe
  src="assets/his_kills.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>
In this Histogram, we can clearly see a trend of an exponential decrease. This shows that as the amount of kills increases, the amount of players with that amount of kills decreases.

<iframe
  src="assets/his_cs.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>

### Bivariate Analysis
<iframe
  src="assets/scatter_cs_cspm.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/scatter_cs_minions.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
In this scatter plot comparing the total cs score and minion kills, the data is increasing linearly. While looking at the plot, I've noticed that there is a very strong line of data.

### Interesting Aggregates
`print(df_grouped[['position', 'kills', 'total cs', 'minionkills', 'monsterkills', 'cspm']].head().to_markdown(index=False))`

| position   |    kills |   total cs |   minionkills |   monsterkills |    cspm |
|:-----------|---------:|-----------:|--------------:|---------------:|--------:|
| bot        | 4.26054  |   278.448  |      256.522  |       22.5487  | 8.8048  |
| jng        | 3.05698  |   172.999  |       33.613  |      143.207   | 5.62992 |
| mid        | 3.50398  |   260.71   |      244.071  |       17.1006  | 8.28325 |
| sup        | 0.874851 |    35.3911 |       34.9547 |        0.44011 | 1.13187 |
| top        | 2.79644  |   247.337  |      232.63   |       15.1276  | 7.86113 |

## Assessment of Missingness
### NMAR Analysis
I believe that the columns `monsterkillsownjungle` and `monsterkillsenemyjungle` are Not Missing At Random NMAR. They do not rely on any other observed columns.


## Hypothesis Testing

**Null Hypothesis:** 
: The average kills in-game are equal across all positions

**Alternative Hypothesis:**
: At least one position has a significantly different average kills in-game

**Test Statistics:**
: The difference in the mean number of kills across all positions

**Signifiance Level:**
: 0.05 or 5%

The result of running this hypothesis test returned a p-value of 0.00. From this, we can reject the null hypothesis that the average kills in-game are equal across all positions. Though the p-value is 0.00, this doesn't mean that it is impossible for the null hypothesis. Remember, we are analyzing the professional league so this may have impacted the results.

<iframe
  src="assets/pos_kills.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>

## Framing a Prediction Problem
**Prediction Problem:**
: Predict the position based on the cs

- Type:
: Multiclass Classification

**Response Variable:**
: Position (Top, Bot, Jungle, Mid, Support)

I chose this variable because each position is unique and contributes to the game differently. Being able to predict the role of the player based on the stats that they generate throughout the game can be valuable in analyzing whether the player has efficiently played their role. The stats used were all collected post-game.

**Metric:**
: Accuracy

I believe that using accuracy as the metric over F1-score is a better choice for this data set because the positions are balanced across the data set with each role per team per game.


## Baseline Model
In my Baseline Model, I used the RandomForestClassifer and had 3 features. I had 2 quantitative features which are `cspm` and `total cs`. For the last feature, `position` is a categorical feature.

The resulting accuracy is 55.18% which is not that good and definitely could be improved on.

## Final Model
The two new features that I added to the model are `minionkills` and `monsterkills`. I believe these are good for my prediction task because from my Interesting Aggregates section, the mean of these features differs significantly based on the position. The accuracy from adding these two features increased to 64.27%

## Fairness Analysis
**Group X:**
: Players with total cs <= 200

**Group Y:**
: Players with total cs > 200


**Evaluation Metric:**
: Precision

**Null Hypothesis:**
: Our model is fair. Its precision for players with total cs greater than 200 and players with total cs less than or equal to 200 are roughly the same, and any differences are due to random chance.

**Alternative Hypothesis:**
: Our model is unfair. Its precision for players with total cs greater than 200 and players with total cs less than or equal to 200 are not roughly the same.

**Test Statistics:**
: The absolute difference in precision between Group X (total CS ≤ 200) and Group Y (total CS > 200)

**Significance Level:**
: 0.05 or 5%

The resulting p-value I got is 0.0000. Due to 0.0000 being less than our significance level of 0.05, we can reject our null hypothesis and conclude that the precision between Group X and Group Y are not roughly the same.

