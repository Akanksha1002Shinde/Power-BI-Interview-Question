# Power-BI-Interview-Question

Power Query
What is Query Folding?
Query Folding refers to the ability of Power Query to push transformations back to the data source, improving performance by reducing the amount of data transferred.

What is M Language?
M is the formula language used in Power Query for data transformation. It’s case-sensitive and functional.

Append vs Merge?
Append combines rows (like UNION in SQL), while Merge joins tables based on keys (like JOIN).

What is a Parameter?
A parameter is a dynamic input used to make queries more flexible, like filtering based on user inputs.

How many tables can be appended or merged?
Multiple tables can be appended. For merging, it is usually done two at a time, but can be chained.

Storage Engine?
Power Query uses the Mashup Engine.

Custom Functions Example?
Yes, I’ve created a custom function to convert time zones dynamically based on parameters.

Handling Credentials?
I configure privacy levels and use organizational-level credentials, stored securely in Power BI service.

Custom Column or Conditional Logic?
Yes, I’ve used “if-then-else” statements to create columns for risk levels based on score thresholds.

Data Type Conversion Techniques?
I ensure consistent data types using the “Change Type” step and perform checks with “Table.Profile”.

CALCULATETABLE vs FILTER?
FILTER returns a table based on conditions; CALCULATETABLE modifies the filter context while returning a table.

🔹 Data Modelling
Fact vs Dimension Tables?
Fact tables hold measurable data; dimension tables hold descriptive data (e.g., Date, Product).

Calculated Column vs Measure?
Use columns for row-level data, measures for aggregated results. Measures are preferred for performance.

Rules for Table Relationships?
There should be a unique key on one side, matching data types, and no circular references.

What is a Data Model?
It’s a logical structure that defines relationships among tables for efficient querying and analysis.

Performance: Calculated Column vs Measure?
Measures give better performance as they are calculated on the fly and not stored.

Clustered vs Non-Clustered Index?
Clustered index sorts physical data; non-clustered creates a separate lookup index.

Scalability Factors?
Minimize relationships, use star schema, reduce columns, avoid bi-directional filters.

Advanced Techniques?
Yes, I’ve used role-playing dimensions for multiple date columns and bridge tables for many-to-many relationships.

SCD Handling?
By creating a versioning system or using Type 2 slowly changing dimensions with historical tracking.

Calculated Tables?
Used when derived tables are needed, like generating a summary table for top N analysis.

Complex Relationships/Hierarchies?
I create hierarchy fields and use bridge tables when many-to-many relationships are involved.

Handling Large Datasets?
Use aggregations, reduce cardinality, optimize relationships, and use import mode when possible.

🔹 Report View
What are Filters?
Filters limit data shown in visuals (Visual, Page, Report level).

Dataset vs Report vs Dashboard?
Dataset is the data model; Report is the visual presentation; Dashboard is a pinboard in Power BI Service.

Cross Filtering?
When selecting a data point in one visual filters data in another.

Report vs Dashboard?
Report is multi-page, created in Desktop; Dashboard is a single page, created in Service.

Make Report Dynamic?
Use parameters, slicers, bookmarks, and dynamic measures.

Custom Visuals Example?
Yes, I’ve used “Bullet Chart” from AppSource to show KPIs.

Filters in Project?
Used page-level slicers for region and visual-level filters for product categories.

Bookmarks?
Yes, used to toggle between different views or states of visuals.

Conditional Formatting?
Yes, based on thresholds for coloring KPIs.

Edit Interactions?
Allows control over how visuals interact when one is filtered.

Edit Interaction in Visuals?
You can make visuals filter, highlight, or ignore interactions.

Calculated Column vs Measure?
Columns are row-based and stored; measures are dynamic and optimized.

When to Use Filter vs Slicer?
Use slicers for end-user filtering and filters for internal logic or restrictions.

