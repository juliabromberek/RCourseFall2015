---
title: "Preliminaries in R"
author: "Brooke Anderson, Assistant Professor of Epidemiology"
job: Colorado State University
logo        : figures/CSU_ram.png
date: "August 24, 2015"
output: ioslides_presentation
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
mode        : selfcontained # {standalone, draft}
---

# R and RStudio

## What is R?

- A statistical programming language
- Open-source
- A core package with many available user-created add-ons (packages)

## What is R?

Currently popular in a number of fields, including:

- Statistics
- Machine learning
- Data journalism / Data analysis

## What is R?

> "The best thing about R is that it was developed by statisticians. The worst thing about R is that... it was developed by statisticians."

> -Bo Cowgill, Google, at the Bay Area R Users Group

## Gratis vs. libre

- Gratis: Free as in beer
- Libre: Free as in speech

With open-source software (free as in speech), you can:

- Check out the code to figure out how the software works
- Share the code (and software) with other people
- Make any changes you want to the code

## What is RStudio?

RStudio is a user interface for R. You download it separately, but it's a "nicer" way to work in R. 

RStudio (the company) currently:

- Develops and freely provides the RStudio IDE
- Provides excellent resources for learning and using R (cheatsheets, )
- Is producing some of the most-used R packages
- Employees some of the top people in R development

## Setting up

If do not already have them, you will need to download and install both R and RStudio. 

