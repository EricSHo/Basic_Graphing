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

Remove grid line and grey background.

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2) +
  scale_fill_brewer(palette = 'Set2') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank()
  )
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-6-1.png)

Change the thickness of x and y axes. Thickness of ticks is matched as well.

For customizing tick marks and labels, read this <http://www.sthda.com/english/wiki/ggplot2-axis-ticks-a-guide-to-customize-tick-marks-and-labels>

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Pretty Barplot', x = 'Status', y = 'Count') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 10)
  ) +
  scale_y_continuous(breaks=seq(0, 4500, 500)) # _discrete means nominal, _continuous means numeric, 
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-7-1.png)

Hide legend variable.

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Pretty Barplot', x = 'Status', y = 'Count') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 10),
    legend.title = element_blank()
  ) +
  scale_y_continuous(breaks=seq(0, 4500, 500)) # _discrete means nominal, _continuous means numeric, 
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-8-1.png)

As the labels beneath the bars have already told us the status, the legend is unnecessary. To remove the legend, set `legend.position = "None"`.

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Pretty Barplot', x = 'Status', y = 'Count') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 10),
    legend.position = "None"
  ) +
  scale_y_continuous(breaks=seq(0, 4500, 500)) # _discrete means nominal, _continuous means numeric, 
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-9-1.png)

Change the width of bars using `width=`. It ranges from 0 to 1, default is 1.

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2, width = 0.5) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Pretty Barplot', x = 'Status', y = 'Count') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 10),
    legend.position = "None"
  ) +
  scale_y_continuous(breaks=seq(0, 4500, 500)) # _discrete means nominal, _continuous means numeric, 
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-10-1.png)

Make a horizontal barplot by `coord_flip()`.

``` r
ggplot(data = storms) +
  geom_bar(mapping = aes(x = status, fill = status), color = 'black', size = 2, width = 0.5) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Pretty Barplot', x = 'Status', y = 'Count') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 10),
    legend.position = "None"
  ) +
  scale_y_continuous(breaks=seq(0, 4500, 500)) +
  coord_flip()
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-11-1.png)

Barplot with error bars
-----------------------

Let's use the `iris` dataset for illustration.

``` r
glimpse(iris)
```

    ## Observations: 150
    ## Variables: 5
    ## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9, 5.4, 4…
    ## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1, 3.7, 3…
    ## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5, 1.5, 1…
    ## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1, 0.2, 0…
    ## $ Species      <fct> setosa, setosa, setosa, setosa, setosa, setosa, setosa, …

``` r
Sepal.Length.summ <- iris %>%
  select(Sepal.Length, Species) %>%
  group_by(Species) %>%
  summarise(se = sd(Sepal.Length), u = mean(Sepal.Length))
glimpse(Sepal.Length.summ)
```

    ## Observations: 3
    ## Variables: 3
    ## $ Species <fct> setosa, versicolor, virginica
    ## $ se      <dbl> 0.3524897, 0.5161711, 0.6358796
    ## $ u       <dbl> 5.006, 5.936, 6.588

A very basic barplot with error bar. Note that the statistical transformation is changed to identity (`stat = 'identity'`), i.e. take the face values.

``` r
ggplot(data = Sepal.Length.summ) +
  geom_bar(mapping = aes(Species, y = u), stat = 'identity') +
  geom_errorbar(mapping = aes(x = Species, ymin = u-se, ymax = u+se))
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-14-1.png)

Make a pretty one.

``` r
ggplot(data = Sepal.Length.summ) +
  geom_bar(mapping = aes(x = Species, y = u, fill = Species), stat = 'identity', color = 'black', size = 2, width = 0.5) +
  geom_errorbar(mapping = aes(x = Species, ymin = u-se, ymax = u+se), width = 0.3, size=1) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Barplot with Error Bar', x = 'Species', y = 'Sepal Length (cm)') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    # axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 10),
    legend.position = "None"
  )
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-15-1.png)

Multipanel plot
---------------

Data preparation.

``` r
tmp.summ <- iris %>%
  group_by(Species) %>%
  summarise(sl.se = sd(Sepal.Length), sl.u = mean(Sepal.Length),
            sw.se = sd(Sepal.Width), sw.u = mean(Sepal.Width),
            pl.se = sd(Petal.Length), pl.u = mean(Petal.Length),
            pw.se = sd(Petal.Width), pw.u = mean(Petal.Width)
  )
sw.summ <- tmp.summ %>%
  select(Species, sw.se, sw.u) %>%
  mutate(Part = 'Sepal.Width') %>%
  rename(se = sw.se, u = sw.u)

sl.summ <- tmp.summ %>%
  select(Species, sl.se, sl.u) %>%
  mutate(Part = 'Sepal.Length') %>%
  rename(se = sl.se, u = sl.u)

pw.summ <- tmp.summ %>%
  select(Species, pw.se, pw.u) %>%
  mutate(Part = 'Petal.Width') %>%
  rename(se = pw.se, u = pw.u)

pl.summ <- tmp.summ %>%
  select(Species, pl.se, pl.u) %>%
  mutate(Part = 'Petal.Length') %>%
  rename(se = pl.se, u = pl.u)

