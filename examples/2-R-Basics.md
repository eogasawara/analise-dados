#### R Package installation and loading

Package checking and instalation


``` r
if(!require(daltoolbox)) { 
  install.packages("daltoolbox")
}
```

Package loading


``` r
library(daltoolbox)
```

#### Variable definitions and evaluation

Variable definition


``` r
weight <- 60
height = 1.75
subject <- "A"
healthy <- TRUE
```

Variable evaluation


``` r
weight
```

```
## [1] 60
```

#### Functions for type checking


``` r
is.numeric(weight) # variable 
```

```
## [1] TRUE
```

``` r
is.double(weight)
```

```
## [1] TRUE
```

``` r
is.integer(weight)
```

```
## [1] FALSE
```

``` r
is.character(subject)
```

```
## [1] TRUE
```

#### Functions for variable conversion


``` r
weight <- as.integer(weight)
is.integer(weight)
```

```
## [1] TRUE
```

#### Formulas and String formatting

Computing the body mass index (BMI) from the weight and height


``` r
#Body mass index (BMI)
bmi <- weight/height^2 
bmi 
```

```
## [1] 19.59184
```

Functions for string manipulation


``` r
message <- sprintf("%.1f", bmi)
print(message)
```

```
## [1] "19.6"
```

#### Vectors

definition


``` r
weight <- c(60, 72, 57, 90, 95, 72) 
height <- c(1.75, 1.80, 1.65, 1.90, 1.74, 1.91)
subject <- c("A", "B", "C", "D", "E", "F")
```

evaluation


``` r
weight
```

```
## [1] 60 72 57 90 95 72
```

``` r
height
```

```
## [1] 1.75 1.80 1.65 1.90 1.74 1.91
```

``` r
subject
```

```
## [1] "A" "B" "C" "D" "E" "F"
```

#### Establishing the vector size

vector of size 10


``` r
vec <- rep(0, 10)
vec
```

```
##  [1] 0 0 0 0 0 0 0 0 0 0
```

vector length


``` r
length(weight)
```

```
## [1] 6
```

#### Vector limits

from one to the length of the vector


``` r
weight[1]
```

```
## [1] 60
```

``` r
weight[length(weight)]
```

```
## [1] 72
```

#### Iteration: for loop

from one to the length of weight


``` r
bmi <- 0
for (i in 1:length(weight)) {
  bmi[i] <- weight[i]/height[i]^2
}
```

evaluation of the bmi vector


``` r
bmi
```

```
## [1] 19.59184 22.22222 20.93664 24.93075 31.37799 19.73630
```

#### Iteration: while loop

run while i is below or equal to the length of weight


``` r
bmi <- 0
i <- 1
while (i <= length(weight)) {
  bmi[i] <- weight[i]/height[i]^2
  i <- i + 1
}
```


``` r
bmi
```

```
## [1] 19.59184 22.22222 20.93664 24.93075 31.37799 19.73630
```

#### Remove a variable


``` r
rm(bmi)
exists("bmi")
```

```
## [1] FALSE
```

#### Processing vectors at once



``` r
bmi <- weight/height^2 
bmi 
```

```
## [1] 19.59184 22.22222 20.93664 24.93075 31.37799 19.73630
```

#### Creating functions

name <- function(parameters) { body }


``` r
compute_bmi <- function(weight, height) {
  bmi <- weight/height^2 
  return(bmi)
}
```

calling it


``` r
bmi <- compute_bmi(60, 1.75)
bmi
```

```
## [1] 19.59184
```

#### Function processing vectors


``` r
bmi <- compute_bmi(weight, height)
bmi
```

```
## [1] 19.59184 22.22222 20.93664 24.93075 31.37799 19.73630
```

#### Example: function to compute the average

(iterating in all elements of the vector)


``` r
average <- function(vec) {
    s <- 0
    n <- length(vec)
    for (x in vec) {
      s <- s + x  
    }
    return(s/n)
}
```

invoking the function


``` r
avg_bmi <- average(bmi)
avg_bmi
```

```
## [1] 23.13262
```

#### Example of a function to compute the average (improved version)

manipulating vectors at once


``` r
average <- function(vec) {
    s <- sum(vec)
    n <- length(vec)
    return(s/n)
}
```

invoking the function


``` r
avg_bmi <- average(bmi)
avg_bmi
```

```
## [1] 23.13262
```

#### Example: function using mean function

Major statistical functions are available in R


