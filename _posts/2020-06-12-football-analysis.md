---
layout: post
title: Premier League Data Analysis - 2018-19
subtitle: English Premier League Data Analysis
categories: Data Analysis
---



```python
# conventional way to import pandas
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline

pd.set_option('display.max_columns', 100)
pd.set_option('display.max_rows', 500)
```


```python
# Read the dataset of Premier League match results for the season 2018-2019 and store the results in a DataFrame
football_data = pd.read_csv('../data/EPL18_19.csv')
```


```python
# Let's first examine the first 5 rows
print("The first five rows of the dataset: ")
football_data.head()
```

    The first five rows of the dataset:





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
      <th>Referee</th>
      <th>HS</th>
      <th>AS</th>
      <th>HST</th>
      <th>AST</th>
      <th>HF</th>
      <th>AF</th>
      <th>HC</th>
      <th>AC</th>
      <th>HY</th>
      <th>AY</th>
      <th>HR</th>
      <th>AR</th>
      <th>B365H</th>
      <th>B365D</th>
      <th>B365A</th>
      <th>BWH</th>
      <th>BWD</th>
      <th>BWA</th>
      <th>IWH</th>
      <th>IWD</th>
      <th>IWA</th>
      <th>PSH</th>
      <th>PSD</th>
      <th>PSA</th>
      <th>WHH</th>
      <th>WHD</th>
      <th>WHA</th>
      <th>VCH</th>
      <th>VCD</th>
      <th>VCA</th>
      <th>Bb1X2</th>
      <th>BbMxH</th>
      <th>BbAvH</th>
      <th>BbMxD</th>
      <th>BbAvD</th>
      <th>BbMxA</th>
      <th>BbAvA</th>
      <th>BbOU</th>
      <th>BbMx&gt;2.5</th>
      <th>BbAv&gt;2.5</th>
      <th>BbMx&lt;2.5</th>
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
      <td>A Marriner</td>
      <td>8</td>
      <td>13</td>
      <td>6</td>
      <td>4</td>
      <td>11</td>
      <td>8</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1.57</td>
      <td>3.9</td>
      <td>7.50</td>
      <td>1.53</td>
      <td>4.0</td>
      <td>7.50</td>
      <td>1.55</td>
      <td>3.80</td>
      <td>7.00</td>
      <td>1.58</td>
      <td>3.93</td>
      <td>7.50</td>
      <td>1.57</td>
      <td>3.8</td>
      <td>6.00</td>
      <td>1.57</td>
      <td>4.0</td>
      <td>7.00</td>
      <td>39</td>
      <td>1.60</td>
      <td>1.56</td>
      <td>4.20</td>
      <td>3.92</td>
      <td>8.05</td>
      <td>7.06</td>
      <td>38</td>
      <td>2.12</td>
      <td>2.03</td>
      <td>1.85</td>
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
      <td>K Friend</td>
      <td>12</td>
      <td>10</td>
      <td>4</td>
      <td>1</td>
      <td>11</td>
      <td>9</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1.90</td>
      <td>3.6</td>
      <td>4.50</td>
      <td>1.90</td>
      <td>3.4</td>
      <td>4.40</td>
      <td>1.90</td>
      <td>3.50</td>
      <td>4.10</td>
      <td>1.89</td>
      <td>3.63</td>
      <td>4.58</td>
      <td>1.91</td>
      <td>3.5</td>
      <td>4.00</td>
      <td>1.87</td>
      <td>3.6</td>
      <td>4.75</td>
      <td>39</td>
      <td>1.93</td>
      <td>1.88</td>
      <td>3.71</td>
      <td>3.53</td>
      <td>4.75</td>
      <td>4.37</td>
      <td>38</td>
      <td>2.05</td>
      <td>1.98</td>
      <td>1.92</td>
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
      <td>M Dean</td>
      <td>15</td>
      <td>10</td>
      <td>6</td>
      <td>9</td>
      <td>9</td>
      <td>11</td>
      <td>5</td>
      <td>5</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>2.50</td>
      <td>3.4</td>
      <td>3.00</td>
      <td>2.45</td>
      <td>3.3</td>
      <td>2.95</td>
      <td>2.40</td>
      <td>3.30</td>
      <td>2.95</td>
      <td>2.50</td>
      <td>3.46</td>
      <td>3.00</td>
      <td>2.45</td>
      <td>3.3</td>
      <td>2.80</td>
      <td>2.50</td>
      <td>3.4</td>
      <td>3.00</td>
      <td>39</td>
      <td>2.60</td>
      <td>2.47</td>
      <td>3.49</td>
      <td>3.35</td>
      <td>3.05</td>
      <td>2.92</td>
      <td>38</td>
      <td>2.00</td>
      <td>1.95</td>
      <td>1.96</td>
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
      <td>C Kavanagh</td>
      <td>6</td>
      <td>13</td>
      <td>1</td>
      <td>4</td>
      <td>9</td>
      <td>8</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>6.50</td>
      <td>4.0</td>
      <td>1.61</td>
      <td>6.25</td>
      <td>3.9</td>
      <td>1.57</td>
      <td>6.20</td>
      <td>4.00</td>
      <td>1.55</td>
      <td>6.41</td>
      <td>4.02</td>
      <td>1.62</td>
      <td>5.80</td>
      <td>3.9</td>
      <td>1.57</td>
      <td>6.50</td>
      <td>4.0</td>
      <td>1.62</td>
      <td>38</td>
      <td>6.85</td>
      <td>6.09</td>
      <td>4.07</td>
      <td>3.90</td>
      <td>1.66</td>
      <td>1.61</td>
      <td>37</td>
      <td>2.05</td>
      <td>1.98</td>
      <td>1.90</td>
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
      <td>M Atkinson</td>
      <td>15</td>
      <td>15</td>
      <td>2</td>
      <td>5</td>
      <td>11</td>
      <td>12</td>
      <td>3</td>
      <td>5</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>3.90</td>
      <td>3.5</td>
      <td>2.04</td>
      <td>3.80</td>
      <td>3.5</td>
      <td>2.00</td>
      <td>3.70</td>
      <td>3.35</td>
      <td>2.05</td>
      <td>3.83</td>
      <td>3.57</td>
      <td>2.08</td>
      <td>3.80</td>
      <td>3.2</td>
      <td>2.05</td>
      <td>3.90</td>
      <td>3.4</td>
      <td>2.10</td>
      <td>39</td>
      <td>4.01</td>
      <td>3.83</td>
      <td>3.57</td>
      <td>3.40</td>
      <td>2.12</td>
      <td>2.05</td>
      <td>38</td>
      <td>2.10</td>
      <td>2.01</td>
      <td>1.88</td>
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
</div>




