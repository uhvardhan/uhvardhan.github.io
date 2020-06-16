# Premier League Data Analysis - 2018-19


```python
# conventional way to import pandas
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score, mean_squared_error

%matplotlib inline

#pd.set_option('display.max_columns', 100)
#pd.set_option('display.max_rows', 500)
```


```python
# Read the dataset of Premier League match results for the season 2018-2019 and store the results in a DataFrame
print("Reading the dataset........")
football_data = pd.read_csv('../data/EPL18_19.csv')
print("Dataset is ready!")
```

    Reading the dataset........
    Dataset is ready!



```python
# Let's first examine the first 5 rows
print("The first five rows of the dataset - ")
football_data.head()
```

    The first five rows of the dataset -





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Div</th>
      <th>Date</th>
      <th>HomeTeam</th>
      <th>AwayTeam</th>
      <th>FTHG</th>
      <th>FTAG</th>
      <th>FTR</th>
      <th>HTHG</th>
      <th>HTAG</th>
      <th>HTR</th>
      <th>...</th>
      <th>BbAv&lt;2.5</th>
      <th>BbAH</th>
      <th>BbAHh</th>
      <th>BbMxAHH</th>
      <th>BbAvAHH</th>
      <th>BbMxAHA</th>
      <th>BbAvAHA</th>
      <th>PSCH</th>
      <th>PSCD</th>
      <th>PSCA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>E0</td>
      <td>10/08/2018</td>
      <td>Man United</td>
      <td>Leicester</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>1</td>
      <td>0</td>
      <td>H</td>
      <td>...</td>
      <td>1.79</td>
      <td>17</td>
      <td>-0.75</td>
      <td>1.75</td>
      <td>1.70</td>
      <td>2.29</td>
      <td>2.21</td>
      <td>1.55</td>
      <td>4.07</td>
      <td>7.69</td>
    </tr>
    <tr>
      <th>1</th>
      <td>E0</td>
      <td>11/08/2018</td>
      <td>Bournemouth</td>
      <td>Cardiff</td>
      <td>2</td>
      <td>0</td>
      <td>H</td>
      <td>1</td>
      <td>0</td>
      <td>H</td>
      <td>...</td>
      <td>1.83</td>
      <td>20</td>
      <td>-0.75</td>
      <td>2.20</td>
      <td>2.13</td>
      <td>1.80</td>
      <td>1.75</td>
      <td>1.88</td>
      <td>3.61</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>E0</td>
      <td>11/08/2018</td>
      <td>Fulham</td>
      <td>Crystal Palace</td>
      <td>0</td>
      <td>2</td>
      <td>A</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>...</td>
      <td>1.87</td>
      <td>22</td>
      <td>-0.25</td>
      <td>2.18</td>
      <td>2.11</td>
      <td>1.81</td>
      <td>1.77</td>
      <td>2.62</td>
      <td>3.38</td>
      <td>2.90</td>
    </tr>
    <tr>
      <th>3</th>
      <td>E0</td>
      <td>11/08/2018</td>
      <td>Huddersfield</td>
      <td>Chelsea</td>
      <td>0</td>
      <td>3</td>
      <td>A</td>
      <td>0</td>
      <td>2</td>
      <td>A</td>
      <td>...</td>
      <td>1.84</td>
      <td>23</td>
      <td>1.00</td>
      <td>1.84</td>
      <td>1.80</td>
      <td>2.13</td>
      <td>2.06</td>
      <td>7.24</td>
      <td>3.95</td>
      <td>1.58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E0</td>
      <td>11/08/2018</td>
      <td>Newcastle</td>
      <td>Tottenham</td>
      <td>1</td>
      <td>2</td>
      <td>A</td>
      <td>1</td>
      <td>2</td>
      <td>A</td>
      <td>...</td>
      <td>1.81</td>
      <td>20</td>
      <td>0.25</td>
      <td>2.20</td>
      <td>2.12</td>
      <td>1.80</td>
      <td>1.76</td>
      <td>4.74</td>
      <td>3.53</td>
      <td>1.89</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 62 columns</p>