``` r
average <- function(vec) {
    return(mean(vec))
}
```

invoking the function


``` r
avg_bmi <- average(bmi)
avg_bmi
```

```
## [1] 23.13262
```

#### Not available (NA)

Operations with NA lead to NA.


``` r
x <- c(10, NA, 13)
y <- average(x)
y
```

```
## [1] NA
```

Addressing NA with na.rm=TRUE


``` r
average <- function(vec) {
    return(mean(vec, na.rm=TRUE))
}
```


``` r
x <- c(10, NA, 13)
y <- average(x)
y
```

```
## [1] 11.5
```

#### Plotting basic graphics

defining variables


``` r
weight <- c(60, 72, 57, 90, 95, 72) 
height <- c(1.75, 1.80, 1.65, 1.90, 1.74, 1.91)
bmi <- weight/height^2 
```

scatter plots


``` r
plot(height, weight)
```

![plot of chunk unnamed-chunk-33](fig/2-R-Basics/unnamed-chunk-33-1.png)

#### Most functions contain many default parameters


``` r
plot(height, weight, pch=2)
```

![plot of chunk unnamed-chunk-34](fig/2-R-Basics/unnamed-chunk-34-1.png)

#### All functions in R that belongs to packages have help with examples


``` r
?base::plot
```

#### Canvas for plotting is still active until a new plot


``` r
plot(height, weight)
hh = c(1.65, 1.70, 1.75, 1.80, 1.85, 1.90)
lines(hh, 22.5 * hh^2)
```

![plot of chunk unnamed-chunk-36](fig/2-R-Basics/unnamed-chunk-36-1.png)

#### Factors

Factors are used to handle categorical data.


``` r
pain <- c(0,3,2,2,1)
fpain <- factor(pain,levels=0:3, ordered=TRUE)
fpain
```

```
## [1] 0 3 2 2 1
## Levels: 0 < 1 < 2 < 3
```

Levels provide correspondence between numerical values and categorical labels


``` r
levels(fpain) <- c("none","mild","medium","severe")
fpain
```

```
## [1] none   severe medium medium mild  
## Levels: none < mild < medium < severe
```

#### Convert height to factor with levels: small, medium, high

coding setting element by element


``` r
lev <- rep("", length(height))

for (i in 1:length(height)) {
  if (height[i] < 1.5)
    lev[i] <- "short"
  else if (height[i] < 1.9)
    lev[i] <- "medium"
  else 
    lev[i] <- "tall"
}

lev <- as.factor(lev)
lev
```

```
## [1] medium medium medium tall   medium tall  
## Levels: medium tall
```

#### Using the function cut


``` r
lev <- cut(height, breaks=c(0, 1.5, 1.9, .Machine$double.xmax), ordered=TRUE)
lev
```

```
## [1] (1.5,1.9]      (1.5,1.9]      (1.5,1.9]      (1.5,1.9]      (1.5,1.9]      (1.9,1.8e+308]
## Levels: (0,1.5] < (1.5,1.9] < (1.9,1.8e+308]
```

``` r
levels(lev) <- c("short", "medium", "tall")
lev
```

```
## [1] medium medium medium medium medium tall  
## Levels: short < medium < tall
```

#### Matrix

Matrices can be filled from vectors or data frames. 


``` r
x <- 1:9
x
```

```
## [1] 1 2 3 4 5 6 7 8 9
```

Converting a vector to matrix


``` r
dim(x) <- c(3,3)
x
```

```
##      [,1] [,2] [,3]
## [1,]    1    4    7
## [2,]    2    5    8
## [3,]    3    6    9
```

#### Scalar multiplication


``` r
y <- 3*x
y
```

```
##      [,1] [,2] [,3]
## [1,]    3   12   21
## [2,]    6   15   24
## [3,]    9   18   27
```

#### Matrix manipulation

Converting a vector to a matrix by row


``` r
x <- matrix(1:9,nrow=3,byrow=T)
x
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]    4    5    6
## [3,]    7    8    9
```

transposing a matrix


``` r
x <- t(x)
x
```

```
##      [,1] [,2] [,3]
## [1,]    1    4    7
## [2,]    2    5    8
## [3,]    3    6    9
```

#### Lists

Lists are used to work with "objects"


``` r
a <- c(5260,5470,5640,6180,6390,6515,6805,7515,7515,8230,8770)
b <- c(3910,4220,3885,5160,5645,4680,5265,5975,6790,6900,7335)

mybag <- list(a, b, 0, "a")
mybag
```

