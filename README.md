# US-Home-Prices

---

### Project Overview

The purpose of this project was to explore correlations between various features of houses that sold in Washington, USA between May - July, 2014, with the goal of determining what factors (if any) were related to sale price. The variables I explored included square footage, bedroom/bathroom/floor counts, year that the house was built, view, condition of the home, the city, etc.

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

My data analysis involved exploring the hypothesis that house prices would be strongly and positively correlated with square feet, condition, bedroom/bathroom/floor counts, view, and city.

### Data Analysis

The following code separated "statezip" into 2 distinct columns for state and zip.

```python
df['state'] = df['statezip'].astype(str).str[:2]
df['zip'] = df['statezip'].astype(str).str[2:]
```

The following code generated a heat map that provides the correlation direction and strength between all variables in the data set. I converted variables of type "object" to numerical categories in order to include them in the correlations.

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

As I created scatter plots to explore correlations, I realized that my hypothesis was not holding up. Price only moderately correlated with sqft_living, sqft_above, and number of bathrooms. In fact, the strongest correlations overall did not involve price. Sqft_above and sqft_living had a strong correlation of 0.874881. Number of bathrooms and sqft_living had a strong correlation of 0.760353. Lastly, sqft_above and bathrooms had a correlation of 0.687679. This makes sense, as these variables are all describing the similar features of a home (size/square feet).

### Implications/Recommendations:

If this project were for the purpose of pricing a home, I would apply the findings from the moderate correlations between price and square feet/number of bathrooms by using square feet as a base for price, and then adjusting based on all other aspects of a house that add value. In order to understand the amount of value that other variables add, I would want to look at data over a longer period of time in Washington. I would also add external factors to measure, such as distances from a school and a grocery store.

### Limitations

There were a few limitations within this data set. One limitation was that the data is 10 years old, and it spans a very narrow time frame of roughly 3 months in the summer. Therefore, we cannot see how price differs across seasons. The data set is also a bit decieving, as it is titled "US Housing Dataset" but only contains data from the state of Washington. Therefore we do not see how pricing varies across state lines.

### References

1. [kaggle.com](https://www.kaggle.com)