```python
# Number of rows and columns
print("The number of rows in the dataset are {}.\nThe number of columns in the dataset are {}."
      .format(football_data.shape[0], football_data.shape[1]))
```

    The number of rows in the dataset are 380.
    The number of columns in the dataset are 62.



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
    FTAG          int64
    FTR          object
    HTHG          int64
    HTAG          int64
    HTR          object
    Referee      object
    HS            int64
    AS            int64
    HST           int64
    AST           int64
    HF            int64
    AF            int64
    HC            int64
    AC            int64
    HY            int64
    AY            int64
    HR            int64
    AR            int64
    B365H       float64
    B365D       float64
    B365A       float64
    BWH         float64
    BWD         float64
    BWA         float64
    IWH         float64
    IWD         float64
    IWA         float64
    PSH         float64
    PSD         float64
    PSA         float64
    WHH         float64
    WHD         float64
    WHA         float64
    VCH         float64
    VCD         float64
    VCA         float64
    Bb1X2         int64
    BbMxH       float64
    BbAvH       float64
    BbMxD       float64
    BbAvD       float64
    BbMxA       float64
    BbAvA       float64
    BbOU          int64
    BbMx>2.5    float64
    BbAv>2.5    float64
    BbMx<2.5    float64
    BbAv<2.5    float64
    BbAH          int64
    BbAHh       float64
    BbMxAHH     float64
    BbAvAHH     float64
    BbMxAHA     float64
    BbAvAHA     float64
    PSCH        float64
    PSCD        float64
    PSCA        float64
    dtype: object



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