```
## [[1]]
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
## 
## [[2]]
##  [1] 3910 4220 3885 5160 5645 4680 5265 5975 6790 6900 7335
## 
## [[3]]
## [1] 0
## 
## [[4]]
## [1] "a"
```

#### Adding elements into a list


``` r
n <- length(mybag)
mybag[[n+1]] <- "b"
mybag
```

```
## [[1]]
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
## 
## [[2]]
##  [1] 3910 4220 3885 5160 5645 4680 5265 5975 6790 6900 7335
## 
## [[3]]
## [1] 0
## 
## [[4]]
## [1] "a"
## 
## [[5]]
## [1] "b"
```

#### List slicing


``` r
slice <- mybag[1]
slice
```

```
## [[1]]
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
```

``` r
is.list(slice)
```

```
## [1] TRUE
```

#### Lists: member reference

Picking the first element


``` r
h <- mybag[[1]]
h
```

```
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
```

An element can be evaluated. In this case, it is a vector.


``` r
is.vector(h)
```

```
## [1] TRUE
```

``` r
is.list(h)
```

```
## [1] FALSE
```

#### Creating lists with attributes

They are properties on the list


``` r
mybag <- list(x=a, y=b, const=0, lit="a")
mybag
```

```
## $x
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
## 
## $y
##  [1] 3910 4220 3885 5160 5645 4680 5265 5975 6790 6900 7335
## 
## $const
## [1] 0
## 
## $lit
## [1] "a"
```

#### Adding, accessing, and removing elements


``` r
mybag$c <- mybag$x - mybag$y
mybag$const <- NULL
mybag$lit <- NULL
mybag
```

```
## $x
##  [1] 5260 5470 5640 6180 6390 6515 6805 7515 7515 8230 8770
## 
## $y
##  [1] 3910 4220 3885 5160 5645 4680 5265 5975 6790 6900 7335
## 
## $c
##  [1] 1350 1250 1755 1020  745 1835 1540 1540  725 1330 1435
```

#### Data frames
Data frames (tables) provide support for structured data. 


``` r
a <- c(5260,5470,5640,6180,6390,6515,6805,7515,7515,8230,8770)
b <- c(3910,4220,3885,5160,5645,4680,5265,5975,6790,6900,7335)
```


``` r
data <- data.frame(A=a, B=b)
head(data)
```

```
##      A    B
## 1 5260 3910
## 2 5470 4220
## 3 5640 3885
## 4 6180 5160
## 5 6390 5645
## 6 6515 4680
```

#### Adding a column in a data frame 


``` r
data$c <- data$A + data$B
head(data)
```

```
##      A    B     c
## 1 5260 3910  9170
## 2 5470 4220  9690
## 3 5640 3885  9525
## 4 6180 5160 11340
## 5 6390 5645 12035
## 6 6515 4680 11195
```

#### Removing a column of a data frame 


``` r
data$A <- NULL
head(data)
```

```
##      B     c
## 1 3910  9170
## 2 4220  9690
## 3 3885  9525
## 4 5160 11340
## 5 5645 12035
## 6 4680 11195
```

####  Reading a csv file
There are many functions for reading CSV, Excel, and RData formats.


``` r
wine = read.table(
    "http://archive.ics.uci.edu/ml/machine-learning-databases/wine/wine.data", 
                  header = TRUE, sep = ",")
  colnames(wine) <- c('Type', 'Alcohol', 'Malic', 'Ash', 
                      'Alcalinity', 'Magnesium', 'Phenols', 
                      'Flavanoids', 'Nonflavanoids',
                      'Proanthocyanins', 'Color', 'Hue', 
                      'Dilution', 'Proline')
head(wine)
```

```
##   Type Alcohol Malic  Ash Alcalinity Magnesium Phenols Flavanoids Nonflavanoids Proanthocyanins
## 1    1   13.20  1.78 2.14       11.2       100    2.65       2.76          0.26            1.28
## 2    1   13.16  2.36 2.67       18.6       101    2.80       3.24          0.30            2.81
## 3    1   14.37  1.95 2.50       16.8       113    3.85       3.49          0.24            2.18
## 4    1   13.24  2.59 2.87       21.0       118    2.80       2.69          0.39            1.82
## 5    1   14.20  1.76 2.45       15.2       112    3.27       3.39          0.34            1.97
## 6    1   14.39  1.87 2.45       14.6        96    2.50       2.52          0.30            1.98
##   Color  Hue Dilution Proline
## 1  4.38 1.05     3.40    1050
## 2  5.68 1.03     3.17    1185
## 3  7.80 0.86     3.45    1480
## 4  4.32 1.04     2.93     735
## 5  6.75 1.05     2.85    1450
## 6  5.25 1.02     3.58    1290
```