all.summ <- bind_rows(sw.summ, sl.summ)
all.summ <- bind_rows(all.summ, pw.summ)
all.summ <- bind_rows(all.summ, pl.summ)


glimpse(all.summ)
```

    ## Observations: 12
    ## Variables: 4
    ## $ Species <fct> setosa, versicolor, virginica, setosa, versicolor, virginica,…
    ## $ se      <dbl> 0.3790644, 0.3137983, 0.3224966, 0.3524897, 0.5161711, 0.6358…
    ## $ u       <dbl> 3.428, 2.770, 2.974, 5.006, 5.936, 6.588, 0.246, 1.326, 2.026…
    ## $ Part    <chr> "Sepal.Width", "Sepal.Width", "Sepal.Width", "Sepal.Length", …

Just plot the `Sepal.Width`.

``` r
ggplot(data = sw.summ) +
  geom_bar(mapping = aes(x = Species, y = u, fill = Species), stat = 'identity', color = 'black', size = 2, width = 0.5) +
  geom_errorbar(mapping = aes(x = Species, ymin = u-se, ymax = u+se), width = 0.3, size=1) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Barplot with Error Bar', x = 'Species', y = 'Sepal Width (cm)') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    # axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 10),
    legend.position = "None"
  )
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-17-1.png)

Combination a boxplot
---------------------

``` r
ggplot(data = all.summ) +
  geom_bar(mapping = aes(x = Species, y = u, fill = Species), stat = 'identity', color = 'black', size = 2, width = 0.5) +
  geom_errorbar(mapping = aes(x = Species, ymin = u-se, ymax = u+se), width = 0.3, size=1) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Barplot with Error Bar', x = 'Species', y = 'Length or Width (cm)') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 8),
    legend.position = "None"
  ) +
  facet_grid( ~ Part)
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-18-1.png)

Make the facet into 2x2 using `facet_wrap(...)` instead of `facet_grid(...)`.

``` r
ggplot(data = all.summ) +
  geom_bar(mapping = aes(x = Species, y = u, fill = Species), stat = 'identity', color = 'black', size = 2, width = 0.5) +
  geom_errorbar(mapping = aes(x = Species, ymin = u-se, ymax = u+se), width = 0.3, size=1) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Barplot with Error Bar', x = 'Species', y = 'Length or Width (cm)') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 8),
    legend.position = "None"
  ) +
  facet_wrap( ~ Part, ncol = 2)
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-19-1.png)

Line graph with error bar. Basically, it is a combination of points with a line connecting a pair of points. Notice that `geom_line(aes(group=1))`. The `aes(group=1)` is to allow the line to span three species.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

``` r
ggplot(data = all.summ, mapping = aes(x = Species, y = u)) +
  geom_line(aes(group=1)) +
  geom_point(size = 2) +
  geom_errorbar(mapping = aes(ymin = u-se, ymax = u+se), width = 0.1, size=1) +
  scale_fill_brewer(palette = 'Set2') +
  labs(title = 'Line plot with Error Bar', x = 'Species', y = 'Length or Width (cm)') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', angle = 45, vjust = 0.5, size = 8),
    legend.position = "None"
  ) +
  facet_wrap( ~ Part, ncol = 2)
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-20-1.png)

Boxplot with individual data points (jitter plot)
-------------------------------------------------

![](Boxplot_Violin_example.png)

Just for `Sepal.Length`. Points in `jitter(...)` are enlarged (`size=4`). The width of the box is 50% of default.

``` r
ggplot(data = select(iris, Species, Sepal.Length), mapping = aes(x = Species, y = Sepal.Length, color = Species)) +
  scale_fill_brewer(palette = 'Set2') +
  geom_jitter(size=4) +
  geom_boxplot(alpha=0.5, width=0.5, color='black') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', vjust = 0.5, size = 8),
    legend.position = "None" 
  )
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-21-1.png)

Jitter plot with a median line

``` r
ggplot(data = select(iris, Species, Sepal.Length), mapping = aes(x = Species, y = Sepal.Length)) +
  geom_jitter() +
  stat_summary(fun.y = median, fun.ymin = median, fun.ymax = median, geom = 'crossbar', width=0.5)
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-22-1.png)

``` r
ggplot(data = select(iris, Species, Sepal.Length), mapping = aes(x = Species, y = Sepal.Length, color = Species)) +
  scale_fill_brewer(palette = 'Set2') +
  geom_jitter(size=4) +
  stat_summary(fun.y = median, fun.ymin = median, fun.ymax = median, geom = 'crossbar', width=0.5, color = 'Black') +
  theme(
    panel.grid = element_blank(),
    panel.background = element_blank(),
    text = element_text(family = 'Arial', size = 18),
    plot.title = element_text(hjust = 0.5), # [0, 1],
    axis.line = element_line(size = 1, linetype = 'solid'),
    axis.ticks = element_line(size = 1),
    axis.text.x = element_text(face = 'bold', vjust = 0.5, size = 8),
    legend.position = "None" 
  )
```

![](Barplot_files/figure-markdown_github/unnamed-chunk-23-1.png)