I am only concerned with few columns. Removing all the unnecesaary columns:


```python
# Selecting only the required dataset
football_data = football_data.loc[:,'Div':'AR']
print("The first five rows of the new dataset:\n{}".format(football_data.head()))
```

    The first five rows of the new dataset:
      Div        Date      HomeTeam        AwayTeam  FTHG  FTAG FTR  HTHG  HTAG  \
    0  E0  10/08/2018    Man United       Leicester     2     1   H     1     0   
    1  E0  11/08/2018   Bournemouth         Cardiff     2     0   H     1     0   
    2  E0  11/08/2018        Fulham  Crystal Palace     0     2   A     0     1   
    3  E0  11/08/2018  Huddersfield         Chelsea     0     3   A     0     2   
    4  E0  11/08/2018     Newcastle       Tottenham     1     2   A     1     2   

      HTR     Referee  HS  AS  HST  AST  HF  AF  HC  AC  HY  AY  HR  AR  
    0   H  A Marriner   8  13    6    4  11   8   2   5   2   1   0   0  
    1   H    K Friend  12  10    4    1  11   9   7   4   1   1   0   0  
    2   A      M Dean  15  10    6    9   9  11   5   5   1   2   0   0  
    3   A  C Kavanagh   6  13    1    4   9   8   2   5   2   1   0   0  
    4   A  M Atkinson  15  15    2    5  11  12   3   5   2   2   0   0  


Terms for each column:

Div = League Division

Date = Match Date (dd/mm/yy)

HomeTeam = Home Team

AwayTeam = Away Team

FTHG = Full Time Home Team Goals

FTAG = Full Time Away Team Goals

FTR = Full Time Result (H=Home Win, D=Draw, A=Away Win)

HTHG = Half Time Home Team Goals

HTAG = Half Time Away Team Goals

HTR = Half Time Result (H=Home Win, D=Draw, A=Away Win)

Referee = Match Referee

HS = Home Team Shots

AS = Away Team Shots

HST = Home Team Shots on Target

AST = Away Team Shots on Target

HF = Home Team Fouls Committed

AF = Away Team Fouls Committed

HC = Home Team Corners

AC = Away Team Corners

HY = Home Team Yellow Cards

AY = Away Team Yellow Cards

HR = Home Team Red Cards

AR = Away Team Red Cards


```python
# Total Number of Goals scored by the HOME Team
home_goals = football_data['FTHG'].sum()
print("The total number of goals scored by the HOME team is: {}".format(home_goals))
```

    The total number of goals scored by the HOME team is: 596



```python
# Total Number of Goals scored by the AWAY Team
away_goals = football_data['FTAG'].sum()
print("The total number of goals scored by the AWAY team is: {}".format(away_goals))
```

    The total number of goals scored by the AWAY team is: 476



```python
# Total Number of Goals scored.
sum_goals = home_goals + away_goals
print("The total number of goals scored in the whole season is: {}".format(sum_goals))
```

    The total number of goals scored in the whole season is: 1072



```python
print('The percentage of goals scored by the Home team during the whole season is {}.'
      .format((home_goals/sum_goals)*100))
print('The percentage of goals scored by the Away team during the whole season is {}.'
      .format((away_goals/sum_goals)*100))

# Plotting
fig1,ax1 = plt.subplots()
ax1.pie([home_goals, away_goals], labels=['Home Goals', 'Away Goals'], autopct='%1.1f%%')
ax1.axis('equal')
ax1.set_title('Percentage of goals scored by the Home Team and Away Team:')
plt.show()
```

    The percentage of goals scored by the Home team during the whole season is 55.59701492537313.
    The percentage of goals scored by the Away team during the whole season is 44.40298507462687.



![png](../assests/img/football_analysis_files/football_analysis_13_1.png)



