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


# Week 5
This week, we're going to go deeper into how you can use data in a story. And you're going to get deeper into reporting your final project.

---

### Lecture

[Slides](https://docs.google.com/presentation/d/1SAIAJIpp8aEBRDGRytwSn5jl6ObeOlnaLxdhElPajqw/edit?usp=sharing)

---

### Hands-on

* Group project discussions. Talk about:

	* how to explore your data set
	* what trends you want to look for
	* what limitations are in the data


---

### Links

* [990
people were shot and killed by police this year
Here’s what we learned.](https://www.washingtonpost.com/graphics/national/police-shootings-year-end/)
* [A MAP OF EVERY BUILDING IN AMERICA](https://www.nytimes.com/interactive/2018/10/12/us/map-of-every-building-in-the-united-states.html)
* [To Help Prevent the Next Big
Wildfire, Let the Forest Burn](https://www.nytimes.com/interactive/2018/11/29/opinion/sunday/california-wildfires-forest-management.html)
* [The Tennis Racket](https://www.buzzfeednews.com/article/heidiblake/the-tennis-racket)
* [Repeat podcast](https://www.scpr.org/repeat)
* [Officer Involved](http://projects.scpr.org/officer-involved/)
* [How California Lawmakers Goosed Jackpots To Create Record-Setting Lottery Sales](http://laist.com/2018/06/19/lottery.php)
* [Precision journalism video](https://www.youtube.com/watch?v=FbYR78vyhw0)

---

### Homework

* Start reporting.
* File another story memo. Due before class.