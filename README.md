# player_predictor
NBA player point predictor using gradient descent and ridge regression, taking stats from the past three years alongside the opposing team's defensive stats.

## Current Layout
Pulls tables from basketball-reference.com with the custom url for each player, filtering stats that correlate to points scored.
Pulls from nbastuffer.com to pull the defensive stats of each team given a year
Corresponds each game played from the last three years (if active), combined with the team's defensive stats from the year.
Lays it out into one data frame (X), with points being the respective result (y)
Runs gradient descent with regression to determine how heavily each feature factors into the amount of points scored at the end of the night.
Given an input of the player name and opposing team's city, sets that into a new df input, and applies the feature strength found from gd. Returning a number and range of expected points.

## Current Limitations

### Instances where players share similar url formats:
the url is separated by first 5 letters of the last name, and first 2 letters of the first name, followed by a number (...01, ...02). If these 7 letters are the same between two players, they are then separated by number, but there is no way to differentiate which one is correct at the moment. This leads to a return of an empty table for some names.
#### Solution:
Either find a more reliable site/dataset that can accurately differentiate these cases when pulling data, or check each number (01, 02, ...) until a table is found (can still lead to inconsistencies).

### Large differentials in expected and actualy points scored (outliers):
Basketball games, and humans, are prone to run into unforseen circumstances, both positive and negative. This predictor may be way off on some instances, but that doesn't mean it's wrong or broken. Things such as player injuries, games going to overtime, or changes in coaching strategy are all factors that can play into a player's score shooting way up or down. This is not reflected in the predictor. This is a measurment of how much they may score against this defense given their usual tendencies in the past.
