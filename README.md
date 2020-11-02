# Amazon_Vine_Analysis_2

## Purpose
Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review. The purpose of this analysis was to find out if there is any bias toward favorable reviews from Vine members. 

### Overview

*Note: Vine members are "paid" reviews

I first initiated a PostgreSQL database in AWS RDS and linked it to PgAdmin on my local machine. I then created a database called "Review_Data" and formulated a database Schema consisting of four tables. I then created these tables in the database. 

The datasource I was working with were links to S3 with files with zipped tab-separated values. These files were approximately 1.6 GB each, so I decided to use a small hadoop cluster using Databricks to compensate for the large amount of data that I needed to process. 

Once my cluster was up and running, I performed ETL on the data, importing it from the S3 bucket and then transforming it using pyspark to fit my PostgreSQL database Schema. Once the data was in a clean form capable of being uploaded, I sent it over to PostgreSQL using a direct connection with jdbc API.

At this point, I could have used either SQL in PostgreSQL to perform my data analysis or Pyspark. I decided to continue using Pyspark, to further showcase my skillset using Pyspark to potential employers, however, I could have just as easily done this in SQL.

The data I was after was in the Vine table. I performed a series of non-destructive transformations on the data to ultimately create a dataframe where total_votes were greater than or equal to 20 and helpful_votes/total_votes was greater than or equal to 50%. Then I created two dataframes off of this one, those that were from Vine reviewers and those that were not. Then for each of these dataframes I found the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews. The final dataframes containing these results are "paid_results" and "unpaid_results".

## Results

The sample is extremely lopsided, with 40,471 reviews from unpaid reviewers and 94 reviews from paid reviewers.

Paid_Reviewers:
* 94 reviews
* 48 five-star reviews
* 51.06% of the reviews were 5-star

Conversely..

Unpaid_Reviewers:
* 40,471 reviews
* 15663 five-star reviews
* 38.70% of the reviews were 5-star

## Summary 

This data suggests that there is a clear bias toward five-star reviews from paid-reviewers. This is clearly portrayed by the disparity between the percentage of reviews that were 5-star between paid and unpaid reviewers.

Further analysis should include testing other sample data to see if this increase in five-star ratings is consistent across different products being reviewed.





![Screen Shot 2020-10-30 at 11 47 32 PM](https://user-images.githubusercontent.com/66881241/97907796-a9235980-1cfa-11eb-9562-b71116c48a11.png)

![Screen Shot 2020-11-01 at 12 47 40 PM](https://user-images.githubusercontent.com/66881241/97907769-9b6dd400-1cfa-11eb-82ef-e2ecd9484e5c.png)

![Screen Shot 2020-11-01 at 1 25 06 PM](https://user-images.githubusercontent.com/66881241/97907762-9a3ca700-1cfa-11eb-8071-8896c83271b7.png)

![Screen Shot 2020-11-02 at 12 20 36 PM](https://user-images.githubusercontent.com/66881241/97917913-15f22000-1d0a-11eb-9704-42c5a2d08a29.png)

![Screen Shot 2020-11-02 at 12 20 36 PM](https://user-images.githubusercontent.com/66881241/97917913-15f22000-1d0a-11eb-9704-42c5a2d08a29.png)

![Screen Shot 2020-11-02 at 11 57 56 AM](https://user-images.githubusercontent.com/66881241/97917945-22767880-1d0a-11eb-9078-828e919b99c1.png)

![Screen Shot 2020-11-02 at 11 25 01 AM](https://user-images.githubusercontent.com/66881241/97917959-2a361d00-1d0a-11eb-95e8-9e9d567c6ba0.png)

![Screen Shot 2020-11-02 at 11 22 39 AM](https://user-images.githubusercontent.com/66881241/97917966-2dc9a400-1d0a-11eb-9d67-b62b032e5172.png)

![Screen Shot 2020-11-02 at 11 14 09 AM](https://user-images.githubusercontent.com/66881241/97917983-35894880-1d0a-11eb-823e-aec8a46e499d.png)

![Screen Shot 2020-11-02 at 11 25 01 AM](https://user-images.githubusercontent.com/66881241/97918037-4934af00-1d0a-11eb-96e2-655c4dc61cb9.png)

![Screen Shot 2020-11-02 at 11 22 39 AM](https://user-images.githubusercontent.com/66881241/97918046-4d60cc80-1d0a-11eb-972d-278b07f4bb6e.png)
