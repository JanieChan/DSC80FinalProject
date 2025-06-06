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
As the dataset initially included 150588 rows × 163 columns, I have brought it down to 7 columns. 

Display of the head of the Dataframe:
print(df[['gameid', 'position', 'kills', 'total cs', 'minionkills', 'monsterkills', 'cspm']].head().to_markdown(index=False))

## Assessment of Missingness

## Hypothesis Testing
## Framing a Prediction Problem
## Baseline Model
## Final Model
## Fairness Analysis
