---
title: "Assignment 4"
author: "Leona Ma"
date: "11/19/2021"
output: 
    html_document:
      toc: yes 
      toc_float: yes
      keep_md : yes 
    github_document:
      html_preview: false
always_allow_html: true
---




```r
library(parallel)
```

# Part1 HPC

## Problem 1: Make sure your code is nice


```r
# Total row sums
fun1 <- function(mat) {
  n <- nrow(mat)
  ans <- double(n) 
  for (i in 1:n) {
    ans[i] <- sum(mat[i, ])
  }
  ans
}

fun1alt <- function(mat) {
  ans <- rowSums(mat)
  ans
}

# Cumulative sum by row
fun2 <- function(mat) {
  n <- nrow(mat)
  k <- ncol(mat)
  ans <- mat
  for (i in 1:n) {
    for (j in 2:k) {
      ans[i,j] <- mat[i, j] + ans[i, j - 1]
    }
  }
  ans
}

fun2alt <- function(mat) {
  ans <- t(apply(mat, 1, cumsum))
  ans
}


# Use the data with this code
set.seed(2315)
dat <- matrix(rnorm(200 * 100), nrow = 200)

# Test for the first
microbenchmark::microbenchmark(
  fun1(dat),
  fun1alt(dat), unit = "relative", check = "equivalent"
)
```

```
## Unit: relative
##          expr      min       lq     mean   median       uq      max neval
##     fun1(dat) 9.496127 12.11795 9.936114 12.62689 12.99239 1.375791   100
##  fun1alt(dat) 1.000000  1.00000 1.000000  1.00000  1.00000 1.000000   100
```

```r
# Test for the second
microbenchmark::microbenchmark(
  fun2(dat),
  fun2alt(dat), unit = "relative", check = "equivalent"
)
```

```
## Unit: relative
##          expr      min       lq     mean   median       uq      max neval
##     fun2(dat) 3.941492 2.705127 2.072749 2.607501 1.985775 1.310076   100
##  fun2alt(dat) 1.000000 1.000000 1.000000 1.000000 1.000000 1.000000   100
```

The code we wrote do get faster. 

## Problem 2: Make things run faster with parallel computing

The following function allows simulating PI

```r
sim_pi <- function(n = 1000, i = NULL) {
  p <- matrix(runif(n*2), ncol = 2)
  mean(rowSums(p^2) < 1) * 4
}

# Here is an example of the run
set.seed(156)
sim_pi(1000) # 3.132
```

```
## [1] 3.132
```

In order to get accurate estimates, we can run this function multiple times, with the following code:

```r
# This runs the simulation a 4,000 times, each with 10,000 points
set.seed(1231)
system.time({
  ans <- unlist(lapply(1:4000, sim_pi, n = 10000))
  print(mean(ans))
})
```

```
## [1] 3.14124
```

```
##    user  system elapsed 
##   5.623   1.573   8.115
```

Rewrite the previous code using parLapply() to make it run faster. Make sure you set the seed using clusterSetRNGStream():


```r
cl <- makePSOCKcluster(4L)
clusterSetRNGStream(cl,1231)
system.time({
  ans <- unlist(parLapply(cl, rep(4000,10000),sim_pi))
  print(mean(ans))
})
```

```
## [1] 3.141521
```

```
##    user  system elapsed 
##   0.010   0.002   3.165
```

```r
stopCluster(cl)
```

The code we wrote do get faster. 

# Part2 SQL

Setup a temporary database by running the following chunk

```r
# install.packages(c("RSQLite", "DBI"))

library(RSQLite)
library(DBI)

# Initialize a temporary in memory database
con <- dbConnect(SQLite(), ":memory:")

# Download tables
film <- read.csv("https://raw.githubusercontent.com/ivanceras/sakila/master/csv-sakila-db/film.csv")
film_category <- read.csv("https://raw.githubusercontent.com/ivanceras/sakila/master/csv-sakila-db/film_category.csv")
category <- read.csv("https://raw.githubusercontent.com/ivanceras/sakila/master/csv-sakila-db/category.csv")

# Copy data.frames to database
dbWriteTable(con, "film", film)
dbWriteTable(con, "film_category", film_category)
dbWriteTable(con, "category", category)
```

## Question 1
How many many movies is there available in each rating category.

```r
dbGetQuery(con, "
SELECT rating,
  COUNT(*) AS 'N movies'
FROM film
GROUP BY rating")
```

```
##   rating N movies
## 1      G      180
## 2  NC-17      210
## 3     PG      194
## 4  PG-13      223
## 5      R      195
```

## Question 2
What is the average replacement cost and rental rate for each rating category.


```r
dbGetQuery(con, "
SELECT rating,
  AVG(replacement_cost) AS avg_replacement_cost,
  AVG(rental_rate) AS avg_rental_tate
FROM film
GROUP BY rating")
```

```
##   rating avg_replacement_cost avg_rental_tate
## 1      G             20.12333        2.912222
## 2  NC-17             20.13762        2.970952
## 3     PG             18.95907        3.051856
## 4  PG-13             20.40256        3.034843
## 5      R             20.23103        2.938718
```

## Question 3
Use table film_category together with film to find the how many films there are with each category ID


```r
combine <- dbGetQuery(con, "
SELECT film.film_id, category_id
FROM film
LEFT JOIN film_category
ON film_category.film_id = film.film_id")

dbWriteTable(con, "combine", combine)

category_movie <- dbGetQuery(con, "
SELECT category_id,
  COUNT(*) AS 'N movies'
FROM combine
GROUP BY category_id")

dbGetQuery(con, "
SELECT category_id,
  COUNT(*) AS 'N movies'
FROM combine
GROUP BY category_id
LIMIT 10")
```

```
##    category_id N movies
## 1           NA        2
## 2            1       64
## 3            2       66
## 4            3       60
## 5            4       57
## 6            5       58
## 7            6       68
## 8            7       62
## 9            8       69
## 10           9       73
```

```r
dbWriteTable(con, "category_movie", category_movie)
```

Since there are 2 film in film table do not have corresponding category ID in film_category table, there is a category NA with 2 observations. 

## Question 4
Incorporate table category into the answer to the previous question to find the name of the most popular category.


```r
combine2 <- dbGetQuery(con, "
SELECT category_movie.category_id, category_movie.`N movies`, name
FROM category_movie
LEFT JOIN category
ON category_movie.category_id = category.category_id")

dbWriteTable(con, "combine2", combine2)

dbGetQuery(con, "
SELECT category_id,name,
 max(`N movies`) as max
FROM combine2")
```

```
##   category_id   name max
## 1          15 Sports  74
```

Sports is the most popular category. 


```r
dbDisconnect(con)
```

