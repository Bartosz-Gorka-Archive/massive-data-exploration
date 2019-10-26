# Getting and Cleaning Data
## Manipulating Data with dplyr
```r
| I've created a variable called path2csv, which contains the full file path to the dataset. Call read.csv()
| with two arguments, path2csv and stringsAsFactors = FALSE, and save the result in a new variable called
| mydf. Check ?read.csv if you need help.
```
```r
> mydf <- read.csv(path2csv, stringsAsFactors = FALSE)

| You are really on a roll!
```
```r
| Use dim() to look at the dimensions of mydf.
```
```r
> dim(mydf)
[1] 225468     11

| You are really on a roll!
```
```r
| Now use head() to preview the data.
```
```r
> head(mydf)
  X       date     time   size r_version r_arch      r_os      package version country ip_id
1 1 2014-07-08 00:54:41  80589     3.1.0 x86_64   mingw32    htmltools   0.2.4      US     1
2 2 2014-07-08 00:59:53 321767     3.1.0 x86_64   mingw32      tseries 0.10-32      US     2
3 3 2014-07-08 00:47:13 748063     3.1.0 x86_64 linux-gnu        party  1.0-15      US     3
4 4 2014-07-08 00:48:05 606104     3.1.0 x86_64 linux-gnu        Hmisc  3.14-4      US     3
5 5 2014-07-08 00:46:50  79825     3.0.2 x86_64 linux-gnu       digest   0.6.4      CA     4
6 6 2014-07-08 00:48:04  77681     3.1.0 x86_64 linux-gnu randomForest   4.6-7      US     3

| You are quite good my friend!
```
```r
| The dplyr package was automatically installed (if necessary) and loaded at the beginning of this lesson.
| Normally, this is something you would have to do on your own. Just to build the habit, type library(dplyr)
| now to load the package again.
```
```r
> library(dplyr)

| You are really on a roll!
```
```r
| It's important that you have dplyr version 0.4.0 or later. To confirm this, type packageVersion("dplyr").
```
```r
> packageVersion("dplyr")
[1] ‘0.8.3’

| You nailed it! Good job!
```
```r
| If your dplyr version is not at least 0.4.0, then you should hit the Esc key now, reinstall dplyr, then
| resume this lesson where you left off.
```
```r
| The first step of working with data in dplyr is to load the data into what the package authors call a 'data
| frame tbl' or 'tbl_df'. Use the following code to create a new tbl_df called cran:
|
| cran <- tbl_df(mydf).
```
```r
> cran <- tbl_df(mydf)

| You are really on a roll!
```
```r
| To avoid confusion and keep things running smoothly, let's remove the original data frame from your
| workspace with rm("mydf").
```
```r
> rm("mydf")

| You nailed it! Good job!
```
```r
| From ?tbl_df, "The main advantage to using a tbl_df over a regular data frame is the printing." Let's see
| what is meant by this. Type cran to print our tbl_df to the console.
```
```r
> cran
# A tibble: 225,468 x 11
       X date       time        size r_version r_arch r_os      package      version country ip_id
   <int> <chr>      <chr>      <int> <chr>     <chr>  <chr>     <chr>        <chr>   <chr>   <int>
 1     1 2014-07-08 00:54:41   80589 3.1.0     x86_64 mingw32   htmltools    0.2.4   US          1
 2     2 2014-07-08 00:59:53  321767 3.1.0     x86_64 mingw32   tseries      0.10-32 US          2
 3     3 2014-07-08 00:47:13  748063 3.1.0     x86_64 linux-gnu party        1.0-15  US          3
 4     4 2014-07-08 00:48:05  606104 3.1.0     x86_64 linux-gnu Hmisc        3.14-4  US          3
 5     5 2014-07-08 00:46:50   79825 3.0.2     x86_64 linux-gnu digest       0.6.4   CA          4
 6     6 2014-07-08 00:48:04   77681 3.1.0     x86_64 linux-gnu randomForest 4.6-7   US          3
 7     7 2014-07-08 00:48:35  393754 3.1.0     x86_64 linux-gnu plyr         1.8.1   US          3
 8     8 2014-07-08 00:47:30   28216 3.0.2     x86_64 linux-gnu whisker      0.3-2   US          5
 9     9 2014-07-08 00:54:58    5928 NA        NA     NA        Rcpp         0.10.4  CN          6
10    10 2014-07-08 00:15:35 2206029 3.0.2     x86_64 linux-gnu hflights     0.1     US          7
# … with 225,458 more rows

| You got it!
```
```r
| This output is much more informative and compact than what we would get if we printed the original data
| frame (mydf) to the console.
```
```r
| First, we are shown the class and dimensions of the dataset. Just below that, we get a preview of the data.
| Instead of attempting to print the entire dataset, dplyr just shows us the first 10 rows of data and only
| as many columns as fit neatly in our console. At the bottom, we see the names and classes for any variables
| that didn't fit on our screen.
```
```r
| According to the "Introduction to dplyr" vignette written by the package authors, "The dplyr philosophy is
| to have small functions that each do one thing well." Specifically, dplyr supplies five 'verbs' that cover
| most fundamental data manipulation tasks: select(), filter(), arrange(), mutate(), and summarize().
```
```r
| Use ?select to pull up the documentation for the first of these core functions.
```
```r
> ?select

| That's a job well done!
```
```r
| Help files for the other functions are accessible in the same way.
```
```r
| As may often be the case, particularly with larger datasets, we are only interested in some of the
| variables. Use select(cran, ip_id, package, country) to select only the ip_id, package, and country
| variables from the cran dataset.
```
```r
> select(cran, ip_id, package, country)
# A tibble: 225,468 x 3
   ip_id package      country
   <int> <chr>        <chr>  
 1     1 htmltools    US     
 2     2 tseries      US     
 3     3 party        US     
 4     3 Hmisc        US     
 5     4 digest       CA     
 6     3 randomForest US     
 7     3 plyr         US     
 8     5 whisker      US     
 9     6 Rcpp         CN     
10     7 hflights     US     
# … with 225,458 more rows

| Perseverance, that's the answer.
```
```r
| The first thing to notice is that we don't have to type cran$ip_id, cran$package, and cran$country, as we
| normally would when referring to columns of a data frame. The select() function knows we are referring to
| columns of the cran dataset.
```
```r
| Also, note that the columns are returned to us in the order we specified, even though ip_id is the
| rightmost column in the original dataset.
```
```r
| Recall that in R, the `:` operator provides a compact notation for creating a sequence of numbers. For
| example, try 5:20.
```
```r
> 5:20
 [1]  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

| You are amazing!
```
```r
| Normally, this notation is reserved for numbers, but select() allows you to specify a sequence of columns
| this way, which can save a bunch of typing. Use select(cran, r_arch:country) to select all columns starting
| from r_arch and ending with country.
```
```r
> select(cran, r_arch:country)
# A tibble: 225,468 x 5
   r_arch r_os      package      version country
   <chr>  <chr>     <chr>        <chr>   <chr>  
 1 x86_64 mingw32   htmltools    0.2.4   US     
 2 x86_64 mingw32   tseries      0.10-32 US     
 3 x86_64 linux-gnu party        1.0-15  US     
 4 x86_64 linux-gnu Hmisc        3.14-4  US     
 5 x86_64 linux-gnu digest       0.6.4   CA     
 6 x86_64 linux-gnu randomForest 4.6-7   US     
 7 x86_64 linux-gnu plyr         1.8.1   US     
 8 x86_64 linux-gnu whisker      0.3-2   US     
 9 NA     NA        Rcpp         0.10.4  CN     
10 x86_64 linux-gnu hflights     0.1     US     
# … with 225,458 more rows

| All that practice is paying off!
```
```r
| We can also select the same columns in reverse order. Give it a try.
```
```r
> select(cran, country:r_arch)
# A tibble: 225,468 x 5
   country version package      r_os      r_arch
   <chr>   <chr>   <chr>        <chr>     <chr>
 1 US      0.2.4   htmltools    mingw32   x86_64
 2 US      0.10-32 tseries      mingw32   x86_64
 3 US      1.0-15  party        linux-gnu x86_64
 4 US      3.14-4  Hmisc        linux-gnu x86_64
 5 CA      0.6.4   digest       linux-gnu x86_64
 6 US      4.6-7   randomForest linux-gnu x86_64
 7 US      1.8.1   plyr         linux-gnu x86_64
 8 US      0.3-2   whisker      linux-gnu x86_64
 9 CN      0.10.4  Rcpp         NA        NA    
10 US      0.1     hflights     linux-gnu x86_64
# … with 225,458 more rows

| That's a job well done!
```
```r
| Print the entire dataset again, just to remind yourself of what it looks like. You can do this at anytime
| during the lesson.
```
```r
> cran
# A tibble: 225,468 x 11
       X date       time        size r_version r_arch r_os      package      version country ip_id
   <int> <chr>      <chr>      <int> <chr>     <chr>  <chr>     <chr>        <chr>   <chr>   <int>
 1     1 2014-07-08 00:54:41   80589 3.1.0     x86_64 mingw32   htmltools    0.2.4   US          1
 2     2 2014-07-08 00:59:53  321767 3.1.0     x86_64 mingw32   tseries      0.10-32 US          2
 3     3 2014-07-08 00:47:13  748063 3.1.0     x86_64 linux-gnu party        1.0-15  US          3
 4     4 2014-07-08 00:48:05  606104 3.1.0     x86_64 linux-gnu Hmisc        3.14-4  US          3
 5     5 2014-07-08 00:46:50   79825 3.0.2     x86_64 linux-gnu digest       0.6.4   CA          4
 6     6 2014-07-08 00:48:04   77681 3.1.0     x86_64 linux-gnu randomForest 4.6-7   US          3
 7     7 2014-07-08 00:48:35  393754 3.1.0     x86_64 linux-gnu plyr         1.8.1   US          3
 8     8 2014-07-08 00:47:30   28216 3.0.2     x86_64 linux-gnu whisker      0.3-2   US          5
 9     9 2014-07-08 00:54:58    5928 NA        NA     NA        Rcpp         0.10.4  CN          6
10    10 2014-07-08 00:15:35 2206029 3.0.2     x86_64 linux-gnu hflights     0.1     US          7
# … with 225,458 more rows

| All that practice is paying off!
```
```r
| Instead of specifying the columns we want to keep, we can also specify the columns we want to throw away.
| To see how this works, do select(cran, -time) to omit the time column.
```
```r
> select(cran, -time)
# A tibble: 225,468 x 10
       X date          size r_version r_arch r_os      package      version country ip_id
   <int> <chr>        <int> <chr>     <chr>  <chr>     <chr>        <chr>   <chr>   <int>
 1     1 2014-07-08   80589 3.1.0     x86_64 mingw32   htmltools    0.2.4   US          1
 2     2 2014-07-08  321767 3.1.0     x86_64 mingw32   tseries      0.10-32 US          2
 3     3 2014-07-08  748063 3.1.0     x86_64 linux-gnu party        1.0-15  US          3
 4     4 2014-07-08  606104 3.1.0     x86_64 linux-gnu Hmisc        3.14-4  US          3
 5     5 2014-07-08   79825 3.0.2     x86_64 linux-gnu digest       0.6.4   CA          4
 6     6 2014-07-08   77681 3.1.0     x86_64 linux-gnu randomForest 4.6-7   US          3
 7     7 2014-07-08  393754 3.1.0     x86_64 linux-gnu plyr         1.8.1   US          3
 8     8 2014-07-08   28216 3.0.2     x86_64 linux-gnu whisker      0.3-2   US          5
 9     9 2014-07-08    5928 NA        NA     NA        Rcpp         0.10.4  CN          6
10    10 2014-07-08 2206029 3.0.2     x86_64 linux-gnu hflights     0.1     US          7
# … with 225,458 more rows

| Great job!
```
```r
| The negative sign in front of time tells select() that we DON'T want the time column. Now, let's combine
| strategies to omit all columns from X through size (X:size). To see how this might work, let's look at a
| numerical example with -5:20.
```
```r
> -5:20
 [1] -5 -4 -3 -2 -1  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

| Keep working like that and you'll get there!
```
```r
| Oops! That gaves us a vector of numbers from -5 through 20, which is not what we want. Instead, we want to
| negate the entire sequence of numbers from 5 through 20, so that we get -5, -6, -7, ... , -18, -19, -20.
| Try the same thing, except surround 5:20 with parentheses so that R knows we want it to first come up with
| the sequence of numbers, then apply the negative sign to the whole thing.
```
```r
> -(5:20)
 [1]  -5  -6  -7  -8  -9 -10 -11 -12 -13 -14 -15 -16 -17 -18 -19 -20

| You nailed it! Good job!
```
```r
| Use this knowledge to omit all columns X:size using select().
```
```r
> select(cran, -(X:size))
# A tibble: 225,468 x 7
   r_version r_arch r_os      package      version country ip_id
   <chr>     <chr>  <chr>     <chr>        <chr>   <chr>   <int>
 1 3.1.0     x86_64 mingw32   htmltools    0.2.4   US          1
 2 3.1.0     x86_64 mingw32   tseries      0.10-32 US          2
 3 3.1.0     x86_64 linux-gnu party        1.0-15  US          3
 4 3.1.0     x86_64 linux-gnu Hmisc        3.14-4  US          3
 5 3.0.2     x86_64 linux-gnu digest       0.6.4   CA          4
 6 3.1.0     x86_64 linux-gnu randomForest 4.6-7   US          3
 7 3.1.0     x86_64 linux-gnu plyr         1.8.1   US          3
 8 3.0.2     x86_64 linux-gnu whisker      0.3-2   US          5
 9 NA        NA     NA        Rcpp         0.10.4  CN          6
10 3.0.2     x86_64 linux-gnu hflights     0.1     US          7
# … with 225,458 more rows

| Keep working like that and you'll get there!
```
```r
| Now that you know how to select a subset of columns using select(), a natural next question is "How do I
| select a subset of rows?" That's where the filter() function comes in.
```
```r
| Use filter(cran, package == "swirl") to select all rows for which the package variable is equal to "swirl".
| Be sure to use two equals signs side-by-side!
```
```r
> filter(cran, package == "swirl")
# A tibble: 820 x 11
       X date       time       size r_version r_arch r_os         package version country ip_id
   <int> <chr>      <chr>     <int> <chr>     <chr>  <chr>        <chr>   <chr>   <chr>   <int>
 1    27 2014-07-08 00:17:16 105350 3.0.2     x86_64 mingw32      swirl   2.2.9   US         20
 2   156 2014-07-08 00:22:53  41261 3.1.0     x86_64 linux-gnu    swirl   2.2.9   US         66
 3   358 2014-07-08 00:13:42 105335 2.15.2    x86_64 mingw32      swirl   2.2.9   CA        115
 4   593 2014-07-08 00:59:45 105465 3.1.0     x86_64 darwin13.1.0 swirl   2.2.9   MX        162
 5   831 2014-07-08 00:55:27 105335 3.0.3     x86_64 mingw32      swirl   2.2.9   US         57
 6   997 2014-07-08 00:33:06  41261 3.1.0     x86_64 mingw32      swirl   2.2.9   US         70
 7  1023 2014-07-08 00:35:36 106393 3.1.0     x86_64 mingw32      swirl   2.2.9   BR        248
 8  1144 2014-07-08 00:00:39 106534 3.0.2     x86_64 linux-gnu    swirl   2.2.9   US        261
 9  1402 2014-07-08 00:41:41  41261 3.1.0     i386   mingw32      swirl   2.2.9   US        234
10  1424 2014-07-08 00:44:49 106393 3.1.0     x86_64 linux-gnu    swirl   2.2.9   US        301
# … with 810 more rows

| Keep working like that and you'll get there!
```
```r
| Again, note that filter() recognizes 'package' as a column of cran, without you having to explicitly
| specify cran$package.
```
```r
| The == operator asks whether the thing on the left is equal to the thing on the right. If yes, then it
| returns TRUE. If no, then FALSE. In this case, package is an entire vector (column) of values, so package
| == "swirl" returns a vector of TRUEs and FALSEs. filter() then returns only the rows of cran corresponding
| to the TRUEs.
```
```r
| You can specify as many conditions as you want, separated by commas. For example filter(cran, r_version ==
| "3.1.1", country == "US") will return all rows of cran corresponding to downloads from users in the US
| running R version 3.1.1. Try it out.
```
```r
> filter(cran, r_version == "3.1.1", country == "US")
# A tibble: 1,588 x 11
       X date       time        size r_version r_arch r_os         package      version country ip_id
   <int> <chr>      <chr>      <int> <chr>     <chr>  <chr>        <chr>        <chr>   <chr>   <int>
 1  2216 2014-07-08 00:48:58  385112 3.1.1     x86_64 darwin13.1.0 colorspace   1.2-4   US        191
 2 17332 2014-07-08 03:39:57  197459 3.1.1     x86_64 darwin13.1.0 httr         0.3     US       1704
 3 17465 2014-07-08 03:25:38   23259 3.1.1     x86_64 darwin13.1.0 snow         0.3-13  US         62
 4 18844 2014-07-08 03:59:17  190594 3.1.1     x86_64 darwin13.1.0 maxLik       1.2-0   US       1533
 5 30182 2014-07-08 04:13:15   77683 3.1.1     i386   mingw32      randomForest 4.6-7   US        646
 6 30193 2014-07-08 04:06:26 2351969 3.1.1     i386   mingw32      ggplot2      1.0.0   US          8
 7 30195 2014-07-08 04:07:09  299080 3.1.1     i386   mingw32      fExtremes    3010.81 US       2010
 8 30217 2014-07-08 04:32:04  568036 3.1.1     i386   mingw32      rJava        0.9-6   US         98
 9 30245 2014-07-08 04:10:41  526858 3.1.1     i386   mingw32      LPCM         0.44-8  US          8
10 30354 2014-07-08 04:32:51 1763717 3.1.1     i386   mingw32      mgcv         1.8-1   US       2122
# … with 1,578 more rows

| You are quite good my friend!
```
```r
| The conditions passed to filter() can make use of any of the standard comparison operators. Pull up the
| relevant documentation with ?Comparison (that's an uppercase C).
```
```r
> ?Comparison

| You are doing so well!
```
```r
| Edit your previous call to filter() to instead return rows corresponding to users in "IN" (India) running
| an R version that is less than or equal to "3.0.2". The up arrow on your keyboard may come in handy here.
| Don't forget your double quotes!
```
```r
> filter(cran, r_version <= "3.0.2", country == "IN")
# A tibble: 4,139 x 11
       X date       time         size r_version r_arch r_os      package       version   country ip_id
   <int> <chr>      <chr>       <int> <chr>     <chr>  <chr>     <chr>         <chr>     <chr>   <int>
 1   348 2014-07-08 00:44:04 10218907 3.0.0     x86_64 mingw32   BH            1.54.0-2  IN        112
 2  9990 2014-07-08 02:11:32   397497 3.0.2     x86_64 linux-gnu equateIRT     1.1       IN       1054
 3  9991 2014-07-08 02:11:32   119199 3.0.2     x86_64 linux-gnu ggdendro      0.1-14    IN       1054
 4  9992 2014-07-08 02:11:33    81779 3.0.2     x86_64 linux-gnu dfcrm         0.2-2     IN       1054
 5 10022 2014-07-08 02:19:45  1557078 2.15.0    x86_64 mingw32   RcppArmadillo 0.4.320.0 IN       1060
 6 10023 2014-07-08 02:19:46  1184285 2.15.1    i686   linux-gnu forecast      5.4       IN       1060
 7 10189 2014-07-08 02:38:06   908854 3.0.2     x86_64 linux-gnu editrules     2.7.2     IN       1054
 8 10199 2014-07-08 02:38:28   178436 3.0.2     x86_64 linux-gnu energy        1.6.1     IN       1054
 9 10200 2014-07-08 02:38:29    51811 3.0.2     x86_64 linux-gnu ENmisc        1.2-7     IN       1054
10 10201 2014-07-08 02:38:29    65245 3.0.2     x86_64 linux-gnu entropy       1.2.0     IN       1054
# … with 4,129 more rows

| You got it!
```
```r
| Our last two calls to filter() requested all rows for which some condition AND another condition were TRUE.
| We can also request rows for which EITHER one condition OR another condition are TRUE. For example,
| filter(cran, country == "US" | country == "IN") will gives us all rows for which the country variable
| equals either "US" or "IN". Give it a go.
```
```r
> filter(cran, country == "US" | country == "IN")
# A tibble: 95,283 x 11
       X date       time        size r_version r_arch r_os      package      version country ip_id
   <int> <chr>      <chr>      <int> <chr>     <chr>  <chr>     <chr>        <chr>   <chr>   <int>
 1     1 2014-07-08 00:54:41   80589 3.1.0     x86_64 mingw32   htmltools    0.2.4   US          1
 2     2 2014-07-08 00:59:53  321767 3.1.0     x86_64 mingw32   tseries      0.10-32 US          2
 3     3 2014-07-08 00:47:13  748063 3.1.0     x86_64 linux-gnu party        1.0-15  US          3
 4     4 2014-07-08 00:48:05  606104 3.1.0     x86_64 linux-gnu Hmisc        3.14-4  US          3
 5     6 2014-07-08 00:48:04   77681 3.1.0     x86_64 linux-gnu randomForest 4.6-7   US          3
 6     7 2014-07-08 00:48:35  393754 3.1.0     x86_64 linux-gnu plyr         1.8.1   US          3
 7     8 2014-07-08 00:47:30   28216 3.0.2     x86_64 linux-gnu whisker      0.3-2   US          5
 8    10 2014-07-08 00:15:35 2206029 3.0.2     x86_64 linux-gnu hflights     0.1     US          7
 9    11 2014-07-08 00:15:25  526858 3.0.2     x86_64 linux-gnu LPCM         0.44-8  US          8
10    12 2014-07-08 00:14:45 2351969 2.14.1    x86_64 linux-gnu ggplot2      1.0.0   US          8
# … with 95,273 more rows

| You got it!
```
```r
| Now, use filter() to fetch all rows for which size is strictly greater than (>) 100500 (no quotes, since
| size is numeric) AND r_os equals "linux-gnu". Hint: You are passing three arguments to filter(): the name
| of the dataset, the first condition, and the second condition.
```
```r
> filter(cran, size > 100500, r_os == "linux-gnu")
# A tibble: 33,683 x 11
       X date       time        size r_version r_arch r_os      package  version country ip_id
   <int> <chr>      <chr>      <int> <chr>     <chr>  <chr>     <chr>    <chr>   <chr>   <int>
 1     3 2014-07-08 00:47:13  748063 3.1.0     x86_64 linux-gnu party    1.0-15  US          3
 2     4 2014-07-08 00:48:05  606104 3.1.0     x86_64 linux-gnu Hmisc    3.14-4  US          3
 3     7 2014-07-08 00:48:35  393754 3.1.0     x86_64 linux-gnu plyr     1.8.1   US          3
 4    10 2014-07-08 00:15:35 2206029 3.0.2     x86_64 linux-gnu hflights 0.1     US          7
 5    11 2014-07-08 00:15:25  526858 3.0.2     x86_64 linux-gnu LPCM     0.44-8  US          8
 6    12 2014-07-08 00:14:45 2351969 2.14.1    x86_64 linux-gnu ggplot2  1.0.0   US          8
 7    14 2014-07-08 00:15:35 3097729 3.0.2     x86_64 linux-gnu Rcpp     0.9.7   VE         10
 8    15 2014-07-08 00:14:37  568036 3.1.0     x86_64 linux-gnu rJava    0.9-6   US         11
 9    16 2014-07-08 00:15:50 1600441 3.1.0     x86_64 linux-gnu RSQLite  0.11.4  US          7
10    18 2014-07-08 00:26:59  186685 3.1.0     x86_64 linux-gnu ipred    0.9-3   DE         13
# … with 33,673 more rows

| You are really on a roll!
```
```r
| Finally, we want to get only the rows for which the r_version is not missing. R represents missing values
| with NA and these missing values can be detected using the is.na() function.
```
```r
| To see how this works, try is.na(c(3, 5, NA, 10)).
```
```r
> is.na(c(3, 5, NA, 10))
[1] FALSE FALSE  TRUE FALSE

| You are doing so well!
```
```r
| Now, put an exclamation point (!) before is.na() to change all of the TRUEs to FALSEs and all of the FALSEs
| to TRUEs, thus telling us what is NOT NA: !is.na(c(3, 5, NA, 10)).
```
```r
> !is.na(c(3, 5, NA, 10))
[1]  TRUE  TRUE FALSE  TRUE

| Excellent work!
```
```r
| Okay, ready to put all of this together? Use filter() to return all rows of cran for which r_version is NOT
| NA. Hint: You will need to use !is.na() as part of your second argument to filter().
```
```r
> filter(cran, !is.na(r_version))
# A tibble: 207,205 x 11
       X date       time        size r_version r_arch r_os      package      version country ip_id
   <int> <chr>      <chr>      <int> <chr>     <chr>  <chr>     <chr>        <chr>   <chr>   <int>
 1     1 2014-07-08 00:54:41   80589 3.1.0     x86_64 mingw32   htmltools    0.2.4   US          1
 2     2 2014-07-08 00:59:53  321767 3.1.0     x86_64 mingw32   tseries      0.10-32 US          2
 3     3 2014-07-08 00:47:13  748063 3.1.0     x86_64 linux-gnu party        1.0-15  US          3
 4     4 2014-07-08 00:48:05  606104 3.1.0     x86_64 linux-gnu Hmisc        3.14-4  US          3
 5     5 2014-07-08 00:46:50   79825 3.0.2     x86_64 linux-gnu digest       0.6.4   CA          4
 6     6 2014-07-08 00:48:04   77681 3.1.0     x86_64 linux-gnu randomForest 4.6-7   US          3
 7     7 2014-07-08 00:48:35  393754 3.1.0     x86_64 linux-gnu plyr         1.8.1   US          3
 8     8 2014-07-08 00:47:30   28216 3.0.2     x86_64 linux-gnu whisker      0.3-2   US          5
 9    10 2014-07-08 00:15:35 2206029 3.0.2     x86_64 linux-gnu hflights     0.1     US          7
10    11 2014-07-08 00:15:25  526858 3.0.2     x86_64 linux-gnu LPCM         0.44-8  US          8
# … with 207,195 more rows

| Keep working like that and you'll get there!
```
```r
| We've seen how to select a subset of columns and rows from our dataset using select() and filter(),
| respectively. Inherent in select() was also the ability to arrange our selected columns in any order we
| please.
```
```r
| Sometimes we want to order the rows of a dataset according to the values of a particular variable. This is
| the job of arrange().
```
```r
| To see how arrange() works, let's first take a subset of cran. select() all columns from size through ip_id
| and store the result in cran2.
```
```r
> cran2 <- select(cran, size:ip_id)

| Your dedication is inspiring!
```
```r
| Now, to order the ROWS of cran2 so that ip_id is in ascending order (from small to large), type
| arrange(cran2, ip_id). You may want to make your console wide enough so that you can see ip_id, which is
| the last column.
```
```r
> arrange(cran2, ip_id)
# A tibble: 225,468 x 8
     size r_version r_arch r_os         package     version country ip_id
    <int> <chr>     <chr>  <chr>        <chr>       <chr>   <chr>   <int>
 1  80589 3.1.0     x86_64 mingw32      htmltools   0.2.4   US          1
 2 180562 3.0.2     x86_64 mingw32      yaml        2.1.13  US          1
 3 190120 3.1.0     i386   mingw32      babel       0.2-6   US          1
 4 321767 3.1.0     x86_64 mingw32      tseries     0.10-32 US          2
 5  52281 3.0.3     x86_64 darwin10.8.0 quadprog    1.5-5   US          2
 6 876702 3.1.0     x86_64 linux-gnu    zoo         1.7-11  US          2
 7 321764 3.0.2     x86_64 linux-gnu    tseries     0.10-32 US          2
 8 876702 3.1.0     x86_64 linux-gnu    zoo         1.7-11  US          2
 9 321768 3.1.0     x86_64 mingw32      tseries     0.10-32 US          2
10 784093 3.1.0     x86_64 linux-gnu    strucchange 1.5-0   US          2
# … with 225,458 more rows

| Keep working like that and you'll get there!
```
```r
| To do the same, but in descending order, change the second argument to desc(ip_id), where desc() stands for
| 'descending'. Go ahead.
```
```r
> arrange(cran2, desc(ip_id))
# A tibble: 225,468 x 8
      size r_version r_arch r_os         package      version country ip_id
     <int> <chr>     <chr>  <chr>        <chr>        <chr>   <chr>   <int>
 1    5933 NA        NA     NA           CPE          1.4.2   CN      13859
 2  569241 3.1.0     x86_64 mingw32      multcompView 0.1-5   US      13858
 3  228444 3.1.0     x86_64 mingw32      tourr        0.5.3   NZ      13857
 4  308962 3.1.0     x86_64 darwin13.1.0 ctv          0.7-9   CN      13856
 5  950964 3.0.3     i386   mingw32      knitr        1.6     CA      13855
 6   80185 3.0.3     i386   mingw32      htmltools    0.2.4   CA      13855
 7 1431750 3.0.3     i386   mingw32      shiny        0.10.0  CA      13855
 8 2189695 3.1.0     x86_64 mingw32      RMySQL       0.9-3   US      13854
 9 4818024 3.1.0     i386   mingw32      igraph       0.7.1   US      13853
10  197495 3.1.0     x86_64 mingw32      coda         0.16-1  US      13852
# … with 225,458 more rows

| Perseverance, that's the answer.
```
```r
| We can also arrange the data according to the values of multiple variables. For example, arrange(cran2,
| package, ip_id) will first arrange by package names (ascending alphabetically), then by ip_id. This means
| that if there are multiple rows with the same value for package, they will be sorted by ip_id (ascending
| numerically). Try arrange(cran2, package, ip_id) now.
```
```r
> arrange(cran2, package, ip_id)
# A tibble: 225,468 x 8
    size r_version r_arch r_os         package version country ip_id
   <int> <chr>     <chr>  <chr>        <chr>   <chr>   <chr>   <int>
 1 71677 3.0.3     x86_64 darwin10.8.0 A3      0.9.2   CN       1003
 2 71672 3.1.0     x86_64 linux-gnu    A3      0.9.2   US       1015
 3 71677 3.1.0     x86_64 mingw32      A3      0.9.2   IN       1054
 4 70438 3.0.1     x86_64 darwin10.8.0 A3      0.9.2   CN       1513
 5 71677 NA        NA     NA           A3      0.9.2   BR       1526
 6 71892 3.0.2     x86_64 linux-gnu    A3      0.9.2   IN       1542
 7 71677 3.1.0     x86_64 linux-gnu    A3      0.9.2   ZA       2925
 8 71672 3.1.0     x86_64 mingw32      A3      0.9.2   IL       3889
 9 71677 3.0.3     x86_64 mingw32      A3      0.9.2   DE       3917
10 71672 3.1.0     x86_64 mingw32      A3      0.9.2   US       4219
# … with 225,458 more rows

| That's the answer I was looking for.
```
```r
| Arrange cran2 by the following three variables, in this order: country (ascending), r_version (descending),
| and ip_id (ascending).
```
```r
> arrange(cran2, country, desc(r_version), ip_id)
# A tibble: 225,468 x 8
      size r_version r_arch r_os      package       version   country ip_id
     <int> <chr>     <chr>  <chr>     <chr>         <chr>     <chr>   <int>
 1 1556858 3.1.1     i386   mingw32   RcppArmadillo 0.4.320.0 A1       2843
 2 1823512 3.1.0     x86_64 linux-gnu mgcv          1.8-1     A1       2843
 3   15732 3.1.0     i686   linux-gnu grnn          0.1.0     A1       3146
 4 3014840 3.1.0     x86_64 mingw32   Rcpp          0.11.2    A1       3146
 5  660087 3.1.0     i386   mingw32   xts           0.9-7     A1       3146
 6  522261 3.1.0     i386   mingw32   FNN           1.1       A1       3146
 7  522263 3.1.0     i386   mingw32   FNN           1.1       A1       3146
 8 1676627 3.1.0     x86_64 linux-gnu rgeos         0.3-5     A1       3146
 9 2118530 3.1.0     x86_64 linux-gnu spacetime     1.1-0     A1       3146
10 2217180 3.1.0     x86_64 mingw32   gstat         1.0-19    A1       3146
# … with 225,458 more rows

| You got it!
```
```r
| To illustrate the next major function in dplyr, let's take another subset of our original data. Use
| select() to grab 3 columns from cran -- ip_id, package, and size (in that order) -- and store the result in
| a new variable called cran3.
```
```r
> cran3 <- select(cran, ip_id, package, size)

| Keep up the great work!
```
```r
| Take a look at cran3 now.
```
```r
> cran3
# A tibble: 225,468 x 3
   ip_id package         size
   <int> <chr>          <int>
 1     1 htmltools      80589
 2     2 tseries       321767
 3     3 party         748063
 4     3 Hmisc         606104
 5     4 digest         79825
 6     3 randomForest   77681
 7     3 plyr          393754
 8     5 whisker        28216
 9     6 Rcpp            5928
10     7 hflights     2206029
# … with 225,458 more rows

| All that hard work is paying off!
```
```r
| It's common to create a new variable based on the value of one or more variables already in a dataset. The
| mutate() function does exactly this.
```
```r
| The size variable represents the download size in bytes, which are units of computer memory. These days,
| megabytes (MB) are a more common unit of measurement. One megabyte is equal to 2^20 bytes. That's 2 to the
| power of 20, which is approximately one million bytes!
```
```r
| We want to add a column called size_mb that contains the download size in megabytes. Here's the code to do
| it:
|
| mutate(cran3, size_mb = size / 2^20)
```
```r
> mutate(cran3, size_mb = size / 2^20)
# A tibble: 225,468 x 4
   ip_id package         size size_mb
   <int> <chr>          <int>   <dbl>
 1     1 htmltools      80589 0.0769
 2     2 tseries       321767 0.307  
 3     3 party         748063 0.713  
 4     3 Hmisc         606104 0.578  
 5     4 digest         79825 0.0761
 6     3 randomForest   77681 0.0741
 7     3 plyr          393754 0.376  
 8     5 whisker        28216 0.0269
 9     6 Rcpp            5928 0.00565
10     7 hflights     2206029 2.10   
# … with 225,458 more rows

| Keep up the great work!
```
```r
| An even larger unit of memory is a gigabyte (GB), which equals 2^10 megabytes. We might as well add another
| column for download size in gigabytes!
```
```r
| One very nice feature of mutate() is that you can use the value computed for your second column (size_mb)
| to create a third column, all in the same line of code. To see this in action, repeat the exact same
| command as above, except add a third argument creating a column that is named size_gb and equal to size_mb
| / 2^10.
```
```r
> mutate(cran3, size_mb = size / 2^20, size_gb = size_mb / 2 ^ 10)
# A tibble: 225,468 x 5
   ip_id package         size size_mb    size_gb
   <int> <chr>          <int>   <dbl>      <dbl>
 1     1 htmltools      80589 0.0769  0.0000751
 2     2 tseries       321767 0.307   0.000300  
 3     3 party         748063 0.713   0.000697  
 4     3 Hmisc         606104 0.578   0.000564  
 5     4 digest         79825 0.0761  0.0000743
 6     3 randomForest   77681 0.0741  0.0000723
 7     3 plyr          393754 0.376   0.000367  
 8     5 whisker        28216 0.0269  0.0000263
 9     6 Rcpp            5928 0.00565 0.00000552
10     7 hflights     2206029 2.10    0.00205   
# … with 225,458 more rows

| You are amazing!
```
```r
| Let's try one more for practice. Pretend we discovered a glitch in the system that provided the original
| values for the size variable. All of the values in cran3 are 1000 bytes less than they should be. Using
| cran3, create just one new column called correct_size that contains the correct size.
```
```r
> mutate(cran3, correct_size = size + 1000)
# A tibble: 225,468 x 4
   ip_id package         size correct_size
   <int> <chr>          <int>        <dbl>
 1     1 htmltools      80589        81589
 2     2 tseries       321767       322767
 3     3 party         748063       749063
 4     3 Hmisc         606104       607104
 5     4 digest         79825        80825
 6     3 randomForest   77681        78681
 7     3 plyr          393754       394754
 8     5 whisker        28216        29216
 9     6 Rcpp            5928         6928
10     7 hflights     2206029      2207029
# … with 225,458 more rows

| You are doing so well!
```
```r
| The last of the five core dplyr verbs, summarize(), collapses the dataset to a single row. Let's say we're
| interested in knowing the average download size. summarize(cran, avg_bytes = mean(size)) will yield the
| mean value of the size variable. Here we've chosen to label the result 'avg_bytes', but we could have named
| it anything. Give it a try.
```
```r
> summarize(cran, avg_bytes = mean(size))
# A tibble: 1 x 1
  avg_bytes
      <dbl>
1   844086.

| That's the answer I was looking for.
```
```r
| That's not particularly interesting. summarize() is most useful when working with data that has been
| grouped by the values of a particular variable.
```
```r
| We'll look at grouped data in the next lesson, but the idea is that summarize() can give you the requested
| value FOR EACH group in your dataset.
```
```r
| In this lesson, you learned how to manipulate data using dplyr's five main functions. In the next lesson,
| we'll look at how to take advantage of some other useful features of dplyr to make your life as a data
| analyst much easier.
```

