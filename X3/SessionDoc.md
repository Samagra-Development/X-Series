_Pre-Requisite_ *__Please refer this [link](https://www.metabase.com/docs/latest/users-guide/02-database-basics.html) for a basic refresher on database basics.__*

# What is Metabase?

An **open-source** basic **Business intelligence** tool to **help visualise** and display your data in a **insightful and user centric manner**

# Why Metabase?

1. Ability to connect different databases
2. Feature set
3. Set of Visualisations offered
4. Open source community
5. Ease of deployment
6. Ease to use GUI (Ease in configuration of database)

# Setting up Metabase locally

## Pre-requisites 

- Docker installed on system. Please refer this [link](https://github.com/Samagra-Development/X-Series/blob/main/X1/InstallationGuide.md) to setup docker on your machine.

## Installing Metabase locally

- Once you have followed the installation steps (i) to (vi) correctly under the [link](https://github.com/Samagra-Development/X-Series/blob/main/X1/InstallationGuide.md), then run following command on your command prompt  
   ```txt
      docker ps
   ```
- Once the command is run, you would see in your logs that metabase engine is running, like in the image mentioned below. *This is the local instance of Metabase that you can use for 
  practising.
  ![image](https://user-images.githubusercontent.com/63345263/132385263-caa9ab07-58e4-48fc-b108-bcd60cb0f793.png)
- Whenever in future, you wish to run the metabase instance, start the docker on your command prompt by going first to the database directory. *(Similar to step-1 above)*, and then running the following
  command
  ```txt
      docker-compose up -d
   ```
- Now open your Chrome and open the following url http://localhost:5003. Metabase GUI should open
  ![image](https://user-images.githubusercontent.com/63345263/132385539-0571631f-04e3-4246-be29-467cab1ce041.png)
-  Set up the metabase with your details and setting the login credentials
-  Once done you will land on the home page.

# Product Walkthrough

## Home Page Overview
![image](https://user-images.githubusercontent.com/63345263/132389131-3189f689-4ed5-43b1-9965-d728ec52bf79.png)
![image](https://user-images.githubusercontent.com/63345263/132389310-3b954a19-c877-4d97-b052-f66cf1ad039c.png)

Following elements are found on the home page

1. Pinned Items
2. Previously collected dashboards and collections
3. A list of the databases you’ve connected to Metabase.

## Menu Features
1. Asking Questions
2. Browsing Data
3. Create Option (Creating a Dashboard/Pulse)
4. Native SQL Query Editor
5. Settings - Admin, Account Settings, Sign out

## Admin Capabilities
1. [Connecting Database](http://localhost:5003/admin/databases)
2. [Caching Databases](http://localhost:5003/admin/settings/caching)
3. [Localisation](http://localhost:5003/admin/settings/localization) and Visualisation settings

# Connecting a Database
1. Go to the Settings Tab
2. On the top of settings tab, Click on *Databases*
3. Click on **Add Database** on the top right, In order to connect the database
4. Inside the form fill the following details
   **DB Type** - PSQL (most of the databases used in Samagra are PSQL)
   **Name** - Descriptor how you want to access the Database later
   **Host** - db (In case of the remote database, enter the IP address of the DB)
   **Port** - 5432 (Port on which the DB running)
   **Database name** - dbname (Name of the database)
   **Username** - user (Wwhat user you use to login to the Database?)
   **Password** - dbpassword (Password to the Database)
 5. Click on Save button at the bottom, you should see a success message. Now you can see the database under the Home tab and also under Browse Data tab.

# Edit Metadata using Data Model
1. Help Save time and cluttering
2. To make changes to your metadata in Metabase, visit the Data Model tab in the Admin Panel. The Data Model tab displays options to edit metadata for the database, tables, and columns. For example, you can edit a column’s name, visibility, type, and description. You can also remap foreign keys to give human readable names to foreign key columns!
3. Here are some ways editing metadata can make life better for your users:
   - When column names are confusing, you can change their names or add a description.
   - If you have address columns, you can hide them from your users to protect privacy.
   - You can pick your preferred filter interface from three options (search box, list of values, or plain input box).
4. **Perhaps the most important piece of metadata you can change is the data type.**

![image](https://user-images.githubusercontent.com/63345263/132396498-3d014706-bc02-4294-9501-765bcb649352.png)

# Asking Questions

## What is a Question?
- A question is essentially a query performed on the data. Think of it as a question you are asking the data – How many students were enrolled district wise, gender wise at a time in the state? 
- Available on the top right side of the home pag
- Many analytics questions can be answered with just four steps:
  - Join a couple of tables to get all the required information in one place.
  - Filter the data so that it only includes the values that are relevant.
  - Group and aggregate those values to create the insight you need.
  - Visualize the result so that you can understand what your data is telling you.
- There are three ways to ask questions: simple, custom, and native queries.

![image](https://user-images.githubusercontent.com/63345263/132398574-4430d1c6-e88c-4913-8690-d9aaf5c00244.png)


## Simple and Custom Questions

- Can be done using GUI

### Simple Questions

- Most basic functionality
- Quick questions directly from Query Builder, Basically *Pick some data, view it, and easily filter, summarize, and visualize it.*
- You pick a metric on which you want to summarise data, and then group over a set of data, and then render the answer.
- For Example - Finding the average rating of the product, average rating of product across categories

#### Steps involved
 - Always involves some **filtering and/or summarising**
 - Filtering - Narrowing down basis some criteria (eg. What category of school?, Elementary or Higher Grades)
      - Just click the Filter button in the top-right of the screen to open the filter sidebar. You’ll see a list of all of the columns in this table, as well as columns from tables that are related to
        the one you’re looking at. Depending on the column you pick, you’ll see slightly different options for your filter. 
  - Summarising - Summarising across a set of metrics (Count, Sum, Average, Deviation)
      - To do this in Metabase, click the Summarize button in the top-right of the screen, and the summary sidebar will open up.
       ![image](https://user-images.githubusercontent.com/63345263/132442005-116245e0-4310-4818-a50d-ff7fc90523ea.png)
      - **Picking Metrics** - The sidebar has two main parts: the top is where you pick the number (“metric”) you want to see, and the part below it is where you pick how to group that number 
                             (or how to “break it out”).
      - You can change this to Count, Average, Distinct values, subtotal
      - **Grouping your metrics** - For example if you want to get average rating for a product category wise, then you will group the average metric under product category.                  
      - When you click on a different grouping column than the one you currently have selected, the grouping will switch to use that column instead. But if you want to add an additional grouping, just click the plus (+) icon on the right side of the column. To remove a grouping, click on the X icon
      - Once you’re done setting your metrics and groupings, click Done to close the Summarize sidebar and see your results in all their glory.
      - In the next step, we will see how to change and generate different visualisations
    
- To Do - 1. Create a Question to show number of products under price $20?
          2. Create a question to show number of products category wise with total price under $20?

### Custom Question

- A question composed using the notebook editor. **Sophisticated version of Simple Question**
  ![image](https://user-images.githubusercontent.com/63345263/132442893-ec016f7b-967f-4f51-904e-033a86c7ee8e.png)
- You can add **custom expressions**, to add basic SQL Functionalities like joining tables, create custom columns, filter and group results, compare time series etc
- Refer this [link](https://www.metabase.com/learn/questions/custom-expressions.html) for more clarity on Custom Questions
- For example - If I want to cappture state wise how many purchases were made, then I will use a custom question
- Checking examples on
   - Custom Column
   - Table Operations (Refer this [link](https://www.geeksforgeeks.org/sql-join-set-1-inner-left-right-and-full-joins/) for refresher on SQL JOIN Operations) [Using JOIN in Metabase](https://www.metabase.com/learn/questions/joins-in-metabase.html)
   - Custom Filters
- Refer this [link](https://www.metabase.com/docs/latest/users-guide/expressions.html) on more clarity on using expressions in notebook editor

### SQL Native Queries

- Sometimes for a complex metric, the custom question may not cater to the requirements, hence in that scenario, Metabase provides native Query Editor to compose questions in SQL

# Visualising Results

## Type of Visualisations

In Metabase, an answer to a question can be visualized in a number of ways:
- Numbers
- Trend
- Progress bar
- Gauge
- Table
- Pivot table
- Line chart
- Bar chart
- Combo chart
- Waterfall chart
- Row chart
- Area chart
- Scatterplot or bubble chart
- Pie/donut chart
- Funnel
- Map

Refer this [link](https://www.metabase.com/docs/latest/users-guide/05-visualizing-results.html) on detailed description of these visualisations. In the scope of the document, we will discuss the most commonly used visualisations used
under the scope of our engagements

## Which visualisation should I use?

**PRIORITY-1 ---- Let Metabase pick the chart for you***

### Case by case discussion 

- **Scenario - 1** Too much data (disparate data bound by a common fields) under one window - **Use Table**
- **Scenario - 2** Provide a downloadable and reviewable visualisation to stakeholder - **Use Table**
  ![image](https://user-images.githubusercontent.com/63345263/132446733-792292d3-0e34-4437-98ba-9f4ed588c2fa.png)
- **Scenario - 3** Data as a time series to see how a particular measure changes over time (like a rolling 7-day average)  - **Use Line Graph**
- ![image](https://user-images.githubusercontent.com/63345263/132446768-30e668d4-0952-42b7-a69e-51b752429a1b.png)
- **Scenario - 3** When you only have one value, a representative value - **Use Number**
  ![image](https://user-images.githubusercontent.com/63345263/132446827-2251791b-16c8-43de-abc5-2d1cefc88c0d.png)
- **Scenario - 4** Show a change in a representative value to stress on the growth or fall - **Use Trend**
  ![image](https://user-images.githubusercontent.com/63345263/132446854-b89ecf76-a30f-4910-ab52-c4c5c944535b.png)
- **Scenario - 5** If you want to see a metric in the context of a goal, or limit, or other threshold - **Use Progress Bar**
  ![image](https://user-images.githubusercontent.com/63345263/132446900-dbdd5d1d-622a-462b-8393-829078b5de1e.png)
- **Scenario - 6** Compare groups of data with just a glance - **Use Bar Chart**
  ![image](https://user-images.githubusercontent.com/63345263/132447073-9c9b146c-3312-494d-92a2-623aa4623e70.png)
- **Scenario - 7** Multiple measures with different scales at one place - **Use Combo Chart**
  ![image](https://user-images.githubusercontent.com/63345263/132447232-1c9a5016-e652-4aa3-8a48-5062a84e3438.png)
- **Scenario - 8** Rendering Breakouts/Comparison - **Use Pie/Donut Charts**
  ![image](https://user-images.githubusercontent.com/63345263/132447310-ea7478ff-60f8-4186-b246-39cca72d9cff.png)
- **Scenario - 9** Categorical Breakout across time or differnet groups - **Use Stacked Charts**
  ![image](https://user-images.githubusercontent.com/63345263/132447428-16542ba2-6450-4e4f-8416-c18fd49d1700.png)
- **Scenario - 10** Data with geographical dimeansions/comparing different regions across set of parameters - **Use Map based Visualisations**

## Deep Dive into Visualisations

1. Tables
2. Bar Charts and Staccked Charts
3. Line Graph
4. Pie Chart
6. Map Based Visualisations

### Tables

- Natural organisation of data with with their columns and rows corresponding to the fields and records of relational databases.
- **May not be as “visual” as a bar chart or a map, but they’re often what you need when you’re working with a lot of fields
- Metabase provides some automatic features and some customisable features for tables
- Tutorial
   - We’ll work with the Orders table in the Sample Dataset included with Metabase 
   - Click on Ask Question, then select Orders table from the Sample Dataset
   - The table with its contents will be displayed on the screen as below
     ![image](https://user-images.githubusercontent.com/63345263/132466528-9b4ab511-b3ff-49a1-a8e8-7f367b8e5154.png)
   - Column Actions - Different options for the columns basis type of data. Click on heading of **Created At** column, you will see options like Ordering, Distribution of dates, distinct filtering, similarly for **Total** column Metabase will present a set of options, like Distribution, Sum, Average etc.
   - You can change settings for each of the columns by either clicking on a column’s heading and selecting the gears icon, or via the Settings sidebar. Metabase will include additional columns from other tables linked via foreign key.
   - You can enable **conditional formatting** by highlighting  cells or rows based on the values they contain, which makes it easier for people to see value ranges and outliers. There are two types of conditional formatting: single color and color range. When you want to color a cell or row if a value in cell meets a certain criteria, use the single color option.
   ![image](https://user-images.githubusercontent.com/63345263/132468741-0de094aa-6cf7-4d91-9aa0-c9808428ebde.png)
   - If instead you want to show the value’s relative position in the range of values for a column (or multiple columns), use the color range option (it’s a subtler version of the mini bar chart).
![image](https://user-images.githubusercontent.com/63345263/132468878-4772fee6-ccd8-49e2-a9cc-b79cc818803e.png)
   - You can control visibility of the columns
   - You can create custom columns using the Notebook Editor. Let’s say you want to include a column that lists the unit price of the product ordered, which we’d calculate by dividing the Subtotal by the Quantity orders. Open up the Notebook Editor, and select the Custom Column option. Enter the calculation in the Field Formula input box, and then give it a name.
![image](https://user-images.githubusercontent.com/63345263/132468969-d8bbbc4b-f458-452d-b95d-a42a26f09ff4.png)


**EXERCISE** - Show Product Category wise revenues at Month Level for 2016.

### Line Charts

- Primary categories used are - time series, trend lines, alerts
- Used for plotting data captured in a sequence, whether that sequence is the passage of time, or steps in a process or flow
- Used to plot a time series (also known as a run chart): a set of markers connected by lines, with the x axis showing the passage of time and the y axis plotting the value of a metric at each moment.
- Steps Involved:
  - From the main navigation bar, click on Ask a Question, select Simple Question, pick the database, and select the relevant table.
  - Click on the Visualization button in the bottom right to bring up the Visualization sidebar.
   ![image](https://user-images.githubusercontent.com/63345263/132471727-1c341310-1635-48fe-b327-e03cd6ad2145.png)
  - To create a line chart, you’ll need to pick a metric for Metabase to plot over time. For example, you could show order totals over time by setting the x axis to created_at and the y axis to total. Metabase will automatically plot the line chart
  - It is very important to pick aggregation unit for line charts, like for a span of 3000 days, you cannot plot the data at time interval of minutes. To do so, Click on the green Summarize button to pull up the Summarize sidebar, then group the relevant metrics at any unit of time, category etc.
- Customising the plot
  - **Display Tab** - Lets you change the line color and style, handle missing values
  - **Trend lines and goal lines** - For time series, toggle the trend line option and Metabase will auto-calculate a trend line. You can also add a goal line by specifying a value and a label.
  ![image](https://user-images.githubusercontent.com/63345263/132472992-cad8ca83-9901-46e7-adbd-155e242725c2.png) 
  - **Axes tab** :- You can adjust the scale of the x and y axes. For the x axis, you can select either time series or ordinal scales. Time series will limit the number of values displayed, whereas the ordinal scale will list each value in the series along the x axis. Use an ordinal scale if you’re plotting steps in a sequence.

**General Tip - Show a trend with the line chart, for better readability**

**EXERCISE** - Plot the trends in sale of Gizmo products across Quarters

### Bar Chart

- With bar charts you can compare groups of data with just a glance. 
- One axis specifies the groups, while the other will quantify their count. 
- The goal is to show big differences between the groups, such as which price points customers buy more of and which media platforms lead new customers to you.
- **Creating a Bar Chart**
  - Follow along with our bar chart walkthrough using Metabase’s Sample Dataset. 
  - Select Ask a Question in the nav bar and create a simple question using the Sample Dataset and its Orders table.
  - Select the green Summarize button in the upper right corner. 
  - Scroll down the Summarize sidebar and select the Category column of the Product table.
 - **Bar Chart Settings**
   - Click on the Settings button at the bottom left of the graph to alter the graph and achieve your desired aesthetic.
   - Setting available are - Data, Display, Axes, Labels, Drill-throughs
   - Use the display option to enable stacking of bars, which helps to display multiple categories inside of a small grouping.
     ![image](https://user-images.githubusercontent.com/63345263/132474073-fccb7330-ab32-4625-8739-5077397ec6f9.png)
   - You can add a goal line that specifies where you want numbers to be and Metabase can alert you when the graph raises or drops to that goal. 
    ![image](https://user-images.githubusercontent.com/63345263/132474098-f80c0134-28ef-4975-960d-26b084235fa0.png)
   - Toggling on Show values places the count value above each column. 
   - Clicking the color swatch at the bottom of the sidebar will open a color palette.
   - Selecting a color from the palette will change the color of the chart visualization and selecting one of the three display options will change the visualization
   - **Labels** - Use the toggles if you don’t want certain axis labels or use the text boxes to enter the desired label for each axis.

### Pie Chart
- A bar chart can be further extended to show a Piechart visualisation 
- Change the visualisation under the Visualisation settings to convert a bar chart to a Pie chart

### Map Visualisation

Metabase features three map types:
- Pin maps mark specific locations.
- Region maps group data by country or state.
- Grid maps distribute a large number of points over a specified area.

We will focus on the Region maps. Grouping people by region can be a great way to detect patterns in your user base. 

#### Adding Map to Metabase

1. To configure this visualisation, you need to have added a map for the corresponding region to the metabase isntance
2. Go to Admin Tab. Go to Maps section. You need to have a correct .geojson file for the districts or blocks  to enable functionality. Reference Maps - [HP MAP](https://raw.githubusercontent.com/umangbholasamagra/Geo-JSON-Files/main/hp.geojson), [UP MAP](https://raw.githubusercontent.com/umangbholasamagra/Geo-JSON-Files/main/group.geojson)
3. Click on **Add Map** option. Add name for the map, how would want to refer it. Then add link for the geojson file of map. Click on load button, Success message should come
4. Select Identifier, identifier refers to the common name which exists in your tables vis-a-vis map
5. Select display name, the name how you would want the list to be shown when visualisation is rendered.
6. Click on Add Map

**Example**
- Follow along with our bar chart walkthrough using Metabase’s Sample Dataset. 
- Select Ask a Question in the nav bar and create a simple question using the Sample Dataset and its Orders table.
- Select the green Summarize button in the upper right corner. 
- Scroll down the Summarize sidebar and select the State column of the User table. By default map visualisation will be selected.
 
 **Region maps require your data to have columns with the (correctly formatted) field type State or Country.**

# Buidling Dashboard

## What is a dashboard?

- Dashboards group questions and present them on a single page. 
- You can think of dashboards as shareable reports that feature a set of related questions. 
- You can set up subscriptions to dashboards via email or Slack to receive the exported results of the dashboard’s questions.
- A dashboard comprises a set of cards arranged on a grid. These cards can be questions - such as tables, charts, or maps - or they can be text boxes.
- You can add filter widgets to dashboards that filter data identically across multiple questions, and customize what happens when people click on a chart or a table.

## How to create a dashboard

- In the top right of the screen, click the + icon to open the Create menu.
- Select New Dashboard. Give your new dashboard a name and a description
- Choose which collection the dashboard should go in, then click Create, and Metabase will take you to your new dashboard.
![image](https://user-images.githubusercontent.com/63345263/132477648-1fd08335-010f-4f7f-9bc4-37ed6541c373.png)
- If you don’t want to build a dashboard from scratch, or want to experiment by making changes to an existing dashboard without affecting the original, you can duplicate an existing dashboard. 
- From an existing dashboard, click on the … menu in the upper right, and select Duplicate.

## Adding saved questions to a dashboard

There are two ways to add questions to a dashboard: from the dashboard, or from the question you want to add.

**From a question:** 
-You can add a newly saved question to a dashboard directly from the window that pops up after you save the question for the first time. 
You can also add a question to a dashboard by clicking on the pencil icon next to the name of the question, and selecting Add to dashboard.

**From a dashboard:** 
- Click on the pencil icon to edit the dashboard. 
- Then click the + icon in the top right of the dashboard editing interface (not the + in the main navigation bar) to add any of your saved questions to the dashboard, regardless of which collection the questions are in.

Once you add a question to your dashboard, it’ll look something like this:

![image](https://user-images.githubusercontent.com/63345263/132477975-6b2d2a87-329e-4a1e-b87b-1c96539dc790.png)

## Adding headings or descriptions with text cards

- Text cards allow you to include descriptions, explanations, notes, or even images and GIFs to your dashboards. 
- You can also use text cards to create separations between sections of charts in your dashboards, or include links to other dashboards, questions, or websites.
- To add a new text card, create a new dashboard (or edit an existing one) and click on the text card button, Aa, in the top-right:
- You can use Markdown to format the text in your text card, create inline tables or code snippets, or even embed linked images (easy on the GIFs, friends). Use this [link](https://www.markdownguide.org/basic-syntax/) to refer markdown tags
![image](https://user-images.githubusercontent.com/63345263/132478933-beed277c-2ea5-4fda-b911-a8d6f50235da.png)

![image](https://user-images.githubusercontent.com/63345263/132478960-e4a8b4d5-7187-4dd6-8b21-0fcd6c693931.png)

## Arranging cards

- Each question on a dashboard is in its own card that you can move around or resize as you see fit. 
- Just click the pencil icon in the top right of a dashboard to enter the dashboard’s editing interface.
- Once you’re in edit mode, you’ll see a grid appear. 
- You can move and resize the cards in the dashboard to your liking and they’ll snap to the grid.
- **To move a card,** just click and drag the card. Other cards will move out of the way.
- **To resize a card**, click the handle at the bottom right corner of the card, and drag to resize. Nearby cards will move away to accommodate the new size.
- **To remove a card**, hover over the card, and click the X icon in the top right corner.

Metabase will automatically update a question’s display to make sure your data looks great at any size you choose.

## Dashboard Filters

### Adding a new filter

To add a filter to a dashboard, first click the pencil icon to enter dashboard editing mode, then click the Add a Filter button that appears in the top-right.

You can choose from a number of filter types:

- Time
- Location
- ID
- Other Categories

The type of filter you choose will determine what the filter widget will look like, as well as which fields you’ll be able to filter your cards by:

#### Time filters

When picking a Time filter, Metabase will prompt you to pick a specific type of filter widget:

- Month and Year
- Quarter and Year
- Single Date
- Date Range
- Relative Date
- All Options
- Single Date and Date Range will provide a calendar widget, while the other options all provide slightly different dropdown interfaces for picking values. To get a widget that’s just like the time filter in the graphical query builder, choose All options.

#### Location filters

There are four types of Location filters to choose from:
- City
- State
- ZIP or Postal Code
- Country
- ID filterhttps://www.metabase.com/learn/dashboards/linking-filters.html

The ID filter provides a simple input box where you can type the ID of a user, order, etc.

##### Other Categories

The Other Categories filter is a flexible filter type that will let you create either a dropdown menu or an input box to filter on any category field in your cards.

Note: If you’re trying to filter Native/SQL questions, you’ll need to add a bit of additional markup to your query in order to use a dashboard filter with that question. For an in-depth article on this, check out Adding filters to dashboards with SQL questions.


### Linking filters

You might need to link the filters to one other, cascading them. Use this [link](https://www.metabase.com/learn/dashboards/linking-filters.html)


## Sharing Dashboard

If your Metabase administrator has enabled public sharing on a saved question or dashboard, you can go to that question or dashboard and click on the sharing icon to find its public links.
 
![image](https://user-images.githubusercontent.com/63345263/132487136-b9af8efd-b2f4-4c81-a765-41e8d5004e6a.png)


Public links can be viewed by anyone, even if they don’t have access to Metabase.

# Managing Dashboard

## Making dashboard faster

When it comes to dashboard performance, there are essentially four ways to get dashboards to load faster:

- Ask for less data.
- Cache answers to questions.
- Organize data to anticipate common questions.
- Ask efficient questions.

### Enabling Caching

- You don’t need to wait for data if it’s already loaded.
- Admins can set up Metabase to cache query results, which will store answers to questions.
- If you have a set of dashboard that everyone runs when they open up their computers first thing in the morning, run that dashboard ahead of time, and the questions in that dashboard will use the saved results for subsequent runs to load in seconds.
- People will have the option to refresh the data, but typically this is unnecessary, as most often people will only need to review data from the previous day and before.

![image](https://user-images.githubusercontent.com/63345263/132487524-aca91884-42b2-4597-8e9c-6406f72ccc2b.png)

- You can configure caching in the Settings tab of the Admin Panel. 
- These settings allow you to configure the minimum query duration to cache (so you only cache long-running queries), the Cache Time-to-live (TTL) Multiplier (to specify how long the cache should stick around), and the Max Cache Entry Size (so you can set an upper limit on the amount of data you cache).


### Organize data to anticipate common questions
The next best thing you can do is organize your data in such a way that it anticipates the questions that will be asked, which will make it easier for your database to retrieve that data.

- Index frequently queried columns.
- Denormalize data.
- Materialize views: create new tables to store query results

**Denormalization is a strategy used on a previously-normalized database to increase performance. In computing, denormalization is the process of trying to improve the read performance of a database, at the expense of losing some write performance, by adding redundant copies of data or by grouping data.**

### Materialised Views

With materialized views, you’ll keep your raw, denormalized data in their tables, and create new tables (typically during off hours) to store query results that combine data from multiple tables in a way that anticipates the questions analysts will ask.

Refer this [link](https://www.complexsql.com/materialized-view/) on how to create Materialised Views and use them.
