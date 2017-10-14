

```python
import pandas as pd
import json
```


```python
with open("purchase_data_3.json") as datafile:
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
      <td>24</td>
      <td>Female</td>
      <td>69</td>
      <td>Frenzy, Defender of the Harvest</td>
      <td>4.82</td>
      <td>Lirtjaskan85</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>Female</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>4.12</td>
      <td>Chanjask65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>Female</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>2.67</td>
      <td>Aerithllora36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Aeralria27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>28</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>4.60</td>
      <td>Haisrisuir60</td>
    </tr>
  </tbody>
</table>
</div>



# **Player Count**


```python
SN_unique=data_file_pd["SN"].value_counts()
SN_unique.head(10)
```




    Lirtilsa71      4
    Chamalo71       4
    Chamistast30    4
    Strithenu87     4
    Qilanrion65     3
    Lisjaskya84     3
    Mindosia50      3
    Aethe80         3
    Aeralria27      3
    Frichistan93    3
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
      <td>581</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Total)


```python
Number_of_Unique_Items=data_file_pd["Item Name"].nunique()
Number_of_Unique_Items
```




    178




```python
Average_Purchase_Price = data_file_pd["Price"].mean()
Average_Purchase_Price

```




    3.03226923076923




```python
Total_Number_of_Purchases=data_file_pd["Item Name"].count()
Total_Number_of_Purchases
```




    780




```python
Total_Revenue=data_file_pd["Price"].sum()
Total_Revenue
```




    2365.169999999999




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
      <td>178</td>
      <td>3.03</td>
      <td>780</td>
      <td>2365.17</td>
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
      <td>178</td>
      <td>$ 3.03</td>
      <td>780</td>
      <td>$ 2,365.17</td>
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
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aedaip85</th>
      <th>Female</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <th>Male</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
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
      <td>21.0</td>
      <td>105.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <th>Male</th>
      <td>23.0</td>
      <td>55.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>Aedaip85</th>
      <th>Female</th>
      <td>24.0</td>
      <td>128.0</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <th>Male</th>
      <td>24.0</td>
      <td>72.0</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <th>Male</th>
      <td>7.0</td>
      <td>106.0</td>
      <td>3.72</td>
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
      <td>21.0</td>
      <td>105.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>Male</td>
      <td>23.0</td>
      <td>55.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>Female</td>
      <td>24.0</td>
      <td>128.0</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>Male</td>
      <td>24.0</td>
      <td>72.0</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>Male</td>
      <td>7.0</td>
      <td>106.0</td>
      <td>3.72</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_gender = len(game_comparison["SN"].unique())
total_gender
```




    581




```python
Male_Players = game_comparison["Gender"].value_counts()["Male"]
Male_Players
```




    475




```python
Female_Players = game_comparison["Gender"].value_counts()["Female"]
Female_Players
```




    99




```python
Other_Non_Disclosed = total_gender - Male_Players - Female_Players
Other_Non_Disclosed
```




    7




```python
male_percent = (Male_Players/total_gender) * 100
male_percent
```




    81.755593803786581




```python
female_percent = (Female_Players/total_gender) * 100
female_percent
```




    17.039586919104991




```python
Other_Non_Disclosed_percent = (Other_Non_Disclosed/total_gender) * 100
Other_Non_Disclosed_percent
```




    1.2048192771084338




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
      <td>81.76</td>
      <td>475</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.04</td>
      <td>99</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>1.20</td>
      <td>7</td>
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
      <th>3</th>
      <td>24</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Aeralria27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>28</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>4.60</td>
      <td>Haisrisuir60</td>
    </tr>
    <tr>
      <th>5</th>
      <td>17</td>
      <td>Male</td>
      <td>112</td>
      <td>Worldbreaker</td>
      <td>2.43</td>
      <td>Alaesu77</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20</td>
      <td>Male</td>
      <td>2</td>
      <td>Verdict</td>
      <td>3.45</td>
      <td>Ilosia88</td>
    </tr>
    <tr>
      <th>7</th>
      <td>25</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Zhestim56</td>
    </tr>
  </tbody>
</table>
</div>




