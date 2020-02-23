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


# Week 6
This week, we're talking about the importance of **functions and loops**. Then we'll discuss **tidy** data ... and how to make your data tidy.

---


### Hands-on — Part 1

Here we're gonna scrape the web with the `rvest` package.

Start by installing and loading it.

```
install.packages("rvest")
library(rvest)
library(tidyverse)
library(magrittr)
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
    extract2(2) %>%
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
colnames(govs)[1] <- c("num_in_office")
colnames(govs)[3] <- c("rank_by_age")
```

Let's delete that pesky last row. See what we're doing here?

```
govs <- head(govs,40)
```

There are also some footnotes in the DOB column. Good for Wikipedia users, not good for us. This is a `regular expression`. Regex could be it's own class, but here we're just removing everything in a string after the `[` character.

```
govs$`Date of birth` <- gsub("\\[.*","",govs$`Date of birth`)
govs$`End ofterm` <- gsub("\\[.*","",govs$`End ofterm`)

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
mdy(govs$`Date of birth`)
```

Perfect. This stuff used to be a total pain, but lubridate has made it so, so painless.

Now we can fix all our dates.

```
govs$`Date of birth` <- mdy(govs$`Date of birth`)
govs$`Date of inauguration` <- mdy(govs$`Date of inauguration`)
govs$`End ofterm` <- mdy(govs$`End ofterm`)
govs$`Date of death` <- mdy(govs$`Date of death`)

```

We can also do math with dates. Check it out.

```
govs$`Date of birth` - govs$`Date of inauguration`
```

Awesome. Let's bring this class full circle and chart the data. We'll do that with the ``ggalt`` package.

```
install.packages("ggalt")
library(ggalt)
```

Now, we can actually plot out their terms in office.

```
govs %>% ggplot(aes(y = reorder(Governor, num_in_office), x = `Date of inauguration`, xend = `End ofterm`)) + geom_dumbbell(color = "steelblue")
```

We can also plot out their lifespans. Some of them are still among the living, so let's code their 'death' as today's date. Take a look at how we do that.

```
govs$`Date of death` <- case_when(is.na(govs$`Date of death`) == TRUE ~ Sys.Date(), TRUE ~ govs$`Date of death`)

govs %>% ggplot(aes(y = reorder(Governor, num_in_office), x = `Date of birth`, xend = `Date of death`)) + geom_dumbbell(color = "steelblue")
```



We can use to this work ... to talk about functions and for loops by building off our scraping.

Let do that, now we want to answer the question: **during what year were the most governors alive at the same time?**

How would we do that, just conceptually?

...

Let's start our journey by just testing out one year, to see which governors were alive then.

```
govs %>% filter(`Date of birth` < mdy("01-01-1900") & `Date of death` > mdy("01-01-1900"))
```

Great. If we just wanted a count, not all the columns, we could do this.

```
govs %>% 
	filter(`Date of birth` < mdy("01-01-1900") & `Date of death` > mdy("01-01-1900")) %>% 
	nrow()
```

Ok, here is what we're going to do. But let's unpack it for a given `i` before we run the whole function. There is a lot going on here.

```
alive_stats <- data.frame()

for (i in 1806:2018) {

	begin <- mdy(paste("01-01-",i,sep=""))
	end <- mdy(paste("01-01-",(i+1),sep=""))

	count_alive <- govs %>% filter(`Date of birth` < begin & `Date of death` > end) %>% nrow() %>% as.numeric()

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


---

### Homework

* **R Data Viz Assignment**. Using data from your Final Project create two charts using ggplot.
	* If you need inspiration, use code from our walkthrough today. Or, take a look at some of these simple cool R chart examples.
	* Due on Monday by 5 PM.
* [Go to this page and register for a Census API Key](https://api.census.gov/data/key_signup.html)
* [Create](https://github.com/join) or make sure you have a Github account and know the PW