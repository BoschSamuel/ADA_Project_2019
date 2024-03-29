# How to ride the shopping cart

## Abstract

Let’s face it: grocery shopping is not a skill most of us intentionally took the time to pursue. However, people more than often find themselves in a situation where they return home with two bags of groceries and realize that they are missing the only item they initially were out for. Sometimes, not having a clear idea about our inventory state, we end up being tempted into the all sorts of treats that are over and above our necessities. Or we buy products to showcase our cooking abilities for the family dinner but somehow we end up with the fridge full of everything, hoping to roll up our sleeves tomorrow. We are often surprised by the amount of items we throw because the expiration date passed two months ago! However, that could change...

The core dataset for our project is the Dunnhumby dataset. It has (nearly) everything we need to tackle our research questions and find out the most reasonable answers.

## Main Research Question

In this project we try to address the following research question:

- Is there an interplay between income and expenses?

### Sub-Questions

In particular, we are interested in the following sub-questions:

- How do households choose to organize their limited annual income according to their shopping expenses?

- Can we infer different household types based on the relation between their income and transaction statistics?

- Are some demographic properties of the household's indicators based on this relation as well? That is, can we indirectly infer common family values from this data? 

## Dataset

### [Dunnhumby](https://www.dunnhumby.com/careers/engineering/sourcefiles)
This dataset will be the main dataset used for our project. It can be downloaded from the website by registering with your full name and email. We analyzed the .pdf user guide for the source files provided with the downloaded .zip file to get a good idea about whether the data contains everything we require for the questions we wish to answer.
The Dunnhumby dataset contains household level transactions over the period of two years from a group of 2,500 households that are frequent shoppers at a retailer. It contains the purchases of each household, and not just those arising from a limited number of categories. For certain households, demographic information as well as direct marketing contact history are included.
The data is in a textual form, represented as a collection of .csv files where each file contains information from a certain table of a relational database. As such, the data can easily be loaded into a local schema or parsed using Pandas. We also expect the data to not contain many inconsistencies, since it must be exported from a database with a relational model.

Below we provide a description of some of the useful files for our project:

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

## List of steps completed until milestone 2

1. Definition of project goal 
- Identification of influencing factors to analyse
2. Preprocessing
- Loading the data
- Identifying and handling missing and incomplete data
- Using the formulas in the documentation to calculate new features
- Type conversion and distribution analysis of categorical data
- Data merging
3. Data Analysis
- Calculation of derived statistics to measure household expenses
- Analysis of underlying distributions of key statistics
- Correlation comparison
- Analysis of joint distributions of income and statistics measuring expenses
4. Trend discovery
- Distribution of coupon usage across income categories
- Distibution of expenses across days of the week
- Mapping between income, expenses and product categories
- Engel curves
- Demographic analysis of 4 households groups derived from income and expenses
5. Applied ML
- Cluster discovery in households based on demographics and income

## Planned steps for until milestone 3

- Dealing with outliers in data and plots
- Interpolation of probability distributions of categorical features
- More thorough analysis of derived statistics measuring expenses: limitations, robustness, improvement
- Identify meaning of household clusters and expand the ML analysis
- Writing of data story
