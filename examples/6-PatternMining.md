# Pattern Mining
## Library


``` r
# DAL ToolBox
# version 1.0.77


library(daltoolbox)

library(arules)
```

```
## Error in library(arules): não há nenhum pacote chamado 'arules'
```

``` r
library(arulesViz)
```

```
## Error in library(arulesViz): não há nenhum pacote chamado 'arulesViz'
```

``` r
library(arulesSequences)
```

```
## Error in library(arulesSequences): não há nenhum pacote chamado 'arulesSequences'
```


``` r
data(AdultUCI)
```

```
## Warning in data(AdultUCI): conjunto de dados 'AdultUCI' não encontrado
```

``` r
dim(AdultUCI)
```

```
## Error: objeto 'AdultUCI' não encontrado
```

``` r
head(AdultUCI)
```

```
## Error: objeto 'AdultUCI' não encontrado
```

## Removing attributes


``` r
AdultUCI$fnlwgt <- NULL
```

```
## Error in eval(ei, envir): objeto 'AdultUCI' não encontrado
```

``` r
AdultUCI$"education-num" <- NULL
```

```
## Error in eval(ei, envir): objeto 'AdultUCI' não encontrado
```

## Conceptual Hierarchy and Binning


``` r
AdultUCI$age <- ordered(cut(AdultUCI$age, c(15,25,45,65,100)),
                              labels = c("Young", "Middle-aged", "Senior", "Old"))
```

```
## Error: objeto 'AdultUCI' não encontrado
```

``` r
AdultUCI$"hours-per-week" <- ordered(cut(AdultUCI$"hours-per-week",
                                             c(0,25,40,60,168)),
                                         labels = c("Part-time", "Full-time", "Over-time", "Workaholic"))
```

```
## Error: objeto 'AdultUCI' não encontrado
```

``` r
AdultUCI$"capital-gain" <- ordered(cut(AdultUCI$"capital-gain",
                                           c(-Inf,0,median(AdultUCI$"capital-gain"[AdultUCI$"capital-gain">0]),
                                             Inf)), labels = c("None", "Low", "High"))
```

```
## Error: objeto 'AdultUCI' não encontrado
```

``` r
AdultUCI$"capital-loss" <- ordered(cut(AdultUCI$"capital-loss",
                                           c(-Inf,0, median(AdultUCI$"capital-loss"[AdultUCI$"capital-loss">0]),
                                             Inf)), labels = c("None", "Low", "High"))
```

```
## Error: objeto 'AdultUCI' não encontrado
```

``` r
head(AdultUCI)
```

```
## Error: objeto 'AdultUCI' não encontrado
```

## Convert to transactions


``` r
AdultTrans <- as(AdultUCI, "transactions")
```

```
## Error: objeto 'AdultUCI' não encontrado
```

## A Priori


``` r
rules <- apriori(AdultTrans, parameter=list(supp = 0.5, conf = 0.9, minlen=2, maxlen= 10, target = "rules"), 
                 appearance=list(rhs = c("capital-gain=None"), default="lhs"), control=NULL)
```

```
## Error in apriori(AdultTrans, parameter = list(supp = 0.5, conf = 0.9, : não foi possível encontrar a função "apriori"
```

``` r
inspect(rules)
```

```
## Error in inspect(rules): não foi possível encontrar a função "inspect"
```


``` r
rules_a <- as(rules, "data.frame")
```

```
## Error: objeto 'rules' não encontrado
```

``` r
head(rules_a)
```

```
## Error: objeto 'rules_a' não encontrado
```

## Analysis of Rules


``` r
imrules <- interestMeasure(rules, transactions = AdultTrans)
```

```
## Error in interestMeasure(rules, transactions = AdultTrans): não foi possível encontrar a função "interestMeasure"
```

``` r
head(imrules)
```

```
## Error: objeto 'imrules' não encontrado
```

## Removing redundant rules


``` r
nrules <- rules[!is.redundant(rules)]
```

```
## Error: objeto 'rules' não encontrado
```


``` r
arules::inspect(nrules)
```

```
## Error in loadNamespace(x): não há nenhum pacote chamado 'arules'
```

## Showing the transactions that support the rules
In this example, we can see the transactions (trans) that support rules 1. 


``` r
st <- supportingTransactions(nrules[1], AdultTrans)
```

```
## Error in supportingTransactions(nrules[1], AdultTrans): não foi possível encontrar a função "supportingTransactions"
```

``` r
trans <- unique(st@data@i)
```

```
## Error: objeto 'st' não encontrado
```

``` r
length(trans)
```

```
## Error: objeto 'trans' não encontrado
```

``` r
print(c(length(trans)/length(AdultTrans), nrules[1]@quality$support))
```

```
## Error: objeto 'trans' não encontrado
```

Now we can see the transactions (trans) that support rules 1 and 2. 
As can be observed, the support for both rules is not the sum of the support of each rule. 


``` r
st <- supportingTransactions(nrules[1:2], AdultTrans)
```

```
## Error in supportingTransactions(nrules[1:2], AdultTrans): não foi possível encontrar a função "supportingTransactions"
```

``` r
trans <- unique(st@data@i)
```

```
## Error: objeto 'st' não encontrado
```

``` r
length(trans)
```

```
## Error: objeto 'trans' não encontrado
```

``` r
print(c(length(trans)/length(AdultTrans), nrules[1:2]@quality$support))
```

```
## Error: objeto 'trans' não encontrado
```

## Rules visualization


``` r
options(repr.plot.width=10, repr.plot.height=5)
plot(rules)
```

```
## Error: objeto 'rules' não encontrado
```


``` r
options(repr.plot.width=10, repr.plot.height=5)
plot(rules, method="paracoord", control=list(reorder=TRUE))
```

```
## Error: objeto 'rules' não encontrado
```

# Sequence Mining


``` r
x <- read_baskets(con = system.file("misc", "zaki.txt", package = "arulesSequences"), info = c("sequenceID","eventID","SIZE"))
```

```
## Error in read_baskets(con = system.file("misc", "zaki.txt", package = "arulesSequences"), : não foi possível encontrar a função "read_baskets"
```

``` r
as(x, "data.frame")
```

```
## Error in as(x, "data.frame"): no method or default for coercing "matrix" to "data.frame"
```


``` r
s1 <- cspade(x, parameter = list(support = 0.4), control = list(verbose = TRUE))
```

```
## Error in cspade(x, parameter = list(support = 0.4), control = list(verbose = TRUE)): não foi possível encontrar a função "cspade"
```

``` r
as(s1, "data.frame")
```

```
## Error: objeto 's1' não encontrado
```

