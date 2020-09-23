---
title: "index"
author: "Petr Bouchal"
output: html_document
---




```r
thisdir <- knitr::current_input(dir = TRUE)
thisdir <- here::here("public/slides")
dirs <- list.dirs(dirname(thisdir), recursive = F)

thisdir <- here::here("public/slides")
dirs <- list.dirs(thisdir, recursive = F)
```


```r
thisdir
```

```
## [1] "/Users/petr/github/petrbouchal.github.io/public/slides"
```

```r
dirs
```

```
## [1] "/Users/petr/github/petrbouchal.github.io/public/slides/pssau2020-07"
```

```r
rmds <- paste0(dirs, "/index.Rmd")
rmds
```

```
## [1] "/Users/petr/github/petrbouchal.github.io/public/slides/pssau2020-07/index.Rmd"
```


```r
dir_link <- function(rmd) {
  yml <- rmarkdown::yaml_front_matter(rmd)
  yml
  # ttl <- yml$title
  # sbttl <- yml$subtitle
  # dt <- yml$date
  # 
  # html_url <- stringr::str_replace(rmd, ".Rmd$", ".html")
  # 
  # a_text <- a(ttl, href = html_url)
  # next_text <- if(!is.null(sbttl)) stringr::str_glue(" - {sbttl}") else ""
  # date_text <- if(!is.null(dt)) stringr::str_glue(" ({dt})") else ""
  # 
  # outpt <- paste(a_text, next_text, date_text)
  # 
  # return(outpt)
}
```


```r
purrr::map(rmds, dir_link)
```

[[1]]
[[1]]$title
[1] "Jak se dostat k českým otevřeným datům"

[[1]]$subtitle
[1] "a využít je v reprodukovatelném výzkumu"

[[1]]$author
[1] "Petr Bouchal"

[[1]]$date
[1] "pro PSSAÚ `r ptrr::format_date_human(as.Date('2020-07-03'))` [neprezentováno]"

[[1]]$output
[[1]]$output$`xaringan::moon_reader`
[[1]]$output$`xaringan::moon_reader`$css
[1] "xaringan-themer.css"

[[1]]$output$`xaringan::moon_reader`$lib_dir
[1] "libs"

[[1]]$output$`xaringan::moon_reader`$yolo
[1] FALSE

[[1]]$output$`xaringan::moon_reader`$nature
[[1]]$output$`xaringan::moon_reader`$nature$ratio
[1] "16:9"

[[1]]$output$`xaringan::moon_reader`$nature$highlightStyle
[1] "github"

[[1]]$output$`xaringan::moon_reader`$nature$highlightLines
[1] TRUE

[[1]]$output$`xaringan::moon_reader`$nature$countIncrementalSlides
[1] FALSE

[[1]]$output$`xaringan::moon_reader`$nature$titleSlideClass
[1] "bottom"  "left"    "inverse"

