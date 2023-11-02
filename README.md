# 2024-MLDS400-Group10

## Weekly Update
### ~ October 13
1. Load the data
- Loading each of the datasets in jupyter notebook and checking if there are any issues or loading errors:
- dealing with importing issues due to inconsistent data structure 
    During Exploration of Dataset "skuinfo" we found that about 8000 rows of the data have ambiguous data formats.
    Analysis resulted in the conclusion, that these rows have an addiinal comma seperated delimiter in column 10 and         therefore don't match the structure of the other rows. The commas that appears in between could be representing period instead of a comma. 
    In order to explore the data we fixed that incosistency by subsetting the 8000 rows, merging together the values of      the ambiguous columns and concetanating it with the rest of the dataset.
- Since the transaction dataset is large we first tried to load just a subset of the data and afterwards the whole set
- we are working on loading the data into postgres to better access it from all devices

2. Understanding the data structure
- Inserting column headers
    All the datasets come without column headers. To explore the data and understand it we inserted the correct             headers to each column.
    - For example, no column names for 'SKSTINFO' file. We need to distinguish the dataset to know which column is SKU, which column is Store, which column is Cost, or which column is Retail.
- We checked the dimensions of each data table to get an idea of the row numbers and column numbers
- We checked the datatypes
- We compared the columns to the meta information

3. Summary statistics and unique values
- We looked at the summary statistics (min, max, mean, median, ...) of each numerical value
- Checking for missing values, outliers and unrealistic values
- count the number of unique values for each categorical value column

4. Plotting (EDA)
- Plotting histograms for all numeric value columns
- Visualize the data box plots, scatter plots check for anything abnormal
- we plot a correlation matrix for all columns of each dataset
- we plot a few pairplots

#### Next step:
- we plan to investigate first correlations between individual predictors.
- clean the data based on the initial analysis of this week.(Figure out the extra columns in transactions)
- upload tables to postgres

### October 14 - October 20
1. Created tables in pgAdmin 4. We can do simple SQL codes to understand the datsets in the database.

2. Cleaned transaction table:
- Two columns are identical except 7 rows. We drop the 7 rows and one of the duplicate columns.
- 'orgprice' has many 0.0 values, filled in some based on sku (assuming products with the same sku have the same original price). But we still have 1202550 missing prices.
- In some rows, amount paid is greater than original price. Are these erroneous data?
- quantity is almost entirely 1s except 7 rows, which are all returns, and all have very small amounts. Are these erroneous too?
- We are certain on all column names at this point and uploaded the data to postgres

3. SKSTinfo table:
- Figuring out four columns after cleaning:
    - First column: SKU (bigint)
    - Second column: Store (int)
    - Third column: Cost (float)
    - Fourth column: Retail (float)
- Some basic descriptive statistics.

4. SKUinfo table:
Goal this week: to further understand and explore the data
- First we checked the null values that are in each column. There are a total of 1564178 rows. For columns 0-10 (the column names for now are still numbers, we haven't figured out what each column exactly represents yet), there aren't any missing values, but for the last two columns, there are 1564158 rows that has missing values, which takes up pretty much all rows. 
- The data type for each columns are objects, so what we did is to convert column 0, 1, 2, 3, 7, 8, and 10 to numeric. We used the describe method to check the details of each column, and we checked the correlation between those columns and plotted a heatmap to clearly depict the results from the correlation matrx:

    - Column 0, 1, and 2: Column 0 has a very weak positive correlation with Column 1 (0.000502) and a weak negative correlation with variable 2 (-0.005997). These correlations are close to zero, suggesting little to no linear relationship. Variables 1 and 2 have a moderate positive correlation (0.113840).

    - Column 0, 1, and 2 with Variables 7 and 8: Column 0, 1, and 2 show little to no correlation with Column 7 and 8, as the correlation coefficients are close to zero (0.001641, -0.005743, -0.009226, -0.002837, -0.033439, -0.092607).

    - Column 7 and 8: Column 7 and 8 are negatively correlated (-0.099739).
    
    - Column 10: Column 10 also shows a weak positive correlation (0.031151) with column 7, suggesting a weak positive linear relationship between them.. 

- The results for the correlation matrix show that most correlations are close to zero (indicating weak or no linear relationships), except for the positive correlation between variables 1 and 2 and the moderate negative correlation between variables 7 and 8. 

#### Next step:
- understand what data is missing, and whether the missing data is random or not.
- fill more missing data based on information between tables 
- develop a relevant business question

### October 21 - October 27
1. SKUinfo table
- Continued EDA and cleaning up the table. 
- After reading in the csv, some columns were shifted due to ',' within values. We identified such rows, and combined the columns back together.
- After merging columns, a couple dozen rows do not have a valid 'vendor', but that shouldn't affect out analysis.
- Checked that 'sku', 'dept', 'packsize', 'vendor' all have correct data types
- Checked that 'dept' match with deptinfo table (all unique 'dept' can be found in deptinfo)

2. Some problems with the data
- 'classid' does not match with schema description. Description showed integers of length 4, but the table has integers with length 3, and also include characters. There are 1055 unique 'classid' in the whole table, within which includes 281 unique 'classid' that contains capital letters.

3. Came up with some business questions: 
    - focusing on some seasonality of the sales
    - How do price changes or discount campaigns impact sales and customer behavior?
    - Are there products that respond well to discounts, and others that do not?
    - What about the customer behaviors?

#### Next step:
- Figure out classid
- Determine what data is needed to answer business questions
- Visualization of data to explore business questions (e.g. correlation or trend)


### October 28 - November 3
1. We have conducted a preliminary meeting to gain an understanding of the datasets. This included clarifying the column names and grasping the structure of all four tables.

2. Formulated a set of business questions to guide our analysis:
- Investigating seasonality patterns in the transaction amounts (AMT).
- Identifying customer segments and their purchasing baskets.
- Conducting a profitability analysis.
- Analyzing return patterns and rates.

3. Addressed specific queries regarding the data:
- Clarified the distinction between 'barcode' and 'SKU'.
- Understood the relationship and hierarchy between 'style', 'class', and 'department'.
- Examined 'packsize' with a focus on values other than 1.
- Compared 'retail price' and 'original price'.
- Explored ideas for web scraping to augment our data.


#### Next Step:
- Continue to seek answers to any remaining questions.
- Proceed with further exploratory data analysis (EDA).
- Define the overarching business question we aim to address through our analysis.
