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

### Bivariate Analysis

### Interesting Aggregates

## Assessment of Missingness

## Hypothesis Testing

**Null Hypothesis** 
: The average kills in-game are equal across all positions

**Alternative Hypothesis**
: At least one position has a significantly different average kills in-game

**Test Statistics**
: The difference in the mean number of kills across all positions

**Signifiance Level**
: 0.05 or 5%

The result of running the ANOVA test on 

<iframe
  src="assets/pos_kills.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Framing a Prediction Problem
**Prediction Problem:**
: Predict the position based on the cs

- Type:
: Multiclass Classification

**Response Variable:**
: Position (Top, Bot, Jungle, Mid, Support)

I chose this variable because each position is unique and contributes to the game differently. Being able to predict the role of the player based on the stats that they generate throughout the game can be valuable in analyzing whether the player has efficiently played their role.

Creep Score / time prediction the total creep score

**Metric:**
: Accuracy

I believe that using accuracy as the metric over F1-score is a better choice for this data set because the positions are balanced across the data set with each role per team per game.


## Baseline Model
## Final Model
## Fairness Analysis
