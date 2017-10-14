

```python
import pandas as pd
import json
```


```python
with open("purchase_data2.json") as datafile:
    data = json.load(datafile)
data_file_pd = pd.DataFrame(data)
```


```python
data_file_pd.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>



# **Player Count**


```python
SN_unique=data_file_pd["SN"].value_counts()
SN_unique.head(10)
```




    Sundaky74      2
    Chaniman66     2
    Aidaira26      2
    Hairith93      2
    Airi27         1
    Lisirra44      1
    Iloni35        1
    Assistast50    1
    Ila44          1
    Streural92     1
    Name: SN, dtype: int64




```python
SN_Number = data_file_pd["SN"].nunique()
SN_Number

Totalplayer_table = pd.DataFrame({'Total player' : [SN_Number]})

Totalplayer_table
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total player</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Total)


```python
Number_of_Unique_Items=data_file_pd["Item Name"].nunique()
Number_of_Unique_Items
```




    63




```python
Average_Purchase_Price = data_file_pd["Price"].mean()
Average_Purchase_Price

```




    2.9243589743589733




```python
Total_Number_of_Purchases=data_file_pd["Item Name"].count()
Total_Number_of_Purchases
```




    78




```python
Total_Revenue=data_file_pd["Price"].sum()
Total_Revenue
```




    228.0999999999999




```python
# Creating a summary DataFrame using above values
Purchasing_Analysis_df = pd.DataFrame({"Number of Unique Items":[Number_of_Unique_Items],
                          "Average_Purchase_Price":[Average_Purchase_Price],
                          "Total_Number_of_Purchases":[Total_Number_of_Purchases],
                          "Total_Revenue":[Total_Revenue]})
Purchasing_Analysis_df=Purchasing_Analysis_df[["Number of Unique Items",
                          "Average_Purchase_Price",
                          "Total_Number_of_Purchases",
                          "Total_Revenue"]]
Purchasing_Analysis_df=Purchasing_Analysis_df.round(2)
Purchasing_Analysis_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average_Purchase_Price</th>
      <th>Total_Number_of_Purchases</th>
      <th>Total_Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>63</td>
      <td>2.92</td>
      <td>78</td>
      <td>228.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Improve formatting before outputting spreadsheet
Purchasing_Analysis_df["Average_Purchase_Price"] = Purchasing_Analysis_df["Average_Purchase_Price"].map("$ {:,.2f}".format)
Purchasing_Analysis_df["Total_Revenue"] = Purchasing_Analysis_df["Total_Revenue"].map("$ {:,.2f}".format)
Purchasing_Analysis_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average_Purchase_Price</th>
      <th>Total_Number_of_Purchases</th>
      <th>Total_Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>63</td>
      <td>$ 2.92</td>
      <td>78</td>
      <td>$ 228.10</td>
    </tr>
  </tbody>
</table>
</div>



# **Gender Demographics**


```python
SN_grouped_df= data_file_pd.groupby(['SN','Gender'])

SN_grouped_df.count().head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aeri79</th>
      <th>Female</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <th>Male</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aesririam61</th>
      <th>Female</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aesurstilis64</th>
      <th>Male</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <th>Male</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
SN_grouped_df.mean()

game_comparison = pd.DataFrame(SN_grouped_df.mean())
game_comparison.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aeri79</th>
      <th>Female</th>
      <td>23.0</td>
      <td>107.0</td>
      <td>4.150</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <th>Male</th>
      <td>40.0</td>
      <td>148.0</td>
      <td>4.650</td>
    </tr>
    <tr>
      <th>Aesririam61</th>
      <th>Female</th>
      <td>39.0</td>
      <td>2.0</td>
      <td>2.650</td>
    </tr>
    <tr>
      <th>Aesurstilis64</th>
      <th>Male</th>
      <td>36.0</td>
      <td>139.0</td>
      <td>4.250</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <th>Male</th>
      <td>21.0</td>
      <td>47.0</td>
      <td>2.565</td>
    </tr>
  </tbody>
</table>
</div>




```python
game_comparison.reset_index(inplace=True)
game_comparison.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Gender</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>Female</td>
      <td>23.0</td>
      <td>107.0</td>
      <td>4.150</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>Male</td>
      <td>40.0</td>
      <td>148.0</td>
      <td>4.650</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>Female</td>
      <td>39.0</td>
      <td>2.0</td>
      <td>2.650</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>Male</td>
      <td>36.0</td>
      <td>139.0</td>
      <td>4.250</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>Male</td>
      <td>21.0</td>
      <td>47.0</td>
      <td>2.565</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_gender = len(game_comparison["SN"].unique())
total_gender
```




    74




