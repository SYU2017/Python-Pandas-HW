

```python
import pandas as pd
import json
```


```python
with open("purchase_data.json") as datafile:
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>



# **Player Count**


```python
SN_unique=data_file_pd["SN"].value_counts()
SN_unique.head(10)
```




    Undirrala66        5
    Hailaphos89        4
    Mindimnya67        4
    Saedue76           4
    Qarwen67           4
    Sondastan54        4
    Frichaya88         3
    Ialistidru50       3
    Tillyrin30         3
    Seorithstilis90    3
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
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Total)


```python
Number_of_Unique_Items=data_file_pd["Item Name"].nunique()
Number_of_Unique_Items
```




    179




```python
Average_Purchase_Price = data_file_pd["Price"].mean()
Average_Purchase_Price

```




    2.931192307692303




```python
Total_Number_of_Purchases=data_file_pd["Item Name"].count()
Total_Number_of_Purchases
```




    780




```python
Total_Revenue=data_file_pd["Price"].sum()
Total_Revenue
```




    2286.3299999999963




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
      <td>179</td>
      <td>2.93</td>
      <td>780</td>
      <td>2286.33</td>
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
      <td>179</td>
      <td>$ 2.93</td>
      <td>780</td>
      <td>$ 2,286.33</td>
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
      <th>Adairialis76</th>
      <th>Male</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <th>Male</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <th>Male</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <th>Male</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <th>Male</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
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
      <th>Adairialis76</th>
      <th>Male</th>
      <td>20.0</td>
      <td>44.000000</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <th>Male</th>
      <td>37.0</td>
      <td>115.000000</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <th>Male</th>
      <td>26.0</td>
      <td>100.333333</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <th>Male</th>
      <td>25.0</td>
      <td>44.000000</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <th>Male</th>
      <td>23.0</td>
      <td>63.000000</td>
      <td>1.270000</td>
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
      <td>Adairialis76</td>
      <td>Male</td>
      <td>20.0</td>
      <td>44.000000</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>Male</td>
      <td>37.0</td>
      <td>115.000000</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>Male</td>
      <td>26.0</td>
      <td>100.333333</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>Male</td>
      <td>25.0</td>
      <td>44.000000</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>Male</td>
      <td>23.0</td>
      <td>63.000000</td>
      <td>1.270000</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_gender = len(game_comparison["SN"].unique())
total_gender
```




    573




```python
Male_Players = game_comparison["Gender"].value_counts()["Male"]
Male_Players
```




    465




```python
Female_Players = game_comparison["Gender"].value_counts()["Female"]
Female_Players
```




    100




```python
Other_Non_Disclosed = total_gender - Male_Players - Female_Players
Other_Non_Disclosed
```




    8




```python
male_percent = (Male_Players/total_gender) * 100
male_percent
```




    81.15183246073299




```python
female_percent = (Female_Players/total_gender) * 100
female_percent
```




    17.452006980802793