## Grouping and Chaining with dplyr
```r
| Warning: This lesson makes use of the View() function. View() may not work properly in every programming
| environment. We highly recommend the use of RStudio for this lesson.
```
```r
| In the last lesson, you learned about the five main data manipulation 'verbs' in dplyr: select(), filter(),
| arrange(), mutate(), and summarize(). The last of these, summarize(), is most powerful when applied to
| grouped data.
```
```r
| The main idea behind grouping data is that you want to break up your dataset into groups of rows based on
| the values of one or more variables. The group_by() function is reponsible for doing this.
```
```r
| We'll continue where we left off with RStudio's CRAN download log from July 8, 2014, which contains
| information on roughly 225,000 R package downloads (http://cran-logs.rstudio.com/).
```
```r
| As with the last lesson, the dplyr package was automatically installed (if necessary) and loaded at the
| beginning of this lesson. Normally, this is something you would have to do on your own. Just to build the
| habit, type library(dplyr) now to load the package again.
```
```r
> library(dplyr)

| Keep working like that and you'll get there!
```
```r
| I've made the dataset available to you in a data frame called mydf. Put it in a 'data frame tbl' using the
| tbl_df() function and store the result in a object called cran. If you're not sure what I'm talking about,
| you should start with the previous lesson. Otherwise, practice makes perfect!
```
```r
> cran <- tbl_df(mydf)

| Nice work!
```
```r
| To avoid confusion and keep things running smoothly, let's remove the original dataframe from your
| workspace with rm("mydf").
```
```r
> rm("mydf")

| Excellent job!
```
```r
| Print cran to the console.
```
```r
> cran
# A tibble: 225,468 x 11
       X date       time        size r_version r_arch r_os      package      version country ip_id
   <int> <chr>      <chr>      <int> <chr>     <chr>  <chr>     <chr>        <chr>   <chr>   <int>
 1     1 2014-07-08 00:54:41   80589 3.1.0     x86_64 mingw32   htmltools    0.2.4   US          1
 2     2 2014-07-08 00:59:53  321767 3.1.0     x86_64 mingw32   tseries      0.10-32 US          2
 3     3 2014-07-08 00:47:13  748063 3.1.0     x86_64 linux-gnu party        1.0-15  US          3
 4     4 2014-07-08 00:48:05  606104 3.1.0     x86_64 linux-gnu Hmisc        3.14-4  US          3
 5     5 2014-07-08 00:46:50   79825 3.0.2     x86_64 linux-gnu digest       0.6.4   CA          4
 6     6 2014-07-08 00:48:04   77681 3.1.0     x86_64 linux-gnu randomForest 4.6-7   US          3
 7     7 2014-07-08 00:48:35  393754 3.1.0     x86_64 linux-gnu plyr         1.8.1   US          3
 8     8 2014-07-08 00:47:30   28216 3.0.2     x86_64 linux-gnu whisker      0.3-2   US          5
 9     9 2014-07-08 00:54:58    5928 NA        NA     NA        Rcpp         0.10.4  CN          6
10    10 2014-07-08 00:15:35 2206029 3.0.2     x86_64 linux-gnu hflights     0.1     US          7
# … with 225,458 more rows

| You are really on a roll!
```
```r
| Our first goal is to group the data by package name. Bring up the help file for group_by().
```
```r
> ?group_by

| Keep working like that and you'll get there!
```
```r
| Group cran by the package variable and store the result in a new object called by_package.
```
```r
> by_package <- group_by(cran, package)

| Excellent job!
```
```r
| Let's take a look at by_package. Print it to the console.
```
```r
> by_package
# A tibble: 225,468 x 11
# Groups:   package [6,023]
       X date       time        size r_version r_arch r_os      package      version country ip_id
   <int> <chr>      <chr>      <int> <chr>     <chr>  <chr>     <chr>        <chr>   <chr>   <int>
 1     1 2014-07-08 00:54:41   80589 3.1.0     x86_64 mingw32   htmltools    0.2.4   US          1
 2     2 2014-07-08 00:59:53  321767 3.1.0     x86_64 mingw32   tseries      0.10-32 US          2
 3     3 2014-07-08 00:47:13  748063 3.1.0     x86_64 linux-gnu party        1.0-15  US          3
 4     4 2014-07-08 00:48:05  606104 3.1.0     x86_64 linux-gnu Hmisc        3.14-4  US          3
 5     5 2014-07-08 00:46:50   79825 3.0.2     x86_64 linux-gnu digest       0.6.4   CA          4
 6     6 2014-07-08 00:48:04   77681 3.1.0     x86_64 linux-gnu randomForest 4.6-7   US          3
 7     7 2014-07-08 00:48:35  393754 3.1.0     x86_64 linux-gnu plyr         1.8.1   US          3
 8     8 2014-07-08 00:47:30   28216 3.0.2     x86_64 linux-gnu whisker      0.3-2   US          5
 9     9 2014-07-08 00:54:58    5928 NA        NA     NA        Rcpp         0.10.4  CN          6
10    10 2014-07-08 00:15:35 2206029 3.0.2     x86_64 linux-gnu hflights     0.1     US          7
# … with 225,458 more rows

| You got it right!
```
```r
| At the top of the output above, you'll see 'Groups: package', which tells us that this tbl has been grouped
| by the package variable. Everything else looks the same, but now any operation we apply to the grouped data
| will take place on a per package basis.
```
```r
| Recall that when we applied mean(size) to the original tbl_df via summarize(), it returned a single number
| -- the mean of all values in the size column. We may care about what that number is, but wouldn't it be so
| much more interesting to look at the mean download size for each unique package?
```
```r
| That's exactly what you'll get if you use summarize() to apply mean(size) to the grouped data in
| by_package. Give it a shot.
```
```r
> summarize(by_package, mean(size))
# A tibble: 6,023 x 2
   package     `mean(size)`
   <chr>              <dbl>
 1 A3                62195.
 2 abc             4826665
 3 abcdeFBA         455980.
 4 ABCExtremes       22904.
 5 ABCoptim          17807.
 6 ABCp2             30473.
 7 abctools        2589394
 8 abd              453631.
 9 abf2              35693.
10 abind             32939.
# … with 6,013 more rows

| All that practice is paying off!
```
```r
| Instead of returning a single value, summarize() now returns the mean size for EACH package in our dataset.
```
```r
| Let's take it a step further. I just opened an R script for you that contains a partially constructed call
| to summarize(). Follow the instructions in the script comments.
|
| When you are ready to move on, save the script and type submit(), or type reset() to reset the script to
| its original state.
```
```r
> submit()

| Sourcing your script...

| You are doing so well!
```
```r
| Print the resulting tbl, pack_sum, to the console to examine its contents.
```
```r
> pack_sum
# A tibble: 6,023 x 5
   package     count unique countries avg_bytes
   <chr>       <int>  <int>     <int>     <dbl>
 1 A3             25     24        10    62195.
 2 abc            29     25        16  4826665
 3 abcdeFBA       15     15         9   455980.
 4 ABCExtremes    18     17         9    22904.
 5 ABCoptim       16     15         9    17807.
 6 ABCp2          18     17        10    30473.
 7 abctools       19     19        11  2589394
 8 abd            17     16        10   453631.
 9 abf2           13     13         9    35693.
10 abind         396    365        50    32939.
# … with 6,013 more rows

| You got it right!
```
```r
| The 'count' column, created with n(), contains the total number of rows (i.e. downloads) for each package.
| The 'unique' column, created with n_distinct(ip_id), gives the total number of unique downloads for each
| package, as measured by the number of distinct ip_id's. The 'countries' column, created with
| n_distinct(country), provides the number of countries in which each package was downloaded. And finally,
| the 'avg_bytes' column, created with mean(size), contains the mean download size (in bytes) for each
| package.
```
```r
| It's important that you understand how each column of pack_sum was created and what it means. Now that
| we've summarized the data by individual packages, let's play around with it some more to see what we can
| learn.
```
```r
| Naturally, we'd like to know which packages were most popular on the day these data were collected (July 8,
| 2014). Let's start by isolating the top 1% of packages, based on the total number of downloads as measured
| by the 'count' column.
```
```r
| We need to know the value of 'count' that splits the data into the top 1% and bottom 99% of packages based
| on total downloads. In statistics, this is called the 0.99, or 99%, sample quantile. Use
| quantile(pack_sum$count, probs = 0.99) to determine this number.
```
```r
> quantile(pack_sum$count, probs = 0.99)
   99%
679.56

| You are really on a roll!
```
```r
| Now we can isolate only those packages which had more than 679 total downloads. Use filter() to select all
| rows from pack_sum for which 'count' is strictly greater (>) than 679. Store the result in a new object
| called top_counts.
```
```r
> top_counts <- filter(pack_sum, count > 679)

| Your dedication is inspiring!
```
```r
| Let's take a look at top_counts. Print it to the console.
```
```r
> top_counts
# A tibble: 61 x 5
   package    count unique countries avg_bytes
   <chr>      <int>  <int>     <int>     <dbl>
 1 bitops      1549   1408        76    28715.
 2 car         1008    837        64  1229122.
 3 caTools      812    699        64   176589.
 4 colorspace  1683   1433        80   357411.
 5 data.table   680    564        59  1252721.
 6 DBI         2599    492        48   206933.
 7 devtools     769    560        55   212933.
 8 dichromat   1486   1257        74   134732.
 9 digest      2210   1894        83   120549.
10 doSNOW       740     75        24     8364.
# … with 51 more rows

| Excellent work!
```
```r
| There are only 61 packages in our top 1%, so we'd like to see all of them. Since dplyr only shows us the
| first 10 rows, we can use the View() function to see more.
```
```r
| View all 61 rows with View(top_counts). Note that the 'V' in View() is capitalized.
```
```r
> View(top_counts)

| You nailed it! Good job!
```
```r
| arrange() the rows of top_counts based on the 'count' column and assign the result to a new object called
| top_counts_sorted. We want the packages with the highest number of downloads at the top, which means we
| want 'count' to be in descending order. If you need help, check out ?arrange and/or ?desc.
```
```r
> top_counts_sorted <- arrange(top_counts, desc(count))

| Excellent work!
```
```r
| Now use View() again to see all 61 rows of top_counts_sorted.
```
```r
> View(top_counts_sorted)

| You got it right!
```
```r
| If we use total number of downloads as our metric for popularity, then the above output shows us the most
| popular packages downloaded from the RStudio CRAN mirror on July 8, 2014. Not surprisingly, ggplot2 leads
| the pack with 4602 downloads, followed by Rcpp, plyr, rJava, ....
```
```r
| ...And if you keep on going, you'll see swirl at number 43, with 820 total downloads. Sweet!
```
```r
| Perhaps we're more interested in the number of *unique* downloads on this particular day. In other words,
| if a package is downloaded ten times in one day from the same computer, we may wish to count that as only
| one download. That's what the 'unique' column will tell us.
```
```r
| Like we did with 'count', let's find the 0.99, or 99%, quantile for the 'unique' variable with
| quantile(pack_sum$unique, probs = 0.99).
```
```r
> quantile(pack_sum$unique, probs = 0.99)
99%
465

| Perseverance, that's the answer.
```
```r
| Apply filter() to pack_sum to select all rows corresponding to values of 'unique' that are strictly greater
| than 465. Assign the result to a object called top_unique.
```
```r
> top_unique <- filter(pack_sum, unique > 465)

| You are quite good my friend!
```
```r
| Let's View() our top contenders!
```
```r
> View(top_unique)

| You're the best!
```
```r
| Now arrange() top_unique by the 'unique' column, in descending order, to see which packages were downloaded
| from the greatest number of unique IP addresses. Assign the result to top_unique_sorted.
```
```r
> top_unique_sorted <- arrange(top_unique, desc(unique))

| Perseverance, that's the answer.
```
```r
| View() the sorted data.
```
```r
> View(top_unique_sorted)

| Keep up the great work!
```
```r
| Now Rcpp is in the lead, followed by stringr, digest, plyr, and ggplot2. swirl moved up a few spaces to
| number 40, with 698 unique downloads. Nice!
```
```r
| Our final metric of popularity is the number of distinct countries from which each package was downloaded.
| We'll approach this one a little differently to introduce you to a method called 'chaining' (or 'piping').
```
```r
| Chaining allows you to string together multiple function calls in a way that is compact and readable, while
| still accomplishing the desired result. To make it more concrete, let's compute our last popularity metric
| from scratch, starting with our original data.
```
```r
| I've opened up a script that contains code similar to what you've seen so far. Don't change anything. Just
| study it for a minute, make sure you understand everything that's there, then submit() when you are ready
| to move on.
```
```r
> submit()

| Sourcing your script...

# A tibble: 46 x 5
   package      count unique countries avg_bytes
   <chr>        <int>  <int>     <int>     <dbl>
 1 Rcpp          3195   2044        84  2512100.
 2 digest        2210   1894        83   120549.
 3 stringr       2267   1948        82    65277.
 4 plyr          2908   1754        81   799123.
 5 ggplot2       4602   1680        81  2427716.
 6 colorspace    1683   1433        80   357411.
 7 RColorBrewer  1890   1584        79    22764.
 8 scales        1726   1408        77   126819.
 9 bitops        1549   1408        76    28715.
10 reshape2      2032   1652        76   330128.
# … with 36 more rows

| That's correct!
```
```r
| It's worth noting that we sorted primarily by country, but used avg_bytes (in ascending order) as a tie
| breaker. This means that if two packages were downloaded from the same number of countries, the package
| with a smaller average download size received a higher ranking.
```
```r
| We'd like to accomplish the same result as the last script, but avoid saving our intermediate results. This
| requires embedding function calls within one another.
```
```r
| That's exactly what we've done in this script. The result is equivalent, but the code is much less readable
| and some of the arguments are far away from the function to which they belong. Again, just try to
| understand what is going on here, then submit() when you are ready to see a better solution.
```
```r
> submit()

| Sourcing your script...

# A tibble: 46 x 5
   package      count unique countries avg_bytes
   <chr>        <int>  <int>     <int>     <dbl>
 1 Rcpp          3195   2044        84  2512100.
 2 digest        2210   1894        83   120549.
 3 stringr       2267   1948        82    65277.
 4 plyr          2908   1754        81   799123.
 5 ggplot2       4602   1680        81  2427716.
 6 colorspace    1683   1433        80   357411.
 7 RColorBrewer  1890   1584        79    22764.
 8 scales        1726   1408        77   126819.
 9 bitops        1549   1408        76    28715.
10 reshape2      2032   1652        76   330128.
# … with 36 more rows

| All that hard work is paying off!
```
```r
| In this script, we've used a special chaining operator, %>%, which was originally introduced in the
| magrittr R package and has now become a key component of dplyr. You can pull up the related documentation
| with ?chain. The benefit of %>% is that it allows us to chain the function calls in a linear fashion. The
| code to the right of %>% operates on the result from the code to the left of %>%.
|
| Once again, just try to understand the code, then type submit() to continue.
```
```r
> submit()

| Sourcing your script...

# A tibble: 46 x 5
   package      count unique countries avg_bytes
   <chr>        <int>  <int>     <int>     <dbl>
 1 Rcpp          3195   2044        84  2512100.
 2 digest        2210   1894        83   120549.
 3 stringr       2267   1948        82    65277.
 4 plyr          2908   1754        81   799123.
 5 ggplot2       4602   1680        81  2427716.
 6 colorspace    1683   1433        80   357411.
 7 RColorBrewer  1890   1584        79    22764.
 8 scales        1726   1408        77   126819.
 9 bitops        1549   1408        76    28715.
10 reshape2      2032   1652        76   330128.
# … with 36 more rows

| You are doing so well!
```
```r
| So, the results of the last three scripts are all identical. But, the third script provides a convenient
| and concise alternative to the more traditional method that we've taken previously, which involves saving
| results as we go along.
```
```r
| Once again, let's View() the full data, which has been stored in result3.
```
```r
> View(result3)

| You nailed it! Good job!
```
```r
| It looks like Rcpp is on top with downloads from 84 different countries, followed by digest, stringr, plyr,
| and ggplot2. swirl jumped up the rankings again, this time to 27th.
```
```r
| To help drive the point home, let's work through a few more examples of chaining.
```
```r
| Let's build a chain of dplyr commands one step at a time, starting with the script I just opened for you.
```
```r
> submit()

| Sourcing your script...

# A tibble: 225,468 x 4
   ip_id country package         size
   <int> <chr>   <chr>          <int>
 1     1 US      htmltools      80589
 2     2 US      tseries       321767
 3     3 US      party         748063
 4     3 US      Hmisc         606104
 5     4 CA      digest         79825
 6     3 US      randomForest   77681
 7     3 US      plyr          393754
 8     5 US      whisker        28216
 9     6 CN      Rcpp            5928
10     7 US      hflights     2206029
# … with 225,458 more rows

| Perseverance, that's the answer.
```
```r
| Let's add to the chain.

> submit()

| Sourcing your script...

# A tibble: 142,021 x 5
   ip_id country package        size size_mb
   <int> <chr>   <chr>         <int>   <dbl>
 1     1 US      htmltools     80589 0.0769
 2     2 US      tseries      321767 0.307  
 3     4 CA      digest        79825 0.0761
 4     3 US      randomForest  77681 0.0741
 5     3 US      plyr         393754 0.376  
 6     5 US      whisker       28216 0.0269
 7     6 CN      Rcpp           5928 0.00565
 8    13 DE      ipred        186685 0.178  
 9    14 US      mnormt        36204 0.0345
10    16 US      iterators    289972 0.277  
# … with 142,011 more rows

| Your dedication is inspiring!
| And finish it off.
```
```r
> submit()

| Sourcing your script...

# A tibble: 142,021 x 5
   ip_id country package                 size size_mb
   <int> <chr>   <chr>                  <int>   <dbl>
 1 11034 DE      phia                  524232   0.500
 2  9643 US      tis                   524152   0.500
 3  1542 IN      RcppSMC               524060   0.500
 4 12354 US      lessR                 523916   0.500
 5 12072 US      colorspace            523880   0.500
 6  2514 KR      depmixS4              523863   0.500
 7  1111 US      depmixS4              523858   0.500
 8  8865 CR      depmixS4              523858   0.500
 9  5908 CN      RcmdrPlugin.KMggplot2 523852   0.500
10 12354 US      RcmdrPlugin.KMggplot2 523852   0.500
# … with 142,011 more rows

| That's the answer I was looking for.
```
```r
| In this lesson, you learned about grouping and chaining using dplyr. You combined some of the things you
| learned in the previous lesson with these more advanced ideas to produce concise, readable, and highly
| effective code. Welcome to the wonderful world of dplyr!
```