```python
Male_Players = game_comparison["Gender"].value_counts()["Male"]
Male_Players
```




    60




```python
Female_Players = game_comparison["Gender"].value_counts()["Female"]
Female_Players
```




    13




```python
Other_Non_Disclosed = total_gender - Male_Players - Female_Players
Other_Non_Disclosed
```




    1




```python
male_percent = (Male_Players/total_gender) * 100
male_percent
```




    81.081081081081081




```python
female_percent = (Female_Players/total_gender) * 100
female_percent
```




    17.567567567567568




```python
Other_Non_Disclosed_percent = (Other_Non_Disclosed/total_gender) * 100
Other_Non_Disclosed_percent
```




    1.3513513513513513




```python
data = {"Percentage of Players":[male_percent, female_percent, Other_Non_Disclosed_percent],"Total Count":[Male_Players,Female_Players,Other_Non_Disclosed]}
Gender_Demographics_df = pd.DataFrame(data, index=['Male','Female','Other_Non_Disclosed'])
Gender_Demographics_df=Gender_Demographics_df[["Percentage of Players","Total Count"]]
Gender_Demographics_df=Gender_Demographics_df.round(2)
Gender_Demographics_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>81.08</td>
      <td>60</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.57</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>1.35</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



# **Purchasing Analysis (Gender)** 


```python
male_df = data_file_pd.loc[data_file_pd["Gender"] == "Male"]

male_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
male_purchase_Count=len(male_df)
male_purchase_Count
```




    64




```python
female_df = data_file_pd.loc[data_file_pd["Gender"] == "Female"]

female_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11</th>
      <td>36</td>
      <td>Female</td>
      <td>173</td>
      <td>Stormfury Longsword</td>
      <td>4.01</td>
      <td>Jiskim75</td>
    </tr>
    <tr>
      <th>12</th>
      <td>20</td>
      <td>Female</td>
      <td>90</td>
      <td>Betrayer</td>
      <td>4.12</td>
      <td>Lirtassa77</td>
    </tr>
    <tr>
      <th>28</th>
      <td>20</td>
      <td>Female</td>
      <td>170</td>
      <td>Shadowsteel</td>
      <td>1.74</td>
      <td>Sondassasya91</td>
    </tr>
    <tr>
      <th>32</th>
      <td>24</td>
      <td>Female</td>
      <td>117</td>
      <td>Heartstriker, Legacy of the Light</td>
      <td>4.71</td>
      <td>Alarap40</td>
    </tr>
    <tr>
      <th>33</th>
      <td>16</td>
      <td>Female</td>
      <td>0</td>
      <td>Splinter</td>
      <td>1.89</td>
      <td>Pharithdil38</td>
    </tr>
  </tbody>
</table>
</div>




```python
female_purchase_Count=len(female_df)
female_purchase_Count
```




    13




```python
other_df = data_file_pd.loc[data_file_pd["Gender"] == "Other / Non-Disclosed"]

other_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>18</th>
      <td>12</td>
      <td>Other / Non-Disclosed</td>
      <td>176</td>
      <td>Relentless Iron Skewer</td>
      <td>2.12</td>
      <td>Inadeu25</td>
    </tr>
  </tbody>
</table>
</div>




```python
other_purchase_Count=len(other_df)
other_purchase_Count
```




    1




```python
male_Average_Purchase_Price = male_df["Price"].mean()
male_Average_Purchase_Price
```




    2.8843749999999995




```python
female_Average_Purchase_Price = female_df["Price"].mean()
female_Average_Purchase_Price
```




    3.183076923076923




```python
other_Average_Purchase_Price = other_df["Price"].mean()
other_Average_Purchase_Price 
```




    2.12




```python
male_Total_Purchase_Value = male_df["Price"].sum()
male_Total_Purchase_Value
```




    184.59999999999997




```python
female_Total_Purchase_Value = female_df["Price"].sum()
female_Total_Purchase_Value
```




    41.38




```python
other_total_Purchase_Price = other_df["Price"].mean()
other_total_Purchase_Price 