```python
Other_Non_Disclosed_percent = (Other_Non_Disclosed/total_gender) * 100
Other_Non_Disclosed_percent
```




    1.3961605584642234




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
      <td>81.15</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>1.40</td>
      <td>8</td>
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
male_purchase_Count=len(male_df)
male_purchase_Count
```




    633




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
      <th>7</th>
      <td>29</td>
      <td>Female</td>
      <td>169</td>
      <td>Interrogator, Blood Blade of the Queen</td>
      <td>3.32</td>
      <td>Iathenudil29</td>
    </tr>
    <tr>
      <th>16</th>
      <td>22</td>
      <td>Female</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>1.14</td>
      <td>Sundista85</td>
    </tr>
    <tr>
      <th>17</th>
      <td>22</td>
      <td>Female</td>
      <td>59</td>
      <td>Lightning, Etcher of the King</td>
      <td>1.65</td>
      <td>Aenarap34</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11</td>
      <td>Female</td>
      <td>11</td>
      <td>Brimstone</td>
      <td>2.52</td>
      <td>Deural48</td>
    </tr>
    <tr>
      <th>29</th>
      <td>16</td>
      <td>Female</td>
      <td>45</td>
      <td>Glinting Glass Edge</td>
      <td>2.46</td>
      <td>Phaedai25</td>
    </tr>
  </tbody>
</table>
</div>




```python
female_purchase_Count=len(female_df)
female_purchase_Count
```




    136




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
      <th>177</th>
      <td>34</td>
      <td>Other / Non-Disclosed</td>
      <td>155</td>
      <td>War-Forged Gold Deflector</td>
      <td>3.73</td>
      <td>Assassa38</td>
    </tr>
    <tr>
      <th>209</th>
      <td>33</td>
      <td>Other / Non-Disclosed</td>
      <td>157</td>
      <td>Spada, Etcher of Hatred</td>
      <td>2.21</td>
      <td>Frichistasta59</td>
    </tr>
    <tr>
      <th>244</th>
      <td>21</td>
      <td>Other / Non-Disclosed</td>
      <td>183</td>
      <td>Dragon's Greatsword</td>
      <td>2.36</td>
      <td>Tyaerith73</td>
    </tr>
    <tr>
      <th>267</th>
      <td>33</td>
      <td>Other / Non-Disclosed</td>
      <td>65</td>
      <td>Conqueror Adamantite Mace</td>
      <td>1.96</td>
      <td>Frichistasta59</td>
    </tr>
    <tr>
      <th>276</th>
      <td>12</td>
      <td>Other / Non-Disclosed</td>
      <td>128</td>
      <td>Blazeguard, Reach of Eternity</td>
      <td>4.00</td>
      <td>Aillycal84</td>
    </tr>
  </tbody>
</table>
</div>




```python
other_purchase_Count=len(other_df)
other_purchase_Count
```




    11




```python
male_Average_Purchase_Price = male_df["Price"].mean()
male_Average_Purchase_Price
```




    2.9505213270142154




```python
female_Average_Purchase_Price = female_df["Price"].mean()
female_Average_Purchase_Price
```




    2.815514705882352




```python
other_Average_Purchase_Price = other_df["Price"].mean()
other_Average_Purchase_Price 
```




    3.2490909090909086




```python
male_Total_Purchase_Value = male_df["Price"].sum()
male_Total_Purchase_Value
```




    1867.6799999999985




```python
female_Total_Purchase_Value = female_df["Price"].sum()
female_Total_Purchase_Value
```




    382.90999999999985




```python
other_total_Purchase_Price = other_df["Price"].mean()
other_total_Purchase_Price 