</div>




```python
# Number of rows and columns
print("The number of rows in the dataset - {}.\nThe number of columns in the dataset - {}."
      .format(football_data.shape[0], football_data.shape[1]))
```

    The number of rows in the dataset - 380.
    The number of columns in the dataset - 62.



```python
# Data Type of each column
print("The data types in the dataset are:\n{}".format(football_data.dtypes))
```

    The data types in the dataset are:
    Div          object
    Date         object
    HomeTeam     object
    AwayTeam     object
    FTHG          int64
                 ...   
    BbMxAHA     float64
    BbAvAHA     float64
    PSCH        float64
    PSCD        float64
    PSCA        float64
    Length: 62, dtype: object



```python
# Get all the columns of the dataset
football_data.columns
```




    Index(['Div', 'Date', 'HomeTeam', 'AwayTeam', 'FTHG', 'FTAG', 'FTR', 'HTHG',
           'HTAG', 'HTR', 'Referee', 'HS', 'AS', 'HST', 'AST', 'HF', 'AF', 'HC',
           'AC', 'HY', 'AY', 'HR', 'AR', 'B365H', 'B365D', 'B365A', 'BWH', 'BWD',
           'BWA', 'IWH', 'IWD', 'IWA', 'PSH', 'PSD', 'PSA', 'WHH', 'WHD', 'WHA',
           'VCH', 'VCD', 'VCA', 'Bb1X2', 'BbMxH', 'BbAvH', 'BbMxD', 'BbAvD',
           'BbMxA', 'BbAvA', 'BbOU', 'BbMx>2.5', 'BbAv>2.5', 'BbMx<2.5',
           'BbAv<2.5', 'BbAH', 'BbAHh', 'BbMxAHH', 'BbAvAHH', 'BbMxAHA', 'BbAvAHA',
           'PSCH', 'PSCD', 'PSCA'],
          dtype='object')




```python
# Too much unnecessary data! Let's remove them!
# Selecting only the required dataset
football_data = football_data.loc[:,'Div':'AR']
print("The first five rows of the new dataset - \n{}".format(football_data.head()))
```

    The first five rows of the new dataset -
      Div        Date      HomeTeam        AwayTeam  FTHG  FTAG FTR  HTHG  HTAG  \
    0  E0  10/08/2018    Man United       Leicester     2     1   H     1     0   
    1  E0  11/08/2018   Bournemouth         Cardiff     2     0   H     1     0   
    2  E0  11/08/2018        Fulham  Crystal Palace     0     2   A     0     1   
    3  E0  11/08/2018  Huddersfield         Chelsea     0     3   A     0     2   
    4  E0  11/08/2018     Newcastle       Tottenham     1     2   A     1     2   

      HTR  ... HST  AST  HF  AF  HC  AC  HY  AY  HR  AR  
    0   H  ...   6    4  11   8   2   5   2   1   0   0  
    1   H  ...   4    1  11   9   7   4   1   1   0   0  
    2   A  ...   6    9   9  11   5   5   1   2   0   0  
    3   A  ...   1    4   9   8   2   5   2   1   0   0  
    4   A  ...   2    5  11  12   3   5   2   2   0   0  

    [5 rows x 23 columns]



```python
# Add 4 new colums -
# Create 'FullTimeResult' dummy variable using the 'map' method
football_data['FullTimeResult'] = football_data['FTR'].map({'H':2, 'A':0, 'D':1})
# Create 'HalfTimeResult' dummy variable using the 'map' method
football_data['HalfTimeResult'] = football_data['HTR'].map({'H':2, 'A':0, 'D':1})

# New columns which is the sum of (Home + Away)Yellow Cards and (Home + Away)Red Cards in each match
football_data['TY'] = football_data['HY'] + football_data['AY']
football_data['TR'] = football_data['HR'] + football_data['AR']
```


