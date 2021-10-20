# Introduction 

## What is ETL?
1. ETL stands for “extract, transform, and load.”  
2. Extraction - refers to retrieval of data from a data source (Database) to a local/remote location in various file formats (commonly used are XLS, .csv). 
3. Transformation refers to the modification of a data set to be loaded to or being extracted from a data set. It might also involve merging and selective retrieval of data. 
4. Loading means uploading a data set into a data source, the data could be raw as loaded from your local location or could be transformed by a set of modification operations applied by you.

## How is it useful? 
1. Part and parcel of the work, to get different data sets, upload them into databases.
2. Loading and retrieval could also involve selective modification of the data set. 
3. Sometimes these sets of operations need periodic scheduling. Hence, requires some tool that should be easily configurable and usable, plus also serve all the requisite use cases. 
4. Talend solves all the use cases that we need in terms of Data ETL. 

## What is Talend?
1. ETL tool for Data Integration.
2. Software solutions for data preparation (you can apply transformations), data quality, data integration (merge data), loading data into the data systems, extract data from data systems into different file formats.
3. Objective is to help learn fundamentals of the Talend tool for basic ETL operations used extensively in different use cases we come across.

# Setting up Talend

## System Requirements

The following are the system requirements to download and work on Talend Open Studio:
* **Recommended Operating systems** Microsoft Windows 10 or Apple macOS 10.13/High Sierra
* **Memory Requirement**  Memory - Recommended 8 GB, Free Storage Space - >=30 GB

*Note − Java 8 must be available with environment variables already set.*

## Installation of JDK 8

1. In order to use Talend, you need to have JAVA 8 and JDK installed
2. You can check that from your Command Line to see if java is installed and what version
3. For Windows, Open command prompt and enter command java -version. If installed, the version is installed, else error message. Make sure it is Java 8
4. For Mac OS, open terminal and enter command java -version. If installed, the version is installed, else error message. Make sure it is Java 8
5. Use this link to install the JDK for your corresponding OS 
6. Once downloaded, install it.

## Talend Installation

1. To download Talend Open Studio for Big Data and Data Integration, please follow the steps given below −
2. Go to this link and click the download button. TOS_BD_xxxxxxx.zip file will start downloading.
3. After the download finishes, extract the contents of the zip file, it will create a folder with all the Talend files in it.
4. Open the Talend folder and double click the executable file: TOS_BD-win-x86_64.exe. Accept the User License Agreement. 
5. Create a new project and click Finish. Click Allow Access in case you get Windows Security Alert.
6. Now, the Talend Open Studio welcome page will open. 
7. Click Finish to install the Required third-party libraries. Accept the terms and click on Finish.
8. Now your Talend Open Studio is ready with necessary libraries

# Using Talend

## Project Operations in Talend (Creation/Import)

### Creating a Project

1. Double click on TOS Big Data executable file, the window shown below will open.
2. Select Create a new project option, mention the name of the project and click on Create.
3. Select the project you created and click Finish.

### Importing a Project

1. Double click on TOS Big Data executable file, you can see the window as shown below. 
2. Select Import a demo project option and click Select.
3. You can choose from the options shown below. Here we are choosing Data Integration Demos.
4. Click Finish.
5. Now, give the Project name and description. Click Finish.
6. You can see your imported project under the existing projects list.
7. Now, let us understand how to import an existing Talend project. 
8. Select Import an existing project option and click on Select.
9. Give Project Name and select the “Select root directory” option.
10. Browse your existing Talend project home directory and click Finish.
11. Your existing Talend project will get imported.
12. Opening a Project
13. Select a project from an existing project and click Finish. This will open that Talend project

### Create a new Job

1. When you launch a new project, you see an option to create a new Job
2. Click on Create a new Job option
3. Enter the name,description and purpose of the job
4. Click on Finish
5. You will be redirected to the main Talend View.
6. You will now see a palette of options on the right side of main tab, which will be used to select the components you will need to perform ETL Operations

### Walkthrough of Major Components

