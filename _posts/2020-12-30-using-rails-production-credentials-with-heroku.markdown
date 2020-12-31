---
layout: post
title: "Using Rails Production Credentials with Heroku"
date: 2020-12-30 21:32:42 -0800
tags:
 - coding
---

Ruby on Rails offers a credentials feature to store secret information in your repository. The keys Rails creates are added to the `.gitignore` file, but any secret information itself is encrypted and can be checked into git. There's more info on credentials [here](https://edgeguides.rubyonrails.org/security.html#custom-credentials).

I found myself confronted with the specific problem of how to use these credentials in Heroku. If you're using only a master key and store your credentials in `config/credentials.ymc.enc`, that's easy: you just set an environment variable in Heroku called `RAILS_MASTER_KEY` to the contents of your `config/master.key` file.

But what if you use separate credential files for each environment? Then the master key won't do. You'll need to use the production key in `config/credentials/production.key`. This key is likewise ignored by git—which you want, for security reasons—so you somehow have to tell Heroku about the production key, presumably also through an environment variable.

First, I tried setting an environment variable called `RAILS_PRODUCTION_KEY`. But that didn't work. Then I found the answer [in this question](https://stackoverflow.com/questions/63642303/how-to-set-rails-production-key-config-var-on-a-rails-6-app-on-heroku): you simply set the environment variable called `RAILS_MASTER_KEY` to your production key. That's how you "trick" Heroku into using your production key as a master key and make credentials work in Heroku if you're using a separate credential file for your production environment.