```python
# Number of HOME Team Wins, Away Team Wins and Draws in the whole season
results = football_data['FTR'].value_counts()
print("The number of HOME Team Wins: {}\nThe Number of AWAY Team Wins: {}\nThe number of DRAWS: {}"
     .format(results[0], results[1], results[2]))
```

    The number of HOME Team Wins: 181
    The Number of AWAY Team Wins: 128
    The number of DRAWS: 71



```python
results.plot.pie(labels=['Home Team Wins', 'Away Team Wins', 'Draws'],
                                             colors=['r', 'g', 'b'],
                                             autopct='%.2f', fontsize=12, figsize=(6, 6));
```


![png](../assests/img/football_analysis_files/football_analysis_15_0.png)



```python
# The Average Number of Goals scored by the HOME Team
# FTHG = Full Time Home Team Goals
mean_home = football_data['FTHG'].mean()
print("The average number of goals scored by the HOME Team - {}".format(mean_home))
```

    The average number of goals scored by the HOME Team: 1.568421052631579



```python
# The Average Number of Goals scored by the AWAY Team
# FTAG = Full Time Away Team Goals
mean_away = football_data['FTAG'].mean()
print("The average number of goals scored by the AWAY Team - {}".format(mean_away))
```

    The average number of goals scored by the AWAY Team: 1.2526315789473683



```python
# The Average Number of Goals scored by the HOME Team at HALF Time
# HTHG = Half Time Home Team Goals
print("The average number of goals scored by the HOME Team at Half Time - {}"
      .format(football_data['HTHG'].mean()))
```

    The average number of goals scored by the HOME Team at Half Time is 0.6789473684210526



