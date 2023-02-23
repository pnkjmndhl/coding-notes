### formatters and using `str.format(value1, value2, ...)`
- placeholders using named indexes -> `{price}`, numbered indexes->`{0}`, and empty placeholders `{}`
  - `My name is {fname}, I'm {age}".format(fname = "John", age = 36)`
  - `"My name is {0}, I'm {1}".format("John",36)`
  - `"My name is {}, I'm {}".format("John",36)`
- formatting types, inside `{}`
  - `:,` uses comma as thousands separator, results 100,000
  - `:.0f` no floating point values, results 4
  - `:.1%` percent with one decimal, results 3.4%


### different file formats that you can save
- if you cast the datatype in dataframe, you'll reduce the size
- when you save as csv and read it back in, you loose information about the dtypes
  - you can add the metadata again using dtypes in read_csv
- when the dataset is very big
- pickle
  - use `df.to_pickle()`
  - faster, smaller and metadata is not lost

- parquet (faster and smaller)
  - `pip install pyarrow`
  - `pip install fastparquet`

- feather (faster than parquet, but a little bit larger than parquet)