# Programming in R - swirl tutorial
## Table of contents
* [Basic Building Blocks](#general)
* [Workspace and Files](#technologies)
* [Sequences of Numbers](#setup)
* [Vectors](#setup)
* [Missing Values](#setup)
* [Subsetting Vectors](#setup)
* [Matrices and Data Frames](#setup)
* [Logic](#setup)
* [Functions](#setup)
* [lapply and sapply](#setup)
* [vapply and tapply](#setup)
* [Looking at Data](#setup)
* [Simulation](#setup)
* [Dates and Times](#setup)
* [Base Graphics](#setup)

## 1. Basic Building Blocks
```r
| In this lesson, we will explore some basic building blocks of the R programming language.
```
```r
| If at any point you'd like more information on a particular topic related to R, you can type help.start()
| at the prompt, which will open a menu of resources (either within RStudio or your default web browser,
| depending on your setup). Alternatively, a simple web search often yields the answer you're looking for.
```
```r
| In its simplest form, R can be used as an interactive calculator. Type 5 + 7 and press Enter.
```
```r
> 5 + 7
[1] 12

| You got it right!
```
```r
| R simply prints the result of 12 by default. However, R is a programming language and often the reason we
| use a programming language as opposed to a calculator is to automate some process or avoid unnecessary
| repetition.
```
```r
| In this case, we may want to use our result from above in a second calculation. Instead of retyping 5 + 7
| every time we need it, we can just create a new variable that stores the result.
```
```r
| The way you assign a value to a variable in R is by using the assignment operator, which is just a 'less
| than' symbol followed by a 'minus' sign. It looks like this: <-
```
```r
| Think of the assignment operator as an arrow. You are assigning the value on the right side of the arrow to
| the variable name on the left side of the arrow.
```
```r
| To assign the result of 5 + 7 to a new variable called x, you type x <- 5 + 7. This can be read as 'x gets
| 5 plus 7'. Give it a try now.
```
```r
> x <- 5 + 7

| Nice work!
```
```r
| You'll notice that R did not print the result of 12 this time. When you use the assignment operator, R
| assumes that you don't want to see the result immediately, but rather that you intend to use the result for
| something else later on.
```
```r
| To view the contents of the variable x, just type x and press Enter. Try it now.
```
```r
> x
[1] 12

| That's correct!
```
```r
| Now, store the result of x - 3 in a new variable called y.
```
```r
> y <- x - 3

| That's correct!
```
```r
| What is the value of y? Type y to find out.
```
```r
> y
[1] 9

| You got it!
```
```r
| Now, let's create a small collection of numbers called a vector. Any object that contains data is called a
| data structure and numeric vectors are the simplest type of data structure in R. In fact, even a single
| number is considered a vector of length one.
```
```r
| The easiest way to create a vector is with the c() function, which stands for 'concatenate' or 'combine'.
| To create a vector containing the numbers 1.1, 9, and 3.14, type c(1.1, 9, 3.14). Try it now and store the
| result in a variable called z.
```
```r
> z <- c(1.1, 9, 3.14)

| That's correct!
```
```r
| Anytime you have questions about a particular function, you can access R's built-in help files via the `?`
| command. For example, if you want more information on the c() function, type ?c without the parentheses
| that normally follow a function name. Give it a try.
```
```r
> ?c

| You are doing so well!
```
```r
| Type z to view its contents. Notice that there are no commas separating the values in the output.
```
```r
> z
[1] 1.10 9.00 3.14

| You are amazing!
```
```r
| You can combine vectors to make a new vector. Create a new vector that contains z, 555, then z again in
| that order. Don't assign this vector to a new variable, so that we can just see the result immediately.
```
```r
> c(z, 555, z)
[1]   1.10   9.00   3.14 555.00   1.10   9.00   3.14

| You are really on a roll!
```
```r
| Numeric vectors can be used in arithmetic expressions. Type the following to see what happens: z * 2 + 100.
```
```r
> z * 2 + 100
[1] 102.20 118.00 106.28

| You nailed it! Good job!
```
```r
| First, R multiplied each of the three elements in z by 2. Then it added 100 to each element to get the
| result you see above.
```
```r
| Other common arithmetic operators are `+`, `-`, `/`, and `^` (where x^2 means 'x squared'). To take the
| square root, use the sqrt() function and to take the absolute value, use the abs() function.
```
```r
| Take the square root of z - 1 and assign it to a new variable called my_sqrt.
```
```r
> my_sqrt <- sqrt(z - 1)

| You are really on a roll!
```
```r
| Before we view the contents of the my_sqrt variable, what do you think it contains?

1: a single number (i.e a vector of length 1)
2: a vector of length 0 (i.e. an empty vector)
3: a vector of length 3
```
```r
Selection: 3

| You got it right!
```
```r
| Print the contents of my_sqrt.
```
```r
> my_sqrt
[1] 0.3162278 2.8284271 1.4628739

| You got it!
```
```r
| As you may have guessed, R first subtracted 1 from each element of z, then took the square root of each
| element. This leaves you with a vector of the same length as the original vector z.
```
```r
| Now, create a new variable called my_div that gets the value of z divided by my_sqrt.
```
```r
> my_div <- z / my_sqrt

| All that hard work is paying off!
```
```r
| Which statement do you think is true?

1: my_div is undefined
2: The first element of my_div is equal to the first element of z divided by the first element of my_sqrt, and so on...
3: my_div is a single number (i.e a vector of length 1)
```
```r
Selection: 2

| Nice work!
```
```r
| Go ahead and print the contents of my_div.
```
```r
> my_div
[1] 3.478505 3.181981 2.146460

| All that practice is paying off!
```
```r
| When given two vectors of the same length, R simply performs the specified arithmetic operation (`+`, `-`,
| `*`, etc.) element-by-element. If the vectors are of different lengths, R 'recycles' the shorter vector
| until it is the same length as the longer vector.
```
```r
| When we did z * 2 + 100 in our earlier example, z was a vector of length 3, but technically 2 and 100 are
| each vectors of length 1.
```
```r
| Behind the scenes, R is 'recycling' the 2 to make a vector of 2s and the 100 to make a vector of 100s. In
| other words, when you ask R to compute z * 2 + 100, what it really computes is this: z * c(2, 2, 2) +
| c(100, 100, 100).
```
```r
| To see another example of how this vector 'recycling' works, try adding c(1, 2, 3, 4) and c(0, 10). Don't
| worry about saving the result in a new variable.
```
```r
> c(1, 2, 3, 4) + c(0, 10)
[1]  1 12  3 14

| You are doing so well!
```
```r
| If the length of the shorter vector does not divide evenly into the length of the longer vector, R will
| still apply the 'recycling' method, but will throw a warning to let you know something fishy might be going
| on.
```
```r
| Try c(1, 2, 3, 4) + c(0, 10, 100) for an example.
```
```r
> c(1, 2, 3, 4) + c(0, 10, 100)
[1]   1  12 103   4
Warning message:
In c(1, 2, 3, 4) + c(0, 10, 100) :
  longer object length is not a multiple of shorter object length

| You are really on a roll!
```
```r
| Before concluding this lesson, I'd like to show you a couple of time-saving tricks.
```
```r
| Earlier in the lesson, you computed z * 2 + 100. Let's pretend that you made a mistake and that you meant
| to add 1000 instead of 100. You could either re-type the expression, or...
```
```r
| In many programming environments, the up arrow will cycle through previous commands. Try hitting the up
| arrow on your keyboard until you get to this command (z * 2 + 100), then change 100 to 1000 and hit Enter.
| If the up arrow doesn't work for you, just type the corrected command.
```
```r
> z * 2 + 1000
[1] 1002.20 1018.00 1006.28

| You are quite good my friend!
```
```r
| Finally, let's pretend you'd like to view the contents of a variable that you created earlier, but you
| can't seem to remember if you named it my_div or myDiv. You could try both and see what works, or...
```
```r
| You can type the first two letters of the variable name, then hit the Tab key (possibly more than once).
| Most programming environments will provide a list of variables that you've created that begin with 'my'.
| This is called auto-completion and can be quite handy when you have many variables in your workspace. Give
| it a try. (If auto-completion doesn't work for you, just type my_div and press Enter.)
```
```r
> my_div
[1] 3.478505 3.181981 2.146460

| You are doing so well!
```

## 2. Workspace and Files
```r
| In this lesson, you'll learn how to examine your local workspace in R and begin to explore the relationship
| between your workspace and the file system of your machine.
```
```r
| Because different operating systems have different conventions with regards to things like file paths, the
| outputs of these commands may vary across machines.
```
```r
| However it's important to note that R provides a common API (a common set of commands) for interacting with
| files, that way your code will work across different kinds of computers.
```
```r
| Let's jump right in so you can get a feel for how these special functions work!
```
```r
| Determine which directory your R session is using as its current working directory using getwd().
```
```r
> getwd()
[1] "/Users/bgorka"

| Excellent job!
```
```r
| List all the objects in your local workspace using ls().
```
```r
> ls()
 [1] "cnames"     "ints"       "my_char"    "my_data"    "my_div"     "my_matrix"  "my_matrix2" "my_na"     
 [9] "my_name"    "my_seq"     "my_sqrt"    "my_vector"  "num_vect"   "old.dir"    "patients"   "tf"        
[17] "vect"       "vect2"      "x"          "y"          "z"         

| Perseverance, that's the answer.
```
```r
| Some R commands are the same as their equivalents commands on Linux or on a Mac. Both Linux and Mac
| operating systems are based on an operating system called Unix. It's always a good idea to learn more about
| Unix!
```
```r
| Assign 9 to x using x <- 9.

> x <- 9

| That's a job well done!
```
```r
| Now take a look at objects that are in your workspace using ls().
```
```r
> ls()
 [1] "cnames"     "ints"       "my_char"    "my_data"    "my_div"     "my_matrix"  "my_matrix2" "my_na"     
 [9] "my_name"    "my_seq"     "my_sqrt"    "my_vector"  "num_vect"   "old.dir"    "patients"   "tf"        
[17] "vect"       "vect2"      "x"          "y"          "z"         

| Excellent work!
```
```r
| List all the files in your working directory using list.files() or dir().
```
```r
> list.files()
 [1] "Applications"       "Desktop"            "Documents"          "Downloads"        

| You are quite good my friend!
```
```r
| As we go through this lesson, you should be examining the help page for each new function. Check out the
| help page for list.files with the command ?list.files.
```
```r
> ?list.files

| You are amazing!
```
```r
| One of the most helpful parts of any R help file is the See Also section. Read that section for list.files.
| Some of these functions may be used in later portions of this lesson.
```
```r
| Using the args() function on a function name is also a handy way to see what arguments a function can take.
```
```r
| Use the args() function to determine the arguments to list.files().
```
```r
> args(list.files)

function (path = ".", pattern = NULL, all.files = FALSE, full.names = FALSE,
    recursive = FALSE, ignore.case = FALSE, include.dirs = FALSE,
    no.. = FALSE)
NULL

| That's correct!
```
```r
| Assign the value of the current working directory to a variable called "old.dir".
```
```r
> old.dir <- getwd()

| You are doing so well!
```
```r
| We will use old.dir at the end of this lesson to move back to the place that we started. A lot of query
| functions like getwd() have the useful property that they return the answer to the question as a result of
| the function.
```
```r
| Use dir.create() to create a directory in the current working directory called "testdir".
```
```r
> dir.create('testdir')
Warning message:
In dir.create("testdir") : 'testdir' already exists

| You got it right!
```
```r
| We will do all our work in this new directory and then delete it after we are done. This is the R analog to
| "Take only pictures, leave only footprints."
```
```r
| Set your working directory to "testdir" with the setwd() command.
```
```r
> setwd('testdir')

| Nice work!
```
```r
| In general, you will want your working directory to be someplace sensible, perhaps created for the specific
| project that you are working on. In fact, organizing your work in R packages using RStudio is an excellent
| option. Check out RStudio at http://www.rstudio.com/
```
```r
| Create a file in your working directory called "mytest.R" using the file.create() function.
```
```r
> file.create('mytest.R')
[1] TRUE

| You got it!
```
```r
| This should be the only file in this newly created directory. Let's check this by listing all the files in
| the current directory.
```
```r
> list.files()
[1] "mytest.R"
```
```r
| Check to see if "mytest.R" exists in the working directory using the file.exists() function.
```
```r
> file.exists('mytest.R')
[1] TRUE
```
```r
| These sorts of functions are excessive for interactive use. But, if you are running a program that loops
| through a series of files and does some processing on each one, you will want to check to see that each
| exists before you try to process it.
```
```r
| Access information about the file "mytest.R" by using file.info().
```
```r
> file.info('mytest.R')
         size isdir mode               mtime               ctime               atime uid gid  uname grname
mytest.R    0 FALSE  644 2019-10-12 16:50:06 2019-10-12 16:50:06 2019-10-12 16:50:06 502  20 bgorka  staff

| That's correct!
```
```r
| You can use the $ operator --- e.g., file.info("mytest.R")$mode --- to grab specific items.
```
```r
| Change the name of the file "mytest.R" to "mytest2.R" by using file.rename().
```
```r
> file.rename('mytest.R', 'mytest2.R')
[1] TRUE

| Nice work!
```
```r
| Your operating system will provide simpler tools for these sorts of tasks, but having the ability to
| manipulate files programatically is useful. You might now try to delete mytest.R using
| file.remove('mytest.R'), but that won't work since mytest.R no longer exists. You have already renamed it.
```
```r
| Make a copy of "mytest2.R" called "mytest3.R" using file.copy().
```
```r
> file.copy('mytest2.R', 'mytest3.R')
[1] TRUE

| That's the answer I was looking for.
```
```r
| You now have two files in the current directory. That may not seem very interesting. But what if you were
| working with dozens, or millions, of individual files? In that case, being able to programatically act on
| many files would be absolutely necessary. Don't forget that you can, temporarily, leave the lesson by
| typing play() and then return by typing nxt().
```
```r
| Provide the relative path to the file "mytest3.R" by using file.path().
```
```r
> file.path('mytest3.R')
[1] "mytest3.R"

| That's correct!
```
```r
| You can use file.path to construct file and directory paths that are independent of the operating system
| your R code is running on. Pass 'folder1' and 'folder2' as arguments to file.path to make a
| platform-independent pathname.
```
```r
> file.path('folder1', 'folder2')
[1] "folder1/folder2"

| You are really on a roll!
```
```r
| Take a look at the documentation for dir.create by entering ?dir.create . Notice the 'recursive' argument.
| In order to create nested directories, 'recursive' must be set to TRUE.
```
```r
> ?dir.create

| Keep working like that and you'll get there!
```
```r
| Create a directory in the current working directory called "testdir2" and a subdirectory for it called
| "testdir3", all in one command by using dir.create() and file.path().
```
```r
> dir.create(file.path('testdir2', 'testdir3'), recursive = TRUE)
Warning message:
In dir.create(file.path("testdir2", "testdir3"), recursive = TRUE) :
  'testdir2/testdir3' already exists

| That's a job well done!
```
```r
| Go back to your original working directory using setwd(). (Recall that we created the variable old.dir with
| the full path for the orginal working directory at the start of these questions.)
```
```r
> setwd(old.dir)

| All that hard work is paying off!
```
```r
| It is often helpful to save the settings that you had before you began an analysis and then go back to them
| at the end. This trick is often used within functions; you save, say, the par() settings that you started
| with, mess around a bunch, and then set them back to the original values at the end. This isn't the same as
| what we have done here, but it seems similar enough to mention.
```
```r
| After you finish this lesson delete the 'testdir' directory that you just left (and everything in it)
```
```r
| Take nothing but results. Leave nothing but assumptions. That sounds like 'Take nothing but pictures. Leave
| nothing but footprints.' But it makes no sense! Surely our readers can come up with a better motto . . .
```
```r
| In this lesson, you learned how to examine your R workspace and work with the file system of your machine
| from within R. Thanks for playing!
```

## 3. Sequences of Numbers
```r
| In this lesson, you'll learn how to create sequences of numbers in R.
```
```r
| The simplest way to create a sequence of numbers in R is by using the `:` operator. Type 1:20 to see how it
| works.
```
```r
> 1:20
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

| All that practice is paying off!
```
```r
| That gave us every integer between (and including) 1 and 20. We could also use it to create a sequence of
| real numbers. For example, try pi:10.
```
```r
> pi:10
[1] 3.141593 4.141593 5.141593 6.141593 7.141593 8.141593 9.141593
```
```r
| The result is a vector of real numbers starting with pi (3.142...) and increasing in increments of 1. The
| upper limit of 10 is never reached, since the next number in our sequence would be greater than 10.
```
```r
| What happens if we do 15:1? Give it a try to find out.
```
```r
> 15:1
 [1] 15 14 13 12 11 10  9  8  7  6  5  4  3  2  1

| You are quite good my friend!
```
```r
| It counted backwards in increments of 1! It's unlikely we'd want this behavior, but nonetheless it's good
| to know how it could happen.
```
```r
| Remember that if you have questions about a particular R function, you can access its documentation with a
| question mark followed by the function name: ?function_name_here. However, in the case of an operator like
| the colon used above, you must enclose the symbol in backticks like this: ?`:`. (NOTE: The backtick (`) key
| is generally located in the top left corner of a keyboard, above the Tab key. If you don't have a backtick
| key, you can use regular quotes.)
```
```r
| Pull up the documentation for `:` now.
```
```r
> ?`:`

| Keep working like that and you'll get there!
```
```r
| Often, we'll desire more control over a sequence we're creating than what the `:` operator gives us. The
| seq() function serves this purpose.
```
```r
| The most basic use of seq() does exactly the same thing as the `:` operator. Try seq(1, 20) to see this.
```
```r
> seq(1, 20)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

| That's the answer I was looking for.
```
```r
| This gives us the same output as 1:20. However, let's say that instead we want a vector of numbers ranging
| from 0 to 10, incremented by 0.5. seq(0, 10, by=0.5) does just that. Try it out.
```
```r
> seq(0, 10, by=0.5)
 [1]  0.0  0.5  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0  7.5  8.0  8.5  9.0  9.5 10.0

| You are amazing!
```
```r
| Or maybe we don't care what the increment is and we just want a sequence of 30 numbers between 5 and 10.
| seq(5, 10, length=30) does the trick. Give it a shot now and store the result in a new variable called
| my_seq.
```
```r
> my_seq <- seq(5, 10, length=30)

| You are really on a roll!
```
```r
| To confirm that my_seq has length 30, we can use the length() function. Try it now.
```
```r
> length(my_seq)
[1] 30

| You are amazing!
```
```r
| Let's pretend we don't know the length of my_seq, but we want to generate a sequence of integers from 1 to
| N, where N represents the length of the my_seq vector. In other words, we want a new vector (1, 2, 3, ...)
| that is the same length as my_seq.
```
```r
| There are several ways we could do this. One possibility is to combine the `:` operator and the length()
| function like this: 1:length(my_seq). Give that a try.
```
```r
> 1:length(my_seq)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30

| Keep up the great work!
```
```r
| Another option is to use seq(along.with = my_seq). Give that a try.
```
```r
> seq(along.with = my_seq)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30

| You nailed it! Good job!
```
```r
| However, as is the case with many common tasks, R has a separate built-in function for this purpose called
| seq_along(). Type seq_along(my_seq) to see it in action.
```
```r
> seq_along(my_seq)
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30
 ```
 ```r
| There are often several approaches to solving the same problem, particularly in R. Simple approaches that
| involve less typing are generally best. It's also important for your code to be readable, so that you and
| others can figure out what's going on without too much hassle.
```
```r
| If R has a built-in function for a particular task, it's likely that function is highly optimized for that
| purpose and is your best option. As you become a more advanced R programmer, you'll design your own
| functions to perform tasks when there are no better options. We'll explore writing your own functions in
| future lessons.
```
```r
| One more function related to creating sequences of numbers is rep(), which stands for 'replicate'. Let's
| look at a few uses.
```
```r
| If we're interested in creating a vector that contains 40 zeros, we can use rep(0, times = 40). Try it out.
```
```r
> rep(0, times = 40)
 [1] 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0

| Keep working like that and you'll get there!
```
```r
| If instead we want our vector to contain 10 repetitions of the vector (0, 1, 2), we can do rep(c(0, 1, 2),
| times = 10). Go ahead.
```
```r
> rep(c(0, 1, 2), times = 10)
 [1] 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2

| Great job!
```
```r
| Finally, let's say that rather than repeating the vector (0, 1, 2) over and over again, we want our vector
| to contain 10 zeros, then 10 ones, then 10 twos. We can do this with the `each` argument. Try rep(c(0, 1,
| 2), each = 10).
```
```r
> rep(c(0, 1, 2), each = 10)
 [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2

| You are really on a roll!
```

## 4. Vectors
```r
| The simplest and most common data structure in R is the vector.
```
```r
| Vectors come in two different flavors: atomic vectors and lists. An atomic vector contains exactly one data
| type, whereas a list may contain multiple data types. We'll explore atomic vectors further before we get to
| lists.
```
```r
| In previous lessons, we dealt entirely with numeric vectors, which are one type of atomic vector. Other
| types of atomic vectors include logical, character, integer, and complex. In this lesson, we'll take a
| closer look at logical and character vectors.
```
```r
| Logical vectors can contain the values TRUE, FALSE, and NA (for 'not available'). These values are
| generated as the result of logical 'conditions'. Let's experiment with some simple conditions.
```
```r
| First, create a numeric vector num_vect that contains the values 0.5, 55, -10, and 6.
```
```r
> num_vect <- c(0.5, 55, -10, 6)

| Excellent job!
```
```r
| Now, create a variable called tf that gets the result of num_vect < 1, which is read as 'num_vect is less
| than 1'.
```
```r
> tf <- num_vect < 1

| You are quite good my friend!
```
```r
| What do you think tf will look like?

1: a vector of 4 logical values
2: a single logical value
```
```r
Selection: 1

| You are really on a roll!
```
```r
| Print the contents of tf now.
```
```r
> tf
[1]  TRUE FALSE  TRUE FALSE

| Keep working like that and you'll get there!
```
```r
| The statement num_vect < 1 is a condition and tf tells us whether each corresponding element of our numeric
| vector num_vect satisfies this condition.
```
```r
| The first element of num_vect is 0.5, which is less than 1 and therefore the statement 0.5 < 1 is TRUE. The
| second element of num_vect is 55, which is greater than 1, so the statement 55 < 1 is FALSE. The same logic
| applies for the third and fourth elements.
```
```r
| Let's try another. Type num_vect >= 6 without assigning the result to a new variable.
```
```r
> num_vect >= 6
[1] FALSE  TRUE FALSE  TRUE

| That's correct!
```
```r
| This time, we are asking whether each individual element of num_vect is greater than OR equal to 6. Since
| only 55 and 6 are greater than or equal to 6, the second and fourth elements of the result are TRUE and the
| first and third elements are FALSE.
```
```r
| The `<` and `>=` symbols in these examples are called 'logical operators'. Other logical operators include
| `>`, `<=`, `==` for exact equality, and `!=` for inequality.
```
```r
| If we have two logical expressions, A and B, we can ask whether at least one is TRUE with A | B (logical
| 'or' a.k.a. 'union') or whether they are both TRUE with A & B (logical 'and' a.k.a. 'intersection').
| Lastly, !A is the negation of A and is TRUE when A is FALSE and vice versa.
```
```r
| It's a good idea to spend some time playing around with various combinations of these logical operators
| until you get comfortable with their use. We'll do a few examples here to get you started.
```
```r
| Try your best to predict the result of each of the following statements. You can use pencil and paper to
| work them out if it's helpful. If you get stuck, just guess and you've got a 50% chance of getting the
| right answer!
```
```r
| (3 > 5) & (4 == 4)

1: TRUE
2: FALSE
```
```r
Selection: 2

| You are really on a roll!
```
```r
| (TRUE == TRUE) | (TRUE == FALSE)

1: FALSE
2: TRUE
```
```r
Selection: 2

| All that hard work is paying off!
```
```r
| ((111 >= 111) | !(TRUE)) & ((4 + 1) == 5)

1: FALSE
2: TRUE
```
```r
Selection: 2

| You are amazing!
```
```r
| Don't worry if you found these to be tricky. They're supposed to be. Working with logical statements in R
| takes practice, but your efforts will be rewarded in future lessons (e.g. subsetting and control
| structures).
```
```r
| Character vectors are also very common in R. Double quotes are used to distinguish character objects, as in
| the following example.
```
```r
| Create a character vector that contains the following words: "My", "name", "is". Remember to enclose each
| word in its own set of double quotes, so that R knows they are character strings. Store the vector in a
| variable called my_char.
```
```r
> my_char <- c('My', 'name', 'is')

| You nailed it! Good job!
```
```r
| Print the contents of my_char to see what it looks like.
```
```r
> my_char
[1] "My"   "name" "is"  

| Perseverance, that's the answer.
```
```r
| Right now, my_char is a character vector of length 3. Let's say we want to join the elements of my_char
| together into one continuous character string (i.e. a character vector of length 1). We can do this using
| the paste() function.
```
```r
| Type paste(my_char, collapse = " ") now. Make sure there's a space between the double quotes in the
| `collapse` argument. You'll see why in a second.
```
```r
> paste(my_char, collapse = " ")
[1] "My name is"

| You are doing so well!
```
```r
| The `collapse` argument to the paste() function tells R that when we join together the elements of the
| my_char character vector, we'd like to separate them with single spaces.
```
```r
| It seems that we're missing something.... Ah, yes! Your name!
```
```r
| To add (or 'concatenate') your name to the end of my_char, use the c() function like this: c(my_char,
| "your_name_here"). Place your name in double quotes where I've put "your_name_here". Try it now, storing
| the result in a new variable called my_name.
```
```r
> my_name <- c(my_char, 'Bart')

| You are really on a roll!
```
```r
| Take a look at the contents of my_name.
```
```r
> my_name
[1] "My"   "name" "is"   "Bart"

| All that hard work is paying off!
```
```r
| Now, use the paste() function once more to join the words in my_name together into a single character
| string. Don't forget to say collapse = " "!
```
```r
> paste(my_name, collapse = " ")
[1] "My name is Bart"

| That's the answer I was looking for.
```
```r
| In this example, we used the paste() function to collapse the elements of a single character vector.
| paste() can also be used to join the elements of multiple character vectors.
```
```r
| In the simplest case, we can join two character vectors that are each of length 1 (i.e. join two words).
| Try paste("Hello", "world!", sep = " "), where the `sep` argument tells R that we want to separate the
| joined elements with a single space.
```
```r
> paste("Hello", "world!", sep = " ")
[1] "Hello world!"

| Keep working like that and you'll get there!
```
```r
| For a slightly more complicated example, we can join two vectors, each of length 3. Use paste() to join the
| integer vector 1:3 with the character vector c("X", "Y", "Z"). This time, use sep = "" to leave no space
| between the joined elements.
```
```r
> paste(1:3, c('X', 'Y', 'Z'), sep = "")
[1] "1X" "2Y" "3Z"

| Keep up the great work!
```
```r
| What do you think will happen if our vectors are of different length? (Hint: we talked about this in a
| previous lesson.)
```
```r
| Vector recycling! Try paste(LETTERS, 1:4, sep = "-"), where LETTERS is a predefined variable in R
| containing a character vector of all 26 letters in the English alphabet.
```
```r
> paste(LETTERS, 1:4, sep = "-")
 [1] "A-1" "B-2" "C-3" "D-4" "E-1" "F-2" "G-3" "H-4" "I-1" "J-2" "K-3" "L-4" "M-1" "N-2" "O-3" "P-4" "Q-1"
[18] "R-2" "S-3" "T-4" "U-1" "V-2" "W-3" "X-4" "Y-1" "Z-2"

| That's a job well done!
```
```r
| Since the character vector LETTERS is longer than the numeric vector 1:4, R simply recycles, or repeats,
| 1:4 until it matches the length of LETTERS.
```
```r
| Also worth noting is that the numeric vector 1:4 gets 'coerced' into a character vector by the paste()
| function.
```
```r
| We'll discuss coercion in another lesson, but all it really means is that the numbers 1, 2, 3, and 4 in the
| output above are no longer numbers to R, but rather characters "1", "2", "3", and "4".
```

## 5. Missing Values
```r
| Missing values play an important role in statistics and data analysis. Often, missing values must not be
| ignored, but rather they should be carefully studied to see if there's an underlying pattern or cause for
| their missingness.
```
```r
| In R, NA is used to represent any value that is 'not available' or 'missing' (in the statistical sense). In
| this lesson, we'll explore missing values further.
```
```r
| Any operation involving NA generally yields NA as the result. To illustrate, let's create a vector c(44,
| NA, 5, NA) and assign it to a variable x.
```
```r
> x <- c(44, NA, 5, NA)

| That's correct!
```
```r
| Now, let's multiply x by 3.
```
```r
> x * 3
[1] 132  NA  15  NA

| You're the best!
```
```r
| Notice that the elements of the resulting vector that correspond with the NA values in x are also NA.
```
```r
| To make things a little more interesting, lets create a vector containing 1000 draws from a standard normal
| distribution with y <- rnorm(1000).
```
```r
> y <- rnorm(1000)

| That's the answer I was looking for.
```
```r
| Next, let's create a vector containing 1000 NAs with z <- rep(NA, 1000).
```
```r
> z <- rep(NA, 1000)

| You are quite good my friend!
```
```r
| Finally, let's select 100 elements at random from these 2000 values (combining y and z) such that we don't
| know how many NAs we'll wind up with or what positions they'll occupy in our final vector -- my_data <-
| sample(c(y, z), 100).
```
```r
> my_data <- sample(c(y, z), 100)

| You got it right!
```
```r
| Let's first ask the question of where our NAs are located in our data. The is.na() function tells us
| whether each element of a vector is NA. Call is.na() on my_data and assign the result to my_na.
```
```r
> my_na <- is.na(my_data)

| You're the best!
```
```r
| Now, print my_na to see what you came up with.
```
```r
> my_na
  [1] FALSE  TRUE FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE
 [18]  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE  TRUE FALSE  TRUE  TRUE FALSE FALSE FALSE  TRUE FALSE
 [35]  TRUE FALSE  TRUE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE
 [52] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE  TRUE  TRUE  TRUE
 [69] FALSE FALSE  TRUE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE  TRUE FALSE  TRUE FALSE  TRUE  TRUE FALSE
 [86]  TRUE  TRUE FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE

| Keep working like that and you'll get there!
```
```r
| Everywhere you see a TRUE, you know the corresponding element of my_data is NA. Likewise, everywhere you
| see a FALSE, you know the corresponding element of my_data is one of our random draws from the standard
| normal distribution.
```
```r
| In our previous discussion of logical operators, we introduced the `==` operator as a method of testing for
| equality between two objects. So, you might think the expression my_data == NA yields the same results as
| is.na(). Give it a try.
```
```r
> my_data == NA
  [1] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
 [36] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA
 [71] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA

| Nice work!
```
```r
| The reason you got a vector of all NAs is that NA is not really a value, but just a placeholder for a
| quantity that is not available. Therefore the logical expression is incomplete and R has no choice but to
| return a vector of the same length as my_data that contains all NAs.
```
```r
| Don't worry if that's a little confusing. The key takeaway is to be cautious when using logical expressions
| anytime NAs might creep in, since a single NA value can derail the entire thing.
```
```r
| So, back to the task at hand. Now that we have a vector, my_na, that has a TRUE for every NA and FALSE for
| every numeric value, we can compute the total number of NAs in our data.
```
```r
| The trick is to recognize that underneath the surface, R represents TRUE as the number 1 and FALSE as the
| number 0. Therefore, if we take the sum of a bunch of TRUEs and FALSEs, we get the total number of TRUEs.
```
```r
| Let's give that a try here. Call the sum() function on my_na to count the total number of TRUEs in my_na,
| and thus the total number of NAs in my_data. Don't assign the result to a new variable.
```
```r
> sum(my_na)
[1] 53

| Perseverance, that's the answer.
```
```r
| Pretty cool, huh? Finally, let's take a look at the data to convince ourselves that everything 'adds up'.
| Print my_data to the console.
```
```r
> my_data
  [1] -0.01700531          NA -0.12764834 -0.67830820          NA          NA          NA  1.17271851
  [9]          NA -1.06365532  0.50428218  0.49849382 -1.13976361          NA -1.46821862  0.80138527
 [17]          NA          NA  0.50996568          NA          NA          NA -0.52559648          NA
 [25]          NA          NA -1.63349342          NA          NA -0.24903868 -0.01015387 -0.07823256
 [33]          NA  0.18765248          NA  0.75027919          NA          NA  0.36655222 -0.44128362
 [41]          NA  0.44994070          NA          NA          NA -0.52934730  0.17763372          NA
 [49]  0.66252533          NA          NA -0.20138914          NA          NA          NA          NA
 [57]          NA          NA          NA          NA  0.48676581          NA  0.29083249 -0.02696813
 [65]  0.87872619          NA          NA          NA  0.38598578  0.40593516          NA          NA
 [73]          NA -0.36469187          NA -0.06701772  1.00850791          NA          NA -0.22054153
 [81]          NA  2.42026564          NA          NA -0.04750434          NA          NA  0.51919350
 [89]          NA -0.04913295          NA  0.86477880 -1.75984812  3.14634038  0.52973111  2.11192946
 [97] -1.15791034  0.94150647 -1.02170307          NA

| Excellent work!
```
```r
| Now that we've got NAs down pat, let's look at a second type of missing value -- NaN, which stands for 'not
| a number'. To generate NaN, try dividing (using a forward slash) 0 by 0 now.
```
```r
> 0 / 0
[1] NaN

| Keep working like that and you'll get there!
```
```r
| Let's do one more, just for fun. In R, Inf stands for infinity. What happens if you subtract Inf from Inf?
```
```r
> Inf - Inf
[1] NaN

| You are quite good my friend!
```

## 6. Subsetting Vectors
```r
| In this lesson, we'll see how to extract elements from a vector based on some conditions that we specify.
```
```r
| For example, we may only be interested in the first 20 elements of a vector, or only the elements that are
| not NA, or only those that are positive or correspond to a specific variable of interest. By the end of
| this lesson, you'll know how to handle each of these scenarios.
```
```r
| I've created for you a vector called x that contains a random ordering of 20 numbers (from a standard
| normal distribution) and 20 NAs. Type x now to see what it looks like.
```
```r
> x
 [1]          NA          NA          NA  0.87747446  0.16095584          NA  0.74623548          NA
 [9] -0.28919183 -0.12159793 -0.23370627          NA  0.79362547          NA -0.05457325 -1.61407080
[17]          NA          NA  0.47815355          NA  0.69337427  1.35672837  1.14479065          NA
[25]          NA          NA          NA -1.90456500          NA -0.20298494          NA  2.45481472
[33]          NA  0.02995458          NA  0.85542384          NA          NA  0.93373838  0.90629573

| That's the answer I was looking for.
```
```r
| The way you tell R that you want to select some particular elements (i.e. a 'subset') from a vector is by
| placing an 'index vector' in square brackets immediately following the name of the vector.
```
```r
| For a simple example, try x[1:10] to view the first ten elements of x.
```
```r
> x[1:10]
 [1]         NA         NA         NA  0.8774745  0.1609558         NA  0.7462355         NA -0.2891918
[10] -0.1215979

| Keep working like that and you'll get there!
```
```r
| Index vectors come in four different flavors -- logical vectors, vectors of positive integers, vectors of
| negative integers, and vectors of character strings -- each of which we'll cover in this lesson.
```
```r
| Let's start by indexing with logical vectors. One common scenario when working with real-world data is that
| we want to extract all elements of a vector that are not NA (i.e. missing data). Recall that is.na(x)
| yields a vector of logical values the same length as x, with TRUEs corresponding to NA values in x and
| FALSEs corresponding to non-NA values in x.
```
```r
| What do you think x[is.na(x)] will give you?

1: A vector with no NAs
2: A vector of TRUEs and FALSEs
3: A vector of length 0
4: A vector of all NAs
```
```r
Selection: 4

| You are amazing!
```
```r
| Prove it to yourself by typing x[is.na(x)].
```
```r
> x[is.na(x)]
 [1] NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA NA

| Your dedication is inspiring!
```
```r
| Recall that `!` gives us the negation of a logical expression, so !is.na(x) can be read as 'is not NA'.
| Therefore, if we want to create a vector called y that contains all of the non-NA values from x, we can use
| y <- x[!is.na(x)]. Give it a try.
```
```r
> y <- x[!is.na(x)]

| Nice work!
```
```r
| Print y to the console.
```
```r
> y
 [1]  0.87747446  0.16095584  0.74623548 -0.28919183 -0.12159793 -0.23370627  0.79362547 -0.05457325
 [9] -1.61407080  0.47815355  0.69337427  1.35672837  1.14479065 -1.90456500 -0.20298494  2.45481472
[17]  0.02995458  0.85542384  0.93373838  0.90629573

| Your dedication is inspiring!
```
```r
| Now that we've isolated the non-missing values of x and put them in y, we can subset y as we please.
```
```r
| Recall that the expression y > 0 will give us a vector of logical values the same length as y, with TRUEs
| corresponding to values of y that are greater than zero and FALSEs corresponding to values of y that are
| less than or equal to zero. What do you think y[y > 0] will give you?

1: A vector of all the negative elements of y
2: A vector of all the positive elements of y
3: A vector of length 0
4: A vector of TRUEs and FALSEs
5: A vector of all NAs
```
```r
Selection: 2

| Keep working like that and you'll get there!
```
```r
| Type y[y > 0] to see that we get all of the positive elements of y, which are also the positive elements of
| our original vector x.
```
```r
> y[y > 0]
 [1] 0.87747446 0.16095584 0.74623548 0.79362547 0.47815355 0.69337427 1.35672837 1.14479065 2.45481472
[10] 0.02995458 0.85542384 0.93373838 0.90629573

| You are doing so well!
```
```r
| You might wonder why we didn't just start with x[x > 0] to isolate the positive elements of x. Try that now
| to see why.
```
```r
> x[x > 0]
 [1]         NA         NA         NA 0.87747446 0.16095584         NA 0.74623548         NA         NA
[10] 0.79362547         NA         NA         NA 0.47815355         NA 0.69337427 1.35672837 1.14479065
[19]         NA         NA         NA         NA         NA         NA 2.45481472         NA 0.02995458
[28]         NA 0.85542384         NA         NA 0.93373838 0.90629573

| Your dedication is inspiring!
```
```r
| Since NA is not a value, but rather a placeholder for an unknown quantity, the expression NA > 0 evaluates
| to NA. Hence we get a bunch of NAs mixed in with our positive numbers when we do this.
```
```r
| Combining our knowledge of logical operators with our new knowledge of subsetting, we could do this --
| x[!is.na(x) & x > 0]. Try it out.
```
```r
> x[!is.na(x) & x > 0]
 [1] 0.87747446 0.16095584 0.74623548 0.79362547 0.47815355 0.69337427 1.35672837 1.14479065 2.45481472
[10] 0.02995458 0.85542384 0.93373838 0.90629573

| Perseverance, that's the answer.
```
```r
| In this case, we request only values of x that are both non-missing AND greater than zero.
```
```r
| I've already shown you how to subset just the first ten values of x using x[1:10]. In this case, we're
| providing a vector of positive integers inside of the square brackets, which tells R to return only the
| elements of x numbered 1 through 10.
```
```r
| Many programming languages use what's called 'zero-based indexing', which means that the first element of a
| vector is considered element 0. R uses 'one-based indexing', which (you guessed it!) means the first
| element of a vector is considered element 1.
```
```r
| Can you figure out how we'd subset the 3rd, 5th, and 7th elements of x? Hint -- Use the c() function to
| specify the element numbers as a numeric vector.
```
```r
> x[c(3, 5, 7)]
[1]        NA 0.1609558 0.7462355

| Great job!
```
```r
| It's important that when using integer vectors to subset our vector x, we stick with the set of indexes {1,
| 2, ..., 40} since x only has 40 elements. What happens if we ask for the zeroth element of x (i.e. x[0])?
| Give it a try.
```
```r
> x[0]
numeric(0)

| Perseverance, that's the answer.
```
```r
| As you might expect, we get nothing useful. Unfortunately, R doesn't prevent us from doing this. What if we
| ask for the 3000th element of x? Try it out.
```
```r
> x[3000]
[1] NA

| Nice work!
```
```r
| Again, nothing useful, but R doesn't prevent us from asking for it. This should be a cautionary tale. You
| should always make sure that what you are asking for is within the bounds of the vector you're working
| with.
```
```r
| What if we're interested in all elements of x EXCEPT the 2nd and 10th? It would be pretty tedious to
| construct a vector containing all numbers 1 through 40 EXCEPT 2 and 10.
```
```r
| Luckily, R accepts negative integer indexes. Whereas x[c(2, 10)] gives us ONLY the 2nd and 10th elements of
| x, x[c(-2, -10)] gives us all elements of x EXCEPT for the 2nd and 10 elements.  Try x[c(-2, -10)] now to
| see this.
```
```r
> x[c(-2, -10)]
 [1]          NA          NA  0.87747446  0.16095584          NA  0.74623548          NA -0.28919183
 [9] -0.23370627          NA  0.79362547          NA -0.05457325 -1.61407080          NA          NA
[17]  0.47815355          NA  0.69337427  1.35672837  1.14479065          NA          NA          NA
[25]          NA -1.90456500          NA -0.20298494          NA  2.45481472          NA  0.02995458
[33]          NA  0.85542384          NA          NA  0.93373838  0.90629573

| You're the best!
```
```r
| A shorthand way of specifying multiple negative numbers is to put the negative sign out in front of the
| vector of positive numbers. Type x[-c(2, 10)] to get the exact same result.
```
```r
> x[-c(2, 10)]
 [1]          NA          NA  0.87747446  0.16095584          NA  0.74623548          NA -0.28919183
 [9] -0.23370627          NA  0.79362547          NA -0.05457325 -1.61407080          NA          NA
[17]  0.47815355          NA  0.69337427  1.35672837  1.14479065          NA          NA          NA
[25]          NA -1.90456500          NA -0.20298494          NA  2.45481472          NA  0.02995458
[33]          NA  0.85542384          NA          NA  0.93373838  0.90629573

| You got it!
```
```r
| So far, we've covered three types of index vectors -- logical, positive integer, and negative integer. The
| only remaining type requires us to introduce the concept of 'named' elements.
```
```r
| Create a numeric vector with three named elements using vect <- c(foo = 11, bar = 2, norf = NA).
```
```r
> vect <- c(foo = 11, bar = 2, norf = NA)

| Nice work!
```
```r
| When we print vect to the console, you'll see that each element has a name. Try it out.
```
```r
> vect
 foo  bar norf
  11    2   NA

| That's a job well done!
```
```r
| We can also get the names of vect by passing vect as an argument to the names() function. Give that a try.
```
```r
> names(vect)
[1] "foo"  "bar"  "norf"

| You nailed it! Good job!
```
```r
| Alternatively, we can create an unnamed vector vect2 with c(11, 2, NA). Do that now.
```
```r
> vect2 <- c(11, 2, NA)

| Keep working like that and you'll get there!
```
```r
| Then, we can add the `names` attribute to vect2 after the fact with names(vect2) <- c("foo", "bar",
| "norf"). Go ahead.
```
```r
> names(vect2) <- c('foo', 'bar', 'norf')

| You got it right!
```
```r
| Now, let's check that vect and vect2 are the same by passing them as arguments to the identical() function.
```
```r
> identical(vect, vect2)
[1] TRUE

| That's a job well done!
```
```r
| Indeed, vect and vect2 are identical named vectors.
```
```r
| Now, back to the matter of subsetting a vector by named elements. Which of the following commands do you
| think would give us the second element of vect?

1: vect["2"]
2: vect["bar"]
3: vect[bar]
```
```r
Selection: 2

| Your dedication is inspiring!
```
```r
| Now, try it out.
```
```r
> vect["bar"]
bar
  2

| Excellent work!
```
```r
| Likewise, we can specify a vector of names with vect[c("foo", "bar")]. Try it out.
```
```r
> vect[c("foo", "bar")]
foo bar
 11   2

| You got it right!
```
```r
| Now you know all four methods of subsetting data from vectors. Different approaches are best in different
| scenarios and when in doubt, try it out!
```

## 7. Matrices and Data Frames
```r
| In this lesson, we'll cover matrices and data frames. Both represent 'rectangular' data types, meaning that
| they are used to store tabular data, with rows and columns.
```
```r
| The main difference, as you'll see, is that matrices can only contain a single class of data, while data
| frames can consist of many different classes of data.
```
```r
| Let's create a vector containing the numbers 1 through 20 using the `:` operator. Store the result in a
| variable called my_vector.
```
```r
> my_vector <- 1:20

| All that practice is paying off!
```
```r
| View the contents of the vector you just created.
```
```r
> my_vector
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20

| All that hard work is paying off!
```
```r
| The dim() function tells us the 'dimensions' of an object. What happens if we do dim(my_vector)? Give it a
| try.
```
```r
> dim(my_vector)
NULL

| You nailed it! Good job!
```
```r
| Clearly, that's not very helpful! Since my_vector is a vector, it doesn't have a `dim` attribute (so it's
| just NULL), but we can find its length using the length() function. Try that now.
```
```r
> length(my_vector)
[1] 20

| You're the best!
```
```r
| Ah! That's what we wanted. But, what happens if we give my_vector a `dim` attribute? Let's give it a try.
| Type dim(my_vector) <- c(4, 5).
```
```r
> dim(my_vector) <- c(4, 5)

| You're the best!
```
```r
| It's okay if that last command seemed a little strange to you. It should! The dim() function allows you to
| get OR set the `dim` attribute for an R object. In this case, we assigned the value c(4, 5) to the `dim`
| attribute of my_vector.
```
```r
| Use dim(my_vector) to confirm that we've set the `dim` attribute correctly.
```
```r
> dim(my_vector)
[1] 4 5

| Keep up the great work!
```
```r
| Another way to see this is by calling the attributes() function on my_vector. Try it now.
```
```r
> attributes(my_vector)
$dim
[1] 4 5


| You're the best!
```
```r
| Just like in math class, when dealing with a 2-dimensional object (think rectangular table), the first
| number is the number of rows and the second is the number of columns. Therefore, we just gave my_vector 4
| rows and 5 columns.
```
```r
| But, wait! That doesn't sound like a vector any more. Well, it's not. Now it's a matrix. View the contents
| of my_vector now to see what it looks like.
```
```r
> my_vector
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    5    9   13   17
[2,]    2    6   10   14   18
[3,]    3    7   11   15   19
[4,]    4    8   12   16   20

| You're the best!
```
```r
| Now, let's confirm it's actually a matrix by using the class() function. Type class(my_vector) to see what
| I mean.
```
```r
> class(my_vector)
[1] "matrix"

| Great job!
```
```r
| Sure enough, my_vector is now a matrix. We should store it in a new variable that helps us remember what it
| is. Store the value of my_vector in a new variable called my_matrix.
```
```r
> my_matrix <- my_vector

| You nailed it! Good job!
```
```r
| The example that we've used so far was meant to illustrate the point that a matrix is simply an atomic
| vector with a dimension attribute. A more direct method of creating the same matrix uses the matrix()
| function.
```
```r
| Bring up the help file for the matrix() function now using the `?` function.
```
```r
> ?matrix

| You are really on a roll!
```
```r
| Now, look at the documentation for the matrix function and see if you can figure out how to create a matrix
| containing the same numbers (1-20) and dimensions (4 rows, 5 columns) by calling the matrix() function.
| Store the result in a variable called my_matrix2.
```
```r
> my_matrix2 <- matrix(1:20, nrow=4, ncol=5)

| That's correct!
```
```r
| Finally, let's confirm that my_matrix and my_matrix2 are actually identical. The identical() function will
| tell us if its first two arguments are the same. Try it out.
```
```r
> identical(my_matrix, my_matrix2)
[1] TRUE

| Keep working like that and you'll get there!
```
```r
| Now, imagine that the numbers in our table represent some measurements from a clinical experiment, where
| each row represents one patient and each column represents one variable for which measurements were taken.
```
```r
| We may want to label the rows, so that we know which numbers belong to each patient in the experiment. One
| way to do this is to add a column to the matrix, which contains the names of all four people.
```
```r
| Let's start by creating a character vector containing the names of our patients -- Bill, Gina, Kelly, and
| Sean. Remember that double quotes tell R that something is a character string. Store the result in a
| variable called patients.
```
```r
> patients <- c('Bill', 'Gina', 'Kelly', 'Sean')

| That's the answer I was looking for.
```
```r
| Now we'll use the cbind() function to 'combine columns'. Don't worry about storing the result in a new
| variable. Just call cbind() with two arguments -- the patients vector and my_matrix.
```
```r
> cbind(patients, my_matrix)
     patients                       
[1,] "Bill"   "1" "5" "9"  "13" "17"
[2,] "Gina"   "2" "6" "10" "14" "18"
[3,] "Kelly"  "3" "7" "11" "15" "19"
[4,] "Sean"   "4" "8" "12" "16" "20"

| Great job!
```
```r
| Something is fishy about our result! It appears that combining the character vector with our matrix of
| numbers caused everything to be enclosed in double quotes. This means we're left with a matrix of character
| strings, which is no good.
```
```r
| If you remember back to the beginning of this lesson, I told you that matrices can only contain ONE class
| of data. Therefore, when we tried to combine a character vector with a numeric matrix, R was forced to
| 'coerce' the numbers to characters, hence the double quotes.
```
```r
| This is called 'implicit coercion', because we didn't ask for it. It just happened. But why didn't R just
| convert the names of our patients to numbers? I'll let you ponder that question on your own.
```
```r
| So, we're still left with the question of how to include the names of our patients in the table without
| destroying the integrity of our numeric data. Try the following -- my_data <- data.frame(patients,
| my_matrix)
```
```r
> my_data <- data.frame(patients, my_matrix)

| All that hard work is paying off!
```
```r
| Now view the contents of my_data to see what we've come up with.
```
```r
> my_data
  patients X1 X2 X3 X4 X5
1     Bill  1  5  9 13 17
2     Gina  2  6 10 14 18
3    Kelly  3  7 11 15 19
4     Sean  4  8 12 16 20

| That's correct!
```
```r
| It looks like the data.frame() function allowed us to store our character vector of names right alongside
| our matrix of numbers. That's exactly what we were hoping for!
```
```r
| Behind the scenes, the data.frame() function takes any number of arguments and returns a single object of
| class `data.frame` that is composed of the original objects.
```
```r
| Let's confirm this by calling the class() function on our newly created data frame.
```
```r
> class(my_data)
[1] "data.frame"

| You nailed it! Good job!
```
```r
| It's also possible to assign names to the individual rows and columns of a data frame, which presents
| another possible way of determining which row of values in our table belongs to each patient.
```
```r
| However, since we've already solved that problem, let's solve a different problem by assigning names to the
| columns of our data frame so that we know what type of measurement each column represents.
```
```r
| Since we have six columns (including patient names), we'll need to first create a vector containing one
| element for each column. Create a character vector called cnames that contains the following values (in
| order) -- "patient", "age", "weight", "bp", "rating", "test".
```
```r
> cnames <- c('patient', 'age', 'weight', 'bp', 'rating', 'test')

| Nice work!
```
```r
| Now, use the colnames() function to set the `colnames` attribute for our data frame. This is similar to the
| way we used the dim() function earlier in this lesson.
```
```r
> colnames(my_data) <- cnames

| Great job!
```
```r
| Let's see if that got the job done. Print the contents of my_data.
```
```r
> my_data
  patient age weight bp rating test
1    Bill   1      5  9     13   17
2    Gina   2      6 10     14   18
3   Kelly   3      7 11     15   19
4    Sean   4      8 12     16   20

| You're the best!
```
```r
| In this lesson, you learned the basics of working with two very important and common data structures --
| matrices and data frames. There's much more to learn and we'll be covering more advanced topics,
| particularly with respect to data frames, in future lessons.
```

## 8. Logic
```r
| This lesson is meant to be a short introduction to logical operations in R.
```
```r
| There are two logical values in R, also called boolean values. They are TRUE and FALSE. In R you can
| construct logical expressions which will evaluate to either TRUE or FALSE.
```
```r
| Many of the questions in this lesson will involve evaluating logical expressions. It may be useful to open
| up a second R terminal where you can experiment with some of these expressions.
```
```r
| Creating logical expressions requires logical operators. You're probably familiar with arithmetic operators
| like `+`, `-`, `*`, and `/`. The first logical operator we are going to discuss is the equality operator,
| represented by two equals signs `==`. Use the equality operator below to find out if TRUE is equal to TRUE.
```
```r
> TRUE == TRUE
[1] TRUE

| You are amazing!
```
```r
| Just like arithmetic, logical expressions can be grouped by parenthesis so that the entire expression (TRUE
| == TRUE) == TRUE evaluates to TRUE.
```
```r
| To test out this property, try evaluating (FALSE == TRUE) == FALSE .
```
```r
> (FALSE == TRUE) == FALSE
[1] TRUE

| Excellent work!
```
```r
| The equality operator can also be used to compare numbers. Use `==` to see if 6 is equal to 7.
```
```r
> 6 == 7
[1] FALSE

| Excellent job!
```
```r
| The previous expression evaluates to FALSE because 6 is less than 7. Thankfully, there are inequality
| operators that allow us to test if a value is less than or greater than another value.
```
```r
| The less than operator `<` tests whether the number on the left side of the operator (called the left
| operand) is less than the number on the right side of the operator (called the right operand). Write an
| expression to test whether 6 is less than 7.
```
```r
> 6 < 7
[1] TRUE

| You are amazing!
```
```r
| There is also a less-than-or-equal-to operator `<=` which tests whether the left operand is less than or
| equal to the right operand. Write an expression to test whether 10 is less than or equal to 10.
```
```r
> 10 <= 10
[1] TRUE

| Perseverance, that's the answer.
```
```r
| Keep in mind that there are the corresponding greater than `>` and greater-than-or-equal-to `>=` operators.
```
```r
| Which of the following evaluates to FALSE?
```
```r
1: 6 < 8
2: 7 == 7
3: 9 >= 10
4: 0 > -36
```
```r
Selection: 3

| You are really on a roll!
```
```r
| Which of the following evaluates to TRUE?

1: 9 >= 10
2: -6 > -7
3: 7 == 9
4: 57 < 8
```
```r
Selection: 2

| You are amazing!
```
```r
| The next operator we will discuss is the 'not equals' operator represented by `!=`. Not equals tests
| whether two values are unequal, so TRUE != FALSE evaluates to TRUE. Like the equality operator, `!=` can
| also be used with numbers. Try writing an expression to see if 5 is not equal to 7.
```
```r
> 5 != 7
[1] TRUE

| You got it!
```
```r
| In order to negate boolean expressions you can use the NOT operator. An exclamation point `!` will cause
| !TRUE (say: not true) to evaluate to FALSE and !FALSE (say: not false) to evaluate to TRUE. Try using the
| NOT operator and the equals operator to find the opposite of whether 5 is equal to 7.
```
```r
> !(5 == 7)
[1] TRUE

| Keep up the great work!
```
```r
| Let's take a moment to review. The equals operator `==` tests whether two boolean values or numbers are
| equal, the not equals operator `!=` tests whether two boolean values or numbers are unequal, and the NOT
| operator `!` negates logical expressions so that TRUE expressions become FALSE and FALSE expressions become
| TRUE.
```
```r
| Which of the following evaluates to FALSE?
```
```r
1: 7 != 8
2: !FALSE
3: 9 < 10
4: !(0 >= -1)
```
```r
Selection: 4

| All that practice is paying off!
```
```r
| What do you think the following expression will evaluate to?: (TRUE != FALSE) == !(6 == 7)

1: FALSE
2: Can there be objective truth when programming?
3: TRUE
4: %>%
```
```r
Selection: 3

| You are amazing!
```
```r
| At some point you may need to examine relationships between multiple logical expressions. This is where the
| AND operator and the OR operator come in.
```
```r
| Let's look at how the AND operator works. There are two AND operators in R, `&` and `&&`. Both operators
| work similarly, if the right and left operands of AND are both TRUE the entire expression is TRUE,
| otherwise it is FALSE. For example, TRUE & TRUE evaluates to TRUE. Try typing FALSE & FALSE to how it is
| evaluated.
```
```r
> FALSE & FALSE
[1] FALSE

| You nailed it! Good job!
```
```r
| You can use the `&` operator to evaluate AND across a vector. The `&&` version of AND only evaluates the
| first member of a vector. Let's test both for practice. Type the expression TRUE & c(TRUE, FALSE, FALSE).
```
```r
> TRUE & c(TRUE, FALSE, FALSE)
[1]  TRUE FALSE FALSE

| You are doing so well!
```
```r
| What happens in this case is that the left operand `TRUE` is recycled across every element in the vector of
| the right operand. This is the equivalent statement as c(TRUE, TRUE, TRUE) & c(TRUE, FALSE, FALSE).
```
```r
| Now we'll type the same expression except we'll use the `&&` operator. Type the expression TRUE && c(TRUE,
| FALSE, FALSE).
```
```r
> TRUE && c(TRUE, FALSE, FALSE)
[1] TRUE

| Keep up the great work!
```
```r
| In this case, the left operand is only evaluated with the first member of the right operand (the vector).
| The rest of the elements in the vector aren't evaluated at all in this expression.
```
```r
| The OR operator follows a similar set of rules. The `|` version of OR evaluates OR across an entire vector,
| while the `||` version of OR only evaluates the first member of a vector.
```
```r
| An expression using the OR operator will evaluate to TRUE if the left operand or the right operand is TRUE.
| If both are TRUE, the expression will evaluate to TRUE, however if neither are TRUE, then the expression
| will be FALSE.
```
```r
| Let's test out the vectorized version of the OR operator. Type the expression TRUE | c(TRUE, FALSE, FALSE).
```
```r
> TRUE | c(TRUE, FALSE, FALSE)
[1] TRUE TRUE TRUE

| You are amazing!
```
```r
| Now let's try out the non-vectorized version of the OR operator. Type the expression TRUE || c(TRUE, FALSE,
| FALSE).
```
```r
> TRUE || c(TRUE, FALSE, FALSE)
[1] TRUE

| You nailed it! Good job!
```
```r
| Logical operators can be chained together just like arithmetic operators. The expressions: `6 != 10 &&
| FALSE && 1 >= 2` or `TRUE || 5 < 9.3 || FALSE` are perfectly normal to see.
```
```r
| As you may recall, arithmetic has an order of operations and so do logical expressions. All AND operators
| are evaluated before OR operators. Let's look at an example of an ambiguous case. Type: 5 > 8 || 6 != 8 &&
| 4 > 3.9
```
```r
> 5 > 8 || 6 != 8 && 4 > 3.9
[1] TRUE

| You got it right!
```
```r
| Let's walk through the order of operations in the above case. First the left and right operands of the AND
| operator are evaluated. 6 is not equal 8, 4 is greater than 3.9, therefore both operands are TRUE so the
| resulting expression `TRUE && TRUE` evaluates to TRUE. Then the left operand of the OR operator is
| evaluated: 5 is not greater than 8 so the entire expression is reduced to FALSE || TRUE. Since the right
| operand of this expression is TRUE the entire expression evaluates to TRUE.
```
```r
| Which one of the following expressions evaluates to TRUE?

1: TRUE && FALSE || 9 >= 4 && 3 < 6
2: 99.99 > 100 || 45 < 7.3 || 4 != 4.0
3: FALSE || TRUE && FALSE
4: TRUE && 62 < 62 && 44 >= 44
```
```r
Selection: 1

| All that hard work is paying off!
```
```r
| Which one of the following expressions evaluates to FALSE?

1: FALSE || TRUE && 6 != 4 || 9 > 4
2: 6 >= -9 && !(6 > 7) && !(!TRUE)
3: FALSE && 6 >= 6 || 7 >= 8 || 50 <= 49.5
4: !(8 > 4) ||  5 == 5.0 && 7.8 >= 7.79
```
```r
Selection: 3

| Nice work!
```
```r
| Now that you're familiar with R's logical operators you can take advantage of a few functions that R
| provides for dealing with logical expressions.
```
```r
| The function isTRUE() takes one argument. If that argument evaluates to TRUE, the function will return
| TRUE. Otherwise, the function will return FALSE. Try using this function by typing: isTRUE(6 > 4)
```
```r
> isTRUE(6 > 4)
[1] TRUE

| Excellent job!
```
```r
| Which of the following evaluates to TRUE?

1: isTRUE(3)
2: !isTRUE(4 < 3)
3: !isTRUE(8 != 5)
4: isTRUE(!TRUE)
5: isTRUE(NA)
```
```r
Selection: 2

| That's a job well done!
```
```r
| The function identical() will return TRUE if the two R objects passed to it as arguments are identical. Try
| out the identical() function by typing: identical('twins', 'twins')
```
```r
> identical('twins', 'twins')
[1] TRUE

| That's the answer I was looking for.
```
```r
| Which of the following evaluates to TRUE?

1: identical(4, 3.1)
2: identical(5 > 4, 3 < 3.1)
3: identical('hello', 'Hello')
4: !identical(7, 7)
```
```r
Selection: 2

| You nailed it! Good job!
```
```r
| You should also be aware of the xor() function, which takes two arguments. The xor() function stands for
| exclusive OR. If one argument evaluates to TRUE and one argument evaluates to FALSE, then this function
| will return TRUE, otherwise it will return FALSE. Try out the xor() function by typing: xor(5 == 6, !FALSE)
```
```r
> xor(5 == 6, !FALSE)
[1] TRUE

| You are quite good my friend!
```
```r
| 5 == 6 evaluates to FALSE, !FALSE evaluates to TRUE, so xor(FALSE, TRUE) evaluates to TRUE. On the other
| hand if the first argument was changed to 5 == 5 and the second argument was unchanged then both arguments
| would have been TRUE, so xor(TRUE, TRUE) would have evaluated to FALSE.
```
```r
| Which of the following evaluates to FALSE?

1: xor(identical(xor, 'xor'), 7 == 7.0)
2: xor(!isTRUE(TRUE), 6 > -1)
3: xor(!!TRUE, !!FALSE)
4: xor(4 >= 9, 8 != 8.0)
```
```r
Selection: 4

| Keep working like that and you'll get there!
```
```r
| For the next few questions, we're going to need to create a vector of integers called ints. Create this
| vector by typing: ints <- sample(10)
```
```r
> ints <- sample(10)

| Perseverance, that's the answer.
```
```r
| Now simply display the contents of ints.
```
```r
> ints
 [1]  2 10  5  6  3  1  8  4  7  9

| You got it!
```
```rs
| The vector `ints` is a random sampling of integers from 1 to 10 without replacement. Let's say we wanted to
| ask some logical questions about contents of ints. If we type ints > 5, we will get a logical vector
| corresponding to whether each element of ints is greater than 5. Try typing: ints > 5
```
```r
> ints > 5
 [1] FALSE  TRUE FALSE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE

| Excellent job!
```
```r
| We can use the resulting logical vector to ask other questions about ints. The which() function takes a
| logical vector as an argument and returns the indices of the vector that are TRUE. For example
| which(c(TRUE, FALSE, TRUE)) would return the vector c(1, 3).
```
```r
| Use the which() function to find the indices of ints that are greater than 7.
```
```r
> which(ints > 7)
[1]  2  7 10

| Nice work!
```
```r
| Which of the following commands would produce the indices of the elements in ints that are less than or
| equal to 2?

1: which(ints <= 2)
2: ints < 2
3: which(ints < 2)
4: ints <= 2
```
```r
Selection: 1

| All that hard work is paying off!
```
```r
| Like the which() function, the functions any() and all() take logical vectors as their argument. The any()
| function will return TRUE if one or more of the elements in the logical vector is TRUE. The all() function
| will return TRUE if every element in the logical vector is TRUE.
```
```r
| Use the any() function to see if any of the elements of ints are less than zero.
```
```r
> any(ints < 0)
[1] FALSE

| Excellent work!
```
```r
| Use the all() function to see if all of the elements of ints are greater than zero.
```
```r
> all(ints > 0)
[1] TRUE

| All that practice is paying off!
```
```r
| Which of the following evaluates to TRUE?

1: any(ints == 10)
2: all(c(TRUE, FALSE, TRUE))
3: all(ints == 10)
4: any(ints == 2.5)
```
```r
Selection: 1

| Excellent job!
```
```r
| That's all for this introduction to logic in R. If you really want to see what you can do with logic, check
| out the control flow lesson!
```

## 9. Functions
```r
| Functions are one of the fundamental building blocks of the R language. They are small pieces of reusable
| code that can be treated like any other R object.
```
```r
| If you've worked through any other part of this course, you've probably used some functions already.
| Functions are usually characterized by the name of the function followed by parentheses.
```
```r
| Let's try using a few basic functions just for fun. The Sys.Date() function returns a string representing
| today's date. Type Sys.Date() below and see what happens.
```
```r
> Sys.Date()
[1] "2019-10-14"

| You are doing so well!
```
```r
| Most functions in R return a value. Functions like Sys.Date() return a value based on your computer's
| environment, while other functions manipulate input data in order to compute a return value.
```
```r
| The mean() function takes a vector of numbers as input, and returns the average of all of the numbers in
| the input vector. Inputs to functions are often called arguments. Providing arguments to a function is also
| sometimes called passing arguments to that function. Arguments you want to pass to a function go inside the
| function's parentheses. Try passing the argument c(2, 4, 5) to the mean() function.
```
```r
> mean(c(2, 4, 5))
[1] 3.666667

| Keep up the great work!
```
```r
| Functions usually take arguments which are variables that the function operates on. For example, the mean()
| function takes a vector as an argument, like in the case of mean(c(2,6,8)). The mean() function then adds
| up all of the numbers in the vector and divides that sum by the length of the vector.
```
```r
| In the following question you will be asked to modify a script that will appear as soon as you move on from
| this question. When you have finished modifying the script, save your changes to the script and type
| submit() and the script will be evaluated. There will be some comments in the script that opens up, so be
| sure to read them!
```
```r
| The last R expression to be evaluated in a function will become the return value of that function. We want
| this function to take one argument, x, and return x without modifying it. Delete the pound sign so that x
| is returned without any modification. Make sure to save your script before you type submit().
```
```r
> submit()

| Sourcing your script...


| Your dedication is inspiring!
```
```r
| Now that you've created your first function let's test it! Type: boring_function('My first function!'). If
| your function works, it should just return the string: 'My first function!'
```
```r
> boring_function('My first function!')
[1] "My first function!"

| You got it right!
```
```r
| Congratulations on writing your first function. By writing functions, you can gain serious insight into how
| R works. As John Chambers, the creator of R once said:
|
| To understand computations in R, two slogans are helpful: 1. Everything that exists is an object. 2.
| Everything that happens is a function call.
```
```r
| If you want to see the source code for any function, just type the function name without any arguments or
| parentheses. Let's try this out with the function you just created. Type: boring_function to view its
| source code.
```
```r
> boring_function
function(x) {
  x
}
<bytecode: 0x7fa11479b148>

| That's a job well done!
```
```r
| Time to make a more useful function! We're going to replicate the functionality of the mean() function by
| creating a function called: my_mean(). Remember that to calculate the average of all of the numbers in a
| vector you find the sum of all the numbers in the vector, and then divide that sum by the number of numbers
| in the vector.
```
```r
| Make sure to save your script before you type submit().

> submit()

| Sourcing your script...


| Nice work!
```
```r
| Now test out your my_mean() function by finding the mean of the vector c(4, 5, 10).
```
```r
> my_mean(c(4, 5, 10))
[1] 6.333333

| Your dedication is inspiring!
```
```r
| Next, let's try writing a function with default arguments. You can set default values for a function's
| arguments, and this can be useful if you think someone who uses your function will set a certain argument
| to the same value most of the time.
```
```r
| Make sure to save your script before you type submit().
```
```r
> submit()

| Sourcing your script...


| That's the answer I was looking for.
```
```r
| Let's do some testing of the remainder function. Run remainder(5) and see what happens.
```
```r
> remainder(5)
[1] 1

| That's a job well done!
```
```r
| Let's take a moment to examine what just happened. You provided one argument to the function, and R matched
| that argument to 'num' since 'num' is the first argument. The default value for 'divisor' is 2, so the
| function used the default value you provided.
```
```r
| Now let's test the remainder function by providing two arguments. Type: remainder(11, 5) and let's see what
| happens.
```
```r
> remainder(11, 5)
[1] 1

| That's the answer I was looking for.
```
```r
| Once again, the arguments have been matched appropriately.
```
```r
| You can also explicitly specify arguments in a function. When you explicitly designate argument values by
| name, the ordering of the arguments becomes unimportant. You can try this out by typing: remainder(divisor
| = 11, num = 5).
```
```r
> remainder(divisor = 11, num = 5)
[1] 5

| You are really on a roll!
```
```r
| As you can see, there is a significant difference between remainder(11, 5) and remainder(divisor = 11, num
| = 5)!
```
```r
| R can also partially match arguments. Try typing remainder(4, div = 2) to see this feature in action.
```
```r
> remainder(4, div = 2)
[1] 0

| You are doing so well!
```
```r
| A word of warning: in general you want to make your code as easy to understand as possible. Switching
| around the orders of arguments by specifying their names or only using partial argument names can be
| confusing, so use these features with caution!
```
```r
| With all of this talk about arguments, you may be wondering if there is a way you can see a function's
| arguments (besides looking at the documentation). Thankfully, you can use the args() function! Type:
| args(remainder) to examine the arguments for the remainder function.
```
```r
> args(reminder)
Error in args(reminder) : object 'reminder' not found
> args(remainder)
function (num, divisor = 2)
NULL

| You got it!
```
```r
| You may not realize it but I just tricked you into doing something pretty interesting! args() is a
| function, remainder() is a function, yet remainder was an argument for args(). Yes it's true: you can pass
| functions as arguments! This is a very powerful concept. Let's write a script to see how it works.
```
```r
| Make sure to save your script before you type submit().

> submit()

| Sourcing your script...


| You're the best!
```
```r
| Let's take your new evaluate() function for a spin! Use evaluate to find the standard deviation of the
| vector c(1.4, 3.6, 7.9, 8.8).
```
```r
> evaluate(sd, c(1.4, 3.6, 7.9, 8.8))
[1] 3.514138

| You are quite good my friend!
```
```r
| The idea of passing functions as arguments to other functions is an important and fundamental concept in
| programming.
```
```r
| You may be surprised to learn that you can pass a function as an argument without first defining the passed
| function. Functions that are not named are appropriately known as anonymous functions.
```
```r
| Let's use the evaluate function to explore how anonymous functions work. For the first argument of the
| evaluate function we're going to write a tiny function that fits on one line. In the second argument we'll
| pass some data to the tiny anonymous function in the first argument.
```
```r
| Type the following command and then we'll discuss how it works: evaluate(function(x){x+1}, 6)
```
```r
> evaluate(function(x){x+1}, 6)
[1] 7

| You're the best!
```
```r
| The first argument is a tiny anonymous function that takes one argument `x` and returns `x+1`. We passed
| the number 6 into this function so the entire expression evaluates to 7.
```
```r
| Try using evaluate() along with an anonymous function to return the first element of the vector c(8, 4, 0).
| Your anonymous function should only take one argument which should be a variable `x`.
```
```r
> evaluate(function(x){x[1]}, c(8, 4, 0))
[1] 8

| Nice work!
```
```r
| Now try using evaluate() along with an anonymous function to return the last element of the vector c(8, 4,
| 0). Your anonymous function should only take one argument which should be a variable `x`.
```
```r
> evaluate(function(x){x[length(x)]}, c(8, 4, 0))
[1] 0

| You are really on a roll!
```
```r
| For the rest of the course we're going to use the paste() function frequently. Type ?paste so we can take a
| look at the documentation for the paste function.
```
```r
> ?paste

| Great job!
```
```r
| As you can see the first argument of paste() is `...` which is referred to as an ellipsis or simply
| dot-dot-dot. The ellipsis allows an indefinite number of arguments to be passed into a function. In the
| case of paste() any number of strings can be passed as arguments and paste() will return all of the strings
| combined into one string.
```
```r
| Just to see how paste() works, type paste("Programming", "is", "fun!")
```
```r
> paste("Programming", "is", "fun!")
[1] "Programming is fun!"

| You got it!
```
```r
| Time to write our own modified version of paste().
```
```r
| Make sure to save your script before you type submit().
```
```r
> submit()

| Sourcing your script...


| That's a job well done!
```
```r
| Now let's test out your telegram function. Use your new telegram function passing in whatever arguments you
| wish!
```
```r
> telegram('Hello')
[1] "START Hello STOP"

| You nailed it! Good job!
```
```r
| Make sure to save your script before you type submit().
```
```r
> submit()

| Sourcing your script...


| You are doing so well!
```
```r
| Time to use your mad_libs function. Make sure to name the place, adjective, and noun arguments in order for
| your function to work.
```
```r
> mad_libs(place='1', adjective = '2', noun = '3')
[1] "News from 1 today where 2 students took to the streets in protest of the new 3 being installed on campus."

| All that hard work is paying off!
```
```r
| We're coming to the end of this lesson, but there's still one more idea you should be made aware of.
```
```r
| You're familiar with adding, subtracting, multiplying, and dividing numbers in R. To do this you use the +,
| -, *, and / symbols. These symbols are called binary operators because they take two inputs, an input from
| the left and an input from the right.
```
```r
| In R you can define your own binary operators. In the next script I'll show you how.
```
```r
| Make sure to save your script before you type submit().
```
```r
> submit()

| Sourcing your script...


| You are doing so well!
```
```r
| You made your own binary operator! Let's test it out. Paste together the strings: 'I', 'love', 'R!' using
| your new binary operator.
```
```r
> 'I' %p% 'love' %p% 'R!'
[1] "I love R!"

| You are doing so well!
```
```r
| We've come to the end of our lesson! Go out there and write some great functions!
```
```r

## 10. lapply and sapply
```r
| In this lesson, you'll learn how to use lapply() and sapply(), the two most important members of R's *apply
| family of functions, also known as loop functions.
```
```r
| These powerful functions, along with their close relatives (vapply() and tapply(), among others) offer a
| concise and convenient means of implementing the Split-Apply-Combine strategy for data analysis.
```
```r
| Each of the *apply functions will SPLIT up some data into smaller pieces, APPLY a function to each piece,
| then COMBINE the results. A more detailed discussion of this strategy is found in Hadley Wickham's Journal
| of Statistical Software paper titled 'The Split-Apply-Combine Strategy for Data Analysis'.
```
```r
| Throughout this lesson, we'll use the Flags dataset from the UCI Machine Learning Repository. This dataset
| contains details of various nations and their flags. More information may be found here:
| http://archive.ics.uci.edu/ml/datasets/Flags
```
```r
| Let's jump right in so you can get a feel for how these special functions work!
```
```r
| I've stored the dataset in a variable called flags. Type head(flags) to preview the first six lines (i.e.
| the 'head') of the dataset.
```
```r
> head(flags)
            name landmass zone area population language religion bars stripes colours red green blue gold
1    Afghanistan        5    1  648         16       10        2    0       3       5   1     1    0    1
2        Albania        3    1   29          3        6        6    0       0       3   1     0    0    1
3        Algeria        4    1 2388         20        8        2    2       0       3   1     1    0    0
4 American-Samoa        6    3    0          0        1        1    0       0       5   1     0    1    1
5        Andorra        3    1    0          0        6        0    3       0       3   1     0    1    1
6         Angola        4    2 1247          7       10        5    0       2       3   1     0    0    1
  white black orange mainhue circles crosses saltires quarters sunstars crescent triangle icon animate text
1     1     1      0   green       0       0        0        0        1        0        0    1       0    0
2     0     1      0     red       0       0        0        0        1        0        0    0       1    0
3     1     0      0   green       0       0        0        0        1        1        0    0       0    0
4     1     0      1    blue       0       0        0        0        0        0        1    1       1    0
5     0     0      0    gold       0       0        0        0        0        0        0    0       0    0
6     0     1      0     red       0       0        0        0        1        0        0    1       0    0
  topleft botright
1   black    green
2     red      red
3   green    white
4    blue      red
5    blue      red
6     red    black

| Keep up the great work!
```
```r
| You may need to scroll up to see all of the output. Now, let's check out the dimensions of the dataset
| using dim(flags).
```
```r
> dim(flags)
[1] 194  30

| Nice work!
```
```r
| This tells us that there are 194 rows, or observations, and 30 columns, or variables. Each observation is a
| country and each variable describes some characteristic of that country or its flag. To open a more
| complete description of the dataset in a separate text file, type viewinfo() when you are back at the
| prompt (>).
```
```r
| As with any dataset, we'd like to know in what format the variables have been stored. In other words, what
| is the 'class' of each variable? What happens if we do class(flags)? Try it out.
```
```r
> class(flags)
[1] "data.frame"

| You got it!
```
```r
| That just tells us that the entire dataset is stored as a 'data.frame', which doesn't answer our question.
| What we really need is to call the class() function on each individual column. While we could do this
| manually (i.e. one column at a time) it's much faster if we can automate the process. Sounds like a loop!
```
```r
| The lapply() function takes a list as input, applies a function to each element of the list, then returns a
| list of the same length as the original one. Since a data frame is really just a list of vectors (you can
| see this with as.list(flags)), we can use lapply() to apply the class() function to each column of the
| flags dataset. Let's see it in action!
```
```r
| Type cls_list <- lapply(flags, class) to apply the class() function to each column of the flags dataset and
| store the result in a variable called cls_list. Note that you just supply the name of the function you want
| to apply (i.e. class), without the usual parentheses after it.
```
```r
> cls_list <- lapply(flags, class)

| You got it!
```
```r
| Type cls_list to view the result.
```
```r
> cls_list
$name
[1] "factor"

$landmass
[1] "integer"

$zone
[1] "integer"

$area
[1] "integer"

$population
[1] "integer"

$language
[1] "integer"

$religion
[1] "integer"

$bars
[1] "integer"

$stripes
[1] "integer"

$colours
[1] "integer"

$red
[1] "integer"

$green
[1] "integer"

$blue
[1] "integer"

$gold
[1] "integer"

$white
[1] "integer"

$black
[1] "integer"

$orange
[1] "integer"

$mainhue
[1] "factor"

$circles
[1] "integer"

$crosses
[1] "integer"

$saltires
[1] "integer"

$quarters
[1] "integer"

$sunstars
[1] "integer"

$crescent
[1] "integer"

$triangle
[1] "integer"

$icon
[1] "integer"

$animate
[1] "integer"

$text
[1] "integer"

$topleft
[1] "factor"

$botright
[1] "factor"


| That's the answer I was looking for.
```
```r
| The 'l' in 'lapply' stands for 'list'. Type class(cls_list) to confirm that lapply() returned a list.
```
```r
> class(cls_list)
[1] "list"

| Keep up the great work!
```
```r
| As expected, we got a list of length 30 -- one element for each variable/column. The output would be
| considerably more compact if we could represent it as a vector instead of a list.
```
```r
| You may remember from a previous lesson that lists are most helpful for storing multiple classes of data.
| In this case, since every element of the list returned by lapply() is a character vector of length one
| (i.e. "integer" and "vector"), cls_list can be simplified to a character vector. To do this manually, type
| as.character(cls_list).
```
```r
> as.character(cls_list)
 [1] "factor"  "integer" "integer" "integer" "integer" "integer" "integer" "integer" "integer" "integer"
[11] "integer" "integer" "integer" "integer" "integer" "integer" "integer" "factor"  "integer" "integer"
[21] "integer" "integer" "integer" "integer" "integer" "integer" "integer" "integer" "factor"  "factor"

| Perseverance, that's the answer.
```
```r
| sapply() allows you to automate this process by calling lapply() behind the scenes, but then attempting to
| simplify (hence the 's' in 'sapply') the result for you. Use sapply() the same way you used lapply() to get
| the class of each column of the flags dataset and store the result in cls_vect. If you need help, type
| ?sapply to bring up the documentation.
```
```r
> ?sapply
> cls_vect <- sapply(flags, class)

| You're the best!
```
```r
| Use class(cls_vect) to confirm that sapply() simplified the result to a character vector.
```
```r
> class(cls_vect)
[1] "character"

| You're the best!
```
```r
| In general, if the result is a list where every element is of length one, then sapply() returns a vector.
| If the result is a list where every element is a vector of the same length (> 1), sapply() returns a
| matrix. If sapply() can't figure things out, then it just returns a list, no different from what lapply()
| would give you.
```
```r
| Let's practice using lapply() and sapply() some more!
```
```r
| Columns 11 through 17 of our dataset are indicator variables, each representing a different color. The
| value of the indicator variable is 1 if the color is present in a country's flag and 0 otherwise.
```
```r
| Therefore, if we want to know the total number of countries (in our dataset) with, for example, the color
| orange on their flag, we can just add up all of the 1s and 0s in the 'orange' column. Try sum(flags$orange)
| to see this.
```
```r
> sum(flags$orange)
[1] 26

| You are doing so well!
```
```r
| Now we want to repeat this operation for each of the colors recorded in the dataset.
```
```r
| First, use flag_colors <- flags[, 11:17] to extract the columns containing the color data and store them in
| a new data frame called flag_colors. (Note the comma before 11:17. This subsetting command tells R that we
| want all rows, but only columns 11 through 17.)
```
```r
> flag_colors <- flags[, 11:17]

| That's a job well done!
```
```r
| Use the head() function to look at the first 6 lines of flag_colors.
```
```r
> head(flag_colors)
  red green blue gold white black orange
1   1     1    0    1     1     1      0
2   1     0    0    1     0     1      0
3   1     1    0    0     1     0      0
4   1     0    1    1     1     0      1
5   1     0    1    1     0     0      0
6   1     0    0    1     0     1      0

| You are amazing!
```
```r
| To get a list containing the sum of each column of flag_colors, call the lapply() function with two
| arguments. The first argument is the object over which we are looping (i.e. flag_colors) and the second
| argument is the name of the function we wish to apply to each column (i.e. sum). Remember that the second
| argument is just the name of the function with no parentheses, etc.
```
```r
> lapply(flag_colors, sum)
$red
[1] 153

$green
[1] 91

$blue
[1] 99

$gold
[1] 91

$white
[1] 146

$black
[1] 52

$orange
[1] 26


| Excellent work!
```
```r
| This tells us that of the 194 flags in our dataset, 153 contain the color red, 91 contain green, 99 contain
| blue, and so on.
```
```r
| The result is a list, since lapply() always returns a list. Each element of this list is of length one, so
| the result can be simplified to a vector by calling sapply() instead of lapply(). Try it now.
```
```r
> sapply(flag_colors, sum)
   red  green   blue   gold  white  black orange
   153     91     99     91    146     52     26

| You got it!
```
```r
| Perhaps it's more informative to find the proportion of flags (out of 194) containing each color. Since
| each column is just a bunch of 1s and 0s, the arithmetic mean of each column will give us the proportion of
| 1s. (If it's not clear why, think of a simpler situation where you have three 1s and two 0s -- (1 + 1 + 1 +
| 0 + 0)/5 = 3/5 = 0.6).
```
```r
| Use sapply() to apply the mean() function to each column of flag_colors. Remember that the second argument
| to sapply() should just specify the name of the function (i.e. mean) that you want to apply.
```
```r
> sapply(flag_colors, mean)
      red     green      blue      gold     white     black    orange
0.7886598 0.4690722 0.5103093 0.4690722 0.7525773 0.2680412 0.1340206

| All that hard work is paying off!
```
```r
| In the examples we've looked at so far, sapply() has been able to simplify the result to vector. That's
| because each element of the list returned by lapply() was a vector of length one. Recall that sapply()
| instead returns a matrix when each element of the list returned by lapply() is a vector of the same length
| (> 1).
```
```r
| To illustrate this, let's extract columns 19 through 23 from the flags dataset and store the result in a
| new data frame called flag_shapes. flag_shapes <- flags[, 19:23] will do it.
```
```r
> flag_shapes <- flags[, 19:23]

| Excellent job!
```
```r
| Each of these columns (i.e. variables) represents the number of times a particular shape or design appears
| on a country's flag. We are interested in the minimum and maximum number of times each shape or design
| appears.
```
```r
| The range() function returns the minimum and maximum of its first argument, which should be a numeric
| vector. Use lapply() to apply the range function to each column of flag_shapes. Don't worry about storing
| the result in a new variable. By now, we know that lapply() always returns a list.
```
```r
> lapply(flag_shapes, range)
$circles
[1] 0 4

$crosses
[1] 0 2

$saltires
[1] 0 1

$quarters
[1] 0 4

$sunstars
[1]  0 50


| Keep working like that and you'll get there!
```
```r
| Do the same operation, but using sapply() and store the result in a variable called shape_mat.
```
```r
> shape_mat <- sapply(flag_shapes, range)

| You got it!
```
```r
| View the contents of shape_mat.
```
```r
> shape_mat
     circles crosses saltires quarters sunstars
[1,]       0       0        0        0        0
[2,]       4       2        1        4       50

| Nice work!
```
```r
| Each column of shape_mat gives the minimum (row 1) and maximum (row 2) number of times its respective shape
| appears in different flags.
```
```r
| Use the class() function to confirm that shape_mat is a matrix.
```
```r
> class(shape_mat)
[1] "matrix"

| Excellent work!
```
```r
| As we've seen, sapply() always attempts to simplify the result given by lapply(). It has been successful in
| doing so for each of the examples we've looked at so far. Let's look at an example where sapply() can't
| figure out how to simplify the result and thus returns a list, no different from lapply().
```
```r
| When given a vector, the unique() function returns a vector with all duplicate elements removed. In other
| words, unique() returns a vector of only the 'unique' elements. To see how it works, try unique(c(3, 4, 5,
| 5, 5, 6, 6)).
```
```r
> unique(c(3, 4, 5, 5, 5, 6, 6))
[1] 3 4 5 6

| Excellent job!
```
```r
| We want to know the unique values for each variable in the flags dataset. To accomplish this, use lapply()
| to apply the unique() function to each column in the flags dataset, storing the result in a variable called
| unique_vals.
```
```r
> unique_vals <- lapply(flags, unique)

| Keep working like that and you'll get there!
```
```r
| Print the value of unique_vals to the console.
```
```r
> unique_vals
$name
  [1] Afghanistan              Albania                  Algeria                  American-Samoa          
  [5] Andorra                  Angola                   Anguilla                 Antigua-Barbuda         
  [9] Argentina                Argentine                Australia                Austria                 
 [13] Bahamas                  Bahrain                  Bangladesh               Barbados                
 [17] Belgium                  Belize                   Benin                    Bermuda                 
 [21] Bhutan                   Bolivia                  Botswana                 Brazil                  
 [25] British-Virgin-Isles     Brunei                   Bulgaria                 Burkina                 
 [29] Burma                    Burundi                  Cameroon                 Canada                  
 [33] Cape-Verde-Islands       Cayman-Islands           Central-African-Republic Chad                    
 [37] Chile                    China                    Colombia                 Comorro-Islands         
 [41] Congo                    Cook-Islands             Costa-Rica               Cuba                    
 [45] Cyprus                   Czechoslovakia           Denmark                  Djibouti                
 [49] Dominica                 Dominican-Republic       Ecuador                  Egypt                   
 [53] El-Salvador              Equatorial-Guinea        Ethiopia                 Faeroes                 
 [57] Falklands-Malvinas       Fiji                     Finland                  France                  
 [61] French-Guiana            French-Polynesia         Gabon                    Gambia                  
 [65] Germany-DDR              Germany-FRG              Ghana                    Gibraltar               
 [69] Greece                   Greenland                Grenada                  Guam                    
 [73] Guatemala                Guinea                   Guinea-Bissau            Guyana                  
 [77] Haiti                    Honduras                 Hong-Kong                Hungary                 
 [81] Iceland                  India                    Indonesia                Iran                    
 [85] Iraq                     Ireland                  Israel                   Italy                   
 [89] Ivory-Coast              Jamaica                  Japan                    Jordan                  
 [93] Kampuchea                Kenya                    Kiribati                 Kuwait                  
 [97] Laos                     Lebanon                  Lesotho                  Liberia                 
[101] Libya                    Liechtenstein            Luxembourg               Malagasy                
[105] Malawi                   Malaysia                 Maldive-Islands          Mali                    
[109] Malta                    Marianas                 Mauritania               Mauritius               
[113] Mexico                   Micronesia               Monaco                   Mongolia                
[117] Montserrat               Morocco                  Mozambique               Nauru                   
[121] Nepal                    Netherlands              Netherlands-Antilles     New-Zealand             
[125] Nicaragua                Niger                    Nigeria                  Niue                    
[129] North-Korea              North-Yemen              Norway                   Oman                    
[133] Pakistan                 Panama                   Papua-New-Guinea         Parguay                 
[137] Peru                     Philippines              Poland                   Portugal                
[141] Puerto-Rico              Qatar                    Romania                  Rwanda                  
[145] San-Marino               Sao-Tome                 Saudi-Arabia             Senegal                 
[149] Seychelles               Sierra-Leone             Singapore                Soloman-Islands         
[153] Somalia                  South-Africa             South-Korea              South-Yemen             
[157] Spain                    Sri-Lanka                St-Helena                St-Kitts-Nevis          
[161] St-Lucia                 St-Vincent               Sudan                    Surinam                 
[165] Swaziland                Sweden                   Switzerland              Syria                   
[169] Taiwan                   Tanzania                 Thailand                 Togo                    
[173] Tonga                    Trinidad-Tobago          Tunisia                  Turkey                  
[177] Turks-Cocos-Islands      Tuvalu                   UAE                      Uganda                  
[181] UK                       Uruguay                  US-Virgin-Isles          USA                     
[185] USSR                     Vanuatu                  Vatican-City             Venezuela               
[189] Vietnam                  Western-Samoa            Yugoslavia               Zaire                   
[193] Zambia                   Zimbabwe                
194 Levels: Afghanistan Albania Algeria American-Samoa Andorra Angola Anguilla Antigua-Barbuda ... Zimbabwe

$landmass
[1] 5 3 4 6 1 2

$zone
[1] 1 3 2 4

$area
  [1]   648    29  2388     0  1247  2777  7690    84    19     1   143    31    23   113    47  1099   600
 [18]  8512     6   111   274   678    28   474  9976     4   623  1284   757  9561  1139     2   342    51
 [35]   115     9   128    43    22    49   284  1001    21  1222    12    18   337   547    91   268    10
 [52]   108   249   239   132  2176   109   246    36   215   112    93   103  3268  1904  1648   435    70
 [69]   301   323    11   372    98   181   583   236    30  1760     3   587   118   333  1240  1031  1973
 [86]  1566   447   783   140    41  1267   925   121   195   324   212   804    76   463   407  1285   300
[103]   313    92   237    26  2150   196    72   637  1221    99   288   505    66  2506    63    17   450
[120]   185   945   514    57     5   164   781   245   178  9363 22402    15   912   256   905   753   391

$population
 [1]   16    3   20    0    7   28   15    8   90   10    1    6  119    9   35    4   24    2   11 1008    5
[22]   47   31   54   17   61   14  684  157   39   57  118   13   77   12   56   18   84   48   36   22   29
[43]   38   49   45  231  274   60

$language
 [1] 10  6  8  1  2  4  3  5  7  9

$religion
[1] 2 6 1 0 5 3 4 7

$bars
[1] 0 2 3 1 5

$stripes
 [1]  3  0  2  1  5  9 11 14  4  6 13  7

$colours
[1] 5 3 2 8 6 4 7 1

$red
[1] 1 0

$green
[1] 1 0

$blue
[1] 0 1

$gold
[1] 1 0

$white
[1] 1 0

$black
[1] 1 0

$orange
[1] 0 1

$mainhue
[1] green  red    blue   gold   white  orange black  brown
Levels: black blue brown gold green orange red white

$circles
[1] 0 1 4 2

$crosses
[1] 0 1 2

$saltires
[1] 0 1

$quarters
[1] 0 1 4

$sunstars
 [1]  1  0  6 22 14  3  4  5 15 10  7  2  9 50

$crescent
[1] 0 1

$triangle
[1] 0 1

$icon
[1] 1 0

$animate
[1] 0 1

$text
[1] 0 1

$topleft
[1] black  red    green  blue   white  orange gold  
Levels: black blue gold green orange red white

$botright
[1] green  red    white  black  blue   gold   orange brown
Levels: black blue brown gold green orange red white


| You are quite good my friend!
```
```r
| Since unique_vals is a list, you can use what you've learned to determine the length of each element of
| unique_vals (i.e. the number of unique values for each variable). Simplify the result, if possible. Hint:
| Apply the length() function to each element of unique_vals.
```
```r
> sapply(unique_vals, length)
      name   landmass       zone       area population   language   religion       bars    stripes    colours
       194          6          4        136         48         10          8          5         12          8
       red      green       blue       gold      white      black     orange    mainhue    circles    crosses
         2          2          2          2          2          2          2          8          4          3
  saltires   quarters   sunstars   crescent   triangle       icon    animate       text    topleft   botright
         2          3         14          2          2          2          2          2          7          8

| Great job!
```
```r
| The fact that the elements of the unique_vals list are all vectors of *different* length poses a problem
| for sapply(), since there's no obvious way of simplifying the result.
```
```r
| Use sapply() to apply the unique() function to each column of the flags dataset to see that you get the
| same unsimplified list that you got from lapply().
```
```r
> sapply(flags, unique)
$name
  [1] Afghanistan              Albania                  Algeria                  American-Samoa          
  [5] Andorra                  Angola                   Anguilla                 Antigua-Barbuda         
  [9] Argentina                Argentine                Australia                Austria                 
 [13] Bahamas                  Bahrain                  Bangladesh               Barbados                
 [17] Belgium                  Belize                   Benin                    Bermuda                 
 [21] Bhutan                   Bolivia                  Botswana                 Brazil                  
 [25] British-Virgin-Isles     Brunei                   Bulgaria                 Burkina                 
 [29] Burma                    Burundi                  Cameroon                 Canada                  
 [33] Cape-Verde-Islands       Cayman-Islands           Central-African-Republic Chad                    
 [37] Chile                    China                    Colombia                 Comorro-Islands         
 [41] Congo                    Cook-Islands             Costa-Rica               Cuba                    
 [45] Cyprus                   Czechoslovakia           Denmark                  Djibouti                
 [49] Dominica                 Dominican-Republic       Ecuador                  Egypt                   
 [53] El-Salvador              Equatorial-Guinea        Ethiopia                 Faeroes                 
 [57] Falklands-Malvinas       Fiji                     Finland                  France                  
 [61] French-Guiana            French-Polynesia         Gabon                    Gambia                  
 [65] Germany-DDR              Germany-FRG              Ghana                    Gibraltar               
 [69] Greece                   Greenland                Grenada                  Guam                    
 [73] Guatemala                Guinea                   Guinea-Bissau            Guyana                  
 [77] Haiti                    Honduras                 Hong-Kong                Hungary                 
 [81] Iceland                  India                    Indonesia                Iran                    
 [85] Iraq                     Ireland                  Israel                   Italy                   
 [89] Ivory-Coast              Jamaica                  Japan                    Jordan                  
 [93] Kampuchea                Kenya                    Kiribati                 Kuwait                  
 [97] Laos                     Lebanon                  Lesotho                  Liberia                 
[101] Libya                    Liechtenstein            Luxembourg               Malagasy                
[105] Malawi                   Malaysia                 Maldive-Islands          Mali                    
[109] Malta                    Marianas                 Mauritania               Mauritius               
[113] Mexico                   Micronesia               Monaco                   Mongolia                
[117] Montserrat               Morocco                  Mozambique               Nauru                   
[121] Nepal                    Netherlands              Netherlands-Antilles     New-Zealand             
[125] Nicaragua                Niger                    Nigeria                  Niue                    
[129] North-Korea              North-Yemen              Norway                   Oman                    
[133] Pakistan                 Panama                   Papua-New-Guinea         Parguay                 
[137] Peru                     Philippines              Poland                   Portugal                
[141] Puerto-Rico              Qatar                    Romania                  Rwanda                  
[145] San-Marino               Sao-Tome                 Saudi-Arabia             Senegal                 
[149] Seychelles               Sierra-Leone             Singapore                Soloman-Islands         
[153] Somalia                  South-Africa             South-Korea              South-Yemen             
[157] Spain                    Sri-Lanka                St-Helena                St-Kitts-Nevis          
[161] St-Lucia                 St-Vincent               Sudan                    Surinam                 
[165] Swaziland                Sweden                   Switzerland              Syria                   
[169] Taiwan                   Tanzania                 Thailand                 Togo                    
[173] Tonga                    Trinidad-Tobago          Tunisia                  Turkey                  
[177] Turks-Cocos-Islands      Tuvalu                   UAE                      Uganda                  
[181] UK                       Uruguay                  US-Virgin-Isles          USA                     
[185] USSR                     Vanuatu                  Vatican-City             Venezuela               
[189] Vietnam                  Western-Samoa            Yugoslavia               Zaire                   
[193] Zambia                   Zimbabwe                
194 Levels: Afghanistan Albania Algeria American-Samoa Andorra Angola Anguilla Antigua-Barbuda ... Zimbabwe

$landmass
[1] 5 3 4 6 1 2

$zone
[1] 1 3 2 4

$area
  [1]   648    29  2388     0  1247  2777  7690    84    19     1   143    31    23   113    47  1099   600
 [18]  8512     6   111   274   678    28   474  9976     4   623  1284   757  9561  1139     2   342    51
 [35]   115     9   128    43    22    49   284  1001    21  1222    12    18   337   547    91   268    10
 [52]   108   249   239   132  2176   109   246    36   215   112    93   103  3268  1904  1648   435    70
 [69]   301   323    11   372    98   181   583   236    30  1760     3   587   118   333  1240  1031  1973
 [86]  1566   447   783   140    41  1267   925   121   195   324   212   804    76   463   407  1285   300
[103]   313    92   237    26  2150   196    72   637  1221    99   288   505    66  2506    63    17   450
[120]   185   945   514    57     5   164   781   245   178  9363 22402    15   912   256   905   753   391

$population
 [1]   16    3   20    0    7   28   15    8   90   10    1    6  119    9   35    4   24    2   11 1008    5
[22]   47   31   54   17   61   14  684  157   39   57  118   13   77   12   56   18   84   48   36   22   29
[43]   38   49   45  231  274   60

$language
 [1] 10  6  8  1  2  4  3  5  7  9

$religion
[1] 2 6 1 0 5 3 4 7

$bars
[1] 0 2 3 1 5

$stripes
 [1]  3  0  2  1  5  9 11 14  4  6 13  7

$colours
[1] 5 3 2 8 6 4 7 1

$red
[1] 1 0

$green
[1] 1 0

$blue
[1] 0 1

$gold
[1] 1 0

$white
[1] 1 0

$black
[1] 1 0

$orange
[1] 0 1

$mainhue
[1] green  red    blue   gold   white  orange black  brown
Levels: black blue brown gold green orange red white

$circles
[1] 0 1 4 2

$crosses
[1] 0 1 2

$saltires
[1] 0 1

$quarters
[1] 0 1 4

$sunstars
 [1]  1  0  6 22 14  3  4  5 15 10  7  2  9 50

$crescent
[1] 0 1

$triangle
[1] 0 1

$icon
[1] 1 0

$animate
[1] 0 1

$text
[1] 0 1

$topleft
[1] black  red    green  blue   white  orange gold  
Levels: black blue gold green orange red white

$botright
[1] green  red    white  black  blue   gold   orange brown
Levels: black blue brown gold green orange red white


| You are quite good my friend!
```
```r
| Occasionally, you may need to apply a function that is not yet defined, thus requiring you to write your
| own. Writing functions in R is beyond the scope of this lesson, but let's look at a quick example of how
| you might do so in the context of loop functions.
```
```r
| Pretend you are interested in only the second item from each element of the unique_vals list that you just
| created. Since each element of the unique_vals list is a vector and we're not aware of any built-in
| function in R that returns the second element of a vector, we will construct our own function.
```
```r
| lapply(unique_vals, function(elem) elem[2]) will return a list containing the second item from each element
| of the unique_vals list. Note that our function takes one argument, elem, which is just a 'dummy variable'
| that takes on the value of each element of unique_vals, in turn.
```
```r
> lapply(unique_vals, function(elem) elem[2])
$name
[1] Albania
194 Levels: Afghanistan Albania Algeria American-Samoa Andorra Angola Anguilla Antigua-Barbuda ... Zimbabwe

$landmass
[1] 3

$zone
[1] 3

$area
[1] 29

$population
[1] 3

$language
[1] 6

$religion
[1] 6

$bars
[1] 2

$stripes
[1] 0

$colours
[1] 3

$red
[1] 0

$green
[1] 0

$blue
[1] 1

$gold
[1] 0

$white
[1] 0

$black
[1] 0

$orange
[1] 1

$mainhue
[1] red
Levels: black blue brown gold green orange red white

$circles
[1] 1

$crosses
[1] 1

$saltires
[1] 1

$quarters
[1] 1

$sunstars
[1] 0

$crescent
[1] 1

$triangle
[1] 1

$icon
[1] 0

$animate
[1] 1

$text
[1] 1

$topleft
[1] red
Levels: black blue gold green orange red white

$botright
[1] red
Levels: black blue brown gold green orange red white


| You got it!
```
```r
| The only difference between previous examples and this one is that we are defining and using our own
| function right in the call to lapply(). Our function has no name and disappears as soon as lapply() is done
| using it. So-called 'anonymous functions' can be very useful when one of R's built-in functions isn't an
| option.
```
```r
| In this lesson, you learned how to use the powerful lapply() and sapply() functions to apply an operation
| over the elements of a list. In the next lesson, we'll take a look at some close relatives of lapply() and
| sapply().
```

## 11. vapply and tapply
```r
| In the last lesson, you learned about the two most fundamental members of R's *apply family of functions:
| lapply() and sapply(). Both take a list as input, apply a function to each element of the list, then
| combine and return the result. lapply() always returns a list, whereas sapply() attempts to simplify the
| result.
```
```r
| In this lesson, you'll learn how to use vapply() and tapply(), each of which serves a very specific purpose
| within the Split-Apply-Combine methodology. For consistency, we'll use the same dataset we used in the
| 'lapply and sapply' lesson.
```
```r
| The Flags dataset from the UCI Machine Learning Repository contains details of various nations and their
| flags. More information may be found here: http://archive.ics.uci.edu/ml/datasets/Flags
```
```r
| I've stored the data in a variable called flags. If it's been a while since you completed the 'lapply and
| sapply' lesson, you may want to reacquaint yourself with the data by using functions like dim(), head(),
| str(), and summary() when you return to the prompt (>). You can also type viewinfo() at the prompt to bring
| up some documentation for the dataset. Let's get started!
```
```r
| As you saw in the last lesson, the unique() function returns a vector of the unique values contained in the
| object passed to it. Therefore, sapply(flags, unique) returns a list containing one vector of unique values
| for each column of the flags dataset. Try it again now.
```
```r
> sapply(flags, unique)
$name
  [1] Afghanistan              Albania                  Algeria                  American-Samoa          
  [5] Andorra                  Angola                   Anguilla                 Antigua-Barbuda         
  [9] Argentina                Argentine                Australia                Austria                 
 [13] Bahamas                  Bahrain                  Bangladesh               Barbados                
 [17] Belgium                  Belize                   Benin                    Bermuda                 
 [21] Bhutan                   Bolivia                  Botswana                 Brazil                  
 [25] British-Virgin-Isles     Brunei                   Bulgaria                 Burkina                 
 [29] Burma                    Burundi                  Cameroon                 Canada                  
 [33] Cape-Verde-Islands       Cayman-Islands           Central-African-Republic Chad                    
 [37] Chile                    China                    Colombia                 Comorro-Islands         
 [41] Congo                    Cook-Islands             Costa-Rica               Cuba                    
 [45] Cyprus                   Czechoslovakia           Denmark                  Djibouti                
 [49] Dominica                 Dominican-Republic       Ecuador                  Egypt                   
 [53] El-Salvador              Equatorial-Guinea        Ethiopia                 Faeroes                 
 [57] Falklands-Malvinas       Fiji                     Finland                  France                  
 [61] French-Guiana            French-Polynesia         Gabon                    Gambia                  
 [65] Germany-DDR              Germany-FRG              Ghana                    Gibraltar               
 [69] Greece                   Greenland                Grenada                  Guam                    
 [73] Guatemala                Guinea                   Guinea-Bissau            Guyana                  
 [77] Haiti                    Honduras                 Hong-Kong                Hungary                 
 [81] Iceland                  India                    Indonesia                Iran                    
 [85] Iraq                     Ireland                  Israel                   Italy                   
 [89] Ivory-Coast              Jamaica                  Japan                    Jordan                  
 [93] Kampuchea                Kenya                    Kiribati                 Kuwait                  
 [97] Laos                     Lebanon                  Lesotho                  Liberia                 
[101] Libya                    Liechtenstein            Luxembourg               Malagasy                
[105] Malawi                   Malaysia                 Maldive-Islands          Mali                    
[109] Malta                    Marianas                 Mauritania               Mauritius               
[113] Mexico                   Micronesia               Monaco                   Mongolia                
[117] Montserrat               Morocco                  Mozambique               Nauru                   
[121] Nepal                    Netherlands              Netherlands-Antilles     New-Zealand             
[125] Nicaragua                Niger                    Nigeria                  Niue                    
[129] North-Korea              North-Yemen              Norway                   Oman                    
[133] Pakistan                 Panama                   Papua-New-Guinea         Parguay                 
[137] Peru                     Philippines              Poland                   Portugal                
[141] Puerto-Rico              Qatar                    Romania                  Rwanda                  
[145] San-Marino               Sao-Tome                 Saudi-Arabia             Senegal                 
[149] Seychelles               Sierra-Leone             Singapore                Soloman-Islands         
[153] Somalia                  South-Africa             South-Korea              South-Yemen             
[157] Spain                    Sri-Lanka                St-Helena                St-Kitts-Nevis          
[161] St-Lucia                 St-Vincent               Sudan                    Surinam                 
[165] Swaziland                Sweden                   Switzerland              Syria                   
[169] Taiwan                   Tanzania                 Thailand                 Togo                    
[173] Tonga                    Trinidad-Tobago          Tunisia                  Turkey                  
[177] Turks-Cocos-Islands      Tuvalu                   UAE                      Uganda                  
[181] UK                       Uruguay                  US-Virgin-Isles          USA                     
[185] USSR                     Vanuatu                  Vatican-City             Venezuela               
[189] Vietnam                  Western-Samoa            Yugoslavia               Zaire                   
[193] Zambia                   Zimbabwe                
194 Levels: Afghanistan Albania Algeria American-Samoa Andorra Angola Anguilla Antigua-Barbuda ... Zimbabwe

$landmass
[1] 5 3 4 6 1 2

$zone
[1] 1 3 2 4

$area
  [1]   648    29  2388     0  1247  2777  7690    84    19     1   143    31    23   113    47  1099   600
 [18]  8512     6   111   274   678    28   474  9976     4   623  1284   757  9561  1139     2   342    51
 [35]   115     9   128    43    22    49   284  1001    21  1222    12    18   337   547    91   268    10
 [52]   108   249   239   132  2176   109   246    36   215   112    93   103  3268  1904  1648   435    70
 [69]   301   323    11   372    98   181   583   236    30  1760     3   587   118   333  1240  1031  1973
 [86]  1566   447   783   140    41  1267   925   121   195   324   212   804    76   463   407  1285   300
[103]   313    92   237    26  2150   196    72   637  1221    99   288   505    66  2506    63    17   450
[120]   185   945   514    57     5   164   781   245   178  9363 22402    15   912   256   905   753   391

$population
 [1]   16    3   20    0    7   28   15    8   90   10    1    6  119    9   35    4   24    2   11 1008    5
[22]   47   31   54   17   61   14  684  157   39   57  118   13   77   12   56   18   84   48   36   22   29
[43]   38   49   45  231  274   60

$language
 [1] 10  6  8  1  2  4  3  5  7  9

$religion
[1] 2 6 1 0 5 3 4 7

$bars
[1] 0 2 3 1 5

$stripes
 [1]  3  0  2  1  5  9 11 14  4  6 13  7

$colours
[1] 5 3 2 8 6 4 7 1

$red
[1] 1 0

$green
[1] 1 0

$blue
[1] 0 1

$gold
[1] 1 0

$white
[1] 1 0

$black
[1] 1 0

$orange
[1] 0 1

$mainhue
[1] green  red    blue   gold   white  orange black  brown
Levels: black blue brown gold green orange red white

$circles
[1] 0 1 4 2

$crosses
[1] 0 1 2

$saltires
[1] 0 1

$quarters
[1] 0 1 4

$sunstars
 [1]  1  0  6 22 14  3  4  5 15 10  7  2  9 50

$crescent
[1] 0 1

$triangle
[1] 0 1

$icon
[1] 1 0

$animate
[1] 0 1

$text
[1] 0 1

$topleft
[1] black  red    green  blue   white  orange gold  
Levels: black blue gold green orange red white

$botright
[1] green  red    white  black  blue   gold   orange brown
Levels: black blue brown gold green orange red white


| All that practice is paying off!
```
```r
| What if you had forgotten how unique() works and mistakenly thought it returns the *number* of unique
| values contained in the object passed to it? Then you might have incorrectly expected sapply(flags, unique)
| to return a numeric vector, since each element of the list returned would contain a single number and
| sapply() could then simplify the result to a vector.
```
```r
| When working interactively (at the prompt), this is not much of a problem, since you see the result
| immediately and will quickly recognize your mistake. However, when working non-interactively (e.g. writing
| your own functions), a misunderstanding may go undetected and cause incorrect results later on. Therefore,
| you may wish to be more careful and that's where vapply() is useful.
```
```r
| Whereas sapply() tries to 'guess' the correct format of the result, vapply() allows you to specify it
| explicitly. If the result doesn't match the format you specify, vapply() will throw an error, causing the
| operation to stop. This can prevent significant problems in your code that might be caused by getting
| unexpected return values from sapply().
```
```r
| Try vapply(flags, unique, numeric(1)), which says that you expect each element of the result to be a
| numeric vector of length 1. Since this is NOT actually the case, YOU WILL GET AN ERROR. Once you get the
| error, type ok() to continue to the next question.
```
```r
> vapply(flags, unique, numeric(1))
Error in vapply(flags, unique, numeric(1)) : values must be length 1,
 but FUN(X[[1]]) result is length 194
> ok()

| Nice work!
```
```r
| Recall from the previous lesson that sapply(flags, class) will return a character vector containing the
| class of each column in the dataset. Try that again now to see the result.
```
```r
> sapply(flags, class)
      name   landmass       zone       area population   language   religion       bars    stripes    colours
  "factor"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"
       red      green       blue       gold      white      black     orange    mainhue    circles    crosses
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"   "factor"  "integer"  "integer"
  saltires   quarters   sunstars   crescent   triangle       icon    animate       text    topleft   botright
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"   "factor"   "factor"

| You're the best!
```
```r
| If we wish to be explicit about the format of the result we expect, we can use vapply(flags, class,
| character(1)). The 'character(1)' argument tells R that we expect the class function to return a character
| vector of length 1 when applied to EACH column of the flags dataset. Try it now.
```
```r
> vapply(flags, class, character(1))
      name   landmass       zone       area population   language   religion       bars    stripes    colours
  "factor"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"
       red      green       blue       gold      white      black     orange    mainhue    circles    crosses
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"   "factor"  "integer"  "integer"
  saltires   quarters   sunstars   crescent   triangle       icon    animate       text    topleft   botright
 "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"  "integer"   "factor"   "factor"

| Keep up the great work!
```
```r
| Note that since our expectation was correct (i.e. character(1)), the vapply() result is identical to the
| sapply() result -- a character vector of column classes.
```
```r
| You might think of vapply() as being 'safer' than sapply(), since it requires you to specify the format of
| the output in advance, instead of just allowing R to 'guess' what you wanted. In addition, vapply() may
| perform faster than sapply() for large datasets. However, when doing data analysis interactively (at the
| prompt), sapply() saves you some typing and will often be good enough.
```
```r
| As a data analyst, you'll often wish to split your data up into groups based on the value of some variable,
| then apply a function to the members of each group. The next function we'll look at, tapply(), does exactly
| that.
```
```r
| Use ?tapply to pull up the documentation.
```
```r
> ?tapply

| Excellent work!
```
```r
| The 'landmass' variable in our dataset takes on integer values between 1 and 6, each of which represents a
| different part of the world. Use table(flags$landmass) to see how many flags/countries fall into each
| group.
```
```r
> table(flags$landmass)

 1  2  3  4  5  6
31 17 35 52 39 20

| Excellent work!
```
```r
| The 'animate' variable in our dataset takes the value 1 if a country's flag contains an animate image (e.g.
| an eagle, a tree, a human hand) and 0 otherwise. Use table(flags$animate) to see how many flags contain an
| animate image.
```
```r
> table(flags$animate)

  0   1
155  39

| You are amazing!
```
```r
| This tells us that 39 flags contain an animate object (animate = 1) and 155 do not (animate = 0).
```
```r
| If you take the arithmetic mean of a bunch of 0s and 1s, you get the proportion of 1s. Use
| tapply(flags$animate, flags$landmass, mean) to apply the mean function to the 'animate' variable separately
| for each of the six landmass groups, thus giving us the proportion of flags containing an animate image
| WITHIN each landmass group.
```
```r
> tapply(flags$animate, flags$landmass, mean)
        1         2         3         4         5         6
0.4193548 0.1764706 0.1142857 0.1346154 0.1538462 0.3000000

| Perseverance, that's the answer.
```
```r
| The first landmass group (landmass = 1) corresponds to North America and contains the highest proportion of
| flags with an animate image (0.4194).
```
```r
| Similarly, we can look at a summary of population values (in round millions) for countries with and without
| the color red on their flag with tapply(flags$population, flags$red, summary).
```
```r
> tapply(flags$population, flags$red, summary)
$`0`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
   0.00    0.00    3.00   27.63    9.00  684.00

$`1`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
    0.0     0.0     4.0    22.1    15.0  1008.0


| You got it right!
```
```r
| What is the median population (in millions) for countries *without* the color red on their flag?

1: 0.0
2: 27.6
3: 4.0
4: 9.0
5: 22.1
6: 3.0

Selection: 6

| You are quite good my friend!
```
```r
| Lastly, use the same approach to look at a summary of population values for each of the six landmasses.
```
```r
> tapply(flags$population, flags$landmass, summary)
$`1`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
   0.00    0.00    0.00   12.29    4.50  231.00

$`2`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
   0.00    1.00    6.00   15.71   15.00  119.00

$`3`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
   0.00    0.00    8.00   13.86   16.00   61.00

$`4`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
  0.000   1.000   5.000   8.788   9.750  56.000

$`5`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
   0.00    2.00   10.00   69.18   39.00 1008.00

$`6`
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
   0.00    0.00    0.00   11.30    1.25  157.00


| That's correct!
```
```r
| What is the maximum population (in millions) for the fourth landmass group (Africa)?

1: 5.00
2: 119.0
3: 56.00
4: 157.00
5: 1010.0
```
```r
Selection: 3

| Nice work!
```
```r
| In this lesson, you learned how to use vapply() as a safer alternative to sapply(), which is most helpful
| when writing your own functions. You also learned how to use tapply() to split your data into groups based
| on the value of some variable, then apply a function to each group. These functions will come in handy on
| your quest to become a better data analyst.
```

## 12. Looking at Data
```r
| Whenever you're working with a new dataset, the first thing you should do is look at it! What is the format
| of the data? What are the dimensions? What are the variable names? How are the variables stored? Are there
| missing data? Are there any flaws in the data?
```
```r
| This lesson will teach you how to answer these questions and more using R's built-in functions. We'll be
| using a dataset constructed from the United States Department of Agriculture's PLANTS Database
| (http://plants.usda.gov/adv_search.html).
```
```r
| I've stored the data for you in a variable called plants. Type ls() to list the variables in your
| workspace, among which should be plants.
```
```r
> ls()
 [1] "%p%"             "boring_function" "cls_list"        "cls_vect"        "cnames"         
 [6] "evaluate"        "flag_colors"     "flag_shapes"     "flags"           "ints"           
[11] "mad_libs"        "my_char"         "my_data"         "my_div"          "my_matrix"      
[16] "my_matrix2"      "my_mean"         "my_na"           "my_name"         "my_seq"         
[21] "my_sqrt"         "my_vector"       "num_vect"        "ok"              "old.dir"        
[26] "patients"        "plants"          "remainder"       "shape_mat"       "telegram"       
[31] "tf"              "unique_vals"     "vect"            "vect2"           "viewinfo"       
[36] "x"               "y"               "z"              

| You are doing so well!
```
```r
| Let's begin by checking the class of the plants variable with class(plants). This will give us a clue as to
| the overall structure of the data.
```
```r
> class(plants)
[1] "data.frame"

| You got it right!
```
```r
| It's very common for data to be stored in a data frame. It is the default class for data read into R using
| functions like read.csv() and read.table(), which you'll learn about in another lesson.
```
```r
| Since the dataset is stored in a data frame, we know it is rectangular. In other words, it has two
| dimensions (rows and columns) and fits neatly into a table or spreadsheet. Use dim(plants) to see exactly
| how many rows and columns we're dealing with.
```
```r
> dim(plants)
[1] 5166   10

| Excellent job!
```
```r
| The first number you see (5166) is the number of rows (observations) and the second number (10) is the
| number of columns (variables).
```
```r
| You can also use nrow(plants) to see only the number of rows. Try it out.
```
```r
> nrow(plants)
[1] 5166

| You got it right!
```
```r
| ... And ncol(plants) to see only the number of columns.
```
```r
> ncol(plants)
[1] 10

| You got it!
```
```r
| If you are curious as to how much space the dataset is occupying in memory, you can use
| object.size(plants).
```
```r
> object.size(plants)
686080 bytes

| Keep working like that and you'll get there!
```
```r
| Now that we have a sense of the shape and size of the dataset, let's get a feel for what's inside.
| names(plants) will return a character vector of column (i.e. variable) names. Give it a shot.
```
```r
> names(plants)
 [1] "Scientific_Name"      "Duration"             "Active_Growth_Period" "Foliage_Color"       
 [5] "pH_Min"               "pH_Max"               "Precip_Min"           "Precip_Max"          
 [9] "Shade_Tolerance"      "Temp_Min_F"          

| Nice work!
```
```r
| We've applied fairly descriptive variable names to this dataset, but that won't always be the case. A
| logical next step is to peek at the actual data. However, our dataset contains over 5000 observations
| (rows), so it's impractical to view the whole thing all at once.
```
```r
| The head() function allows you to preview the top of the dataset. Give it a try with only one argument.
```
```r
> head(plants)
               Scientific_Name          Duration Active_Growth_Period Foliage_Color pH_Min pH_Max Precip_Min
1                  Abelmoschus              <NA>                 <NA>          <NA>     NA     NA         NA
2       Abelmoschus esculentus Annual, Perennial                 <NA>          <NA>     NA     NA         NA
3                        Abies              <NA>                 <NA>          <NA>     NA     NA         NA
4               Abies balsamea         Perennial    Spring and Summer         Green      4      6         13
5 Abies balsamea var. balsamea         Perennial                 <NA>          <NA>     NA     NA         NA
6                     Abutilon              <NA>                 <NA>          <NA>     NA     NA         NA
  Precip_Max Shade_Tolerance Temp_Min_F
1         NA            <NA>         NA
2         NA            <NA>         NA
3         NA            <NA>         NA
4         60        Tolerant        -43
5         NA            <NA>         NA
6         NA            <NA>         NA

| You are quite good my friend!
```
```r
| Take a minute to look through and understand the output above. Each row is labeled with the observation
| number and each column with the variable name. Your screen is probably not wide enough to view all 10
| columns side-by-side, in which case R displays as many columns as it can on each line before continuing on
| the next.
```
```r
| By default, head() shows you the first six rows of the data. You can alter this behavior by passing as a
| second argument the number of rows you'd like to view. Use head() to preview the first 10 rows of plants.
```
```r
> head(plants, 10)
                     Scientific_Name          Duration Active_Growth_Period Foliage_Color pH_Min pH_Max
1                        Abelmoschus              <NA>                 <NA>          <NA>     NA     NA
2             Abelmoschus esculentus Annual, Perennial                 <NA>          <NA>     NA     NA
3                              Abies              <NA>                 <NA>          <NA>     NA     NA
4                     Abies balsamea         Perennial    Spring and Summer         Green      4    6.0
5       Abies balsamea var. balsamea         Perennial                 <NA>          <NA>     NA     NA
6                           Abutilon              <NA>                 <NA>          <NA>     NA     NA
7               Abutilon theophrasti            Annual                 <NA>          <NA>     NA     NA
8                             Acacia              <NA>                 <NA>          <NA>     NA     NA
9                  Acacia constricta         Perennial    Spring and Summer         Green      7    8.5
10 Acacia constricta var. constricta         Perennial                 <NA>          <NA>     NA     NA
   Precip_Min Precip_Max Shade_Tolerance Temp_Min_F
1          NA         NA            <NA>         NA
2          NA         NA            <NA>         NA
3          NA         NA            <NA>         NA
4          13         60        Tolerant        -43
5          NA         NA            <NA>         NA
6          NA         NA            <NA>         NA
7          NA         NA            <NA>         NA
8          NA         NA            <NA>         NA
9           4         20      Intolerant        -13
10         NA         NA            <NA>         NA

| You got it!
```
```r
| The same applies for using tail() to preview the end of the dataset. Use tail() to view the last 15 rows.
```
```r
> tail(plants, 15)
                      Scientific_Name  Duration Active_Growth_Period Foliage_Color pH_Min pH_Max Precip_Min
5152                          Zizania      <NA>                 <NA>          <NA>     NA     NA         NA
5153                 Zizania aquatica    Annual               Spring         Green    6.4    7.4         30
5154   Zizania aquatica var. aquatica    Annual                 <NA>          <NA>     NA     NA         NA
5155                Zizania palustris    Annual                 <NA>          <NA>     NA     NA         NA
5156 Zizania palustris var. palustris    Annual                 <NA>          <NA>     NA     NA         NA
5157                      Zizaniopsis      <NA>                 <NA>          <NA>     NA     NA         NA
5158             Zizaniopsis miliacea Perennial    Spring and Summer         Green    4.3    9.0         35
5159                            Zizia      <NA>                 <NA>          <NA>     NA     NA         NA
5160                     Zizia aptera Perennial                 <NA>          <NA>     NA     NA         NA
5161                      Zizia aurea Perennial                 <NA>          <NA>     NA     NA         NA
5162                 Zizia trifoliata Perennial                 <NA>          <NA>     NA     NA         NA
5163                          Zostera      <NA>                 <NA>          <NA>     NA     NA         NA
5164                   Zostera marina Perennial                 <NA>          <NA>     NA     NA         NA
5165                           Zoysia      <NA>                 <NA>          <NA>     NA     NA         NA
5166                  Zoysia japonica Perennial                 <NA>          <NA>     NA     NA         NA
     Precip_Max Shade_Tolerance Temp_Min_F
5152         NA            <NA>         NA
5153         50      Intolerant         32
5154         NA            <NA>         NA
5155         NA            <NA>         NA
5156         NA            <NA>         NA
5157         NA            <NA>         NA
5158         70      Intolerant         12
5159         NA            <NA>         NA
5160         NA            <NA>         NA
5161         NA            <NA>         NA
5162         NA            <NA>         NA
5163         NA            <NA>         NA
5164         NA            <NA>         NA
5165         NA            <NA>         NA
5166         NA            <NA>         NA

| All that practice is paying off!
```
```r
| After previewing the top and bottom of the data, you probably noticed lots of NAs, which are R's
| placeholders for missing values. Use summary(plants) to get a better feel for how each variable is
| distributed and how much of the dataset is missing.
```
```r
> summary(plants)
                     Scientific_Name              Duration              Active_Growth_Period
 Abelmoschus                 :   1   Perennial        :3031   Spring and Summer   : 447     
 Abelmoschus esculentus      :   1   Annual           : 682   Spring              : 144     
 Abies                       :   1   Annual, Perennial: 179   Spring, Summer, Fall:  95     
 Abies balsamea              :   1   Annual, Biennial :  95   Summer              :  92     
 Abies balsamea var. balsamea:   1   Biennial         :  57   Summer and Fall     :  24     
 Abutilon                    :   1   (Other)          :  92   (Other)             :  30     
 (Other)                     :5160   NA's             :1030   NA's                :4334     
      Foliage_Color      pH_Min          pH_Max         Precip_Min      Precip_Max         Shade_Tolerance
 Dark Green  :  82   Min.   :3.000   Min.   : 5.100   Min.   : 4.00   Min.   : 16.00   Intermediate: 242  
 Gray-Green  :  25   1st Qu.:4.500   1st Qu.: 7.000   1st Qu.:16.75   1st Qu.: 55.00   Intolerant  : 349  
 Green       : 692   Median :5.000   Median : 7.300   Median :28.00   Median : 60.00   Tolerant    : 246  
 Red         :   4   Mean   :4.997   Mean   : 7.344   Mean   :25.57   Mean   : 58.73   NA's        :4329  
 White-Gray  :   9   3rd Qu.:5.500   3rd Qu.: 7.800   3rd Qu.:32.00   3rd Qu.: 60.00                      
 Yellow-Green:  20   Max.   :7.000   Max.   :10.000   Max.   :60.00   Max.   :200.00                      
 NA's        :4334   NA's   :4327    NA's   :4327     NA's   :4338    NA's   :4338                        
   Temp_Min_F    
 Min.   :-79.00  
 1st Qu.:-38.00  
 Median :-33.00  
 Mean   :-22.53  
 3rd Qu.:-18.00  
 Max.   : 52.00  
 NA's   :4328    

| You are doing so well!
```
```r
| summary() provides different output for each variable, depending on its class. For numeric data such as
| Precip_Min, summary() displays the minimum, 1st quartile, median, mean, 3rd quartile, and maximum. These
| values help us understand how the data are distributed.
```
```r
| For categorical variables (called 'factor' variables in R), summary() displays the number of times each
| value (or 'level') occurs in the data. For example, each value of Scientific_Name only appears once, since
| it is unique to a specific plant. In contrast, the summary for Duration (also a factor variable) tells us
| that our dataset contains 3031 Perennial plants, 682 Annual plants, etc.
```
```r
| You can see that R truncated the summary for Active_Growth_Period by including a catch-all category called
| 'Other'. Since it is a categorical/factor variable, we can see how many times each value actually occurs in
| the data with table(plants$Active_Growth_Period).
```
```r
> table(plants$Active_Growth_Period)

Fall, Winter and Spring                  Spring         Spring and Fall       Spring and Summer
                     15                     144                      10                     447
   Spring, Summer, Fall                  Summer         Summer and Fall              Year Round
                     95                      92                      24                       5

| You are amazing!
```
```r
| Each of the functions we've introduced so far has its place in helping you to better understand the
| structure of your data. However, we've left the best for last....
```
```r
| Perhaps the most useful and concise function for understanding the *str*ucture of your data is str(). Give
| it a try now.
```
```r
> str(plants)
'data.frame':	5166 obs. of  10 variables:
 $ Scientific_Name     : Factor w/ 5166 levels "Abelmoschus",..: 1 2 3 4 5 6 7 8 9 10 ...
 $ Duration            : Factor w/ 8 levels "Annual","Annual, Biennial",..: NA 4 NA 7 7 NA 1 NA 7 7 ...
 $ Active_Growth_Period: Factor w/ 8 levels "Fall, Winter and Spring",..: NA NA NA 4 NA NA NA NA 4 NA ...
 $ Foliage_Color       : Factor w/ 6 levels "Dark Green","Gray-Green",..: NA NA NA 3 NA NA NA NA 3 NA ...
 $ pH_Min              : num  NA NA NA 4 NA NA NA NA 7 NA ...
 $ pH_Max              : num  NA NA NA 6 NA NA NA NA 8.5 NA ...
 $ Precip_Min          : int  NA NA NA 13 NA NA NA NA 4 NA ...
 $ Precip_Max          : int  NA NA NA 60 NA NA NA NA 20 NA ...
 $ Shade_Tolerance     : Factor w/ 3 levels "Intermediate",..: NA NA NA 3 NA NA NA NA 2 NA ...
 $ Temp_Min_F          : int  NA NA NA -43 NA NA NA NA -13 NA ...

| Perseverance, that's the answer.
```
```r
| The beauty of str() is that it combines many of the features of the other functions you've already seen,
| all in a concise and readable format. At the very top, it tells us that the class of plants is 'data.frame'
| and that it has 5166 observations and 10 variables. It then gives us the name and class of each variable,
| as well as a preview of its contents.
```
```r
| str() is actually a very general function that you can use on most objects in R. Any time you want to
| understand the structure of something (a dataset, function, etc.), str() is a good place to start.
```
```r
| In this lesson, you learned how to get a feel for the structure and contents of a new dataset using a
| collection of simple and useful functions. Taking the time to do this upfront can save you time and
| frustration later on in your analysis.
```

## 13. Simulation
```r
| One of the great advantages of using a statistical programming language like R is its vast collection of
| tools for simulating random numbers.
```
```r
| This lesson assumes familiarity with a few common probability distributions, but these topics will only be
| discussed with respect to random number generation. Even if you have no prior experience with these
| concepts, you should be able to complete the lesson and understand the main ideas.
```
```r
| The first function we'll use to generate random numbers is sample(). Use ?sample to pull up the
| documentation.
```
```r
> ?sample

| Excellent work!
```
```r
| Let's simulate rolling four six-sided dice: sample(1:6, 4, replace = TRUE).
```
```r
> sample(1:6, 4, replace = TRUE)
[1] 1 5 6 3

| Great job!
```
```r
| Now repeat the command to see how your result differs. (The probability of rolling the exact same result is
| (1/6)^4 = 0.00077, which is pretty small!)
```
```r
> sample(1:6, 4, replace = TRUE)
[1] 1 1 2 6

| That's correct!
```
```r
| sample(1:6, 4, replace = TRUE) instructs R to randomly select four numbers between 1 and 6, WITH
| replacement. Sampling with replacement simply means that each number is "replaced" after it is selected, so
| that the same number can show up more than once. This is what we want here, since what you roll on one die
| shouldn't affect what you roll on any of the others.
```
```r
| Now sample 10 numbers between 1 and 20, WITHOUT replacement. To sample without replacement, simply leave
| off the 'replace' argument.
```
```r
> sample(1:20, 10)
 [1]  6 18  1 15 10  8 13 11  2  9

| Keep working like that and you'll get there!
```
```r
| Since the last command sampled without replacement, no number appears more than once in the output.
```
```r
| LETTERS is a predefined variable in R containing a vector of all 26 letters of the English alphabet. Take a
| look at it now.
```
```r
> LETTERS
 [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S" "T" "U" "V" "W" "X" "Y" "Z"

| You are amazing!
```
```r
| The sample() function can also be used to permute, or rearrange, the elements of a vector. For example, try
| sample(LETTERS) to permute all 26 letters of the English alphabet.
```
```r
> sample(LETTERS)
 [1] "F" "A" "Y" "O" "B" "G" "Z" "N" "L" "E" "M" "V" "H" "T" "S" "D" "X" "C" "J" "P" "I" "Q" "W" "U" "K" "R"

| Keep up the great work!
```
```r
| This is identical to taking a sample of size 26 from LETTERS, without replacement. When the 'size' argument
| to sample() is not specified, R takes a sample equal in size to the vector from which you are sampling.
```
```r
| Now, suppose we want to simulate 100 flips of an unfair two-sided coin. This particular coin has a 0.3
| probability of landing 'tails' and a 0.7 probability of landing 'heads'.
```
```r
| Let the value 0 represent tails and the value 1 represent heads. Use sample() to draw a sample of size 100
| from the vector c(0,1), with replacement. Since the coin is unfair, we must attach specific probabilities
| to the values 0 (tails) and 1 (heads) with a fourth argument, prob = c(0.3, 0.7). Assign the result to a
| new variable called flips.
```
```r
> flips <- sample(c(0, 1), 100, replace = TRUE, prob = c(0.3, 0.7))

| All that practice is paying off!
```
```r
| View the contents of the flips variable.
```
```r
> flips
  [1] 1 1 1 0 1 1 1 0 0 1 1 1 0 0 1 0 0 1 1 1 1 0 0 0 1 0 1 1 1 0 1 0 1 0 0 1 1 1 1 1 1 1 1 1 1 1 1 0 1 1 0 1
 [53] 1 1 1 1 1 0 1 1 1 1 1 0 1 1 0 1 1 0 1 0 1 1 0 1 1 1 0 0 1 0 1 1 1 1 1 1 1 1 0 1 1 0 0 1 1 1 1 1

| All that hard work is paying off!
```
```r
| Since we set the probability of landing heads on any given flip to be 0.7, we'd expect approximately 70 of
| our coin flips to have the value 1. Count the actual number of 1s contained in flips using the sum()
| function.
```
```r
> sum(flips)
[1] 71

| Keep up the great work!
```
```r
| A coin flip is a binary outcome (0 or 1) and we are performing 100 independent trials (coin flips), so we
| can use rbinom() to simulate a binomial random variable. Pull up the documentation for rbinom() using
| ?rbinom.
```
```r
> ?rbinom

| That's a job well done!
```
```r
| Each probability distribution in R has an r*** function (for "random"), a d*** function (for "density"), a
| p*** (for "probability"), and q*** (for "quantile"). We are most interested in the r*** functions in this
| lesson, but I encourage you to explore the others on your own.
```
```r
| A binomial random variable represents the number of 'successes' (heads) in a given number of independent
| 'trials' (coin flips). Therefore, we can generate a single random variable that represents the number of
| heads in 100 flips of our unfair coin using rbinom(1, size = 100, prob = 0.7). Note that you only specify
| the probability of 'success' (heads) and NOT the probability of 'failure' (tails). Try it now.
```
```r
> rbinom(1, size = 100, prob = 0.7)
[1] 70

| All that hard work is paying off!
```
```r
| Equivalently, if we want to see all of the 0s and 1s, we can request 100 observations, each of size 1, with
| success probability of 0.7. Give it a try, assigning the result to a new variable called flips2.
```
```r
> flips2 <- rbinom(100, size = 1, prob = 0.7)

| All that practice is paying off!
```
```r
| View the contents of flips2.
```
```r
> flips2
  [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 0 0 1 0 1 1 1 0 0 1 1 1 1 1 0 1 0 1 1 1 0 1 1 1 1 1 1 1 1 0 1 1 1 1 1 1 1 1
 [53] 1 0 0 1 1 1 1 1 1 1 1 0 1 1 0 1 0 1 1 1 1 0 0 0 1 1 1 1 0 1 1 0 1 1 0 1 1 1 0 0 1 1 1 0 0 1 0 0

| That's correct!
```
```r
| Now use sum() to count the number of 1s (heads) in flips2. It should be close to 70!

> sum(flips2)
[1] 74

| Keep up the great work!
```
```r
| Similar to rbinom(), we can use R to simulate random numbers from many other probability distributions.
| Pull up the documentation for rnorm() now.
```
```r
> ?rnorm

| Excellent work!
```
```r
| The standard normal distribution has mean 0 and standard deviation 1. As you can see under the 'Usage'
| section in the documentation, the default values for the 'mean' and 'sd' arguments to rnorm() are 0 and 1,
| respectively. Thus, rnorm(10) will generate 10 random numbers from a standard normal distribution. Give it
| a try.
```
```r
> rnorm(10)
 [1] -0.3330341  1.1902496  1.7744606  1.3594416  0.5705276  0.4070259 -0.7847961  1.2389566 -1.5085626
[10] -1.9027076

| Excellent work!
```
```r
| Now do the same, except with a mean of 100 and a standard deviation of 25.
```
```r
> rnorm(10, mean = 100, sd = 25)
 [1]  71.23227  95.89021 119.73531 118.30479  97.17749  90.64156 108.75344 109.95472 132.91888 110.14700

| You are really on a roll!
```
```r
| Finally, what if we want to simulate 100 *groups* of random numbers, each containing 5 values generated
| from a Poisson distribution with mean 10? Let's start with one group of 5 numbers, then I'll show you how
| to repeat the operation 100 times in a convenient and compact way.
```
```r
| Generate 5 random values from a Poisson distribution with mean 10. Check out the documentation for rpois()
| if you need help.
```
```r
> ?rpois
> rpois(5, lambda = 10)
[1] 10  9  5  9  8

| You are really on a roll!
```
```r
| Now use replicate(100, rpois(5, 10)) to perform this operation 100 times. Store the result in a new
| variable called my_pois.
```
```r
> my_pois <- replicate(100, rpois(5, 10))

| Excellent job!
```
```r
| Take a look at the contents of my_pois.
```
```r
> my_pois
     [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10] [,11] [,12] [,13] [,14] [,15] [,16] [,17] [,18] [,19]
[1,]    5   21    4   12   13    8   10   14    9     7     8    11     6     5    10     8     7    10     9
[2,]   13   13   10   10   14   14   13   10   12    12    12     6    14    10     7     5    13    15     9
[3,]    6    9    9    9   13    9    9    9   19     6    12    18     5     7     8     8     8    11    11
[4,]   10    5    8   10    7   12   10    8   16    11     7    11     7    16     8     6    11    11     7
[5,]   12   10   16   10    8   17   10   10   11    11    11     6     9    10     6     5    17    13     7
     [,20] [,21] [,22] [,23] [,24] [,25] [,26] [,27] [,28] [,29] [,30] [,31] [,32] [,33] [,34] [,35] [,36]
[1,]     6    12     7    19    10     9    11    15     9     8    10    16    13    14    13    11    10
[2,]     9     6    14    11    10    12    19    14     7    16    10    10     6     9     8    10    16
[3,]    10    10     5     6     7    10     8    10     8     8    10    15     5     8     7    13    16
[4,]    11    11    10     3    10     4     7     6     7     7    10     4    13    11    12    14    11
[5,]    15    11    10    12    14    16     5     6     9     5     9    10    10    13    11     8     5
     [,37] [,38] [,39] [,40] [,41] [,42] [,43] [,44] [,45] [,46] [,47] [,48] [,49] [,50] [,51] [,52] [,53]
[1,]     9     9    13    12    15     9    11     9     6     8    12    16    10     5    11     6     7
[2,]     7    11    18     7    10    15    10    11    11    19     9     8    14    10     9    11    11
[3,]    12     7     8     9    10     9    12    12     8    10     9    10    11     8    12    13    16
[4,]    10    10    10    11    10     8    12    13    12    12     9    12     8     5     4    10     8
[5,]    11     6    11    10     8     9    11    10    10    12     6    14     9     7     9    13    12
     [,54] [,55] [,56] [,57] [,58] [,59] [,60] [,61] [,62] [,63] [,64] [,65] [,66] [,67] [,68] [,69] [,70]
[1,]     6     9     6    11     7    11     9    10    12    13     8     7    11    11     6     9    10
[2,]    11    10     7    10    13    10    11    10     7    10    18    12    13    13     7    10    12
[3,]     6     9    10    12    12     9    18    11    10     7    10     7    16     8    14    11     6
[4,]    15     8    10    12     7    16     5    10    15    17     8     9    11    15     9    10     8
[5,]    13    10    11     7    15    11    11    18     7    10     9    10     7     8    11    12    11
     [,71] [,72] [,73] [,74] [,75] [,76] [,77] [,78] [,79] [,80] [,81] [,82] [,83] [,84] [,85] [,86] [,87]
[1,]    12     9     9     7    11     8    16     5     7    13     6    12     8    10     9     8     8
[2,]     9    22    13    10    10     7     8    11    12     7     9     7    12    10     9     7    13
[3,]     4    13    13    15     9     7     9    16     8    11    14     3     7    14     9    12    16
[4,]    12    10     8     6    11     7     6    11     9    12     9    13    12    10     7    13    10
[5,]     6    13    12    10     7    12     7    11    18    14    10    10     5    13     8    12     6
     [,88] [,89] [,90] [,91] [,92] [,93] [,94] [,95] [,96] [,97] [,98] [,99] [,100]
[1,]    10     5     7    12     7    13    10     5    10     8    10    12      5
[2,]     7    13     8    14    19    15     8    15     9     8    15    14     11
[3,]     7     9    14    12     8    11     9     8    12     6     7     8     11
[4,]    16     5    10    10    15     7     8     8    11    16    11     8     10
[5,]    13     9    13     4    10     7     9    12     8     8    10     4     12

| You're the best!
```
```r
| replicate() created a matrix, each column of which contains 5 random numbers generated from a Poisson
| distribution with mean 10. Now we can find the mean of each column in my_pois using the colMeans()
| function. Store the result in a variable called cm.
```
```r
> cm <- colMeans(my_pois)

| That's a job well done!
```
```r
| And let's take a look at the distribution of our column means by plotting a histogram with hist(cm).
```
```r
> hist(cm)

| Keep working like that and you'll get there!
```
```r
| Looks like our column means are almost normally distributed, right? That's the Central Limit Theorem at
| work, but that's a lesson for another day!
```
```r
| All of the standard probability distributions are built into R, including exponential (rexp()), chi-squared
| (rchisq()), gamma (rgamma()), .... Well, you see the pattern.
```
```r
| Simulation is practically a field of its own and we've only skimmed the surface of what's possible. I
| encourage you to explore these and other functions further on your own.
```

## 14. Dates and Times
```r
| R has a special way of representing dates and times, which can be helpful if you're working with data that
| show how something changes over time (i.e. time-series data) or if your data contain some other temporal
| information, like dates of birth.
```
```r
| Dates are represented by the 'Date' class and times are represented by the 'POSIXct' and 'POSIXlt' classes.
| Internally, dates are stored as the number of days since 1970-01-01 and times are stored as either the
| number of seconds since 1970-01-01 (for 'POSIXct') or a list of seconds, minutes, hours, etc. (for
| 'POSIXlt').
```
```r
| Let's start by using d1 <- Sys.Date() to get the current date and store it in the variable d1. (That's the
| letter 'd' and the number 1.)
```
```r
> d1 <- Sys.Date()

| You're the best!
```
```r
| Use the class() function to confirm d1 is a Date object.
```
```r
> class(d1)
[1] "Date"

| You are quite good my friend!
```
```r
| We can use the unclass() function to see what d1 looks like internally. Try it out.
```
```r
> unclass(d1)
[1] 18184

| That's correct!
```
```r
| That's the exact number of days since 1970-01-01!
```
```r
| However, if you print d1 to the console, you'll get today's date -- YEAR-MONTH-DAY. Give it a try.
```
```r
> d1
[1] "2019-10-15"

| Excellent work!
```
```r
| What if we need to reference a date prior to 1970-01-01? Create a variable d2 containing
| as.Date("1969-01-01").
```
```r
> d2 <- as.Date('1969-01-01')

| That's a job well done!
```
```r
| Now use unclass() again to see what d2 looks like internally.
```
```r
> unclass(d2)
[1] -365

| That's a job well done!
```
```r
| As you may have anticipated, you get a negative number. In this case, it's -365, since 1969-01-01 is
| exactly one calendar year (i.e. 365 days) BEFORE 1970-01-01.
```
```r
| Now, let's take a look at how R stores times. You can access the current date and time using the Sys.time()
| function with no arguments. Do this and store the result in a variable called t1.
```
```r
> t1 <- Sys.time()

| You are doing so well!
```
```r
| View the contents of t1.
```
```r
> t1
[1] "2019-10-15 07:47:53 CEST"

| That's correct!
```
```r
| And check the class() of t1.
```
```r
> class(t1)
[1] "POSIXct" "POSIXt"

| You got it right!
```
```r
| As mentioned earlier, POSIXct is just one of two ways that R represents time information. (You can ignore
| the second value above, POSIXt, which just functions as a common language between POSIXct and POSIXlt.) Use
| unclass() to see what t1 looks like internally -- the (large) number of seconds since the beginning of
| 1970.
```
```r
> unclass(t1)
[1] 1571118474

| You are really on a roll!
```
```r
| By default, Sys.time() returns an object of class POSIXct, but we can coerce the result to POSIXlt with
| as.POSIXlt(Sys.time()). Give it a try and store the result in t2.
```
```r
> t2 <- as.POSIXlt(Sys.time())

| Excellent work!
```
```r
| Check the class of t2.
```
```r
> class(t2)
[1] "POSIXlt" "POSIXt"

| You got it right!
```
```r
| Now view its contents.
```
```r
> t2
[1] "2019-10-15 07:48:29 CEST"

| Keep working like that and you'll get there!
```
```r
| The printed format of t2 is identical to that of t1. Now unclass() t2 to see how it is different
| internally.
```
```r
> unclass(t2)
$sec
[1] 29.93399

$min
[1] 48

$hour
[1] 7

$mday
[1] 15

$mon
[1] 9

$year
[1] 119

$wday
[1] 2

$yday
[1] 287

$isdst
[1] 1

$zone
[1] "CEST"

$gmtoff
[1] 7200

attr(,"tzone")
[1] ""     "CET"  "CEST"

| Excellent work!
```
```r
| t2, like all POSIXlt objects, is just a list of values that make up the date and time. Use str(unclass(t2))
| to have a more compact view.
```
```r
> str(unclass(t2))
List of 11
 $ sec   : num 29.9
 $ min   : int 48
 $ hour  : int 7
 $ mday  : int 15
 $ mon   : int 9
 $ year  : int 119
 $ wday  : int 2
 $ yday  : int 287
 $ isdst : int 1
 $ zone  : chr "CEST"
 $ gmtoff: int 7200
 - attr(*, "tzone")= chr [1:3] "" "CET" "CEST"

| That's the answer I was looking for.
```
```r
| If, for example, we want just the minutes from the time stored in t2, we can access them with t2$min. Give
| it a try.
```
```r
> t2$min
[1] 48

| Excellent work!
```
```r
| Now that we have explored all three types of date and time objects, let's look at a few functions that
| extract useful information from any of these objects -- weekdays(), months(), and quarters().
```
```r
| The weekdays() function will return the day of week from any date or time object. Try it out on d1, which
| is the Date object that contains today's date.
```
```r
> weekdays(d1)
[1] "Tuesday"

| You are doing so well!
```
```r
| The months() function also works on any date or time object. Try it on t1, which is the POSIXct object that
| contains the current time (well, it was the current time when you created it).
```
```r
> months(t1)
[1] "October"

| You nailed it! Good job!
```
```r
| The quarters() function returns the quarter of the year (Q1-Q4) from any date or time object. Try it on t2,
| which is the POSIXlt object that contains the time at which you created it.
```
```r
> quarters(t2)
[1] "Q4"

| That's a job well done!
```
```r
| Often, the dates and times in a dataset will be in a format that R does not recognize. The strptime()
| function can be helpful in this situation.
```
```r
| strptime() converts character vectors to POSIXlt. In that sense, it is similar to as.POSIXlt(), except that
| the input doesn't have to be in a particular format (YYYY-MM-DD).
```
```r
| To see how it works, store the following character string in a variable called t3: "October 17, 1986 08:24"
| (with the quotes).
```
```r
> t3 <- "October 17, 1986 08:24"

| Nice work!
```
```r
| Now, use strptime(t3, "%B %d, %Y %H:%M") to help R convert our date/time object to a format that it
| understands. Assign the result to a new variable called t4. (You should pull up the documentation for
| strptime() if you'd like to know more about how it works.)
```
```r
> t4 <- strptime(t3, "%B %d, %Y %H:%M")

| Excellent work!
```
```r
| Print the contents of t4.
```
```r
> t4
[1] "1986-10-17 08:24:00 CET"

| You are doing so well!
```
```r
| That's the format we've come to expect. Now, let's check its class().
```
```r
> class(t4)
[1] "POSIXlt" "POSIXt"

| That's correct!
```
```r
| Finally, there are a number of operations that you can perform on dates and times, including arithmetic
| operations (+ and -) and comparisons (<, ==, etc.)
```
```r
| The variable t1 contains the time at which you created it (recall you used Sys.time()). Confirm that some
| time has passed since you created t1 by using the 'greater than' operator to compare it to the current
| time: Sys.time() > t1
```
```r
> Sys.time() > t1
[1] TRUE

| Excellent work!
```
```r
| So we know that some time has passed, but how much? Try subtracting t1 from the current time using
| Sys.time() - t1. Don't forget the parentheses at the end of Sys.time(), since it is a function.
```
```r
> Sys.time() - t1
Time difference of 2.871195 mins

| You got it right!
```
```r
| The same line of thinking applies to addition and the other comparison operators. If you want more control
| over the units when finding the above difference in times, you can use difftime(), which allows you to
| specify a 'units' parameter.
```
```r
| Use difftime(Sys.time(), t1, units = 'days') to find the amount of time in DAYS that has passed since you
| created t1.
```
```r
> difftime(Sys.time(), t1, units = 'days')
Time difference of 0.002108413 days

| You are doing so well!
```
```r
| In this lesson, you learned how to work with dates and times in R. While it is important to understand the
| basics, if you find yourself working with dates and times often, you may want to check out the lubridate
| package by Hadley Wickham.
```

## 15. Base Graphics
```r
| One of the greatest strengths of R, relative to other programming languages, is the ease with which we can
| create publication-quality graphics. In this lesson, you'll learn about base graphics in R.
```
```r
| We do not cover the more advanced portions of graphics in R in this lesson. These include lattice, ggplot2
| and ggvis.
```
```r
| There is a school of thought that this approach is backwards, that we should teach ggplot2 first. See
| http://varianceexplained.org/r/teach_ggplot2_to_beginners/ for an outline of this view.
```
```r
| Load the included data frame cars with data(cars).
```
```r
> data(cars)

| All that practice is paying off!
```
```r
| To fix ideas, we will work with simple data frames. Our main goal is to introduce various plotting
| functions and their arguments. All the output would look more interesting with larger, more complex data
| sets.
```
```r
| Pull up the help page for cars.
```
```r
> ?cars

| Great job!
```
```r
| As you can see in the help page, the cars data set has only two variables: speed and stopping distance.
| Note that the data is from the 1920s.
```
```r
| Run head() on the cars data.
```
```r
> head(cars)
  speed dist
1     4    2
2     4   10
3     7    4
4     7   22
5     8   16
6     9   10

| That's a job well done!
```
```r
| Before plotting, it is always a good idea to get a sense of the data. Key R commands for doing so include,
| dim(), names(), head(), tail() and summary().
```
```r
| Run the plot() command on the cars data frame.
```
```r
> plot(cars)

| You got it!
```
```r
| As always, R tries very hard to give you something sensible given the information that you have provided to
| it. First, R notes that the data frame you have given it has just two columns, so it assumes that you want
| to plot one column versus the other.
```
```r
| Second, since we do not provide labels for either axis, R uses the names of the columns. Third, it creates
| axis tick marks at nice round numbers and labels them accordingly. Fourth, it uses the other defaults
| supplied in plot().
```
```r
| We will now spend some time exploring plot, but many of the topics covered here will apply to most other R
| graphics functions. Note that 'plot' is short for scatterplot.
```
```r
| Look up the help page for plot().
```
```r
> ?plot

| You're the best!
```
```r
| The help page for plot() highlights the different arguments that the function can take. The two most
| important are x and y, the variables that will be plotted. For the next set of questions, include the
| argument names in your answers. That is, do not type plot(cars$speed, cars$dist), although that will work.
| Instead, use plot(x = cars$speed, y = cars$dist).
```
```r
| Use plot() command to show speed on the x-axis and dist on the y-axis from the cars data frame. Use the
| form of the plot command in which vectors are explicitly passed in as arguments for x and y.
```
```r
> plot(x = cars$speed, y = cars$dist)

| Perseverance, that's the answer.
```
```r
| Note that this produces a slightly different answer than plot(cars). In this case, R is not sure what you
| want to use as the labels on the axes, so it just uses the arguments which you pass in, data frame name and
| dollar signs included.
```
```r
| Note that there are other ways to call the plot command, i.e., using the "formula" interface. For example,
| we get a similar plot to the above with plot(dist ~ speed, cars). However, we will wait till later in the
| lesson before using the formula interface.
```
```r
| Use plot() command to show dist on the x-axis and speed on the y-axis from the cars data frame. This is the
| opposite of what we did above.
```
```r
> plot(x = cars$dist, y = cars$speed)

| Great job!
```
```r
| It probably makes more sense for speed to go on the x-axis since stopping distance is a function of speed
| more than the other way around. So, for the rest of the questions in this portion of the lesson, always
| assign the arguments accordingly.
```
```r
| In fact, you can assume that the answers to the next few questions are all of the form plot(x = cars$speed,
| y = cars$dist, ...) but with various arguments used in place of the ...
```
```r
| Recreate the plot with the label of the x-axis set to "Speed".
```
```r
> plot(x = cars$speed, y = cars$dist, xlab = 'Speed')

| Nice work!
```
```r
| Recreate the plot with the label of the y-axis set to "Stopping Distance".
```
```r
> plot(x = cars$speed, y = cars$dist, ylab = 'Stopping Distance')

| You are quite good my friend!
```
```r
| Recreate the plot with "Speed" and "Stopping Distance" as axis labels.
```
```r
> plot(x = cars$speed, y = cars$dist, xlab = 'Speed', ylab = 'Stopping Distance')

| You are really on a roll!
```
```r
| The reason that plots(cars) worked at the beginning of the lesson was that R was smart enough to know that
| the first element (i.e., the first column) in cars should be assigned to the x argument and the second
| element to the y argument. To save on typing, the next set of answers will all be of the form, plot(cars,
| ...) with various arguments added.
```
```r
| For each question, we will only want one additional argument at a time. Of course, you can pass in more
| than one argument when doing a real project.
```
```r
| Plot cars with a main title of "My Plot". Note that the argument for the main title is "main" not "title".
```
```r
> plot(cars, main = "My Plot")

| Excellent job!
```
```r
| Plot cars with a sub title of "My Plot Subtitle".
```
```r
> plot(cars, sub = 'My Plot Subtitle')
There were 12 warnings (use warnings() to see them)

| Your dedication is inspiring!
```
```r
| The plot help page (?plot) only covers a small number of the many arguments that can be passed in to plot()
| and to other graphical functions. To begin to explore the many other options, look at ?par. Let's look at
| some of the more commonly used ones. Continue using plot(cars, ...) as the base answer to these questions.
```
```r
| Plot cars so that the plotted points are colored red. (Use col = 2 to achieve this effect.)
```
```r
> plot(cars, col = 2)

| Keep working like that and you'll get there!
```
```r
| Plot cars while limiting the x-axis to 10 through 15.  (Use xlim = c(10, 15) to achieve this effect.)
```
```r
> plot(cars, xlim = c(10, 15))

| You are doing so well!
```
```r
| You can also change the shape of the symbols in the plot. The help page for points (?points) provides the
| details.
```
```r
| Plot cars using triangles.  (Use pch = 2 to achieve this effect.)
```
```r
> plot(cars, pch = 2)

| Great job!
```
```r
| Arguments like "col" and "pch" may not seem very intuitive. And that is because they aren't! So, many/most
| people use more modern packages, like ggplot2, for creating their graphics in R.
```
```r
| It is, however, useful to have an introduction to base graphics because many of the idioms in lattice and
| ggplot2 are modeled on them.
```
```r
| Let's now look at some other functions in base graphics that may be useful, starting with boxplots.
```
```r
| Load the mtcars data frame.
```
```r
> data(mtcars)

| You got it!
```
```r
| Anytime that you load up a new data frame, you should explore it before using it. In the middle of a swirl
| lesson, just type play(). This temporarily suspends the lesson (without losing the work you have already
| done) and allows you to issue commands like dim(mtcars) and head(mtcars). Once you are done examining the
| data, just type nxt() and the lesson will pick up where it left off.
```
```r
| Look up the help page for boxplot().
```
```r
> ?boxplot

| You got it!
```
```r
| Instead of adding data columns directly as input arguments, as we did with plot(), it is often handy to
| pass in the entire data frame. This is what the "data" argument in boxplot() allows.
```
```r
| boxplot(), like many R functions, also takes a "formula" argument, generally an expression with a tilde
| ("~") which indicates the relationship between the input variables. This allows you to enter something like
| mpg ~ cyl to plot the relationship between cyl (number of cylinders) on the x-axis and mpg (miles per
| gallon) on the y-axis.
```
```r
| Use boxplot() with formula = mpg ~ cyl and data = mtcars to create a box plot.
```
```r
> boxplot(mpg ~ cyl, mtcars)
```
```r
| The plot shows that mpg is much lower for cars with more cylinders. Note that we can use the same set of
| arguments that we explored with plot() above to add axis labels, titles and so on.
```
```r
| When looking at a single variable, histograms are a useful tool. hist() is the associated R function. Like
| plot(), hist() is best used by just passing in a single vector.
```
```r
| Use hist() with the vector mtcars$mpg to create a histogram.
```
```r
> hist(mtcars$mpg)

| You are amazing!
```
```r
| In this lesson, you learned how to work with base graphics in R. The best place to go from here is to study
| the ggplot2 package. If you want to explore other elements of base graphics, then this web page
| (http://www.ling.upenn.edu/~joseff/rstudy/week4.html) provides a useful overview.
```