```python
male_purchase_Count=len(male_df)
male_purchase_Count
```




    642




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
      <th>0</th>
      <td>24</td>
      <td>Female</td>
      <td>69</td>
      <td>Frenzy, Defender of the Harvest</td>
      <td>4.82</td>
      <td>Lirtjaskan85</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>Female</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>4.12</td>
      <td>Chanjask65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>Female</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>2.67</td>
      <td>Aerithllora36</td>
    </tr>
    <tr>
      <th>8</th>
      <td>25</td>
      <td>Female</td>
      <td>150</td>
      <td>Deathraze</td>
      <td>4.82</td>
      <td>Lisassa26</td>
    </tr>
    <tr>
      <th>10</th>
      <td>18</td>
      <td>Female</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>1.76</td>
      <td>Lisossan98</td>
    </tr>
  </tbody>
</table>
</div>




```python
female_purchase_Count=len(female_df)
female_purchase_Count
```




    130




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
      <th>86</th>
      <td>9</td>
      <td>Other / Non-Disclosed</td>
      <td>171</td>
      <td>Scalpel</td>
      <td>1.74</td>
      <td>Eusri26</td>
    </tr>
    <tr>
      <th>162</th>
      <td>9</td>
      <td>Other / Non-Disclosed</td>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>3.59</td>
      <td>Iduelis31</td>
    </tr>
    <tr>
      <th>168</th>
      <td>22</td>
      <td>Other / Non-Disclosed</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Jiskassan80</td>
    </tr>
    <tr>
      <th>183</th>
      <td>22</td>
      <td>Other / Non-Disclosed</td>
      <td>141</td>
      <td>Persuasion</td>
      <td>3.57</td>
      <td>Aisurphos78</td>
    </tr>
    <tr>
      <th>212</th>
      <td>16</td>
      <td>Other / Non-Disclosed</td>
      <td>96</td>
      <td>Blood-Forged Skeletal Spine</td>
      <td>1.79</td>
      <td>Tanimnya91</td>
    </tr>
  </tbody>
</table>
</div>




```python
other_purchase_Count=len(other_df)
other_purchase_Count
```




    8




```python
male_Average_Purchase_Price = male_df["Price"].mean()
male_Average_Purchase_Price
```




    3.0303894080996847




```python
female_Average_Purchase_Price = female_df["Price"].mean()
female_Average_Purchase_Price
```




    3.0446153846153843




```python
other_Average_Purchase_Price = other_df["Price"].mean()
other_Average_Purchase_Price 
```




    2.9824999999999995




```python
male_Total_Purchase_Value = male_df["Price"].sum()
male_Total_Purchase_Value
```




    1945.5099999999977




```python
female_Total_Purchase_Value = female_df["Price"].sum()
female_Total_Purchase_Value
```




    395.79999999999995




```python
other_total_Purchase_Price = other_df["Price"].mean()
other_total_Purchase_Price 

```




    2.9824999999999995




```python
male_Normalized_Totals = male_Total_Purchase_Value/Male_Players
male_Normalized_Totals
```




    4.0958105263157849




```python
female_Normalized_Totals = female_Total_Purchase_Value/Female_Players
female_Normalized_Totals
```




    3.9979797979797973




