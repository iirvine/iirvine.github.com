---
layout: post
title: "obligatory octopress metablog post"
date: 2012-07-22 18:04
comments: true
categories: 
---
###Octopress, YAY. 
Keeping with the tradition of using one of your first posts on your new Octopress blog to blog about how you set up your new Octopress blog, here are some notes. 

I've had to do this twice now, both times with some small amount of goofiness, but all in all quite an untroubled installation, considering I know nothing about Jekyll/Ruby and am not git's most favorite person in the world. These were my general steps for getting things up and running on a span brankin' new MacBook Air.

First, install git. Self explanatory, really. Although I did run into some funny business installing Git manually vs through [Homebrew](http://mxcl.github.com/homebrew/), vs some older version that was installed when I downloaded XCode - generally, I'd recommend just saving yourself some trouble and getting it from Homebrew to begin with. 
 
As an aside: in switching to a new, more professionally aliased GitHub account, git had something of a tantrum and was having difficulty letting go of my old user name. I changed the global git config, which did absolutely nothing. Finally I deleted my old ssh keys, generated new ones, and ran ssh-add, and that seemed to do the trick, so git is off my shit list - *for now*.
 
Next was installing [rbenv](https://github.com/sstephenson/rbenv#section_2) and [ruby-build](https://github.com/sstephenson/ruby-build). Again, Homebrew to the rescue here. They both installed with pretty much no hassle. 

Of note was that I went with rbenv instead of rvm because it seems the latter has fallen out of favor as of late, at least that's what I inferred from [this](https://twitter.com/octopress/status/219423650477129728) tweet.

Next is setting up your repo on GitHub. If you're starting a user site, don't do what I did and spend an hour trying to figure out why your repo called "username" isn't building a proper Github page and is messing up all of Octopress' rake tasks and generally nothing is working - make a repo named "username.github.com", like you're supposed to, otherwise, you'll feel really dumb.

Now you'll setup your local directory, ie, some folder on your machine called "MyAwesomeBlog" - then use rbenv to set the local ruby version to Octopress' preferred flavor, the esoterically named "1.9.2-p290": 

```
rbenv local 1.9.2-p290
```

It'll probably tell you that it's not been installed yet, silly, which you can do with 

```
rbenv install 1.9.2-p290 
```

You can check that all is well in ruby-land with 

```
rbenv local
```

Okay, now comes the fun stuff. "Install" Octopress by cloning it into the local directory you'll be using to house your blog, ie 

```
git clone git://github.com/imathis/octopress.git MyAwesomeBlog/
```

All done? Get those delicious dependencies with bundler! 

```
gem install bundler #if you've not installed it already
bundle install
```

From this point, it's pretty much smooth sailing. Work your way through the [documentation](http://octopress.org/docs/), use the super convenient rake tasks to install the default theme and setup github pages…

Then do a rake generate! Then a rake deploy! Then browse to username.github.com and *gaze* upon the splendidness of the base, unadorned octopress theme! Then do a happy dance, because everything is working splendidly, and you are obviously splendid, etc etc. (I recommend playing [this song](http://www.youtube.com/watch?v=mwrbOEaJPBY) for this part).

Then install a new theme, because rolling with a basic, untouched octopress design is like, so 2011. Update your _config.yml with your name and super clever title and BOOM. You're pretty much good to go. 
 