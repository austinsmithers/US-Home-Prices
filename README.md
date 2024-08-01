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

My data analysis involved exploring the following hypotheses:

1. Price would be strongly and positively correlated with square feet, condition,
2. Non-linear regression: PM2.5 concentration (variable measuring air pollution) will have a non-linear relationship to the remaining variables in the data set.

### Data Analysis

The following code generates a scatter plot illustrating the relationship between temperature and pressure, with a blue linear regression line overlaid. There is a negative correlation here.

```python
sns.regplot(x="TEMP", y="PRES", data=df, scatter_kws={"color": "red"}, line_kws={"color":"blue"})
```

The following code generates a heat map that provides the correlation direction and strength across all variables in the data set. I converted "combined wind direction" from object type to numerical categories in order to include it in the heat map.

```python
df_numerized = df
for col_name in df_numerized.columns:
    if(df_numerized[col_name].dtype == 'object'):
        df_numerized[col_name] = df_numerized[col_name].astype('category')
        df_numerized[col_name] = df_numerized[col_name].cat.codes
correlation_matrix = df_numerized.corr()
sns.heatmap(correlation_matrix, annot=True)

plt.title("Correlation Matrix")
plt.xlabel("Air Quality Factors")
plt.ylabel("Air Quality Factors")
plt.show()
```

### Results/Findings

The analysis results are summarized as follows:
1. Temperature, pressure and dew point are all strongly, linearly correlated. As temperature and dew point increase, pressure decreases.
2. The correlations between environmental factors and air pollution, measured as PM2.5 concentration, appear to be strong, non-linear correlations. They do not appear to be strongly related on the heat map, because they are not linearly correlated.

### Implications/Recommendations:

If this project were for the purpose of reducing pollution in Beijing, I would continue my analysis by further exploring the strong, non-linear relationships associated with PM2.5 concentration. The goal would be to determine what factor(s) most impact PM2.5 levels and then figure out how to indirectly influence these variables (via legislation, systemic change, etc.) to decrease PM2.5 levels. Determining how to manipulate the environmental factors that influence PM2.5 concentration would require further analysis on these variables.

### Limitations

There were a few limitations within this data set. One limitation was that each row (apartment) included in a multi-sale transaction did not report the individual sale price for that apartment, but rather the sale price for all of the apartments in the multi-sale transaction. This resulted in an inflated sale volume when analyzing the data. Although I was able to control for some of these transactions, others were not controlled for if the transactions did not close on the same day, in the same building, or if the same building address was written differently for different apartments. Therefore, it is important to note that these numbers might be slightly inflated across all boroughs. I mostly included this field in my analysis to understand how boroughs ranked against each other, rather than to determine accurate sale prices. Additionally, I intended to only analyze residential buildings, but the building categories included in the data set did not fully separate residential and commercial buildings. This fact also may be contributing to inflated sales volume, since commercial listings are often more expensive. Since I was mainly looking for trends and practicing my SQL skills, I continued on with my analysis. If I were to actually use this data set with a client, I would focus on a smaller section of the data, making sure to go through and completely control for the multi-sale transactions and remove all commercial buildings.

### References

1. [Data.gov](https://data.gov/)
