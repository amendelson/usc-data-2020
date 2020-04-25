<div class="header">
<h1 class="ml7">
  <span class="text-wrapper">
    <span class="letters"><p id ="usc p">Data&nbsp;&nbsp;Journalism&nbsp;&nbsp;&nbsp;USC&nbsp;&nbsp;2020</p></span>
  </span>
</h1>
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/animejs/2.0.2/anime.min.js"></script>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

<style>
.header{
      background-image: linear-gradient(to right, #ff5f6d, #ffc371);
}

.ml7 {
  position: relative;
  font-weight: 1200;


}
.ml7 .text-wrapper {
  position: relative;
  display: inline-block;
  padding-top: 0.2em;
  padding-right: 0.05em;
  padding-bottom: 0.1em;
  overflow: hidden;
  padding-left: 14px;

}
.ml7 .letter {
  transform-origin: 0 100%;
  display: inline-block;
  line-height: 1.3em;
  font-size: 3.6em;
  color: #FFFFFF
}


</style>


<script>
// Wrap every letter in a span
$('.ml7 .letters').each(function(){
  $(this).html($(this).text().replace(/([^\x00-\x80]|\w)/g, "<span class='letter'>$&</span>"));
});

anime.timeline({loop: true})
  .add({
    targets: '.ml7 .letter',
    translateY: ["1.1em", 0],
    translateX: ["0.55em", 0],
    translateZ: 0,
    rotateZ: [180, 0],
    duration: 1050,
    easing: "easeOutExpo",
    delay: function(el, i) {
      return 50 * i;
    }
  }).add({
    targets: '.ml7',
    opacity: 0,
    duration: 1000,
    easing: "easeOutExpo",
    delay: 1000
  });
</script>


# Week 15

### Hands-on pt. 1 — correlation

[Inspiration](https://xkcd.com/552/) for today:

<img src = "https://imgs.xkcd.com/comics/correlation.png">

Let's begin by installing and loading some packages.

```
# install new
install.packages("PerformanceAnalytics")
install.packages("psych")

# load them
library(PerformanceAnalytics)
library(psych)
library(tidyverse)

```

Let's load our data ... which I think is based on an old TV show.

```
Data <- read_csv("https://amendelson.github.io/usc-data-2020/week15/Data.csv")
```

OK, one easy way to spot correlation is using charts. Let's try this.

```
pairs(data=Data,
    ~ Grade + Weight + Calories + Sodium + Score)
```

The corr.test function in the psych package can be used in a similar way, with the output being a table of correlation coefficients and a table of p-values.

A p-value is a measure of correlation.

Let's get a dataframe of just numeric vectors.

```
Data_num <- Data %>% select(-Instructor)
```

Now let's get the p-values.

```
corr.test(Data_num,
          use    = "pairwise",
          method = "pearson",
          adjust = "none")
```

The thing to keep in mind: the closer to 1 or -1, the more significant the correlation.

Another way to explore the correlation is through the PerformanceAnalytics package.

```
chart.Correlation(Data_num,
                  method="pearson",
                  histogram=TRUE,
                  pch=16)
```

And ggplot can also give us a good indication of correlation, by providing the 'line of best fit' with a confidence interval.

```
ggplot(Data,
       aes(x = Calories,
           y = Sodium)) +
    geom_point() +
    geom_smooth(method  = "lm",
                formula = y ~ poly(x, 2, raw=TRUE), se = TRUE)
```

*With debt to [this tutorial](https://rcompanion.org/handbook/I_10.html)*

### Part 2 — animation

Let's check out something I've been meaning to explore: [gganimate](https://www.r-graph-gallery.com/271-ggplot2-animated-gif-chart-with-gganimate.html).

### Part 3 — choose your own adventure

The htmlwidgets are a great way to get your data in front of your readers:

* [htmlwidgets collection](https://www.htmlwidgets.org/index.html)

With any extra time, we can also check out these neat packages:

* [rayshader](https://www.rayshader.com/)
* [mapdeck](https://symbolixau.github.io/mapdeck/articles/layers.html)
* [datatables](https://rstudio.github.io/DT/)

