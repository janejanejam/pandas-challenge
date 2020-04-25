### Heroes Of Pymoli Data Analysis
* Of the 1163 active players, the vast majority are male (84%). There also exists, a smaller, but notable proportion of female players (14%).

* Our peak age demographic falls between 20-24 (44.8%) with secondary groups falling between 15-19 (18.60%) and 25-29 (13.4%).  
-----

### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup
import pandas as pd
import pathlib

# File to Load (Remember to Change These)
file_to_load = pathlib.Path("Resources/purchase_data.csv")

# Read Purchasing File and store into Pandas data frame
purchase_raw_df = pd.read_csv(file_to_load)
purchase_raw_df.head()

#780 rows, 7 columns
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
      <th>Purchase ID</th>
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
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count

* Display the total number of players



```python
# Display total number of players
unique_players = pd.Series(purchase_raw_df["SN"]).unique()
player_count = {"Total Players": [len(unique_players)]}
player_count_df = pd.DataFrame(data=player_count)
player_count_df

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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python

```


```python
# Run calculations to obtain number of unique items, avg price, number of purchase, total revenue
unique_items = len(pd.Series(purchase_raw_df["Item ID"]).unique())
average_price = purchase_raw_df["Price"].mean()
number_purchases = len(pd.Series(purchase_raw_df["Purchase ID"]))
total_revenue = purchase_raw_df["Price"].sum()

# Create summary data frame to hold results
purchase_summary_df = pd.DataFrame({
    "Number of Unique Items": [unique_items], 
    "Average Price": [average_price], 
    "Number of Purchases": [number_purchases], 
    "Total Revenue": [total_revenue]})

# Display data in cleaner format
purchase_summary_df.style.format({
    "Average Price": "${:.2f}",
    "Total Revenue": "${:,.2f}"})

```




<style  type="text/css" >
</style><table id="T_e8d6a71e_8527_11ea_a02c_50de06c7c5d4" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Number of Unique Items</th>        <th class="col_heading level0 col1" >Average Price</th>        <th class="col_heading level0 col2" >Number of Purchases</th>        <th class="col_heading level0 col3" >Total Revenue</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_e8d6a71e_8527_11ea_a02c_50de06c7c5d4level0_row0" class="row_heading level0 row0" >0</th>
                        <td id="T_e8d6a71e_8527_11ea_a02c_50de06c7c5d4row0_col0" class="data row0 col0" >179</td>
                        <td id="T_e8d6a71e_8527_11ea_a02c_50de06c7c5d4row0_col1" class="data row0 col1" >$3.05</td>
                        <td id="T_e8d6a71e_8527_11ea_a02c_50de06c7c5d4row0_col2" class="data row0 col2" >780</td>
                        <td id="T_e8d6a71e_8527_11ea_a02c_50de06c7c5d4row0_col3" class="data row0 col3" >$2,379.77</td>
            </tr>
    </tbody></table>




```python

```

## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
# Create data frame of unique players grouped by gender
unique_players_df=purchase_raw_df.drop_duplicates(subset=["SN"])
gender_unique_df = unique_players_df.groupby(["Gender"])

# Run calculations for total count and percentage of players by gender
total_gender_count = gender_unique_df["Gender"].count()
percentage_players_gender = gender_unique_df["Gender"].count() / unique_players_df["Gender"].count() * 100

# Create summary data frame to hold results
gender_summary_df = pd.DataFrame({
    "Total Count": total_gender_count,
    "Percentage of Players": percentage_players_gender})
            
# Sort data by total count
gender_sorted_df = gender_summary_df.sort_values(["Total Count"], ascending=False)

# Display data in cleaner format
gender_sorted_df.style.format({
    "Percentage of Players":"{:.2f}%"})

