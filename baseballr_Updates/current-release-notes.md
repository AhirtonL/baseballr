---
layout: page
title: baseballr current release notes (11-22-2016)
tags: rstats, web-scraping, baseballr, NCAA
---

The latest release of the [`baseballr`](https://billpetti.github.io/baseballr/) (0.3.1) includes a function for acquiring player statistics from the [NCAA's website](http://stats.ncaa.org) for baseball teams across the three major divisions (I, II, III).

The function, `ncaa_scrape`, requires the user to pass values for three parameters for the function to work:

`school_id`: numerical code used by the NCAA for each school
`year`: a four-digit year
`type`: whether to pull data for batters or pitchers

If you want to pull batting statistics for Vanderbilt for the 2013 season, you would use the following:

```r
> baseballr::ncaa_scrape(736, 2013, "batting") %>%
+     select(year:OBPct)
   year     school   conference division Jersey            Player Yr Pos GP GS    BA OBPct
1  2013 Vanderbilt Southeastern        1     18 Yastrzemski, Mike Sr  OF 66 66 0.312 0.411
2  2013 Vanderbilt Southeastern        1     20   Harrell, Connor Sr  OF 66 66 0.312 0.418
3  2013 Vanderbilt Southeastern        1      3      Conde, Vince So INF 66 65 0.307 0.380
4  2013 Vanderbilt Southeastern        1      6        Kemp, Tony Jr  OF 66 66 0.391 0.471
5  2013 Vanderbilt Southeastern        1     55    Gregor, Conrad Jr  OF 65 65 0.308 0.440
6  2013 Vanderbilt Southeastern        1      9    Turner, Xavier Fr INF 59 51 0.324 0.387
7  2013 Vanderbilt Southeastern        1      5    Navin, Spencer Jr   C 57 56 0.302 0.430
8  2013 Vanderbilt Southeastern        1     51        Lupo, Jack Sr  OF 57 51 0.297 0.352
9  2013 Vanderbilt Southeastern        1      8    Wiseman, Rhett Fr  OF 54 11 0.289 0.360
10 2013 Vanderbilt Southeastern        1     10     Norwood, John So  OF 33  9 0.328 0.388
11 2013 Vanderbilt Southeastern        1     43      Wiel, Zander So INF 33 15 0.305 0.406
12 2013 Vanderbilt Southeastern        1     44     Harvey, Chris So   C 29 13 0.250 0.328
13 2013 Vanderbilt Southeastern        1     42   McKeithan, Joel Jr INF 25 12 0.220 0.267
14 2013 Vanderbilt Southeastern        1     39       Smith, Kyle Fr INF 23  7 0.250 0.455
15 2013 Vanderbilt Southeastern        1     17    Harris, Andrew Sr INF 21  0 0.125 0.222
16 2013 Vanderbilt Southeastern        1      2   Campbell, Tyler Fr INF 12  2 0.312 0.389
17 2013 Vanderbilt Southeastern        1      7   Swanson, Dansby Fr INF 11  4 0.188 0.435
18 2013 Vanderbilt Southeastern        1     25        Luna, D.J. Jr INF  8  0 0.000 0.333
19 2013 Vanderbilt Southeastern        1     23      Cooper, Will So  OF  4  0 1.000 1.000
20 2013 Vanderbilt Southeastern        1      -            Totals  -   -  -  - 0.313 0.407
21 2013 Vanderbilt Southeastern        1      -   Opponent Totals  -   -  -  - 0.220 0.320
```

The same can be done for pitching, just by changing the `type` parameter:

```r
> baseballr::ncaa_scrape(736, 2013, "pitching") %>%
+     select(year:ERA)
   year     school   conference division Jersey           Player Yr Pos GP App GS  ERA
1  2013 Vanderbilt Southeastern        1     11     Beede, Tyler So   P 37  17 17 2.32
2  2013 Vanderbilt Southeastern        1     33    Miller, Brian So   P 32  32 NA 1.58
3  2013 Vanderbilt Southeastern        1     35    Ziomek, Kevin Jr   P 32  17 17 2.12
4  2013 Vanderbilt Southeastern        1     15   Fulmer, Carson Fr   P 26  26 NA 2.39
5  2013 Vanderbilt Southeastern        1     39      Smith, Kyle Fr INF 23   1 NA 0.00
6  2013 Vanderbilt Southeastern        1     28    Miller, Jared So   P 22  22 NA 2.31
7  2013 Vanderbilt Southeastern        1     19     Rice, Steven Jr   P 21  21 NA 2.57
8  2013 Vanderbilt Southeastern        1     13  Buehler, Walker Fr   P 16  16  9 3.14
9  2013 Vanderbilt Southeastern        1     22  Pfeifer, Philip So   P 15  15 12 3.68
10 2013 Vanderbilt Southeastern        1     12  Ravenelle, Adam So   P 11  11 NA 3.18
11 2013 Vanderbilt Southeastern        1     40   Pecoraro, T.J. Jr   P 10  10  7 5.97
12 2013 Vanderbilt Southeastern        1     45  Ferguson, Tyler Fr   P  8   8  4 4.21
13 2013 Vanderbilt Southeastern        1     27 Kolinsky, Keenan Jr   P  2   2 NA 0.00
14 2013 Vanderbilt Southeastern        1     24    Wilson, Nevin So   P  1   1 NA 0.00
15 2013 Vanderbilt Southeastern        1      -           Totals  -   -  -  NA NA 2.76
16 2013 Vanderbilt Southeastern        1      -  Opponent Totals  -   -  -  NA NA 6.19
```

Now, the function is dependent on the user knowing the `school_id` used by the NCAA website. Given that, I've included a `school_id_lu` function so that users can find the `school_id` they need.

Just pass a string to the function and it will return possible matches based on the school's name:

```r
> school_id_lu("Vand")
# A tibble: 4 × 6
      school   conference school_id  year division conference_id
       <chr>        <chr>     <dbl> <dbl>    <dbl>         <dbl>
1 Vanderbilt Southeastern       736  2013        1           911
2 Vanderbilt Southeastern       736  2014        1           911
3 Vanderbilt Southeastern       736  2015        1           911
4 Vanderbilt Southeastern       736  2016        1           911
```