```python
# Total Number of Goals scored by the HOME Team
home_goals = football_data['FTHG'].sum()
print("The total number of goals scored by the HOME team is - {}".format(home_goals))
```

    The total number of goals scored by the HOME team is - 596



```python
# Total Number of Goals scored by the AWAY Team
away_goals = football_data['FTAG'].sum()
print("The total number of goals scored by the AWAY team is - {}".format(away_goals))
```

    The total number of goals scored by the AWAY team is - 476



```python
# Total Number of Goals scored.
sum_goals = home_goals + away_goals
print("The total number of goals scored in the whole season is - {}".format(sum_goals))
```

    The total number of goals scored in the whole season is - 1072



```python
print('The percentage of goals scored by the Home team during the whole season - {}%.'
      .format((home_goals/sum_goals)*100))
print('The percentage of goals scored by the Away team during the whole season - {}%.'
      .format((away_goals/sum_goals)*100))

# Plotting
fig1,ax1 = plt.subplots()
ax1.pie([home_goals, away_goals], labels=['Home Goals', 'Away Goals'], autopct='%1.1f%%')
ax1.axis('equal')
ax1.set_title('Percentage of goals scored by the Home Team and Away Team:')
plt.show()
```

    The percentage of goals scored by the Home team during the whole season - 55.59701492537313%.
    The percentage of goals scored by the Away team during the whole season - 44.40298507462687%.



![png](../assests/img/FootballAnalysis_files/FootballAnalysis_12_1.png)



```python
# Number of HOME Team Wins, Away Team Wins and Draws in the whole season
results = football_data['FTR'].value_counts()
print("The number of HOME Team Wins - {}\nThe Number of AWAY Team Wins - {}\nThe number of DRAWS - {}"
     .format(results[0], results[1], results[2]))
```

    The number of HOME Team Wins - 181
    The Number of AWAY Team Wins - 128
    The number of DRAWS - 71



```python
results.plot.pie(labels=['Home Team Wins', 'Away Team Wins', 'Draws'],
                                             colors=['r', 'g', 'b'],
                                             autopct='%.2f', fontsize=12, figsize=(6, 6));
```


![png](../assests/img/FootballAnalysis_files/FootballAnalysis_14_0.png)



```python
# The Average Number of Goals scored by the HOME Team
# FTHG = Full Time Home Team Goals
mean_home = football_data['FTHG'].mean()
print("The average number of goals scored by the HOME Team - {}".format(mean_home))
```

    The average number of goals scored by the HOME Team - 1.568421052631579



```python
# The Average Number of Goals scored by the AWAY Team
# FTAG = Full Time Away Team Goals
mean_away = football_data['FTAG'].mean()
print("The average number of goals scored by the AWAY Team - {}".format(mean_away))
```

    The average number of goals scored by the AWAY Team - 1.2526315789473683



```python
# The Average Number of Goals scored by the HOME Team at HALF Time
# HTHG = Half Time Home Team Goals
print("The average number of goals scored by the HOME Team at Half Time - {}"
      .format(football_data['HTHG'].mean()))
```

    The average number of goals scored by the HOME Team at Half Time - 0.6789473684210526



```python
# The Average Number of Goals scored by the AWAY Team at HALF Time
# HTAG = Half Time Away Team Goals
print("The average number of goals scored by the AWAY Team at Half Time - {}"
      .format(football_data['HTAG'].mean()))
```

    The average number of goals scored by the AWAY Team at Half Time - 0.5736842105263158



```python
# The Average Number of Shots by the HOME Team
# HS = Home Team Shots
print("The average number of shots by the HOME Team - {}".format(football_data['HS'].mean()))
```

    The average number of shots by the HOME Team - 14.134210526315789



```python
# The Average Number of Shots by the AWAY Team
# AS = Away Team Shots
print("The average number of shots by the AWAY Team - {}".format(football_data['AS'].mean()))
```

    The average number of shots by the AWAY Team - 11.144736842105264



