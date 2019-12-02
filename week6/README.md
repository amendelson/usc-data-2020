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


# Week 6
This week, we'll use those new mapping skills (and some old-fashioned problem solving) to tackle a breaking news challenge.

---

### Lecture

There is no lecture! No time! There's breaking news!

---

### Hands-on

We've got some piping-hot data: the latest unemployment figures for California.

You're the only data journalist around in the newsroom, and the editors want a map ASAP.

What do you do?

[Start here](https://data.edd.ca.gov/Labor-Force-and-Unemployment-Rates/Labor-Force-and-Unemployment-Rate-for-California-C/r8rw-9pxx).

We'll go over how to wrangle that and make a county-by-county map. 

BTW, here is a [definition](https://web.archive.org/web/20061217002213/http://www.labormarketinfo.edd.ca.gov/article.asp?ARTICLEID=118) of *seasonally-adjusted*:

> Over the course of a year, the size of the labor force, the levels of employment and unemployment, and other measures of labor market activity undergo fluctuations due to seasonal events including changes in weather, harvests, major holidays, and school schedules.  Because these seasonal events follow a more or less regular pattern each year, their influence on statistical trends can be eliminated by seasonally adjusting the statistics from month to month.  These seasonal adjustments make it easier to observe the cyclical*, underlying trend, and other nonseasonal movements in the series. 

> As a general rule, the monthly employment and unemployment numbers reported in the news are seasonally adjusted data.  Seasonally adjusted data are useful when comparing several months of data. Annual average estimates are calculated from the not seasonally adjusted data series. 


And then you'll use QGIS to make another map using the data.

**Your editor demands a fresh angle on the unemployment rate, putting this month's numbers in historical context.** What can you come up with?

...

([Here is something we will need](https://data.ca.gov/dataset/ca-geographic-boundaries/resource/091ff50d-bb24-4537-a974-2ce89c6e8663)) 

---

### Links

* An example of [cool stuff](http://graphics.latimes.com/calmap-california-county-unemployment/) you can do with unemployment data.
* Quartz on [how the unemployment rate can mislead](https://qz.com/877432/the-us-unemployment-rate-measure-is-deceptive-and-doesnt-need-to-be/)

---

### Homework

* You are working on your Final Project
* Story memo: 50-100 words about Final Project progress over last week