```




<style  type="text/css" >
</style><table id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Total Count</th>        <th class="col_heading level0 col1" >Percentage of Players</th>    </tr>    <tr>        <th class="index_name level0" >Gender</th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4level0_row0" class="row_heading level0 row0" >Male</th>
                        <td id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4row0_col0" class="data row0 col0" >484</td>
                        <td id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4row0_col1" class="data row0 col1" >84.03%</td>
            </tr>
            <tr>
                        <th id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4level0_row1" class="row_heading level0 row1" >Female</th>
                        <td id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4row1_col0" class="data row1 col0" >81</td>
                        <td id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4row1_col1" class="data row1 col1" >14.06%</td>
            </tr>
            <tr>
                        <th id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4level0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th>
                        <td id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4row2_col0" class="data row2 col0" >11</td>
                        <td id="T_f1af9a44_8527_11ea_a02c_50de06c7c5d4row2_col1" class="data row2 col1" >1.91%</td>
            </tr>
    </tbody></table>




## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Create data frame of all purchases grouped by gender
gender_all_df = purchase_raw_df.groupby(["Gender"])

# Run calculations for purchase count, avg purchase price, total purchase value, avg purchase per person
purchase_count = gender_all_df["Purchase ID"].count()
avg_purchase_price = gender_all_df["Price"].mean()
total_purchase_value = gender_all_df["Price"].sum()
total_gender_count = gender_all_df.nunique()["SN"]
avg_purchase_per_person = total_purchase_value / total_gender_count

# Create summary data frame to hold results
gender_purchase_summary_df = pd.DataFrame({
    "Purchase Count": purchase_count,
    "Average Purchase Price": avg_purchase_price,
    "Total Purchase Value": total_purchase_value,
    "Avg Total Purchase per Person": avg_purchase_per_person})

# Sort data by purchase count
gender_purchase_sorted_df = gender_purchase_summary_df.sort_values(["Purchase Count"], ascending=False)

# Display data in cleaner format
gender_purchase_sorted_df.style.format({
    "Average Purchase Price": "${:,.2f}",
    "Total Purchase Value": "${:,.2f}",
    "Avg Total Purchase per Person": "${:,.2f}"})


```




<style  type="text/css" >
</style><table id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th>    </tr>    <tr>        <th class="index_name level0" >Gender</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4level0_row0" class="row_heading level0 row0" >Male</th>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row0_col0" class="data row0 col0" >652</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row0_col1" class="data row0 col1" >$3.02</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row0_col2" class="data row0 col2" >$1,967.64</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row0_col3" class="data row0 col3" >$4.07</td>
            </tr>
            <tr>
                        <th id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4level0_row1" class="row_heading level0 row1" >Female</th>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row1_col0" class="data row1 col0" >113</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row1_col1" class="data row1 col1" >$3.20</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row1_col2" class="data row1 col2" >$361.94</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row1_col3" class="data row1 col3" >$4.47</td>
            </tr>
            <tr>
                        <th id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4level0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row2_col0" class="data row2 col0" >15</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row2_col1" class="data row2 col1" >$3.35</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row2_col2" class="data row2 col2" >$50.19</td>
                        <td id="T_f2cf3178_8527_11ea_a02c_50de06c7c5d4row2_col3" class="data row2 col3" >$4.56</td>
            </tr>
    </tbody></table>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
# Establish bins and group names for ages
bins_to_cut = [0, 9.9, 14, 19, 24, 29, 34, 39, 100]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

# Categorize players into age bins
unique_players_df["Age Groups"] = pd.cut(
    x=unique_players_df["Age"],
    bins=bins_to_cut,
    labels=group_names,
    include_lowest=True)

# Run calculations for total count of players and percentage of players by age groups 
total_count_age = unique_players_df["Age Groups"].value_counts()
percentage_players_age = (unique_players_df["Age Groups"].value_counts() / len(unique_players_df)) * 100

# Create data frame to hold results
age_summary_df = pd.DataFrame({
    "Total Count": total_count_age,
    "Percentage of Players": percentage_players_age})
                  
# Sort data by age groups
age_sorted_df = age_summary_df.sort_index(ascending=True)

# Display data in cleaner format
age_sorted_df.style.format({
    "Percentage of Players": "{:.2f}%"})