```




    2.12




```python
male_Normalized_Totals = male_Total_Purchase_Value/Male_Players
male_Normalized_Totals
```




    3.0766666666666662




```python
female_Normalized_Totals = female_Total_Purchase_Value/Female_Players
female_Normalized_Totals
```




    3.1830769230769231




```python
other_Normalized_Totals = other_total_Purchase_Price/Other_Non_Disclosed
other_Normalized_Totals
```




    2.1200000000000001




```python
data = {"Purchase Count":[male_purchase_Count, female_purchase_Count, other_purchase_Count],"Average Purchase Price":[male_Average_Purchase_Price, female_Average_Purchase_Price,other_Average_Purchase_Price], "Total Purchase Value":[male_Total_Purchase_Value,female_Total_Purchase_Value,other_total_Purchase_Price], "Normalized Totals":[male_Normalized_Totals,female_Normalized_Totals,other_Normalized_Totals]}
Gender_Demographics_df = pd.DataFrame(data, index=['Male','Female','Other_Non_Disclosed'])
Gender_Demographics_df=Gender_Demographics_df[["Purchase Count","Average Purchase Price","Total Purchase Value","Normalized Totals"]]

Gender_Demographics_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>64</td>
      <td>2.884375</td>
      <td>184.60</td>
      <td>3.076667</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>13</td>
      <td>3.183077</td>
      <td>41.38</td>
      <td>3.183077</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>1</td>
      <td>2.120000</td>
      <td>2.12</td>
      <td>2.120000</td>
    </tr>
  </tbody>
</table>
</div>




```python
Gender_Demographics_df["Average Purchase Price"] = Gender_Demographics_df["Average Purchase Price"].map('${:,.2f}'.format)
Gender_Demographics_df["Total Purchase Value"] = Gender_Demographics_df["Total Purchase Value"].map('${:,.2f}'.format)
Gender_Demographics_df["Normalized Totals"] = Gender_Demographics_df["Normalized Totals"].map('${:,.2f}'.format)
Gender_Demographics_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>64</td>
      <td>$2.88</td>
      <td>$184.60</td>
      <td>$3.08</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>13</td>
      <td>$3.18</td>
      <td>$41.38</td>
      <td>$3.18</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>1</td>
      <td>$2.12</td>
      <td>$2.12</td>
      <td>$2.12</td>
    </tr>
  </tbody>
</table>
</div>



# Age Demographics


```python
bins = [0, 10, 15, 20, 25, 30, 35, 40, 100]

group_names = ['<10', '10-14', '15-19', '20-24','25-29','30-34','35-39','>40']
```


```python
pd.cut(data_file_pd["Age"], bins, labels=group_names)
```




    0     15-19
    1     20-24
    2     15-19
    3     15-19
    4     20-24
    5       <10
    6     35-39
    7     25-29
    8     15-19
    9     35-39
    10    20-24
    11    35-39
    12    15-19
    13    30-34
    14      <10
    15    20-24
    16    20-24
    17      <10
    18    10-14
    19    20-24
    20    30-34
    21    10-14
    22    15-19
    23    15-19
    24    20-24
    25    15-19
    26      <10
    27    20-24
    28    15-19
    29    20-24
          ...  
    48    20-24
    49    15-19
    50    20-24
    51    25-29
    52    20-24
    53    15-19
    54    20-24
    55    15-19
    56    15-19
    57    20-24
    58    25-29
    59    35-39
    60    20-24
    61    20-24
    62    15-19
    63    10-14
    64    20-24
    65    20-24
    66    20-24
    67    20-24
    68    20-24
    69    30-34
    70    20-24
    71    20-24
    72    20-24
    73    30-34
    74    35-39
    75    10-14
    76    20-24
    77    15-19
    Name: Age, Length: 78, dtype: category
    Categories (8, object): [<10 < 10-14 < 15-19 < 20-24 < 25-29 < 30-34 < 35-39 < >40]




```python
data_file_pd["Age Summary"] = pd.cut(data_file_pd["Age"], bins, labels=group_names)
data_file_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age Summary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
age_grouped_df= data_file_pd.groupby(['Age Summary'])

pc_df = age_grouped_df.count().head(10)
pc_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
    <tr>
      <th>Age Summary</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pc_df.reset_index(inplace=True)
pc_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
      <td>33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pc1_df=pc_df[["Age Summary","Item Name"]]
