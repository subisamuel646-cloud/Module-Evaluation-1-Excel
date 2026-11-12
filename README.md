# Module-Evaluation-1-Excel
Module Evaluation 1:: Excel
Data Cleaning: (5 marks)
1) Check for the number of missing values marked with '?' in each column of the “Medical
Examinations” Table and "Hospitalization Details" Table.

Sol: We can use =COUNTIF(A2:I2344,"?*") ---> For range select the entire dataset

In power query , we can replace '?' with "Null" using Replace Values option in Home tab
Then View ---> Check column quality and column profile ---> Hover over each column to view the null counts

2) Fill in the missing values of ‘month’ with Sep and ‘year’ with its average rounded to the
nearest integer.

Sol : Find and Replace --> Find ? and replace with "Sep"
	Find the average value of the column "year" =ROUND(AVERAGE(B2:B2344),0)
	Then use Find and replace. Find what "?" and Replace "1983"

In Power Query, Home --> Replace Values
Select the Year column --> Transform --> Statistics --> Average --> Note the value as rounded integer(1983) and use Home --> Replace values

3) Determine the most frequently occurring values in the ‘smoker’, 'Hospital tier' and 'City
tier' columns, and fill in the missing values accordingly.

Sol: Find and Replace function or IF(G2="?",tier - 2,G2)

In power query, Find the most frequent value using Value Distribution tab at the bottom by clicking on the column ----> View ---> Column profile
Home ---> Replace Values

4) If any 'State ID' values are missing, consider filling them with 'Unknown' or using another
appropriate strategy

Sol : IF(I2="?",Unknown,I2) Using this formula we can replace the values

Home --> Replace Values


Data Transformation: (8 marks)
1) Split the ‘names’ column in the “Customer Names” Table into 3 meaningful columns: ‘Title’, ‘First Name’, and ‘Last Name’.

Sol: Select column ----> Duplicate column
Last name : Select duplicated column ---> Home --> Split column --> By delimiter 1. Comma 2. Left most --->OK
Title : Select duplicated column ---> Home --> Split column --> By delimiter 1. Custom "." 2. Left most --->OK
First Name : Name the column and trim and clean or format each columns

2) Convert the "NumberOfMajorSurgeries" column in the “Medical Examinations” Table to numerical data by replacing non-numeric characters with meaningful numerical values.

Sol: Select column ---> Home ---> Replace Values ---> "No major surgery" with "0" ---> Ok
Then change type of column as "Whole Number"

3) Check for inconsistencies in the 'Heart Issues' and 'smoker' columns and propose corrective actions if necessary.

Sol: Checking for case sensitivity and all
Select the column ---> Transform ---> Format (Clean, Trim , Capitalize each word)

4) Create a new column named “Weight Status” that categorizes BMI into different categories as below:

Sol: Select column ---> Add column ---> Conditional column ---> Specify the conditions --->Ok

5) Create a new column named “Diabetes Status” and fill it as per the information given below:

Sol: Select column ---> Add column ---> Conditional column ---> Specify the conditions --->Ok

6) Merge ‘year’, ‘month’ and ‘date’ columns in the “Hospitalization Details” Table into one
column named ‘Date of Birth’ and format it in ‘DD-MMM-YYYY’ custom format.

Sol: Reorder the columns as Date, Month, Year ----> Select all 3 columns ---> Transform ---> Merge Columns ---> Specify needed --> ok
Select the new column ---> Change type (if needed)

7) Calculate the ‘Age’ of each customer based on their ‘Date of Birth’ and the date of
collection of the dataset, which is 8th June 2023.

Sol : For the sample date given ----> Add column --> Custom column ---> Name as Reference Date and #date(2023, 6, 8) this formula --> ok
Change the type of Both columns to date before calculation
Select both columns ---> Add column --> Date --> Subtract Days ---> Column with values appears as Subtraction
Select the subtraction ---> Add column ---> Custom column ---> Age and Number.RoundDown([Subtraction] / 365.25) ---> Ok

8) Format ‘charges’ column as currency ($).

Sol : Select the column ---> change type


Data Exploration, Analysis & Visualization: (12 marks)

➢ Create a new sheet named “Healthcare", combine all three tables into one, using Customer ID as the common column, utilizing VLOOKUP.
➢ Retain the following necessary columns: Customer ID, First Name, BMI, HBA1C, Heart Issues, Any Transplants, Cancer history, NumberOfMajorSurgeries, smoker, Weight Status, Diabetes Status, Date of Birth, charges, Hospital tier, City tier, State ID, Age.

Sol: Copy the columns needed --> For CustomerID column copy the unique ID set from the base table then VLOOKUP
VLOOKUP(A2,Medical_Examinations,2,FALSE) like this for the columns needed
For date column, it comes in serial number format, select the data and change type as needed

Create pivot tables if required to do the following analysis, then visualize through charts:
----> Make the vlookup data as table ---> Select complete dataset with header ---> Insert --> Pivot Table --> In new worksheet --->ok

Analysis using Pie/Donut Chart:
➢ What is the distribution of cancer history among smokers and non-smokers?

Sol: In Pivot, Rows : Smokers , columns : Cancer , Values: Count of CustomerId
Select the pivot ---> PivotTable Analyze --> Pivot Chart --> Pie ---> Format

➢ How does the total number of major surgeries and average HbA1C differ between
patients with and without a history of transplants?

Sol: In pivot, rows : Any transplants, Values : No. of major surgeries and Hba1C
Select the pivot ---> PivotTable Analyze --> Pivot Chart--> Pie --> Format


Analysis using Column/Bar Chart:
➢ How do healthcare charges vary based on different weight statuses and diabetes
statuses?

Sol: In pivot, rows : Weight Status, Columns : Diabetes Status , Values : Charges
Select the pivot ---> PivotTable Analyze --> Pivot Chart--> Column --> Format

➢ Can you compare the average charges for each hospital tier within different states?

Sol: In pivot, rows : State ID, Columns : Hospital tier , Values : Average of Charges
Select the pivot ---> PivotTable Analyze --> Pivot Chart--> Bar --> Format


Analysis using Line/Scatter Plot:
➢ Is there any correlation between age and both BMI and HbA1C in the dataset?

Sol: Copy the healthCare dataset to new sheet --> Sort the dataset by Age ---> CTRL and Select both columns ---> Insert --> scatter Chart for Age and BMI --> Format
Do the same for Age and HbA1c.

➢ Explore the relationship between age and healthcare charges.

Sol: Copy the healthCare dataset to new sheet --> Sort the dataset by Age ---> CTRL and Select both columns ---> Insert --> scatter Chart for Age and Charges --> Format

Dashboard Creation:
➢ Build an interactive dashboard that consolidates all key insights using the above visualizations. Ensure visual clarity and ease of interpretation for all chart types.

Sol: Add a new sheet then Copy and paste all required pivot tables and charts required for the Dashboard and format.

➢ Add slicers for the fields “Weight Status” and “Diabetes Status” to enable filtering across

Sol: Go to the pivot table of the above ---> Pivot Table Analyze Tab ---> Insert slicer --> Select which ones we need --> ok
Paste it on the dashboard and arrange
We must create the connections so that slicer selection affects all the charts and table --> Click inside slicer ---> Slicer --> Report Connections ---> Select the ones needed --> ok
