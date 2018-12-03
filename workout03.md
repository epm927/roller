Workout 3 Tutorial
================
Ethan M.
December 2, 2018

``` r
library(roller)
```

    ## 
    ## Attaching package: 'roller'

    ## The following object is masked from 'package:graphics':
    ## 
    ##     plot

``` r
set.seed(123)
```

### General Information

This package is designed to simulate rolling a specificed `device()` a specified number of times.

### Device:

Users are able to specify any type of device, so long as the number of sides is greater than one and the probabilities obey the basic axioms of probability (i.e. are nonnegative, between 0 and 1, and sum to 1). The default is a fair "coin" with two sides ("1" and "2") of equal probability:

``` r
fair_coin <- device()
fair_coin
```

    ## object "device"
    ## 
    ##   sides prob
    ## 1     1  0.5
    ## 2     2  0.5

You can also specify nonstandard devices, of any length:

``` r
tri_die <- device(c("1", "2", "3"), prob = c(1/3, 1/3, 1/3))
tri_die
```

    ## object "device"
    ## 
    ##   sides      prob
    ## 1     1 0.3333333
    ## 2     2 0.3333333
    ## 3     3 0.3333333

 

### Rolls:

Users are also able to simulate rolling a device using the `roll()` function. The function takes an object of class "device" and rolls it a specified number of times (`times` must be a positive integer).

``` r
roll(fair_coin, 2)
```

    ## object 'rolls' 
    ## 
    ## $rolls
    ## [1] 2 1

``` r
roll(tri_die, 100)
```

    ## object 'rolls' 
    ## 
    ## $rolls
    ##   [1] "3" "1" "1" "2" "3" "1" "3" "3" "1" "3" "1" "3" "2" "1" "2" "2" "2"
    ##  [18] "1" "1" "1" "3" "1" "3" "1" "3" "3" "2" "2" "1" "1" "1" "1" "2" "3"
    ##  [35] "1" "2" "2" "2" "2" "3" "3" "3" "2" "2" "2" "3" "2" "1" "2" "3" "1"
    ##  [52] "2" "3" "2" "2" "1" "1" "3" "3" "2" "3" "2" "1" "3" "1" "1" "1" "3"
    ##  [69] "1" "3" "1" "2" "3" "2" "3" "3" "3" "2" "2" "1" "3" "1" "2" "3" "1"
    ##  [86] "1" "1" "2" "2" "3" "3" "3" "2" "2" "1" "2" "3" "3" "3" "2"

 

### Plotting:

This package comes with a default `plot()` function, which produces a frequency barchart of the rolls of a device.

``` r
die <- device(sides = 1:6, prob = rep(1/6, 6))
rolls100 <- roll(die, 100)
plot(rolls100)
```

![](workout03_files/figure-markdown_github/unnamed-chunk-5-1.png)

 

### Additional methods

You can subset, replace, and add rolls using `[`, `[<-`, and `+`&lt; respectively:

``` r
die100 <- roll(die, 100)
die100[30]
```

    ## [1] 4

``` r
die100[30] <- 2
die200 <- die100 + 100
summary(die200)
```

    ## summary "rolls"
    ## 
    ##   side count  prop
    ## 1    1    33 0.165
    ## 2    2    36 0.180
    ## 3    3    35 0.175
    ## 4    4    37 0.185
    ## 5    5    25 0.125
    ## 6    6    34 0.170

``` r
die200$total
```

    ## [1] 200

 

### Some Examples:

Here are some examples of how to use the advanced functionality of the `Roller` Package:

``` r
# roll fair 8-sided die
set.seed(123)
fair_dev <- device(sides = letters[1:8], prob = rep(1/8, 8))
fair500 <- roll(fair_dev, times = 500)

# summary method
summary(fair500)
```

    ## summary "rolls"
    ## 
    ##   side count  prop
    ## 1    a    63 0.126
    ## 2    b    54 0.108
    ## 3    c    73 0.146
    ## 4    d    69 0.138
    ## 5    e    69 0.138
    ## 6    f    51 0.102
    ## 7    g    65 0.130
    ## 8    h    56 0.112

``` r
# extracting roll in position 500
fair500[500]
```

    ## [1] "h"

``` r
# replacing last roll
fair500[500] <- 'a'
fair500[500]
```

    ## [1] "a"

``` r
# adding 100 rolls
fair600 <- fair500 + 100
summary(fair600)
```

    ## summary "rolls"
    ## 
    ##   side count      prop
    ## 1    a    79 0.1316667
    ## 2    b    69 0.1150000
    ## 3    c    78 0.1300000
    ## 4    d    85 0.1416667
    ## 5    e    78 0.1300000
    ## 6    f    67 0.1116667
    ## 7    g    74 0.1233333
    ## 8    h    70 0.1166667

``` r
# plot method
plot(fair500)
```

![](workout03_files/figure-markdown_github/unnamed-chunk-7-1.png)