pc1_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Item Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pc2_df=pc1_df.rename(columns={"Item Name":"Purchase Count"})
pc2_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
average_df=age_grouped_df.mean().head(10)
average_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Age Summary</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>8.000000</td>
      <td>63.000000</td>
      <td>2.764000</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>12.250000</td>
      <td>128.750000</td>
      <td>3.052500</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>18.450000</td>
      <td>90.650000</td>
      <td>2.734500</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>23.090909</td>
      <td>100.909091</td>
      <td>3.043030</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>29.000000</td>
      <td>48.250000</td>
      <td>2.692500</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>33.428571</td>
      <td>76.571429</td>
      <td>2.352857</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>37.800000</td>
      <td>125.000000</td>
      <td>3.944000</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
average_df.reset_index(inplace=True)
average_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>8.000000</td>
      <td>63.000000</td>
      <td>2.764000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>12.250000</td>
      <td>128.750000</td>
      <td>3.052500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>18.450000</td>
      <td>90.650000</td>
      <td>2.734500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>23.090909</td>
      <td>100.909091</td>
      <td>3.043030</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>29.000000</td>
      <td>48.250000</td>
      <td>2.692500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>33.428571</td>
      <td>76.571429</td>
      <td>2.352857</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>37.800000</td>
      <td>125.000000</td>
      <td>3.944000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
a1_df=average_df[["Age Summary","Price"]]
a1_df

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>2.764000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>3.052500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>2.734500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>3.043030</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>2.692500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>2.352857</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>3.944000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
a2_df=a1_df.rename(columns={"Price":"Average Purchase Price"})
a2_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>2.764000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>3.052500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>2.734500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>3.043030</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>2.692500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>2.352857</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>3.944000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
merge1 = pd.merge(pc2_df, a2_df, on="Age Summary")
merge1
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>5</td>
      <td>2.764000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>4</td>
      <td>3.052500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>20</td>
      <td>2.734500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>33</td>
      <td>3.043030</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>4</td>
      <td>2.692500</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>7</td>
      <td>2.352857</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>5</td>
      <td>3.944000</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum_df=age_grouped_df.sum().head(10)
sum_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>Age Summary</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>40.0</td>
      <td>315.0</td>
      <td>13.82</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>49.0</td>
      <td>515.0</td>
      <td>12.21</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>369.0</td>
      <td>1813.0</td>
      <td>54.69</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>762.0</td>
      <td>3330.0</td>
      <td>100.42</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>116.0</td>
      <td>193.0</td>
      <td>10.77</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>234.0</td>
      <td>536.0</td>
      <td>16.47</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>189.0</td>
      <td>625.0</td>
      <td>19.72</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum_df.reset_index(inplace=True)
sum_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>40.0</td>
      <td>315.0</td>
      <td>13.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>49.0</td>
      <td>515.0</td>
      <td>12.21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>369.0</td>
      <td>1813.0</td>
      <td>54.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>762.0</td>
      <td>3330.0</td>
      <td>100.42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>116.0</td>
      <td>193.0</td>
      <td>10.77</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>234.0</td>
      <td>536.0</td>
      <td>16.47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>189.0</td>
      <td>625.0</td>
      <td>19.72</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum1_df=sum_df[["Age Summary","Price"]]
sum1_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>13.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>12.21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>54.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>100.42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>10.77</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>16.47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>19.72</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
sum2_df=sum1_df.rename(columns={"Price":"Total Purchase Value"})
sum2_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>13.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>12.21</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>54.69</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>100.42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>10.77</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>16.47</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>19.72</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
Normalized_total=sum2_df["Total Purchase Value"]/pc_df["SN"].nunique()
Normalized_total
```




    0     2.303333
    1     2.035000
    2     9.115000
    3    16.736667
    4     1.795000
    5     2.745000
    6     3.286667
    7          NaN
    Name: Total Purchase Value, dtype: float64




```python
sum2_df["Normalized Total"] =Normalized_total
sum2_df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Total Purchase Value</th>
      <th>Normalized Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>13.82</td>
      <td>2.303333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>12.21</td>
      <td>2.035000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>54.69</td>
      <td>9.115000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>100.42</td>
      <td>16.736667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>10.77</td>
      <td>1.795000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>16.47</td>
      <td>2.745000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>19.72</td>
      <td>3.286667</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
