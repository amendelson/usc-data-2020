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


# Week 12
This week, we're talking about the importance of **tidy** data ... and how to make your data tidy.

---

### Lecture

[Slides](https://docs.google.com/presentation/d/1SlCA6neTiBd6G7ZVfJohozj0AYrhkDS_Nz_ttENfvNM/edit#slide=id.p)

---

### Hands-on — Part 1

Let's talk about functions and for loops by building off our scraping work last week.

I've packaged everything we did into a single R script, [available here](/https://github.com/amendelson/usc-course-spring-2019/blob/gh-pages/week12/govs_scraping.R). Download the file.

Let's see how you can run R from the command line. Open up your terminal or powershell. Type in `R` to launch R.

It should look a little different. If it does, type a version of this in, making an adjustment for the location of the R script you just downloaded.

```
source("~/data-path-to-your-file/govs_scraping.r", echo = TRUE)
```

Cool, right?

Now let's fire up R Studio and try the exact same line of code.

```
source("~/data-path-to-your-file/govs_scraping.r", echo = TRUE)
```

Should've done the same thing. And now you've got the dataframe loaded in your environment.

OK, now we want to answer the question: **during what year were the most governors alive at the same time?**

How would we do that, just conceptually?

...

Let's start our journey by just testing out one year, to see which governors were alive then.

```
govs %>% filter(Date.of.birth < mdy("01-01-1900") & Date.of.death > mdy("01-01-1900"))
```

Great. If we just wanted a count, not all the columns, we could do this.

```
govs %>% filter(Date.of.birth < mdy("01-01-1900") & Date.of.death > mdy("01-01-1900")) %>% nrow()
```

Ok, here is what we're going to do. But let's unpack it for a given `i` before we run the whole function. There is a lot going on here.

```
alive_stats <- data.frame()

for (i in 1806:2018) {

	begin <- mdy(paste("01-01-",i,sep=""))
	end <- mdy(paste("01-01-",(i+1),sep=""))
	
	count_alive <- govs %>% filter(Date.of.birth < begin & Date.of.death > end) %>% nrow() %>% as.numeric()
	
	alive_stats <- rbind(count_alive, alive_stats)
	
	alive_stats$yr[1] <- i

}
```

Let's rename that first column.

```
colnames(alive_stats)[1] <- c("count")
```

And of course, we can plot this out.

```
alive_stats %>% ggplot(aes(x=yr, y=count)) + geom_bar(stat="identity")
```


### Hands-on — Part 2


We're going to be learning about tidy data from the creator of the tidyverse, Hadley Wickham. This tutorial is adapted from his [Data Science in the Tidyverse](https://github.com/hadley/data-science-in-tidyverse/tree/master/slides) workshop.

**1. So what's tidy data?**

<img src ="imgs/1.png" width = "600">

It's easy to work with. For example, you can quickly calculate a per capita rate if you already have the population data right there.

Here are the main functions we'll be working with.

<img src ="imgs/2.png" width = "600">

**2. Let's look at some untidy data**

Add a dataset manually.

```
cases <- tribble(
  ~Country, ~"2011", ~"2012", ~"2013",
      "FR",    7000,    6900,    7000,
      "DE",    5800,    6000,    6200,
      "US",   15000,   14000,   13000
)
```
Take a look. What are our variables?

```
head(cases)
```

* Country
* Year
* Count

Take out a piece of paper and draw what it would look like if we rearranged our data so it had three columns: country, year, n

**3. Gather**

Let's parse this

And then run it oursevles.

<img src ="imgs/3.png" width = "600">


```
cases %>% gather(key = "year", value = "n", 2:4)
```
Neat! Now we've got something we could chart. Try this.

```
cases %>% gather(key = "year", value = "n", 2:4) %>% ggplot(aes(x= year, y=n, group=Country, color=Country)) + geom_line(lwd=3)
```

**4. Spread**

Let's use some new data.

```
pollution <- tribble(
       ~city,   ~size, ~amount,
  "New York", "large",      23,
  "New York", "small",      14,
    "London", "large",      22,
    "London", "small",      16,
   "Beijing", "large",     121,
   "Beijing", "small",     56
)

head(pollution)
```

The second column is *particle size*. What if we wanted to add together the particle counts for each city?

Right now, we can't.

But ... if 'large' and 'small' were their own columns, then we could. What would our dataset look like if the three columns were city, large, and small.

Draw it out on your piece of paper.

To make that happen, we need `spread`.

<img src ="imgs/4.png" width = "600">

```
pollution %>% spread(size, amount)
```

Nice. Now we can create the total particle count for each city.

```
pollution %>% mutate(total = large + small)
```

Or the percent of particles that are large. How would we do that?

If we have any extra time, let's do Final Project updates.


---

### Homework

* **TURN IN YOUR DRAFT!** It's due Sunday at 5 PM.


* [Go to this page and register for a Census API Key](https://api.census.gov/data/key_signup.html)
* Read these data stories to prep for next week:
	* [Battling treacherous office chairs and aching backs, aging cops and firefighters miss years of work and collect twice the pay](https://www.latimes.com/local/california/la-me-drop-20180203-htmlstory.html)
	* [Veteran L.A. cops and firefighters can work one shift, then collect double pay for years](https://www.latimes.com/local/lanow/la-me-drop-one-day-rule-20180218-story.html)
		* Optional but interesting: [Before becoming LAPD chief, Moore retired, collected a $1.27-million payout, then was rehired
](https://www.latimes.com/local/lanow/la-me-chief-drop-2018-08012-story.html)	
	* [L.A. and Orange counties are an epicenter of overcrowded housing](https://www.latimes.com/local/la-me-crowding-20140308-story.html)
	* [Mapping the country's crowded homes](http://graphics.latimes.com/crowding-map/)