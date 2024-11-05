# **Introduction**

This is my approach on the Google Data Analytics Capstone – Case Study 2: How Can a Wellness Technology Company Play It Smart?
I have taken the Data Analyst steps:

* Ask
* Prepare
* Process
* Analyze
* Share
* Act

These steps will be outlined in this Notebook.

# **Scenario**

I am a junior data analyst working on the marketing analyst team at Bellabeat, a high-tech manufacturer of health-focused products for women. Bellabeat is a successful small company, but they have the potential to become a larger player in the global smart device market. I have been asked to focus on one of Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices. The insights I discover will then help guide marketing strategy for the company. I will present my analysis to the Bellabeat executive team along with my high-level recommendations for Bellabeat’s marketing strategy.

## **ASK**

This step of the process involves asking SMART (Specific, Measureable, Action-Oriented, Relevant, and Time-bound) questions, as well as, understanding Stakeholder expectiations. The following questions will help achieve that:

**1. What are some trends in smart device usage?**

**2. How could these trends apply to Bellabeat customers?**

**3. How could these trends help influence Bellabeat marketing strategy?**

#### **Guiding Questions**

**1. What is the problem you are trying to solve?**

The problem to be solved is to gain insight into how non-Bellabeat customers use smart devices to find trends that can be used to create high level recommendations for a strategy for the Bellabeat marketing team for Bellabeat products

**2. How can your insights drive business decisions?**

My insights will help Bellabeat achieve more business to grow in their current field and be a force to be reckoned with.

#### **Key Tasks** 

**1. Identify the business task**

To provide high-level recommendations that can be applied to one of Bellabeat’s current products’ marketing strategy by investigating existing smart device trends of non Bellabeat smart devices.

**2. Consider key stakeholders**

**Primary stakeholder:**

Urška Sršen: Bellabeat’s cofounder and Chief Creative Officer

Sando Mur: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team

**Secondary stakeholder:**

Bellabeat marketing analytics team