Once you create a Job, you will enter the Job view. The main section to go through is the Palette window view on the right side of Job View. Palette contains all the components you will need to create the Jobs

![image](https://user-images.githubusercontent.com/63345263/138073907-38423372-eb04-49bc-873a-5a99d4fc8119.png)

1. **DB Components** - Under the Databases option, you will see DB Specific options, which contain DB upload or extraction operators. The most relevant ones are under PostgresSQL - ttPostgresqlInput and ttPostgresqOutput 
     * **tPostgresqlInput** - Reads a database and extracts fields based on a query
     * **tPostgresqOutput** - Writes, updates, makes changes or suppresses entries in a database.
2. **File Components** - Used for File input and output operations.
     * **tFileOutputDelimited** - Output data to a delimited file eg. CSV. This component writes a delimited file that holds data organized according to the defined schema.
     * **tFileInputDelimited** - Reads a given file row by row with simple separated fields. Opens a file and reads it row by row to split them up into fields then sends fields as defined in the Schema
     * **tFileInputExcel** - Reads an Excel file (.xls or .xlsx) and extracts data line by line. Opens a file and reads it row by row to split data up into fields using regular expressions. Then sends fields as defined in the schema
     * **tFileOutputExcel** - Outputs data to an MS Excel type of file. Writes an MS Excel file with separated data value according to a defined schema.
3. **Data Quality components** - Modification and control of data quality
      * **tUniqRow** - Compares entries and sorts out duplicate entries from the input flow.
4. **Processing components** - Family of components that allow you to work with & transform your data.
      * **tFilterRow** - Filters input rows by setting one or more conditions on the selected columns.
     * **tMap** -  One of the most commonly used components. Transforms and routes data from single or multiple sources to single or multiple destinations.
     * **tSortRow** - Sorts input data based on one or several columns, by sort type and order

### Setting up Database Connection

1. In order to perform an ETL task, you will need to connect it to the DB wrt which the operation is to be performed.
2. On the left side you will see a Repository window
3. The repository window will contain an expandable option of Metadata
4. Click to expand Metadata. Under metadata the first option is Database Connections
5.If you expand this option, you will see all the Databases you would have connected to in the past
6. Right click on Database connection. You will see an option of Create connection
7.Click on the option. 
8. A window will open. Enter the name by which you want to save the connection. Then, click next
9. Select the DB Type. For most of our commonly used Databases, the type will be PostgresSQL.
10. Enter the username of the database under the login textbox. Enter the password
11. Enter the Hostname and port for the DB
12. On the bottom right of the dialog box, you will see a “Test Connection” option.
13. Click this option to test if the connection is working successfully. If running for the first time, you will be asked to download a couple of dependencies or libraries. Accept the download
14. If the connection details are working fine, you will see a successful connection message
15. Click Finish. The connection will be added to the list of DB Connections
16. Extracting Data from a DB Table
17. The first task is to extract data from a  DB Table to a CSV.

### Retrieving Table Schema

1. In order to extract the table, first you will need to retrieve that table from the DB schema
2. Go to the DB connection corresponding to the DB from which you want to extract the data from
3. Right click on the DB Connection, then select the Retrieve the DB Schema option
4. Schema selection Dialog box will open
5. Click Next, then select the relevant schema which you want to extract table data from
6. List of tables will be rendered. Check the relevant tables
7. After selecting the relevant tables, click on Finish
8. You will see the tables under the Table Schema option of the same DB Connection

### Creating a Extraction Job

1. Under the palette option on the right end, select Databases >> DB Specifics >> PostgresSQL
2. Drag the tPostgresSQLInput to the main Job window.
3. Under the job window you will see 4 tabs - Job, Contexts, Component, Advanced
4. Double click on the tPostgresSQLInput and then select Components window
5. You will see multiple options under Components window
6. Check if the database type selected is PostgresSQL
7. Under the Property Type dropdown select Repository, once you select that a new dropdown will appear on the right
8. Select the DB connection for which you want to want to create Extraction job
9. The details of the DB like host,credentials will get autofilled
10. Under the schema option, click on 3 dots, and then a dialog box will launch
11. Select the db connection >> Table Schema >> Table for which you want to extract data for
12. The Table name will be auto filled
13. To the right of Query Type, select the Guess Query option, the SELECT query at bottom will be updated and you can remove irrelevant columns which you don’t want to extract
14. Then select tMap from the palette and also drag it to the job window
15. Also select tFileOutputDelimited and drag it to job window
16. Connect the DBInput to the tMap and then connect tMap to the tFileOutputDelimited
17. Double click on the tMap, and then drag and drop the columns you want to add to the CSV file, and then click save
18. Double click on the Delimited file and then in the component window at the bottom, select the separator to be “,”. Also, if you want to add the header to the columns, tick the header box
19. Under the advanced settings, uncheck the box of “Throw an error if the file already exists”
20. You can change the name of the output file under the component tab
21. Once done, go to the Run window and then run the job. If run successfully, the data will be available on your system as a CSV file

### Uploading Data to Talend

#### Creating a Delimited File

1. Click on the Metadata on the left window.
2. Right click on the File Delimited option
3. A file upload dialog will launch
4. Enter the name of the file. Click Next. Browse to select the CSV file you want to upload
5. Under the option Field Separator, choose comma
6. Under escape char settings, select CSV Radio button
7. Under Escape Char and text enclosure choose “\””
8. Under the preview option, check the box if the top row is a heading row, and has to be ignored. Then click Refresh Preview
9. Click Next
10. You will see the column names there imported from the CSV. You can change column names as per your convenience
11. If any of the column needs to be unique, check the Key checkbox
12. Also, you can change the value in length column, which constraints the maximum length of any value
13. The type denotes the data type that it will be stored in. Most commonly used are Integer, String, Date, boolean, float,double
14. For Float and Double types you can change the precision value
15. For Data pattern you can define the Data format like DD-MM-YYYY or DD-MM-YYYYTHH:MM:SS
16. Default column is used to override the values which are blank for a particular column
17. Once done, click on finish and the file will be uploaded
18. **Please note that you link the path to the CSV file not the actual file is uploaded which means, if the rows are added to csv the data is loaded automatically, but if the schema is changed, then you might need to edit the file schema.**

#### Creating a new Table via CSV

1. Drag the input delimited file created to the Job Window
2. Then select tMap from the palette and also drag it to the job window
3. Go to palette >> Databases >> DB Specifics>> tPostgresSQLOutput
4. Drag it to the job window
5. Connect tFileInputDelimited → tMap → tPostgresSQLOutput
6. Double click on tPostgresSQLOutput
7. Select the relevant DB into which you want to load data from repository
8. Then if you want to create a new table, enter the name of table in double quotes in Table field
9. Under the action option, select “Create Table if it does not exist” and select Insert option under Action on data option
10. Double click on tMap and then drag to the output which columns you want in the output table
11. Click Apply >> Save >> Accept to propagate changes
12. Run the Job
13. You can check on PGAdmin if the table is successfully created with data added

#### Insert data to existing Table via CSV

1. Drag the input delimited file created to the Job Window
2. Then select tMap from the palette and also drag it to the job window
3. Go to palette >> Databases >> DB Specifics>> tPostgresSQLOutput
4. Drag it to the job window
5. Connect tFileInputDelimited → tMap → tPostgresSQLOutput
6. Double click on tPostgresSQLOutput
7. Select the relevant DB into which you want to load data from repository
8. Then if you want to import data from an existing table, make sure that you have retrieved data from an existing DB Connection
9. Under the table, select the relevant table
10. Make sure that column names in your CSV match with table column names, else you will have to map via tMap
11. Under the action option, select “Default” and select Insert option under Action on data option. If there is a chance that your new data might override existing data, then select the Insert or Update option. Also in this case it is essential to mark the key in case of while uploading CSV, to identify anchor around which data is to be updated
12. Double click on tMap and then drag to the output which columns you want to add in the output table
13. Click Apply >> Save >> Accept to propagate changes
14. Run the Job
15. You can check on PGAdmin if the data is successfully added


