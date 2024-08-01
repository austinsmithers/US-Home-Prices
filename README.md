# US-Home-Prices

---

### Project Overview

The purpose of this project was to explore correlations between various features of homes that sold in Washington, USA between May - July, 2014, with the goal of determining what factors (if any) were related to sale price. These factors I explored included square footage, bedroom/bathroom/floor counts, year that the house was built, view, condition of the home, the city, etc.

### Data Sources

The primary dataset used for this analysis is "USAHousingDataset.csv" containing detailed information from Kaggle.com on the sale transactions that occurred in Washington state between May 2014 to July 2014.

### Tools

- Python - Data Analysis

### Data Cleaning/Preparation
In the initial data preparation phase, I performed the following:
1. Loaded the data and inspected it.
2. Checked for missing values.
3. Changed price to an integer to remove decimal places.
4. Ordered data by date and price.
5. Removed duplicate rows.
6. Separated state and zip code into two columns.
7. Dropped country and state columns, as all homes were located in Washington, USA, so these variables were not showing up on the correlation heat map.

### Hypotheses:

My data analysis involved exploring the hypothesis that the prices of the homes would be strongly and positively correlated with square feet, condition, bedroom/bathroom/floor counts, view, and the city that the homes are located.

### Data Analysis

The following code separated the state and zip code data from "statezip" into 2 distinct columns.

```python
df['state'] = df['statezip'].astype(str).str[:2]
df['zip'] = df['statezip'].astype(str).str[2:]
```

The following code generates a heat map that provides the correlation direction and strength across all variables in the data set. I converted variables of type "object" to numerical categories in order to include them in the correlations.

```python
df_numerized = df
for col_name in df_numerized.columns:
    if(df_numerized[col_name].dtype == 'object'):
        df_numerized[col_name] = df_numerized[col_name].astype('category')
        df_numerized[col_name] = df_numerized[col_name].cat.codes

correlation_matrix = df_numerized.corr()
sns.heatmap(correlation_matrix, annot=True)

plt.title("Correlation Matrix")
plt.xlabel("US Home Variables")
plt.ylabel("US Home Variables")
plt.show()
```

### Results/Findings

As I created scatter plots, I realized that my hypothesis was not holding up. Price's strongest correlations were with sqft_living, sqft_above, and number of bathrooms, but these correlations were not very strong, falling slightly below .5. The strongest correlations overall did not include price. Sqft_above and sqft_living had a strong correlation of 0.874881. Number of bathrooms and sqft_living had a strong correlation of 0.760353. Lastly, sqft_above and bathrooms had a correlation of 0.687679. Thus, the variables measuring size/square feet all seem to be correlated, which makes sense.

### Implications/Recommendations:

If this project were for the purpose of pricing a home, I would apply the findings from the moderate correlation between price and square feet/number of bathrooms. I would use square feet as a base for the price, and then adjust it based on all of the other aspects of a home that add value. In order to understand the degree of value that other variables add to a home, I would want to look at data over a longer period of time in Washington. I would also add external factors to measure such as distances from a school and a grocery store.

### Limitations

There were a few limitations within this data set. One limitation was that this data is 10 years old, and it spanned a very narrow time frame from May - July months. Therefore, we do not get a sense of how seasonality affects pricing.

each row (apartment) included in a multi-sale transaction did not report the individual sale price for that apartment, but rather the sale price for all of the apartments in the multi-sale transaction. This resulted in an inflated sale volume when analyzing the data. Although I was able to control for some of these transactions, others were not controlled for if the transactions did not close on the same day, in the same building, or if the same building address was written differently for different apartments. Therefore, it is important to note that these numbers might be slightly inflated across all boroughs. I mostly included this field in my analysis to understand how boroughs ranked against each other, rather than to determine accurate sale prices. Additionally, I intended to only analyze residential buildings, but the building categories included in the data set did not fully separate residential and commercial buildings. This fact also may be contributing to inflated sales volume, since commercial listings are often more expensive. Since I was mainly looking for trends and practicing my SQL skills, I continued on with my analysis. If I were to actually use this data set with a client, I would focus on a smaller section of the data, making sure to go through and completely control for the multi-sale transactions and remove all commercial buildings.

### References

1. [kaggle.com](https://data.gov/)