```python
# The Average Number of Goals scored by the AWAY Team at HALF Time
# HTAG = Half Time Away Team Goals
print("The average number of goals scored by the AWAY Team at Half Time - {}"
      .format(football_data['HTAG'].mean()))
```

    The average number of goals scored by the AWAY Team at Half Time is 0.5736842105263158



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
football_data.head()
```




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
      <th>Referee</th>
      <th>HS</th>
      <th>AS</th>
      <th>HST</th>
      <th>AST</th>
      <th>HF</th>
      <th>AF</th>
      <th>HC</th>
      <th>AC</th>
      <th>HY</th>
      <th>AY</th>
      <th>HR</th>
      <th>AR</th>
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
      <td>A Marriner</td>
      <td>8</td>
      <td>13</td>
      <td>6</td>
      <td>4</td>
      <td>11</td>
      <td>8</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
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
      <td>K Friend</td>
      <td>12</td>
      <td>10</td>
      <td>4</td>
      <td>1</td>
      <td>11</td>
      <td>9</td>
      <td>7</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
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
      <td>M Dean</td>
      <td>15</td>
      <td>10</td>
      <td>6</td>
      <td>9</td>
      <td>9</td>
      <td>11</td>
      <td>5</td>
      <td>5</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
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
      <td>C Kavanagh</td>
      <td>6</td>
      <td>13</td>
      <td>1</td>
      <td>4</td>
      <td>9</td>
      <td>8</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
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
      <td>M Atkinson</td>
      <td>15</td>
      <td>15</td>
      <td>2</td>
      <td>5</td>
      <td>11</td>
      <td>12</td>
      <td>3</td>
      <td>5</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




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

    The average number of Corner for the HOME Team - 5.705263157894737



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
# The number of times HOME Team was trailing at HALF Time but WON at Full-Time
(football_data[(football_data['HTR'] == 'A') & (football_data['FTR'] == 'H')])
```




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
      <th>Referee</th>
      <th>HS</th>
      <th>AS</th>
      <th>HST</th>
      <th>AST</th>
      <th>HF</th>
      <th>AF</th>
      <th>HC</th>
      <th>AC</th>
      <th>HY</th>
      <th>AY</th>
      <th>HR</th>
      <th>AR</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>74</th>
      <td>E0</td>
      <td>06/10/2018</td>
      <td>Man United</td>
      <td>Newcastle</td>
      <td>3</td>
      <td>2</td>
      <td>H</td>
      <td>0</td>
      <td>2</td>
      <td>A</td>
      <td>A Taylor</td>
      <td>18</td>
      <td>13</td>
      <td>10</td>
      <td>8</td>
      <td>16</td>
      <td>8</td>
      <td>10</td>
      <td>6</td>
      <td>2</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>130</th>
      <td>E0</td>
      <td>30/11/2018</td>
      <td>Cardiff</td>
      <td>Wolves</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>A Marriner</td>
      <td>17</td>
      <td>15</td>
      <td>3</td>
      <td>4</td>
      <td>3</td>
      <td>12</td>
      <td>7</td>
      <td>6</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>137</th>
      <td>E0</td>
      <td>02/12/2018</td>
      <td>Arsenal</td>
      <td>Tottenham</td>
      <td>4</td>
      <td>2</td>
      <td>H</td>
      <td>1</td>
      <td>2</td>
      <td>A</td>
      <td>M Dean</td>
      <td>22</td>
      <td>11</td>
      <td>7</td>
      <td>6</td>
      <td>15</td>
      <td>17</td>
      <td>8</td>
      <td>5</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>149</th>
      <td>E0</td>
      <td>05/12/2018</td>
      <td>Wolves</td>
      <td>Chelsea</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>J Moss</td>
      <td>6</td>
      <td>17</td>
      <td>2</td>
      <td>3</td>
      <td>18</td>
      <td>10</td>
      <td>1</td>
      <td>5</td>
      <td>4</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>157</th>
      <td>E0</td>
      <td>08/12/2018</td>
      <td>West Ham</td>
      <td>Crystal Palace</td>
      <td>3</td>
      <td>2</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>A Taylor</td>
      <td>13</td>
      <td>8</td>
      <td>6</td>
      <td>4</td>
      <td>10</td>
      <td>8</td>
      <td>5</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>222</th>
      <td>E0</td>
      <td>19/01/2019</td>
      <td>Liverpool</td>
      <td>Crystal Palace</td>
      <td>4</td>
      <td>3</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>J Moss</td>
      <td>19</td>
      <td>9</td>
      <td>9</td>
      <td>3</td>
      <td>6</td>
      <td>8</td>
      <td>8</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>231</th>
      <td>E0</td>
      <td>29/01/2019</td>
      <td>Fulham</td>
      <td>Brighton</td>
      <td>4</td>
      <td>2</td>
      <td>H</td>
      <td>0</td>
      <td>2</td>
      <td>A</td>
      <td>L Probert</td>
      <td>24</td>
      <td>15</td>
      <td>7</td>
      <td>6</td>
      <td>10</td>
      <td>5</td>
      <td>10</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>234</th>
      <td>E0</td>
      <td>29/01/2019</td>
      <td>Newcastle</td>
      <td>Man City</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>P Tierney</td>
      <td>6</td>
      <td>12</td>
      <td>2</td>
      <td>4</td>
      <td>9</td>
      <td>7</td>
      <td>1</td>
      <td>8</td>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>239</th>
      <td>E0</td>
      <td>30/01/2019</td>
      <td>Tottenham</td>
      <td>Watford</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>G Scott</td>
      <td>17</td>
      <td>9</td>
      <td>3</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>9</td>
      <td>5</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>282</th>
      <td>E0</td>
      <td>02/03/2019</td>
      <td>Man United</td>
      <td>Southampton</td>
      <td>3</td>
      <td>2</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>S Attwell</td>
      <td>16</td>
      <td>6</td>
      <td>6</td>
      <td>3</td>
      <td>7</td>
      <td>10</td>
      <td>9</td>
      <td>7</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>294</th>
      <td>E0</td>
      <td>09/03/2019</td>
      <td>Newcastle</td>
      <td>Everton</td>
      <td>3</td>
      <td>2</td>
      <td>H</td>
      <td>0</td>
      <td>2</td>
      <td>A</td>
      <td>L Mason</td>
      <td>19</td>
      <td>7</td>
      <td>7</td>
      <td>3</td>
      <td>13</td>
      <td>10</td>
      <td>8</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>295</th>
      <td>E0</td>
      <td>09/03/2019</td>
      <td>Southampton</td>
      <td>Tottenham</td>
      <td>2</td>
      <td>1</td>
      <td>H</td>
      <td>0</td>
      <td>1</td>
      <td>A</td>
      <td>K Friend</td>
      <td>12</td>
      <td>16</td>
      <td>4</td>
      <td>5</td>
      <td>16</td>
      <td>9</td>
      <td>1</td>
      <td>10</td>
      <td>4</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>301</th>
      <td>E0</td>
      <td>16/03/2019</td>
      <td>West Ham</td>
      <td>Huddersfield</td>
      <td>4</td>
      <td>3</td>
      <td>H</td>
      <td>1</td>
      <td>2</td>
      <td>A</td>
      <td>J Moss</td>
      <td>16</td>
      <td>15</td>
      <td>5</td>
      <td>5</td>
      <td>7</td>
      <td>15</td>
      <td>5</td>
      <td>8</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
