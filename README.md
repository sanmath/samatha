Samatha v0.4
============

#### Copyright David Springate 2013 ([CC BY 3.0](creativecommons.org/licenses/by/3.0))
##### @datajujitsu


Samatha is an R package for quickly building _Github-ready_ static sites in R. It contains a simple, functional-style DSL for rendering HTML, an engine for compilation of static websites as you build them and a development web-server for viewing your sites of line before you deploy. 

*This project is still in active development. Feel free to contact me with any issues/bugs/suggestions*

The Static site engine uses the Samatha DSL to build layout templates which it then combines with content to generate individual pages. templates are written as a nested R expression, with no need for extenal templating systems.
There are two ways to build pages:

1. Pages are written entirely in the Samatha DSL and compiled with a layout file. This is ideal for introductiory pages and index pages.
2. Blog posts are written in .Rmd format, which is then converted to md using [knitr](http://yihui.name/knitr/) and then to html using [markdown](http://cran.r-project.org/web/packages/markdown/index.html). Posts are then rendered within the layout for that post. 

The Samatha engine `samatha()` now functions as expected. It compiles your site and then updates in real time according to the following rules:

* if a layout file is altered
    - The whole site is re-built
        - pages compiled to html
        - posts knitted and then compiled to html
        - rss and tag files generated
* if any page/post source files are newer than their corresponding html or if the html doesn't exist:
    - Pages in question are knitted and/or re-compiled
    - rss and tag files re-generated
* Any html files without a corresponding source are deleted

Extra features:

* simple wrapper functions for including snippet files containing md or html/js (e.g. for external comments site code and analytics)
* You can include tags for posts in the first line of a post .Rmd file by starting the line with `%`. All words on the rest of the line are coerced to tags and included in the RSS file.
* Automatically generates an RSS file at the top level of your site with global paths and per item tags, content and full links to images etc. Tags/categroies for the whole site can be set in the template/config/config.R file.  This is the format required by [Rbloggers](www.rbloggers.com) for blog submission.
* Helper functions for building lists of tags and lists of posts

Sites are created with the following structure:

* __basename__
    - __template__ the source for your site
        - __layouts__ layout templates for pages and posts
        - __config__ contains config.R file for rss, tags, post layoutss and figure path
        - __pages__ Content of pages built with the Samatha dsl
        - __posts__ Rmd files of blog posts
        - __resources__ html/js/md snippets
    - __basename__ the compiled site.  Copy the contents to a git repo to have a functioning site
        - __css__ Put your css files (e.g. from twitter bootstrap) here
        - __img__ plots from knitted Rmd are automatically placed here
        - __pages__ html for site pages
        - __posts__
        - __tags__

## Examples

My [personal blog](http://daspringate.github.io) was built using Samatha, [twitter bootstrap](http://twitter.github.io/bootstrap/) and [Github pages](http://pages.github.com/). I used the [Readable](http://bootswatch.com/readable/) theme. See [here](https://github.com/DASpringate/blog) for the file structure of a Samatha site.

## Install

You should be able to install the current version of Samatha with devtools:


```r
# check install_github()
require(devtools)
load_all(".")  # In the correct directory!
```

```
## Loading samatha
```


## Documentation

_I'm still working on it!_

* [Wiki](https://github.com/DASpringate/samatha/wiki/_pages)
* [API docs](https://github.com/DASpringate/samatha/tree/master/man)

## Glaring ommisions (To be fixed very soon):

* Automatic creation of config files and example default templates.  For now, check my [site structure](https://github.com/DASpringate/blog) for setup details.



