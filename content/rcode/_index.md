---
date: "2021-06-01T21:43:05+02:00"
title: "R Project Principles"
authors: []
categories:
  -
tags:
  -
draft: false
---

This is a set of standards, design choices and technology choices I like to keep consistent across projects I work on. I don't always succeed in sticking to the ambitions around e.g. reproducibility and style, but I try to keep improving.

These are also standards that I hope will make collaboration easier.

# Project structure and organisation

- everything needed to run the project should be contained in one directory.
- all paths should begin at the `/` root of the project directory
- use RStudio projects if you use RStudio
- if there are more than a handful of scripts, they should be in a subdirectly named e.g. `code`, `src`, or, ideally, `R`. If there is code in other languages, it should live in subdirectories named for each language
- scripts that need to be run in order should be numbered in their names
- use machine readable file names [a la this guide](http://www2.stat.duke.edu/~rcs46/lectures_2015/01-markdown-git/slides/naming-slides/naming-slides.pdf)
  - `01_load_excel-file.R`: underscores separate parts of names, dashes separate word breaks within parts of names
  - no spaces in names
  - only ASCII in file names
  - numbering and file name structure should play well with default ordering
  - dates should be e.g. 2021-02-28
  - versioning should be done mostly by git, not file names
- one project, on git/Github repository
- I tend to use `data-input`, `data-output`, `data-processed` and `data-export` directories for data. The exact names don't matter, but the point is that input data != output data != intermediate data storage.
- `docs` is a sensible name for the directory containing rendered HTML documentation to be published via Github pages

# Tools

- prefer `{tidyverse}` tools to base R (within reason)
- prefer `{ggplot2}` to other graphics systems
- for accessing data from the Czech Statistical Office, check if the data is available in open format and use the `{czso}` package if possible (on CRAN)
- ditto for public finance data (Státní pokladna, package {statnipokladna} on CRAN)
- `{pointblank}` is my preferred data validation package which I recommend
- `{arrow}` is now mature enough that it should be the default format for storing intermediate data and exporting for other code-based users - mainly because of speed and efficiency of storage and access (esp. partintioned Arrow datasets).
- if using Czech spatial data, check out `{CzechData}` from @JanCaha and `{RCzechia}` on CRAN.
- for OECD data, there is `{oecd}`, for Eurostat there is `{eurostat}`, and for World Bank data there is `{wbstats}`.
- for EU spatial data (NUTS regions etc.), there is [`{giscoR}`](https://dieghernan.github.io/giscoR/) but beware the licensing conditions on the underlying data

# Reports and other outputs

- if the project results in a report, write it in Rmarkdown, with git playing the role of tracked changes
- {redoc} may be useful for gathering external feedback through Word documents
- [hypothes.is](https://web.hypothes.is/) is a good, easy way to gather feedback on web-facing content; it may even be worth generating a HTML page of a draft report just for getting feedback
- use the built-in citation system; can easily be linked to Zotero via the Better BibTex Zotero Plugin (or nowadays perhaps even without it); CSL-JSON may well be the most sensible format for storing citation data
- in (R)markdown, when using git for version control it's nice to put each sentence on its own line (just one line break, so in the rendered Docx or PDF it stays as one paragraph = ["Semantic Line Breaks"](https://sembr.org/))

# Workflow

- use git and Github for version control
- use {targets} if the project contains more than a single script and a single data source - this is fast becoming the gold standard for efficient pipeline/workflow orchestration in R
- it does not make a whole lot of sense to me to develop analysis projects into packages - for many of the reasons mentioned by [Miles McBain](https://www.milesmcbain.com/posts/an-okay-idea/).
- Github issues are quite good for tracking bunches of work to be done and storing information which will be needed to make progress
- only commit outputs to git at reasonable key points
- {pointblank} and {convo} (once/if the latte matures) may be good for codifying and validating outputs
- for simple input parameters (paths, numbers, dates), using {config} helps to keep them in one place (config.yml)


# Documentation

- `README.md` in every directory, describing the files in that directory
- the top-level README or a document like `rev.md` or some such should describe how to reproduce the work, but more importantly it should give a good overview of the project
- comments in code
- it may make sense to document the whole project in a set of (R)md files, including some which showcase the outputs or even create the main report, and which together form an Rmarkdown website
- there are a few rough templats in my personal package `[{ptrr}](https://github.com/petrbouchal/ptrr)` - xaringan/remark slides, Rmarkdown website, basic one-page Rmd/HTML documentation

# Reproducibility

- see above on {targets} - highly recommend to put in the work to make the workflow clear and efficient and thus easy to tweak without having to re-run everything or having to dig into where a particular object is used.
- esp. for {targets}-based pipelines, it may be helpful to put all file paths, time periods and other inputs which you expect to change over time (e.g. when in the future the pipeline is rerun with update data) into a `config.yml` file and pass the config values to the pipeline via the {config} package. The main benefit is that all the settings are in one place and one does not need to hunt for them in the depth of the code itself.
- use {renv} religiously to track exact versions of the packages on which the project depends.
- [don's use `rm(list = ls())`](https://www.tidyverse.org/blog/2017/12/workflow-vs-script/)
- ditto for `setwd()` - if it is necessary, something is wrong with the project structure
- use `{here}` for paths
- there should be a simple way to run the whole workflow from start to finish, perhaps via {targets} or a build script.
- (as I've found out the hard way), an Rmarkdown website where all work is done across multiple Rmarkdown scripts is not a sustainable framework for reproducibility. Much better to use Rmarkdown to weave artifacts (models, visuals, numbers) generated in a proper workflow in R scripts.

# Style

- snake case object/variable names
- snake-case column names in data frames, with no spaces and diacritics (`janitor::clean_names()` is great for this)
- if in doubt, use spaces between things
- all package loading to be done at the top of the script
- use whitespace and code sections (Ctrl+R in Rstudio)
- prefer `{purrr}` map-type functions to loops and `*apply()` functions
- if you do the same thing more than twice, write a function
- git commits should be in the form "do something"; ideally each commit should contain an increment of work such that the whole project will run when checked out at that commit

# Visuals

- do the hard work to make the chart/table easy to use for the reader
- prefer direct labels to legends
- `{ggforce}` contains great helpers for annotation
- `{ggiraph}` is nice for basic interactivity on web pages
- `{gt}` seems to be the most sensible table formatting tool nowadays