```python
other_Normalized_Totals = other_total_Purchase_Price/Other_Non_Disclosed
other_Normalized_Totals
```




    0.42607142857142849




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
      <td>642</td>
      <td>3.030389</td>
      <td>1945.5100</td>
      <td>4.095811</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>130</td>
      <td>3.044615</td>
      <td>395.8000</td>
      <td>3.997980</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>8</td>
      <td>2.982500</td>
      <td>2.9825</td>
      <td>0.426071</td>
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
      <td>642</td>
      <td>$3.03</td>
      <td>$1,945.51</td>
      <td>$4.10</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>130</td>
      <td>$3.04</td>
      <td>$395.80</td>
      <td>$4.00</td>
    </tr>
    <tr>
      <th>Other_Non_Disclosed</th>
      <td>8</td>
      <td>$2.98</td>
      <td>$2.98</td>
      <td>$0.43</td>
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




    0      20-24
    1      10-14
    2      20-24
    3      20-24
    4      25-29
    5      15-19
    6      15-19
    7      20-24
    8      20-24
    9      20-24
    10     15-19
    11     35-39
    12     25-29
    13     20-24
    14     10-14
    15     15-19
    16     15-19
    17     25-29
    18     20-24
    19     15-19
    20     30-34
    21     35-39
    22     25-29
    23     35-39
    24     35-39
    25     25-29
    26     30-34
    27     20-24
    28       >40
    29     30-34
           ...  
    750    20-24
    751    20-24
    752    25-29
    753    20-24
    754    15-19
    755      <10
    756    20-24
    757      <10
    758    10-14
    759    20-24
    760    10-14
    761    25-29
    762    20-24
    763    15-19
    764    15-19
    765    10-14
    766    20-24
    767    20-24
    768    25-29
    769      <10
    770    20-24
    771    10-14
    772    35-39
    773    35-39
    774      <10
    775    20-24
    776    15-19
    777    20-24
    778    30-34
    779    15-19
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
      <td>24</td>
      <td>Female</td>
      <td>69</td>
      <td>Frenzy, Defender of the Harvest</td>
      <td>4.82</td>
      <td>Lirtjaskan85</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>Female</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>4.12</td>
      <td>Chanjask65</td>
      <td>10-14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>Female</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>2.67</td>
      <td>Aerithllora36</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Aeralria27</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>28</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>4.60</td>
      <td>Haisrisuir60</td>
      <td>25-29</td>
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
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>173</td>
      <td>173</td>
      <td>173</td>
      <td>173</td>
      <td>173</td>
      <td>173</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>322</td>
      <td>322</td>
      <td>322</td>
      <td>322</td>
      <td>322</td>
      <td>322</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>77</td>
      <td>77</td>
      <td>77</td>
      <td>77</td>
      <td>77</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>53</td>
      <td>53</td>
      <td>53</td>
      <td>53</td>
      <td>53</td>
      <td>53</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>45</td>
      <td>45</td>
      <td>45</td>
      <td>45</td>
      <td>45</td>
      <td>45</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
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
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
      <td>39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>173</td>
      <td>173</td>
      <td>173</td>
      <td>173</td>
      <td>173</td>
      <td>173</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>322</td>
      <td>322</td>
      <td>322</td>
      <td>322</td>
      <td>322</td>
      <td>322</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>77</td>
      <td>77</td>
      <td>77</td>
      <td>77</td>
      <td>77</td>
      <td>77</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>53</td>
      <td>53</td>
      <td>53</td>
      <td>53</td>
      <td>53</td>
      <td>53</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>45</td>
      <td>45</td>
      <td>45</td>
      <td>45</td>
      <td>45</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
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
      <td>39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>173</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>322</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>77</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>53</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>6</td>
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
      <td>39</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>173</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>322</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>77</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>53</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>6</td>
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
      <td>8.025641</td>
      <td>90.102564</td>
      <td>2.922308</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>13.861538</td>
      <td>89.138462</td>
      <td>3.026923</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>18.705202</td>
      <td>85.919075</td>
      <td>3.062659</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>23.043478</td>
      <td>94.295031</td>
      <td>2.991677</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>28.376623</td>
      <td>86.376623</td>
      <td>3.154935</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>33.264151</td>
      <td>81.226415</td>
      <td>2.778679</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>38.022222</td>
      <td>109.355556</td>
      <td>3.279556</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>43.500000</td>
      <td>80.500000</td>
      <td>3.918333</td>
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
      <td>8.025641</td>
      <td>90.102564</td>
      <td>2.922308</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>13.861538</td>
      <td>89.138462</td>
      <td>3.026923</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>18.705202</td>
      <td>85.919075</td>
      <td>3.062659</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>23.043478</td>
      <td>94.295031</td>
      <td>2.991677</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>28.376623</td>
      <td>86.376623</td>
      <td>3.154935</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>33.264151</td>
      <td>81.226415</td>
      <td>2.778679</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>38.022222</td>
      <td>109.355556</td>
      <td>3.279556</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>43.500000</td>
      <td>80.500000</td>
      <td>3.918333</td>
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
      <td>2.922308</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>3.026923</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>3.062659</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>2.991677</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>3.154935</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>2.778679</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>3.279556</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3.918333</td>
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
      <td>2.922308</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>3.026923</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>3.062659</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>2.991677</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>3.154935</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>2.778679</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>3.279556</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>3.918333</td>
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
      <td>39</td>
      <td>2.922308</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>65</td>
      <td>3.026923</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>173</td>
      <td>3.062659</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>322</td>
      <td>2.991677</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>77</td>
      <td>3.154935</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>53</td>
      <td>2.778679</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>45</td>
      <td>3.279556</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>6</td>
      <td>3.918333</td>
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
      <td>313</td>
      <td>3514</td>
      <td>113.97</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>901</td>
      <td>5794</td>
      <td>196.75</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>3236</td>
      <td>14864</td>
      <td>529.84</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>7420</td>
      <td>30363</td>
      <td>963.32</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>2185</td>
      <td>6651</td>
      <td>242.93</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>1763</td>
      <td>4305</td>
      <td>147.27</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>1711</td>
      <td>4921</td>
      <td>147.58</td>
    </tr>
    <tr>
      <th>&gt;40</th>
      <td>261</td>
      <td>483</td>
      <td>23.51</td>
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
      <td>313</td>
      <td>3514</td>
      <td>113.97</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>901</td>
      <td>5794</td>
      <td>196.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>3236</td>
      <td>14864</td>
      <td>529.84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>7420</td>
      <td>30363</td>
      <td>963.32</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>2185</td>
      <td>6651</td>
      <td>242.93</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>1763</td>
      <td>4305</td>
      <td>147.27</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>1711</td>
      <td>4921</td>
      <td>147.58</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>261</td>
      <td>483</td>
      <td>23.51</td>
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
      <td>113.97</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>196.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>529.84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>963.32</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>242.93</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>147.27</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>147.58</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>23.51</td>
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
      <td>113.97</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>196.75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>529.84</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>963.32</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>242.93</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>147.27</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>147.58</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>23.51</td>
    </tr>
  </tbody>