```




    3.2490909090909086




```python
male_Normalized_Totals = male_Total_Purchase_Value/Male_Players
male_Normalized_Totals
```




    4.0165161290322544




```python
female_Normalized_Totals = female_Total_Purchase_Value/Female_Players
female_Normalized_Totals
```




    3.8290999999999986




```python
other_Normalized_Totals = other_total_Purchase_Price/Other_Non_Disclosed
other_Normalized_Totals
```




    0.40613636363636357




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
      <td>633</td>
      <td>2.950521</td>
      <td>1867.680000</td>
      <td>4.016516</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>2.815515</td>
      <td>382.910000</td>
      <td>3.829100</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>11</td>
      <td>3.249091</td>
      <td>3.249091</td>
      <td>0.406136</td>
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
      <td>633</td>
      <td>$2.95</td>
      <td>$1,867.68</td>
      <td>$4.02</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>$3.83</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>11</td>
      <td>$3.25</td>
      <td>$3.25</td>
      <td>$0.41</td>
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




    0      35-39
    1      20-24
    2      30-34
    3      20-24
    4      20-24
    5      15-19
    6      15-19
    7      25-29
    8      20-24
    9      30-34
    10     20-24
    11     15-19
    12     25-29
    13     20-24
    14     35-39
    15     20-24
    16     20-24
    17     20-24
    18     25-29
    19     30-34
    20     20-24
    21     10-14
    22     10-14
    23     15-19
    24     10-14
    25     20-24
    26     25-29
    27     30-34
    28     10-14
    29     15-19
           ...  
    750    20-24
    751    25-29
    752    10-14
    753    15-19
    754    30-34
    755    20-24
    756    20-24
    757    30-34
    758    15-19
    759    15-19
    760    25-29
    761    25-29
    762    35-39
    763    25-29
    764    20-24
    765    10-14
    766    20-24
    767    15-19
    768    20-24
    769    20-24
    770    20-24
    771    20-24
    772    10-14
    773    20-24
    774    20-24
    775    20-24
    776    10-14
    777    15-19
    778    15-19
    779    20-24
    Name: Age, Length: 780, dtype: category
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
      <td>35-39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
      <td>30-34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
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
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>78</td>
      <td>78</td>
      <td>78</td>
      <td>78</td>
      <td>78</td>
      <td>78</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>305</td>
      <td>305</td>
      <td>305</td>
      <td>305</td>
      <td>305</td>
      <td>305</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>58</td>
      <td>58</td>
      <td>58</td>
      <td>58</td>
      <td>58</td>
      <td>58</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>44</td>
      <td>44</td>
      <td>44</td>
      <td>44</td>
      <td>44</td>
      <td>44</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
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
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>78</td>
      <td>78</td>
      <td>78</td>
      <td>78</td>
      <td>78</td>
      <td>78</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
      <td>184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>305</td>
      <td>305</td>
      <td>305</td>
      <td>305</td>
      <td>305</td>
      <td>305</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
      <td>76</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>58</td>
      <td>58</td>
      <td>58</td>
      <td>58</td>
      <td>58</td>
      <td>58</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>44</td>
      <td>44</td>
      <td>44</td>
      <td>44</td>
      <td>44</td>
      <td>44</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
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
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>78</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>305</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>76</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>58</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>44</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3</td>
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
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>78</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>305</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>76</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>58</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>44</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3</td>
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
      <td>7.843750</td>
      <td>83.218750</td>
      <td>3.019375</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>13.987179</td>
      <td>91.435897</td>
      <td>2.873718</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>18.842391</td>
      <td>86.005435</td>
      <td>2.873587</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>23.163934</td>
      <td>89.085246</td>
      <td>2.959377</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>28.157895</td>
      <td>97.447368</td>
      <td>2.892368</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>32.810345</td>
      <td>104.327586</td>
      <td>3.073448</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>38.227273</td>
      <td>106.136364</td>
      <td>2.897500</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>43.333333</td>
      <td>97.000000</td>
      <td>2.880000</td>
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
      <td>7.843750</td>
      <td>83.218750</td>
      <td>3.019375</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>13.987179</td>
      <td>91.435897</td>
      <td>2.873718</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>18.842391</td>
      <td>86.005435</td>
      <td>2.873587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>23.163934</td>
      <td>89.085246</td>
      <td>2.959377</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>28.157895</td>
      <td>97.447368</td>
      <td>2.892368</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>32.810345</td>
      <td>104.327586</td>
      <td>3.073448</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>38.227273</td>
      <td>106.136364</td>
      <td>2.897500</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>43.333333</td>
      <td>97.000000</td>
      <td>2.880000</td>
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
      <td>3.019375</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>2.873718</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>2.873587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>2.959377</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>2.892368</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>3.073448</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>2.897500</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>2.880000</td>
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
      <td>3.019375</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>2.873718</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>2.873587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>2.959377</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>2.892368</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>3.073448</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>2.897500</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>2.880000</td>
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
      <td>32</td>
      <td>3.019375</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>78</td>
      <td>2.873718</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>184</td>
      <td>2.873587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>305</td>
      <td>2.959377</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>76</td>
      <td>2.892368</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>58</td>
      <td>3.073448</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>44</td>
      <td>2.897500</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3</td>
      <td>2.880000</td>
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
      <td>251</td>
      <td>2663</td>
      <td>96.62</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>1091</td>
      <td>7132</td>
      <td>224.15</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>3467</td>
      <td>15825</td>
      <td>528.74</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>7065</td>
      <td>27171</td>
      <td>902.61</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>2140</td>
      <td>7406</td>
      <td>219.82</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>1903</td>
      <td>6051</td>
      <td>178.26</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>1682</td>
      <td>4670</td>
      <td>127.49</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>130</td>
      <td>291</td>
      <td>8.64</td>
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
      <td>251</td>
      <td>2663</td>
      <td>96.62</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>1091</td>
      <td>7132</td>
      <td>224.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>3467</td>
      <td>15825</td>
      <td>528.74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>7065</td>
      <td>27171</td>
      <td>902.61</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>2140</td>
      <td>7406</td>
      <td>219.82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>1903</td>
      <td>6051</td>
      <td>178.26</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>1682</td>
      <td>4670</td>
      <td>127.49</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>130</td>
      <td>291</td>
      <td>8.64</td>
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
      <td>96.62</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>224.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>528.74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>902.61</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>219.82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>178.26</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>127.49</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>8.64</td>
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
      <td>96.62</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>224.15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>528.74</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>902.61</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>219.82</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>178.26</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>127.49</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>8.64</td>
    </tr>
  </tbody>
</table>
</div>




```python
Normalized_total=sum2_df["Total Purchase Value"]/pc_df["SN"].nunique()
Normalized_total
```




    0     12.07750
    1     28.01875
    2     66.09250
    3    112.82625
    4     27.47750
    5     22.28250
    6     15.93625
    7      1.08000
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
      <td>96.62</td>
      <td>12.07750</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>224.15</td>
      <td>28.01875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>528.74</td>
      <td>66.09250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>902.61</td>
      <td>112.82625</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>219.82</td>
      <td>27.47750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>178.26</td>
      <td>22.28250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>127.49</td>
      <td>15.93625</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>8.64</td>
      <td>1.08000</td>
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
      <td>32</td>
      <td>3.019375</td>
      <td>96.62</td>
      <td>12.07750</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>78</td>
      <td>2.873718</td>
      <td>224.15</td>
      <td>28.01875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>184</td>
      <td>2.873587</td>
      <td>528.74</td>
      <td>66.09250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>305</td>
      <td>2.959377</td>
      <td>902.61</td>
      <td>112.82625</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>76</td>
      <td>2.892368</td>
      <td>219.82</td>
      <td>27.47750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>58</td>
      <td>3.073448</td>
      <td>178.26</td>
      <td>22.28250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>44</td>
      <td>2.897500</td>
      <td>127.49</td>
      <td>15.93625</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3</td>
      <td>2.880000</td>
      <td>8.64</td>
      <td>1.08000</td>
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
      <td>32</td>
      <td>3.019375</td>
      <td>96.62</td>
      <td>12.07750</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>78</td>
      <td>2.873718</td>
      <td>224.15</td>
      <td>28.01875</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>184</td>
      <td>2.873587</td>
      <td>528.74</td>
      <td>66.09250</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>305</td>
      <td>2.959377</td>
      <td>902.61</td>
      <td>112.82625</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>76</td>
      <td>2.892368</td>
      <td>219.82</td>
      <td>27.47750</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>58</td>
      <td>3.073448</td>
      <td>178.26</td>
      <td>22.28250</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>44</td>
      <td>2.897500</td>
      <td>127.49</td>
      <td>15.93625</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3</td>
      <td>2.880000</td>
      <td>8.64</td>
      <td>1.08000</td>
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
      <td>32</td>
      <td>$ 3.02</td>
      <td>$ 96.62</td>
      <td>$ 12.08</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>78</td>
      <td>$ 2.87</td>
      <td>$ 224.15</td>
      <td>$ 28.02</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>184</td>
      <td>$ 2.87</td>
      <td>$ 528.74</td>
      <td>$ 66.09</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>305</td>
      <td>$ 2.96</td>
      <td>$ 902.61</td>
      <td>$ 112.83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>76</td>
      <td>$ 2.89</td>
      <td>$ 219.82</td>
      <td>$ 27.48</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>58</td>
      <td>$ 3.07</td>
      <td>$ 178.26</td>
      <td>$ 22.28</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>44</td>
      <td>$ 2.90</td>
      <td>$ 127.49</td>
      <td>$ 15.94</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3</td>
      <td>$ 2.88</td>
      <td>$ 8.64</td>
      <td>$ 1.08</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders


```python
with open("purchase_data.json") as datafile:
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
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
      <th>Adairialis76</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela59</th>
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
      <th>Adairialis76</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela59</th>
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
      <td>Adairialis76</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
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
      <td>Adairialis76</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>1</td>
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
      <th>Adairialis76</th>
      <td>20.0</td>
      <td>44.000000</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>37.0</td>
      <td>115.000000</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>26.0</td>
      <td>100.333333</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>25.0</td>
      <td>44.000000</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>23.0</td>
      <td>63.000000</td>
      <td>1.270000</td>
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
      <td>Adairialis76</td>
      <td>20.0</td>
      <td>44.000000</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>37.0</td>
      <td>115.000000</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>26.0</td>
      <td>100.333333</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>25.0</td>
      <td>44.000000</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>23.0</td>
      <td>63.000000</td>
      <td>1.270000</td>
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
      <td>Adairialis76</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>1.270000</td>
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
      <td>Adairialis76</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>3</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>3</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>1</td>
      <td>1.270000</td>
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
      <td>Adairialis76</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>3</td>
      <td>2.233333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>3</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>1</td>
      <td>2.460000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>1</td>
      <td>1.270000</td>
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
      <th>Adairialis76</th>
      <td>20</td>
      <td>44</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>111</td>
      <td>345</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>Aeduera68</th>
      <td>78</td>
      <td>301</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>25</td>
      <td>44</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>Aela59</th>
      <td>23</td>
      <td>63</td>
      <td>1.27</td>
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
      <td>Adairialis76</td>
      <td>20</td>
      <td>44</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>111</td>
      <td>345</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>78</td>
      <td>301</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>25</td>
      <td>44</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>23</td>
      <td>63</td>
      <td>1.27</td>
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
      <td>Adairialis76</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>1.27</td>
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
      <td>Adairialis76</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>1.27</td>
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
      <td>Adairialis76</td>
      <td>1</td>
      <td>2.460000</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>3</td>
      <td>2.233333</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aeduera68</td>
      <td>3</td>
      <td>1.933333</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>1</td>
      <td>2.460000</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aela59</td>
      <td>1</td>
      <td>1.270000</td>
      <td>1.27</td>
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
      <th>538</th>
      <td>Undirrala66</td>
      <td>5</td>
      <td>3.412000</td>
      <td>17.06</td>
    </tr>
    <tr>
      <th>428</th>
      <td>Saedue76</td>
      <td>4</td>
      <td>3.390000</td>
      <td>13.56</td>
    </tr>
    <tr>
      <th>354</th>
      <td>Mindimnya67</td>
      <td>4</td>
      <td>3.185000</td>
      <td>12.74</td>
    </tr>
    <tr>
      <th>181</th>
      <td>Haellysu29</td>
      <td>3</td>
      <td>4.243333</td>
      <td>12.73</td>
    </tr>
    <tr>
      <th>120</th>
      <td>Eoda93</td>
      <td>3</td>
      <td>3.860000</td>
      <td>11.58</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