🔹 Power BI Service
What is Power BI Service?
A cloud platform to share, schedule, and collaborate on reports.

Licenses in Power BI?
Free, Pro, Premium Per User (PPU), and Premium Capacity.

License Used?
Pro license for report publishing and sharing.

Embedding Options?
Yes, using Power BI Embedded and REST APIs.

RLS?
Row-Level Security restricts data at user level using DAX filters.

🔹 Connectivity
Data Sources?
SQL Server, Excel, Web API, SharePoint, Salesforce, etc.

Import vs DirectQuery?
Import is faster, stores data in-memory; DirectQuery queries source on demand.

Connectivity Modes?
Import, DirectQuery, Live Connection, Composite.

Sources Used?
SQL Server, Excel, and SharePoint.

Source Database?
SQL Server or Oracle, depending on project.

Gateway?
Used to connect on-premise data to the cloud; types: Personal and Standard.

Alerts?
Set on dashboards using card tiles for KPIs.

Microsoft Fabric?
An integrated analytics platform combining Power BI, Synapse, and Data Factory.

Testing Visuals from Source?
Cross-check results with backend SQL query or Excel data.

🔹 DAX
What is DAX?
Data Analysis Expressions – formula language for Power BI, Power Pivot, etc.

CALCULATE?
Modifies filter context to evaluate an expression.

SUM() vs SUMX()?
SUM works on column; SUMX is row context + expression.

DISTINCT() vs VALUES()?
DISTINCT returns unique values; VALUES returns unique + blank (useful for relationships).

Basic DAX Functions?
SUM, COUNT, AVERAGE, CALCULATE, IF, SWITCH, RELATED, FILTER.

FILTER Function Use?
Used to return a table that meets a condition.

GROUP BY in DAX?
SUMMARIZE, GROUPBY used to create grouped tables.

Using Variables in DAX?
Improve readability, performance, and prevent repeated calculations.

Bi-Directional Cross Filtering?
Allows filters to flow in both directions – useful but can degrade performance.

CALCULATE vs CALCULATETABLE?
CALCULATE returns a value, CALCULATETABLE returns a table.

ALL vs ALL EXCEPT?
ALL removes all filters; ALL EXCEPT removes all except selected columns.

TOTALYTD?
Calculates year-to-date total.

Previous Year YTD?
Use: TOTALYTD([Sales], Dates[Date], SAMEPERIODLASTYEAR(Dates[Date]))

LOOKUP Function?
Use LOOKUPVALUE to fetch value from another table based on match.

SUMMARIZE vs SUMMARIZECOLUMNS?
SUMMARIZECOLUMNS is preferred; better performance and syntax.

 Scenario-Based – DAX
Sales for April – DAX Expression:
Use:
DAX
Copy
Edit
CALCULATE(SUM(Sales[Amount]), MONTH(Sales[Date]) = 4)
Or using MONTH filtering from Date table:
DAX
Copy
Edit
CALCULATE([Total Sales], 'Date'[MonthName] = "April")
DATEADD vs PARALLELPERIOD – Case Example:
DATEADD shifts date context with full support for time intelligence, and respects filters.
PARALLELPERIOD simply shifts a fixed number of periods, not filter-aware.
In my project, I used DATEADD() to compare current month sales with the previous month to show trend analysis, while I used PARALLELPERIOD() for fiscal YTD comparison.