Age_Demographics = pd.merge(merge1,sum2_df, on="Age Summary")
Age_Demographics
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>5</td>
      <td>2.764000</td>
      <td>13.82</td>
      <td>2.303333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>4</td>
      <td>3.052500</td>
      <td>12.21</td>
      <td>2.035000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>20</td>
      <td>2.734500</td>
      <td>54.69</td>
      <td>9.115000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>33</td>
      <td>3.043030</td>
      <td>100.42</td>
      <td>16.736667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>4</td>
      <td>2.692500</td>
      <td>10.77</td>
      <td>1.795000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>7</td>
      <td>2.352857</td>
      <td>16.47</td>
      <td>2.745000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>5</td>
      <td>3.944000</td>
      <td>19.72</td>
      <td>3.286667</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
Age_Demographics= Age_Demographics.replace({"NaN": "0"})
Age_Demographics
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>5</td>
      <td>2.764000</td>
      <td>13.82</td>
      <td>2.303333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>4</td>
      <td>3.052500</td>
      <td>12.21</td>
      <td>2.035000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>20</td>
      <td>2.734500</td>
      <td>54.69</td>
      <td>9.115000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>33</td>
      <td>3.043030</td>
      <td>100.42</td>
      <td>16.736667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>4</td>
      <td>2.692500</td>
      <td>10.77</td>
      <td>1.795000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>7</td>
      <td>2.352857</td>
      <td>16.47</td>
      <td>2.745000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>5</td>
      <td>3.944000</td>
      <td>19.72</td>
      <td>3.286667</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
Age_Demographics["Average Purchase Price"] = Age_Demographics["Average Purchase Price"].map("$ {:,.2f}".format)
Age_Demographics["Total Purchase Value"] = Age_Demographics["Total Purchase Value"].map("$ {:,.2f}".format)
Age_Demographics["Normalized Total"] = Age_Demographics["Normalized Total"].map("$ {:,.2f}".format)
Age_Demographics
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Summary</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>5</td>
      <td>$ 2.76</td>
      <td>$ 13.82</td>
      <td>$ 2.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>4</td>
      <td>$ 3.05</td>
      <td>$ 12.21</td>
      <td>$ 2.04</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>20</td>
      <td>$ 2.73</td>
      <td>$ 54.69</td>
      <td>$ 9.12</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>33</td>
      <td>$ 3.04</td>
      <td>$ 100.42</td>
      <td>$ 16.74</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>4</td>
      <td>$ 2.69</td>
      <td>$ 10.77</td>
      <td>$ 1.79</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>7</td>
      <td>$ 2.35</td>
      <td>$ 16.47</td>
      <td>$ 2.75</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>5</td>
      <td>$ 3.94</td>
      <td>$ 19.72</td>
      <td>$ 3.29</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>0</td>
      <td>$ nan</td>
      <td>$ nan</td>
      <td>$ nan</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders


```python
with open("purchase_data2.json") as datafile:
    data = json.load(datafile)
data_file_pd = pd.DataFrame(data)
data_file_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
SNonly_grouped_df= data_file_pd.groupby(['SN'])
SNonly_grouped_df.count().head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aeri79</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aesririam61</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aesurstilis64</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
count_df=pd.DataFrame(SNonly_grouped_df.count())
count_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aeri79</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aesririam61</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aesurstilis64</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
count_df.reset_index(inplace=True)
count_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
count_df=count_df[["SN", "Item Name"]]
count_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Item Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
SNonly_grouped_df.mean().head()
avg_p=pd.DataFrame(SNonly_grouped_df.mean())
avg_p.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aeri79</th>
      <td>23.0</td>
      <td>107.0</td>
      <td>4.150</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>40.0</td>
      <td>148.0</td>
      <td>4.650</td>
    </tr>
    <tr>
      <th>Aesririam61</th>
      <td>39.0</td>
      <td>2.0</td>
      <td>2.650</td>
    </tr>
    <tr>
      <th>Aesurstilis64</th>
      <td>36.0</td>
      <td>139.0</td>
      <td>4.250</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>21.0</td>
      <td>47.0</td>
      <td>2.565</td>
    </tr>
  </tbody>
</table>
</div>




```python
avg_p.reset_index(inplace=True)
avg_p.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>23.0</td>
      <td>107.0</td>
      <td>4.150</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>40.0</td>
      <td>148.0</td>
      <td>4.650</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>39.0</td>
      <td>2.0</td>
      <td>2.650</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>36.0</td>
      <td>139.0</td>
      <td>4.250</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>21.0</td>
      <td>47.0</td>
      <td>2.565</td>
    </tr>
  </tbody>
</table>
</div>




