# Massive Data Exploration

## S language
* Created in 1976 as a programming language for statisticians

## R language
* Based on S language (is a dialect of S language)
* Interactive
* Packets-based
* Amazing for data visualization
* Open source, free to use
* Weak 3D visualization support
* In memory storage - issue when huge amount of data

### Types
* Five basic types - `character`, `numeric`, `integer`, `complex` and `logical`
* `vector` - base for complex data, can store items of one type
* Numbers are as default `numeric` (float value), for `integer` we need use `L` padding (eg. `12L`)
* Special `Inf` (infinity) and `NaN` (not a number)

### Attributes
* For object we can use `names`, `dimnames`, `dimensions`, `class`, `length` and many prepared by user metadata
* Attributes can be write / read by function `attributes()`

### Console
* `variable <- value` where `<-` mean assign
* `#` we should use to start comment
* Display variable: just write `variable` or directly `print(variable)`

### Vectors
* `c()` can be used to concatenate objects into vector (you can use also `vector()` constructor)
* Sometimes we should use cast function `as.numeric` or another `as.TYPE`, if cast fail as result `NA`

### Matrix
* Vector with attribute `dimension` (vector `nrow`, `ncol`)
* Can be created by `matrix(nrow = X, ncol = Y)`
* `cbind(x, y)` or `rbind(x, y)` can be used to create matrix with filled fields

### Lists
* Can store elements of many types
* Constructor `list(elem1, elem2, ...)`

### Data frames
* Can store tabularized data with named columns
* `data.frame(foo = 1:4, bar = c(T, T, F, F))` generate matrix with `nrow(x) = 4` and `ncol(x) = 4`
```
   foo  bar
1   1  TRUE
2   2  TRUE
3   3  FALSE
4   4  FALSE
```

### Enums
* In R called `factor` type
* Each value `level` can be represented by integer value with string
* Can be `orderly` or `non orderly` (nominal)

### Missing values
* `NA` - Not Available values
* `NaN` also is a missing value
* Has own `class` attribute so `NA` for `integer` can be different than for `character`
* `is.na/1` or `is.nan/1` checks - as return `TRUE | FALSE`
