---
author: Vashishtha Jogi
categories:
  - Programming
date: 2018-04-15T14:08:55-07:00
description: >-
  I recently moved my blog to Hugo. After going through a few how-tos, posts about where to host it, etc. I have the final result. This [Hugo](https://gohugo.io/) blog is based on the [Atlas, Hugo Boilerplate](https://github.com/indigotree/atlas) modified to fit my needs. Here are some notes that I took along the way.
draft: false
slug: moving-to-hugo
tags:
  - programming
  - hugo
  - netlify
title: "Moving to Hugo"
---

I have picked up blogging again. I keep telling myself that I will keep blogging this time. Not sure how long it will last, but here goes the first post after a long time. Recently I moved my blog to Hugo. After going through a few how-tos, posts about where to host it, etc. I have the final result. Here are some notes that I took along the way.

Before stumbling upon [Hugo](https://gohugo.io) I took a look at numerous other solutions. The good old Wordpress, Tumblr, Micro.blog, Ghost, Squarespace and Jekyll. Each one of those has their shortcomings. Some of them are expensive to host ($20/month for Ghost, $12/month for Squarespace), some of those are not so expensive ($4/month for Wordpress). Some of those give you a little control over design by the way of templates, some of them give you complete control (Hugo and Jekyll). I love static websites for their speed. Squarespace and Ghost are nice but they are bloated and are expensive with very little control over.

Here are the requirements I had for this blog:

* Static website
* Cheap hosting
* Clean design with full conrol
* No commenting support
* Static syntax highlighting
* SSL support for hosting
* [SCSS](https://sass-lang.com) support

Jekyll satisfies almost all of the above requirements but it requires Ruby. I am not a huge fan of Ruby (I have been bitten in the past, details of which warrant another post). Hugo seemed like a very good option.

For hosting, I wanted something that required zero maintenance. That meant and VPC solution was a non starter. S3 is great for static websites but for something like a blog I would have to keep updating the bucket all the time, including fixing typos and such. That's when I stumbled upon [Netlify](https://netlify.com). Netlify is great. I was able to get my blog running in a matter of minutes. It has some great features:

* Easy setup
* Support for easy deploy from a Github repo
* Support for custom domains with SSL (they use Lets Encrypt)
* Support for preview builds via PRs

The best part. Netlify has a 100% free personal plan that has all of the above features. My workflow now is simple - Write a post, push to github, Netlify deploys it in less than a minute. 

## Additions

This [Hugo](https://gohugo.io/) blog is based on the [Atlas, Hugo Boilerplate](https://github.com/indigotree/atlas). I have modified it to fit my needs.

* Use [normalize.css](https://github.com/necolas/normalize.css) and a modified version of [Skeleton](https://github.com/dhg/Skeleton/)
* Minify CSS action added to the `styles.html` that minifies and concatenates all the CSS files into one `site.css` file
* Use Hugo's inbuilt syntax highlighting with Xcode syntax style
* Added pagination for posts with 10 posts/page by default
* Remove Netlify CMS
* Zero Javascript usage
* Use YAML for `config`
* Added an [Archive](https://jogi.blog/archive/) page inspired from [David Tran](https://davidtranscend.com/blog/how-to-create-an-archives-page-with-hugo/)
* Added [JSON Feed](https://jsonfeed.org) generation in addition to XML RSS Feed
* Added [Twitter Card](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started) support

### Layout Modifications

The layout is loosely based on [Fatih Arslan's blog](https://arslan.io), [Attila Ghost theme](https://github.com/zutrinken/attila) and styles from my other [photography](https://jogi.photos) website. The goal that I set out with was to have a very clean design.

* The main page consists of a blog header that only shows up on the home page
* Rest all pages have a mini nav bar with the blog title
* Pagination with links to Older and Newer Posts along with the page number context
* Single post page has the date and a link to the category(s) the post is in
* Show tags at the bottom of the single post page controlled by `displayPostTags` in `config.yaml`
* Footer with links to XML RSS, JSON Feed and Archive page

### Available Commands

There are 3 commands available:

* `npm run build` - Builds assets (sass, js, fonts, images) and runs `hugo`
* `npm run build:preview` - The same as `build`, but runs `hugo --buildDrafts --buildFuture`
* `npm run server` - Runs BrowserSync and watches for changes, running `build` when changes are detected

Before you can run this, make sure you run `npm install` to install the dependencies.


## File Structure

```
│
└──── /layouts                         - Template files
│   │ 404.html                         - 404 Template
│   │ index.json                       - JSON Feed conforming template
│   │ index.headers                    - Custom Netlify HTTP headers
│   │ index.redirects                  - Custom Netlify redirect rules
│   │ robots.txt                       - Template for robots.txt
│   │
│   └──── /_default                    - Base templates for list & singular pages
│   │   │ baseof.html                  - Base template
│   │   │ list.html                    - List/taxonomy template
│   │   │ single.html                  - Singular page/post template
│   │
│   └──── /partials                    - Partials
│       │
│       └──── /site                    - Site partials loaded into _default/baseof.html template
│           │ meta.html                - Site <meta> tags
│           │ nav.html                 - Top nav that shows up on non home pages
│           │ blog-header.html         - Site header that shows up on the home page
│           │ post-summary.html        - Summary of a post shown on the home page
│           │ pagination.html          - Pagination links
│           │ footer.html              - Sites primary <footer>
│           │ twitter-card.html        - Twitter card meta tags
│           │ scripts.html             - JavaScript <script> referenced before closing </body>
│           │ styles.html              - Stylesheets referenced before closing </head>
│   │
|   └──── /src                         - Source files for assets (SASS, JS, Images, Fonts etc)
│   │
│   └──── /static                      - Hugo static resources
│
│ .gitignore
│ .sass-lint.yml                       - Linting rules for sass-lint
│ LICENSE
│ README.md
│ config.yaml                          - Hugo configuration
│ netlify.toml                         - Netlify configuration
│ package.json
```

## What's Next
My todo list right now:

* Add support for related posts
* Better image support (wider, @2x images)

If you have any questions/feedback feel free to hit me up on Twitter: [@VashishthaJogi](https://twitter.com/VashishthaJogi).