####  saving in binary format 

saving a data frame



``` r
save(wine, file="wine.RData")
```

removing a data frame from memory


``` r
rm(wine)
```

loading it


``` r
load("wine.RData")
head(wine, 3)
```

```
##   Type Alcohol Malic  Ash Alcalinity Magnesium Phenols Flavanoids Nonflavanoids Proanthocyanins
## 1    1   13.20  1.78 2.14       11.2       100    2.65       2.76          0.26            1.28
## 2    1   13.16  2.36 2.67       18.6       101    2.80       3.24          0.30            2.81
## 3    1   14.37  1.95 2.50       16.8       113    3.85       3.49          0.24            2.18
##   Color  Hue Dilution Proline
## 1  4.38 1.05     3.40    1050
## 2  5.68 1.03     3.17    1185
## 3  7.80 0.86     3.45    1480
```

####  exporting data.frame into csv file


``` r
write.table(wine, file="wine.csv", row.names=FALSE, quote = FALSE, sep = ",")
```

####  filtering vectors


``` r
a <- c(5260,5470,5640,6180,6390,6515,6805,7515,7515,8230,8770)

# logical vector
bool <- (a > 7000)
bool
```

```
##  [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE  TRUE  TRUE
```


``` r
# selecting elements from positions that are true
a[bool] 
```

```
## [1] 7515 7515 8230 8770
```

``` r
a[a > 7000] 
```

```
## [1] 7515 7515 8230 8770
```
####  filtering data frames


``` r
a <- c(5260,5470,5640,6180,6390,6515,6805,7515,7515,8230,8770)
b <- c(3910,4220,3885,5160,5645,4680,5265,5975,6790,6900,7335)
data <- data.frame(a = a, b = b)
head(data[data$a > 7000,])
```

```
##       a    b
## 8  7515 5975
## 9  7515 6790
## 10 8230 6900
## 11 8770 7335
```

####  filtering data frames (rows and columns)


``` r
head(data[data$a > 7000,c(1)])
```

```
## [1] 7515 7515 8230 8770
```

#### Benchmarking performance of matrix and data frames


``` r
rheight <- rnorm(100000, 1.8, sd=0.2)
rweight <- rnorm(100000, 72, sd=15)
```

#### Computing a column at once in a data frame


``` r
start_time <- Sys.time()

hw <- data.frame(height=rheight, weight=rweight)
hw$bmi <- hw$weight/hw$height^2

end_time <- Sys.time()
end_time - start_time
```

```
## Time difference of 0.001940012 secs
```

``` r
object.size(hw)
```

```
## 2400984 bytes
```

#### Computing a column in a data frame cell by cell


``` r
start_time <- Sys.time()
hw <- data.frame(height=rheight, weight=rweight)
for (i in 1:nrow(hw)) {
  hw$bmi[i] <- hw$weight[i]/hw$height[i]^2
}
end_time <- Sys.time()
end_time - start_time
```

```
## Time difference of 9.116586 secs
```

#### Converting a data frame to a matrix, processing it, and going back


``` r
start_time <- Sys.time()
hw <- data.frame(height=rheight, weight=rweight)

hw <- as.matrix(hw)

hw <- cbind(hw, 0)
for (i in 1:nrow(hw)) {
  hw[i,3] <- hw[i,2]/hw[i,1]^2
}

hw <- as.data.frame(hw)

end_time <- Sys.time()
end_time - start_time
```

```
## Time difference of 0.3820381 secs
```

#### Pipelines
The operator |> creates a pipeline. 

The first parameter of the next invoked function receives the data from the pipeline. 

Library $dplyr$ contains a set of functions that support relational algebra operations.


``` r
flight_data <- read.table(text = "Year Quarter Flights Delays
                     2016 1 11 6
                     2016 2 12 5
                     2016 3 13 3
                     2016 4 12 5
                     2017 1 10 4
                     2017 2 9 3
                     2017 3 11 4
                     2017 4 25 15
                     2018 1 14 3
                     2018 2 12 5
                     2018 3 13 3
                     2018 4 15 4",
                     header = TRUE,sep = "")  
```

