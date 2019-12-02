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

# Week 7
This week, we're gonna talk election maps and interactivity. And then we'll start on an interactive map of our own — and start coding for the first time this semester.

---

### Lecture

[Slides](https://docs.google.com/presentation/d/1NFou_0UfhSHlNGxb3QEeVgLE2SBRFpB_J6gnVEkcnLQ/edit#slide=id.g4a430350dc_0_161)

---

### Hands-on

We're going to learn how to build an interactive map, following [this tutorial](https://leafletjs.com/examples/choropleth/).

Leaflet is a popular library for creating maps — and it's open source. We're pro-maps and pro-open source in this class.

Download [this index.html file](files/index.html) to get started with the tutorial. We'll go through it together, step by step.

We'll also need this for the tutorial.

```
pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw
```

*Here's [a finished version](files/finished.html) of the file*.

---

### Links
2016 election maps

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

[Click here to download the data](https://amendelson.github.io/usc-course-spring-2019/data/prop64.zip) that you'll use.

What is it? It's precinct-level election results, from California's [landmark Proposition 64](https://ballotpedia.org/California_Proposition_64,_Marijuana_Legalization_(2016)) in 2016. That was the ballot measure that legalized recreational marijuana in the Golden State. The shapefile features precincts in Los Angeles County. Roughly 1 in 4 California voters lives here in L.A. County.

I want you to **create and export a Prop 64 election map** in QGIS, with the following features:

* A title
* A legend
* A text annotation, describing some takeaway or geographic trend in the election results map. [Here's how you make one](https://docs.qgis.org/2.14/fi/docs/user_manual/introduction/general_tools.html#annotation-tools)

Once you do that, write a pitch of 100 words for a data story you could do with this information.

Please send the map by 5 PM Monday.

**Due Monday at 5 PM**.

* Final Project: Your data should be set, and you should be reporting and writing as you go.
* Story memo: 50-100 words about Final Project progress over last week