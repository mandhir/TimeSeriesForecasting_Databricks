# TimeSeriesForecasting_Databricks

#### *Parts of this notebook have been obfuscated to protect privacy and security*

### Installation and Import Packages

```sh
%sh
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list 
apt-get update
ACCEPT_EULA=Y apt-get install msodbcsql17
apt-get -y install unixodbc-dev
sudo apt-get install python3-pip -y
pip3 install --upgrade pyodbc
```

```python
import os

import pandas as pd
import pyodbc as dbc
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```


### Importing data from SQL Server and exploring range of data

```python
#set up connection to SQL prod server
prod_conn = dbc.connect('DRIVER={ODBC Driver 17 for SQL Server};'
                       'SERVER=SERVER_NAME;'
                       'DATABASE=DATABASE_NAME;UID=USERNAME;'
                       'PWD=PASSWORD')

query = '''
select MIN(TRANSACTION_DATE) minimum_date, MAX(TRANSACTION_DATE) maximum_date, COUNT(*) number_of_rows
FROM DATABASE_NAME.TABLE_NAME
WHERE ORG_ID = 87
'''
date_range = pd.read_sql_query(query, prod_conn)
date_range

```



