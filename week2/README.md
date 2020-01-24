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


# Week Two
This week, we're going to talk about what makes a great data story, and how you can create one of your own.

---

### Survey responses

<img src="survey1.png" width = "1000">

<img src="survey2.png" width = "1000">

---

### Lecture

[Slides](https://docs.google.com/presentation/d/1NoKsLIV9dK4agyiTyc2XGbSux6WzJgpidJ5tLHQH8jc/edit?usp=sharing)

---

### Links

Some stories mentioned:

* [Fatal Force](https://www.washingtonpost.com/graphics/2018/national/police-shootings-2018/?utm_term=.2af26663c5d2)
* [Spies in the skies](https://www.buzzfeednews.com/article/peteraldhous/spies-in-the-skies#.ymOqmNLdjW)
* [Why Kevin Durant’s Shoes Keep Falling Off
](https://fivethirtyeight.com/features/why-kevin-durants-shoes-keep-falling-off/)
* ['A tricky area of philanthropy': LA mayor solicits millions for his favored causes](https://www.scpr.org/news/2017/08/23/74917/la-mayor-garcetti-behested-payments/)
* [Where will the West's next deadly wildfire strike? The risks are everywhere](https://www.azcentral.com/in-depth/news/local/arizona-wildfires/2019/07/22/wildfire-risks-more-than-500-spots-have-greater-hazard-than-paradise/1434502001/)

---

### Homework

* **Important**: Sign up [using this spreadsheet](https://docs.google.com/spreadsheets/d/14IInAih3Vt4fj4e2IH1uIUXeJbnzcM8XhdVx9w-V8oc/edit#gid=0) to do a critique
* **Also important**: Final Project: Every group pitches 3 ideas by Monday @ 5 PM