## Tidying Data with tidyr
```r
| In this lesson, you'll learn how to tidy your data with the tidyr package.
```
```r
| Parts of this lesson will require the use of dplyr. If you don't have a basic knowledge of dplyr, you
| should exit this lesson and begin with the dplyr lessons from earlier in the course.
```
```r
| tidyr was automatically installed (if necessary) and loaded when you started this lesson. Just to build the
| habit, (re)load the package with library(tidyr).
```
```r
> library(tidyr)

| That's a job well done!
```
```r
| The author of tidyr, Hadley Wickham, discusses his philosophy of tidy data in his 'Tidy Data' paper:
|
| http://vita.had.co.nz/papers/tidy-data.pdf
|
| This paper should be required reading for anyone who works with data, but it's not required in order to
| complete this lesson.
```
```r
| Tidy data is formatted in a standard way that facilitates exploration and analysis and works seamlessly
| with other tidy data tools. Specifically, tidy data satisfies three conditions:
|
| 1) Each variable forms a column
|
| 2) Each observation forms a row
|
| 3) Each type of observational unit forms a table
```
```r
| Any dataset that doesn't satisfy these conditions is considered 'messy' data. Therefore, all of the
| following are characteristics of messy data, EXCEPT...

1: Multiple types of observational units are stored in the same table
2: Multiple variables are stored in one column
3: Column headers are values, not variable names
4: A single observational unit is stored in multiple tables
5: Every column contains a different variable
6: Variables are stored in both rows and columns

Selection: 5

| All that practice is paying off!
```
```r
| The incorrect answers to the previous question are the most common symptoms of messy data. Let's work
| through a simple example of each of these five cases, then tidy some real data.
```
```r
| The first problem is when you have column headers that are values, not variable names. I've created a
| simple dataset called 'students' that demonstrates this scenario. Type students to take a look.
```
```r
> students
  grade male female
1     A    5      3
2     B    4      1
3     C    8      6
4     D    4      5
5     E    5      5

| Nice work!
```
```r
| The first column represents each of five possible grades that students could receive for a particular
| class. The second and third columns give the number of male and female students, respectively, that
| received each grade.
```
```r
| This dataset actually has three variables: grade, sex, and count. The first variable, grade, is already a
| column, so that should remain as it is. The second variable, sex, is captured by the second and third
| column headings. The third variable, count, is the number of students for each combination of grade and
| sex.
```
```r
| To tidy the students data, we need to have one column for each of these three variables. We'll use the
| gather() function from tidyr to accomplish this. Pull up the documentation for this function with ?gather.
```
```r
> ?gather

| Your dedication is inspiring!
```
```r
| Using the help file as a guide, call gather() with the following arguments (in order): students, sex,
| count, -grade. Note the minus sign before grade, which says we want to gather all columns EXCEPT grade.
```
```r
> gather(students, sex, count, -grade)
   grade    sex count
1      A   male     5
2      B   male     4
3      C   male     8
4      D   male     4
5      E   male     5
6      A female     3
7      B female     1
8      C female     6
9      D female     5
10     E female     5

| You got it!
```
```r
| Each row of the data now represents exactly one observation, characterized by a unique combination of the
| grade and sex variables. Each of our variables (grade, sex, and count) occupies exactly one column. That's
| tidy data!
```
```r
| It's important to understand what each argument to gather() means. The data argument, students, gives the
| name of the original dataset. The key and value arguments -- sex and count, respectively -- give the column
| names for our tidy dataset. The final argument, -grade, says that we want to gather all columns EXCEPT the
| grade column (since grade is already a proper column variable.)
```
```r
| The second messy data case we'll look at is when multiple variables are stored in one column. Type
| students2 to see an example of this.
```
```r
> students2
  grade male_1 female_1 male_2 female_2
1     A      7        0      5        8
2     B      4        0      5        8
3     C      7        4      5        6
4     D      8        2      8        1
5     E      8        4      1        0

| You are doing so well!
```
```r
| This dataset is similar to the first, except now there are two separate classes, 1 and 2, and we have total
| counts for each sex within each class. students2 suffers from the same messy data problem of having column
| headers that are values (male_1, female_1, etc.) and not variable names (sex, class, and count).
```
```r
| However, it also has multiple variables stored in each column (sex and class), which is another common
| symptom of messy data. Tidying this dataset will be a two step process.
```
```r
| Let's start by using gather() to stack the columns of students2, like we just did with students. This time,
| name the 'key' column sex_class and the 'value' column count. Save the result to a new variable called res.
| Consult ?gather again if you need help.
```
```r
> res <- gather(students2, sex_class, count, -grade)

| Excellent job!
```
```r
| Print res to the console to see what we accomplished.
```
```r
> res
   grade sex_class count
1      A    male_1     7
2      B    male_1     4
3      C    male_1     7
4      D    male_1     8
5      E    male_1     8
6      A  female_1     0
7      B  female_1     0
8      C  female_1     4
9      D  female_1     2
10     E  female_1     4
11     A    male_2     5
12     B    male_2     5
13     C    male_2     5
14     D    male_2     8
15     E    male_2     1
16     A  female_2     8
17     B  female_2     8
18     C  female_2     6
19     D  female_2     1
20     E  female_2     0

| You are quite good my friend!
```
```r
| That got us half way to tidy data, but we still have two different variables, sex and class, stored
| together in the sex_class column. tidyr offers a convenient separate() function for the purpose of
| separating one column into multiple columns. Pull up the help file for separate() now.
```
```r
> ?separate

| All that hard work is paying off!
```
```r
| Call separate() on res to split the sex_class column into sex and class. You only need to specify the first
| three arguments: data = res, col = sex_class, into = c("sex", "class"). You don't have to provide the
| argument names as long as they are in the correct order.
```
```r
> separate(res, sex_class, c('sex', 'class'))
   grade    sex class count
1      A   male     1     7
2      B   male     1     4
3      C   male     1     7
4      D   male     1     8
5      E   male     1     8
6      A female     1     0
7      B female     1     0
8      C female     1     4
9      D female     1     2
10     E female     1     4
11     A   male     2     5
12     B   male     2     5
13     C   male     2     5
14     D   male     2     8
15     E   male     2     1
16     A female     2     8
17     B female     2     8
18     C female     2     6
19     D female     2     1
20     E female     2     0

| Your dedication is inspiring!
```
```r
| Conveniently, separate() was able to figure out on its own how to separate the sex_class column. Unless you
| request otherwise with the 'sep' argument, it splits on non-alphanumeric values. In other words, it assumes
| that the values are separated by something other than a letter or number (in this case, an underscore.)
```
```r
| Tidying students2 required both gather() and separate(), causing us to save an intermediate result (res).
| However, just like with dplyr, you can use the %>% operator to chain multiple function calls together.
```
```r
| I've opened an R script for you to give this a try. Follow the directions in the script, then save the
| script and type submit() at the prompt when you are ready. If you get stuck and want to start over, you can
| type reset() to reset the script to its original state.
```
```r
> submit()

| Sourcing your script...

   grade    sex class count
1      A   male     1     7
2      B   male     1     4
3      C   male     1     7
4      D   male     1     8
5      E   male     1     8
6      A female     1     0
7      B female     1     0
8      C female     1     4
9      D female     1     2
10     E female     1     4
11     A   male     2     5
12     B   male     2     5
13     C   male     2     5
14     D   male     2     8
15     E   male     2     1
16     A female     2     8
17     B female     2     8
18     C female     2     6
19     D female     2     1
20     E female     2     0

| That's a job well done!
```
```r
| A third symptom of messy data is when variables are stored in both rows and columns. students3 provides an
| example of this. Print students3 to the console.
```
```r
> students3
    name    test class1 class2 class3 class4 class5
1  Sally midterm      A   <NA>      B   <NA>   <NA>
2  Sally   final      C   <NA>      C   <NA>   <NA>
3   Jeff midterm   <NA>      D   <NA>      A   <NA>
4   Jeff   final   <NA>      E   <NA>      C   <NA>
5  Roger midterm   <NA>      C   <NA>   <NA>      B
6  Roger   final   <NA>      A   <NA>   <NA>      A
7  Karen midterm   <NA>   <NA>      C      A   <NA>
8  Karen   final   <NA>   <NA>      C      A   <NA>
9  Brian midterm      B   <NA>   <NA>   <NA>      A
10 Brian   final      B   <NA>   <NA>   <NA>      C

| Perseverance, that's the answer.
```
```r
| In students3, we have midterm and final exam grades for five students, each of whom were enrolled in
| exactly two of five possible classes.
```
```r
| The first variable, name, is already a column and should remain as it is. The headers of the last five
| columns, class1 through class5, are all different values of what should be a class variable. The values in
| the test column, midterm and final, should each be its own variable containing the respective grades for
| each student.
```
```r
| This will require multiple steps, which we will build up gradually using %>%. Edit the R script, save it,
| then type submit() when you are ready. Type reset() to reset the script to its original state.
```
```r
> submit()

| Sourcing your script...

    name    test  class grade
1  Sally midterm class1     A
2  Sally   final class1     C
9  Brian midterm class1     B
10 Brian   final class1     B
13  Jeff midterm class2     D
14  Jeff   final class2     E
15 Roger midterm class2     C
16 Roger   final class2     A
21 Sally midterm class3     B
22 Sally   final class3     C
27 Karen midterm class3     C
28 Karen   final class3     C
33  Jeff midterm class4     A
34  Jeff   final class4     C
37 Karen midterm class4     A
38 Karen   final class4     A
45 Roger midterm class5     B
46 Roger   final class5     A
49 Brian midterm class5     A
50 Brian   final class5     C

| You nailed it! Good job!
```
```r
| The next step will require the use of spread(). Pull up the documentation for spread() now.
```
```r
> ?spread

| That's a job well done!
```
```r
| Edit the R script, then save it and type submit() when you are ready. Type reset() to reset the script to
| its original state.
```
```r
> submit()

| Sourcing your script...

    name  class final midterm
1  Brian class1     B       B
2  Brian class5     C       A
3   Jeff class2     E       D
4   Jeff class4     C       A
5  Karen class3     C       C
6  Karen class4     A       A
7  Roger class2     A       C
8  Roger class5     A       B
9  Sally class1     C       A
10 Sally class3     C       B

| You are doing so well!
```
```r
| readr is required for certain data manipulations, such as `parse_number(), which will be used in the next
| question.  Let's, (re)load the package with library(readr).
```
```r
> library(readr)