```

    /Applications/anaconda3/lib/python3.7/site-packages/ipykernel_launcher.py:10: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      # Remove the CWD from sys.path while we load stuff.





<style  type="text/css" >
</style><table id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Total Count</th>        <th class="col_heading level0 col1" >Percentage of Players</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4level0_row0" class="row_heading level0 row0" ><10</th>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row0_col0" class="data row0 col0" >17</td>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row0_col1" class="data row0 col1" >2.95%</td>
            </tr>
            <tr>
                        <th id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4level0_row1" class="row_heading level0 row1" >10-14</th>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row1_col0" class="data row1 col0" >22</td>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row1_col1" class="data row1 col1" >3.82%</td>
            </tr>
            <tr>
                        <th id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4level0_row2" class="row_heading level0 row2" >15-19</th>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row2_col0" class="data row2 col0" >107</td>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row2_col1" class="data row2 col1" >18.58%</td>
            </tr>
            <tr>
                        <th id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4level0_row3" class="row_heading level0 row3" >20-24</th>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row3_col0" class="data row3 col0" >258</td>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row3_col1" class="data row3 col1" >44.79%</td>
            </tr>
            <tr>
                        <th id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4level0_row4" class="row_heading level0 row4" >25-29</th>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row4_col0" class="data row4 col0" >77</td>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row4_col1" class="data row4 col1" >13.37%</td>
            </tr>
            <tr>
                        <th id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4level0_row5" class="row_heading level0 row5" >30-34</th>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row5_col0" class="data row5 col0" >52</td>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row5_col1" class="data row5 col1" >9.03%</td>
            </tr>
            <tr>
                        <th id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4level0_row6" class="row_heading level0 row6" >35-39</th>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row6_col0" class="data row6 col0" >31</td>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row6_col1" class="data row6 col1" >5.38%</td>
            </tr>
            <tr>
                        <th id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4level0_row7" class="row_heading level0 row7" >40+</th>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row7_col0" class="data row7 col0" >12</td>
                        <td id="T_0dbcde68_8528_11ea_a02c_50de06c7c5d4row7_col1" class="data row7 col1" >2.08%</td>
            </tr>
    </tbody></table>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Categorize purchases into age bins
purchase_raw_df["Age Groups"] = pd.cut(
    x=purchase_raw_df["Age"],
    bins=bins_to_cut,
    labels=group_names,
    include_lowest=True)

# Create data frame of purchases grouped by age groups
age_groupby_df = purchase_raw_df.groupby(["Age Groups"])

# Run calculations for purchase counts, avg purchase, total purchase, avg purchase per person by age groups
purchase_count_age = age_groupby_df["Purchase ID"].count()
avg_purchase_age = age_groupby_df["Price"].mean()
total_purchase_age = age_groupby_df["Price"].sum()
total_age_count = age_groupby_df.nunique()["SN"]
avg_purchase_person_age = total_purchase_age / total_age_count

# Create data frame to hold results
purchasing_age_summary_df = pd.DataFrame({
    "Purchase Count": purchase_count_age,
    "Average Purchase Price": avg_purchase_age,
    "Total Purchase Value": total_purchase_age,
    "Avg Total Purchase per Person": avg_purchase_person_age})

# Sort data by age groups
purchasing_age_sorted_df = purchasing_age_summary_df.sort_index(ascending=True)

# Display data in cleaner format
purchasing_age_sorted_df.style.format({
    "Average Purchase Price": "${:.2f}",
    "Total Purchase Value": "${:.2f}",
    "Avg Total Purchase per Person": "${:.2f}"})



```




<style  type="text/css" >
</style><table id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th>    </tr>    <tr>        <th class="index_name level0" >Age Groups</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4level0_row0" class="row_heading level0 row0" ><10</th>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row0_col0" class="data row0 col0" >23</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row0_col1" class="data row0 col1" >$3.35</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row0_col2" class="data row0 col2" >$77.13</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row0_col3" class="data row0 col3" >$4.54</td>
            </tr>
            <tr>
                        <th id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4level0_row1" class="row_heading level0 row1" >10-14</th>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row1_col0" class="data row1 col0" >28</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row1_col1" class="data row1 col1" >$2.96</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row1_col2" class="data row1 col2" >$82.78</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row1_col3" class="data row1 col3" >$3.76</td>
            </tr>
            <tr>
                        <th id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4level0_row2" class="row_heading level0 row2" >15-19</th>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row2_col0" class="data row2 col0" >136</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row2_col1" class="data row2 col1" >$3.04</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row2_col2" class="data row2 col2" >$412.89</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row2_col3" class="data row2 col3" >$3.86</td>
            </tr>
            <tr>
                        <th id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4level0_row3" class="row_heading level0 row3" >20-24</th>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row3_col0" class="data row3 col0" >365</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row3_col1" class="data row3 col1" >$3.05</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row3_col2" class="data row3 col2" >$1114.06</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row3_col3" class="data row3 col3" >$4.32</td>
            </tr>
            <tr>
                        <th id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4level0_row4" class="row_heading level0 row4" >25-29</th>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row4_col0" class="data row4 col0" >101</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row4_col1" class="data row4 col1" >$2.90</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row4_col2" class="data row4 col2" >$293.00</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row4_col3" class="data row4 col3" >$3.81</td>
            </tr>
            <tr>
                        <th id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4level0_row5" class="row_heading level0 row5" >30-34</th>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row5_col0" class="data row5 col0" >73</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row5_col1" class="data row5 col1" >$2.93</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row5_col2" class="data row5 col2" >$214.00</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row5_col3" class="data row5 col3" >$4.12</td>
            </tr>
            <tr>
                        <th id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4level0_row6" class="row_heading level0 row6" >35-39</th>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row6_col0" class="data row6 col0" >41</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row6_col1" class="data row6 col1" >$3.60</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row6_col2" class="data row6 col2" >$147.67</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row6_col3" class="data row6 col3" >$4.76</td>
            </tr>
            <tr>
                        <th id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4level0_row7" class="row_heading level0 row7" >40+</th>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row7_col0" class="data row7 col0" >13</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row7_col1" class="data row7 col1" >$2.94</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row7_col2" class="data row7 col2" >$38.24</td>
                        <td id="T_1e89bb80_8528_11ea_a02c_50de06c7c5d4row7_col3" class="data row7 col3" >$3.19</td>
            </tr>
    </tbody></table>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Create data frame of purchases grouped by players
