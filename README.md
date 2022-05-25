<div align='center'>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Pandas_logo.svg/1200px-Pandas_logo.svg.png" width=85% height=75%>  
</div>

## Install
```
python -m pip install pandas
```
## How to Use
### import  
```
import pandas as pd
```
## Open Excel  
- Useful params
```
filepath = csv_name,  
sheet_name = sheet_name,  
usecols = ['col1', 'col2'],  
header = None,     # 設置沒有index  
keep_default_na=False # replace nan > ''  
dtype = {'column':str, 'column2':int} # set output format
```
#### if data > 15MB
- use hdf (more faster)
#### if data < 15MB
- use csv

- CSV
```
pd.read_csv(...)
```
- XLSX
```
# python -m pip install openpyxl
pd.read_Excel(..., engine='openpyxl')
```
- HDF
```
# python -m pip install tables
pd.read_hdf('test.h5', key='asd') # key can be anything
```

## DataFrame
```
import pandas as pd
test = [{'p1':3, 'p2':5}, {'p1':7, 'p2':8}]
pd.DataFrame(test)
```
|p1|p2|  
|--|--|  
|3 | 5|  
|7 | 8|  

### filter
- normal
```
df = df[
        (df[column] == 'test') &
        (df[column2] == 'test1)
        ]
# 小括弧必加！！
```
- fuzzy search
```
df = df[
        df[column].str.startwith('te') &   # startwith 'te'
        df[column].str.endwith('st') &   # endwith 'st'
        df[column].str.contains('es') &   # string contains es 
        ]
```

### add Data
```
data = [{'test1':1, 'test2':2}, {'test1':1, 'test2':2}]
df = pd.DataFrame(data)
new_data = [{'test1':2, 'test2':3}, {'test1':2, 'test2':3}]
new_df = pd.DataFrame(new_data)
df.append(new_df, inplace=True) # inplace 可直接迭代
```

### edit Data
1. 先篩選出要修改的欄位
2. 根據篩選出的index替換column資料
```
match_df = df[df[column] == 'test]
df.loc[match_df.index, column] = 'test1'
```

### drop Data
1. 先篩選出要刪除的欄位
2. 根據篩選出的index刪除
```
match_df = df[df[column] == 'test]
df.drop(match_df.index, inplace = True) # inplace 可直接迭代
```

### Turn data to list dict
```
data = pd.DataFrame(test, columns=['p1','p2'])
output = data.iloc('records')
```
>> output = [{'p1':3, 'p2':5}, {'p1':7, 'p2':8}]

### trans Data NaN > None  
```
method1
df = df.where(df.notnull(), None)
method2
import numpy as np
df = df.replace({np.nan: None})
```

### sorted by values
```
# method1
df.sort_values(by=col, inplace=True) #inplace 若True 可迭代
# method2
df.sort_values([col1, col2], ascending=[True, False])
```

### concat column values to list
```
df['test'] = list(zip(df[col1], df[col2]))
```

### group_by
|p1|p2|  
|--|--|  
|3 | 5|  
|7 | 8|  
```
df = df.groupby([p1, p2])
df.groups # group = value
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

### group sort
```
df = df.sort_values(['a', 'b'], ascending=True) # 升冪
```

### pivot重作DataFrame(groupby後)  
```
exist_df = df[df['MTNO'] != '無匹配資料']
output_df = exist_df_group.pivot('MTNO', 'date').fillna(0)
```

### 輸出合併儲存格
example:  
```
writer = pd.ExcelWriter('foo.xlsx')
workbook = writer.book
workbook_format = workbook.add_format({'align':'center', 'border':True}) # 改變儲存格格式
df = pd.DataFrame(new_data)
df.to_excel(writer, sheet_name='Sheet1', index=False)
write_sheet = writer.sheets['Sheet1']
write_sheet.merge_range('B1:C1', '材料編號', workbook_format) # 合併
write_sheet.merge_range('D1:G1', '規格', workbook_format)
writer.save()
```


## Download
- excel
```
df.to_excel(f'{path_name}', sheet_name=f'{sheet_name}')
```
- csv
```
df.to_csv(f'{path_name}', sheet_name=f'{sheet_name}')
```
- hdf
```
df.to_hdf(f'{path_name}', key='abc')
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
