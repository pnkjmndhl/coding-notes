### merge, join, concatenate and compare

- `pd.concat([df1, df2, df3], join = "outer", ignore_index=False)`


### locate

- `df.iloc[x,y]`
  - stands for "integer location", based on the count
  - x-> row, y->column
- `df.loc[x,y]`
  - stands for "location", based on the labels (index or columns)
     
### groupby
- `df.groupby(['column1', 'column2']).agg({'column3': sum, 'column4': mean, 'column5': custom_func})`
  - the column1 and column2 would be the columns whose unique values would be grouped by
  - the agg columns are the columns that would be aggregated
### pivot_table
- `pd.pivot_table(data, values= None , index= None, columns= None,  aggfunc='mean')`
  - `values` -> the list of the columns that you want to perform `aggfunc`  (optional)
  -  `index` -> columns that would be used in the pivottable index
  -  `columns` -> columns that would be used in the pivottable columns
  - tldr: a `groupby` + columns



### read_csv
```py
- sep = ","
- delimiter = '"' # sep and delimiter cannot both exist
- on_bad_lines = <function> # the function should take bad_lines as argument and handle it
- quotechar = '"'
- dtype = {'colname': 'dtype', ...}
- na_values = [...] # list of values that should be considered np.nan
- keep_default_na = True/False # do you want to keep or remove the default nan values
- engine = "python"/"c"/"pyarrow" 
- encoding = 'utf-8'
``` 


### create a .txt file and write
```py
with open('filename.txt', 'a') as file: # 'r'-> read, 'w'->write, 'a'->append
    file.write(line + "\n")
```

### create a .txt file and write
```py
with open('filename.txt', 'r') as file: # 'r'-> read, 'w'->write, 'a'->append
    lines = file.readlines() # creates a list of lines in python
```    