player_groupby_df = purchase_raw_df.groupby(["SN"])

# Run calculations for purchase count, avg purchase, total purchase by spender
purchase_count_spender = player_groupby_df["Purchase ID"].count()
avg_purchase_spender = player_groupby_df["Price"].mean()
total_purchase_spender = player_groupby_df["Price"].sum()

# Create data frame to hold results
top_spenders_summary_df = pd.DataFrame({
    "Purchase Count": purchase_count_spender,
    "Average Purchase Price": avg_purchase_spender,
    "Total Purchase Value": total_purchase_spender})

# Sort data by total purchase value
top_spenders_sorted_df = top_spenders_summary_df.sort_values(["Total Purchase Value"], ascending=False).head()

# Display data in cleaner format
top_spenders_sorted_df.style.format({
    "Average Purchase Price": "${:.2f}",
    "Total Purchase Value": "${:.2f}"})

```




<style  type="text/css" >
</style><table id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >SN</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4level0_row0" class="row_heading level0 row0" >Lisosia93</th>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row0_col0" class="data row0 col0" >5</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row0_col1" class="data row0 col1" >$3.79</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row0_col2" class="data row0 col2" >$18.96</td>
            </tr>
            <tr>
                        <th id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4level0_row1" class="row_heading level0 row1" >Idastidru52</th>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row1_col0" class="data row1 col0" >4</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row1_col1" class="data row1 col1" >$3.86</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row1_col2" class="data row1 col2" >$15.45</td>
            </tr>
            <tr>
                        <th id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4level0_row2" class="row_heading level0 row2" >Chamjask73</th>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row2_col0" class="data row2 col0" >3</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row2_col1" class="data row2 col1" >$4.61</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row2_col2" class="data row2 col2" >$13.83</td>
            </tr>
            <tr>
                        <th id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4level0_row3" class="row_heading level0 row3" >Iral74</th>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row3_col0" class="data row3 col0" >4</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row3_col1" class="data row3 col1" >$3.40</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row3_col2" class="data row3 col2" >$13.62</td>
            </tr>
            <tr>
                        <th id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4level0_row4" class="row_heading level0 row4" >Iskadarya95</th>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row4_col0" class="data row4 col0" >3</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row4_col1" class="data row4 col1" >$4.37</td>
                        <td id="T_1fde6f3a_8528_11ea_a02c_50de06c7c5d4row4_col2" class="data row4 col2" >$13.10</td>
            </tr>
    </tbody></table>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Create data frame of purchases grouped by item ID and item name
popular_items_df = purchase_raw_df[["Item ID", "Item Name", "Price"]]
popular_groupby_df = popular_items_df.groupby(["Item ID", "Item Name"])

# Run calculations for purchase count, total purchases and item price
purchase_count_popular = popular_groupby_df["Price"].count()
total_purchase_popular = popular_groupby_df["Price"].sum()
item_price_popular = total_purchase_popular / purchase_count_popular

# Create data frame to hold results
popular_item_summary = pd.DataFrame({
    "Purchase Count": purchase_count_popular,
    "Item Price": item_price_popular,
    "Total Purchase Value": total_purchase_popular})

# Sort data by purchase count
popular_item_sorted = popular_item_summary.sort_values(["Purchase Count"], ascending=False).head()

# Display data in cleaner format
popular_item_sorted.style.format({
    "Item Price": "${:.2f}",
    "Total Purchase Value": "${:.2f}"})


```