| Keep working like that and you'll get there!
```
```r
| Lastly, we want the values in the class column to simply be 1, 2, ..., 5 and not class1, class2, ...,
| class5. We can use the parse_number() function from readr to accomplish this. To see how it works, try
| parse_number("class5").
```
```r
> parse_number("class5")
[1] 5

| You are quite good my friend!
```
```r
| Now, the final step. Edit the R script, then save it and type submit() when you are ready. Type reset() to
| reset the script to its original state.
```
```r
> submit()

| Sourcing your script...

    name class final midterm
1  Brian     1     B       B
2  Brian     5     C       A
3   Jeff     2     E       D
4   Jeff     4     C       A
5  Karen     3     C       C
6  Karen     4     A       A
7  Roger     2     A       C
8  Roger     5     A       B
9  Sally     1     C       A
10 Sally     3     C       B

| Nice work!
```
```r
| The fourth messy data problem we'll look at occurs when multiple observational units are stored in the same
| table. students4 presents an example of this. Take a look at the data now.
```
```r
> students4
    id  name sex class midterm final
1  168 Brian   F     1       B     B
2  168 Brian   F     5       A     C
3  588 Sally   M     1       A     C
4  588 Sally   M     3       B     C
5  710  Jeff   M     2       D     E
6  710  Jeff   M     4       A     C
7  731 Roger   F     2       C     A
8  731 Roger   F     5       B     A
9  908 Karen   M     3       C     C
10 908 Karen   M     4       A     A

