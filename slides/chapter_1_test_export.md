---
title: Box and whisker plots and reordering levels
key: ff2bfc53b0daea92741ed64184f68c9e
video_link:
    hls: https://videos.datacamp.com/transcoded/3094_lattice/v3/hls-ch1_3.master.m3u8
    mp4: https://videos.datacamp.com/transcoded_mp4/3094_lattice/v3/ch1_3.mp4
transformations:
    translateX: 70
    translateY: -6
    scale: 1.30


--- type:TitleSlide key:48a6fbd967
## Box and whisker plots and reordering levels


*** =lower_third
name: Deepayan Sarkar
title: Associate Professor, Indian Statistical Institute

*** =script



--- type:FullSlide key:9beee12ea2
## Box and whisker plots: `bwplot()`

*** =part1

```r
> bwplot(~ rate.male, data = USCancerRates)
```

![](http://s3.amazonaws.com/assets.datacamp.com/production/course_3094/datasets/ch1-bw1-1.png)


*** =script


By now, it should be clear to you that lattice has _different_ high-level functions, for different plot types.

So far, we've seen `xyplot()` for scatter plots, `histogram()` for histograms, and `densityplot()` for kernel density estimates.

Next you'll learn about `bwplot()`, for box and whisker plots.

Lattice box and whisker plots consist of a dot representing the median, and a box representing the first and third quartiles. 

Whiskers normally extend from the box to the most extreme data points, but in R they are no longer than 1.5 times the inter-quartile range.

Any data point beyond this limit is flagged as a potential outlier and plotted separately.

In a way, box and whisker plots serve the same purpose as a histogram or a density plot, because it visually describes the distribution of a numeric variable. 

So, the formula in a `bwplot()` call can look similar to the formula in a `histogram()` or `densityplot()` call. 

--- type:FullSlide key:2d76f9dc87
## Comparative box and whisker plots

*** =part1

```r
> bwplot(state ~ rate.male, data = USCancerRates)
```

![](http://www.isid.ac.in/~deepayan/tmp/figures/ch1-bw2-1.png)


*** =script

However, the main advantage of the design of a box and whisker plot, is that it's more compact, and so it can be used not just to summarize, but also _compare_ several distributions at once.

Here for example, we compare the death-rate due to cancer, across states. 

This is done by specifying `state` as the `y`-variable in the formula for `bwplot()`.

This plot illustrates a phenomenon that's common when working with categorical variables, or factors, such as `state` in this example. 

By default, R orders the levels of a categorical variable by sorting them alphabetically. 

This is a reasonable default if there's no  natural ordering.

However, when plotting numeric data after grouping them by a factor, it's often useful to change the order of the factor levels to match the numeric data in some way. 

--- type:FullSlide key:713af59743
## Reordering factor levels

*** =part1

```r
> library(dplyr)
> USCancerRates <- mutate(USCancerRates, 
+     state.ordered = reorder(state, rate.male, median, na.rm = TRUE))
> bwplot(state.ordered ~ rate.male, data = USCancerRates)
```

![](http://www.isid.ac.in/~deepayan/tmp/figures/ch1-bw3-1.png)


*** =script

The R function `reorder()` is very useful in such situations. 

It reorders the levels of a factor so that the new order matches some summary measure of a relevant numeric variable.

For example, we use it here to reorder the states by the median value of `rate.male`. 

In the new order, the first state has lowest median rate, and the last state has highest median rate.

From the box and whisker plot created using this new ordering, it's easy to identify the states, which have relatively low or high rates of death. 

It's also easier to see how much the states differ from each other. 

You'll now create some box and whisker plots of your own.

--- type:FinalSlide key:931fdc58ae
## Let's practice!
