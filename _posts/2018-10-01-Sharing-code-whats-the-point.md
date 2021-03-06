---
title: "Sharing code, what's the point?"
author: "Danny Wong"
date: "01 October, 2018"
layout: post
blog: true
tag:
- R
- coding
- R Markdown
- Perioperative Medicine
---

I've recently had the great fortune of publishing a [paper](https://bjanaesthesia.org/article/S0007-0912(18)30565-8/fulltext) which had significant interest from the general news media, it even managed to get picked up by the [BBC](https://www.bbc.co.uk/news/health-45432538), [The Guardian](https://www.theguardian.com/society/2018/sep/07/nhs-cancels-14-of-operations-at-last-minute-research-finds?CMP=Share_iOSApp_Other) and all the major newspapers in the UK!

As per usual, I've shared the source code for the analysis publicly, this time electing to serve it up on [GitHub as a repository](https://github.com/dannyjnwong/SNAP2_Cancellations), including both the manuscript as an `.Rmd` file and having the data wrangling and modelling code as a chunk located at the start of the `.Rmd` file, as well as the knitted `.html` version of the manuscript output to allow people to visualise what would happen if they knitted the document in `R`, IF they had the raw data at hand.

Which brings me to the two points of my post. Firstly, I cannot share the raw data in public, because it contains too much sensitive personal information and sensitive information about individual hospitals in the UK who contributed data. There could be unscrupulous individuals who might be able to identify patients within the data and link it to other bits of publicly available data, which is a big nono. Secondly, even as I share this code, people within my field of research don't have the necessary skills to do anything with it.

Currently in the clinical research world, we are facing a big headache. On one hand we want transparency in research in order to tackle the problems of unreproducible research, and much commentary has been written about the [reproducibility crisis affecting science](https://www.nature.com/news/over-half-of-psychology-studies-fail-reproducibility-test-1.18248). The assertion is that we want to be able to understand how research teams arrive at their findings, and showing the working behind the statistical analyses in order to ensure that findings are real and replicable, and not merely spurious. On the other hand, we need to ensure that confidentiality of individual patients is maintained, especially in the case of large epidemiological studies where patients may not necessarily have given their consent in sharing their data.

Even if the data was shared alongside my code, there may not be enough people out there who could read or understand the code. In Health Services Research (my area of clinical research), there have been some studies into which software packages are most widely used. In [one study](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3205033/) looking at the US literature, "Stata and SAS were overwhelmingly the most commonly used software applications employed (in 46.0% and 42.6% of articles respectively)." And while the popularity of `R` is [rising](https://stackoverflow.blog/2017/10/10/impressive-growth-r/), very few consumers of research (as opposed to producers of research) would ever know how to code in `R`. This means that the code that is shared would barely ever be read by anybody.

So is there any point in me sharing my code? I guess my answer would have to be principled if not pragmatic. I hope that by sharing my code, someone who comes to repeat my studies in the future can do so without having to reinvent the wheel again from scratch, and perhaps that someone can take my work and build upon it. Also it is an opportunity for a hypothetical future person to look at and offer up suggestions to my code to help me improve, or to serve as a teaching point. There may be a future world where lots more researchers would switch to using `R` or where more consumers of research would become comfortable with reading code. Indeed we are encouraging that future by [teaching as many people](http://datascibc.org/Data-Science-for-Docs/) as possible the basics of R and reproducible research.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Successful first day of our Data Science for Doctors course September 2018 edition. 20 more people who have been introduced to the world of <a href="https://twitter.com/hashtag/rstats?src=hash&amp;ref_src=twsrc%5Etfw">#rstats</a>, to go forth into the <a href="https://twitter.com/hashtag/NHS?src=hash&amp;ref_src=twsrc%5Etfw">#NHS</a> and academic world! <a href="https://twitter.com/datascibc?ref_src=twsrc%5Etfw">@datascibc</a></p>&mdash; Danny Wong 黄永年 (@dannyjnwong) <a href="https://twitter.com/dannyjnwong/status/1045337362853744640?ref_src=twsrc%5Etfw">September 27, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Day 2 of our Data Science for Doctors course at <a href="https://twitter.com/RCoANews?ref_src=twsrc%5Etfw">@RCoANews</a>! The students are learning to visualise data! <a href="https://t.co/yN72L8aqJU">pic.twitter.com/yN72L8aqJU</a></p>&mdash; Danny Wong 黄永年 (@dannyjnwong) <a href="https://twitter.com/dannyjnwong/status/1045598915846918144?ref_src=twsrc%5Etfw">September 28, 2018</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

However, there remains a lot of work to do in the area of improving research reproducibility. We need to come up with some solutions to at least share simulated toy data examples in order for third parties to run the code in order to fully appreciate it in its entirety. Just looking at the code and working it out in our heads doesn't allow the code to be fully dissected independently. We also need to encourage journals to recruit editorial board members who have some coding ability, and encourage keen coders to provide code reviews for submitted journal papers. Until that happens, we should encourage people to post their code online and reward authors for doing so by pushing them to cite their code as evidence of scientific output.


{% highlight r %}
sessionInfo()
{% endhighlight %}



{% highlight text %}
## R version 3.5.1 (2018-07-02)
## Platform: x86_64-w64-mingw32/x64 (64-bit)
## Running under: Windows >= 8 x64 (build 9200)
## 
## Matrix products: default
## 
## locale:
## [1] LC_COLLATE=English_United Kingdom.1252 
## [2] LC_CTYPE=English_United Kingdom.1252   
## [3] LC_MONETARY=English_United Kingdom.1252
## [4] LC_NUMERIC=C                           
## [5] LC_TIME=English_United Kingdom.1252    
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] knitr_1.20
## 
## loaded via a namespace (and not attached):
##  [1] Rcpp_0.12.18     rstudioapi_0.7   bindr_0.1.1      magrittr_1.5    
##  [5] tidyselect_0.2.4 munsell_0.5.0    colorspace_1.3-2 R6_2.2.2        
##  [9] rlang_0.2.2      stringr_1.3.1    plyr_1.8.4       dplyr_0.7.6     
## [13] tools_3.5.1      grid_3.5.1       gtable_0.2.0     yaml_2.2.0      
## [17] lazyeval_0.2.1   assertthat_0.2.0 tibble_1.4.2     anomalize_0.1.1 
## [21] crayon_1.3.4     bindrcpp_0.2.2   purrr_0.2.5      ggplot2_3.0.0   
## [25] evaluate_0.11    glue_1.3.0       stringi_1.1.7    compiler_3.5.1  
## [29] pillar_1.3.0     scales_1.0.0     pkgconfig_2.0.2
{% endhighlight %}
