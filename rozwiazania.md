#%% md
# Exercise 1. - Getting and Knowing your Data
#%% md
This time we are going to pull data directly from the internet.
Special thanks to: https://github.com/justmarkham for sharing the dataset and materials.

Check out [Occupation Exercises Video Tutorial](https://www.youtube.com/watch?v=W8AB5s-L3Rw&list=PLgJhDSE2ZLxaY_DigHeiIDC1cD09rXgJv&index=4) to watch a data scientist go through the exercises

### Step 1. Import the necessary libraries
#%%
import pandas as pd
import numpy as np

#%% md
### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/justmarkham/DAT8/master/data/u.user). 
#%% md
### Step 3. Assign it to a variable called users and use the 'user_id' as index
#%%
plik = pd.read_csv('https://raw.githubusercontent.com/justmarkham/DAT8/master/data/u.user')
users = pd.read_csv('https://raw.githubusercontent.com/justmarkham/DAT8/master/data/u.user', sep='|', index_col='user_id')
#%% md
### Step 4. See the first 25 entries
#%%
users.head(25)
#%% md
### Step 5. See the last 10 entries
#%%
users.tail(10)
#%% md
### Step 6. What is the number of observations in the dataset?
#%%
len(users)
#%% md
### Step 7. What is the number of columns in the dataset?
#%%
users.shape[0]
#%% md
### Step 8. Print the name of all the columns.
#%%
users.columns
#%% md
### Step 9. How is the dataset indexed?
#%%
users.index
#%% md
### Step 10. What is the data type of each column?
#%%
users.dtypes
#%% md
### Step 11. Print only the occupation column
#%%
users.occupation
#%% md
### Step 12. How many different occupations are in this dataset?
#%%
len(users.occupation.unique())
#%% md
### Step 13. What is the most frequent occupation?
#%%
users.occupation.value_counts()
#%% md
### Step 14. Summarize the DataFrame.
#%%
users.describe()
#%% md
### Step 15. Summarize all the columns
#%%
users.describe(include='all')
#%% md
### Step 16. Summarize only the occupation column
#%%
users.occupation.describe()
#%% md
### Step 17. What is the mean age of users?
#%%
users.age.mean()
#%%

#%% md
### Step 18. What is the age with least occurrence?
#%%

users.age.value_counts().tail()



#%% md
# Exercise 2. - Filtering and Sorting Data

Check out [Euro 12 Exercises Video Tutorial](https://youtu.be/iqk5d48Qisg) to watch a data scientist go through the exercises
#%% md
This time we are going to pull data directly from the internet.

### Step 1. Import the necessary libraries
#%%
import pandas as pd
import numpy as np
from pandas import read_csv
#%% md
### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/kflisikowsky/pandas_exercises/refs/heads/main/Euro_2012_stats_TEAM.csv). 
#%% md
### Step 3. Assign it to a variable called euro12.
#%%
euro12 = read_csv('https://raw.githubusercontent.com/kflisikowsky/pandas_exercises/refs/heads/main/Euro_2012_stats_TEAM.csv')
#%% md
### Step 4. Select only the Goal column.
#%%
euro12.Goals
#%% md
### Step 5. How many team participated in the Euro2012?
#%%
len(euro12.Team.unique())
#%% md
### Step 6. What is the number of columns in the dataset?
#%%
euro12.shape[1]
#%% md
### Step 7. View only the columns Team, Yellow Cards and Red Cards and assign them to a dataframe called discipline
#%%
discipline = euro12[['Team', 'Yellow Cards', 'Red Cards']]
#%% md
### Step 8. Sort the teams by Red Cards, then to Yellow Cards
#%%
discipline.sort_values(['Red Cards', 'Yellow Cards'])
#%% md
### Step 9. Calculate the mean Yellow Cards given per Team
#%%
discipline['Yellow Cards'].mean()
#%% md
### Step 10. Filter teams that scored more than 6 goals
#%%
euro12[euro12.Goals > 6]
#%% md
### Step 11. Select the teams that start with G
#%%
euro12[euro12.Team.str.startswith('G')]
#%% md
### Step 12. Select the first 7 columns
#%%
euro12.iloc[:, 0:7]
#%% md
### Step 13. Select all columns except the last 3.
#%%
euro12.iloc[:, :-3]
#%% md
### Step 14. Present only the Shooting Accuracy from England, Italy and Russia
#%%
teams_filter = euro12.Team.isin(['England', 'Italy', 'Russia'])
euro12.loc[teams_filter, ['Team', 'Shooting Accuracy']]



#%% md
# Exercise 3. - GroupBy
#%% md
### Introduction:

GroupBy can be summarized as Split-Apply-Combine.

Special thanks to: https://github.com/justmarkham for sharing the dataset and materials.

Check out this [Diagram](http://i.imgur.com/yjNkiwL.png)  

Check out [Alcohol Consumption Exercises Video Tutorial](https://youtu.be/az67CMdmS6s) to watch a data scientist go through the exercises


### Step 1. Import the necessary libraries
#%%
import numpy as np
import pandas as pd
#%% md
### Step 2. Import the dataset from this [address](https://raw.githubusercontent.com/justmarkham/DAT8/master/data/drinks.csv). 
#%% md
### Step 3. Assign it to a variable called drinks.
#%%
drinks = pd.read_csv('https://raw.githubusercontent.com/justmarkham/DAT8/master/data/drinks.csv')
#%% md
### Step 4. Which continent drinks more beer on average?
#%%
drinks.groupby('continent').beer_servings.mean().sort_values(ascending=False).head(1)
#%% md
### Step 5. For each continent print the statistics for wine consumption.
#%%
drinks.groupby('continent').wine_servings.describe()
#%% md
### Step 6. Print the mean alcohol consumption per continent for every column
#%%
drinks.groupby('continent').wine_servings.mean()
#%% md
### Step 7. Print the median alcohol consumption per continent for every column
#%%
drinks.groupby('continent').wine_servings.median()
#%% md
### Step 8. Print the mean, min and max values for spirit consumption.
#### This time output a DataFrame
#%%
wynik = drinks.groupby('continent').spirit_servings.describe()
wynik[['mean', 'min', 'max']]
