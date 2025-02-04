# Transactions

Transactions is a project created for monitoring and reviewing financial transactions. Financial transaction data from the Bank of Nova Scotia is obtained from the instituion website. The report compares the different transactions performed to provide meaningfull financial insight such as unknown charges, high value transactions, comparing previous date period data and more.

#### <ins> Report info </ins>

Page 1: General<br/>
Contains a summary of the transactions. Shows the amount spend each year, month, quarter and day. Top debit and credit transactions for the time periods mentioned earlier are listed as Multi-row cards. A KPI visual is added to check if the amount debited is larger than amount credited for the selected time period.

Page 2: Type<br/>
Debit and Credit transactions are visualized according to the amount. Year, month and account type filters are availabe. This page can be help with finding about spend on different types.

Page 3: Location <br/>
Map visual available to locate transactions geographically. Amount spend on each city is available as a pie chart.

Page 4: Detailed report<br/>
This page is used for reviewing transactions in detail. Filters are available for every need to find unusual activity or to compare transactions with a different time period.

#### <ins> Data Sources </ins>
1. Dates - Date table, created using Dataflow Gen 2 in Fabric or Power Query using M language in Power BI Desktop app.
2. Location - Table consisting of Canadian cities and respective data downloaded from https://simplemaps.com/data/canada-cities as CSV file.
  <img src="https://github.com/abychen01/Transactions/blob/35b27ccf73b930a15ab3fb1114fe97ceb187c14a/location%20sample.png" width="900">
3. Newtransactiondata - Table with the latest transaction data.


#### <ins> ETL process </ins>
1. Financial transaction data (fact table data) from the Bank of Nova Scotia is exported manually (API not avaialable at the moment) from the instituion website as CSV files. At the end of each month two CSV files are generated - one for the debit and one for the credit account.
2. A Fabric workspace called Transactions - dev is setup using large semantic model storage format. Data will be stored in the Transactions Lakehouse inside the Transactions - dev workspace.     
  <img src="https://github.com/abychen01/Transactions/blob/812758bb7d752b5d4a24b08d21ac40f2ec6c6114/Transactions%20-%20dev%20workspace.png" width="400">
3. CSV files are uploaded as files to the Monthly Data folder for ETL. Data can be directly uploaded from the Fabric website or using OneLake File Explorer.
  <img src="https://github.com/abychen01/Transactions/blob/35b27ccf73b930a15ab3fb1114fe97ceb187c14a/Monthly%20Data%20folder.png" width="400">
4. Monthly data ETL Notebook is created inside the Transactions - dev workspace for transforming the data as needed for the report. Credit and Debit CSV files are combined and Type columns is created after comparing with different keywords to find out the type of transaction. Sample CSV transaction data is listed below:
<img src="https://github.com/abychen01/Transactions/blob/562994d6ba1182c6d43a77586e1071433cbc4d12/transaction%20sample%20data.png" width="900">
5. Once the transformation is completed, the data is saved to newtransactiondata table inside the Lakehouse and CSV files inside the Monthly Data folder is deleted. Monthtly data ETL Data Pipeline is used to automate this process each month and once completed, an email will be send as a confirmation.
<img src="https://github.com/abychen01/Transactions/blob/b280254b1c69d5c77f75f255a9b20a81e1e3373d/MonthlyDataETL%20Pipeline.png" width="400">   
6. A new semantic model is created for Power BI report called newTransactionData from the Lakehouse tables. The model contains the dates, newtransactiondata and location table.
7. Power BI desktop is connected live to the semantic model using DirectLake storage mode.
<img src="https://github.com/abychen01/Transactions/blob/4c7e0d05623817eb58cc8fd981ad613610fe2f8b/newTransactionData.png" width="400">
