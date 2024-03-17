# 1

<table>
<colgroup>
<col style="width: 27%" />
<col style="width: 27%" />
<col style="width: 32%" />
<col style="width: 13%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;"></th>
<th style="text-align: center;">Cancer</th>
<th style="text-align: center;">Not Cancer</th>
<th style="text-align: center;"></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Test = +</td>
<td style="text-align: center;">.009,row=.04, col=.9,</td>
<td style="text-align: center;">.198 , row=.96, col=.2</td>
<td style="text-align: center;">.207</td>
</tr>
<tr class="even">
<td style="text-align: left;">Test = -</td>
<td style="text-align: center;">.001 , row=.001, col=.1</td>
<td style="text-align: center;">.792, row=.99, col=.8</td>
<td style="text-align: center;">.793</td>
</tr>
<tr class="odd">
<td style="text-align: left;"></td>
<td style="text-align: center;">0.01</td>
<td style="text-align: center;">.99</td>
<td style="text-align: center;">1</td>
</tr>
</tbody>
</table>

\#2

This is a conditional row probability. the probability of P(Cancer|+) =
.04

\#3

    library(ggplot2)

    tp <- .9 
    tn <- .95
    p_values <- seq(0, 1, by=0.01)

    ppv_values = (p_values * tp) / (p_values * tp + (1 - p_values) * (1 - tn))

    df <- data.frame(Cancer_Incidence = p_values, Positive_Predictive_Value = ppv_values)

    ggplot(df, aes(x = Cancer_Incidence, y = Positive_Predictive_Value)) +
      geom_line() +
      labs(title = 'Positive Predictive Value vs Cancer Incidence',
           x = 'Cancer Incidence',
           y = 'Positive Predictive Value') +
      theme_minimal()

![](Homework11_files/figure-markdown_strict/unnamed-chunk-1-1.png)