| That's the answer I was looking for.
```
```r
| students4 is almost the same as our tidy version of students3. The only difference is that students4
| provides a unique id for each student, as well as his or her sex (M = male; F = female).
```
```r
| At first glance, there doesn't seem to be much of a problem with students4. All columns are variables and
| all rows are observations. However, notice that each id, name, and sex is repeated twice, which seems quite
| redundant. This is a hint that our data contains multiple observational units in a single table.
```
```r
| Our solution will be to break students4 into two separate tables -- one containing basic student
| information (id, name, and sex) and the other containing grades (id, class, midterm, final).
|
| Edit the R script, save it, then type submit() when you are ready. Type reset() to reset the script to its
| original state.
```
```r
> submit()

| Sourcing your script...

    id  name sex
1  168 Brian   F
2  168 Brian   F
3  588 Sally   M
4  588 Sally   M
5  710  Jeff   M
6  710  Jeff   M
7  731 Roger   F
8  731 Roger   F
9  908 Karen   M
10 908 Karen   M

| You're the best!
```
```r
| Notice anything strange about student_info? It contains five duplicate rows! See the script for directions
| on how to fix this. Save the script and type submit() when you are ready, or type reset() to reset the
| script to its original state.
```
```r
> submit()

| Sourcing your script...

   id  name sex
