#### Plotting charts


``` r
# The easiest way to get ggplot2 is to install the whole tidyverse
#install.packages("tidyverse")
#install.packages("ggplot2")

# It is also important to choose the right colors
#install.packages("RColorBrewer")
```


# Data visualization
Data visualization



``` r
library(daltoolbox)
library(ggplot2)
library(RColorBrewer)
```

### Iris datasets
The exploratory analysis is done using iris dataset.


``` r
colors <- brewer.pal(4, 'Set1')
font <- theme(text = element_text(size=16))
```

