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

# Week 13


---

### Hands-on

[overcrowding code](https://github.com/ryanvmenezes/notebooks/blob/master/Z-values.ipynb)

---

### Links


* [Go to this page and register for a Census API Key](https://api.census.gov/data/key_signup.html)
* Read these data stories to prep for next week:
	* [Battling treacherous office chairs and aching backs, aging cops and firefighters miss years of work and collect twice the pay](https://www.latimes.com/local/california/la-me-drop-20180203-htmlstory.html)
	* [Veteran L.A. cops and firefighters can work one shift, then collect double pay for years](https://www.latimes.com/local/lanow/la-me-drop-one-day-rule-20180218-story.html)
		* Optional but interesting: [Before becoming LAPD chief, Moore retired, collected a $1.27-million payout, then was rehired
](https://www.latimes.com/local/lanow/la-me-chief-drop-2018-08012-story.html)	
	* [L.A. and Orange counties are an epicenter of overcrowded housing](https://www.latimes.com/local/la-me-crowding-20140308-story.html)
	* [Mapping the country's crowded homes](http://graphics.latimes.com/crowding-map/)



