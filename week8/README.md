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


# Week 8


---

### Quick hands-on

**1. Bring in census data, tidily and easily**

There's a great R package for importing census data. Let's install and load it.

```
library(leaflet)
library(tidyverse)
```

```
install.packages("tidycensus")
library(tidycensus)
```

To get the data from the Census' API, you need to provide an API Key. Find yours and use it.

```
census_api_key("TK", overwrite = FALSE, install = FALSE)
```

Once you've done that, you can quickly grab data. If you want to know the median rent by state in 1990 ... now you can.

```
m90 <- get_decennial(geography = "state", variables = "H043A001", year = 1990)
```

It can also easily be plotted.

```
m90 %>%
  ggplot(aes(x = value, y = reorder(NAME, value))) +
  geom_point()
```

We can also grab data from the more-frequently-updated American Community Survey. It's like a rolling Census that's being conducted all the time.

Let's look at public transit.

```
transpo <- get_acs(geography = "state", variables = "B08006_008", geometry = FALSE, survey = "acs5", year = 2017)
```

```
head(transpo)
```

Interesting. But what we really want is the **rate** of transit riders. Not the raw number. So let's get that, starting with the total number of folks who commute to work.

```
transpo_total <- get_acs(geography = "state", variables = "B08006_001", geometry = FALSE, survey = "acs5", year = 2017)
head(transpo_total)

```

Alright, now we need to get these ... together in the same data frame! That's where the `join` comes in. We did some of these in QGIS. What could we use in these two datasets to link them up?

**2. A detour into joins**

All you need to join is a common column. Here's how it works in tidyverse.

```
transpo <- transpo %>% left_join(transpo_total, by = "NAME")
```

Now we can get the rate.

```
transpo$rate <- transpo$estimate.x / transpo$estimate.y * 100
head(transpo)
```

**3. Map out (after another join)**

We need to join that transportation data to our shapefile. Unfortunately, the syntax there is a little different. Fortunately, it does work.

For this, we'll need to bring back the states shapefile we used last week,

```
library(rgdal)
states <- readOGR("path/to/yourfile/",
  layer = "tl_2019_us_state", GDAL1_integer64_policy = TRUE)
```

Then we can do a join.

```
states_with_rate <- sp::merge(states, transpo, by = "NAME")
```

Let's try this out.

```
qpal <- colorQuantile("PiYG", states_with_rate$rate, 9)


states_with_rate %>% leaflet() %>% addTiles() %>%
  addPolygons(weight = 1, smoothFactor = 0.5, opacity = 1.0, fillOpacity = 0.5,
    color = ~qpal(rate),
    highlightOptions = highlightOptions(color = "white", weight = 2,
      bringToFront = TRUE))
```

Alright. What does each line do? Let's play around with it and see what changes?

If we have extra time, we'll work on adding [popup text](https://rstudio.github.io/leaflet/popups.html) and [a legend](https://rstudio.github.io/leaflet/legends.html).




---

### Homework

* Github: Create an account if you don't already have one. If you do, make sure you know the password.
* HW: Finish coding if we didn't in class.
* Final Project: Your data analysis should almost done. You should be reporting and writing as you go.
* Story memo: 50-100 words about Final Project progress over last week