- Go to [CRAN](https://cran.r-project.org) and download the latest version of R for your system. Install.
- Go to the [RStudio download page](https://www.rstudio.com/products/rstudio/download/) and download the latest version of RStudio for your system. Install. 
- Defaults should be fine for everything.

# The "package" system

## R packages

Your original download of R is only a starting point:

<img src="figures/BrioBasicSet.jpg" width="400" />

## R packages

To take full advantage of R, you'll want to add on packages:

<img src="figures/BrioFancySet.jpg" width="800" />

## R packages

You can get packages to add-on to your version of R from:

- CRAN (currently 7050 available packages)
- GitHub
- Your friends and collaborators
- Make them yourself

## Installing from CRAN

The most popular place from which to get packages is currently CRAN. You can install packages from CRAN using R code. 

<img src="figures/telephone_keypad.png" width="150" />

For example, to get the package `phonenumber`, you could use:


```r
install.packages("phonenumber")
```

## Loading an installed package

Once you have a package, you can load it to an R session using the `library()` function. 


```r
library("phonenumber")
```

Once it's loaded, you can use all its functions.


```r
fedex_number <- "GoFedEx"
letterToNumber(fedex_number)
```

```
## [1] "4633339"
```

# Some basics of R code

## R's MVP: <-

`<-` is R's assignment operator. It takes whatever you've created on the right hand side of the `<-` and saves it as an object with the name you put on the left hand side of the `<-` : 


```r
## Note: Generic code-- this will not work
[name of object] <- [thing I want to save]
```

## R's MVP: <-

For example, if I just type `"GoFedEx"`, R will print it back to me, but won't save it anywhere for me to use later:


```r
"GoFedEx"
```

```
## [1] "GoFedEx"
```

## R's MVP: <-

However, if I assign it to an object, I can print it out or use it later by referencing that object name:


```r
fedex_number <- "GoFedEx"
fedex_number
```

```
## [1] "GoFedEx"
```

```r
letterToNumber(fedex_number)
```

```
## [1] "4633339"
```

## <- vs. =

You can make assignments using either `<-` or `=`, and you'll see both when you're reading other people's code. 

However, R gurus advise using `<-` in your own code, and as you move to doing more complex things, problems might crop up if you use `=`. 

## <- vs. =

For now, though, it will be helpful for you to know that these two calls do the same thing:


```r
one_to_ten <- 1:10
one_to_ten
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
one_to_ten = 1:10
one_to_ten
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

## Naming objects

> “There are only two hard things in Computer Science: cache invalidation and naming things.”

> — Phil Karlton

## Naming objects

- Use only letters, numbers, and underscores
- Don't start with anything but a letter

*From [Hadley Wickham's R style guide](http://adv-r.had.co.nz/Style.html)*

- Use lower case for variable names (`fedex_number`, not `FedExNumber`)
- Use an underscore as a separator (`fedex_number`, not `fedex.number` or `fedexNumber`)
- Avoid using names that are already defined in R (e.g., don't name an object `mean`, because as `mean` function exists)

## R's most basic object types

The two most basic types of objects for data in R are **vectors** (1D) and **dataframes** (2D). 

## Vectors

- A vector is a string of values. 
- All values must be of the same class (i.e., all numbers, all characters, all dates)
- You can use `c()` to join values together to create a vector
- The *length* of the vector is how many values it has in it

For example:

```r
fibonacci <- c(1, 1, 2, 3, 5)
fibonacci
```

```
## [1] 1 1 2 3 5
```

```r
length(fibonacci)
```

```
## [1] 5
```

## Vectors

An example using characters instead of numbers:


```r
one_to_five <- c("one", "two", "three", "four", "five")
one_to_five
```

```
## [1] "one"   "two"   "three" "four"  "five"
```

If you mix classes, it will default to most generic:


```r
mixed_classes <- c(1, 3, "five")
mixed_classes
```

```
## [1] "1"    "3"    "five"
```

## Vectors

You can pull out certain values by using indexing (`[...]`) to identify the locations you want to get


```r
fibonacci[2] # Get the second value
```

```
## [1] 1
```

```r
fibonacci[c(1, 5)] # Get first and fifth values
```

```
## [1] 1 5
```

```r
fibonacci[1:3] # Get the first three values
```

```
## [1] 1 1 2
```

## Dataframes

A dataframe is one or more vectors of the same length stuck together side-by-side. It is the closest R has to what you'd get with an Excel spreadsheet. 

You can create dataframes using the `data.frame()` function. However, most often you will create a dataframe by reading in data from a file using something like `read.csv()`. 

## Dataframes

For example, to create a dataframe from vectors you already have saved as R objects:


```r
fibonacci_seq <- data.frame(num_in_seq = one_to_five,
                            fibonacci_num = fibonacci)
fibonacci_seq
```

```
##   num_in_seq fibonacci_num
## 1        one             1
## 2        two             1
## 3      three             2
## 4       four             3
## 5       five             5
```

## Dataframes

The format for using `data.frame()` is:


```r
## Note: Generic code-- this will not work
[name of object] <- data.frame([1st column name] = [1st column content],
                               [2nd column name] = [2nd column content])
```

## Dataframes

You can use indexing (`[..., ...]`) for dataframes, too, but now they'll have two dimensions (rows, then columns). Put the rows you want before the comma, the columns after. If you want all of something, leave the designated spot blank. For example:


```r
fibonacci_seq[1:2, 2] # First two rows, second column
```

```
## [1] 1 1
```

```r
fibonacci_seq[5, ] # Last row, all columns
```

```
##   num_in_seq fibonacci_num
## 5       five             5
```

## Dataframes

Usually, instead of creating a dataframe from vectors, you'll read one in from data on an outside file. For example, to read in a dataset from a CSV file called `daily_show_guests.csv`:


```r
daily_show <- read.csv("daily_show_guests.csv",
                       header = TRUE,
                       skip = 4)
daily_show[1:2, ]
```

```
##   YEAR GoogleKnowlege_Occupation    Show  Group  Raw_Guest_List
## 1 1999                     actor 1/11/99 Acting  Michael J. Fox
## 2 1999                  Comedian 1/12/99 Comedy Sandra Bernhard
```

## Dataframes

You can use the functions `dim()`, `nrow()`, and `ncol` to figure out the dimensions (number of rows and columns) of a dataframe:


```r
dim(daily_show)
```

```
## [1] 2693    5
```

```r
nrow(daily_show)
```

```
## [1] 2693
```

```r
ncol(daily_show)
```

```
## [1] 5
```

## Functions

In general, functions in R take the following structure:


```r
function.name(required information, options)  ## Generic code
```

The result of the function will be output to your R session, unless you choose to save the output in an object:


```r
new.object <- function.name(required information, options)  ## Generic code
```

## Functions

Examples of this structure:


```r
head(daily_show)
head(daily_show, n = 3)
daily_show <- read.csv("daily_show_guests.csv",
                    skip = 4,
                    header = TRUE)
```

Find out more about a function by using `?` (e.g., ,`?head`, `?read.csv`). This will take you to the help page for the function, where you can find out all the possible arguments for the function, required and optional.
