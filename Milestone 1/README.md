# How to ride the shopping cart

## Abstract

Let’s face it: grocery shopping is not a skill most of us intentionally took the time to pursue. However, people more than often find themselves in a situation where they return home with two bags of groceries and realize that they are missing the only item they initially were out for. Sometimes, not having a clear idea about our inventory state, we end up being tempted into the all sorts of treats that are over and above our necessities. Or we buy products to showcase our cooking abilities for the family dinner but somehow we end up with the fridge full of everything, hoping to roll up our sleeves tomorrow. We are often surprised by the amount of items we throw because the expiration date passed two months ago! However, that could change...

The purpose of this project is to explore the trends in transactions, recognize anomalies, find connection between items and delicious recipes, discover the intentions behind the transactions, classify the households to get better understanding of their values, and gain insights on whether or not people take grocery shopping for granted. Having this information in our hands, we can draw conclusions and propose effective methods to people in order to make their next visit to the market an enjoyable experience.

The core dataset for our project is the Dunnhumby dataset. It has (nearly) everything we need to tackle our research questions and find out the most reasonable answers.

## Research questions

- Do people take grocery shopping as a guessing game?
	- *Awareness of the contents in their inventory*
- Do people take hunger as an advisor to the store?
	- *Intention vs. impulse*
- Do people join the pantry minimalist movement?
	- *Preventing overstocking*
- Are people realistic about their cooking enthusiasm?
	- *Keep cooking simple*
- Do people create a positive eating environment?
	- *For them and their family*
- Quality over quantity?
	- *The effect of campaings*
- Interplay between income and expenses?
	- *Family values*

## Dataset

### [Dunnhumby](https://www.dunnhumby.com/careers/engineering/sourcefiles)
This dataset will be the main dataset used for our project. It can be downloaded from the website by registering with your full name and email. We analyzed the .pdf user guide for the source files provided with the downloaded .zip file to get a good idea about whether the data contains everything we require for the questions we wish to answer.
The Dunnhumby dataset contains household level transactions over the period of two years from a group of 2,500 households that are frequent shoppers at a retailer. It contains the purchases of each household, and not just those arising from a limited number of categories. For certain households, demographic information as well as direct marketing contact history are included.
The data is in a textual form, represented as a collection of .csv files where each file contains information from a certain table of a relational database. As such, the data can easily be loaded into a local schema or parsed using Pandas. We also expect the data to not contain many inconsistencies, since it must be exported from a database with a relational model.

A description of some of the most useful files:

`hh_demographic.csv` - 801 rows, ~45 KB
This table contains demographic information for a portion of the households.
Columns:
 - HOUSEHOLD_KEY: Id of the household
 - AGE_DESC: Estimated age range, categorical
 - MARITAL_STATUS_CODE: Marital status (A - Married, B - Single, U - Unknown), categorical
 - INCOME_DESC: Household income (in ranges), categorical
 - HOMEOWNER_DESC: Type of homeownership (Renter, Homeowner etc.), categorical
 - HH_COMP_DESC: Type of household composition (Single Female, 2 Adults No Kids etc.), categorical
 - HOUSEHOLD_SIZE_DESC: Number of people in the household (0-5+)
 - KID_CATEGORY_DESC: Number of children in the household (0-3+)

`transaction_data.csv` - 2595732 rows, ~140 MB
This table contains all the products purchased by households within this study. Each line found in this table is essentially the same line that would be found on a store receipt. It is explained in the user guide that the value of sales in this table is not the real price of the purchased product. However, a formula is provided to calculate the real price using the quantity and coupon discounts.
Columns:
 - HOUSEHOLD_KEY: Id of the household which made the transaction
 - BASKET_ID: Id of the transaction
 - DAY: On which day the transaction occured, integer 1-711, so we have transactions for 711 different days or about two years
 - PRODUCT_ID: Id of the product
 - QUANTITY: Number of instances of the purchased product, positive integer
 - SALES_VALUE: Amount of dollars the store received (in dollars, including discounts from coupons and sales), float
 - STORE_ID: Id of the store
 - TRANS_TIME: Time of the day when the transaction occured in 24hr format, 0000-2359 
 - WEEK_NO: Week of the transaction, 1-102, so we have transactions for 102 different weeks
 - RETAIL_DISC: Discount applied due to the store's loyalty card program, negative float
 - COUPON_DISC: Discount applied to the amount of money client payed due to a coupon, negative float
 - COUPON_MATCH_DISC: Discount applied to the amount of money the store received due to a coupon, negative float

`product.csv` - 92353 rows, ~6 MB
This table contains information on each product that was sold.
Columns: 
- PRODUCT_ID: Id of the product
- DEPARTMENT: Most general first-level product categorization
- COMMODITY_DESC: Second-level product categorization
- SUB_COMMODITY_DESC: Lowest third-level categorization of the product
- MANUFACTURER: Id of the product's company/manufacturer
- BRAND: Type of manufacturer, Private or National
- CURR_SIZE_OF_PRODUCT: Package size of the product, textual, number + various measurement units

The tables `campaign_table.csv` and `campaign_desc.csv` provide information about the campaigns received by each household and the starting and ending date of each campaign. The tables `coupon.csv` and `coupon_redempt.csv` provide information about all the coupons sent to customers as part of the campaign, as well as the products for which each coupon is redeemable, and also which household redeemed which coupon and when. All of this information overall will be useful to analyze the effectiveness of each campaign.

The final table `causal_data.csv` (36786524 rows, ~680 MB) contains information about how all the products were marketed in every store, each week. Information whether and how the product was on the display in the store and in mailed catalouges is provided in categorical format. As of now, we believe we may not require this information in its full form for our analysis. Nevertheless, we will use it as a way to look more deeper into the selected customer's behaviour when buying certain items.


### [Recipe1M+](http://pic2recipe.csail.mit.edu)
In addition to the Dunnhumby dataset, we wish to enrich our data with external information. For one of our research questions we require information about which food products are commonly combined together in recipes to make various dishes, so that we are able to analyse cooking habits of the shoppers.
The Recipe1M+ dataset contains over 1 million recipe entries, where each recipe is linked to a list of required ingredients, list of required steps and an image of the prepared dish. The original purpose of this dataset was to create a deep learning recipe classifier.
The dataset can be downloaded only by registered users and, after creating an account and logging-in to the website, the dataset can be accessed. As we solely require the ingredients, we only downloaded the file containing lists of ingredients attached to the recipe ids.
This file (~350 MB) was encoded in JSON format and can be easily parsed.
To successfully merge this data with the previous one, we will need to find which of the products in the Dunnhumby dataset appear in the recipe ingredients and construct a mapping. Therefore, after this process we might end up using only the part of the ingredient data from Recipe1M+.


## A list of internal milestones up until project milestone 2

- Perform data preparation and store data for analysis
- Inspect the data for inconsistencies
- Compute product prices using formula in the description
- Analyze the data on transaction level for shopping patterns
- Find a link between shopping products and recipes
- Find keywords in product names related to healthy lifestyle
- Analyze the data on campaign level
- Categorize households based on income and expenses


## Questions for TAs

- Are the scope of our project and research questions adequate for this course? If it's too broad or too narrow, what would be your recommendation to change it?
- Do you suggest to us including any external data sources? If yes, what kind?
- What types of visualizations might be the best for data such as ours?
- Should we show results even when we do not find any common pattern? Is it fine to discard a research question in such case?