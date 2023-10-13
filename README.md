# 2024-MLDS400-Group10

## Weekly Update
### 1. Week
1. Load the data
- Loading each of the datasets and checking if there are any issues or loading errors:
- dealing with importing issues due to inconsistent datastructure 
    During Exploration of Dataset "skuinfo" we found that about 8000 rows of the data have ambiguous data formats.
    Analysis resulted in the conclusion, that these rows have an addiinal comma seperated delimiter in column 10 and         therefore don't match the structure of the other rows.
    In order to explore the data we fixed that incosistency by subsetting the 8000 rows, merging together the values of      the ambiguous columns and concetanating it with the rest of the dataset.
- Since the transaction dataset is large we first tried to load just a subset of the data and afterwards the whole set
- we are working on loading the data into postgres to better access it from all devices

2. Understanding the data structure
- Inserting column headers
    All the datasets come without column headers. To explore the data and understand it we inserted the correct             headers to each column.
- We checked the dimensions of each data table to get an idea of the row numbers and column numbers
- We checked the datatypes
- We compared the columns to the meta information
- We dropped irrelevant columns (STRINFO and DEPTINFO had columns of 0s and 1s)

3. Summary statistics and unique values
- We looked at the summary statistics (min, max, mean, median, ...) of each numerical value
- Checking for missing values, outliers and unrealistic values
- count the number of unique values for each categorical value column

4. Plotting (EDA)
- Plotting histograms for all numeric value columns
- Visualize the data box plots, scatter plots check for anything abnormal
--> anthing special?
- we plot a correlation matrix for all columns of each dataset
- we plot a few pairplots
--> did anyone see some interesting pattern/ correlation?