## **PREPARE**
Here we are importing the data provided into JupyterLab to get prepared to be processed and analyzed.
Data Source Used In This Project can be found [here](https://www.kaggle.com/datasets/arashnic/fitbit?select=Fitabase+Data+4.12.16-5.12.16).

### Setting up my environment
Here I'm setting up my environment by installing and loading pandas and other packages to help me with analysis


```python
#installing the packages needed for analysis
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### Importing dataset
Here I am importing the 'dailyActivity_merged.csv', 'hourlySteps_merged', and 'hourlycalories_merged' dataset into Python from the Fitbit Dataset Archive located [here](https://www.kaggle.com/datasets/arashnic/fitbit?select=Fitabase+Data+4.12.16-5.12.16) I was going to do 'sleepDay' as well, but it turns out it doesn't include all the participants.


```python
#Importing data set
da = pd.read_csv("dailyActivity_merged.csv")
h_step = pd.read_csv("hourlysteps_merged.csv")
h_cal = pd.read_csv("hourlycalories_merged.csv")
sd = pd.read_csv("sleepDay_merged.csv")
```


```python
da.head()
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
      <th>Id</th>
      <th>ActivityDate</th>
      <th>TotalSteps</th>
      <th>TotalDistance</th>
      <th>TrackerDistance</th>
      <th>LoggedActivitiesDistance</th>
      <th>VeryActiveDistance</th>
      <th>ModeratelyActiveDistance</th>
      <th>LightActiveDistance</th>
      <th>SedentaryActiveDistance</th>
      <th>VeryActiveMinutes</th>
      <th>FairlyActiveMinutes</th>
      <th>LightlyActiveMinutes</th>
      <th>SedentaryMinutes</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016</td>
      <td>13162</td>
      <td>8.50</td>
      <td>8.50</td>
      <td>0.0</td>
      <td>1.88</td>
      <td>0.55</td>
      <td>6.06</td>
      <td>0.0</td>
      <td>25</td>
      <td>13</td>
      <td>328</td>
      <td>728</td>
      <td>1985</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/13/2016</td>
      <td>10735</td>
      <td>6.97</td>
      <td>6.97</td>
      <td>0.0</td>
      <td>1.57</td>
      <td>0.69</td>
      <td>4.71</td>
      <td>0.0</td>
      <td>21</td>
      <td>19</td>
      <td>217</td>
      <td>776</td>
      <td>1797</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/14/2016</td>
      <td>10460</td>
      <td>6.74</td>
      <td>6.74</td>
      <td>0.0</td>
      <td>2.44</td>
      <td>0.40</td>
      <td>3.91</td>
      <td>0.0</td>
      <td>30</td>
      <td>11</td>
      <td>181</td>
      <td>1218</td>
      <td>1776</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/15/2016</td>
      <td>9762</td>
      <td>6.28</td>
      <td>6.28</td>
      <td>0.0</td>
      <td>2.14</td>
      <td>1.26</td>
      <td>2.83</td>
      <td>0.0</td>
      <td>29</td>
      <td>34</td>
      <td>209</td>
      <td>726</td>
      <td>1745</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/16/2016</td>
      <td>12669</td>
      <td>8.16</td>
      <td>8.16</td>
      <td>0.0</td>
      <td>2.71</td>
      <td>0.41</td>
      <td>5.04</td>
      <td>0.0</td>
      <td>36</td>
      <td>10</td>
      <td>221</td>
      <td>773</td>
      <td>1863</td>
    </tr>
  </tbody>
</table>
</div>




```python
h_step.head()
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
      <th>Id</th>
      <th>ActivityHour</th>
      <th>StepTotal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016 12:00:00 AM</td>
      <td>373</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/12/2016 1:00:00 AM</td>
      <td>160</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/12/2016 2:00:00 AM</td>
      <td>151</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/12/2016 3:00:00 AM</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/12/2016 4:00:00 AM</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
h_cal.head()
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
      <th>Id</th>
      <th>ActivityHour</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016 12:00:00 AM</td>
      <td>81</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/12/2016 1:00:00 AM</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/12/2016 2:00:00 AM</td>
      <td>59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/12/2016 3:00:00 AM</td>
      <td>47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/12/2016 4:00:00 AM</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
</div>




```python
h_cal.shape
```




    (22099, 3)




```python
h_step.shape
```




    (22099, 3)




```python
da.shape
```




    (940, 15)




```python
da.dtypes
```




    Id                            int64
    ActivityDate                 object
    TotalSteps                    int64
    TotalDistance               float64
    TrackerDistance             float64
    LoggedActivitiesDistance    float64
    VeryActiveDistance          float64
    ModeratelyActiveDistance    float64
    LightActiveDistance         float64
    SedentaryActiveDistance     float64
    VeryActiveMinutes             int64
    FairlyActiveMinutes           int64
    LightlyActiveMinutes          int64
    SedentaryMinutes              int64
    Calories                      int64
    dtype: object




```python
h_step.dtypes
```




    Id               int64
    ActivityHour    object
    StepTotal        int64
    dtype: object




```python
h_cal.dtypes
```




    Id               int64
    ActivityHour    object
    Calories         int64
    dtype: object



## Process
Next it's time to clean and transform the data so it can be ready to analyze. First we clean it with Python tools.

### Cleaning Data
After checking the shape and data types, we're going to combine the hourly steps and calories then change the ActivityHour to Date and change the format. Next changing the format for the daily activities dataframe and checking for missing values for all the data frames. After that, we will drop the columns we don't need for analysis.


```python
#Merging the hourly dataframes to have the steps and calories in one DF.
h_merged = pd.merge(h_step, h_cal, on=["Id","ActivityHour"], how="inner")
```


```python
#Making sure the size of the dataframe is still the same
h_merged.shape
```




    (22099, 4)




```python
h_merged.head()
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
      <th>Id</th>
      <th>ActivityHour</th>
      <th>StepTotal</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016 12:00:00 AM</td>
      <td>373</td>
      <td>81</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/12/2016 1:00:00 AM</td>
      <td>160</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/12/2016 2:00:00 AM</td>
      <td>151</td>
      <td>59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/12/2016 3:00:00 AM</td>
      <td>0</td>
      <td>47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/12/2016 4:00:00 AM</td>
      <td>0</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Formatting the date from object to Date
da['ActivityDate'] = pd.to_datetime(da['ActivityDate'])
```


```python
h_merged['ActivityHour'] = pd.to_datetime(h_merged['ActivityHour'])
```

    C:\Users\patto\AppData\Local\Temp\ipykernel_888\1626773981.py:1: UserWarning: Could not infer format, so each element will be parsed individually, falling back to `dateutil`. To ensure parsing is consistent and as-expected, please specify a format.
      h_merged['ActivityHour'] = pd.to_datetime(h_merged['ActivityHour'])
    


```python
h_merged.head()
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
      <th>Id</th>
      <th>ActivityHour</th>
      <th>StepTotal</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>2016-04-12 00:00:00</td>
      <td>373</td>
      <td>81</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>2016-04-12 01:00:00</td>
      <td>160</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>2016-04-12 02:00:00</td>
      <td>151</td>
      <td>59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>2016-04-12 03:00:00</td>
      <td>0</td>
      <td>47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>2016-04-12 04:00:00</td>
      <td>0</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Checking to make sure they are formated correctly
da.dtypes
```




    Id                                   int64
    ActivityDate                datetime64[ns]
    TotalSteps                           int64
    TotalDistance                      float64
    TrackerDistance                    float64
    LoggedActivitiesDistance           float64
    VeryActiveDistance                 float64
    ModeratelyActiveDistance           float64
    LightActiveDistance                float64
    SedentaryActiveDistance            float64
    VeryActiveMinutes                    int64
    FairlyActiveMinutes                  int64
    LightlyActiveMinutes                 int64
    SedentaryMinutes                     int64
    Calories                             int64
    dtype: object




```python
h_merged.dtypes
```




    Id                       int64
    ActivityHour    datetime64[ns]
    StepTotal                int64
    Calories                 int64
    dtype: object




```python
#Checking for null values in all data frames.
da.isnull().sum()
```




    Id                          0
    ActivityDate                0
    TotalSteps                  0
    TotalDistance               0
    TrackerDistance             0
    LoggedActivitiesDistance    0
    VeryActiveDistance          0
    ModeratelyActiveDistance    0
    LightActiveDistance         0
    SedentaryActiveDistance     0
    VeryActiveMinutes           0
    FairlyActiveMinutes         0
    LightlyActiveMinutes        0
    SedentaryMinutes            0
    Calories                    0
    dtype: int64




```python
da.rename(columns = {"ActivityDate": "Date"}, inplace=True)
```


```python
#Remove unecessary columns.
da.drop(["TrackerDistance", "LoggedActivitiesDistance", "TotalDistance", "SedentaryActiveDistance"], axis=1, inplace=True)
```


```python
da.head()
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
      <th>Id</th>
      <th>Date</th>
      <th>TotalSteps</th>
      <th>VeryActiveDistance</th>
      <th>ModeratelyActiveDistance</th>
      <th>LightActiveDistance</th>
      <th>VeryActiveMinutes</th>
      <th>FairlyActiveMinutes</th>
      <th>LightlyActiveMinutes</th>
      <th>SedentaryMinutes</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>2016-04-12</td>
      <td>13162</td>
      <td>1.88</td>
      <td>0.55</td>
      <td>6.06</td>
      <td>25</td>
      <td>13</td>
      <td>328</td>
      <td>728</td>
      <td>1985</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>2016-04-13</td>
      <td>10735</td>
      <td>1.57</td>
      <td>0.69</td>
      <td>4.71</td>
      <td>21</td>
      <td>19</td>
      <td>217</td>
      <td>776</td>
      <td>1797</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>2016-04-14</td>
      <td>10460</td>
      <td>2.44</td>
      <td>0.40</td>
      <td>3.91</td>
      <td>30</td>
      <td>11</td>
      <td>181</td>
      <td>1218</td>
      <td>1776</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>2016-04-15</td>
      <td>9762</td>
      <td>2.14</td>
      <td>1.26</td>
      <td>2.83</td>
      <td>29</td>
      <td>34</td>
      <td>209</td>
      <td>726</td>
      <td>1745</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>2016-04-16</td>
      <td>12669</td>
      <td>2.71</td>
      <td>0.41</td>
      <td>5.04</td>
      <td>36</td>
      <td>10</td>
      <td>221</td>
      <td>773</td>
      <td>1863</td>
    </tr>
  </tbody>
</table>
</div>



## **ANALYZE**

Now it's time to move onto the Analyze steps. Here we're going to take a look at the data and see what it tells us. It has been formatted properly and organized how I would like it. I'm going to look for trends and use those insights to answer the business questions.

### Adding Days of the Week 

I want to determine what day of the week the dates are so I can better analyze the data in the next step.


```python
#Creating day of the week column to help with analysis.
da['Day_of_week'] = da['Date'].dt.day_name()
```


```python
da.head()
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
      <th>Id</th>
      <th>Date</th>
      <th>TotalSteps</th>
      <th>VeryActiveDistance</th>
      <th>ModeratelyActiveDistance</th>
      <th>LightActiveDistance</th>
      <th>VeryActiveMinutes</th>
      <th>FairlyActiveMinutes</th>
      <th>LightlyActiveMinutes</th>
      <th>SedentaryMinutes</th>
      <th>Calories</th>
      <th>Day_of_week</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>2016-04-12</td>
      <td>13162</td>
      <td>1.88</td>
      <td>0.55</td>
      <td>6.06</td>
      <td>25</td>
      <td>13</td>
      <td>328</td>
      <td>728</td>
      <td>1985</td>
      <td>Tuesday</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>2016-04-13</td>
      <td>10735</td>
      <td>1.57</td>
      <td>0.69</td>
      <td>4.71</td>
      <td>21</td>
      <td>19</td>
      <td>217</td>
      <td>776</td>
      <td>1797</td>
      <td>Wednesday</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>2016-04-14</td>
      <td>10460</td>
      <td>2.44</td>
      <td>0.40</td>
      <td>3.91</td>
      <td>30</td>
      <td>11</td>
      <td>181</td>
      <td>1218</td>
      <td>1776</td>
      <td>Thursday</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>2016-04-15</td>
      <td>9762</td>
      <td>2.14</td>
      <td>1.26</td>
      <td>2.83</td>
      <td>29</td>
      <td>34</td>
      <td>209</td>
      <td>726</td>
      <td>1745</td>
      <td>Friday</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>2016-04-16</td>
      <td>12669</td>
      <td>2.71</td>
      <td>0.41</td>
      <td>5.04</td>
      <td>36</td>
      <td>10</td>
      <td>221</td>
      <td>773</td>
      <td>1863</td>
      <td>Saturday</td>
    </tr>
  </tbody>
</table>
</div>



### Looking at Active and Very Active Minutes

According to the CDC (Centers for Disease Control) and WHO (World Health Organization) adults 18-64 should have at least 150 minutes of moderate-intensity aerobic physical activity, 75 minutes of vigorous-intensity aerobic physical activity, or an equivalent mix of both every week. The links can be found [here](https://www.cdc.gov/physicalactivity/basics/adults/index.htm) for the CDC and and [here](https://www.who.int/news-room/fact-sheets/detail/physical-activity) for the WHO. 

It looks like for the most part, they do correlate with one another. 

Next I want to see if, on average, the Fairly and Very active minutes are where they should be according to the CDC and WHO. Breaking the minutes throughout the week, moderate-intensity per day would be 21.43 mins, vigorous-intensity per day would be 10.71, and an equivalent mix per day would be about 16.07 mins.


```python
#Creating a column with the equivalent minutes mix.
da['MinMix'] = (da['FairlyActiveMinutes'] + da['VeryActiveMinutes']) / 2
```


```python
da.head()
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
      <th>Id</th>
      <th>Date</th>
      <th>TotalSteps</th>
      <th>VeryActiveDistance</th>
      <th>ModeratelyActiveDistance</th>
      <th>LightActiveDistance</th>
      <th>VeryActiveMinutes</th>
      <th>FairlyActiveMinutes</th>
      <th>LightlyActiveMinutes</th>
      <th>SedentaryMinutes</th>
      <th>Calories</th>
      <th>Day_of_week</th>
      <th>MinMix</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>2016-04-12</td>
      <td>13162</td>
      <td>1.88</td>
      <td>0.55</td>
      <td>6.06</td>
      <td>25</td>
      <td>13</td>
      <td>328</td>
      <td>728</td>
      <td>1985</td>
      <td>Tuesday</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>2016-04-13</td>
      <td>10735</td>
      <td>1.57</td>
      <td>0.69</td>
      <td>4.71</td>
      <td>21</td>
      <td>19</td>
      <td>217</td>
      <td>776</td>
      <td>1797</td>
      <td>Wednesday</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>2016-04-14</td>
      <td>10460</td>
      <td>2.44</td>
      <td>0.40</td>
      <td>3.91</td>
      <td>30</td>
      <td>11</td>
      <td>181</td>
      <td>1218</td>
      <td>1776</td>
      <td>Thursday</td>
      <td>20.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>2016-04-15</td>
      <td>9762</td>
      <td>2.14</td>
      <td>1.26</td>
      <td>2.83</td>
      <td>29</td>
      <td>34</td>
      <td>209</td>
      <td>726</td>
      <td>1745</td>
      <td>Friday</td>
      <td>31.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>2016-04-16</td>
      <td>12669</td>
      <td>2.71</td>
      <td>0.41</td>
      <td>5.04</td>
      <td>36</td>
      <td>10</td>
      <td>221</td>
      <td>773</td>
      <td>1863</td>
      <td>Saturday</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
da_group = da.groupby("Id").agg({"FairlyActiveMinutes":'mean', "VeryActiveMinutes": 'mean', "MinMix": 'mean', "TotalSteps": 'mean',"Calories":'mean'})
```


```python
da_mins_avg = da_group.reset_index()
da_mins_avg
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
      <th>Id</th>
      <th>FairlyActiveMinutes</th>
      <th>VeryActiveMinutes</th>
      <th>MinMix</th>
      <th>TotalSteps</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>19.161290</td>
      <td>38.709677</td>
      <td>28.935484</td>
      <td>12116.741935</td>
      <td>1816.419355</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1624580081</td>
      <td>5.806452</td>
      <td>8.677419</td>
      <td>7.241935</td>
      <td>5743.903226</td>
      <td>1483.354839</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1644430081</td>
      <td>21.366667</td>
      <td>9.566667</td>
      <td>15.466667</td>
      <td>7282.966667</td>
      <td>2811.300000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1844505072</td>
      <td>1.290323</td>
      <td>0.129032</td>
      <td>0.709677</td>
      <td>2580.064516</td>
      <td>1573.483871</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1927972279</td>
      <td>0.774194</td>
      <td>1.322581</td>
      <td>1.048387</td>
      <td>916.129032</td>
      <td>2172.806452</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2022484408</td>
      <td>19.354839</td>
      <td>36.290323</td>
      <td>27.822581</td>
      <td>11370.645161</td>
      <td>2509.967742</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2026352035</td>
      <td>0.258065</td>
      <td>0.096774</td>
      <td>0.177419</td>
      <td>5566.870968</td>
      <td>1540.645161</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2320127002</td>
      <td>2.580645</td>
      <td>1.354839</td>
      <td>1.967742</td>
      <td>4716.870968</td>
      <td>1724.161290</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2347167796</td>
      <td>20.555556</td>
      <td>13.500000</td>
      <td>17.027778</td>
      <td>9519.666667</td>
      <td>2043.444444</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2873212765</td>
      <td>6.129032</td>
      <td>14.096774</td>
      <td>10.112903</td>
      <td>7555.774194</td>
      <td>1916.967742</td>
    </tr>
    <tr>
      <th>10</th>
      <td>3372868164</td>
      <td>4.100000</td>
      <td>9.150000</td>
      <td>6.625000</td>
      <td>6861.650000</td>
      <td>1933.100000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>3977333714</td>
      <td>61.266667</td>
      <td>18.900000</td>
      <td>40.083333</td>
      <td>10984.566667</td>
      <td>1513.666667</td>
    </tr>
    <tr>
      <th>12</th>
      <td>4020332650</td>
      <td>5.354839</td>
      <td>5.193548</td>
      <td>5.274194</td>
      <td>2267.225806</td>
      <td>2385.806452</td>
    </tr>
    <tr>
      <th>13</th>
      <td>4057192912</td>
      <td>1.500000</td>
      <td>0.750000</td>
      <td>1.125000</td>
      <td>3838.000000</td>
      <td>1973.750000</td>
    </tr>
    <tr>
      <th>14</th>
      <td>4319703577</td>
      <td>12.322581</td>
      <td>3.580645</td>
      <td>7.951613</td>
      <td>7268.838710</td>
      <td>2037.677419</td>
    </tr>
    <tr>
      <th>15</th>
      <td>4388161847</td>
      <td>20.354839</td>
      <td>23.161290</td>
      <td>21.758065</td>
      <td>10813.935484</td>
      <td>3093.870968</td>
    </tr>
    <tr>
      <th>16</th>
      <td>4445114986</td>
      <td>1.741935</td>
      <td>6.612903</td>
      <td>4.177419</td>
      <td>4796.548387</td>
      <td>2186.193548</td>
    </tr>
    <tr>
      <th>17</th>
      <td>4558609924</td>
      <td>13.709677</td>
      <td>10.387097</td>
      <td>12.048387</td>
      <td>7685.129032</td>
      <td>2033.258065</td>
    </tr>
    <tr>
      <th>18</th>
      <td>4702921684</td>
      <td>26.032258</td>
      <td>5.129032</td>
      <td>15.580645</td>
      <td>8572.064516</td>
      <td>2965.548387</td>
    </tr>
    <tr>
      <th>19</th>
      <td>5553957443</td>
      <td>13.000000</td>
      <td>23.419355</td>
      <td>18.209677</td>
      <td>8612.580645</td>
      <td>1875.677419</td>
    </tr>
    <tr>
      <th>20</th>
      <td>5577150313</td>
      <td>29.833333</td>
      <td>87.333333</td>
      <td>58.583333</td>
      <td>8304.433333</td>
      <td>3359.633333</td>
    </tr>
    <tr>
      <th>21</th>
      <td>6117666160</td>
      <td>2.035714</td>
      <td>1.571429</td>
      <td>1.803571</td>
      <td>7046.714286</td>
      <td>2261.142857</td>
    </tr>
    <tr>
      <th>22</th>
      <td>6290855005</td>
      <td>3.793103</td>
      <td>2.758621</td>
      <td>3.275862</td>
      <td>5649.551724</td>
      <td>2599.620690</td>
    </tr>
    <tr>
      <th>23</th>
      <td>6775888955</td>
      <td>14.807692</td>
      <td>11.000000</td>
      <td>12.903846</td>
      <td>2519.692308</td>
      <td>2131.769231</td>
    </tr>
    <tr>
      <th>24</th>
      <td>6962181067</td>
      <td>18.516129</td>
      <td>22.806452</td>
      <td>20.661290</td>
      <td>9794.806452</td>
      <td>1982.032258</td>
    </tr>
    <tr>
      <th>25</th>
      <td>7007744171</td>
      <td>16.269231</td>
      <td>31.038462</td>
      <td>23.653846</td>
      <td>11323.423077</td>
      <td>2544.000000</td>
    </tr>
    <tr>
      <th>26</th>
      <td>7086361926</td>
      <td>25.354839</td>
      <td>42.580645</td>
      <td>33.967742</td>
      <td>9371.774194</td>
      <td>2566.354839</td>
    </tr>
    <tr>
      <th>27</th>
      <td>8053475328</td>
      <td>9.580645</td>
      <td>85.161290</td>
      <td>47.370968</td>
      <td>14763.290323</td>
      <td>2945.806452</td>
    </tr>
    <tr>
      <th>28</th>
      <td>8253242879</td>
      <td>14.315789</td>
      <td>20.526316</td>
      <td>17.421053</td>
      <td>6482.157895</td>
      <td>1788.000000</td>
    </tr>
    <tr>
      <th>29</th>
      <td>8378563200</td>
      <td>10.258065</td>
      <td>58.677419</td>
      <td>34.467742</td>
      <td>8717.709677</td>
      <td>3436.580645</td>
    </tr>
    <tr>
      <th>30</th>
      <td>8583815059</td>
      <td>22.193548</td>
      <td>9.677419</td>
      <td>15.935484</td>
      <td>7198.516129</td>
      <td>2732.032258</td>
    </tr>
    <tr>
      <th>31</th>
      <td>8792009665</td>
      <td>4.034483</td>
      <td>0.965517</td>
      <td>2.500000</td>
      <td>1853.724138</td>
      <td>1962.310345</td>
    </tr>
    <tr>
      <th>32</th>
      <td>8877689391</td>
      <td>9.935484</td>
      <td>66.064516</td>
      <td>38.000000</td>
      <td>16040.032258</td>
      <td>3420.258065</td>
    </tr>
  </tbody>
</table>
</div>




```python
da_mins_avg[da_mins_avg.FairlyActiveMinutes > 21.43].count()
```




    Id                     5
    FairlyActiveMinutes    5
    VeryActiveMinutes      5
    MinMix                 5
    TotalSteps             5
    Calories               5
    dtype: int64




```python
da_mins_avg[da_mins_avg.VeryActiveMinutes > 10.71].count()
```




    Id                     16
    FairlyActiveMinutes    16
    VeryActiveMinutes      16
    MinMix                 16
    TotalSteps             16
    Calories               16
    dtype: int64




```python
da_mins_avg[da_mins_avg.MinMix > 16.07].count()
```




    Id                     14
    FairlyActiveMinutes    14
    VeryActiveMinutes      14
    MinMix                 14
    TotalSteps             14
    Calories               14
    dtype: int64




```python
da_mins_avg[da_mins_avg.TotalSteps > 10000].count()
```




    Id                     7
    FairlyActiveMinutes    7
    VeryActiveMinutes      7
    MinMix                 7
    TotalSteps             7
    Calories               7
    dtype: int64



In theory, steps should correlate with calories burned. So I'm going to graph it to make sure that is accurate.


```python
#Confirming steps correlate with calories burned.
sns.set_theme()
sns.regplot(data=da, x= "TotalSteps", y= "Calories", scatter_kws = {"color": "orange"}, line_kws = {"color":"black"})
```




    <Axes: xlabel='TotalSteps', ylabel='Calories'>




    
![png](Case_Study_2_files/Case_Study_2_40_1.png)
    


Next, I'm taking a quick look at the sleep data. It wasn't originally going to be used due to it only have 23 out of the 33 people that were supposed to be using it. But it turns out to be useful in showing that, on average, half the people that did use it got less than the recommened 7 hours. The 7 hours (420 minutes) comes from the National Insitute of Health [here](https://www.nhlbi.nih.gov/health/sleep/how-much-sleep).


```python
sd.head()
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
      <th>Id</th>
      <th>SleepDay</th>
      <th>TotalSleepRecords</th>
      <th>TotalMinutesAsleep</th>
      <th>TotalTimeInBed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016 12:00:00 AM</td>
      <td>1</td>
      <td>327</td>
      <td>346</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/13/2016 12:00:00 AM</td>
      <td>2</td>
      <td>384</td>
      <td>407</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/15/2016 12:00:00 AM</td>
      <td>1</td>
      <td>412</td>
      <td>442</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/16/2016 12:00:00 AM</td>
      <td>2</td>
      <td>340</td>
      <td>367</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/17/2016 12:00:00 AM</td>
      <td>1</td>
      <td>700</td>
      <td>712</td>
    </tr>
  </tbody>
</table>
</div>




```python
sd.dtypes
```




    Id                     int64
    SleepDay              object
    TotalSleepRecords      int64
    TotalMinutesAsleep     int64
    TotalTimeInBed         int64
    dtype: object




```python
sd['SleepDay'] = pd.to_datetime(sd['SleepDay'])
```

    C:\Users\patto\AppData\Local\Temp\ipykernel_888\413052152.py:1: UserWarning: Could not infer format, so each element will be parsed individually, falling back to `dateutil`. To ensure parsing is consistent and as-expected, please specify a format.
      sd['SleepDay'] = pd.to_datetime(sd['SleepDay'])
    


```python
sd_group = sd.groupby("Id")["TotalMinutesAsleep"].mean()
sd_group = sd_group.reset_index(drop=False)
sd_group
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
      <th>Id</th>
      <th>TotalMinutesAsleep</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>360.280000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1644430081</td>
      <td>294.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1844505072</td>
      <td>652.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1927972279</td>
      <td>417.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2026352035</td>
      <td>506.178571</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2320127002</td>
      <td>61.000000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2347167796</td>
      <td>446.800000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3977333714</td>
      <td>293.642857</td>
    </tr>
    <tr>
      <th>8</th>
      <td>4020332650</td>
      <td>349.375000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>4319703577</td>
      <td>476.653846</td>
    </tr>
    <tr>
      <th>10</th>
      <td>4388161847</td>
      <td>403.125000</td>
    </tr>
    <tr>
      <th>11</th>
      <td>4445114986</td>
      <td>385.178571</td>
    </tr>
    <tr>
      <th>12</th>
      <td>4558609924</td>
      <td>127.600000</td>
    </tr>
    <tr>
      <th>13</th>
      <td>4702921684</td>
      <td>421.142857</td>
    </tr>
    <tr>
      <th>14</th>
      <td>5553957443</td>
      <td>463.483871</td>
    </tr>
    <tr>
      <th>15</th>
      <td>5577150313</td>
      <td>432.000000</td>
    </tr>
    <tr>
      <th>16</th>
      <td>6117666160</td>
      <td>478.777778</td>
    </tr>
    <tr>
      <th>17</th>
      <td>6775888955</td>
      <td>349.666667</td>
    </tr>
    <tr>
      <th>18</th>
      <td>6962181067</td>
      <td>448.000000</td>
    </tr>
    <tr>
      <th>19</th>
      <td>7007744171</td>
      <td>68.500000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>7086361926</td>
      <td>453.125000</td>
    </tr>
    <tr>
      <th>21</th>
      <td>8053475328</td>
      <td>297.000000</td>
    </tr>
    <tr>
      <th>22</th>
      <td>8378563200</td>
      <td>443.343750</td>
    </tr>
    <tr>
      <th>23</th>
      <td>8792009665</td>
      <td>435.666667</td>
    </tr>
  </tbody>
</table>
</div>




```python
sd_group[sd_group.TotalMinutesAsleep < 420].count()
```




    Id                    12
    TotalMinutesAsleep    12
    dtype: int64




```python
sns.regplot(data = sd, x = "TotalMinutesAsleep", y= "TotalTimeInBed", scatter_kws = {"color": "orange"}, line_kws = {"color":"black"})
```




    <Axes: xlabel='TotalMinutesAsleep', ylabel='TotalTimeInBed'>




    
![png](Case_Study_2_files/Case_Study_2_47_1.png)
    


## **SHARE**

Now that the data has been analyzed, it's time to move onto the Share phase. During this next step, I will make some visualizations to try and tell the story that the data tells me. 

#### **Key Tasks** 

**1. Determine the best way to share your findings.**

* Create visualizations to show results of analyzing


```python
fig, axes = plt.subplots(nrows = 3, figsize=[12,12])
sns.regplot(data=da_mins_avg, x= "VeryActiveMinutes", y = "Calories", ax=axes[0], scatter_kws = {"color": "orange"}, line_kws = {"color":"green"})
sns.regplot(data=da_mins_avg, x= "FairlyActiveMinutes", y = "Calories",ax = axes[2], scatter_kws = {"color": "orange"}, line_kws = {"color":"red"})
sns.regplot(data=da_mins_avg, x= "MinMix", y = "Calories", ax = axes[1], scatter_kws = {"color": "orange"}, line_kws = {"color":"orange"})
```




    <Axes: xlabel='MinMix', ylabel='Calories'>




    
![png](Case_Study_2_files/Case_Study_2_49_1.png)
    


**Findings:**
* More calories are burned when people are "Very" active and a mix of "Very" and "Fairly" active compared to just being "Fairly" active.
* Less than half of the people achieved the minimum "Very" and "Fairly" active minutes.
* According to the analysis, people achieved the minimnum needed of activity a day when being "Very" active (about half) and "Mixed" active(also half).
* Only 7 peolpe, on average, achieve their daily step goals
* A little over a fifth of the people, on average, get the recommended 7 hours of sleep. This dataset was missing 8 people.
* There were only 8 people who logged thier weight and not very often.

## **ACT**

Lastly, I will share my recommendations for Bellabeats marketing department.

**Recommendations for Bellabeats:**

* From the lack of people logging their weight, it stands to reason that a possibility could be the lack of effort people want to go through with having to log the weight their self. Other features automatically log the information, so I would recommend having one for weight, as well. A smart scale would take some of the effort out the customer's hands.
* Same automatic logging of sleep would help gather more data on sleep to make future insights more accurate.
* Trends noted with other health tracking technology that has been rising is competition with friends and others on the same app to keep each other accountable for maintaining and achieving their health goals.
* Hourly, daily, and weekly reminders should be considered. To help people keep track of their daily progress, goals should be set for them when they wake. Througout the daily, the app or device will let them know how they are doing according to average or their personal goals. 

## Citations

1. Mobius. (n.d.). *Fitbit Dataset*. Kaggle. [https://www.kaggle.com/datasets/arashnic/fitbit](https://www.kaggle.com/datasets/arashnic/fitbit)

2. Stack Overflow. (n.d.). *Assistance with Python code, visualization, and usage of various libraries*. Various authors.

3. Centers for Disease Control and Prevention. (n.d.). *Physical Activity Basics: Guidelines for Adults*. Author unknown. [https://www.cdc.gov/physical-activity-basics/guidelines/adults.html](https://www.cdc.gov/physical-activity-basics/guidelines/adults.html)

4. World Health Organization. (n.d.). *Physical Activity*. Author unknown. [https://www.who.int/europe/news-room/fact-sheets/item/physical-activity](https://www.who.int/europe/news-room/fact-sheets/item/physical-activity)
