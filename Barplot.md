Barplot
================

A Simple Barplot
----------------

To make a barplot like the example below:

![](barplot_example.png)

In essence, we need to change the following graphical attributes:

-   Thickness of axes

-   Ticks of y-axis

-   Font type

-   Bold font

-   Color of filled bars

Code
----

I will use the `storms` dataset to illustrate how to make a plot like the example above. The example plot shows the number of storms for each `status`.

Take a look at the data:

``` r
require(tidyverse)

glimpse(storms)
```

    ## Observations: 10,010
    ## Variables: 13
    ## $ name        <chr> "Amy", "Amy", "Amy", "Amy", "Amy", "Amy", "Amy", "Amy", "…
    ## $ year        <dbl> 1975, 1975, 1975, 1975, 1975, 1975, 1975, 1975, 1975, 197…
    ## $ month       <dbl> 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 7, 7, 7, …
    ## $ day         <int> 27, 27, 27, 27, 28, 28, 28, 28, 29, 29, 29, 29, 30, 30, 3…
    ## $ hour        <dbl> 0, 6, 12, 18, 0, 6, 12, 18, 0, 6, 12, 18, 0, 6, 12, 18, 0…
    ## $ lat         <dbl> 27.5, 28.5, 29.5, 30.5, 31.5, 32.4, 33.3, 34.0, 34.4, 34.…
    ## $ long        <dbl> -79.0, -79.0, -79.0, -79.0, -78.8, -78.7, -78.0, -77.0, -…
    ## $ status      <chr> "tropical depression", "tropical depression", "tropical d…
    ## $ category    <ord> -1, -1, -1, -1, -1, -1, -1, -1, 0, 0, 0, 0, 0, 0, 0, 0, 0…
    ## $ wind        <int> 25, 25, 25, 25, 25, 25, 25, 30, 35, 40, 45, 50, 50, 55, 6…
    ## $ pressure    <int> 1013, 1013, 1013, 1013, 1012, 1012, 1011, 1006, 1004, 100…
    ## $ ts_diameter <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    ## $ hu_diameter <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…

The standard `ggplot2` way to create barplot is

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status))
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-1-1.png)

The pretty version of the standard `barplot`.
---------------------------------------------

The first step is to install the package `extrafont`. Right after installation, import fonts to your machine. You only need to do this step once. Notice that the fonts imported are machine-dependent.

``` r
if (!( "extrafont" %in% .packages())) {
  
  require(extrafont)
  
  font_import(prompt = F)
  loadfonts(quiet = T)
}
```

Use different color to fill the bar and change the outline to thick black.

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2)
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-3-1.png)

Choose a differnt color palette. The concept of palette can be found here: <https://www.r-bloggers.com/colorspace-new-tools-for-colors-and-palettes/>

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2) +
  scale_fill_brewer(palette = 'Set2')
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-4-1.png)

Use another palette

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2) +
  scale_fill_brewer(palette = 'Cold')
```

    ## Warning in pal_name(palette, type): Unknown palette Cold

![](Barplot_files/figure-markdown_github/unnamed-chunk-5-1.png)

Here is a map of palettes from <https://i2.wp.com/eeecon.uibk.ac.at/~zeileis/assets/posts/2019-01-14-colorspace/hcl-palettes-1.png?ssl=1>

![](hcl-palettes-1.png)

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black') +
  labs(title = "New Font") +
  theme(
    text = element_text(family = 'Courier', size = 24)
  )
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-6-1.png)
