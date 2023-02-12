### formatters and using `str.format(value1, value2, ...)`
- placeholders using named indexes -> `{price}`, numbered indexes->`{0}`, and empty placeholders `{}`
  - `My name is {fname}, I'm {age}".format(fname = "John", age = 36)`
  - `"My name is {0}, I'm {1}".format("John",36)`
  - `"My name is {}, I'm {}".format("John",36)`
- formatting types, inside `{}`
  - `:,` uses comma as thousands separator, results 100,000
  - `:.0f` no floating point values, results 4
  - `:.1%` percent with one decimal, results 3.4%