1 168 Brian   F
3 588 Sally   M
5 710  Jeff   M
7 731 Roger   F
9 908 Karen   M

| Great job!
```
```r
| Now, using the script I just opened for you, create a second table called gradebook using the id, class,
| midterm, and final columns (in that order).
|
| Edit the R script, save it, then type submit() when you are ready. Type reset() to reset the script to its
| original state.
```
```r
> submit()

| Sourcing your script...

    id class midterm final
1  168     1       B     B
2  168     5       A     C
3  588     1       A     C
4  588     3       B     C
5  710     2       D     E
6  710     4       A     C
7  731     2       C     A
8  731     5       B     A
9  908     3       C     C
10 908     4       A     A

| All that hard work is paying off!
```
```r
| It's important to note that we left the id column in both tables. In the world of relational databases,
| 'id' is called our 'primary key' since it allows us to connect each student listed in student_info with
| their grades listed in gradebook. Without a unique identifier, we might not know how the tables are
| related. (In this case, we could have also used the name variable, since each student happens to have a
| unique name.)
```
```r
| The fifth and final messy data scenario that we'll address is when a single observational unit is stored in
| multiple tables. It's the opposite of the fourth problem.
```
```r
| To illustrate this, we've created two datasets, passed and failed. Take a look at passed now.
```
```r
> passed
   name class final