🔹 Scenario-Based – Report View
Slicer affects only 2 visuals out of 5:
Use “Edit Interactions” in Power BI Desktop – click on slicer > Format tab > Edit Interactions > Turn off filter icon for the 3 visuals that should not be affected
Top 10 Regions by Volume in Donut Chart:
Apply Top N filter in the visual-level filter pane: choose “Top 10” by volume column.
No bar chart in Rolling 24 months visual:
Use Line Chart or Area Chart for smoother time-series representation.
Country-wise Sales in Percentage:
DAX
Copy
Edit
CountryWise% = DIVIDE(SUM(Sales[Amount]), CALCULATE(SUM(Sales[Amount]), ALL(Sales[Country])))
Bring two visuals from Page 1 into a Tile in Page 2:
Use Bookmarks or create report page tooltip and display it as a tile usng an image or shape with an action link.
Navigate back to Home Page from other pages:
Use “Buttons” with “Page Navigation” action or create a “Home” bookmark.
Show detailed information dynamically:
Use Drillthrough pages or Tooltip pages to show more data upon clicking.
Visuals not loading (in your project):
I checked DAX queries, reduced visual count, optimized measures, checked for heavy relationships, and used Performance Analyzer to debug the bottlenecks.
If you remove filter from a measure, will data in card be same?
No, removing filters changes the context, so data in the card will change.

🔹 Scenario-Based – Performance & Optimization
Visuals loading slowly – how to improve?
Reduce number of visuals per page
Use measures instead of calculated columns
Optimize DAX (avoid iterator functions where possible)
Remove unused columns/tables
Enable “Performance Analyzer” to identify slow visuals
Use aggregations or pre-aggregated tables if possible
Slicer on Page 1 affects Page 2:
Use Sync Slicers feature from the View tab, then select pages to sync across.
Can Qty × Unit Price (calculated column) and SUM(Sales) (measure) be combined?
Yes, with SUMX:
DAX
Copy
Edit
Total Sales = SUMX(Sales, Sales[Qty] * Sales[Unit Price])

🔹 Scenario-Based – Power BI Services
Before Schedule Refresh – SQL Server Steps:
Ensure the gateway is running, credentials are updated, and the query doesn’t return errors in Power BI Desktop. Also check for nulls and data source connectivity.
Country-wise Sales in Percent (repeat of earlier):
Use DIVIDE with ALL function to calculate percent contribution.
% of Sales per City:
DAX
Copy
Edit
CityWise% = DIVIDE(SUM(Sales[Amount]), CALCULATE(SUM(Sales[Amount]), ALL(Sales)))
Many-to-Many Relationship – How handled?
Used a bridge table to break the many-to-many. Set relationship to single-direction to avoid ambiguity.

🔹 Scenario-Based – Connectivity & Stakeholder Management
Import vs Direct Query – Difference:
Import is faster as it caches data in memory. DirectQuery fetches data live from the source with each interaction – real-time but slower. I recommend Import for small/medium datasets for better performance.
Stakeholder Requests Major Change in Data Relationships:
I first evaluate the impact on existing models, create a backup, then redesign the model, revalidate DAX, and update visuals. I also explain trade-offs in performance and complexity.
Stakeholder prefers Direct Query – convince for Import:
I’ll explain that Import mode provides faster performance, supports complex DAX, offline access, and lower load on source DB. Direct Query is best only when near real-time data is essential. I can show a performance comparison dashboard.

Extra question 
 Q2: Can you list the various components that make up Power BI?
The components include:
Power BI Desktop
Power BI Service
Power BI Data Sources
Power Query
Power Pivot
Power Maps
Power Gateway
Power BI Report Server
Power BI Embedded
Power Q&A
Power View

🔹 Q3: What is a visual, dashboard, and report in Power BI?
Visual: A graphical representation of data (chart, table, etc.)
Dashboard: A one-page summary combining mutiple visuals
Report: A multi-page set of visuals to explore and analyze data

🔹 Q4: What kind of data can you store in Power BI?
Fact tables: Quantitative data for analysis
Dimension tables: Descriptive attributes for fact tables

🔹 Q5: What are the disadvantages of using Power BI?
Cannot parameterize dashboards for different users/accounts
Sharing is limited to same-domain users without Premium

🔹 Q6: How can you import data into Power BI?
You can import from Excel, CSV, databases, web APIs, SharePoint, etc.

🔹 Q7: What types of data sources are supported in Power BI?
Cloud services
On-premises sources
Flat files (Excel, CSV)
APIs and web-based sources

