---
author: Vashishtha Jogi
categories:
  - Programming
date: 2025-12-05T14:08:55-07:00
description: >-
  I recently moved my blog to Hugo. After exploring different options for hosting, I settled on GitHub Pages with automated deployment. This [Hugo](https://gohugo.io/) blog is based on the [Atlas, Hugo Boilerplate](https://github.com/indigotree/atlas). Here are some notes from the process.
draft: false
slug: moving-to-hugo
tags:
  - programming
  - hugo
  - github-pages
title: "Moving to Hugo"
---

I've picked up blogging again. I keep telling myself that I'll keep at it this time. Not sure how long it will last, but here goes the first post after a long time. Recently I moved my blog to Hugo. After exploring different static site generators and hosting options, I landed on Hugo with GitHub Pages. Here are some notes from the process.

Before stumbling upon [Hugo](https://gohugo.io), I took a look at numerous other solutions: the good old WordPress, Tumblr, Micro.blog, Ghost, Squarespace, and Jekyll. Each one has its shortcomings. Some are expensive to host ($20/month for Ghost, $12/month for Squarespace), while others are more affordable ($4/month for WordPress). Some give you limited control over design through templates, while others give you complete control (Hugo and Jekyll). I love static websites for their speed. Squarespace and Ghost are nice, but they're bloated and expensive with limited customization options.

Here are the requirements I had for this blog:

* Static website
* Cheap hosting
* Clean design with full control
* No commenting support
* Static syntax highlighting
* SSL support
* [SCSS](https://sass-lang.com) support

Jekyll satisfies almost all of these requirements, but it requires Ruby. I'm not particularly fond of Ruby (I've been bitten in the past—details of which warrant another post). Hugo seemed like a good alternative.

For hosting, I wanted something with minimal maintenance. VPS solutions felt like overkill. S3 is great for static websites but would require manual updates for every change. That's when I discovered [GitHub Pages](https://pages.github.com/). It turned out to be a good fit:

* Simple setup
* Automatic deployment from a GitHub repo
* Support for custom domains with SSL
* Free hosting for public repositories
* GitHub Actions for automated builds

My workflow is straightforward: write a post, push to GitHub, and GitHub Actions builds and deploys it automatically. 

## Customizations

This [Hugo](https://gohugo.io/) blog is based on the [Atlas, Hugo Boilerplate](https://github.com/indigotree/atlas). I made some adjustments along the way:

* Uses [normalize.css](https://github.com/necolas/normalize.css) and a modified version of [Skeleton](https://github.com/dhg/Skeleton/)
* CSS minification in `styles.html` that concatenates all CSS files into one `site.css` file
* Hugo's built-in syntax highlighting with Monokai style
* Pagination with 10 posts per page
* Minimal JavaScript (just Google Analytics)
* YAML configuration files
* An [Archive](https://jogi.blog/archive/) page (inspired by [David Tran](https://davidtranscend.com/blog/how-to-create-an-archives-page-with-hugo/))
* [JSON Feed](https://jsonfeed.org) generation alongside XML RSS
* [Twitter Card](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started) support

### Layout

The layout draws inspiration from [Fatih Arslan's blog](https://arslan.io), [Attila Ghost theme](https://github.com/zutrinken/attila), and my [photography](https://jogi.photos) website. I was aiming for a clean, simple design:

* Blog header on the home page
* Minimal nav bar with the blog title on other pages
* Pagination with links to older and newer posts
* Post pages show the date and category links
* Tags at the bottom of posts (controlled by `displayPostTags` in `config.yaml`)
* Footer with links to XML RSS, JSON Feed, and Archive page

### Development

The setup includes a few npm scripts for local development:

* `npm run build` - Builds assets and runs `hugo`
* `npm run build:preview` - Same as `build`, but includes drafts and future posts
* `npm run server` - Starts a local server with live reload

Run `npm install` first to install dependencies.


## File Structure

```
│
└──── /layouts                         - Template files
│   │ 404.html                         - 404 Template
│   │ index.json                       - JSON Feed template
│   │ robots.txt                       - Template for robots.txt
│   │
│   └──── /_default                    - Base templates for list & singular pages
│   │   │ baseof.html                  - Base template
│   │   │ list.html                    - List/taxonomy template
│   │   │ single.html                  - Singular page/post template
│   │
│   └──── /partials                    - Partials
│       │
│       └──── /site                    - Site partials
│           │ meta.html                - Site <meta> tags
│           │ nav.html                 - Top navigation bar
│           │ blog-header.html         - Site header on home page
│           │ post-summary.html        - Post summary on home page
│           │ pagination.html          - Pagination links
│           │ footer.html              - Site footer
│           │ twitter-card.html        - Twitter card meta tags
│           │ scripts.html             - JavaScript scripts
│           │ styles.html              - Stylesheets
│   │
|   └──── /src                         - Source files for assets
│   │
│   └──── /static                      - Hugo static resources
│
└──── /.github/workflows               - GitHub Actions workflows
│   │ hugo.yml                         - Build and deploy workflow
│
│ .gitignore
│ .sass-lint.yml                       - Linting rules for sass-lint
│ LICENSE
│ README.md
│ config/_default/config.yaml          - Hugo configuration
│ package.json
```

## What's Next

Some things I'd like to add:

* Support for related posts
* Better image support (wider images, @2x retina support)

If you have questions or feedback, feel free to reach out on Twitter: [@VashishthaJogi](https://twitter.com/VashishthaJogi).