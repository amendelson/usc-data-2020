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


# Week 9
This week, we are going to take some big steps in our coding journey.

---

### Lecture

[Slides](https://docs.google.com/presentation/d/1Gg1DM3Q1OT5QFbs8Q4Pes57PqbwqdObb8-p58ph7pKg/edit#slide=id.p)

---

### Hands-on

**0. The pre-reqs**

You've already installed R, Miniconda and created your Github account.

**1. Let's code**

Anytime you see something that looks like `this`, or that looks like

```
this
```

...that's code. These course webpages are tutorials we're going to go through.

**2. Taking the terminal for a spin**

Alright, open up your **terminal**. On Windows, this may be called **PowerShell**.

It make take a sec to boot up. You should see something like this

<img src="imgs/1.png" width="400">

That dollar sign is important. After the dollar sign, we'll put the code in many examples (like what we're about to do). Try this out:

```
$ ls
```

Now this:

```
$ open .
```

Let's navigate to somewhere you keep code. If I want to keep it on a folder on my desktop called 'code', here's how I'd do that:

```
$ cd ~/Desktop/code/
```

Now try ```ls``` again.

Neat. [Here is a list of common commands](https://www.tjhsst.edu/~dhyatt/superap/unixcmd.html) — worth bookmarking.

**3. Setting up our notebook**

OK, now we want to get our notebook up and running. But there's a catch.

We need to download Jupyter first.

```
pip install jupyter
```

And oh, by the way, R, our programming language of choice, doesn't come pre-installed on Jupyter notebooks. This is the type of setup challenge that is common in coding. With a little googling and persistence, we can fix it.

So let's install it. In the terminal, do this:

```
$ R
```

If you have R installed, you've opened it up. (Notice the dollar sign is gone.) Now run this:

```
install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'pbdZMQ', 'devtools', 'uuid', 'digest'))
 
```

You'll have to pick a 'mirror' to install them.

Now, let's install one more package, with the following code:

```
devtools::install_github('IRkernel/IRkernel')
```

Getting close. We need to run this to make the package available:

```
IRkernel::installspec(user = FALSE)
```

**4. Opening up the notebook**

Alright, time to open up that notebook. Open a new window or tab in your terminal, just like you would on a web browser. Then navigate to a folder where you keep your code (like we did above).

And type in:

```
jupyter notebook
```

And boom!

**5. Wait, did my web browser just open up?**

Yes it did. You use a Jupyter Notebook through the browser.

Except it's not online—it's actually running "locally" — only on your computer. Pretty nifty.

You should see all the files of wherever you directed your terminal window in step two. If it's in the right place, click on the "new" button and add an R notebook.

**6. Test things out**

The way Jupyter works is that you type your code into the gray cell, and then see the output below.

Your work can continue in the *next* gray cell after that.

Start by typing this in

```
demo(graphics)
```

Look familar?

**7. Lets look at some data**

Try this

```
head(mtcars)
```

Now this

```
head(mtcars, 25)
```

What's the difference?

OK, how about

```
summary(mtcars)
```

Or

```
str(mtcars)
```

OK, now type each of these things in and see what happens

```
"I should exercise more."
1+1
1==2
1:1000
animals <- c("bears","monkeys","donkeys")
animals[1]
class(animals)
class(1==2)
class(1:1000)
```

**9. Explore some data**

OK, let's go back to the cars data. What does this do.

```
mtcars$mpg
```

In that code, `mtcars` is our dataframe. And `mpg` is the vector of the dataframe. It's a column, basically.

We can do math on the whole dataframe:

```
mtcars$mpg * 2

```
Alright, let's make a quick chart. In data journalism, you make approximately 100 charts for internal use and data exploration for every chart you actually publish. So here's a chart to explore the miles per gallon these cars get. 

```
hist(mtcars$mpg)
```
Cool! A histogram. So what's this showing us?

Ok, here's a different type of graph:

```
plot(mtcars$mpg)
```

And we can plot two variables at once on a scatterplot.

```
plot(mtcars$hp, mtcars$mpg)
```

If you don't understand how something works in R, you can always put a quesiton mark in front of it to get the help box to pop up.

```
?plot
```

You can also plot every variable against every other variable:

```
pairs(mtcars)
```

Now, so your prof can prepare for the rest of the course, type this in:

```
install.packages("tidyverse")
```

And then this:

```
library(tidyverse)
```

Questions? If we have any extra time, we'll look at brining in some real life data...or commiting everything to Github.

---

### Links

---

### Homework

* Mapping Assignment 3: I want you to map some data related to your Final Project. Doesn't have to be something you'll necessarily use in your Final Project, just something related. Every group member needs to make their own map.
	* You've got two weeks to do it, so I expect something good.
* Story memo: 50-100 words about Final Project progress over last week