🔹 Q8: Difference between Direct Query and Import mode?
Direct Query: Live connection, real-time, slower
Import: Data loaded into memory, faster performance

🔹 Q9: What is DAX in Power BI?
DAX (Data Analysis Expressions) is a formula language used to build calculations and measures in Power BI.

🔹 Q10: What is a measure in Power BI? How is it different from a calculated column?
Measure: Calculated at query time, dynamic
Calculated Column: Stored in the model, evaluated during data load

🔹 Q11: Why do we use the Selection Pane in Power BI?
To control visibility of visuals and organize multiple elements by grouping.

🔹 Q12: What are data alerts in Power BI?
Alerts notify users when data crosses a predefined threshold in a KPI card.

🔹 Q13: Difference between a slicer and a filter in Power BI?
Filter: Restricts data behind the scenes
Slicer: User-facing visual to select data interactively

🔹 Q14: Steps to create a hierarchy in Power BI?
Select fields, right-click, and choose “Create Hierarchy” to build drillable levels.

🔹 Q15: What is a Drill-through?
Allows navigating from summary to detailed data on a separate page.

🔹 Q16: How to create a Calculated Table in Power BI?
Go to Modeling → New Table → Write a DAX expression.

🔹 Q17: What is a join in Power BI?
Combining tables based on keys. Types: inner, left, right, full outer joins.

🔹 Q18: What is a Data Model in Power BI?
Defines relationships and structure of data for efficient analysis and report building.

🔹 Q19: How do you create relationships between tables in Power BI?
Use “Manage Relationships” to link tables via primary/foreign keys.

🔹 Q20: How to create a bookmark in Power BI?
View → Bookmarks → Add → Save the current visual state.

🔹 Q21: Can you join two different data sources in a single dashboard?
Yes, using Power Query to connect and relate them in the model.

🔹 Q22: Can we create multiple dynamic relationships between tables?
No, only one active relationship at a time. Others can be inactive and used with USERELATIONSHIP() in DAX.

🔹 Q23: How to hide/unhide a report?
Use the Selection Pane or set page visibility properties.

🔹 Q24: How to buy Power BI suite?
From the official Power BI website, choose Pro or Premium licenses.

🔹 Q25: Common Data-Shaping Techniques?
Removing columns, renaming, splitting, merging, and changing data types.

🔹 Q26: Working of Power BI in 3 stages?
Data Integration
Data Processing
Data Visualization

🔹 Q27: Applications of Power BI?
Business analysis, marketing campaigns, data cleaning, sales tracking, and real-time analytics.

🔹 Q28: How to reshape data in Power BI?
Use Power Query Editor to transform rows and columns.

Q29: How can you optimize the performance of a Power BI report?
Reduce number of visuals
Use Import mode over DirectQuery
Minimize calculated columns
Use filters and aggregations
Use star schema for modeling

🔹 Q30: How can you handle errors in Power BI?
Use Power Query’s error-handling step
Use DAX functions like IFERROR(), ISERROR()
Validate data using “View as Role” and testing filters

🔹 Q31: What are the types of filters in Power BI?
Visual-level
Page-level
Report-level
Drill-through filter

🔹 Q32: What is a KPI in Power BI?
A KPI (Key Performance Indicator) visual shows a value, its target, and status (e.g., up/down vs. target).

🔹 Q33: Power BI Desktop vs Power BI Service?
Desktop: Used for development
Service: Used for sharing, collaboration, and publishing

🔹 Q34: How to publish a Power BI report to the web?
Use “Publish to Web” under File → Generate an embed code → Share on blog/website.

🔹 Q35: What are tiles in Power BI?
Visual snapshots pinned to a dashboard from reports, Excel, SSRS, or Q&A box.

🔹 Q36: How to create a slicer in Power BI?
Choose the slicer visual → Drag a field onto it → Customize for date, category, etc.