```python
# The Average Number of Shots on Target by the HOME Team
# HST = Home Team Shots on Target
print("The average number of shots on target by the HOME Team - {}".format(football_data['HST'].mean()))
```

    The average number of shots on target by the HOME Team - 4.778947368421052



```python
# The Average Number of Shots on Target by the AWAY Team
# AST = Away Team Shots on Target
print("The average number of shots on target by the AWAY Team - {}".format(football_data['AST'].mean()))
```

    The average number of shots on target by the AWAY Team - 3.9289473684210527



```python
# The Average Number of Fouls committed by the HOME Team
# HF = Home Team Fouls
print("The average number of fouls conceded by the HOME Team - {}".format(football_data['HF'].mean()))
```

    The average number of fouls conceded by the HOME Team - 10.152631578947368



```python
# The Average Number of Fouls committed by the AWAY Team
# AF = AWAY Team Fouls
print("The average number of fouls conceded by the AWAY Team - {}".format(football_data['AF'].mean()))
```

    The average number of fouls conceded by the AWAY Team - 10.305263157894737



```python
# The Average Number of Corners for the HOME Team
# HC = Home Team Corners
print("The average number of Corners for the HOME Team - {}".format(football_data['HC'].mean()))
```

    The average number of Corners for the HOME Team - 5.705263157894737



```python
# The Average Number of Corners for the AWAY Team
# AC = Away Team Corners
print("The average number of Corners for the AWAY Team - {}".format(football_data['AC'].mean()))
```

    The average number of Corners for the AWAY Team - 4.552631578947368



```python
# The Average Number of Yellow Cards for the HOME Team
# HY = Home Team Yellow Cards
print("The average number of Yellow Cards for the HOME Team - {}".format(football_data['HY'].mean()))
```

    The average number of Yellow Cards for the HOME Team - 1.5263157894736843



```python
# The Average Number of Yellow Cards for the AWAY Team
# AY = AWAY Team Yellow Cards
print("The average number of Yellow Cards for the AWAY Team - {}".format(football_data['AY'].mean()))
```

    The average number of Yellow Cards for the AWAY Team - 1.6842105263157894



```python
# The Average Number of RED Cards for the HOME Team
# HY = Home Team Yellow Cards
print("The average number of RED Cards for the HOME Team - {}".format(football_data['HR'].mean()))
```

    The average number of RED Cards for the HOME Team - 0.04736842105263158



```python
# The Average Number of RED Cards for the AWAY Team
# AY = AWAY Team Yellow Cards
print("The average number of RED Cards for the AWAY Team - {}".format(football_data['AR'].mean()))
```

    The average number of RED Cards for the AWAY Team - 0.07631578947368421



```python
# Names of referees
num_ref = football_data['Referee'].nunique()
ref_names = list(football_data['Referee'].unique())
print("There were {} different referees in the 2018-2019 season.\nNames of Referees - ".format(num_ref))
for name in ref_names:
    print(name)
```

    There were 18 different referees in the 2018-2019 season.
    Names of Referees -
    A Marriner
    K Friend
    M Dean
    C Kavanagh
    M Atkinson
    J Moss
    C Pawson
    M Oliver
    A Taylor
    G Scott
    L Mason
    S Attwell
    P Tierney
    L Probert
    D Coote
    R East
    S Hooper
    A Madley



```python
# Plotting
for index, avg in football_data['Referee'].value_counts().iteritems():
    print("The number of games officiated by {} - {}".format(index, avg))

football_data["Referee"].value_counts().plot(kind='bar');
```

    The number of games officiated by A Taylor - 32
    The number of games officiated by M Oliver - 30
    The number of games officiated by M Atkinson - 29
    The number of games officiated by M Dean - 29
    The number of games officiated by A Marriner - 27
    The number of games officiated by K Friend - 27
    The number of games officiated by J Moss - 27
    The number of games officiated by C Pawson - 26
    The number of games officiated by C Kavanagh - 24
    The number of games officiated by P Tierney - 24
    The number of games officiated by S Attwell - 20
    The number of games officiated by L Mason - 19
    The number of games officiated by L Probert - 18
    The number of games officiated by G Scott - 17
    The number of games officiated by D Coote - 11
    The number of games officiated by R East - 10
    The number of games officiated by S Hooper - 8
    The number of games officiated by A Madley - 2