with open("purchase_data.json") as datafile:
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
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
      <td>Abyssal Shard</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
      <td>7</td>
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
      <td>Abyssal Shard</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>7</td>
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
      <td>Abyssal Shard</td>
      <td>22.333333</td>
      <td>162.0</td>
      <td>2.04</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>19.500000</td>
      <td>137.0</td>
      <td>4.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>23.000000</td>
      <td>120.0</td>
      <td>1.91</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>23.285714</td>
      <td>130.0</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>22.571429</td>
      <td>79.0</td>
      <td>2.88</td>
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
      <td>Abyssal Shard</td>
      <td>162.0</td>
      <td>2.04</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>137.0</td>
      <td>4.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>120.0</td>
      <td>1.91</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>130.0</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>79.0</td>
      <td>2.88</td>
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
      <td>Abyssal Shard</td>
      <td>3</td>
      <td>162.0</td>
      <td>2.04</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>4</td>
      <td>137.0</td>
      <td>4.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>5</td>
      <td>120.0</td>
      <td>1.91</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>7</td>
      <td>130.0</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>7</td>
      <td>79.0</td>
      <td>2.88</td>
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
      <td>Abyssal Shard</td>
      <td>67</td>
      <td>486</td>
      <td>6.12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>78</td>
      <td>548</td>
      <td>19.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>115</td>
      <td>600</td>
      <td>9.55</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>163</td>
      <td>910</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>158</td>
      <td>553</td>
      <td>20.16</td>
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
      <td>Abyssal Shard</td>
      <td>6.12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>19.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>9.55</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>20.16</td>
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
      <td>Abyssal Shard</td>
      <td>3</td>
      <td>162.0</td>
      <td>2.04</td>
      <td>6.12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>4</td>
      <td>137.0</td>
      <td>4.75</td>
      <td>19.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>5</td>
      <td>120.0</td>
      <td>1.91</td>
      <td>9.55</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>7</td>
      <td>130.0</td>
      <td>1.56</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>7</td>
      <td>79.0</td>
      <td>2.88</td>
      <td>20.16</td>
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
      <th>56</th>
      <td>Final Critic</td>
      <td>14</td>
      <td>95.857143</td>
      <td>2.757143</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Arcane Gem</td>
      <td>11</td>
      <td>84.000000</td>
      <td>2.230000</td>
      <td>24.53</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Betrayal, Whisper of Grieving Widows</td>
      <td>11</td>
      <td>39.000000</td>
      <td>2.350000</td>
      <td>25.85</td>
    </tr>
    <tr>
      <th>137</th>
      <td>Stormcaller</td>
      <td>10</td>
      <td>105.000000</td>
      <td>3.465000</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>173</th>
      <td>Woeful Adamantite Claymore</td>
      <td>9</td>
      <td>175.000000</td>
      <td>1.240000</td>
      <td>11.16</td>
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
      <th>56</th>
      <td>Final Critic</td>
      <td>14</td>
      <td>95.857143</td>
      <td>2.757143</td>
      <td>38.60</td>
    </tr>
    <tr>
      <th>112</th>
      <td>Retribution Axe</td>
      <td>9</td>
      <td>34.000000</td>
      <td>4.140000</td>
      <td>37.26</td>
    </tr>
    <tr>
      <th>137</th>
      <td>Stormcaller</td>
      <td>10</td>
      <td>105.000000</td>
      <td>3.465000</td>
      <td>34.65</td>
    </tr>
    <tr>
      <th>132</th>
      <td>Spectral Diamond Doomblade</td>
      <td>7</td>
      <td>115.000000</td>
      <td>4.250000</td>
      <td>29.75</td>
    </tr>
    <tr>
      <th>96</th>
      <td>Orenmir</td>
      <td>6</td>
      <td>32.000000</td>
      <td>4.950000</td>
      <td>29.70</td>
    </tr>
  </tbody>
</table>
</div>


