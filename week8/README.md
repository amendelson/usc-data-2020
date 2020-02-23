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


# Week 8


---

### Hands-on

holding for a guest speaker...

### Intro to Github

Let's download [the file we used to scrape the governor data](https://github.com/amendelson/usc-data-2020/blob/gh-pages/week12/govs_scraping.R).

That was a pretty cool thing we did, so we want to save it for the future, and to share it with the world.

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

You do that by returning to your terminal. If your notebook server is running, hit the CTRL-C key combination to return the standard command line. Then entering the following:

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



---

### Homework

* Final Project: Your data should be set, and you should be reporting and writing as you go.
* Story memo: 50-100 words about Final Project progress over last week
* Github: Create an account if you don't already have one. If you do, make sure you know the password.
