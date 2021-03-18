# Blog

This [Hugo](https://gohugo.io/) blog is based on the [Atlas, Hugo Boilerplate](https://github.com/indigotree/atlas). It has been modified to fit my needs.

**Disclaimer** - This boilerplate has been integrated with [Netlify](https://www.netlify.com/), and therefore many features are specific to the Netlify platform and may not work with other hosting providers.

**Disclaimer** - Atlas is a boilerplate (starter kit) for bespoke Hugo projects. It's not a Hugo theme and cannot be placed inside the `/themes` directory. Check the [theme](#themes) docs for more information.

## Features

Atlas provides the following features out of the box:

* Environment driven `robots.txt` file (disallows robots on everything other than production)
* Base HTML templates with easy customisation/extension
* [Configuration](/netlify.toml) for Netlify deployments
* [Better defaults](#security-headers) for configuring HTTPS
* [Better redirects](#redirects) with Netlify instead of `<meta http-equiv="refresh">`

For more information on these features go to the [Atlas](https://github.com/indigotree/atlas) repo.

## Additions

A few modifications have been done to the base Atlas boilerplate code to fit my needs.

* Use [normalize.css](https://github.com/necolas/normalize.css) and a modified version of [Skeleton](https://github.com/dhg/Skeleton/)
* Minify CSS action added to the `styles.html` that minifies and concatinates all the CSS files into one `site.css` file
* Use Hugo's inbuilt syntax highlighting with Xcode syntax style
* Added pagination for posts with 10 posts/page by default
* Remove Netlify CMS
* No other javascript except Google Analytics
* Use YAML all around (TOML is nice but I like YAML)
* Added an [Archive](https://jogi.blog/archive/) page inspired from [David Tran](https://davidtranscend.com/blog/how-to-create-an-archives-page-with-hugo/)
* Added [JSON Feed](https://jsonfeed.org) generation in addition to XML RSS Feed
* Added [Twitter Card](https://developer.twitter.com/en/docs/tweets/optimize-with-cards/guides/getting-started) support

### Layout Modifications

The layout is loosely based on [Attila Ghost theme](https://github.com/zutrinken/attila) and styles from my other [photography](https://jogi.photos) website.

* The main page consists of a blog header that only shows up on the home page
* Rest all pages have a mini nav bar with the blog title
* Pagination with links to Older and Newer Posts along with the page number context
* Single post page has the date and a link to the category(s) the post is in
* Show tags at the bottom of the single post page controlled by `displayPostTags` in `config.yaml`
* Footer with links to XML RSS, JSON Feed and Archive page

## Prerequisite

This starter project does not include a copy of the `hugo` binary. You will need to [install Hugo](https://gohugo.io/getting-started/installing/) first you can run any of the [commands](#available-commands) mentioned below.

## Getting Started

To get started, you can either clone the repository, or deploy straight to [Netlify](#deploy-to-netlify). Then run the following from the project root:

```
npm install
npm run server
```

### Available Commands

There are 3 commands available:

* `npm run build` - Builds assets (sass, js, fonts, images) and runs `hugo`
* `npm run build:preview` - The same as `build`, but runs `hugo --buildDrafts --buildFuture`
* `npm run server` - Runs BrowserSync and watches for changes, running `build` when changes are detected


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
│           │ pagination.html          - Pagination links
│           │ post-summary.html        - Post summary shown on the home page
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

## Deploy to Netlify

You can deploy directly to Netlify using this button:

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/jogi/jogi.blog)

## License

MIT © [Vashishtha Jogi](https://jogi.blog)