1 Brian     1     B
2 Roger     2     A
3 Roger     5     A
4 Karen     4     A

| You're the best!
```
```r
| Now view the contents of failed.
```
```r
> failed
   name class final
1 Brian     5     C
2 Sally     1     C
3 Sally     3     C
4  Jeff     2     E
5  Jeff     4     C
6 Karen     3     C

| You nailed it! Good job!
```
```r
| Teachers decided to only take into consideration final exam grades in determining whether students passed
| or failed each class. As you may have inferred from the data, students passed a class if they received a
| final exam grade of A or B and failed otherwise.
```
```r
| The name of each dataset actually represents the value of a new variable that we will call 'status'. Before
| joining the two tables together, we'll add a new column to each containing this information so that it's
| not lost when we put everything together.
```
```r
| Use dplyr's mutate() to add a new column to the passed table. The column should be called status and the
| value, "passed" (a character string), should be the same for all students. 'Overwrite' the current version
| of passed with the new one.
```
```r
> passed <- mutate(passed, status = 'passed')

| You got it right!
```
```r
| Now, do the same for the failed table, except the status column should have the value "failed" for all
| students.
```
```r
> failed <- mutate(failed, status = 'failed')

| Great job!
```
```r
| Now, pass as arguments the passed and failed tables (in order) to the dplyr function bind_rows(), which
| will join them together into a single unit. Check ?bind_rows if you need help.
|
| Note: bind_rows() is only available in dplyr 0.4.0 or later. If you have an older version of dplyr, please
| quit the lesson, update dplyr, then restart the lesson where you left off. If you're not sure what version
| of dplyr you have, type packageVersion('dplyr').
```
```r
> bind_rows(passed, failed)
    name class final status
1  Brian     1     B passed
2  Roger     2     A passed
3  Roger     5     A passed
4  Karen     4     A passed
5  Brian     5     C failed
6  Sally     1     C failed
7  Sally     3     C failed
8   Jeff     2     E failed
9   Jeff     4     C failed
10 Karen     3     C failed

| That's the answer I was looking for.
```
```r
| Of course, we could arrange the rows however we wish at this point, but the important thing is that each
| row is an observation, each column is a variable, and the table contains a single observational unit. Thus,
| the data are tidy.
```
```r
| We've covered a lot in this lesson. Let's bring everything together and tidy a real dataset.
```
```r
| The SAT is a popular college-readiness exam in the United States that consists of three sections: critical
| reading, mathematics, and writing. Students can earn up to 800 points on each section. This dataset
| presents the total number of students, for each combination of exam section and sex, within each of six
| score ranges. It comes from the 'Total Group Report 2013', which can be found here:
|
| http://research.collegeboard.org/programs/sat/data/cb-seniors-2013
```
```r
| I've created a variable called 'sat' in your workspace, which contains data on all college-bound seniors
| who took the SAT exam in 2013. Print the dataset now.
```
```r
> sat
# A tibble: 6 x 10
  score_range read_male read_fem read_total math_male math_fem math_total write_male write_fem write_total
  <chr>           <int>    <int>      <int>     <int>    <int>      <int>      <int>     <int>       <int>
1 700-800         40151    38898      79049     74461    46040     120501      31574     39101       70675
2 600-690        121950   126084     248034    162564   133954     296518     100963    125368      226331
3 500-590        227141   259553     486694    233141   257678     490819     202326    247239      449565
4 400-490        242554   296793     539347    204670   288696     493366     262623    302933      565556
5 300-390        113568   133473     247041     82468   131025     213493     146106    144381      290487
6 200-290         30728    29154      59882     18788    26562      45350      32500     24933       57433

| You got it!
```
```r
| As we've done before, we'll build up a series of chained commands, using functions from both tidyr and
| dplyr. Edit the R script, save it, then type submit() when you are ready. Type reset() to reset the script
| to its original state.
```
```r
> submit()

| Sourcing your script...

# A tibble: 36 x 4
   score_range part  sex    count
   <chr>       <chr> <chr>  <int>
 1 700-800     read  male   40151
 2 600-690     read  male  121950
 3 500-590     read  male  227141
 4 400-490     read  male  242554
 5 300-390     read  male  113568
 6 200-290     read  male   30728
 7 700-800     read  fem    38898
 8 600-690     read  fem   126084
 9 500-590     read  fem   259553
10 400-490     read  fem   296793
# … with 26 more rows

| Great job!
```
```r
| Finish off the job by following the directions in the script. Save the script and type submit() when you
| are ready, or type reset() to reset the script to its original state.
```
```r
> submit()

| Sourcing your script...

# A tibble: 36 x 6
# Groups:   part, sex [6]
   score_range part  sex    count  total   prop
   <chr>       <chr> <chr>  <int>  <int>  <dbl>
 1 700-800     read  male   40151 776092 0.0517
 2 600-690     read  male  121950 776092 0.157
 3 500-590     read  male  227141 776092 0.293
 4 400-490     read  male  242554 776092 0.313
 5 300-390     read  male  113568 776092 0.146
 6 200-290     read  male   30728 776092 0.0396
 7 700-800     read  fem    38898 883955 0.0440
 8 600-690     read  fem   126084 883955 0.143
 9 500-590     read  fem   259553 883955 0.294
10 400-490     read  fem   296793 883955 0.336
# … with 26 more rows

| You are doing so well!
```
```r
| In this lesson, you learned how to tidy data with tidyr and dplyr. These tools will help you spend less
| time and energy getting your data ready to analyze and more time actually analyzing it.
```

## Dates and Times with lubridate
```r
| In this lesson, we'll explore the lubridate R package, by Garrett Grolemund and Hadley Wickham. According
| to the package authors, "lubridate has a consistent, memorable syntax, that makes working with dates fun
| instead of frustrating." If you've ever worked with dates in R, that statement probably has your attention.
```
```r
| Unfortunately, due to different date and time representations, this lesson is only guaranteed to work with
| an "en_US.UTF-8" locale. To view your locale, type Sys.getlocale("LC_TIME").
```
```r
> Sys.getlocale("LC_TIME")
[1] "en_US.UTF-8"

| Excellent job!
```
```r
| If the output above is not "en_US.UTF-8", this lesson is not guaranteed to work correctly. Of course, you
| are welcome to try it anyway. We apologize for this inconvenience.
```
```r
| lubridate was automatically installed (if necessary) and loaded upon starting this lesson. To build the
| habit, we'll go ahead and (re)load the package now. Type library(lubridate) to do so.
```
```r
> library(lubridate)

| That's a job well done!
```
```r
| lubridate contains many useful functions. We'll only be covering the basics here. Type help(package =
| lubridate) to bring up an overview of the package, including the package DESCRIPTION, a list of available
| functions, and a link to the official package vignette.
```
```r
> help(package = lubridate)

| Nice work!
```
```r
| Let's get going!
```
```r
| The today() function returns today's date. Give it a try, storing the result in a new variable called
| this_day.
```
```r
> this_day <- today()

| Great job!
```
```r
| Print the contents of this_day to the console.
```
```r
> this_day
[1] "2019-10-26"

| Nice work!
```
```r
| There are three components to this date. In order, they are year, month, and day. We can extract any of
| these components using the year(), month(), or day() function, respectively. Try any of those on this_day
| now.
```
```r
> year(this_day)
[1] 2019

| You are amazing!
```
```r
| We can also get the day of the week from this_day using the wday() function. It will be represented as a
| number, such that 1 = Sunday, 2 = Monday, 3 = Tuesday, etc. Give it a shot.
```
```r
> wday(this_day)
[1] 7

| You're the best!
```
```r
| Now try the same thing again, except this time add a second argument, label = TRUE, to display the *name*
| of the weekday (represented as an ordered factor).
```
```r
> wday(this_day, label = TRUE)
[1] Sat
Levels: Sun < Mon < Tue < Wed < Thu < Fri < Sat

