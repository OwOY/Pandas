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
usecols = ['col1', 'col2'],  # If 
header = None,     # 設置沒有index
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

### Turn data to list dict
```
data = pd.DataFrame(test, columns=['p1','p2'])
output = data.iloc('records')
```
>> output = [{'p1':3, 'p2':5}, {'p1':7, 'p2':8}]

### trans Data NaN > None  
df = pd.read_csv('test.csv')  
```
method1
df = df.where(df.notnull(), None)
method2
import numpy as np
df = df.replace({np.nan: None})
```
### sorted by values
```
df.sort_values(by=col, inplace=True)    #inplace 若True 可迭代
```
### concat column values to list
```
df['test'] = list(zip(df[col1], df[col2]))
```
### group_by get_group
|p1|p2|  
|--|--|  
|3 | 5|  
|7 | 8|  
```
df = df.groupby([p1, p2])
df.get_group((3, 5))
```
### group_by and concat another column
```
df = df.groupby([col1, col2, col3])['test'].apply(list)
```
### group_by keep column
```
df = df.groupby('model', as_index=False) # 可保留 group 之 Column
```
>> [(a,b,c):['1','2','3']]  
## Download
- excel
```
df.to_excel(f'{path_name}', sheet_name=f'{sheet_name}')
```
- csv
```
df.to_csv(f'{path_name}', sheet_name=f'{sheet_name}')
```
- multisheet
```
writer = pd.ExcelWriter(f'{excel_name}', engine='xlsxwriter')
df1.to_excel(writer, sheet_name='sheet_name1')
df2.to_excel(writer, sheet_name='sheet_name2')
writer.save()
```
- memory
```
from io import BytesIO
output = BytesIO()
writer = pd.ExcelWriter(output, engine='xlsxwriter')
df_MLB.to_excel(writer, sheet_name='MLB Build Plan')
df_PAD.to_excel(writer, sheet_name='IPAD Build Plan')
writer.save()
output.seek(0)
```
