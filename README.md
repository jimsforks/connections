
<!-- README.md is generated from README.Rmd. Please edit that file -->

# connections

<!-- badges: start -->

[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
[![Travis build
status](https://travis-ci.com/edgararuiz/connections.svg?branch=master)](https://travis-ci.com/edgararuiz/connections)
[![Codecov test
coverage](https://codecov.io/gh/edgararuiz/connections/branch/master/graph/badge.svg)](https://codecov.io/gh/edgararuiz/connections?branch=master)
<!-- badges: end -->

Provides a generic implementation of the [RStudio Connection
Contract](https://rstudio.github.io/rstudio-extensions/connections-contract.html)
to make it easier for database connections, and other type of
connections, opened via R packages to take advantage of the Connections
Pane inside the RStudio IDE.

## Installation

Install the development version from [GitHub](https://github.com/) with:

``` r
# install.packages("remotes")
remotes::install_github("edgararuiz/connections")
```

## Usage

### Basic

``` r
library(connections)
library(RSQLite)
library(DBI)

con <- connection_open(SQLite(), path = ":dbname")
```

<img src = "man/figures/sqlite-1.png" width = "400px"> <br/>

``` r
dbWriteTable(con, "db_mtcars", mtcars)
```

<img src = "man/figures/sqlite-2.png" width = "400px"> <br/>

Preview button works as expected

<img src = "man/figures/sqlite-3.png" width = "600px"> <br/>

``` r
connection_close(con)
```

<img src = "man/figures/sqlite-4.png" width = "400px"> <br/>

### Not integrated

``` r
con <- dbConnect(SQLite(), path = ":dbname")
```

``` r
connection_view(con)
```

<img src = "man/figures/sqlite-5.png" width = "400px"> <br/>

``` r
dbWriteTable(con, "db_mtcars", mtcars)
```

``` r
connection_update(con)
```

<img src = "man/figures/sqlite-6.png" width = "400px"> <br/>

``` r
connection_close(con)
```

<img src = "man/figures/sqlite-7.png" width = "400px"> <br/>

### Customize names

``` r
con <- dbConnect(SQLite(), path = ":dbname")
```

``` r
connection_view(
  con, 
  host = "my_host", 
  name = "my_name",
  connection_code = "library(connections)\ndbConnect(...)"
  )
```

<img src = "man/figures/sqlite-8.png" width = "400px"> <br/>

Connection code is sourced from `connection_code`

<img src = "man/figures/sqlite-9.png" width = "400px"> <br/>

## `DBI` packages examples

### `bigrquery`

``` r
library(DBI)
library(bigrquery)

con <- dbConnect(
  bigquery(),
  project = "bigquery-public-data",
  dataset = "austin_311",
  billing = "rstudio-bigquery-event",
  use_legacy_sql = FALSE
)
```

``` r
connection_view(con)
```