```python
avg_p=avg_p[["SN", "Price"]]

avg_p.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>4.150</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>4.650</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>2.650</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>4.250</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>2.565</td>
    </tr>
  </tbody>
</table>
</div>




```python
sortmerge1 = pd.merge(count_df,avg_p, on="SN")
sortmerge1.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>1</td>
      <td>4.150</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>1</td>
      <td>4.650</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>1</td>
      <td>2.650</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>1</td>
      <td>4.250</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>2</td>
      <td>2.565</td>
    </tr>
  </tbody>
</table>
</div>




```python
sortmerge1=sortmerge1.rename(columns={"Item Name":"Purchase Count","Price":"Average Purchase Price"})
sortmerge1.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>1</td>
      <td>4.150</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>1</td>
      <td>4.650</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>1</td>
      <td>2.650</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>1</td>
      <td>4.250</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>2</td>
      <td>2.565</td>
    </tr>
  </tbody>
</table>
</div>




```python
SNonly_grouped_df= data_file_pd.groupby(['SN'])

SNonly_grouped_df.sum().head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aeri79</th>
      <td>23</td>
      <td>107</td>
      <td>4.15</td>
    </tr>
    <tr>
      <th>Aerithllora36</th>
      <td>40</td>
      <td>148</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>Aesririam61</th>
      <td>39</td>
      <td>2</td>
      <td>2.65</td>
    </tr>
    <tr>
      <th>Aesurstilis64</th>
      <td>36</td>
      <td>139</td>
      <td>4.25</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>42</td>
      <td>94</td>
      <td>5.13</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_df=pd.DataFrame(SNonly_grouped_df.sum())
total_df.head()
total_df.reset_index(inplace=True)
total_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>23</td>
      <td>107</td>
      <td>4.15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>40</td>
      <td>148</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>39</td>
      <td>2</td>
      <td>2.65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>36</td>
      <td>139</td>
      <td>4.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>42</td>
      <td>94</td>
      <td>5.13</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_df=total_df[["SN","Price"]]
total_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>4.15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>2.65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>4.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>5.13</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_df=total_df.rename(columns={"Price":"Total Purchase Value"})
total_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>4.15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>2.65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>4.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>5.13</td>
    </tr>
  </tbody>
</table>
</div>




```python
Top_Spenders = pd.merge(sortmerge1,total_df, on="SN")
Top_Spenders.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aeri79</td>
      <td>1</td>
      <td>4.150</td>
      <td>4.15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aerithllora36</td>
      <td>1</td>
      <td>4.650</td>
      <td>4.65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aesririam61</td>
      <td>1</td>
      <td>2.650</td>
      <td>2.65</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aesurstilis64</td>
      <td>1</td>
      <td>4.250</td>
      <td>4.25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>2</td>
      <td>2.565</td>
      <td>5.13</td>
    </tr>
  </tbody>
</table>
</div>




```python
sort_df = Top_Spenders.sort_values("Total Purchase Value", ascending=False)
sort_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SN</th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>63</th>
      <td>Sundaky74</td>
      <td>2</td>
      <td>3.705</td>
      <td>7.41</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aidaira26</td>
      <td>2</td>
      <td>2.565</td>
      <td>5.13</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Eusty71</td>
      <td>1</td>
      <td>4.810</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Chanirra64</td>
      <td>1</td>
      <td>4.780</td>
      <td>4.78</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Alarap40</td>
      <td>1</td>
      <td>4.710</td>
      <td>4.71</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
with open("purchase_data2.json") as datafile:
    data = json.load(datafile)
data_file_pd = pd.DataFrame(data)
data_file_pd.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
id_grouped_df= data_file_pd.groupby(["Item Name"])
id_grouped_df.count().head()
totalID_df=pd.DataFrame(id_grouped_df.count())
totalID_df.head()
totalID_df.reset_index(inplace=True)
totalID_df.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alpha, Oath of Zeal</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcane Gem</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blade of the Grave</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
totalID_df=totalID_df[["Item Name","Item ID"]]
totalID_df
totalID_df=totalID_df.rename(columns={"Item ID":"Purchase Count"})
totalID_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alpha, Oath of Zeal</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcane Gem</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blade of the Grave</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
id_grouped_df.mean().head()
totalID2_df=pd.DataFrame(id_grouped_df.mean())
totalID2_df.head()
totalID2_df.reset_index(inplace=True)
totalID2_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alpha, Oath of Zeal</td>
      <td>17.0</td>
      <td>79.0</td>
      <td>1.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>27.5</td>
      <td>93.0</td>
      <td>4.49</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcane Gem</td>
      <td>25.0</td>
      <td>84.0</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>20.5</td>
      <td>90.0</td>
      <td>4.12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blade of the Grave</td>
      <td>16.0</td>
      <td>172.0</td>
      <td>2.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
