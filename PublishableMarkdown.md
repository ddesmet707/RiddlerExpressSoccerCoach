Riddler Express: Soccer Coach
================
David DeSmet
5/24/2019

``` r
knitr::opts_chunk$set(echo = TRUE)
```

## How I solved it

Because I’m terrible at solving anything with beautiful mathematics, I
solved this like I always do Riddlers - with brute force on R.

It’s immediately evident that you should be dealing with the fractions
of their team numbers so that you’re dealing with units of “Goals per
Game” rather than “Games per Goal.” Therefore it also follows that once
we find one solution, we need to go no further as this will be the
optimal solution.

There were two main issues. I assumed I was going to need to make
combinations of numbers, but my computer makes anything past about
choosing 11 numbers out of 26 prohibitively slow. The second concern was
that the computer would make rounding errors that would make the number
work within a tolerance, but not be precisely the answer. So, I need to
demonstrate through nice, round math that the answer truly is precisely
2 goals per game.

``` r
teamNumbers <- combn(26,11)
teamStats <- 1/teamNumbers
teamScores <- colSums(teamStats)
inds <- which((teamScores<2.0000001)&(teamScores>1.9999999))
finalTeam <- teamNumbers[,inds]
productTeam <- 5*2^3*3^2 # 360
Numerator <- productTeam/finalTeam
# If this is precisely the right team number, then this should be precisely 360*2, and it is.
TwoTimes <- sum(Numerator)
if (TwoTimes/productTeam==2){print("Exactly two times!")}
```

    ## [1] "Exactly two times!"

``` r
#Therefore we know the final team is:
print(finalTeam)
```

    ##  [1]  1  5  6  8  9 10 12 15 18 20 24

``` r
#And therefore the optimally weakest player is:
print(finalTeam[11])
```

    ## [1] 24
