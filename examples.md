---
title: rCharts nvd3 Tests
author: Ramnath Vaidyanathan and Timely Portfolio
framework: bootstrap
mode: selfcontained
highlighter: prettify
hitheme: twitter-bootstrap
---

<style>
iframe {
  height: 500px;
  width: 900px;
}
</style>





```r
## {title: Scatter Chart}
p1 <- nPlot(mpg ~ wt, group = "cyl", data = mtcars, type = "scatterChart")
p1$xAxis(axisLabel = "Weight")
p1$setLib(lib = "libraries/widgets/nvd3")
p1
```

<iframe src=assets/fig/p1.html seamless></iframe>



```r
## {title: MultiBar Chart}
hair_eye = as.data.frame(HairEyeColor)
p2 <- nPlot(Freq ~ Hair, group = 'Eye', data = subset(hair_eye, Sex == "Female"), type = 'multiBarChart')
p2$chart(color = c('brown', 'blue', '#594c26', 'green'))
p2$setLib(lib="libraries/widgets/nvd3")
p2
```

<iframe src=assets/fig/p2.html seamless></iframe>




```r
## {title: MultiBar Horizontal Chart}
p3 <- nPlot(~cyl, group = "gear", data = mtcars, type = "multiBarHorizontalChart")
p3$chart(showControls = F)
p3$setLib(lib = "libraries/widgets/nvd3")
p3
```

<iframe src=assets/fig/p3.html seamless></iframe>



```r
## {title: Pie Chart}
p4 <- nPlot(~cyl, data = mtcars, type = "pieChart")
p4$setLib(lib = "libraries/widgets/nvd3")
p4
```

<iframe src=assets/fig/p4.html seamless></iframe>



```r
## {title: Donut Chart}
p5 <- nPlot(~cyl, data = mtcars, type = "pieChart")
p5$chart(donut = TRUE)
p5$setLib(lib = "libraries/widgets/nvd3")
p5
```

<iframe src=assets/fig/p5.html seamless></iframe>



```r
## {title: Line Chart}
data(economics, package = "ggplot2")
p6 <- nPlot(uempmed ~ date, data = economics, type = "lineChart")
p6$setLib(lib = "libraries/widgets/nvd3")
p6
```

<iframe src=assets/fig/p6.html seamless></iframe>



```r
## {title: Line with Focus Chart }
ecm <- reshape2::melt(economics[, c("date", "uempmed", "psavert")], id = "date")
p7 <- nPlot(value ~ date, group = "variable", data = ecm, type = "lineWithFocusChart")
# test format dates on the xAxis also good test of javascript functions as
# parameters dates from R to JSON will come over as number of days since
# 1970-01-01 so convert to milliseconds 86400000 in a day and then format
# with d3 on lineWithFocusChart type xAxis will also set x2Axis unless it
# is specified
p7$xAxis(tickFormat = "#!function(d) {return d3.time.format('%b %Y')(new Date( d * 86400000 ));}!#")
# test xAxis also sets x2Axis
p7$setLib(lib = "libraries/widgets/nvd3")
p7
```

<iframe src=assets/fig/p7.html seamless></iframe>




```r
# now test setting x2Axis to something different test format dates on the
# x2Axis test to show %Y format which is different than xAxis
p7$x2Axis(tickFormat = "#!function(d) {return d3.time.format('%Y')(new Date( d * 86400000 ));}!#")
p7
```

<iframe src=assets/fig/p7a.html seamless></iframe>

```r
# test set xAxis again to make sure it does not override set x2Axis
p7$xAxis(NULL, replace = T)
p7
```

<iframe src=assets/fig/p7a.html seamless></iframe>



```r
## {title: Stacked Area Chart}
dat <- data.frame(t = rep(0:23, each = 4), var = rep(LETTERS[1:4], 4), val = round(runif(4 * 
    24, 0, 50)))
p8 <- nPlot(val ~ t, group = "var", data = dat, type = "stackedAreaChart", id = "chart")
p8$setLib(lib = "libraries/widgets/nvd3")
p8
```

<iframe src=assets/fig/p8.html seamless></iframe>



```r
## {title: InteractiveGuidline(Multi-Tooltips) on Line}
p9 <- nPlot(value ~ date, group = "variable", data = ecm, type = "lineChart")
p9$xAxis(tickFormat = "#!function(d) {return d3.time.format('%b %Y')(new Date( d * 86400000 ));}!#")
# try new interactive guidelines feature
p9$chart(useInteractiveGuideline = TRUE)
p9$setLib(lib = "libraries/widgets/nvd3")
p9
```

<iframe src=assets/fig/p9.html seamless></iframe>



```r
## {title: InteractiveGuidline(Multi-Tooltips) on Stack}
p10 <- p8
p10$chart(useInteractiveGuideline = TRUE)
p10$setLib(lib = "libraries/widgets/nvd3")
p10
```

<iframe src=assets/fig/p10.html seamless></iframe>



```r
## {title: showDistX and showDistY}
p11 <- p1
p11$chart(showDistX = TRUE, showDistY = TRUE)
p11$setLib(lib = "libraries/widgets/nvd3")
p11
```

<iframe src=assets/fig/p11.html seamless></iframe>



```r
## {title: multiChart}
p12 <- nPlot(value ~ date, group = "variable", data = ecm, type = "multiChart")
p12$params$multi = list(uempmed = list(type = "area", yAxis = 1), psavert = list(type = "line", 
    yAxis = 2))
p12$setLib(lib = "libraries/widgets/nvd3")
p12$templates$script = "libraries/widgets/nvd3/layouts/multiChart.html"
p12
```

<iframe src=assets/fig/p12.html seamless></iframe>



```r
## {title: Facets}
p13 <- nPlot(mpg ~ wt, data = mtcars, group = "gear", type = "scatterChart")
p13$params$facet = "cyl"
p13$setLib(lib = "libraries/widgets/nvd3")
p13$templates$script = "libraries/widgets/nvd3/layouts/nvd3FacetPlot.html"
p13
```

<iframe src=assets/fig/p13.html seamless></iframe>



```r
hair_eye = as.data.frame(HairEyeColor)
p14 <- nPlot(Freq ~ Hair, group = "Eye", data = hair_eye, type = "multiBarChart")
p14$params$facet = "Sex"
p14$setLib(lib = "libraries/widgets/nvd3")
p14$templates$script = "libraries/widgets/nvd3/layouts/nvd3FacetPlot.html"
# p14$chart(color = c('brown', 'blue', '#594c26', 'green'))
p14
```

<iframe src=assets/fig/p14.html seamless></iframe>

