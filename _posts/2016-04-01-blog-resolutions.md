---
layout: post
title:  Github Pages Jekyll and Stale Resolutions 
date:   2016-04-01 
categories: jekyll update
author: "Matt R"
featured_image: 'http://placekitten.com/400/400'
tags: [JEKYLL, GITHUB PAGES, BLOG, HOWTO ]
---

### Resolution reality check.

That's right it's April fools day, and I'm starting a new blog. This year is one third in the bag, which means I really should get cracking on those New Year's resolutions. Let's see, what they were? Where did I put that list? 

Oh right here we go.

> 1. Surpass John Skeet's rep on Stack Overflow for the c# tag
> 2. Launch a photo-sharing app that is acquired by a to-be-named social media platform for bazillion dollars.
> 3. Start a professional blog. 

OK admittedly the first two may well have been the champagne talking, and in the stark light of April are seem tougher than last round of Cook’s (nothing but the best) led me to believe. But that number 3 is looking mighty approachable. So a new blog, on April fools day, I suppose that makes me your April fool. On with it!

### I need a blog and I need it FAST!

Good news, if you're reading this, you can exhale, it all worked out, the blog is live! But how you may ask did you go from the unblogged masses to the bloggerati in a mere 24 hours. I mean sure I'm a trained software professional, sure I have years of experience but where do I start? Roll my own? That would take forever! Wordpress? Boring. And where should I host it? If only there was a preferred solution to well integrated with a solution that I already use.

Github Pages and Jekyll to the rescue! ![jeykll octocat](/images/octojekyll.png)

### First things first, setup your Github Page repo

There are two basic types of pages, profile/orginization, and project pages. There are slight differences, but the gist is you get one profile/organization page per account and one project page per repository. Here we'll be setting up a profile page.

#### Step 1: Create a repo
Open your github profile. And add a new Repository. It must be named username.github.io where username is your username.

<img class="img-thumbnail" src="/images/add-repo.png">

#### Step 2: Clone your new repo locally
{% highlight bash %}
~ $ git clone https://github.com/username/username.github.io
{% endhighlight %}

#### Step 3: Hello World
{% highlight bash %}
~ $ cd username.github.io
~ $ echo "Hello World" > index.html
{% endhighlight %}

#### Step 4: Add, commit, push and enjoy!
{% highlight bash %}
~ $ git add --all
~ $ git commit -m "My awesome index page"
~ $ git push -u origin master
{% endhighlight %}

That's it, your site is now live, just browse to "username.github.io" (your username) Which is great but we probably want a bit more than the old "Hello World". That's where Jekyll comes in. 

#### Who's this Jekyll guy anyway?

Jekyll is an easy to use static site generator built in Ruby. Basically, it lets you implement many features of a full CMS, but without the overhead of maintaining a database. Jekyll lets you build reusable page templates and includes in [Liquid][Liquid] a template engine built for [Shopify](http://www.shopify.com/). [Liquid][Liquid] Templates are simple, secure and stateless. Jekyll is "blog-aware" out of the box, so things like permalinks, categories, pages, and posts are standard right out of the box. 

### Getting up and running with Jekyll

#### Step 1: System Prerequisites
Jekyll is a cmd line tool written in Ruby, so naturally you'll need to have Ruby installed. But first, you'll want to be sure that Xcode Command Line Tool are installed as well as [homebrew](http://brew.sh/). 

{% highlight bash %}
~ $ xcode-select -p
{% endhighlight %}

If you get the following output you're good to go.  

{% highlight bash %}
/Applications/Xcode.app/Contents/Developer
{% endhighlight %}

Otherwise you'll need to install them, the following command will kick off a download and install dialog.
 
{% highlight bash %}
~ $ xcode-select --install
{% endhighlight %}

Now we can Instal Ruby. 

{% highlight bash %}
~ $ brew update
~ $ brew install rbenv ruby-build

# Add rbenv to bash so that it loads every time you open a terminal
~ $ echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
~ $ source ~/.bash_profile

# Install Ruby
~ $ rbenv install 2.2.3
~ $ rbenv global 2.2.3
~ $ ruby -v
{% endhighlight %}

#### Step 2: Install and run Jekyll 
{% highlight bash %}
~ $ gem install jekyll
~ $ gem install github-pages
~ $ jekyll new my-site
~ $ cd my-site
~ /my-site $ jekyll serve
# => Now browse to http://localhost:4000
{% endhighlight %}

That's it you've just built your first Jekyll site!


<img class="img-thumbnail" src="/images/yourawesomesite.png">


Jekyll ships with it's own tiny webserver so you can get right to hacking on your new site. It also is configured to watch your file system and recompile when changes are detected. How cool is that?

That enough for now, crack a beer for a job well done. In our next post we'll cover Jekyll plugins for useful things like pagination, taming layouts with [Liquid][Liquid], Less and Bootstrap and getting our custom domain properly configured. 


[Liquid]:https://github.com/Shopify/liquid/wiki