# Transactions

Transactions is a project created for monitoring and reviewing financial transactions. Financial transaction data from the Bank of Nova Scotia is obtained from the instituion website. The report compares the different transactions performed to provide meaningfull financial insight such as unknown charges, high value transactions, comparing previous date period data and more.

#### <ins> Data Sources </ins>
1. Dates - Date table, created using Dataflow Gen 2 in Fabric or Power Query using M language in Power BI Desktop app.
2. Location - Table consisting of Canadian cities and respective data downloaded from https://simplemaps.com/data/canada-cities as CSV file.
  <img src="https://github.com/abychen01/Transactions/blob/35b27ccf73b930a15ab3fb1114fe97ceb187c14a/location%20sample.png" width="900">
3. Newtransactiondata - Table with the latest transaction data.

#### <ins> Functionality </ins>
1. Financial transaction data (fact table data) from the Bank of Nova Scotia is exported manually (API not avaialable at the moment) from the instituion website as CSV files.
2. A Fabric workspace called Transactions - dev is setup using large semantic model storage format. Data will be stored in the Transactions Lakehouse inside the Transactions - dev workspace.     
  <img src="https://github.com/abychen01/Transactions/blob/812758bb7d752b5d4a24b08d21ac40f2ec6c6114/Transactions%20-%20dev%20workspace.png" width="400">
3. CSV files are uploaded as files to the Monthly Data folder for ETL. Data can be directly uploaded from the Fabric website or using OneLake File Explorer.
  <img src="https://github.com/abychen01/Transactions/blob/35b27ccf73b930a15ab3fb1114fe97ceb187c14a/Monthly%20Data%20folder.png" width="400">
4. 