<style  type="text/css" >
</style><table id="T_27598402_8528_11ea_a02c_50de06c7c5d4" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Item Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >Item ID</th>        <th class="index_name level1" >Item Name</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level0_row0" class="row_heading level0 row0" >92</th>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level1_row0" class="row_heading level1 row0" >Final Critic</th>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row0_col0" class="data row0 col0" >13</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row0_col1" class="data row0 col1" >$4.61</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row0_col2" class="data row0 col2" >$59.99</td>
            </tr>
            <tr>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level0_row1" class="row_heading level0 row1" >178</th>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level1_row1" class="row_heading level1 row1" >Oathbreaker, Last Hope of the Breaking Storm</th>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row1_col0" class="data row1 col0" >12</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row1_col1" class="data row1 col1" >$4.23</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row1_col2" class="data row1 col2" >$50.76</td>
            </tr>
            <tr>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level0_row2" class="row_heading level0 row2" >145</th>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level1_row2" class="row_heading level1 row2" >Fiery Glass Crusader</th>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row2_col0" class="data row2 col0" >9</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row2_col1" class="data row2 col1" >$4.58</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row2_col2" class="data row2 col2" >$41.22</td>
            </tr>
            <tr>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level0_row3" class="row_heading level0 row3" >132</th>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level1_row3" class="row_heading level1 row3" >Persuasion</th>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row3_col0" class="data row3 col0" >9</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row3_col1" class="data row3 col1" >$3.22</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row3_col2" class="data row3 col2" >$28.99</td>
            </tr>
            <tr>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level0_row4" class="row_heading level0 row4" >108</th>
                        <th id="T_27598402_8528_11ea_a02c_50de06c7c5d4level1_row4" class="row_heading level1 row4" >Extraction, Quickblade Of Trembling Hands</th>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row4_col0" class="data row4 col0" >9</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row4_col1" class="data row4 col1" >$3.53</td>
                        <td id="T_27598402_8528_11ea_a02c_50de06c7c5d4row4_col2" class="data row4 col2" >$31.77</td>
            </tr>
    </tbody></table>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
# Sort data by total purchase value
profitable_item_sorted = popular_item_summary.sort_values(["Total Purchase Value"], ascending=False).head()

# Display data in cleaner format
profitable_item_sorted.style.format({
    "Item Price": "${:.2f}",
    "Total Purchase Value": "${:.2f}"})
```




<style  type="text/css" >
</style><table id="T_00780df0_8522_11ea_a02c_50de06c7c5d4" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Item Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >Item ID</th>        <th class="index_name level1" >Item Name</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level0_row0" class="row_heading level0 row0" >92</th>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level1_row0" class="row_heading level1 row0" >Final Critic</th>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row0_col0" class="data row0 col0" >13</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row0_col1" class="data row0 col1" >$4.61</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row0_col2" class="data row0 col2" >$59.99</td>
            </tr>
            <tr>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level0_row1" class="row_heading level0 row1" >178</th>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level1_row1" class="row_heading level1 row1" >Oathbreaker, Last Hope of the Breaking Storm</th>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row1_col0" class="data row1 col0" >12</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row1_col1" class="data row1 col1" >$4.23</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row1_col2" class="data row1 col2" >$50.76</td>
            </tr>
            <tr>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level0_row2" class="row_heading level0 row2" >82</th>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level1_row2" class="row_heading level1 row2" >Nirvana</th>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row2_col0" class="data row2 col0" >9</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row2_col1" class="data row2 col1" >$4.90</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row2_col2" class="data row2 col2" >$44.10</td>
            </tr>
            <tr>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level0_row3" class="row_heading level0 row3" >145</th>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level1_row3" class="row_heading level1 row3" >Fiery Glass Crusader</th>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row3_col0" class="data row3 col0" >9</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row3_col1" class="data row3 col1" >$4.58</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row3_col2" class="data row3 col2" >$41.22</td>
            </tr>
            <tr>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level0_row4" class="row_heading level0 row4" >103</th>
                        <th id="T_00780df0_8522_11ea_a02c_50de06c7c5d4level1_row4" class="row_heading level1 row4" >Singed Scalpel</th>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row4_col0" class="data row4 col0" >8</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row4_col1" class="data row4 col1" >$4.35</td>
                        <td id="T_00780df0_8522_11ea_a02c_50de06c7c5d4row4_col2" class="data row4 col2" >$34.80</td>
            </tr>
    </tbody></table>




```python

```
