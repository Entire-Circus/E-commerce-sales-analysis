# E-commerce-sales-analysis
Data analysis project using Python to explore synthetic sales data from an e-commerce store. Includes data cleaning, trend analysis, and visualizations using Pandas, Matplotlib, and Seaborn.

## Tools & Libraries
- **Python** (Jupyter Notebook)
- **Pandas**, **Matplotlib**, **Seaborn**, **NumPy**
- **SciPy**, **OpenPyXL**

## Project Highlights

- Cleaned a corrupted dataset with 500+ empty rows and missing values
- Combined multiple CSV files into one unified dataset
- Performed exploratory data analysis on:
  - Monthly and quarterly revenue trends
  - Top-selling product categories
  - Sales performance over time
- Created visualizations with Matplotlib and Seaborn to uncover patterns

## Code Preview
```python
# Find product with highest rating
df_hrating_gr = df.groupby("Product")["Review_Rating"].mean().reset_index()

# Sort the df to have only top 5 products with highest rating and to dispaly Campaign source in descending order
df_hrating_gr_s = df_hrating_gr.sort_values("Review_Rating", ascending=False)
df_top_products = df_hrating_gr_s.iloc[:5]

filtered_df = df[df["Product"].isin(df_top_products["Product"])] # create a copy of main df with data only related to top products
filtered_df2 = filtered_df[["Product", "Campaign_Source"]] # remove all other columns beside product and camaign source
filtered_df2_gr = filtered_df2.groupby("Product")["Campaign_Source"].value_counts() # count campaing sources
reset_df = filtered_df2_gr.reset_index()
```
## Visualization example
![Marketing campaing performance](Images/Marketing&20Campaing&20Performance.png)
```python
plt.figure(figsize=(12, 6))
sns.barplot(data=reset_df, x="Product", y="count", hue="Campaign_Source")

# Customizing the plot
plt.xlabel("Product")
plt.ylabel("Count of Campaign Sources")
plt.title("Marketing Campaign Performance by Product")
plt.xticks(rotation=30)  # Rotate x labels for better readability
plt.legend(title="Campaign Source")

# Show the plot
plt.show()
```
