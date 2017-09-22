<!-- 
---
layout: post
title: "Executive Summaries in R Markdown"
date: 2017-09-22
---
-->

Transitioning from a primarily academic job into a more industrial job
has required me to adapt my workflow a little. One of the adaptations
that I'm still struggling to understand is how to generate reports that
those in my laboratory will read. In academic research, I generally
started all of my analysis reports with a description of the statistical
properties of the study, described the data, presented summaries of the
analysis procedures, and wrapped up with a discussion of conclusions and
limitations. What took me by surprise when coming into industry is that
no one here was interested in reading the details and nuances of the
analysis. The very first time I drafted an analysis report, I was
immediately asked to generate an executive summary at the front.

<!--excerpt-->

We'll put aside all of the concerns I have about management implementing
ideas without exploring the nuances and details of the analysis (it's
classic Dilbert material). We can just settle on the fact that
regardless of how I felt about it, I was now expected to summarize the
core findings in a few paragraphs at the start of each report.
Essentially, they wanted the equivalent of the abstract of an academic
article.

Up to this point, I've never actually written an academic article
myself. I've always been the statistical consultant; someone else wrote
the article and the accompanying abstract. Fortunately, generating the
summary wasn't really all that hard. Afterall, I can practically copy my
conclusions and limitations from the end of my report to the front.

Except I use R Markdown scripts for all of my reports and my conclusions
and limitations often depend on objects created in the analysis. How was
I supposed to reference objects that hadn't yet been created?

My initial solution used the `brew` package, as described in an answer
to a [StackOverflow
Question](https://stackoverflow.com/questions/23570718/creating-summaries-at-the-top-of-a-knitr-report-that-use-variables-that-are-defi)
from 2014. Recently, while browsing topics at the [RStudio
Community](community.rstudio.com), I came across [this
gem](https://community.rstudio.com/t/best-practices-for-organizing-rmarkdown-projects/914)
that describes exactly what it was I wanted to do.

The magic happens by using the [`ref.label` chunk
option](https://yihui.name/knitr/options/#code-chunk). Use of this chunk
option lets you make reference to objects that are defined in chunks
that appear later in the script. To illustrate, let's use three chunks
labeled `exec-summary`, `model`, and `table`. The `model` table will
generate a linear model object called `fit`, and the `table` chunk will
generate a `dust` object summarizing the linear model.

Here's how such a script looks:

---
    title: Report
    output: html_document
    ---
    
    ```{r}
    library(pixiedust)
    options(pixiedust_print_method = "html")
    ```
    
    ### Executive Summary 

    ```{r exec-summary, echo = FALSE, ref.label = c("model", "table")}
    ```

    Now I can make reference to `fit` here, even though it isn't yet defined in the script. For example, a can get the slope for the `qsec` variable by calling `round(coef(fit)[2], 2)`, which yields 0.93.

    Next, I want to show the full table of results. This is stored in the `fittab` object created in the `"table"` chunk.

    ```{r, echo = FALSE}
    fittab
    ```
    
    ### Results

    Then I need a chunk named `"model"` in which I define a model of some kind.

    ```{r model}
    fit <- lm(mpg ~ qsec + wt, data = mtcars)
    ```

    And lastly, I create the `"table"` chunk to generate `fittab`.

    ```{r table}
    fittab <- 
      dust(fit) %>%
      medley_model() %>% 
      medley_bw() %>% 
      sprinkle(pad = 4,
               bg_pattern_by = "rows")
    ```
    
And this is what the result looks like--notice that the results of the analysis are being displayed before I've run the analysis.

### Executive Summary 

Now I can make reference to `fit` here, even though it isn't yet defined
in the script. For example, a can get the slope for the `qsec` variable
by calling `round(coef(fit)[2], 2)`, which yields 0.93.

Next, I want to show the full table of results. This is stored in the

<table align="center" style="border-collapse:collapse;">
<tr>
<th colspan="1" ; rowspan="1" ; style="text-align:left;border-top:1px solid Black;">
term
</th>
<th colspan="1" ; rowspan="1" ; style="text-align:right;border-top:1px solid Black;">
estimate
</th>
<th colspan="1" ; rowspan="1" ; style="text-align:right;border-top:1px solid Black;">
std.error
</th>
<th colspan="1" ; rowspan="1" ; style="text-align:right;border-top:1px solid Black;">
statistic
</th>
<th colspan="1" ; rowspan="1" ; style="text-align:right;border-top:1px solid Black;">
p.value
</th>
</tr>
<tr>
<td colspan="1" ; rowspan="1" ; style="text-align:left;background-color:#FFFFFF;border-top:1px solid Black;padding:4px;">
(Intercept)
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#FFFFFF;border-top:1px solid Black;padding:4px;">
19.75
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#FFFFFF;border-top:1px solid Black;padding:4px;">
5.25
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#FFFFFF;border-top:1px solid Black;padding:4px;">
3.76
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#FFFFFF;border-top:1px solid Black;padding:4px;">
&lt; 0.001
</td>
</tr>
<tr>
<td colspan="1" ; rowspan="1" ; style="text-align:left;background-color:#DDDDDD;padding:4px;">
qsec
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#DDDDDD;padding:4px;">
0.93
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#DDDDDD;padding:4px;">
0.27
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#DDDDDD;padding:4px;">
3.51
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#DDDDDD;padding:4px;">
0.001
</td>
</tr>
<tr>
<td colspan="1" ; rowspan="1" ; style="text-align:left;background-color:#FFFFFF;border-bottom:1px solid Black;padding:4px;">
wt
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#FFFFFF;border-bottom:1px solid Black;padding:4px;">
-5.05
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#FFFFFF;border-bottom:1px solid Black;padding:4px;">
0.48
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#FFFFFF;border-bottom:1px solid Black;padding:4px;">
-10.43
</td>
<td colspan="1" ; rowspan="1" ; style="text-align:right;background-color:#FFFFFF;border-bottom:1px solid Black;padding:4px;">
&lt; 0.001
</td>
</tr>
</table>
</br></br>

### Results

Then I need a chunk named `"model"` in which I define a model of some
kind.

```r
fit <- lm(mpg ~ qsec + wt, data = mtcars)
```

And lastly, I create the `"table"` chunk to generate `fittab`.

```r
fittab <- 
  dust(fit) %>%
  medley_model() %>% 
  medley_bw() %>% 
  sprinkle(pad = 4,
           bg_pattern_by = "rows")
``` 