totalID2_df=totalID2_df[["Item Name","Item ID","Price"]]
totalID2_df.head()

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alpha, Oath of Zeal</td>
      <td>79.0</td>
      <td>1.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>93.0</td>
      <td>4.49</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcane Gem</td>
      <td>84.0</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>90.0</td>
      <td>4.12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blade of the Grave</td>
      <td>172.0</td>
      <td>2.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
idmerge1 = pd.merge(totalID_df,totalID2_df, on="Item Name")
idmerge1.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alpha, Oath of Zeal</td>
      <td>1</td>
      <td>79.0</td>
      <td>1.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>2</td>
      <td>93.0</td>
      <td>4.49</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcane Gem</td>
      <td>1</td>
      <td>84.0</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>2</td>
      <td>90.0</td>
      <td>4.12</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blade of the Grave</td>
      <td>1</td>
      <td>172.0</td>
      <td>2.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
id_grouped_df.sum().head()
totalID3_df=pd.DataFrame(id_grouped_df.sum())
totalID3_df.head()
totalID3_df.reset_index(inplace=True)
totalID3_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alpha, Oath of Zeal</td>
      <td>17</td>
      <td>79</td>
      <td>1.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>55</td>
      <td>186</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcane Gem</td>
      <td>25</td>
      <td>84</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>41</td>
      <td>180</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blade of the Grave</td>
      <td>16</td>
      <td>172</td>
      <td>2.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
totalID3_df=totalID3_df[["Item Name","Price"]]
totalID3_df
totalID3_df=totalID3_df.rename(columns={"Price":"Total Purchase Value"})
totalID3_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alpha, Oath of Zeal</td>
      <td>1.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcane Gem</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blade of the Grave</td>
      <td>2.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
Popular_Items= pd.merge(idmerge1,totalID3_df, on="Item Name")
Popular_Items.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alpha, Oath of Zeal</td>
      <td>1</td>
      <td>79.0</td>
      <td>1.31</td>
      <td>1.31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>2</td>
      <td>93.0</td>
      <td>4.49</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Arcane Gem</td>
      <td>1</td>
      <td>84.0</td>
      <td>4.81</td>
      <td>4.81</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>2</td>
      <td>90.0</td>
      <td>4.12</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Blade of the Grave</td>
      <td>1</td>
      <td>172.0</td>
      <td>2.71</td>
      <td>2.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
sort_Popular_Items =Popular_Items.sort_values("Purchase Count", ascending=False)
sort_Popular_Items.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>31</th>
      <td>Mourning Blade</td>
      <td>3</td>
      <td>94.0</td>
      <td>3.64</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Deadline, Voice Of Subtlety</td>
      <td>2</td>
      <td>98.0</td>
      <td>1.29</td>
      <td>2.58</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Stormcaller</td>
      <td>2</td>
      <td>180.0</td>
      <td>2.77</td>
      <td>5.54</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Relentless Iron Skewer</td>
      <td>2</td>
      <td>176.0</td>
      <td>2.12</td>
      <td>4.24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>2</td>
      <td>93.0</td>
      <td>4.49</td>
      <td>8.98</td>
    </tr>
  </tbody>
</table>
</div>



# **Most Profitable Items**


```python
sort_Profitable_Items =Popular_Items.sort_values("Total Purchase Value", ascending=False)
sort_Profitable_Items.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Purchase Count</th>
      <th>Item ID</th>
      <th>Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>31</th>
      <td>Mourning Blade</td>
      <td>3</td>
      <td>94.0</td>
      <td>3.64</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Heartstriker, Legacy of the Light</td>
      <td>2</td>
      <td>117.0</td>
      <td>4.71</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Apocalyptic Battlescythe</td>
      <td>2</td>
      <td>93.0</td>
      <td>4.49</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Betrayer</td>
      <td>2</td>
      <td>90.0</td>
      <td>4.12</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Feral Katana</td>
      <td>2</td>
      <td>154.0</td>
      <td>4.11</td>
      <td>8.22</td>
    </tr>
  </tbody>
</table>
</div>