![png](../assests/img/FootballAnalysis_files/FootballAnalysis_32_1.png)



```python
# Average number of Yellow Cards given by each of the referees
for index, avg in football_data.groupby('Referee').TY.mean().sort_values().iteritems():
    print("On average, {} gives out the {} yellow cards per match.".format(index, avg))
```

    On average, A Madley gives out the 1.0 yellow cards per match.
    On average, G Scott gives out the 2.235294117647059 yellow cards per match.
    On average, S Hooper gives out the 2.5 yellow cards per match.
    On average, L Probert gives out the 2.5555555555555554 yellow cards per match.
    On average, A Marriner gives out the 2.7037037037037037 yellow cards per match.
    On average, M Oliver gives out the 2.7666666666666666 yellow cards per match.
    On average, C Kavanagh gives out the 3.0833333333333335 yellow cards per match.
    On average, M Atkinson gives out the 3.1379310344827585 yellow cards per match.
    On average, S Attwell gives out the 3.15 yellow cards per match.
    On average, D Coote gives out the 3.1818181818181817 yellow cards per match.
    On average, A Taylor gives out the 3.1875 yellow cards per match.
    On average, L Mason gives out the 3.3157894736842106 yellow cards per match.
    On average, K Friend gives out the 3.4074074074074074 yellow cards per match.
    On average, P Tierney gives out the 3.4166666666666665 yellow cards per match.
    On average, J Moss gives out the 3.4444444444444446 yellow cards per match.
    On average, C Pawson gives out the 3.5384615384615383 yellow cards per match.
    On average, M Dean gives out the 4.379310344827586 yellow cards per match.
    On average, R East gives out the 4.4 yellow cards per match.



```python
# Average number of Red Cards given by each of the referees
for index, avg in football_data.groupby('Referee').TR.mean().sort_values().iteritems():
    print("On average, {} gives out the {} red cards per match.".format(index, avg))
```

    On average, A Madley gives out the 0.0 red cards per match.
    On average, R East gives out the 0.0 red cards per match.
    On average, D Coote gives out the 0.0 red cards per match.
    On average, S Hooper gives out the 0.0 red cards per match.
    On average, A Taylor gives out the 0.03125 red cards per match.
    On average, M Atkinson gives out the 0.034482758620689655 red cards per match.
    On average, P Tierney gives out the 0.041666666666666664 red cards per match.
    On average, S Attwell gives out the 0.05 red cards per match.
    On average, L Mason gives out the 0.05263157894736842 red cards per match.
    On average, G Scott gives out the 0.058823529411764705 red cards per match.
    On average, C Kavanagh gives out the 0.08333333333333333 red cards per match.
    On average, A Marriner gives out the 0.1111111111111111 red cards per match.
    On average, K Friend gives out the 0.1111111111111111 red cards per match.
    On average, J Moss gives out the 0.18518518518518517 red cards per match.
    On average, L Probert gives out the 0.2222222222222222 red cards per match.
    On average, M Oliver gives out the 0.23333333333333334 red cards per match.
    On average, C Pawson gives out the 0.2692307692307692 red cards per match.
    On average, M Dean gives out the 0.3448275862068966 red cards per match.



```python
plt.rcParams["figure.figsize"]=20,20
sns.heatmap(football_data.corr(), annot=True, fmt = ".2f");
```


![png](../assests/img/FootballAnalysis_files/FootballAnalysis_35_0.png)



```python
# Get Respective Points for the season
# Steps:
```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```


```python

```
