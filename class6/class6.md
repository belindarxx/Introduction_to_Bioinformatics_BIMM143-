Class 6 R Functions
================
Belinda Xue
10/17/2019

# This is heading 1

This is my work from Class 6 in **BIMM 143**.

``` r
# this code chunk is treating as code in R script :)
plot(1:10)
```

![](class6_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

## Practice reading files \!\!\!\!\!

``` r
read.table("test1.txt")
```

    ##               V1
    ## 1 Col1,Col2,Col3
    ## 2          1,2,3
    ## 3          4,5,6
    ## 4          7,8,9
    ## 5          a,b,c

``` r
read.table("test2.txt")
```

    ##               V1
    ## 1 Col1$Col2$Col3
    ## 2          1$2$3
    ## 3          4$5$6
    ## 4          7$8$9
    ## 5          a$b$c

``` r
read.table("test3.txt")
```

    ##   V1 V2 V3
    ## 1  1  6  a
    ## 2  2  7  b
    ## 3  3  8  c
    ## 4  4  9  d
    ## 5  5 10  e

``` r
# can use any read.xxx for anything as along as you specify the sep=""

# text 1 is separate by comma, default common is to use read.cvs--> if you read.csv for text 1, don't have to put sep""
read.csv("https://bioboot.github.io/bimm143_S19/class-material/test1.txt", header=TRUE)
```

    ##   Col1 Col2 Col3
    ## 1    1    2    3
    ## 2    4    5    6
    ## 3    7    8    9
    ## 4    a    b    c

``` r
# can use read.table for text 1, but specify sep=","
read.table("https://bioboot.github.io/bimm143_S19/class-material/test1.txt", sep=",", header=TRUE)
```

    ##   Col1 Col2 Col3
    ## 1    1    2    3
    ## 2    4    5    6
    ## 3    7    8    9
    ## 4    a    b    c

``` r
# text 2 is separate by $, use any read.xxx but specify sep="$"
# read.csv & read.delim give you the same thing
read.csv("https://bioboot.github.io/bimm143_S19/class-material/test2.txt", sep="$", header=TRUE)
```

    ##   Col1 Col2 Col3
    ## 1    1    2    3
    ## 2    4    5    6
    ## 3    7    8    9
    ## 4    a    b    c

``` r
read.delim("https://bioboot.github.io/bimm143_S19/class-material/test2.txt", sep="$", header=TRUE)
```

    ##   Col1 Col2 Col3
    ## 1    1    2    3
    ## 2    4    5    6
    ## 3    7    8    9
    ## 4    a    b    c

``` r
#text 3 is separate by white space
# use read.table as defalut , dont have to put sep""
# header=false when the first row is not your header
read.table("https://bioboot.github.io/bimm143_S19/class-material/test3.txt", header=FALSE)
```

    ##   V1 V2 V3
    ## 1  1  6  a
    ## 2  2  7  b
    ## 3  3  8  c
    ## 4  4  9  d
    ## 5  5 10  e

``` r
read.delim("https://bioboot.github.io/bimm143_S19/class-material/test3.txt", sep="", header=FALSE)
```

    ##   V1 V2 V3
    ## 1  1  6  a
    ## 2  2  7  b
    ## 3  3  8  c
    ## 4  4  9  d
    ## 5  5 10  e

``` r
# simplify the code... 
#df$a <- (df$a - min(df$a)) / (max(df$a) - min(df$a))
#df$b <- (df$b - min(df$a)) / (max(df$b) - min(df$b))
#df$c <- (df$c - min(df$c)) / (max(df$c) - min(df$c))
#df$d <- (df$d - min(df$d)) / (max(df$a) - min(df$d))
```

``` r
# Simplify to work with a generic vector named “x”
# note that we call the min() function twice.. 
# x <- (x - min(x)) / (max(x) - min(x))


# name min(x) to xmin, then rename the entire thing as x
# xmin <- min(x)
# x <- (x - xmin) / (max(x) - xmin)

# Further optimization to use the range() function..
# instead of using xmin; rng[1] 
# rng <- range(x)
# x <- (x - rng[1]) / (rng[2] - rng[1])

rescale <- function(x) {
  rng <- range(x)
  (x - rng[2]) / (rng[2] - rng[1])
}

rescale(1:2)
```

    ## [1] -1  0

``` r
rescale <- function(x, na.rm=TRUE, plot=FALSE) {
  
    rng <-range(x, na.rm=na.rm)
    print("Hello")
    
   answer <- (x - rng[1]) / (rng[2] - rng[1])
   # return(answer) here? just give you answer of the previous function, basically stop here
   
   print("is it me you are looking for?")
   
   if(plot) {
      plot(answer, typ="b", lwd=4)
   }
   print("I can see it in ...")
   return(answer)
}
```

``` r
rescale(1:10, plot=TRUE)
```

    ## [1] "Hello"
    ## [1] "is it me you are looking for?"

![](class6_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

    ## [1] "I can see it in ..."

    ##  [1] 0.0000000 0.1111111 0.2222222 0.3333333 0.4444444 0.5555556 0.6666667
    ##  [8] 0.7777778 0.8888889 1.0000000

``` r
add <- function(x,y=1)
  # sum the input x and y
  x + y
```

``` r
add(1)
```

    ## [1] 2

``` r
# 1 = x , add x + y, y=1 is at the defalut
add(5,5)
```

    ## [1] 10

``` r
# add(1, "bb") will give error


add <- function(x, y=1) {
  # summ the input x and y
  x + y
}

add(x=1, y=4)
```

    ## [1] 5

``` r
add(1,4)
```

    ## [1] 5

``` r
add(1)
```

    ## [1] 2

``` r
add(c(1,2,3))
```

    ## [1] 2 3 4

``` r
add(c(1,2,3),4)
```

    ## [1] 5 6 7

``` r
# add(1, 2, 2)
# add(x=1, y="b")
# those two above will give you error becuase there no thrid thing, and do not use characters
```

A new function to re-scale data

``` r
# need a "name", "arguments", and "body"..
rescale <- function(x) {
   rng <-range(x)
   (x - rng[1]) / (rng[2] - rng[1])
}
```

``` r
# test on a small example where you know the answer rescale  (1:10)
rescale(1:10)
```

    ##  [1] 0.0000000 0.1111111 0.2222222 0.3333333 0.4444444 0.5555556 0.6666667
    ##  [8] 0.7777778 0.8888889 1.0000000

``` r
# rescale(c(1,2,NA,3,10))
# this will give you error because of the NA
```

``` r
x <- c(1,2,NA,3,10)
rng <- range(x)
rng
```

    ## [1] NA NA

``` r
# remove the NA = TRUE so will just give NA on the third space 
rescale2 <- function(x) {
   rng <-range(x, na.rm=TRUE)
   (x - rng[1]) / (rng[2] - rng[1])
}
```

``` r
rescale2 (c(1,2,NA,3,10))
```

    ## [1] 0.0000000 0.1111111        NA 0.2222222 1.0000000

``` r
rescale3 <- function(x, na.rm=TRUE, plot=FALSE) {
  
    rng <-range(x, na.rm=na.rm)
    print("Hello")
    
   answer <- (x - rng[1]) / (rng[2] - rng[1])
   return(answer)
   
   print("is it me you are looking for?")
   if(plot) {
      plot(answer, typ="b", lwd=4)
   }
   print("I can see it in ...")
   return(answer)
}
```

``` r
rescale3(1:10, plot=TRUE)
```

    ## [1] "Hello"

    ##  [1] 0.0000000 0.1111111 0.2222222 0.3333333 0.4444444 0.5555556 0.6666667
    ##  [8] 0.7777778 0.8888889 1.0000000

# Section 2 of Hands-on Worksheet

Install the **bio3d** package for sequence and structure analysis

``` r
# after install the package, read the library of the package
library(bio3d)
s1 <- read.pdb("4AKE")  # kinase with drug
```

    ##   Note: Accessing on-line PDB file

``` r
s2 <- read.pdb("1AKE")  # kinase no drug
```

    ##   Note: Accessing on-line PDB file
    ##    PDB has ALT records, taking A only, rm.alt=TRUE

``` r
s3 <- read.pdb("1E4Y")  # kinase with drug
```

    ##   Note: Accessing on-line PDB file

``` r
s1.chainA <- trim.pdb(s1, chain="A", elety="CA")
s2.chainA <- trim.pdb(s2, chain="A", elety="CA")
s3.chainA <- trim.pdb(s1, chain="A", elety="CA")

s1.b <- s1.chainA$atom$b
s2.b <- s2.chainA$atom$b
s3.b <- s3.chainA$atom$b

plotb3(s1.b, sse=s1.chainA, typ="l", ylab="Bfactor")
```

![](class6_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
plotb3(s2.b, sse=s2.chainA, typ="l", ylab="Bfactor")
```

![](class6_files/figure-gfm/unnamed-chunk-18-2.png)<!-- -->

``` r
plotb3(s3.b, sse=s3.chainA, typ="l", ylab="Bfactor")
```

![](class6_files/figure-gfm/unnamed-chunk-18-3.png)<!-- -->
