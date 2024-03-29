    library(readr)
    library(dplyr)

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

    url <- "https://tgstewart.cloud/soda.csv"
    class_data <- read_csv(url)

    ## Rows: 70 Columns: 2

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): cola, sugar
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

    class_data

    ## # A tibble: 70 × 2
    ##    cola                     sugar               
    ##    <chr>                    <chr>               
    ##  1 Something else           Regular (full sugar)
    ##  2 Something else           Regular (full sugar)
    ##  3 Something else           Regular (full sugar)
    ##  4 Something else           Regular (full sugar)
    ##  5 <NA>                     <NA>                
    ##  6 Cola (Coke, Pepsi, etc.) Zero sugar or diet  
    ##  7 Something else           Regular (full sugar)
    ##  8 Something else           Zero sugar or diet  
    ##  9 Cola (Coke, Pepsi, etc.) Regular (full sugar)
    ## 10 Something else           Zero sugar or diet  
    ## # ℹ 60 more rows

# 1

    cola_table <- table(class_data$cola)
    cola_table_props <- prop.table(cola_table)
    cola_table_props

    ## 
    ## Cola (Coke, Pepsi, etc.)           Something else 
    ##                0.3030303                0.6969697

<table>
<colgroup>
<col style="width: 49%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Colas</th>
<th>No Colas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>20 (<span class="math inline">$\frac{20}{66} =
0.\bar{30}$</span>)</td>
<td>46 (<span class="math inline">$\frac{46}{66} = 0.\bar{69}$</span>
)</td>
</tr>
</tbody>
</table>

\#2

    sugar_table <- table(class_data$sugar)
    sugar_table_props <- prop.table(sugar_table)
    sugar_table_props

    ## 
    ## Regular (full sugar)   Zero sugar or diet 
    ##            0.6060606            0.3939394

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Regular</th>
<th>Zero Sugar</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>40 (<span class="math inline">$\frac{40}{66} =
0.\bar{60}$</span>)</td>
<td>26 (<span class="math inline">$\frac{26}{66} =
0.\bar{39}$</span>)</td>
</tr>
</tbody>
</table>

\#3

    cont_table <- table(class_data$sugar,class_data$cola)
    cont_table_props <- prop.table(cont_table)
    cont_table

    ##                       
    ##                        Cola (Coke, Pepsi, etc.) Something else
    ##   Regular (full sugar)                       10             30
    ##   Zero sugar or diet                         10             16

    cont_table_props

    ##                       
    ##                        Cola (Coke, Pepsi, etc.) Something else
    ##   Regular (full sugar)                0.1515152      0.4545455
    ##   Zero sugar or diet                  0.1515152      0.2424242

\#4 & 5

    require(dplyr)
    require(pander)

    ## Loading required package: pander

    d1 <- read.csv("https://tgstewart.cloud/soda.csv") |>
      filter(!is.na(cola) & !is.na(sugar))
    descr::CrossTable(
          d1$sugar
        , d1$cola
        , prop.chisq = FALSE
    ) |>
    pander(split.table=Inf)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 31%" />
<col style="width: 19%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: center;"> <br />
d1$sugar</th>
<th style="text-align: center;">d1$cola<br />
Cola (Coke, Pepsi, etc.)</th>
<th style="text-align: center;"> <br />
Something else</th>
<th style="text-align: center;"> <br />
Total</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: center;"><strong>Regular (full
sugar)</strong><br />
N<br />
Row(%)<br />
Column(%)<br />
Total(%)</td>
<td style="text-align: center;"> <br />
10<br />
25.0000%<br />
50.0000%<br />
15.1515%</td>
<td style="text-align: center;"> <br />
30<br />
75.0000%<br />
65.2174%<br />
45.4545%</td>
<td style="text-align: center;"> <br />
40<br />
60.6061%<br />
<br />
</td>
</tr>
<tr class="even">
<td style="text-align: center;"><strong>Zero sugar or
diet</strong><br />
N<br />
Row(%)<br />
Column(%)<br />
Total(%)</td>
<td style="text-align: center;"> <br />
10<br />
38.4615%<br />
50.0000%<br />
15.1515%</td>
<td style="text-align: center;"> <br />
16<br />
61.5385%<br />
34.7826%<br />
24.2424%</td>
<td style="text-align: center;"> <br />
26<br />
39.3939%<br />
<br />
</td>
</tr>
<tr class="odd">
<td style="text-align: center;">Total<br />
</td>
<td style="text-align: center;">20<br />
30.303%</td>
<td style="text-align: center;">46<br />
69.697%</td>
<td style="text-align: center;">66<br />
</td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 31%" />
<col style="width: 22%" />
<col style="width: 22%" />
<col style="width: 22%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Colas</th>
<th>Not Colas</th>
<th>Total</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Regular</td>
<td>10 (<span class="math inline">$\frac{10}{66} =
0.\bar{15}$</span>)</td>
<td>30 (<span class="math inline">$\frac{30}{66} =
0.\bar{45}$</span>)</td>
<td>40 (<span class="math inline">$\frac{40}{66} =
0.\bar{60}$</span>)</td>
</tr>
<tr class="even">
<td>    Row</td>
<td>10 (<span class="math inline">$\frac{10}{40} = 0.25$</span>)</td>
<td>30 (<span class="math inline">$\frac{30}{40} = .75$</span>)</td>
<td></td>
</tr>
<tr class="odd">
<td>    Col</td>
<td>10 (<span class="math inline">$\frac{10}{20} = 0.5$</span>)</td>
<td>30 (<span class="math inline">$\frac{30}{46} = 0.6521$</span>)</td>
<td></td>
</tr>
<tr class="even">
<td>No Sugar/Diet</td>
<td>10 (<span class="math inline">$\frac{10}{66} =
0.\bar{15}$</span>)</td>
<td>16 (<span class="math inline">$\frac{16}{66} =
0.\bar{24}$</span>)</td>
<td>26 (<span class="math inline">$\frac{26}{66} =
0.\bar{39}$</span>)</td>
</tr>
<tr class="odd">
<td>    Row</td>
<td>10 (<span class="math inline">$\frac{10}{26} = 0.3846$</span>)</td>
<td>16 (<span class="math inline">$\frac{16}{26} = 0.6154$</span>)</td>
<td></td>
</tr>
<tr class="even">
<td>    Col</td>
<td>10 (<span class="math inline">$\frac{10}{20} = 0.5$</span>)</td>
<td>16 (<span class="math inline">$\frac{16}{46} = 0.3478$</span>)</td>
<td></td>
</tr>
<tr class="odd">
<td>Total</td>
<td>20 (<span class="math inline">$\frac{20}{66} =
0.\bar{30}$</span>)</td>
<td>46 (<span class="math inline">$\frac{46}{66} =
0.\bar{69}$</span>)</td>
<td>66 (1)</td>
</tr>
</tbody>
</table>
