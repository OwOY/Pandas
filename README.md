<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/1200px-Pandas_logo.svg.png">  

## Install
```
python -m pip install pandas
```
## How to Use
### import  
```
import pandas as pd
```
### Open Excel
- CSV
```
pd.read_csv(...)
```
- XLSX
```
# python -m pip install openpyxl
pd.read_Excel(..., engine='openpyxl')
```
### Useful params
```
filepath = csv_name,
sheet_name = sheet_name,
usecols = ['col1', 'col2'],
header = None,     #設置沒有index
```
## Use Data
### DataFrame
```
import pandas as pd
test = [{'p1':3, 'p2':5}, {'p1':7, 'p2':8}]
pd.DataFrame(test)
```
|p1|p2|  
|--|--|  
|3 | 5|  
|7 | 8|  
