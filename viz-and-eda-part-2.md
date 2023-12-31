VIZ part 2
================
2023-10-09

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
knitr::opts_chunk$set(
  fig.width = 6,
  fig.asp = .6,
  out.width = "90%"
)
```

``` r
weather_df = 
  rnoaa::meteo_pull_monitors(
    c("USW00094728", "USW00022534", "USS0023B17S"),
    var = c("PRCP", "TMIN", "TMAX"), 
    date_min = "2021-01-01",
    date_max = "2022-12-31") |>
  mutate(
    name = recode(
      id, 
      USW00094728 = "CentralPark_NY", 
      USW00022534 = "Molokai_HI",
      USS0023B17S = "Waterhole_WA"),
    tmin = tmin / 10,
    tmax = tmax / 10) |>
  select(name, id, everything())
```

    ## using cached file: C:\Users\bradf\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USW00094728.dly

    ## date created (size, mb): 2023-10-09 11:57:58.716969 (0.344)

    ## file min/max dates: 2021-01-01 / 2023-10-31

    ## using cached file: C:\Users\bradf\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USW00022534.dly

    ## date created (size, mb): 2023-10-09 11:58:00.244156 (0.282)

    ## file min/max dates: 2021-01-01 / 2023-10-31

    ## using cached file: C:\Users\bradf\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USS0023B17S.dly

    ## date created (size, mb): 2023-10-09 11:58:01.00176 (0.122)

    ## file min/max dates: 2021-01-01 / 2023-10-31

\##same plot from last time

``` r
weather_df |>
  ggplot(aes(x = tmin, y = tmax, color = name)) +
  geom_point(alpha = .5) +
  labs(
    title = "Temparture Plot",
    x = "Min daily temp (Degrees c)",
    y = "M ax daily temp",
    color = "Location",
    caption = "max vs min daily temp in three locations; data from nrad"
  ) +
  scale_x_continuous(
  breaks = c(-15, 0, 15),
  labels = c("-15C", "0", "15")
  ) +
  scale_y_continuous(
    position = "right", 
    trans = "sqrt"
  )
```

    ## Warning in self$trans$transform(x): NaNs produced

    ## Warning: Transformation introduced infinite values in continuous y-axis

    ## Warning: Removed 142 rows containing missing values (`geom_point()`).

<img src="viz-and-eda-part-2_files/figure-gfm/unnamed-chunk-3-1.png" width="90%" />

``` r
weather_df = 
  rnoaa::meteo_pull_monitors(
    c("USW00094728", "USW00022534", "USS0023B17S"),
    var = c("PRCP", "TMIN", "TMAX"), 
    date_min = "2021-01-01",
    date_max = "2022-12-31") |>
  mutate(
    name = recode(
      id, 
      USW00094728 = "CentralPark_NY", 
      USW00022534 = "Molokai_HI",
      USS0023B17S = "Waterhole_WA"),
    tmin = tmin / 10,
    tmax = tmax / 10) |>
  select(name, id, everything())
```

    ## using cached file: C:\Users\bradf\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USW00094728.dly

    ## date created (size, mb): 2023-10-09 11:57:58.716969 (0.344)

    ## file min/max dates: 2021-01-01 / 2023-10-31

    ## using cached file: C:\Users\bradf\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USW00022534.dly

    ## date created (size, mb): 2023-10-09 11:58:00.244156 (0.282)

    ## file min/max dates: 2021-01-01 / 2023-10-31

    ## using cached file: C:\Users\bradf\AppData\Local/R/cache/R/rnoaa/noaa_ghcnd/USS0023B17S.dly

    ## date created (size, mb): 2023-10-09 11:58:01.00176 (0.122)

    ## file min/max dates: 2021-01-01 / 2023-10-31

\##same plot from last time

``` r
weather_df |>
  ggplot(aes(x = tmin, y = tmax, color = name)) +
  geom_point(alpha = .5) +
  labs(
    title = "Temparture Plot",
    x = "Min daily temp (Degrees c)",
    y = "M ax daily temp",
    color = "Location",
    caption = "max vs min daily temp in three locations; data from nrad" ) +
      viridis::scale_color_viridis(discrete = TRUE)
```

    ## Warning: Removed 17 rows containing missing values (`geom_point()`).

<img src="viz-and-eda-part-2_files/figure-gfm/unnamed-chunk-5-1.png" width="90%" />

``` r
weather_df |>
  ggplot(aes(x = tmin, y = tmax, color = name)) +
  geom_point(alpha = .5) +
  labs(
    title = "Temparture Plot",
    x = "Min daily temp (Degrees c)",
    y = "M ax daily temp",
    color = "Location",
    caption = "max vs min daily temp in three locations; data from nrad" ) +
      viridis::scale_color_viridis(discrete = TRUE) +
  theme_bw()
```

    ## Warning: Removed 17 rows containing missing values (`geom_point()`).

<img src="viz-and-eda-part-2_files/figure-gfm/unnamed-chunk-6-1.png" width="90%" />

``` r
  theme(legend.position = "bottom") 
```

    ## List of 1
    ##  $ legend.position: chr "bottom"
    ##  - attr(*, "class")= chr [1:2] "theme" "gg"
    ##  - attr(*, "complete")= logi FALSE
    ##  - attr(*, "validate")= logi TRUE

\##data argumen

``` r
weather_df |>
  ggplot(aes(x = date, y = tmax, color = name)) +
  geom_point() +
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 17 rows containing non-finite values (`stat_smooth()`).

    ## Warning: Removed 17 rows containing missing values (`geom_point()`).

<img src="viz-and-eda-part-2_files/figure-gfm/unnamed-chunk-7-1.png" width="90%" />

``` r
nyc_weather_df = 
  weather_df |> 
  filter(name == "CentralPark_NY")

hawaii_weather_df =
  weather_df |>
  filter(name == "Molokai_HI")

ggplot(nyc_weather_df, aes(x = date, y = tmax, color = name)) +
  geom_point() +
  geom_line(data = hawaii_weather_df)
```

<img src="viz-and-eda-part-2_files/figure-gfm/unnamed-chunk-7-2.png" width="90%" />

## ‘patchwork’

``` r
weather_df |>
  ggplot(aes(x = date, y = tmax, color = name)) + 
  geom_point() +
  facet_grid(. ~ name)
```

    ## Warning: Removed 17 rows containing missing values (`geom_point()`).

<img src="viz-and-eda-part-2_files/figure-gfm/unnamed-chunk-8-1.png" width="90%" />

``` r
ggp_temp_scatter = 
  weather_df |>
  ggplot(aes(x = tmin, y = tmax, color = names)) + 
  geom_point(alpha = .5)

ggp_prcp_density = 
 weather_df |>
  ggplot(aes(x = prcp, color = names)) +
  geom_density()
```