football_referees
```




    ['A Marriner',
     'K Friend',
     'M Dean',
     'C Kavanagh',
     'M Atkinson',
     'J Moss',
     'C Pawson',
     'M Oliver',
     'A Taylor',
     'G Scott',
     'L Mason',
     'S Attwell',
     'P Tierney',
     'L Probert',
     'D Coote',
     'R East',
     'S Hooper',
     'A Madley']




```python

```


```python

```


```python

```


```python

```


```python
# Names of referee and the number of games they were judging
football_data['Referee'].value_counts()
```




    A Taylor      32
    M Oliver      30
    M Dean        29
    M Atkinson    29
    J Moss        27
    A Marriner    27
    K Friend      27
    C Pawson      26
    C Kavanagh    24
    P Tierney     24
    S Attwell     20
    L Mason       19
    L Probert     18
    G Scott       17
    D Coote       11
    R East        10
    S Hooper       8
    A Madley       2
    Name: Referee, dtype: int64




```python
# Since, I am only concerned with 'Arsenal' matches, I choose only those games where
# ('HomeTeam' == 'Arsenal') OR ('AwayTeam' == 'Arsenal')
arsenal_data = football_data[(football_data['HomeTeam'] == 'Arsenal') | (football_data['AwayTeam'] == 'Arsenal')]
arsenal_data.head()
```


```python
# Shape of the Arsenal data: Should be 38 for 38 games in a single season.
total_games, total_features = arsenal_data.shape
total_games
```


```python
# Calculate Arsenal summary statistics
arsenal_data.describe()
# This data is pretty useless considering that we don't know who is home and who is away.
# Let's do the analysis for all HOME games for arsenal
```

## Arsenal - HOME Analysis


```python
arsenal_home = arsenal_data[arsenal_data['HomeTeam']=='Arsenal']
arsenal_home.head()
# 19 Home Games per season
```


```python
home_games, total_features = arsenal_home.shape
home_games
```


```python
# The total number of goals scored by Arsenal at HOME
arsenal_home['FTHG'].sum()
```


```python
# The total number of goals conceded by Arsenal at HOME
arsenal_home['FTAG'].sum()
```


```python
# The number of Wins/Losses/Draw for Arsenal at HOME
arsenal_home['FTR'].value_counts()
```


```python
arsenal_home['FTR'].value_counts().plot.pie(labels=['Home Wins', 'Home Losses', 'Draws'],
                                             colors=['r', 'g', 'b'],
                                             autopct='%.2f', fontsize=12, figsize=(6, 6))
```


```python
# The games where Arsenal was trailing at HALF Time but Won the game at FULL Time
arsenal_home[(arsenal_home['HTR'] == 'A') & (arsenal_home['FTR'] == 'H')]
```

NICE!! Against the Arch Rivals!


```python
arsenal_home[(arsenal_home['HTR'] == 'H') & (arsenal_home['FTR'] == 'H')]
```


```python

```
