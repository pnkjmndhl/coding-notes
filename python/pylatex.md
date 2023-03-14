### intro


### setting up
`from pylatex import Document, Package, Center, NoEscape`

### building tables

#### some basic commands
- using `multirow` and `multicolumn`
- `table.add_hline()` adds a horizontal line
- `table.add_row((MultiColumn(4, align='|c|', data='Multicolumn'),))` adds a row, with 4 combined columns, aligned in the middle, and the content is 'Multicolumn'
- `table1.add_row((1, 2, 3, 4))` adds a row, with 4 columns with values mentioned\
- `table.add_row(('9', MultiColumn(3, align='|c|', data='Multicolumn not on left')))` adds a row with 2 columns, out of which later 3 are combined with content "Multicolumn not on left"
- `table.add_row((MultiRow(3, data='Multirow'), 1, 2))` adds a row (the first column is 1/3), and the remaining two has values of 1 and 2
- `table.add_hline(2,3)` adds a horizontal line but only on 2 and 3 columns