## Use First Row as Headers
1. Launch Power BI Desktop, and click **Get** data on the Home ribbon.
2. **Choose Excel,** then navigate to and select Open on the [Failed Bank List.xlsx](http://https://github.com/fenago/ISM2410C/blob/main/Data/Failed%20Bank%20List.xlsx "Failed Bank List.xlsx") file that is available in the github files.
3. In the Navigator window, select the table called **Data**, then choose **Transform Data**. When the Power Query Editor launches, you should notice that the column headers are not automatically imported. In fact, the column headers are in the first row of the data.
4. To push the column names that are in the first row of data to the header section, select the transform called **Use First Row as Headers**** from the Home ribbon.

## Remove Columns

1. Multi-select (Ctrl + click) the column headers of the columns you wish to keep as part of your solution. In this scenario, select the columns Bank Name, City, ST, and Closing Date.
2. With these four columns selected, choose the down arrow for Remove Columns and choose Remove Other Columns

## Change Data Types

1. Locate the data type indicator on the column header to the left of the column name.
2. Click the data type icon, and a menu will open that allows you to choose whichever data type you desire

## Create Column from Examples

1. Find and select the Add Column tab in the Power Query Editor ribbon.
2. Select the Column From Examples button and, if prompted, choose From All Columns. This will launch a new Add Column From Examples interface:
3. Our goal is to leverage this feature to combine the City and ST columns together. In the first empty cell, type Barboursville, WV and then hit Enter. You will notice that the text you typed has automatically been translated into an M query and applied for every row in the dataset.
4. Once you click OK, the transform is finalized and automatically added to the overall M query that has been built through the user interface. The newly merged column will be added with the rest of your columns and you can optionally rename the column something more appropriate by double-clicking on the column header.

## Conditional Columns

1. Start by connecting to the FIPS_CountyName.txt file that is found in the github files using the Text/CSV connector.
2. Launch the Power Query Editor by selecting Transform Data, then start by changing the data type of Column1 to Text. When you do this, you will be prompted to replace an existing type conversion. You can accept this by clicking Replace current.
3. Now, on Column2, filter out the value UNITED STATES from the column by clicking the arrow next to the column header and unchecking UNITED STATES. Then, click OK.
4. Remove the state abbreviation from Column2 by right-clicking on the column header and selecting Split Column | By Delimiter. Choose -- Custom -- for the delimiter type, and type , before then clicking OK,
5. Next, rename the column names Column1, Column 2.1, and Column 2.2, to County Code, County Name, and State Abbreviation, respectively.
6. To isolate the full state name into its own column, you will need to implement Conditional Column. Go to the Add Column ribbon and select Conditional Column.
7. Change the New column name property to State Name and implement the logic If State Abbreviation equals null Then return County Name Else return null as shown in Figure 2.8. To return the value from another column, you must select the icon in the Output property, then choose Select a column. Once this is complete, click OK. This results in a new column called State Name, which has the fully spelled-out state name only appearing on rows where the State Abbreviation is null

## Fill Down

1. Right-click on the State Name column header and select Transform | Capitalize Each Word. This transform should be self-explanatory.
2. Next, select the State Name column and, in the Transform ribbon, select Fill | Down. This will take the value in the State Name column and replace all non-null values until there is another State Name value that it can switch to. After performing this transform, scroll through the results to ensure that the value of Alabama switches to Alaska when appropriate.
3. To finish this example, filter out any null values that appear in the State Abbreviation column.

## Unipivot

1. Launch a new instance of the Power BI Desktop, and use the Excel connector to import the workbook called Income Per Person.xlsx found in the github source files. Once you select this workbook, choose the spreadsheet called Data in the Navigator window, and then select Transform Data to launch the Power Query Editor. Figure 2.13 shows what our data looks like before the Unpivot operation:
2. Now, make the first row of data into column headers by selecting the transform called Use First Row as Headers on the Home ribbon.
3. Rename the GDP per capita PPP, with projections column to Country.
4. If you look closely at the column headers, you can tell that most of the column names are actually years and the values inside those columns are the income for those years. This is not the ideal way to store this data because it would be incredibly difficult to answer a question like, What is the average income per person for Belgium? To make it easier to answer this type of question, right-click on the Country column and select Unpivot Other Columns.
5. Rename the columns Attribute and Value to Year and Income, respectively.
6. To finish this first example, you should also rename this query Income.

## Unipivot 2

1. Remain in the Power Query Editor, and select New Source from the Home ribbon. Use the Excel connector to import the Total Population.xlsx workbook from the github source files. Once you select this workbook, choose the spreadsheet called Data in the Navigator window, and then select OK. 
2. Like the last example, you will again need to make the first row of data into column headers by selecting the transform called Use First Row as Headers on the Home ribbon.
3. Then, rename the column Total population to Country.
4. This time, multi-select all the columns except Country, then right-click on one of the selected columns and choose Unpivot Other Columns. The easiest way to multi-select these columns is to select the first column then hold Shift before clicking the last column:
5. Rename the columns from Attribute and Value to Year and Population, respectively

## Merge Query

1. With the Population query selected, find and select Merge Queries | Merge Queries as New on the Home ribbon.
2. In the Merge dialog box, select the Income query from the drop-down selection in the middle of the screen.
3. Then, multi-select the Country and Year columns on the Population query, and do the same under the Income query. This defines which columns will be used to join the two queries together. Ensure that the number indicators next to the column headers match. If they don't, you could accidentally attempt to join on the incorrect columns.
4. Next, select Inner (only matching rows) for Join Kind. This join type will return rows only when the columns you chose to join on have values that exist in both queries. 
5. Once you select OK, this will create a new query called Merge1 that combines the results of the two queries. Go ahead and rename this query Country Stats.
6. You will also notice that there is a column called Income that has a value of Table for each row. This column is actually representative of the entire Income query that you joined to. To choose which columns you want from this query, click the Expand button on the column header. After clicking the Expand button, uncheck Country, Year, and Use original column name as prefix, then click OK.
7. Rename the column called Income.1 to Income.
8. Finally, since you chose the option Merge Queries as New in Step 1, you can disable the load option for the original queries that you started with. To do this, right-click on the Income query in the Queries pane and click Enable load to disable it. Do the same thing for the Population query as shown in Figure 2.20. Disabling these queries means that the only query that will be loaded into your Power BI data model is the new one, called Country Stats

## Append Query

1. Launch a new instance of the Power BI Desktop, and use the Excel connector to import the workbook called Student Loan Complaints.xlsx found in the github source files. Once you select this workbook, choose the spreadsheet called Student Loan Complaints in the Navigator window, and then select Transform Data to launch the Power Query Editor.
2. Next, import the credit card data by selecting New Source | Text/CSV, then choose the file called Credit Card Complaints.csv found in the book source files. Click OK to bring this data into the Power Query Editor.
3. With the Credit Card Complaints query selected, find and select Append Queries | Append Queries as New on the Home ribbon.
4. Select Student Loan Complaints as the table to append to, then select OK
5. Rename the newly created query All Complaints and view the results
6. Similar to the previous example, you would likely want to disable the load option for the original queries that you started with. To do this, right-click on the Student Load Complaints query in the Queries pane and click Enable load to disable it.
7. Do the same to the Credit Card Complaints query, and then select Close & Apply.

## AI - Sentiment Analysis with Power BI

1. Launch a new instance of Power BI Desktop, and use the Excel connector to import the workbook called Hotel Ratings.xlsx found in the github source files. Once you select this workbook, choose the spreadsheet called Reviews in the Navigator window, and then select Transform Data to launch the Power Query Editor.
2. Select Text Analytics on the Home ribbon of the Power Query Editor. If this is your first time using this feature, you may be prompted to sign into a Power BI account that has Power BI Premium capacity assigned to it.
3. Next, you will be prompted to choose which Text Analytics algorithm you would like to use. Select Score sentiment, and ensure the ReviewText field is the Text that will be analyzed. Then click OK.
4. If prompted with a data privacy warning, click Continue and then select Ignore Privacy Levels check for this file before clicking Save. This type of warning can occur when you combine two disparate sources or services together and is to ensure it is OK for these data sources to be combined.
