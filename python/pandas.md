### merge, join, concatenate and compare

- `pd.concat([df1, df2, df3], join = "outer", ignore_index=False)`


### locate

- `df.iloc[x,y]`
  - stands for "integer location", based on count
  - x-> row, y->column
- `df.loc[x,y]`
  - stands for "locaation", based on the labels (index or columns)
     

### pivot_table

pd.pivot_table(dataframe, values= , columns= , )