</table>
</div>




```python
Normalized_total=sum2_df["Total Purchase Value"]/pc_df["SN"].nunique()
Normalized_total
```




    0     14.24625
    1     24.59375
    2     66.23000
    3    120.41500
    4     30.36625
    5     18.40875
    6     18.44750
    7      2.93875
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
      <td>113.97</td>
      <td>14.24625</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>196.75</td>
      <td>24.59375</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>529.84</td>
      <td>66.23000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>963.32</td>
      <td>120.41500</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>242.93</td>
      <td>30.36625</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>147.27</td>
      <td>18.40875</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>147.58</td>
      <td>18.44750</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>23.51</td>
      <td>2.93875</td>
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
      <td>39</td>
      <td>2.922308</td>
      <td>113.97</td>
      <td>14.24625</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>65</td>
      <td>3.026923</td>
      <td>196.75</td>
      <td>24.59375</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>173</td>
      <td>3.062659</td>
      <td>529.84</td>
      <td>66.23000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>322</td>
      <td>2.991677</td>
      <td>963.32</td>
      <td>120.41500</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>77</td>
      <td>3.154935</td>
      <td>242.93</td>
      <td>30.36625</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>53</td>
      <td>2.778679</td>
      <td>147.27</td>
      <td>18.40875</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>45</td>
      <td>3.279556</td>
      <td>147.58</td>
      <td>18.44750</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>6</td>
      <td>3.918333</td>
      <td>23.51</td>
      <td>2.93875</td>
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
      <td>39</td>
      <td>2.922308</td>
      <td>113.97</td>
      <td>14.24625</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>65</td>
      <td>3.026923</td>
      <td>196.75</td>
      <td>24.59375</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>173</td>
      <td>3.062659</td>
      <td>529.84</td>
      <td>66.23000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>322</td>
      <td>2.991677</td>
      <td>963.32</td>
      <td>120.41500</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>77</td>
      <td>3.154935</td>
      <td>242.93</td>
      <td>30.36625</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>53</td>
      <td>2.778679</td>
      <td>147.27</td>
      <td>18.40875</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>45</td>
      <td>3.279556</td>
      <td>147.58</td>
      <td>18.44750</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>6</td>
      <td>3.918333</td>
      <td>23.51</td>
      <td>2.93875</td>
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
      <td>39</td>
      <td>$ 2.92</td>
      <td>$ 113.97</td>
      <td>$ 14.25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10-14</td>
      <td>65</td>
      <td>$ 3.03</td>
      <td>$ 196.75</td>
      <td>$ 24.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>15-19</td>
      <td>173</td>
      <td>$ 3.06</td>
      <td>$ 529.84</td>
      <td>$ 66.23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20-24</td>
      <td>322</td>
      <td>$ 2.99</td>
      <td>$ 963.32</td>
      <td>$ 120.42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>25-29</td>
      <td>77</td>
      <td>$ 3.15</td>
      <td>$ 242.93</td>
      <td>$ 30.37</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30-34</td>
      <td>53</td>
      <td>$ 2.78</td>
      <td>$ 147.27</td>
      <td>$ 18.41</td>
    </tr>
    <tr>
      <th>6</th>
      <td>35-39</td>
      <td>45</td>
      <td>$ 3.28</td>
      <td>$ 147.58</td>
      <td>$ 18.45</td>
    </tr>
    <tr>
      <th>7</th>
      <td>&gt;40</td>
      <td>6</td>
      <td>$ 3.92</td>
      <td>$ 23.51</td>
      <td>$ 2.94</td>
    </tr>
  </tbody>
