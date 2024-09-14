# Project_Music_Store_Analysis

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
  


### Project Overview
SQL Project Music Store Analysis involves examining sales data, customer behavior, and product performance in a music retail store. The analysis helps identify trends, optimize inventory, and improve marketing strategies to boost revenue and customer satisfaction.


###  Data Sources

Music Store Data : The primary dataset used for this analysis is the 'Music_Store_database.sql' file containing detailed information about each sale made by the company , also the performsnce of the product and customer behaviour.

###  Tools
* Excel [Download Here](https://github.com/ABHILASHNAYAK20/music-store-analysis/blob/33f95e2ad673ae5b31fb48e59198577d854b8e8c/music%20store%20data.zip)
* Postgre SQL
* PgAdmin4

###   Data Cleaning
In the initial data preparation phase we have performed the following tasks:
- Data handling and inspection
- Handling missing values
- Data cleaning and formatting

### Exploratory Data Analysis
EDA involved exploring the sales data to answer key questions , such as:
- What is the overall sales trend?
- Which products are top sellers?
- What genres people like to listen to the most

### Data Analysis

Include some interesting code/features worked with
```sql
WITH popular_genre AS 
(
    SELECT COUNT(invoice_line.quantity) AS purchases, customer.country, genre.name, genre.genre_id, 
	ROW_NUMBER() OVER(PARTITION BY customer.country ORDER BY COUNT(invoice_line.quantity) DESC) AS RowNo 
    FROM invoice_line 
	JOIN invoice ON invoice.invoice_id = invoice_line.invoice_id
	JOIN customer ON customer.customer_id = invoice.customer_id
	JOIN track ON track.track_id = invoice_line.track_id
	JOIN genre ON genre.genre_id = track.genre_id
	GROUP BY 2,3,4
	ORDER BY 2 ASC, 1 DESC
)
SELECT * FROM popular_genre WHERE RowNo <= 1
```

### Results
The analysis results are summarized as follows:
- The most popular music genre varies by country, with genres like Rock, Alternative & Punk appearing frequently in certain regions.
-  Rock is a dominant genre in several countries, such as Australia, Austria, Belgium, and Brazil, indicating its widespread appeal across different nations.
-  In countries like Argentina, Alternative & Punk stands out as a leading genre, showcasing diverse musical preferences in different parts of the world


### Recommendations
Based on the analysis , we recommend the following actions:
- Stock and promote popular genres like Rock in countries where they sell the most, like Brazil and Australia.

- Create special marketing campaigns for each country, focusing on the music genres that are most popular there.

- Offer bundles or playlists in countries with different popular genres to attract more customers with varied music tastes.







### Schema- Music Store Database  
![MusicDatabaseSchema](https://user-images.githubusercontent.com/112153548/213707717-bfc9f479-52d9-407b-99e1-e94db7ae10a3.png)