#### Displaying the data frame


``` r
head(flight_data)
```

```
##   Year Quarter Flights Delays
## 1 2016       1      11      6
## 2 2016       2      12      5
## 3 2016       3      13      3
## 4 2016       4      12      5
## 5 2017       1      10      4
## 6 2017       2       9      3
```

#### Basic Query



``` r
library(dplyr)
```


``` r
result <- flight_data |> 
   filter(Delays > 5) |> 
   select(Year, Quarter, Flights)
head(result)
```

```
##   Year Quarter Flights
## 1 2016       1      11
## 2 2017       4      25
```

#### Aggregated query



``` r
result <- flight_data |> 
   group_by(Year) |> 
   summarize(mean = mean(Flights), sd = sd(Flights))
head(result)
```

```
## # A tibble: 3 × 3
##    Year  mean    sd
##   <int> <dbl> <dbl>
## 1  2016  12   0.816
## 2  2017  13.8 7.54 
## 3  2018  13.5 1.29
```

#### Table join

Store table


``` r
stores <- data.frame(
  city = c("Rio de Janeiro", "Sao Paulo", "Paris", "New York", "Tokyo"),
  value = c(10, 12, 20, 25, 18))
head(stores)
```

```
##             city value
## 1 Rio de Janeiro    10
## 2      Sao Paulo    12
## 3          Paris    20
## 4       New York    25
## 5          Tokyo    18
```

Division table


``` r
divisions <- data.frame(
  city = c("Rio de Janeiro", "Sao Paulo", "Paris", "New York", "Tokyo"),
  country = c("Brazil", "Brazil", "France", "US", "Japan"))
head(divisions)
```

```
##             city country
## 1 Rio de Janeiro  Brazil
## 2      Sao Paulo  Brazil
## 3          Paris  France
## 4       New York      US
## 5          Tokyo   Japan
```

#### Merge function

The function $merge$ can be used to join data frames. It can be used to produce inner, left, right, and outer joins. 


``` r
stdiv <- merge(stores, divisions, by.x="city", by.y="city")
head(stdiv)
```

```
##             city value country
## 1       New York    25      US
## 2          Paris    20  France
## 3 Rio de Janeiro    10  Brazil
## 4      Sao Paulo    12  Brazil
## 5          Tokyo    18   Japan
```
#### Aggregating merged data frame


``` r
result <- stdiv |> group_by(country) |> 
   summarize(count = n(), amount = sum(value))
head(result)
```

```
## # A tibble: 4 × 3
##   country count amount
##   <chr>   <int>  <dbl>
## 1 Brazil      2     22
## 2 France      1     20
## 3 Japan       1     18
## 4 US          1     25
```

#### Statistical analysis
There are many statistical tests in R.
One of the most used is the t-test. It checks if the mean of observations is not different from a theoretical value.


``` r
weight <- c(60, 72, 57, 90, 95, 72) 
height <- c(1.75, 1.80, 1.65, 1.90, 1.74, 1.91)
bmi <- weight/height^2 
```


``` r
t.test(bmi, mu=22.5)
```

```
## 
## 	One Sample t-test
## 
## data:  bmi
## t = 0.34488, df = 5, p-value = 0.7442
## alternative hypothesis: true mean is not equal to 22.5
## 95 percent confidence interval:
##  18.41734 27.84791
## sample estimates:
## mean of x 
##  23.13262
```

#### Python + R integration


Python code at retic.py
```text
import pyreadr
import pandas

def add(x, y):
  return x + y

def read_rdata_mem(data):
  x = data["x"]
  print(x)
  y = data["y"]
  data["z"] = x + y
  return(data)
```

Library reticulate enables seamless integration with Python

``` r
library(reticulate)
source_python('https://raw.githubusercontent.com/eogasawara/analise-dados/refs/heads/main/python/retic.py')
x <- add(5, 10)
x
```

```
## [1] 15
```


#### Python + R dataset integration


``` r
data <- data.frame(x = c(1:5), y=c(11:15))
dfm <- read_rdata_mem(data)
```

```
## 0    1
## 1    2
## 2    3
## 3    4
## 4    5
## Name: x, dtype: int32
```

``` r
head(dfm)
```

```
##   x  y  z
## 1 1 11 12
## 2 2 12 14
## 3 3 13 16
## 4 4 14 18
## 5 5 15 20
```
