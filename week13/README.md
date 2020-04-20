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

# Week 13
This week, we're gonna talk election maps and interactivity. And then we'll start on a map of our own.

---

### Lecture

[Slides](https://docs.google.com/presentation/d/1NFou_0UfhSHlNGxb3QEeVgLE2SBRFpB_J6gnVEkcnLQ/edit#slide=id.p)

---

### Hands-on

We've got some piping-hot data: the latest unemployment figures for California.

You're the only data journalist around in the newsroom, and the editors want a map ASAP.

What do you do?

[Start here](https://data.edd.ca.gov/Labor-Force-and-Unemployment-Rates/Labor-Force-and-Unemployment-Rate-for-California-C/r8rw-9pxx).

We'll go over how to wrangle.

And then you'll go into groups, and use QGIS to make another map using the data.

**Your editor demands a fresh map on the unemployment rate, putting this month's numbers in geographical context.** What can you come up with?

For you map, please:

* Color counties based on unemployment rate
* Add labels
* Find the text annotation tool and add a note to the map
* Export the map with a legend


BTW, here is a [definition](https://web.archive.org/web/20061217002213/http://www.labormarketinfo.edd.ca.gov/article.asp?ARTICLEID=118) of *seasonally-adjusted*:

> Over the course of a year, the size of the labor force, the levels of employment and unemployment, and other measures of labor market activity undergo fluctuations due to seasonal events including changes in weather, harvests, major holidays, and school schedules.  Because these seasonal events follow a more or less regular pattern each year, their influence on statistical trends can be eliminated by seasonally adjusting the statistics from month to month.  These seasonal adjustments make it easier to observe the cyclical*, underlying trend, and other nonseasonal movements in the series.

> As a general rule, the monthly employment and unemployment numbers reported in the news are seasonally adjusted data.  Seasonally adjusted data are useful when comparing several months of data. Annual average estimates are calculated from the not seasonally adjusted data series.



...

([Here is something we will need](https://data.ca.gov/dataset/ca-geographic-boundaries))

---

### Links

* An example of [cool stuff](http://graphics.latimes.com/calmap-california-county-unemployment/) you can do with unemployment data.
* Quartz on [how the unemployment rate can mislead](https://qz.com/877432/the-us-unemployment-rate-measure-is-deceptive-and-doesnt-need-to-be/)

Election maps

[Presenting the least misleading map of the 2016 election](https://www.washingtonpost.com/news/politics/wp/2018/07/30/presenting-the-least-misleading-map-of-the-2016-election/?utm_term=.0d639286a97d) | [An extremely detailed map of the 2016 election](https://www.washingtonpost.com/news/politics/wp/2018/07/30/presenting-the-least-misleading-map-of-the-2016-election/?utm_term=.0d639286a97d) | [Trump to display map of 2016 election results in the White House: report](https://thehill.com/blogs/blog-briefing-room/332927-trump-will-hang-map-of-2016-election-results-in-the-white-house)

2018 election maps

[WaPo](https://thehill.com/blogs/blog-briefing-room/332927-trump-will-hang-map-of-2016-election-results-in-the-white-house) | [NYT](https://www.nytimes.com/interactive/2018/11/06/us/elections/results-house-elections.html) | [LAT](https://www.latimes.com/projects/la-pol-na-us-general-election-results-2018/)

Other/interactivity:

* [In America's 'Worst Bike City,' Laws To Protect Cyclists Are Rarely Enforced](https://laist.com/2018/12/04/bike_safety_los_angeles_law_three-feet-law.php)
* [The Problem With Interactive Graphics](https://www.fastcompany.com/3069008/the-problem-with-interactive-graphics)
* [In Defense of Interactive Graphics](https://www.vis4.net/blog/2017/03/in-defense-of-interactive-graphics/)
* [Why we are doing fewer  interactives](https://github.com/archietse/malofiej-2016/blob/master/tse-malofiej-2016-slides.pdf)

---

### Homework

**Mapping assignment 2**

We talked election maps this week. Now it's your turn to make one of your own.

[Click here to download the data](https://amendelson.github.io/usc-data-2020/data/prop64.zip) that you'll use.

What is it? It's precinct-level election results, from California's [landmark Proposition 64](https://ballotpedia.org/California_Proposition_64,_Marijuana_Legalization_(2016)) in 2016. That was the ballot measure that legalized recreational marijuana in the Golden State. The shapefile features precincts in Los Angeles County. Roughly 1 in 4 California voters lives here in L.A. County.

I want you to **create and export a Prop 64 election map** in QGIS, with the following features:

* A title
* A legend
* A text annotation, describing some takeaway or geographic trend in the election results map. [Here's how you make one](https://docs.qgis.org/2.14/fi/docs/user_manual/introduction/general_tools.html#annotation-tools)

Once you do that, write a pitch of 100 words for a data story you could do with this information.

Please send the map by 5 PM Monday.

**Due Monday at 5 PM**.