🔹 Q37: What is the purpose of drill-through?
To analyze detailed data related to a particular data point in another report page.

🔹 Q38: Pie chart vs Donut chart in Power BI?
Donut has a center hole for more info/text; otherwise, both show part-to-whole.

🔹 Q39: Where is Power BI data stored?
Azure Blob Storage: User-uploaded data
Azure SQL Database: Metadata and system artifacts

🔹 Q40: What are Content Packs?
Bundles of dashboards, datasets, and reports.
Types:
Service Content Packs
Organizational/User Content Packs

🔹 Q41: What is Power Pivot?
An Excel add-in for modeling large data, creating relationships, and writing DAX formulas.

🔹 Q42: Types of Custom Visuals in Power BI?
Marketplace visuals
Developer visuals using SDK
Organizational visuals for internal use

🔹 Q43: What is Self-Service BI?
Empowers business users to build reports and dashboards without IT dependency.
Components: Excel BI Toolkit, Power BI

🔹 Q44: How are relationships defined in Power BI Desktop?
Automatically detected
Manually via “Manage Relationships”
Must match key columns

🔹 Q45: What is Bi-Directional Cross Filtering?
Filters flow both ways between related tables — useful for complex models but can slow performance.

🔹 Q46: What is Grouping in Power BI?
Combining items in visuals into categories. Use Ctrl + click → Right-click → “Group”.

🔹 Q47: What is Query Folding?
When Power Query pushes transformations back to the source DB for efficient execution.

🔹 Q48: What is the Advanced Editor?
Lets you view/edit M code of the query steps manually. Accessed via: Home → Edit Queries → Advanced Editor.

🔹 Q49: How do you create a custom visual in Power BI?
Use Power BI Developer Tools
Install Node.js and Power BI CLI
Create visual project with CLI
Develop visuals using TypeScript and D3.js
Test, build, and package for Power BI

🔹 Q50: Steps to set up Row-Level Security (RLS) in Power BI?
Go to Modeling > Manage Roles
Define roles and DAX filters (e.g., [Region] = "West" )
Assign users to roles in Power BI Service
Use “View As Role” to test

🔹 Q51: What is Power BI Premium and how is it different from Power BI Pro?
Power BI Pro: Individual license with 10 GB/user, shared capacity
Power BI Premium: Dedicated capacity, higher refresh rates, large datasets, paginated reports

🔹 Q52: Difference between Power BI and Excel?
Power BI: Advanced visualization, DAX, cloud publishing
Excel: Spreadsheet-focused, limited visuals, uses VBA
Power BI is more scalable for enterprise BI.

🔹 Q53: Data types used in DAX?
Integer
Decimal
Currency
DateTime
Boolean
Text
Variant
Binary

🔹 Q54: Types of Views in Power BI?
Report View: Build visuals
Data View: Explore table data
Model View: Manage relationships, modeling structure

🔹 Q55: Optimizing performance for large datasets?
Use Import mode
Reduce cardinality
Use aggregations
Partition data
Avoid unnecessary relationships and columns

🔹 Q56: What is a Composite Model in Power BI?
Allows combining Import and DirectQuery data in the same model.

🔹 Q57: How to build a data-driven culture using Power BI?
Identify business KPIs
Build self-service dashboards
Train teams on Power BI
Foster decision-making based on insights

🔹 Q58: What are refresh options in Power BI?
Data/model refresh
Tile refresh
Package refresh (OneDrive sync)
Visual container refresh

🔹 Q59: Connectivity modes in Power BI?
Import: Data is loaded into PBIX file
DirectQuery: Real-time query to source
Live Connection: Connects to Analysis Services (no Power Query)

🔹 Q60: How to assign SSRS with Power BI?
In SSRS portal → click “Power BI” icon → Pin elements to Power BI dashboard.

