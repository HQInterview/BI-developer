# BI assignment 

The goal of this BI assignment is to find out if you could join our BI star-team to help us build a world-class data-driven startup.

We expect you to have not just lots of experience with building a data warehouse, but also hand-on experience with programming in other languages such as Python, Go, Nodejs, or PHP.

We will be evaluating the overall quality of your output, incl. the code quality & cleaness, SQL query optimisation, proper usage of a versioning tool and human-readable comments.

The assignment is split into 3 parts:

1. Data warehouse & ETL load
2. Fix and clean the data
3. API endpoint

We expect you'll submit (1) and (3) to new separate public git repositories (i.e. GitHub) - more info below.

Please use `Readme.md` file in each repository to give us more info re. how did you approach the problem, why did you chose the solution you implemented etc.

### 1. Data warehouse & ETL

You can find these 3 tables in CSV files on AWS S3 (data storage):

* offer 
* hotel
* ..........XXX

Please download the 3 files and create a simple ETL & data mart.

1. Create a new MySQL database & load the 3 tables (above) 1:1 to a new schema: `primary_data`
2. Create new schema: `bi_data` with the structure below
2. Create an ETL process to extract, transform and load the data from `primary_data` schema to `bi_data` schema


#### Data structure of `bi_data`


#### How to submit?

1. Create a new repository in GitHub, push the code and send us a link to the repository (see format below).
2. Write your notes to the `Readme.md` file in the repository.




### 3. API endpoint

Please prepare a single API endpoint in whatever language you choose (Nodejs, PHP, Ruby, Python, ...). Pick a language you're most familiar with or the one you'd like to experiment with - in any case get ready for some follow-up questions.

The endpoint should expose some of the data from the newly created table based on the request parameters. It should return a JSON response with the best (lowest) price matching the criteria. 

For the purpose of this assignment **you don't need to take care of the currency exchange** - some prices will be in Thai Bath, some in USD... just return the lowest amount.

Endpoint URL:

* /offer

Request parameters:

* hotelId
* checkinDate
* checkoutDate

JSON output:

```
{
	offerId: 12345567,
	checkinDate: '2015-11-11',
	checkoutDate: '2015-11-12',
	sellingPrice: 234.34,
	currencyCode: 'USD'
}
```

#### How to submit?

1. Create a new repository in GitHub, push the code and send us a link to the repository.
2. Write your notes to the `Readme.md` file in the repository.


## Example output

This is the output we expect to get from you. But feel free to over-deliver!

===== ===== ===== ===== ===== 

*Dear BI Team,*

*It was lots of fun with the BI assignment and I'm happy I did it! The links are below:*

1. *DataMart & ETL*
	* URL to the repository: [GitHub link](http://www.github.com/example/repo2)
	* More info with screenshots & comments: `Readme.md` in the repository
2. *Fix and clean the data*
	* 
3. *API endpoint*
	* URL to the repository: [GitHub link](http://www.github.com/example/repo2)
	* More info: `Readme.md` in the repository

*Talk to you soon!*

===== ===== ===== ===== ===== 

This will be enough for our team to jump on and evaluate. 

Good luck! :-)

~HQ BI Team




