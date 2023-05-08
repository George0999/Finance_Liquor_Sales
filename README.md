# Finance Liquor Sales

A dataset that contains Liquor Sales in the state of Iowa in USA between 2012-2020 to find the most popular item per zipcode and the percentage of sales per store in the period between 2016-2019.

The concept is that we are given a dataset that contains Liquor Sales in the state of Iowa in USA between 2012-2020 and we are asked to find the most popular item per zipcode and the percentage of sales per store in the period between 2016-2019.

We are also asked to visualize the Data and present them in either a matplotlib format or in Tableau Public.

---

# **Steps followed for the completion of this project**

1. I imported the provided Dataset to MySQL Workbench.
2. To retrieve the wanted results between the years 2016 and 2019, I run the query below:
    
    ```sql
    SELECT * 
    FROM `finance_liquor_sales` 
    WHERE `date` BETWEEN '2016-01-01' AND '2020-01-01';
    ```
    
3. Then, I extracted the results to a csv file.
4. I imported NumPy, Pandas, MatPlotLib packages and the csv file to the PyCharm (Python IDE).
    
    ```python
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    
    df = pd.read_csv("finance_liquor_sales.csv")
    ```
    
5. To find the most popular item per zipcode, I grouped all data by “zip_code” and “item_description” and using the “sum()” method I found the total bottles sold. Then, using the “idxmax()” method I found the item with the maximum total bottles sold.
    
    ```python
    grouped = df.groupby(['zip_code', 'item_description'])['bottles_sold'].sum()
    most_popular_item = grouped.groupby('zip_code').idxmax()
    ```
    
    ```python
    grouped = df.groupby(['zip_code', 'item_description'])['bottles_sold'].sum()
    most_popular_item = grouped.groupby('zip_code').idxmax()
    ```
    
6. To find the percentage of sales per store, I grouped all the data by “store_name”, sum the “sale_dollars” and found the percentage by multiplying by 100 the fraction of “sales_by_store” and “total_sales”.
    
    ```python
    sales_by_store = df.groupby('store_name')['sale_dollars'].sum()
    total_sales = sales_by_store.sum()
    sales_percentages = (sales_by_store / total_sales) * 100
    ```
    
7. Next task was to visualize a scatter plot in MatPlotLib showing the bottles sold per zip code. After grouping and aggregating “zip_code” and “bottles_sold”, I created a scatter plot with ‘Zip Code” on the x-axis and “Bottles Sold” on the y-axis.
    
    ```python
    scatter_data = df.groupby('zip_code')['bottles_sold'].sum()
    plt.scatter(scatter_data.index, scatter_data.values)
    plt.xlabel('Zip Code')
    plt.ylabel('Bottles Sold')
    plt.title('Bottles Sold')
    plt.show()
    ```
    
8. Finally, using the Tableau, I imported the same csv file and created a Dashboard showing the following:
    1. A map with bottles sold.
    2. A table showing the number of bottles sold per item and zip code.
    3. I created a new calculated field in order to find the sales percentage.
    4. A bubble chart visualizing the Sales Percentage per store.
    5. A bar chart visualizing the Sales Percentage per store.
    
    (Follow the link below to see the Tableau visualization)
    

[](https://public.tableau.com/app/profile/george.ch./viz/DataAnalyst2023Workearly-FinalAssignment/LiquorStoresDashboard?publish=yes)

---

# **Built with:**

- MySQL Workbench
- PyCharm
- Tableau
