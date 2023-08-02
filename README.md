
<!-- README.md is generated from README.Rmd. Please edit that file -->

# certificate

<!-- badges: start -->

[![R-CMD-check](https://github.com/forwards/certificate/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/forwards/certificate/actions/workflows/R-CMD-check.yaml)
[![Codecov test
coverage](https://codecov.io/gh/forwards/certificate/branch/main/graph/badge.svg)](https://app.codecov.io/gh/forwards/certificate?branch=main)
<!-- badges: end -->

The **certificate** package is designed to help generate certificates
for R courses.

## Installation

This package is not on CRAN. You can install the package from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("forwards/certificate")
```

## Example

First load the package

``` r
library(certificate)
```

Certificates can be generate for multiple participants at once. Here we
specify a couple of fake names for illustration (generated with
`charlatan::ch_name`):

``` r
attendees <- c("Marnie Dickinson", "Dr. Marlin Wilderman")
```

Then we specify the basic metadata of the workshop, which will be the
same for all certificates

``` r
workshop <- "Package development workshop"
date <- as.Date("2023-07-01")
location <- "R-Ladies Natal"
```

The curriculum is a summary of the workshop contents. This should be
specified in markdown format and it is easier to write this in a
separate markdown file. An example is included in the **certificate**
package.

``` r
curriculum <- system.file("rmarkdown", "templates",
                          "workshop_certificate", "resources",
                          "default_workshop_contents.md", 
                          package = "certificate")
readLines(curriculum)
#> [1] "- Making code into an R package"    ""                                  
#> [3] "- Collaborative coding with GitHub" ""                                  
#> [5] "- Writing a vignette or an article" ""                                  
#> [7] "- Building a package webpage"       ""                                  
#> [9] "- Submitting a package to CRAN"
```

The last set of required information is about the certifying person and
the certifying organization

``` r
certifier <- "Jeanne Raquel de Andrade Franco"
credentials <- "Coorganizadora"
organization <- "R-Ladies Global"
organization_url <- "forwards.github.io/"
```

Now we can generate the certificates in a new directory, e.g.

``` r
dir <- "C:/Users/jeann/Documents/R-Ladies Natal/certificados_rladies_natal"
create_workshop_certificates(attendees, workshop, date, location,
                             curriculum, certifier, credentials,
                             organization, organization_url,
                             dir)
#> 
#> 
#> processing file: skeleton.Rmd
#>   |                                                           |                                                   |   0%  |                                                           |...                                                |   6%                     |                                                           |......                                             |  12% [setup]             |                                                           |.........                                          |  18%                     |                                                           |............                                       |  24% [attendee]          |                                                           |...............                                    |  29%                     |                                                           |..................                                 |  35% [action_text]       |                                                           |.....................                              |  41%                     |                                                           |........................                           |  47% [workshop]          |                                                           |...........................                        |  53%                     |                                                           |..............................                     |  59% [location]          |                                                           |.................................                  |  65%                     |                                                           |....................................               |  71% [curriculum_title]  |                                                           |.......................................            |  76%                     |                                                           |..........................................         |  82% [curriculum]        |                                                           |.............................................      |  88%                     |                                                           |................................................   |  94% [signature]         |                                                           |...................................................| 100%                   
#> output file: skeleton.knit.md
#> "C:/Users/jeann/AppData/Local/Pandoc/pandoc" +RTS -K512m -RTS skeleton.knit.md --to latex --from markdown+autolink_bare_uris+tex_math_single_backslash --output pandoc25f879a17a4a.tex --lua-filter "C:\Users\jeann\AppData\Local\R\win-library\4.3\rmarkdown\rmarkdown\lua\pagebreak.lua" --lua-filter "C:\Users\jeann\AppData\Local\R\win-library\4.3\rmarkdown\rmarkdown\lua\latex-div.lua" --embed-resources --standalone --template template.tex --highlight-style tango --pdf-engine xelatex
#> 
#> Output created: package_development_workshop_2023-07-01_marnie_dickinson.pdf
#> 
#> 
#> processing file: skeleton.Rmd
#>   |                                                           |                                                   |   0%  |                                                           |...                                                |   6%                     |                                                           |......                                             |  12% [setup]             |                                                           |.........                                          |  18%                     |                                                           |............                                       |  24% [attendee]          |                                                           |...............                                    |  29%                     |                                                           |..................                                 |  35% [action_text]       |                                                           |.....................                              |  41%                     |                                                           |........................                           |  47% [workshop]          |                                                           |...........................                        |  53%                     |                                                           |..............................                     |  59% [location]          |                                                           |.................................                  |  65%                     |                                                           |....................................               |  71% [curriculum_title]  |                                                           |.......................................            |  76%                     |                                                           |..........................................         |  82% [curriculum]        |                                                           |.............................................      |  88%                     |                                                           |................................................   |  94% [signature]         |                                                           |...................................................| 100%                   
#> output file: skeleton.knit.md
#> "C:/Users/jeann/AppData/Local/Pandoc/pandoc" +RTS -K512m -RTS skeleton.knit.md --to latex --from markdown+autolink_bare_uris+tex_math_single_backslash --output pandoc25f837075bad.tex --lua-filter "C:\Users\jeann\AppData\Local\R\win-library\4.3\rmarkdown\rmarkdown\lua\pagebreak.lua" --lua-filter "C:\Users\jeann\AppData\Local\R\win-library\4.3\rmarkdown\rmarkdown\lua\latex-div.lua" --embed-resources --standalone --template template.tex --highlight-style tango --pdf-engine xelatex
#> 
#> Output created: package_development_workshop_2023-07-01_dr_marlin_wilderman.pdf
```

See `?create_workshop_certificate` for more detail on the arguments of
this function, which allow customization of the wording, logo and
colours, as well as the option to supply an image of a signature to
place on the signature line.
