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


# Week One
This week, we'll talk about what data journalism is, how to do it, and what are goals are for this class. 

We'll also do some housekeeping and get to know one another.

---

### Lecture

[Slides](https://docs.google.com/presentation/d/1HCtEYXhYAqZxRhrCECONrv6RTScKqk7spzMMwC35tdA/edit?usp=sharing)

---

### Links

[QGIS](https://download.qgis.org/)

[R Studio](https://www.rstudio.com/products/rstudio/download/)

[R](https://cran.rstudio.com/)

[Arrest data](https://data.lacity.org/A-Safe-City/Arrest-Data-from-2010-to-Present/yru6-6re4)

---

### Homework

* [Fill out the survey](https://docs.google.com/forms/d/e/1FAIpQLSe4a5ZWgu1Tde99acbMBysX4QuS0VWtYnp0cDQb97HWGfGq5w/viewform?usp=sf_link)
* [Install or update QGIS](https://download.qgis.org/)
* Email Aaron (aaron.a.mendelsonATgmailDOTcom) if you want to choose your own group for the Final Project