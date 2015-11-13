# BI assignment 

The goal of this BI assignment is to find out if you could join our BI star-team to help us build a world-class data-driven startup.

We expect you to have not just lots of experience with building a data warehouse, but also hands-on experience with software development in other languages such as Python, Go, Nodejs, or PHP.

We will be evaluating the overall quality of your output, incl. the code quality & cleaness, SQL query optimisation, proper usage of a versioning tool and human-readable comments.

The assignment is split into 3 parts:

1. **Data warehouse & ETL load** => submission to a new GitHub repository
2. **Data cleaning** => submission to the same GitHub repository as (1), just another sub-folder
3. **API endpoint** => submission to a new GitHub repository

Please use `Readme.md` file in each repository to give us more info re. how did you approach the problem, why did you chose the solution you implemented etc.

### 1. Data warehouse & ETL

You can find these 3 tables in CSV files on AWS S3 (data storage):

* Table `offer` ([download here, 777 MB](https://s3-ap-southeast-2.amazonaws.com/hq-bi/bi-assignment/offer.csv))
* Table `lst_currency` ([download here, 0.5 MB](https://s3-ap-southeast-2.amazonaws.com/hq-bi/bi-assignment/lst_currency.csv))
* Table `fx_rate` ([download here, 3.8 MB](https://s3-ap-southeast-2.amazonaws.com/hq-bi/bi-assignment/fx_rate.csv))

Please download the 3 files and create simple ETL scripts & a data-mart.

1. Create a new database
2. Create a new schema: `primary_data`
2. Load the 3 tables (above) 1:1 to the `primary_data` schema (structure same as the CSV files have)
2. Create a new schema: `bi_data` (see the structure below)
2. Create ETL scripts to extract, transform and load the data from the `primary_data` schema to the `bi_data` schema

#### Stack

At HotelQuickly we use **MySQL, PosgreSQL (AWS Redshift) and MongoDB** databases. Thus we suggest you create the database in either **MySQL or PostgreSQL.** Both are open-source and easy to install for those few of you who don't have it yet. If you're more familiar with i.e. Oracle or MS SQL and prefer to use these, we're fine with that.

#### Data structure of `bi_data`

Please create new tables with the following structure. Add the SQL scripts to the repository.

* Table `valid_offers` - should include only active offers - `offer`.`valid_offer_flag` = 1
	* `offer_id` `INT`
	* `hotel_id` `INT`
	* `hotel_name` `VARCHAR(255)`
	* `price_usd` `FLOAT`
	* `original_price` `FLOAT`
	* `original_currency_code` `VARCHAR(35)`
	* `breakfast_included_flag` `TINYINT`
	* `valid_from_date` `DATETIME`
	* `valid_to_date` `DATETIME`
* Table `hotel_offers` - should include info about each hotel, for each day and each hour indicates if the hotel had at least one valid offer
	* `hotel_id` `INT`
	* `date` `DATE`
	* `hour` `TINYINT`
	* `breakfast_included_flag` `TINYINT`
	* `valid_offer_available_flag` `TINYINT`

#### Mini-glossary

* `offer` = deals that hotels give us (offers from hotels)
* `lst_currency` = list of all supported currencies
* `fx_rate` = foreign exchange rates (currency exchange rates from `prim_currency_id` to `scnd_currency_id`)
* `prim_currency_id` = primary currency ID (exchange *from* this currency)
* `scnd_currency_id` = secondary currency ID (exchange *to* this currency)
* `primary_data` = schema which includes the primary tables
* `bi_data` = schema which includes the tables for the BI team
* `valid_offer_available_flag` = indication if a hotel has a valid offer during the specified period (at least 1 minute within the 1 hour)
* `price_isd` = the `original_price` converted to USD
* `valid_from_date` / `valid_to_date` = indication of time date&time when the offer became active / inactive. Please note the offers cannot overlap for one hotel with the same parameters (checkin, checkout, source, breakfast)

#### ETLs

Please create scripts or procedures to transform the data from `primary_data` to the new tables in `bi_data`. Include the scripts to the repository.

The `valid_offers` table should show only valid offers with price converted to USD.

The `hotel_offers` table should indicate for each hotel if the hotel had offers for each day and hour. The days & hours when the hotel was not available should have indication `valid_offer_available_flag = 0`.

#### How to submit?

1. Create a new repository in GitHub
2. Write your notes to the `Readme.md` file in the repository.
3. Add the scripts to a sub-folder in the repository, push the code and send us a link to the repository

### 2. Data cleaning

* **Problem:** There are ocassionaly problems with the underlying data, there could be a bug in the production system or some of the data are manually adjusted.
* **Your objective:** Create a system to identify the outliers.
	* Create a new folder in the GitHub repository `data-cleaning`
	* Explain in a `/data-cleaning/Readme.md` file how would you design such a system, how could it run autonomously
	* Create a simple stored procedure to identify these outliers. No need to setup the whole autonomous system, just write the stored procedure. The name & functionality of the procedure is up to you.
	* Add the procedure to a new file `/data-cleaning/cleaning-procedure.sql`
	* Explain in the `/data-cleaning/Readme.md` file which outliers has the procedure been able to identify (just enumerate in bullet points)

### 3. API endpoint

Please prepare a single API endpoint in whatever language you chose (Nodejs, PHP, Ruby, Python, ...). Pick a language you're most familiar with or the one you'd like to experiment with - in any case get ready for some follow-up questions.

The endpoint should expose some of the data from the newly created table `valid_offers` based on the request parameters. It should return a JSON response with the best deal (discount) for the hotel/checkin/checkout parameters. In other words - this API endpoint should return the offer with the best discount.

Request GET parameters:

* `hotelId`
* `checkinDate`
* `checkoutDate`

Create an endpoint `/offer/best-deal` with example GET params:

* `/offer/best-deal?hotelId=1234&checkinDate=2015-11-11&checkoutDate=2015-11-12`

JSON output which your new endpoint should return:

```
{
	offerId: 12345678,
	hotelId: 1234,
	checkinDate: '2015-11-11',
	checkoutDate: '2015-11-12',
	sellingPrice: 234.34,
	currencyCode: 'USD'
}
```

#### How to submit?

1. Create a new repository in GitHub
2. Write your notes to the `Readme.md` file in the repository.
3. Add the scripts to a sub-folder in the repository, push the code and send us a link to the repository

If you host this project on some publicly available IP, please send us the URL.

We should be able to run the project on localhost without any hassle (expectations: no bugs, easy setup, well documented `Readme.md`...).


## Example output

This is the output we expect to get from you. But feel free to over-deliver!

*****

*Dear BI Team,*

*It was lots of fun with the BI assignment and I'm happy I did it! The links are below:*

1. *DataMart & ETL*
	* URL to the repository: [GitHub link](http://www.github.com/example/repo2)
	* More info with screenshots & comments: See the `Readme.md` in the repository
2. *Data cleaning*
	* In the same repository as (1), please see sub-folder `/data-cleaning`
		* Files: `/data-cleaning/cleaning-procedure.sql` and `/data-cleaning/Readme.md`
3. *API endpoint*
	* URL to the repository: [GitHub link](http://www.github.com/example/repo2)
	* More info: See the `Readme.md` in the repository

*Talk to you soon!*

*****

This will be enough for our team to jump on and evaluate. 

Good luck,

*~Your BI Team*

