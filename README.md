# DataSourcing

## [FRED Data](https://github.com/GRDInvestmentSystemsConsultingInc/DataSourcing/tree/main/FRED)

### Project Purpose & Scope

Construct a dictionary containing all parent and child relationships, along with the series data that is available from FRED.  This will allow for:

1.  Greater understanding of the time series data that is available in FRED by centralizing data,

2.  The construction of a single dictionary upon which to build an automated data sourcing platform for analytical purposes (i.e. time series analysis, ML algo, charting, etc.)

3.  A programmatic approach to sourcing economic time series data,

4.  The current scope of the project is for the [Money, Banking, & Finance](https://fred.stlouisfed.org/categories/32991) category.

### Resources
1. FRED Homepage:  https://fred.stlouisfed.org/

2. FRED API Documentation:  https://fred.stlouisfed.org/docs/api/fred/

3. FRED Categories (Web):  https://fred.stlouisfed.org/categories

### FRED Data Stracture

FRED utilizes parent and child ids to link levels in a hierchial manner.  
The origin or root level parent id is assigned a value equal to zero (i.e. parent_id = 0) and each subsequent level is assinged a non-zero numerical value:

| child_id | name | parent_id |
| ----------- | ----------- | -------- |
| 32991      | Money, Banking, & Finance | 0 |
| 10   | Population, Employment, & Labor Markets | 0 |
| 32992 | National Accounts | 0 |
| 1 | Production & Business Activity | 0 |
| 32455 | Prices | 0 |
| 32263 | International Data | 0 |
| 3008 | U.S. Regional Data | 0 |
| 33060 | Academic Data | 0 |


The next level of categories for Money, Banking, & Finance:

| child_id | name | parent_id |
| ----------- | ----------- | -------- |
| 22 | Interest Rates | 32991 |
| 15   | Exchange Rates | 32991 |
| 24 | Monetary Data | 32991 |
| 46 | Financial Indicators | 32991 |
| 23 | Banking | 32991 |
| 32360 | Business Lending | 32991 |
| 32145 | Foreign Exchange Intervention | 32991 |

Note, that each child category within Money, Banking, & Finance (id = 32991) is assigned a child id.  
For example, child_id = 22 (Interest Rates) is linked to the prior higher level category using the parent_id field.

### General Process

1. To ensure all data levels were sourced for dictionary construction purposes, the [fred/category/children](https://api.stlouisfed.org/fred/category/children?category_id=13&api_key=abcdefghijklmnopqrstuvwxyz123456&file_type=json) api endpoint was used to call subsequent category levels until no further category information was returned.

2.  FRED does not specifically note where series data will appear.  Time series data may appear at a series data end point or within a category that is further segmented into child categories.  This was addressed within the solution.

3.  The following Excel file provides all the category relationships for the Money, Banking, & Finance category: [Category 32991 Parent-Child Category Relationships](https://github.com/GRDInvestmentSystemsConsultingInc/DataSourcing/blob/main/FRED/Category32991_parent_child_relationships.xlsx).  From left to right, each subsequent column within the Excel represents the child category of the prior until no further category levels are available.  Blank columns indicate that no further categories exist.
4.  All parent-child relationships are captured within the three levels presented within the Excel file.

### Jupyter Notebook: [MasterDictionary_Open_Category_32991.ipynb](https://github.com/GRDInvestmentSystemsConsultingInc/DataSourcing/blob/35e90405f01326e4f1d749c8cb3a1682174727b3/FRED/MasterDictionary_Open_Category_32991.ipynb)

This notebook illustrates how the parent-child relationships can be used in conjution with the dictionary for category 32991.  The notebook does not call any series data, as this was beyond the scope of this project, however the 'Series' API end point is used to call this data.  The user must request an API Key from FRED to source this data.
