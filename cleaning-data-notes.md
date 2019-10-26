# Getting and Cleaning Data Notes

## Data analyze should contains
* Original (raw) dataset
* Cleared dataset
* Variables with meaning (description)
* Each variable should be in separated column
* Each observation as single row
* Remember to add units for variables' description
* Write in report each decision why use or prepare something
* Code how from original dataset make cleared
* Script should allows us to do the same process more than one time, each time we should receive the same result

## dplyr
* With `tbl_df` we can create a data frame from dataset
* The main advantage to using a `tbl_df` over a regular `data frame` is the printing
* `select(tbl_df, columns ...)` - we can use columns without `$name`, just `name`; support also `start:end` columns and except by `-ignored_column_name`
* `filter(df, query)` - select a subset of rows, when we decide to use `AND` we should separate queries by `,` (comma); for `OR` we need use `|`
* `arrange(df, asc(field_1), desc(field_2))` - order by `asc: field_1`, `desc: field_2`
* `mutate(df, new_column = operation)` - create `new_column` like described in `operation`
* `summarize(df, column = operation)` - collapse the data frame to a single row
* `group_by(df, group by column)`
* `n()`, `n_distinct(key)`
* `%>%` - chaining operator, as first parameter we have result from previous function
* `bind_rows(df_1, df_2)` - join dfs into single unit

## tidyr
* `gather(source, key, value, except)`
* `separate(data, col, into)`
* `spread()`

## readr
* `parse_number()`

## lubridate
* `today()`
* `now()`
* `wday()`
* `ymd(string / int)`, `dym()`, `mdy()`
* `with_tz()` - convert time to expected Time Zone