</table>
</div>



# Top Spenders


```python
with open("purchase_data_3.json") as datafile:
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
      <td>24</td>
      <td>Female</td>
      <td>69</td>
      <td>Frenzy, Defender of the Harvest</td>
      <td>4.82</td>
      <td>Lirtjaskan85</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>Female</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>4.12</td>
      <td>Chanjask65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>Female</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>2.67</td>
      <td>Aerithllora36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Aeralria27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>28</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>4.60</td>
      <td>Haisrisuir60</td>
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
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aedaip85</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
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
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aedaip85</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
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
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
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
      <td>21.0</td>
      <td>105.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>23.0</td>
      <td>55.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>Aedaip85</th>
      <td>24.0</td>
      <td>128.0</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>24.0</td>
      <td>72.0</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>7.0</td>
      <td>106.0</td>
      <td>3.72</td>
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
      <td>21.0</td>
      <td>105.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>23.0</td>
      <td>55.0</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>24.0</td>
      <td>128.0</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>24.0</td>
      <td>72.0</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>7.0</td>
      <td>106.0</td>
      <td>3.72</td>
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
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>3.72</td>
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
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>1</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>1</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>1</td>
      <td>3.72</td>
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
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>1</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>1</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2</td>
      <td>1.67</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>1</td>
      <td>3.72</td>
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
      <td>21</td>
      <td>105</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>Aduephos78</th>
      <td>23</td>
      <td>55</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>Aedaip85</th>
      <td>24</td>
      <td>128</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>Aela49</th>
      <td>48</td>
      <td>144</td>
      <td>3.34</td>
    </tr>
    <tr>
      <th>Aelalis34</th>
      <td>7</td>
      <td>106</td>
      <td>3.72</td>
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
      <td>21</td>
      <td>105</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>23</td>
      <td>55</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>24</td>
      <td>128</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>48</td>
      <td>144</td>
      <td>3.34</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>7</td>
      <td>106</td>
      <td>3.72</td>
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
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>3.34</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>3.72</td>
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
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>3.34</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>3.72</td>
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
      <td>1.59</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aduephos78</td>
      <td>1</td>
      <td>1.59</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aedaip85</td>
      <td>1</td>
      <td>2.78</td>
      <td>2.78</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aela49</td>
      <td>2</td>
      <td>1.67</td>
      <td>3.34</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aelalis34</td>
      <td>1</td>
      <td>3.72</td>
      <td>3.72</td>
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
      <th>81</th>
      <td>Chamalo71</td>
      <td>4</td>
      <td>3.362500</td>
      <td>13.45</td>
    </tr>
    <tr>
      <th>492</th>
      <td>Strithenu87</td>
      <td>4</td>
      <td>3.207500</td>
      <td>12.83</td>
    </tr>
    <tr>
      <th>371</th>
      <td>Mindosia50</td>
      <td>3</td>
      <td>4.003333</td>
      <td>12.01</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Aeralria27</td>
      <td>3</td>
      <td>3.793333</td>
      <td>11.38</td>
    </tr>
    <tr>
      <th>133</th>
      <td>Eudai71</td>
      <td>3</td>
      <td>3.790000</td>
      <td>11.37</td>
    </tr>
  </tbody>
</table>
</div>



# Most Popular Items


```python
with open("purchase_data_3.json") as datafile:
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
      <td>24</td>
      <td>Female</td>
      <td>69</td>
      <td>Frenzy, Defender of the Harvest</td>
      <td>4.82</td>
      <td>Lirtjaskan85</td>
    </tr>
    <tr>
      <th>1</th>
      <td>12</td>
      <td>Female</td>
      <td>75</td>
      <td>Brutality Ivory Warmace</td>
      <td>4.12</td>
      <td>Chanjask65</td>
    </tr>
    <tr>
      <th>2</th>
      <td>21</td>
      <td>Female</td>
      <td>114</td>
      <td>Yearning Mageblade</td>
      <td>2.67</td>
      <td>Aerithllora36</td>
    </tr>
    <tr>
      <th>3</th>
      <td>24</td>
      <td>Male</td>
      <td>130</td>
      <td>Alpha</td>
      <td>4.53</td>
      <td>Aeralria27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>28</td>
      <td>Male</td>
      <td>9</td>
      <td>Thorn, Conqueror of the Corrupted</td>
      <td>4.60</td>
      <td>Haisrisuir60</td>
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
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
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
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>4</td>
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
      <td>20.333333</td>
      <td>162.0</td>
      <td>2.47</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>23.500000</td>
      <td>137.0</td>
      <td>1.37</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>27.250000</td>
      <td>120.0</td>
      <td>4.93</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>24.800000</td>
      <td>130.0</td>
      <td>4.53</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>26.000000</td>
      <td>79.0</td>
      <td>4.99</td>
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
      <td>2.47</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>137.0</td>
      <td>1.37</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>120.0</td>
      <td>4.93</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>130.0</td>
      <td>4.53</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>79.0</td>
      <td>4.99</td>
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
      <td>2.47</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>4</td>
      <td>137.0</td>
      <td>1.37</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>8</td>
      <td>120.0</td>
      <td>4.93</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>5</td>
      <td>130.0</td>
      <td>4.53</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>4</td>
      <td>79.0</td>
      <td>4.99</td>
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
      <td>61</td>
      <td>486</td>
      <td>7.41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>94</td>
      <td>548</td>
      <td>5.48</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>218</td>
      <td>960</td>
      <td>39.44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>124</td>
      <td>650</td>
      <td>22.65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>104</td>
      <td>316</td>
      <td>19.96</td>
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
      <td>7.41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>5.48</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>39.44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>22.65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>19.96</td>
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
      <td>2.47</td>
      <td>7.41</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aetherius, Boon of the Blessed</td>
      <td>4</td>
      <td>137.0</td>
      <td>1.37</td>
      <td>5.48</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>8</td>
      <td>120.0</td>
      <td>4.93</td>
      <td>39.44</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alpha</td>
      <td>5</td>
      <td>130.0</td>
      <td>4.53</td>
      <td>22.65</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alpha, Oath of Zeal</td>
      <td>4</td>
      <td>79.0</td>
      <td>4.99</td>
      <td>19.96</td>
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
      <th>70</th>
      <td>Hatred</td>
      <td>11</td>
      <td>52.000000</td>
      <td>4.59</td>
      <td>50.49</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Final Critic</td>
      <td>11</td>
      <td>95.272727</td>
      <td>2.70</td>
      <td>29.70</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Primitive Blade</td>
      <td>9</td>
      <td>174.000000</td>
      <td>1.39</td>
      <td>12.51</td>
    </tr>
    <tr>
      <th>87</th>
      <td>Misery's End</td>
      <td>9</td>
      <td>111.000000</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <td>The Oculus, Token of Lost Worlds</td>
      <td>8</td>
      <td>49.000000</td>
      <td>4.61</td>
      <td>36.88</td>
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
      <th>70</th>
      <td>Hatred</td>
      <td>11</td>
      <td>52.0</td>
      <td>4.59</td>
      <td>50.49</td>
    </tr>
    <tr>
      <th>87</th>
      <td>Misery's End</td>
      <td>9</td>
      <td>111.0</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Agatha</td>
      <td>8</td>
      <td>120.0</td>
      <td>4.93</td>
      <td>39.44</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Apocalyptic Battlescythe</td>
      <td>8</td>
      <td>93.0</td>
      <td>4.85</td>
      <td>38.80</td>
    </tr>
    <tr>
      <th>145</th>
      <td>The Oculus, Token of Lost Worlds</td>
      <td>8</td>
      <td>49.0</td>
      <td>4.61</td>
      <td>36.88</td>
    </tr>
  </tbody>
</table>
</div>


