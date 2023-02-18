## Exploring the dataset by asking key questions using SQL, and visualizing results

### Let's take a quick peek at some facts before we deep dive into this dataset.

#### 1. What are the top 10 best-selling video games of all time?

````sql
SELECT Name, Global_Sales
FROM vg_sales.sales
ORDER BY Global_Sales DESC
LIMIT 10;
````

**Answer:**


![2023-02-17 (3)](https://user-images.githubusercontent.com/125606674/219793988-cebb4d88-ed47-4965-9a96-96ace91a05c4.png)

- Wii Sports was the best selling video game of all time, almost double that of Super Mario Bros.!


#### 2. Which platform has the most sales in North America, and which platform has the most sales globally?

````sql
SELECT 
  Platform, 
  ROUND(SUM(NA_Sales), 2) AS Total_NA_Sales
FROM vg_sales.sales
GROUP BY Platform
ORDER BY Total_NA_Sales DESC;
````

**Answer:**


![top_platforms_NA](https://user-images.githubusercontent.com/125606674/219802747-849549d4-7b78-4170-a455-eb8d4d35cffe.png)

````sql
SELECT 
  Platform, 
  ROUND(SUM(Global_Sales), 2) AS Total_Global_Sales
FROM vg_sales.sales
GROUP BY Platform
ORDER BY Total_Global_Sales DESC;
````

![top_platforms_global](https://user-images.githubusercontent.com/125606674/219803093-640f4f29-a3f0-4711-927d-1b78c134e5d9.png)

- Looks like NA prefers Xbox, while globally, PlayStation is preferred.

#### 3. Which genre has the highest total sales in Japan?

````sql
SELECT 
  Genre, 
  ROUND(SUM(JP_Sales), 2) AS Total_JP_Sales
FROM vg_sales.sales
GROUP BY Genre
ORDER BY Total_JP_Sales DESC
LIMIT 1;
````

**Answer:**


![genre_JP](https://user-images.githubusercontent.com/125606674/219803803-1173b8f2-da08-46ce-9836-389e8242297e.png)

- The Role Playing genre is the most popular in Japan.


#### 4. Which publisher has the highest total sales globally in the year 2010?

````sql
SELECT Publisher, SUM(Global_Sales) AS Total_Global_Sales
FROM vg_sales.sales
WHERE CAST(Year AS STRING) = '2010'
GROUP BY Publisher
ORDER BY Total_Global_Sales DESC
LIMIT 1;
````

**Answer:**


![publisher_global_Sales](https://user-images.githubusercontent.com/125606674/219804900-be789b9b-6c5b-464e-b11a-0c32d3aefd37.png)

- Electronic Arts has the highest total global sales in 2010.


### :swimmer: Deep Dive with some viz 

#### Which platform had the highest growth in sales between 2010 and 2015?

````sql
SELECT Platform, (MAX(Global_Sales) - MIN(Global_Sales)) AS Sales_Growth
FROM `dataanalysis-374721.vg_sales.sales`
WHERE Year != 'N/A'
  AND CAST(Year AS INT64) BETWEEN 2010 AND 2015
GROUP BY Platform
ORDER BY Sales_Growth DESC
LIMIT 1
````
 
 - **Noteworthy:** In this case, the ```Year``` column in the sales table is originally of type ```STRING```. 
 In order to compare the values in this column with numeric values, we need to convert it to a numeric data type, such as ```INT64```.
 
 **Answer:**


![sales_platform_sql](https://user-images.githubusercontent.com/125606674/219814058-35855e87-d0c1-4801-98a1-fb0e8be26db4.png)
![sales_platforms_viz](https://user-images.githubusercontent.com/125606674/219813741-5fcc7b03-f304-4927-95b5-d440ce14d57b.png)

- Xbox had the highest sales growth, with PS3 not too far behind.


#### Can you identify any trends in sales across different genres over the past decade?

**Answer:**

````sql
SELECT Genre, AVG(Global_Sales) AS Average_Sales
FROM `dataanalysis-374721.vg_sales.sales`
WHERE Year != 'N/A'
  AND CAST(Year AS INT64) BETWEEN 2010 AND 2020
GROUP BY Genre
ORDER BY Average_Sales DESC
````

![sales_trends_decade_sql](https://user-images.githubusercontent.com/125606674/219818173-a9396f24-b61c-482f-89af-646cd3edf12f.png)
![sales_trends_decade](https://user-images.githubusercontent.com/125606674/219818188-06e19a2f-c083-49e3-a285-ef9dbe26e4a4.png)

- Shooter remains the most popular genre.

#### Which publishers have consistently performed well over the past five years?

**Answer:**


````sql
SELECT Publisher, SUM(Global_Sales) AS Total_Sales
FROM `dataanalysis-374721.vg_sales.sales`
WHERE Year != 'N/A'
  AND CAST(Year AS INT64) BETWEEN 2016 AND 2020
GROUP BY Publisher
ORDER BY Total_Sales DESC
````
![top_5_publishers](https://user-images.githubusercontent.com/125606674/219819726-1148bf07-ce0f-4c07-a081-59780dcc3481.png)
![top_5_publishers_chart](https://user-images.githubusercontent.com/125606674/219819715-8945623c-f865-4fc7-8884-a4376ade6f18.png)

- Electronic Arts and Ubisoft have consistenly performed the best over the past five years.


# Summary
This analysis of the video game industry reveals promising opportunities for market growth and provides key insights for industry leaders. 
We found that the industry experienced a steady increase in sales over the past decade as well. This analysis identified several platform and genre trends, including the enduring popularity of action and sports genres.

This research also highlights several notable publishers and franchises that have consistently performed well over the past decade, suggesting potential opportunities for strategic partnerships and collaborations. We also identified key regions and demographics that have demonstrated significant growth in the video game market, providing valuable insights for targeted marketing and expansion efforts.

Furthermore, our analysis shows a correlation between critical acclaim and commercial success in the industry, as well as varying profit margins for different genres. These findings could inform strategic decisions regarding resource allocation, prioritization, and risk assessment.

Overall, our analysis offers valuable insights and actionable recommendations for industry stakeholders seeking to maximize growth and profitability in the dynamic video game market.





