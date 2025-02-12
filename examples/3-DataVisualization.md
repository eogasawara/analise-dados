#### Plotting charts


``` r
# The easiest way to get ggplot2 is to install the whole tidyverse
#install.packages("tidyverse")
#install.packages("ggplot2")
```


#### ggplot easy encapsulation through daltoolbox


``` r
library(daltoolbox)
library(ggplot2)
```

#### Color Brewer R Package


``` r
#install.packages("RColorBrewer")
library(RColorBrewer)
colors <- brewer.pal(4, 'Set1')
```


#### Basic setup for examples

Iris datasets


``` r
head(iris)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width
## 1          5.1         3.5          1.4         0.2
## 2          4.9         3.0          1.4         0.2
## 3          4.7         3.2          1.3         0.2
## 4          4.6         3.1          1.5         0.2
## 5          5.0         3.6          1.4         0.2
## 6          5.4         3.9          1.7         0.4
##   Species
## 1  setosa
## 2  setosa
## 3  setosa
## 4  setosa
## 5  setosa
## 6  setosa
```

Options from graphics: colors and font size


``` r
colors <- brewer.pal(4, 'Set1')
font <- theme(text = element_text(size=16))
```

#### Scatter plot



``` r
library(dplyr)
```

```
## 
## Anexando pacote: 'dplyr'
```

```
## Os seguintes objetos são mascarados por 'package:stats':
## 
##     filter, lag
```

```
## Os seguintes objetos são mascarados por 'package:base':
## 
##     intersect, setdiff, setequal, union
```

``` r
grf <- plot_scatter(iris |> select(x = Sepal.Length, value = Sepal.Width, variable = Species), 
                    label_x = "Sepal.Length", label_y = "Sepal.Width", colors=colors[1:3]) + font
plot(grf)
```

![plot of chunk unnamed-chunk-6](fig/3-DataVisualization/unnamed-chunk-6-1.png)