🔹 Q61: Power BI vs Tableau
Feature	Power BI	Tableau
Language	DAX	MDX
Data Handling	Moderate	Large data volumes
Integration	Strong with Microsoft tools	Broad data source support
Ease of Use	Moderate	Drag-and-drop, user-friendly

🔹 Q62: What is GetData in Power BI?
It allows users to connect to multiple data sources like Excel, SQL, APIs, etc.

🔹 Q63: Key Components of SSAS?
OLAP engine
PivotTables
Slicers
Drilldown capabilities

🔹 Q64: Key consideration when installing Data Gateway?
Number of concurrent users — it affects real-time refresh and query speed.

🔹 Q65: Can a data gateway handle both Import and DirectQuery?
Yes, but it’s recommended to separate them for performance reasons.

🔹 Q66: What is Z-order in Power BI?
Z-order defines the layering of visuals — helps place visuals on top or behind others.

🔹 Q67: Prerequisite for connecting to Azure SQL Database?
Configure firewall to allow IP addresses for remote Power BI access.

Q68: What is DAX, and what is it used for in Power BI?
DAX (Data Analysis Expressions) is a formula language used to define custom calculations and aggregations in Power BI, Power Pivot, and SSAS Tabular models.

🔹 Q69: Categories of functions in DAX?
Logical
Text
Date/Time
Filter
Information
Aggregation

🔹 Q70: Calculated Column vs Measure in DAX?
Calculated Column: Evaluated row by row and stored in the table
Measure: Evaluated on the fly based on filter context

🔹 Q71: DAX formula for Running Total?
DAX
Copy
Edit
RunningTotal = 
CALCULATE(
    SUM(Sales[Amount]),
    FILTER(
        ALL(Sales[Date]),
        Sales[Date] <= MAX(Sales[Date])
    )
)

🔹 Q72: What is SUMX used for?
SUMX() iterates over a table and sums the result of an expression for each row.
Example:
DAX
Copy
Edit
SUMX(Sales, Sales[Qty] * Sales[Price])

🔹 Q73: Purpose of CALCULATE()?
Changes the context of a calculation. It evaluates an expression with modified filters.

🔹 Q74: What is Filter Context?
Filter context defines the subset of data that is considered during calculation based on report filters, slicers, or visuals.

🔹 Q75: What is CALENDARAUTO()?
Creates a continuous date table automatically based on the data in your model.
DAX
Copy
Edit
CALENDARAUTO()

🔹 Q76: What is KEEPFILTERS()?
Used in CALCULATE() to preserve existing filter context when new filters are applied.

🔹 Q77: Three Text Functions in DAX?
CONCATENATE()
REPLACE()
UPPER()

🔹 Q78: Difference between DISTINCT() and VALUES()?
DISTINCT() returns unique values only.
VALUES() returns unique values + blank row (for relationship logic).

🔹 Q79: What are DAX Patterns?
Reusable formula templates and best practices for common business scenarios (e.g., YTD, Top N, Rolling Average).

🔹 Q80: Difference between MAX() and MAXA()?
MAX() works only on numeric values
MAXA() evaluates numbers, text, and logical values (TRUE = 1)

🔹 Q81: Types of Contexts in DAX?
Row Context
Filter Context
Query Context

🔹 Q82: Which context executes first – Filter or Row?
Filter Context executes first and overrides Row Context when used inside CALCULATE().

🔹 Q83: Difference between M and DAX?
M: Used in Power Query for data transformation
DAX: Used in the data model for calculations and aggregations

🔹 Q84: What is a DAX Variable?
Used to simplify complex logic and improve performance/readability.
DAX
Copy
Edit
VAR x = 10  
RETURN x * 2

🔹 Q85: What are Circular Dependencies?
Occurs when two calculations reference each other directly or indirectly, preventing Power BI from evaluating the result.

