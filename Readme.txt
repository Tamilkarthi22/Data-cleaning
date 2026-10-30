DATA CLEANING PYTHON USING JUPYTER NOTEBOOK

Import  CSV or Excel files 
Use the method that matches your files. Ensure the file is in the notebook's working folder or provide the full file path. 
CSV files 
cars = pd.read_csv("SalesCars.csv") 
Excel files
 cars = pd.read_excel("SalesCars.xlsx") 

Understand the data
Check rows and columns 
cars.shape 
result: (8000, 14), meaning 8000 rows and 14 columns.
View the first and last records
cars.head() 
cars.tail()
Check column names, data types, and non-empty counts
cars.info()
Count missing values in each column
cars.isnull().sum()
Count fully duplicated rows
cars.duplicated().sum()



Clean the data 
Remove exact duplicate rows 
cars = cars.drop_duplicates() 
This removes rows that match across every column. It does not automatically remove records that merely share a customer ID

Find Issues
Run these checks to locate records that need investigation:
Find repeated customer IDs
cars[cars["Model"].duplicated(keep=False)]
Find Units_sold outside the practice rule (100 to 1000)
cars[(cars["Units_Sold"] < 100) | (cars["Units_Sold"] > 1000)]
Find negative Profitability
cars[cars["Profitability"] < 1]
Display rows containing at least one missing value
cars[cars.isnull().any(axis=1)]

Validate the cleaned dataset 
print("Missing values:") 
print(cars.isnull().sum()) 
print("Exact duplicate rows:", cars.duplicated().sum())
print("Negative Profitability:", (cars["Profitability"] < =1).sum())

Validation confirms whether the cleaning steps worked. Also check that data types, ranges, row counts, and business rules are still correct



Analyze the cleaned data
Calculate average profit
 cars["Profitability"].mean() 
Calculate average profit by city
 cars.groupby("Brand")["Profitability"].mean()  

Count customers by Brand
 cars.groupby("Brand")["Model"].count()
Plot average salary by Brand
cars.groupby("Brand")["Profitability"].mean().plot(kind="bar") 
plt.ylabel("Average Profitability") 
plt.title("Average Profitability by Brand")
plt.tight_layout()
plt.show()

