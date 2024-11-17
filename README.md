# Exploratory Data Analysis (BCG X Data Science Project Part 1)
![Introductory Picture](EDA.png)
## Introduction
This is Part 1 of a project from the [BCG X Data Science micro-internship](https://www.theforage.com/simulations/bcg/data-science-ccdz). The Boston Consulting Group (BCG) is an American global consulting firm that  partners with leaders in business and society to tackle their most important challenges. It is one of the world's 3 largest consulting firms along with McKinsey & Company and Bain & Company. BCG X is a new initiative from BCG that combines the firm's consulting expertise with tech building and design.

In this task, I take on the role of a junior data analyst employed at BCG X. BCG X's client, a major gas and electricity utility called PowerCo, is concerned about their customers leaving for better offers from other energy providers.

## Problem Statement
PowerCo has expressed concern over their customers leaving them for better offers from competing energy companies. This concern is exacerbated by the fact that the energy market has had a lot of change in recent years and there are more options than ever for customers to choose from. During a meeting with the Associate Director of the Data Science team, one potential reason for churn is price sensitivity. I am tasked with investigating this hypothesis. To gain a holistic understanding of the data provided by PowerCo, my first task is to conduct exploratory data analysis.

## Skills Demonstrated
* Python
* Exploratory Data Analysis
* Data Visualization
* Descriptive Statistics

## Data Sourcing
This data was provided to me by the BCG X Data Science microinternship hosted by Forage. A copy of the data is included in this repository under the file name: client_data (1).csv and price_data (1).csv.

## Data Attributes
The data provided by PowerCo is separated into 2 files: client_data(1).csv and price_data(1).csv. The client data contains information about power consumption, sales channels, forecasted power consumption, and whether the client has churned or not. Each row contains data for 1 client.

The price data contains information on the price of energy that each client pays during various peak times of the day. Most clients will have 12 rows of data, one row for each month in a year.

Attributes for client data:
* id - Client company identifier.
* channel_sales - Code of the sales channel.
* cons_12m - Electricity consumption of the past 12 months.
* cons_gas_12m - Gas consumption of the past 12 months.
* cons_last_month - Electricity consumption of the last month.
* date_activ - Date of activation of the contract.
* date_end - Registered date of the end of the contract.
* date_modif_prod - Date of the last modification of the product.
* date_renewal - Date of the next contract renewal.
* forecast_cons_12m - FForecasted electricity consumption for next 12 months.
* forecast_cons_year - Forecasted electricity consumption for the next calendar year.
* forecast_discount_energy - Forecasted value of current discount.
* forecast_meter_rent_12m - Forecasted bill of meter rental for the next 2 months.
* forecast_price_energy_off_peak - Forecasted energy price for 1st period (off peak).
* forecast_price_energy_peak - Forecasted energy price for 2nd period (peak).
* forecast_price_pow_off_peak - Forecasted power price for 1st period (off peak).
* has_gas - Indicated if client is also a gas client.
* imp_cons - Current paid consumption.
* margin_gross_pow_ele - Gross margin on power subscription.
* margin_net_pow_ele - Net margin on power subscription.
* nb_prod_act - Number of active products and services.
* net_margin - Total net margin.
* num_years_antig - Antiquity of the client (in number of years).
* origin_up - Code of the electricity campaign the customer first subscribed to.
* pow_max - Subscribed power.
* churn - Has the client churned over the next 3 months.

Attributes for price data:
* id - Client company identifier.
* price_date - Reference date.
* price_off_peak_var - Price of energy for the 1st period (off peak).
* price_peak_var - Price of energy for the 2nd period (peak).
* price_mid_peak_var - Price of energy for the 3rd period (mid peak).
* price_off_peak_fix - Price of power for the 1st period (off peak).
* price_peak_fix - Price of power for the 2nd period (peak).
* price_mid_peak_fix - Price of power for the 3rd period (mid peak).

## Exploratory Data Analysis and Data Visualizations
Exploratory data analysis is used to gain a holistic understanding of the data.
Exploratory data analysis uses statistical techniques and visualizations to gain a better understanding of the statistical properties that the data holds.
A copy of this analysis is included in this repository under the file name: James Weber Exploratory Data Analysis.ipynb.

### 1. Importing Libraries and Data
To start with data analysis, we must first import libraries which contains the commands we need for analysis.
Then we import the data from the client_data(1).csv and price_data(1).csv files into dataframes.

```
# Importing libraries

import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

# Use the read_csv() command to import .csv files.
# Create a client_df dataframe for the client data and a price_df dataframe for the price data.

client_df = pd.read_csv(r'C:/Users/jwebe/Desktop/client_data (1).csv')
price_df = pd.read_csv(r'C:/Users/jwebe/Desktop/price_data (1).csv')
```
<br/>

### 2. Descriptive Statistics for Client and Price Data
#### 2a. Client Data
Once we have both client and price data imported into dataframes, we can use the .describe() command to get descriptive statistics for client and price data.
Descriptive statistics are statistics that summarizes and describes the main features of a dataset.
This includes the the mean, standard deviation, min, max, and the 25% 50% and 75% quartiles for each column.

```
# Use the .describe() command to get the mean, standard deviation, min, max, and the 25% 50% and 75% quartiles of a dataframe.

client_df.describe()
```

![Descriptive Statistics for Client Data](Descriptive_Statistics_Client.png)

Based on the percentile values, we have a lot of highly skewed data.
Skewed data occurs when most of the data points are to the right or left side of the mean value.

![Skewed Data](Skewed_Data.png)

Too much skewness degrades the model’s ability to describe typical cases because the model has to deal with rare cases on extreme values.

#### 2b. Price Data
```
# Use the .describe() command to get the mean, standard deviation, min, max, and the 25% 50% and 75% quartiles of a dataframe.

client_df.describe()
```
![Descriptive Statistics for Price Data](Descriptive_Statistics_Price.png)

Overall, the price data looks good.

### 3. Churn Data Visualization
To fully analyze the data, we will need to create visualizations to determine if there are any patterns in the data that cannot be shown with statistics alone. 
We can get an overall understanding of the churn rate (the percentage of customers who stop doing business with a company) by visualizin the data on a bar chart.

The code below is used to create a dataframe which will count the number of customers who have churned and the number of customers who will continue their business with PowerCo.
```
# Create a churn dataframe using the churn column.
# Use the .value_counts() command to count the number of unique values in the churn column.
# Use the .reset_index(name = 'churn_count') command to create a dataframe and reset the index.

client_churn_count = client_df['churn'].value_counts().reset_index(name = 'churn_count')

# Use the .astype(str) command to convert the churn column from int data type to string data type.
# Use the .replace() command to replace 0 with 'Not Churned' and 1 with 'Churned'.

client_churn_count['churn'] = client_churn_count['churn'].astype(str)
client_churn_count['churn'] = client_churn_count['churn'].replace('0', 
                                                                  'Not Churned')
client_churn_count['churn'] = client_churn_count['churn'].replace('1', 
                                                                  'Churned')
```
The code below will create a new column that will calculate the percentage of customers who have or have not churned.
```
# Calculate the total number of customers by using the .sum() command to sum all the values in the churn_count column.
# Create a column called churn_percent and calculate the percentage of customers who have churned and customers who have not churned.
# Use the .round(2) command to round the values in the churn_percent column to 2 decimal places.

total_churn = client_churn_count['churn_count'].sum()
client_churn_count['churn_percent'] = (client_churn_count['churn_count']/total_churn) * 100
client_churn_count['churn_percent'] = client_churn_count['churn_percent'].round(2)
```
The code below will create a bar chart using the dataframe that we created,
```
# Use the fig, ax = plt.subplots() command to create a set of subplots within one cell.

fig, ax = plt.subplots(1, 1, figsize=(5, 5))

# Use the sns.barplot() command to create a bar plot.

sns.barplot( 
            data = client_churn_count, 
            x = 'churn', 
            y = 'churn_percent').set(title = 'Percent of Customers Churned', 
                                     xlabel = None, 
                                     ylabel = None)

ax.bar_label(ax.containers[0])
```
![Bar Chart of Churn Percentage](Churn_Bar_Chart.png)<br/>
The graph above depicts the number of customers who churned compared to the customers who are staying with PowerCo. The percentage of customers who have churned is 9.72%. The ideal churn rate for an established business is approximately 5% to 7%. Although the churn rate for Power is not bad, it could be improved.

### 4. Churn Based on Sales Channels
Sales channels are methods or pathways businesses use to sells their product or service to customers. Examples of sales channels are retail, mobile apps, social media, and direct sales. By determining the churn rate based on sales channels, we can gain some insight on the types of businesses that will stay with PowerCo or will leave PowerCo.

The code below is used to create a dataframe which group all of PowerCo's customers based on their sales channel. The code will then count the number of customers who have or have not churned for each group.
```
# Create a sales channel dataframe using the id, channel_sales, and churn columns.

s_channel = client_df[['id', 
                       'channel_sales', 
                       'churn']]

# Use the .grouby() command to group the data based on values in the channel_sales column.
# Use the .value_counts() command to count the number values in each group.
# Use the .reset_index(name = 'churn_count') command to create a dataframe and reset the index.

s_channel_churn_count = s_channel['churn'].groupby(s_channel['channel_sales']).value_counts().reset_index(name = 's_channel_churn_count
```
The sales channel data is encrypted for privacy. The code below is used to replace the encrypted sales channel with Channel_1, Channel_2, etc. for readability.
```
# The values in the channel_sales column are jumbled to protect the privacy of the company.
# Use the .replace() command to replace sales channel names with names that are more readable (Channel_1, Channel_2, etc.)

s_channel_churn_count['channel_sales'] = s_channel_churn_count['channel_sales'].replace('epumfxlbckeskwekxbiuasklxalciiuu', 
                                                                                        'Channel_1')
s_channel_churn_count['channel_sales'] = s_channel_churn_count['channel_sales'].replace('ewpakwlliwisiwduibdlfmalxowmwpci', 
                                                                                        'Channel_2')
s_channel_churn_count['channel_sales'] = s_channel_churn_count['channel_sales'].replace('fixdbufsefwooaasfcxdxadsiekoceaa', 
                                                                                        'Channel_3')
s_channel_churn_count['channel_sales'] = s_channel_churn_count['channel_sales'].replace('foosdfpfkusacimwkcsosbicdxkicaua', 
                                                                                        'Channel_4')
s_channel_churn_count['channel_sales'] = s_channel_churn_count['channel_sales'].replace('lmkebamcaaclubfxadlmueccxoimlema', 
                                                                                        'Channel_5')
s_channel_churn_count['channel_sales'] = s_channel_churn_count['channel_sales'].replace('sddiedcslfslkckwlfkdpoeeailfpeds', 
                                                                                        'Channel_6')
s_channel_churn_count['channel_sales'] = s_channel_churn_count['channel_sales'].replace('usilxuppasemubllopkaafesmlibmsdf', 
                                                                                        'Channel_7')
```
The next set of code is used to calculate the churn rate for each group.
```
# Create a column called s_channel_churn_percent and calculate the percentage of customers who have churned and customers who have not churned.
# Use the .round(2) command to round the values in the churn_percent column to 2 decimal places.
# To caculate churn percentage, use the total_churn variable that was calculated in the previous section.

s_channel_churn_count['s_channel_churn_percent'] = (s_channel_churn_count['s_channel_churn_count']/total_churn) * 100
s_channel_churn_count['s_channel_churn_percent'] = s_channel_churn_count['s_channel_churn_percent'].round(2)
```
The last set of code is used to create the bar chart withe the dataframe we created.
```
# Use the fig, ax = plt.subplots() command to create a set of subplots within one cell.

fig, ax = plt.subplots(1, 1, figsize=(15, 20))

# Use the sns.barplot() command to create a bar plot.

sns.barplot( 
            data = s_channel_churn_count, 
            x = 'channel_sales', 
            y = 's_channel_churn_percent', 
            hue = 'churn', 
            errorbar = None).set(title = 'Percent of Customers by Sales Channel', 
                                 xlabel = None, 
                                 ylabel = None)

ax.bar_label(ax.containers[0])
ax.bar_label(ax.containers[1])
```
![Churn Rate Based on Sales Channel](Sales_Channel_Churn.png)