Q86: How would you design a Power BI dashboard to track sales performance across different regions?
Connect to sales data and clean it using Power Query
Create calculated columns or measures for total sales, growth %, etc.
Use visuals like bar/column charts for region-wise comparison
Add slicers for time period and region
Include KPIs to show targets vs. actuals
Apply conditional formatting and tooltips for deeper insights

🔹 Q87: How would you use Power BI to analyze customer churn rate?
Import customer activity and subscription status
Define churned customers (e.g., inactive for 90 days or canceled plan)
Create a DAX measure for churn rate:
DAX
Copy
Edit
Churn Rate = DIVIDE([Churned Customers], [Total Customers])
Visualize churn trends by month, region, or service type
Use slicers to filter by segments or plans

🔹 Q88: How would you use Power BI to visualize a customer journey?
Import data showing different touchpoints (ads, website, signup, support)
Use custom visuals like Sankey charts or flow diagrams
Show the drop-off rate at each stage
Combine with demographic filters to analyze behavior by age/location
Add tooltips with key metrics at each touchpoint

🔹 Q89: How would you use Power BI to track website traffic and engagement?
Connect to Google Analytics or log data
Use line charts for time trends in page views, bounce rate, and sessions
Create dashboards for top landing pages, device usage, traffic sources
Add cards showing average session duration and conversion rate
Apply filters for date ranges and user types (new vs returning)

🔹 Q90: How would you use Power BI to analyze social media data and sentiment?
Connect to social media APIs or third-party tools (e.g., Brandwatch)
Perform sentiment analysis using Power Query + AI/ML integration
Create dashboards showing mentions, sentiment trends, and top posts
Use pie charts for sentiment distribution and word clouds for keywords
Use slicers to filter by platform (Twitter, Instagram, etc.)

🔹 Q91: How can you use Power BI to analyze real-time data?
Use DirectQuery or streaming datasets via Azure Stream Analytics
Build real-time dashboards with line charts or KPI cards
Use Power BI Service to push data through REST APIs
Set up data alerts for threshold breaches
Ideal for monitoring sensors, stock prices, or user activity

🔹 Q92: How will you optimize data model relationships for better performance in Power BI?
Use single-direction relationships instead of bi-directional
Maintain star schema with dimension and fact tables
Reduce cardinality and remove unnecessary columns
Avoid complex calculated columns and large joins in Power Query
Disable auto-detect relationships

🔹 Q93: How will you use Power BI to handle data from multiple sources?
Use Power Query to connect and clean different data sources
Normalize columns (e.g., date format, currency)
Merge or append datasets
Create relationships in the data model
Validate with source data and use composite models if needed

🔹 Q94: How can you refresh Power BI reports once they are published on the cloud?
Use Personal Gateway or Enterprise Gateway
Set up refresh schedule in Power BI Service
Ensure credentials and privacy levels are configured
Use incremental refresh for large datasets
Monitor refresh status in the Power BI workspace

🔹 Q95: Can you audit and monitor user activity in Power BI?
Yes, using:
Audit Logs in the Microsoft 365 Compliance Center
Usage Metrics for dashboards and reports
Admin Portal to monitor workspace activity
PowerShell scripts for advanced tracking

🔹 Q96: How will you embed Power BI reports in custom applications?
Register your app in Azure
Generate client ID and secret
Use Power BI REST API or JavaScript SDK
Authenticate via token
Embed the report in a web app or portal

🔹 Q97: What are key factors that impact Power BI report performance?
Data volume and refresh frequency
Number of visuals per page
Complex DAX calculations
Data model design (snowflake vs star)
Use of DirectQuery vs Import

🔹 Q98: How does DAX handle data discrepancies and errors?
Data cleaning: Use TRIM(), SUBSTITUTE() to clean text
Error handling: Use IFERROR(), ISERROR(), DIVIDE() for safe math

🔹 Q99: Power BI visuals used for hierarchical data?
Treemap
Sunburst Chart
Decomposition Tree
Hierarchy Slicer
