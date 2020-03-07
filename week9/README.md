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


# Week 9

We'll be spending some more time with R, getting more practice with Github, and exploring other ways to use R.

---

## Hands-on


## Part 0: Intro to Github

Let's use an R script you've created in this class for this part of the lesson.

First, create a folder somewhere that you keep code and put that in it.

Put your R code inside it.

Now, fire up your terminal/command prompt etc. Navigate to your directory using one of these, with the correct path.

```
chdir /Code/my_folder/
cd /Code/my_folder/
```

Alright, now let's check if you've got git installed.

```
git --version
```

Hopefully, something pops up telling you that you've got git. If not, [check out these instructions](https://www.firstpythonnotebook.org/prerequisites/git.html).

From here on out, we're borrowing heavily from [a great tutorial](https://www.firstpythonnotebook.org) of interest to all you Python mavens out there.

The first step in working with git is to convert a directory on your computer into a repository that will have its contents tracked going forward.

Enter the following:

```
$ git init .
```

That will instruct git to initialize a new repository in your current folder, which is represented by the period.

If this is your first time using git, you should configure git with your name and email. This will ensure that your work is properly logged by the respository’s history file. Like the init command above, this is something that only needs to be done once.

```
$ git config --global user.email "your@email.com"
$ git config --global user.name "your name"
```

Now you’re ready to start logging your work. Changes to you code are logged by git in batches known as “commits.”

It is not required but a good first step before committing any work is to run git’s status command, which will output the current state of your repository.

```
git status
```

Since your repository is brand new, all of the files will be listed as “untracked.” That means that while git sees that these files exist it is not monitoring them for changes.

The first step in logging your work is to ask git to start tracking your files using the add command.

In this repository, we will go ahead and add any and everything.

```
$ git add .
```

Now, let's check the status again.

```
git status
```

Log its addition with git’s commit command. You must include a personalized message, which you can provide along with the command by adding on the -m flag along with a description of the work you’ve done.

```
git commit -m "First commit"
```

That’s it. You’ve made your first git commit.

We're not done yet. We still need to publish this to Github.

Visit GitHub and create a new public repository named usc-r. Don’t check “Initialize with README.” You want to start with a blank repository.

This will create a new repository page. It needs to be synchronized with the local repository we’ve already created.

You can connect your local directory to GitHub’s site by returning to the terminal and using git’s “remote add” command to connect it with GitHub.

```
git remote add origin https://github.com/<yourusername>/usc-r.git
```

Next we’ll try “pushing” the latest commit from your repository up to GitHub. Assuming all of your work has been properly logged to your local repository, here’s what it takes.

```
git push origin master
```

That ... should work! Congrats!

I keep [this cheatsheet at my desk for answering Github Qs](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)...it's helped out many times. You'll see there are many other commands.

We'll come back to Github later, but for now ... let's map in R!


## Part 1: Rmarkdown


Let's do something new today: Let's work from a Rmarkdown file.

These files are a popular way to share code, and not unlike the notebooks we discussed earlier this year.

