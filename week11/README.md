<div class="header">
<h1 class="ml7">
  <span class="text-wrapper">
    <span class="letters"><p id ="usc p">Data&nbsp;&nbsp;Journalism&nbsp;&nbsp;&nbsp;USC&nbsp;&nbsp;2019</p></span>
  </span>
</h1>
</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/animejs/2.0.2/anime.min.js"></script>

<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

<style>
.header{
      background-image: linear-gradient(to right, #e66465, #9198e5);
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


# Week 11
This week, we're going to become wizards of ggplot2, the best way to create graphics in R.

---

### Hands-on

Adapted from a great tutorial by [Rebecca Barter](http://www.rebeccabarter.com/blog/2017-11-17-ggplot2_tutorial/).

**The layered grammar of graphics**

ggplot2 is based around three ideas. They make more sense in practice, but it's helpful to outline them up front:

* data: a data frame containing the variables that you want to visualize
* geoms: geometric objects (circles, lines, text) that you will actually see
* aesthetics: the mapping from the data to the geographic objects (e.g. by describing position, size, colour, etc)

**1.Let's download our data and start making a chart**

We're using the the gapminder dataset again this week.

First, fire up R Studio. Then, we'll load everything we need and remind ourselves what this data looks like.

```
library(tidyverse)
library(gapminder)
head(gapminder)
```

So ggplot. We tell it what data (a data frame) we are interested in and how each of the variables in our dataset will be used (e.g. as an x or y coordinate, as a coloring variable or a size variable, etc).

The output of this function is a grid with gdpPercap as the x-axis and lifeExp as the y-axis. However, we have not yet told ggplot what type of geometric object the data will be mapped to, so no data has been displayed.

Essentially, we've created the grid for the chart. But not the chart yet.

```
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp))
```

Next, we will add a “geom” layer to our ggplot object. This one will be points.

```
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  # add a points layer on top
  geom_point()
```

Now we're talking.

**2. Transparency, color, size**

What we've done is map each country (row) in the data to a point in the space defined by the GDP and life expectancy value. The end result is a fascinating blob of points. Fortunately, there are many things that we can do to make this blob of points look better.

One possibility? Change the transparency of the points by setting the transparency.


Let's change the 'alpha' argument.

```
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.5)
```

What other tweaks could we make? How about changing the color of the points to be blue instead of black, and making the points smaller.

```
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp)) +
  geom_point(alpha = 0.5, col = "cornflowerblue", size = 0.5)
```
As you can see, ggplot will change many things at the same time.

But what if we want different colors for the points, based on the continent of each country?

We can make use of the aes() function. Let check out what those continents are first.

```
unique(gapminder$continent)
```

Got it. Ok, so we can plug that continent vector into ggplot, and ask it to color the points differently, depending on what continent the country represents.

```
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp, color = continent)) +
  geom_point(alpha = 0.5, size = 0.5)
```
Nice! There's other things we can change, too, like the size of the points. Say we want to make those correspond to the population of the country.

```
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp, color = continent, size = pop)) +
  geom_point(alpha = 0.5)
```

**3. Other chart types**

So far, we have only seen scatterplots (point geoms). But there are many other geoms we *could* add, including:

* lines
* histograms
* boxplots and violin plots
* barplots
* smoothed curves

Let's try some out

What's different about this one?

```
ggplot(gapminder, aes(x = year, y = lifeExp, group = country, color = continent)) +
  geom_line(alpha = 0.5)
```

How might this one be different?

```
ggplot(gapminder, aes(x = continent, y = lifeExp, fill = continent)) +
  geom_boxplot()
```

Let's bust out a historgram.
```
ggplot(gapminder, aes(x = lifeExp)) + 
  geom_histogram(binwidth = 3)
```

And finally let's try to find how a mathematical model might interpret our data. Don't publish these, but they can be helpful for internal use.

```
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp, size = pop)) +
  geom_point(aes(color = continent), alpha = 0.5) +
  geom_smooth(se = FALSE, method = "loess", color = "grey30")
```

**4.Let's make something publishable**

We want a focused chart to show readers. So let’s filter to a single year.

```
gapminder_2007 <- gapminder %>% filter(year == 2007)
ggplot(gapminder_2007, aes(x = gdpPercap, y = lifeExp, color = continent, size = pop)) +
  geom_point(alpha = 0.5)
```

Let's get fancy and use a logorithmic scale. Who kjnows what that is?

Here's how we do that.

```
ggplot(gapminder_2007, aes(x = gdpPercap, y = lifeExp, color = continent, size = pop)) +
  geom_point(alpha = 0.5) +
  scale_x_log10()
```

Now it's time to add a title and change the name of the y-axis and legends using the labs function.

```
ggplot(gapminder_2007, aes(x = gdpPercap, y = lifeExp, color = continent, size = pop)) +
  # add scatter points
  geom_point(alpha = 0.5) +
  # log-scale the x-axis
  scale_x_log10() +
  # change labels
  labs(title = "GDP versus life expectancy in 2007",
       x = "GDP per capita (log scale)",
       y = "Life expectancy",
       size = "Popoulation",
       color = "Continent")
```


**5. Themes**

Mabye you, like me, kinda hate this gray background.

Well, you can change it with the ggthemes package.

```
install.packages("ggthemes")
library(ggthemes)
```

Let's take a look at some of [the available themes](https://yutannihilation.github.io/allYourFigureAreBelongToUs/ggthemes/) and try them out on that last chart.

Finally, let's go crazy and see if we can figure out everything this is doing.

```
ggplot(gapminder_2007, aes(x = gdpPercap, y = lifeExp, color = continent, size = pop)) +
  # add scatter points
  geom_point(alpha = 0.5) +
  # clean the axes names and breaks
  scale_x_log10(breaks = c(1000, 10000),
                limits = c(200, 120000)) +
  # change labels
  labs(title = "GDP versus life expectancy in 2007",
       x = "GDP per capita (log scale)",
       y = "Life expectancy",
       size = "Popoulation (millions)",
       color = "Continent") +
  # change the size scale
  scale_size(range = c(0.1, 10),
             breaks = 1000000 * c(250, 500, 750, 1000, 1250),
             labels = c("250", "500", "750", "1000", "1250")) +
  # add a nicer theme
  theme_classic(base_family = "Helvetica")
```

And let's talk about how to save a chart you create in R.

### EXTRA BONUS HAND-ON CODING

Here we're gonna scrape the web with the `rvest` package.

Start by installing and loading it.

```
install.packages("rvest")
library(rvest)
```

Next, we're going to tell it the URL of the page we want to scrape.

```
url <- "https://en.wikipedia.org/wiki/List_of_Governors_of_California_by_age"
```

Next, we're gonna ... just go ahead and scrape the table. There's a lot going on here, so let's examine closely.

```
govs <- url %>%
    read_html() %>%
    html_nodes("table") %>%
    html_table(header = NA) %>%
    as.data.frame()
```

Let's take a look. There are some issues, so let's fix them before getting to the fun stuff. Let's delete these columns we don't need, first off.

```
govs$Age.at.inauguration <- NULL
govs$Age.at.endof.term <- NULL
govs$Length.ofretirement <- NULL
govs$Lifespan <- NULL
```
Let's rename some vectors with ugly names.

```
colnames(govs)[1] <- c("rank_by_age")
colnames(govs)[3] <- c("num_in_office")
```

Let's delete that pesky last row. See what we're doing here?

```
govs <- head(govs,40)
```

There are also some footnotes in the DOB column. Good for Wikipedia users, not good for us. This is a `regular expression`. Regex could be it's own class, but here we're just removing everything in a string after the `[` character.

```
govs$Date.of.birth <- gsub("\\[.*","",govs$Date.of.birth)
```

And finally, let's make the number in office an actual number. We'll need this later.

```
govs$num_in_office <- as.numeric(govs$num_in_office)
```

Whew. Data should be much cleaner now. Except ... our dates don't look like dates at all.

How can we change that? Let's do it with the `lubridate` package.

```
install.packages("lubridate")
library(lubridate)
```

Let's see what this function does

```
mdy(govs$Date.of.birth)
```

Perfect. This stuff used to be a total pain, but lubridate has made it so, so painless.

Now we can fix all our dates.

```
govs$Date.of.birth <- mdy(govs$Date.of.birth)
govs$Date.of.inauguration <- mdy(govs$Date.of.inauguration)
govs$End.ofterm <- mdy(govs$End.ofterm)
govs$Date.of.death <- mdy(govs$Date.of.death)

```

We can also do math with dates. Check it out.

```
govs$Date.of.birth - govs$Date.of.inauguration
```

Awesome. Let's bring this class full circle and chart the data. We'll do that with the ``ggalt`` package.

```
install.packages("ggalt")
library(ggalt)
```

Now, we can actually plot out their terms in office.

```
govs %>% ggplot(aes(y = reorder(Governor, num_in_office), x = Date.of.inauguration, xend = End.ofterm)) + geom_dumbbell(color = "steelblue")
```

We can also plot out their lifespans. Some of them are still among the living, so let's code their 'death' as today's date. Take a look at how we do that.

```
govs$Date.of.death <- case_when(is.na(govs$Date.of.death) == TRUE ~ Sys.Date(), TRUE ~ govs$Date.of.death)

govs %>% ggplot(aes(y = reorder(Governor, num_in_office), x = Date.of.birth, xend = Date.of.death)) + geom_dumbbell(color = "steelblue")
```

---

### Homework

* R Data Viz Assignment. Using data from your Final Project create two charts using ggplot.
	* If you need inspiration, use code from our walkthrough today. Or, take a look at some of these [simple cool R chart examples](https://www.r-graph-gallery.com/).
	* Due on **Sunday by 5 PM**.
* Story memo: 50-100 words about Final Project progress over last week