---
layout: default
title: Getting Started
category: batman
permalink: /batman/getting-started
---
# Batman + Rails - Getting Started
  This guide covers a basic rails setup with javascript client side MVC framework.  
  
  After reading this guide you'll be able to:
  
  1. How to install rails, batman.js and connect to a database
  2. Then general layout of rails and batman.js
  3. The basics of a REST api and JSON endpoints
  4. How to do relationship modelling from Rails to batman.js
  
## Guide Assumptions

  This guide is designed for someone new to rails and javascript.  You should have a good grasp of programming, but no experience with the web is needed.  To be able to follow this guide you should have the following installed:
  
  - The [Ruby](http://www.ruby-lang.org/en/downloads) language ( >= 1.9.3 )
  - The [RubyGems](http://rubygems.org/) system
  - A text editor of your choice ( I use [Emacs](http://www.gnu.org/s/emacs) )

I wrote this guide on OSX, but it should be similar on Linux.  
  
## Introduction

  To demonstrate the framework, we are going to build a Foosball Ladder.  It will consist of users, teams and matches.  The ranking will be an ELO system, though it's not terribly important for the purpose of this guide.
  
## Setup

  The first thing you should do is see if Ruby is on your path, and install rails.  If you already have this done, you can skip but make sure you have Rails 4.0.0 installed.
  
{% highlight bash %}
$ ruby -v
$ gem install rails
$ rails -v
{% endhighlight %}

I'm using ruby version 1.9.3 and rails 4.0.0rc2.
  
## Generate the project

Now since we have the prequisite binaries installed, it's time to generate the project.  Open your terminal again ( or use the same one ) and navigate to a place you would like your code to inhabit ( I like to use ~/devel, some people like ~/Code, it's up to you! )
  
Generate the rails project by:
{% highlight bash %}
$ rails new foosball-ladder
{% endhighlight %}
  
This will create a default rails 4 project into the directory "foosball-ladder".  Go into that directory and open the Gemfile in your favourite text editor.  
  
For this project my Gemfile looks like this:
  
{% highlight ruby %}
source 'https://rubygems.org'
gem 'rails', '4.0.0.rc2'
gem 'sass-rails',   '~> 4.0.0.rc2'
gem 'coffee-rails', '~> 4.0.0'
gem 'uglifier', '>= 1.0.3'
gem 'jquery-rails'
gem 'jbuilder', '~> 1.2'
gem 'unicorn'
gem 'turbolinks'
gem 'batman-rails'
gem 'devise'
gem 'sqlite3'
gem 'debugger', group: [:development, :test]
{% endhighlight %}

The important things being:

  - batman-rails  the batman.js gem
  - devise        for easy user login code
  - debugger      to step through your code
   
After you have saved the Gemfile, go into your terminal and type:
{% highlight bash %}
$ bundle install
{% endhighlight %}

This will install of the gems you indicated above.

## Database Setup

Since we are using the default SQlite installation, we should only have to type:
{% highlight bash %}
$ rake db:create
{% endhighlight %}
   
And you should be good to go!

## Setup Devise
We'll be using the gem [devise](https://github.com/plataformatec/devise) to handle user management.  Don't worry, I've never used it either.
  
Now we'll run the generator:
{% highlight bash %}
$ rails generate devise:install
{% endhighlight %}
Follow the instructions on the screen, they're pretty important.
  
Next we'll generate a `User` model 
{% highlight bash %}
$ rails generate devise User
{% endhighlight %}
  
We can worry about the rest later.
  
## Setup the batman.js

Now to the meat, we'll be generating a default configuration for batman.js.
From your project root do the following:
  
{% highlight bash %}
$ rails generate batman:app
{% endhighlight %}
  
All of the batman.js files will be `app/assets/batman`.  For the context of these tutorials, make sure you look there first.  There will be other javascripts in `app/assets/javascripts` but those are the rails defaults.
  
  
Ok, now we have some javascript in there!  We will be using `coffee-script`, which many find easier than dealing with `javascript` ( myself included.)
  
## Setup source control ( Optional but recommended )

It's a good idea to use source control, we will be using [git](http://git-scm.com) and using [Github](http://www.github.com) as the server.  The repo for the code used in this project will be availble on my github [http://github.com/ibawt/foosball-ladder].
  
First open your terminal and go into the root of your project ( in my case `~/Code/Ruby/foosball-ladder` )
Type the following:
{% highlight bash %}
$ git init
{% endhighlight %}
This will create an empty repository.
 
Then add all of your files:
{% highlight bash %}
$ git add .
$ git commit -m "initial commit"
{% endhighlight %}
If you don't want to host your code on Github you can skip this next step.  
  
Go to [Github](http://www.github.com), navigate to create a repository and make one called `foosball-ladder`. You omit the `.gitignore`, rails will generate one for you.  
  
Now back to the terminal and type:
{% highlight bash %}
$ git add remote origin https://github.com/<username>/foosball
$ git pull --rebase
$ git push origin master
{% endhighlight %}

Now you have source control setup, with an easy way to share your code with others or show it to prospective employers.
  
## We're done!

Sort of, lets generate the default tables that `devise` made by the following command:
{% highlight bash %}
$ rake db:migrate
{% endhighlight %}

Now you can start rails from the root of your project:
  
{% highlight bash %}
$ bundle exec rails s
{% endhighlight %}  

And open a browser to <a href="http://localhost:3000">http://localhost:3000</a> and you should see the batman.js starting page!
  
Now go drink some beer.