| You're the best!
```
```r
| In addition to handling dates, lubridate is great for working with date and time combinations, referred to
| as date-times. The now() function returns the date-time representing this exact moment in time. Give it a
| try and store the result in a variable called this_moment.
```
```r
> this_moment <- now()

| Excellent work!
```
```r
| View the contents of this_moment.
```
```r
> this_moment
[1] "2019-10-26 11:30:34 CEST"

| Great job!
```
```r
| Just like with dates, we can extract the year, month, day, or day of week. However, we can also use hour(),
| minute(), and second() to extract specific time information. Try any of these three new functions now to
| extract one piece of time information from this_moment.
```
```r
> second(this_moment)
[1] 34.46107

| You nailed it! Good job!
```
```r
| today() and now() provide neatly formatted date-time information. When working with dates and times 'in the
| wild', this won't always (and perhaps rarely will) be the case.
```
```r
| Fortunately, lubridate offers a variety of functions for parsing date-times. These functions take the form
| of ymd(), dmy(), hms(), ymd_hms(), etc., where each letter in the name of the function stands for the
| location of years (y), months (m), days (d), hours (h), minutes (m), and/or seconds (s) in the date-time
| being read in.
```
```r
| To see how these functions work, try ymd("1989-05-17"). You must surround the date with quotes. Store the
| result in a variable called my_date.
```
```r
> my_date <- ymd("1989-05-17")

| You got it!
```
```r
| Now take a look at my_date.
```
```r
> my_date
[1] "1989-05-17"

| That's the answer I was looking for.
```
```r
| It looks almost the same, except for the addition of a time zone, which we'll discuss later in the lesson.
| Below the surface, there's another important change that takes place when lubridate parses a date. Type
| class(my_date) to see what that is.
```
```r
> class(my_date)
[1] "Date"

| You are quite good my friend!
```
```r
| So ymd() took a character string as input and returned an object of class POSIXct. It's not necessary that
| you understand what POSIXct is, but just know that it is one way that R stores date-time information
| internally.
```
```r
| "1989-05-17" is a fairly standard format, but lubridate is 'smart' enough to figure out many different
| date-time formats. Use ymd() to parse "1989 May 17". Don't forget to put quotes around the date!
```
```r
> ymd("1989 May 17")
[1] "1989-05-17"

| You're the best!
```
```r
| Despite being formatted differently, the last two dates had the year first, then the month, then the day.
| Hence, we used ymd() to parse them. What do you think the appropriate function is for parsing "March 12,
| 1975"? Give it a try.
```
```r
> mdy("March 12, 1975")
[1] "1975-03-12"

| You got it!
```
```r
| We can even throw something funky at it and lubridate will often know the right thing to do. Parse
| 25081985, which is supposed to represent the 25th day of August 1985. Note that we are actually parsing a
| numeric value here -- not a character string -- so leave off the quotes.
```
```r
> dmy(25081985)
[1] "1985-08-25"

| That's a job well done!
```
```r
| But be careful, it's not magic. Try ymd("192012") to see what happens when we give it something more
| ambiguous. Surround the number with quotes again, just to be consistent with the way most dates are
| represented (as character strings).
```
```r
> ymd("192012")
[1] NA
Warning message:
All formats failed to parse. No formats found.

| You are amazing!
```
```r
| You got a warning message because it was unclear what date you wanted. When in doubt, it's best to be more
| explicit. Repeat the same command, but add two dashes OR two forward slashes to "192012" so that it's clear
| we want January 2, 1920.
```
```r
> ymd("1920/1/2")
[1] "1920-01-02"

| You are amazing!
```
```r
| In addition to dates, we can parse date-times. I've created a date-time object called dt1. Take a look at
| it now.
```
```r
> dt1
[1] "2014-08-23 17:23:02"

| You got it right!
```
```r
| Now parse dt1 with ymd_hms().
```
```r
> ymd_hms(dt1)
[1] "2014-08-23 17:23:02 UTC"

| Your dedication is inspiring!
```
```r
| What if we have a time, but no date? Use the appropriate lubridate function to parse "03:22:14" (hh:mm:ss).
```
```r
> hms("03:22:14")
[1] "3H 22M 14S"

| You nailed it! Good job!
```
```r
| lubridate is also capable of handling vectors of dates, which is particularly helpful when you need to
| parse an entire column of data. I've created a vector of dates called dt2. View its contents now.
```
```r
> dt2
[1] "2014-05-14" "2014-09-22" "2014-07-11"

| That's the answer I was looking for.
```
```r
| Now parse dt2 using the appropriate lubridate function.
```
```r
> ymd(dt2)
[1] "2014-05-14" "2014-09-22" "2014-07-11"

| Excellent work!
```
```r
| The update() function allows us to update one or more components of a date-time. For example, let's say the
| current time is 08:34:55 (hh:mm:ss). Update this_moment to the new time using the following command:
|
| update(this_moment, hours = 8, minutes = 34, seconds = 55).
```
```r
> update(this_moment, hours = 8, minutes = 34, seconds = 55)
[1] "2019-10-26 08:34:55 CEST"

| You nailed it! Good job!
```
```r
| It's important to recognize that the previous command does not alter this_moment unless we reassign the
| result to this_moment. To see this, print the contents of this_moment.
```
```r
> this_moment
[1] "2019-10-26 11:30:34 CEST"

| You got it!
```
```r
| Unless you're a superhero, some time has passed since you first created this_moment. Use update() to make
| it match the current time, specifying at least hours and minutes. Assign the result to this_moment, so that
| this_moment will contain the new time.
```
```r
> this_moment <- update(this_moment, hours = 8, minutes = 34, seconds = 55)

| Great job!
```
```r
| Take one more look at this_moment to see that it's been updated.
```
```r
> this_moment
[1] "2019-10-26 08:34:55 CEST"

| That's a job well done!
```
```r
| Now, pretend you are in New York City and you are planning to visit a friend in Hong Kong. You seem to have
| misplaced your itinerary, but you know that your flight departs New York at 17:34 (5:34pm) the day after
| tomorrow. You also know that your flight is scheduled to arrive in Hong Kong exactly 15 hours and 50
| minutes after departure.
```
```r
| Let's reconstruct your itinerary from what you can remember, starting with the full date and time of your
| departure. We will approach this by finding the current date in New York, adding 2 full days, then setting
| the time to 17:34.
```
```r
| To find the current date in New York, we'll use the now() function again. This time, however, we'll specify
| the time zone that we want: "America/New_York". Store the result in a variable called nyc. Check out ?now
| if you need help.
```
```r
> ?now
> nyc <- now("America/New_York")

| Perseverance, that's the answer.
```
```r
| For a complete list of valid time zones for use with lubridate, check out the following Wikipedia page:
|
| http://en.wikipedia.org/wiki/List_of_tz_database_time_zones
```
```r
| View the contents of nyc, which now contains the current date and time in New York.
```
```r
> nyc
[1] "2019-10-26 05:38:13 EDT"

| You nailed it! Good job!
```
```r
| Your flight is the day after tomorrow (in New York time), so we want to add two days to nyc. One nice
| aspect of lubridate is that it allows you to use arithmetic operators on dates and times. In this case,
| we'd like to add two days to nyc, so we can use the following expression: nyc + days(2). Give it a try,
| storing the result in a variable called depart.
```
```r
> depart <- nyc + days(2)

| Nice work!
```
```r
| Take a look at depart.
```
```r
> depart
[1] "2019-10-28 05:38:13 EDT"

| You are doing so well!
```
```r
| So now depart contains the date of the day after tomorrow. Use update() to add the correct hours (17) and
| minutes (34) to depart. Reassign the result to depart.
```
```r
> depart <- update(depart, hours = 17, minutes = 34)

| That's the answer I was looking for.
```
```r
| Take one more look at depart.
```
```r
> depart
[1] "2019-10-28 17:34:13 EDT"

| All that practice is paying off!
```
```r
| Your friend wants to know what time she should pick you up from the airport in Hong Kong. Now that we have
| the exact date and time of your departure from New York, we can figure out the exact time of your arrival
| in Hong Kong.
```
```r
| The first step is to add 15 hours and 50 minutes to your departure time. Recall that nyc + days(2) added
| two days to the current time in New York. Use the same approach to add 15 hours and 50 minutes to the
| date-time stored in depart. Store the result in a new variable called arrive.
```
```r
> arrive <- depart + hours(15) + minutes(50)

| You're the best!
```
```r
| The arrive variable contains the time that it will be in New York when you arrive in Hong Kong. What we
| really want to know is what time it will be in Hong Kong when you arrive, so that your friend knows when to
| meet you.
```
```r
| The with_tz() function returns a date-time as it would appear in another time zone. Use ?with_tz to check
| out the documentation.
```
```r
> ?with_tz

| You got it!
```
```r
| Use with_tz() to convert arrive to the "Asia/Hong_Kong" time zone. Reassign the result to arrive, so that
| it will get the new value.
```
```r
> arrive <- with_tz(arrive, "Asia/Hong_Kong")

| You got it right!
```
```r
| Print the value of arrive to the console, so that you can tell your friend what time to pick you up from
| the airport.
```
```r
> arrive
[1] "2019-10-29 21:24:13 HKT"

| You are really on a roll!
```
```r
| Fast forward to your arrival in Hong Kong. You and your friend have just met at the airport and you realize
| that the last time you were together was in Singapore on June 17, 2008. Naturally, you'd like to know
| exactly how long it has been.
```
```r
| Use the appropriate lubridate function to parse "June 17, 2008", just like you did near the beginning of
| this lesson. This time, however, you should specify an extra argument, tz = "Singapore". Store the result
| in a variable called last_time.
```
```r
> last_time <- mdy("June 17, 2008", tz= "Singapore")

| You are quite good my friend!
```
```r
| View the contents of last_time.
```
```r
> last_time
[1] "2008-06-17 +08"

| All that hard work is paying off!
```
```r
| Pull up the documentation for interval(), which we'll use to explore how much time has passed between
| arrive and last_time.
```
```r
> ?interval

| You are really on a roll!
```
```r
| Create an interval() that spans from last_time to arrive. Store it in a new variable called how_long.
```
```r
> how_long <- interval(last_time, arrive)

| You got it!
```
```r
| Now use as.period(how_long) to see how long it's been.
```
```r
> as.period(how_long)
[1] "11y 4m 12d 21H 24M 13S"

| You are really on a roll!
```
```r
| This is where things get a little tricky. Because of things like leap years, leap seconds, and daylight
| savings time, the length of any given minute, day, month, week, or year is relative to when it occurs. In
| contrast, the length of a second is always the same, regardless of when it occurs.
```
```r
| To address these complexities, the authors of lubridate introduce four classes of time related objects:
| instants, intervals, durations, and periods. These topics are beyond the scope of this lesson, but you can
| find a complete discussion in the 2011 Journal of Statistical Software paper titled 'Dates and Times Made
| Easy with lubridate'.
```
```r
| This concludes our introduction to working with dates and times in lubridate. I created a little timer that
| started running in the background when you began this lesson. Type stopwatch() to see how long you've been
| working!
```
```r
> stopwatch()
[1] "13M 29.4670310020447S"

| That's a job well done!
```