Most of the basics of the markdown language are [laid out here](https://rmarkdown.rstudio.com/authoring_basics.html).

Let's open one up and save it. Make sure to save it in a new folder — we're going to commit this to Github later. You have to essentially save it twice — first setting it up, and second saving it to your computer.

We can see how the basic setup works but running the code in the template it provides.

Basically, the Rmarkdown notebooks let us alternate code and text in a reader-friendly way. When might this be helpful in a newsroom?

Let's get a sense of what that looks like by "knitting" our document into an HTML page.

Do that, and then let's spend a moment examining how our R code translates into what we see on the webpage.

## Part 2: Data transformations and mapping in ggplot

With **tidycensus**, you can actually download the shape files with the data you want already attached. No joins necessary.

I didn't tell you this in previous weeks ... because it's important to learn about joins the hard way.

So let's delete what's already in our markdown file. And create our first code chunk.

```
```{r tidyness, warning=F, message=F, echo=T}
library(tidycensus)
library(tidyverse)```
```

Cool! Nothing happened. We need to run it. There are multiple ways to do that.

All this does is load tidycensus. We also need to load your census API, if it is not already installed.

```
```{r key, eval=F}
# Pass it the census key you set up before
census_api_key("YOUR API KEY GOES HERE")```
```

Now let's get unemployment data for LA County. Lot going on here, so let's get it running and then see what it's doing.

```
```{r racejobvars, warning=F, message=F, quietly=T, echo=T, results='hide'}
jobs <- c(labor_force = "B23025_005E",
              unemployed = "B23025_002E")
lac <- get_acs(geography="tract", year=2016,
                  variables= jobs, county = "Los Angeles",
                  state="CA", geometry=T)```
```

And what does that look like?

```
```{r lac, echo=T}
head(lac)```
```

We want to get the rate, right? The data is not in the right shape yet. What do we need to do?

Let's do it all in one fell swoop.

```
```{r}
lac_tidy <- lac %>%
  mutate(variable=case_when(
    variable=="B23025_005" ~ "Unemployed",
    variable=="B23025_002" ~ "Workforce")) %>%
  select(-moe) %>%
  spread(variable, estimate) %>%
  mutate(percent_unemployed=round(Unemployed/Workforce*100,2))```

```

We can now plot it.

```
```{r}
lac_tidy %>% ggplot(aes(fill=percent_unemployed)) +
  geom_sf(color=NA) +
  theme_void() +
  theme(panel.grid.major = element_line(colour = NA)) +
  scale_fill_distiller(palette="Reds", direction=1, name="Estimate") +
  labs(title="Percent unemployed in Los Angeles")```
```

Hmm. Might be easier to read without those pesky, ecologically-rich islands. Let's filter them out. Spot the difference.

```
```{r}
lac_tidy %>%
	filter(GEOID != "06037599000" & GEOID != "06037599100") %>%
	ggplot(aes(fill=percent_unemployed)) +
	  geom_sf(color=NA) +
	  theme_void() +
	  theme(panel.grid.major = element_line(colour = NA)) +
	  scale_fill_distiller(palette="Reds", direction=1, name="Estimate") +
	  labs(title="Percent unemployed in Los Angeles")```
```

Neat. Let's knit it and see what that looks like.

Thanks to [this great tutorial for our inspiration here](https://github.com/andrewbtran/NICAR-2019-mapping/blob/master/01_maps_code.Rmd).

## Let's commit that to Github

We're repurposing this from [last week](https://amendelson.github.io/usc-data-2020/week8/).

Start by opening your terminal. Make sure you are in your new folder.

Now you’re ready to start logging your work. Changes to you code are logged by git in batches known as “commits.”

It is not required but a good first step before committing any work is to run git’s status command, which will output the current state of your repository.

```
git status
```

Since your repository is brand new, all of the files will be listed as “untracked.” That means that while git sees that these files exist it is not monitoring them for changes.

The first step in logging your work is to ask git to start tracking your files using the add command.

In this repository, we will go ahead and add any and everything.

```
$ git add .
```

Now, let's check the status again.

```
git status
```

Log its addition with git’s commit command. You must include a personalized message, which you can provide along with the command by adding on the -m flag along with a description of the work you’ve done.

```
git commit -m "First commit"
```

That’s it. You’ve made your first git commit.

We're not done yet. We still need to publish this to Github.

We’ll try “pushing” the latest commit from your repository up to GitHub. Assuming all of your work has been properly logged to your local repository, here’s what it takes.

```
git push origin master
```

Cool. Now try this again.

```
git status
```

## Creating a searchable table

One thing you may want to do in your journalism life is create a searchable table, whether to publish, for your own use, or to share with editors and collaborators.

Thankfully, that's easy to do. Let's check out the `DT` library.

```
install.packages("DT")
library(DT)```
```

Let's get rid of a couple vectors we don't need, and use it.

```
```{r}
lac_tidy$geometry <- NULL
lac_tidy$GEOID <- NULL
datatable(lac_tidy)```
```

This is one of [many great htmlwidets in R](https://www.htmlwidgets.org/showcase_datatables.html) that make creating things for the internet a breeze.

Let's commit again to Github. And with any remaining time we can

1) meet in Final Project groups

2) explore some of those widgets

---

### Homework

<div class ="header">
<h1><font color = "White">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Spring break&nbsp;!&nbsp;!&nbsp;!


