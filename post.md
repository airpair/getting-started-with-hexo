I decided to get back to blogging last week. I was looking an alternative to [Wordpress](https://wordpress.com/), which I was tired of for many reasons:
+ It felt big & slow
+ It felt "closed" & old.
+ It wasn't developer friendly:
    -- I wanted to put write in Markdown
    -- I wanted to put in code blocks and have them formatted.

After a bit of Googling, I saw that [Jekyll](http://jekyllrb.com/) with [GitHub pages](https://pages.github.com/) for hosting was a popular option. Though this looked promising, I just couldn't wrap my head around Jekyll. It was bigger than what I had in mind, and just didn't fit me. GitHub pages seemed sweet though.

The search continued, and then I found [Hexo](https://hexo.io/). It was love at first sight. The initial set up was painless, there were many themes and plugins and the write/publish workflow was smooth.

Here's my guide on **"Getting started with Hexo"**, follow along and let's get a bit of lovin' over to you!

## The initial set up
Assuming you have node installed on your machine, this is fairly simple. On my Mac, this installs the hexo command line interface:
```
$ sudo npm install -g hexo-cli
```

After this, I initialized my blog directory & saved the node modules needed for the blog to render:
```
$ hexo init appapappa
$ npm install hexo --save
```
This done, I was all set to power up hexo and check-it out:

```
$ hexo server
```

And then power up Chrome at http://localhost:4000 to see something like this...

![before](https://www.anony.ws/i/2015/05/19/hexo.png)

This done, it was time to configure hexo. Hexo has a very simple YAML config file under \_config.yml.

This is how my config file started to look after a few simple customizations; the main things I changed were the title, the author, the language (to en), the URL and the default category from uncategorized to journal.

```
# Site
title: a cuppa appa
subtitle:
description:
author: Arun Rajappa
language: en
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://appapappa.com
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link: true # Open external links in new tab
filename_case: 0
render_drafts: false
post_asset_folder: true
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  tab_replace:

# Category & Tag
default_category: journal
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: landscape
```

## Themes : Install & Configure
Working with themes is easy in Hexo, so this is what I did next: I looked at the themes available for Hexo, and decided to get the Hueman theme which looked good:
```
$ git clone https://github.com/ppoffice/hexo-theme-hueman.git themes/hueman
```
I then had to make a few changes to configure this, firstly in the \_config.yml in the root directory, I changed the theme from landscape to hueman:
```
theme: hueman
```

I also read up the documentation about Hueman and configured it like so, by modifying the \_config.yml under the themes/hueman directory:
```
# Logo Url
# Please enter the absolute path to your logo file
# or remove the following line with replacing logo-header.png with your own logo
# logo:
# Header
menu:
  Home: /
  # Delete this row if you don't want categories in your header nav bar
  Categories:
  About: /about/index.html

# Article list grouped by year
groupByYear: true

# Content
fancybox: true

# Thumbnail
thumbnail: false

# Scroll Loading
scrollLoading: true

# Sidebar
social_links:
  twitter: http://twitter.com/appa
  github: https://github.com/arunr
  rss: atom.xml
widgets:
- recent_posts
- category
- archive
- links

# Links
links:
  Twyst: http://twyst.in

# Don't Use Google APIs if you are in google-blocked areas
use_google_apis: false

# Miscellaneous
google_analytics:
favicon: /favicon.png
fb_admins:
fb_app_id:
```
Since many of my posts didn't have thumbnails, I set thumnail to false, I set up the social links correctly, removed the tag and tagcloud widgets that I didn't want, set up the links I wanted and left it at that for the moment.

With my theme configured, it was looking like this now:

![after](https://www.anony.ws/i/2015/05/19/hexo_2.png)

I then created a new post, and edited it with my favourite markdown editor, [Atom.io](http://atom.io):
```
$ hexo new blog_ready
```

When editing my new posts, there's a bit of configuration at the top of each post that allows Hexo to give it a title, tags, categories etc. That's this section:

````
title: "Getting started with Hexo"
date: 2015-05-19 20:12:56
tags:
categories:
  - tech
---
```

And below that is just beautiful, simple content in Markdown. Now it was time to publish my awesome blog...

## Publishing to GitHub & setting up GoDaddy

Publishing to GitHub is fairly painless. There is some initial set up to do on GitHub, which is captured well [here](https://pages.github.com/). All you need to do though is just the first step: to create a new repo on GitHub called _username_.github.io.

After that, install the Git Deployer plugin:
```
$ npm install hexo-deployer-git --save
```

After that, you need to change your \_config.yml file in the root directory of your blog like this:

```
deploy:
  type: git
  repo: https://github.com/_username_/<username>.github.io
```

Now, you should be all set to deploy! Run
```
$ hexo deploy
```

And then visit http://_username_.github.io to see your blog show up (if everything goes well!).

To configure your own domain, things couldn't be simpler:
1. Go to GoDaddy (or your domain provider) and add an A Record for the following IP address in your domain management:
  - 192.30.252.153
  - 192.30.252.154

2. In your GitHub repo (_username_.github.io), create a file called CNAME that just has the name of your domain (appapappa.com).

That's it - after this visit http://domainname.com and you'll see your blog up!

## Migrating content from WordPress

The next step was to get over the content from my existing Wordpress blog. This was very painless too. First, I had to install the Wordpress Migrator plugin

```
$ npm install hexo-migrator-wordpress --save
```

Then, I went into my WordPress admin panel and exported all my content. After that, it was easy-peasy:

```
$ hexo migrate wordpress ~/Downloads/appapappa.xml
```

With that done, I could see all my posts migrated into the _posts folder of Hexo (under source). I visited http://localhost:4000 and checked that all my WordPress content was there - cool!

## Tag plugins
When checking my WordPress migrated content, I noticed that some of my posts didn't show up correctly - esepecially the ones with references to YouTube or [Gists](https://gist.github.com/) embedded in them. This required fixing up, using what Hexo calls "Tag plugins", but it couldn't have been easier:

1. For YouTube: just edit your migrated WordPress post, and put in the fragment below to handle showing videos from YouTube.
```
{% youtube video_id %}
```
2. For Gists: edit your migrated WordPress post, and put in this fragment to embed the Gist.
```
{% gist gist_id %}
```

Hexo has a number of other tag plugins, all listed [here](https://hexo.io/docs/tag-plugins.html)

## Configuring a few other things...

This were looking sweet now - I had my theme figured out, had written a post, deployed to GitHub and my own domain, migrated my WordPress content and even fixed up issues with them. What could be left? Well there were a number of things, lets look at each of them:

1. **Comments**: At this time, I noticed that I didn't have comments on my blog. Now, what is a blog without comments? Boring, that's what! The way Hexo fixes this up is by integrating [Disqus](https://disqus.com/) into your blog. To do this, you will need to sign-up for Disqus, and then once you have your Disqus ID, add this to your \_config.yml file:

```
disqus_shortname: <your shortname>
```

That's it - you'll have comments enabled on your posts now!


2. **RSS**: I also wanted for my blog to show up as an Atom/RSS feed. For this, I needed to do three things. Firstly, I had to install the RSS plugin.
```
$ npm install hexo-generator-feed --save
```

I then had to update the \_config.yml file in the root directory with this:
```
feed:
  type: atom
  path: atom.xml
  limit: 20
```

I then had to update the \_config.yml file in the Hueman theme directory, so I could link to the RSS feed:
```
social_links:
  rss: atom.xml
```

3. **Search**: For this, I had to do two things - sign-up for [Google Webmaster Tools](https://www.google.com/webmasters/tools/), and then submit the sitemap.xml. To create the sitemap.xml, this is what I did:
```
$ npm install hexo-generator-sitemap --save
```
Once that's done, re-generate your blog which will create the sitemap, and submit the sitemap.xml to Google, in the Webmaster Tools UI.
```
$ hexo generate
```

4. Analytics: This was very simple, you just need to sign-up for [Google Analytics](http://www.google.com/analytics/), and once you have a tracking ID, update your blog \_config.yml with this information:
```
google_analytics: <your tracking ID>
```

All set now - comments, search, analytics and RSS all set up!

## Write-Publish workflow

Whew, the initial set-up took some time, but now my workflow is really simple:

1. Create a new post
```
$ hexo new <postname>
```

2. Write the post using my favourite editor, Atom.IO.

3. Deploy to my blog after verifying locally:
```
$ hexo deploy
```

And that's it!


## Closing thoughts

I'm really liking Hexo, and haven't found anything wanting in it so far. I can write posts in Markdown, with code blogs, and deploy to my domain very easily.

The only thing I may want is more variety of themes - but the nice thing is that I could imagine me being able to do this myself.

My verdict: Hexo is a fantastic platform for developers, and if you are writing about programming or technology, definitely give Hexo a spin!

Happy blogging, [@appa](http://www.twitter.com/appa)
