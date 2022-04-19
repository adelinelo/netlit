
<!-- README.md is generated from README.Rmd. Please edit that file -->

# netlit: Augment a literature review with network analysis statistics

------------------------------------------------------------------------

`netlit` provides functions to generate network statistics from a
literature review. Specifically, it processes a dataset where each row
is a proposed relationship (“edge”) between two concepts or variables
(“nodes”).

To install `netlit` from CRAN, run the following:

``` r
install.packages("netlit")
```

## Basic Usage

The `review()` function takes in a dataframe, `data`, that includes
`from` and `to` columns (a directed graph structure).

In the example below, we use example data from [this project on
redistricting](https://github.com/judgelord/redistricting). These data
are a set of related concepts (`from` and `to`) in the redistricting
literature and citations for these relationships (`cites` and
`cites_empirical`). See `vignette("netlit")` for more details on this
example.

``` r
library(netlit)

data("literature")

head(literature)
```

    #>                               from                               to                                                                               cites              cites_empirical
    #> 1                        computers            detect gerrymandering Altman & McDonald 2010; Wang 2016; Altman & McDonald 2011; Ramachandran & Gold 2018                    Wang 2016
    #> 2                        computers             public participation                                      Altman & McDonald 2010; Altman & McDonald 2011                         <NA>
    #> 3  number of competitive districts preserve communities of interest                                                        Gimpel & Harbridge-Yong 2020 Gimpel & Harbridge-Yong 2020
    #> 4               partisan advantage                  proportionality                                                     Caughey et al. 2017; Tamas 2019                         <NA>
    #> 5          partisan gerrymandering                   efficiency gap                                                                           Chen 2017                    Chen 2017
    #> 6 preserve communities of interest              constitutional test                                                                 Stephanopoulos 2012                         <NA>

`netlit` offers four functions: `make_edgelist()`, `make_nodelist()`,
`augment_nodelist()`, and `review()`.

`review()` is the primary function (and probably the only one you need).
The others are helper functions that perform the individual steps that
`review()` does all at once. `review()` takes in a dataframe with at
least two columns representing linked concepts (e.g., a cause and an
effect) and returns data augmented with network statistics. Users must
either specify “from” nodes and “to” nodes with the `from` and `to`
arguments or include columns named `from` and `to` in the supplied
`data` object.

`review()` returns a list of three objects:

1.  an augmented `edgelist` (a list of relationships with
    `edge_betweenness` calculated),
2.  an augmented `nodelist` (a list of concepts with `degree` and
    `betweenness` calculated), and
3.  a `graph` object suitable for use in other `igraph` functions or
    other network visualization packages.

### Including node attributes

Users may wish to include edge attributes (e.g., information about the
relationship between the two concepts) or node attributes (information
about each concept). We show how to do so below. But first, consider the
basic use of `review()`:

``` r
lit <- review(literature, from = "from", to = "to")

lit
```

    #> A netlit_review object with the following components:
    #> 
    #> $edgelist
    #>  - 69 edges
    #>  - edge attributes: edge_betweenness
    #> $nodelist
    #>  - 56 nodes
    #>  - node attributes: degree_in, degree_out, degree_total, betweenness
    #> $graph
    #>    an igraph object

``` r
head(lit$edgelist)
```

    #>                               from                               to edge_betweenness
    #> 1                        computers            detect gerrymandering              2.0
    #> 2                        computers             public participation              1.0
    #> 3  number of competitive districts preserve communities of interest             86.0
    #> 4               partisan advantage                  proportionality             19.5
    #> 5          partisan gerrymandering                   efficiency gap             13.5
    #> 6 preserve communities of interest              constitutional test              7.0

``` r
head(lit$nodelist)
```

    #>                               node degree_in degree_out degree_total betweenness
    #> 1                        computers         0          2            2         0.0
    #> 2  number of competitive districts         1          2            3        64.0
    #> 3               partisan advantage         6          8           14       111.5
    #> 4          partisan gerrymandering         1          7            8        42.0
    #> 5 preserve communities of interest         2          6            8        79.0
    #> 6      mean-median vote comparison         0          2            2         0.0

Edge and node attributes can be added using the `edge_attributes` and
`node_attributes` arguments.

`edge_attributes` is a vector that identifies columns in the supplied
data frame that the user would like to retain. (To retain all variables
from `literature`, use `edge_attributes = names(literature)`.)

`node_attributes` is a separate dataframe that contains attributes for
each node in the primary data set. `node_attributes` must be a dataframe
with a column `node` with values matching the `to` or `from` columns of
the `data` argument.

The example `node_attributes` data include one column `type` indicating
a type for each each node/variable/concept.

``` r
data("node_attributes")

head(node_attributes)
```

    #>                                node      type
    #> 1      campaign resource allocation    effect
    #> 2                 candidate quality    effect
    #> 3 change in constituency boundaries condition
    #> 4  preserve communities of interest      goal
    #> 5                   competitiveness      goal
    #> 6                         computers condition

``` r
lit <- review(literature,
              edge_attributes = c("cites", "cites_empirical"),
              node_attributes = node_attributes)

lit
```

    #> A netlit_review object with the following components:
    #> 
    #> $edgelist
    #>  - 69 edges
    #>  - edge attributes: cites, cites_empirical, edge_betweenness
    #> $nodelist
    #>  - 56 nodes
    #>  - node attributes: type, degree_in, degree_out, degree_total, betweenness
    #> $graph
    #>    an igraph object

``` r
head(lit$edgelist)
```

    #>                               from                               to                                                                               cites              cites_empirical edge_betweenness
    #> 1                        computers            detect gerrymandering Altman & McDonald 2010; Wang 2016; Altman & McDonald 2011; Ramachandran & Gold 2018                    Wang 2016              2.0
    #> 2                        computers             public participation                                      Altman & McDonald 2010; Altman & McDonald 2011                         <NA>              1.0
    #> 3  number of competitive districts preserve communities of interest                                                        Gimpel & Harbridge-Yong 2020 Gimpel & Harbridge-Yong 2020             86.0
    #> 4               partisan advantage                  proportionality                                                     Caughey et al. 2017; Tamas 2019                         <NA>             19.5
    #> 5          partisan gerrymandering                   efficiency gap                                                                           Chen 2017                    Chen 2017             13.5
    #> 6 preserve communities of interest              constitutional test                                                                 Stephanopoulos 2012                         <NA>              7.0

``` r
head(lit$nodelist)
```

    #>                               node      type degree_in degree_out degree_total betweenness
    #> 1                        computers condition         0          2            2         0.0
    #> 2  number of competitive districts      goal         1          2            3        64.0
    #> 3               partisan advantage      goal         6          8           14       111.5
    #> 4          partisan gerrymandering condition         1          7            8        42.0
    #> 5 preserve communities of interest      goal         2          6            8        79.0
    #> 6      mean-median vote comparison    metric         0          2            2         0.0
