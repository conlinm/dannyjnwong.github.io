---
title: "Hacking for anaesthesia: #gashack"
author: "Danny Wong"
date: "26 October 2017"
layout: post
blog: true
tag:
- coding
- shiny
- Perioperative Medicine
---

What do you get when you have a roomful of anaesthetists and software developers? Something geekier than just the two separately!

I recently had the pleasure of being part of exactly the scenario above, and I must say it was extremely enjoyable! The [Royal College of Anaesthetists](rcoa.ac.uk) and the [Society for Computing and Technology in Anaesthesia (SCATA)](scata.org.uk) jointly hosted the [#gashack](http://gashack.rcoa.it/index.html) event at the RCoA, over a weekend (21-22 October 2017), and quite a few people turned up to pitch their ideas and work on possible solutions.

From the pitches that were presented, I joined a group of 4 people to work on an app that could be used to provide customisable preoperative medication advice for patients who present to preoperative assessment clinics, so that they can modify their drug regimens in preparation for their surgery.

Often what happens in this situation is that patients would turn up to clinic and be seen by either an anaesthetist or a preassessment nurse and their medical history would be noted along with any medications they might be taking. The medications would then be looked up in books or guideline documents and the information then gets conveyed back to the patient in a variable format. Our group set out to streamline this process to provide an elegant printable list for the patient to then go home with so that they know what exactly to do with their medication before they undergo their operation.

Our group had 2 people with previous experience of developing software: J. Grant Forrest, who has had a long involvement with SCATA, and myself, who has had some limited experience with making simple R shiny apps. We first scraped recommendations from the [Royal Cornwall Hospitals NHS Trust Preoperative Assessment Guidelines](https://doclibrary-rcht.cornwall.nhs.uk/DocumentsLibrary/RoyalCornwallHospitalsTrust/Clinical/Anaesthetics/PreOperativeAssessmentGuidelines.pdf), which one of our group had had previous experience using. To scrape the data we used [Tabula](http://tabula.technology/), an open source `.pdf` solution that works on both Windows and Macs.

The group then branched off into 2 directions. Grant created a solution which utilised PHP/SQL and I used an R Shiny solution that loaded up the scraped data as a `.csv` file that served as a lookup table, and used the `selectizeInput()` [function](https://shiny.rstudio.com/articles/selectize.html) in my `ui.R` file to allow the selection of multiple drug names. The drug name inputs were then used to filter the lookup table and make a customised drugs list with advice for medication management on the `server.R` script. To see my solution live, [click here](https://dannyjnwong.shinyapps.io/PreopDrugs/). I've included the code for my solution below.


{% highlight r %}
# ui.R
library(shiny)
library(dplyr)

drugs_ui <- read.csv("drug_instructions.csv", stringsAsFactors = FALSE) 

# Define UI for application that draws a histogram
shinyUI(fluidPage(
  
  # Application title
  titlePanel("Preop Medication Advice v0.1"),
  p("Disclaimer: This advice comes from the Royal Cornwall Hospital, used without permission. Seek further advice from your doctor."),
  a(href="https://doclibrary-rcht.cornwall.nhs.uk/DocumentsLibrary/RoyalCornwallHospitalsTrust/Clinical/Anaesthetics/PreOperativeAssessmentGuidelines.pdf", "Click here for the original guidelines upon which this advice is based."),
  p("MIT License; Copyright (c) 2017 Danny Jon Nian Wong."), 
  a(href="https://github.com/dannyjnwong/PreopDrugs", "Click here for the source code for this app."),
  
  # Sidebar with a slider input for number of bins 
  sidebarLayout(
    sidebarPanel(
      selectizeInput("drug_name", "Search for drug names", 
                     choices = list("Type in a drug" = "", "Names" = drugs_ui$Drug), 
                     selected = NULL, 
                     multiple = TRUE,
                     options = NULL)
    ),
    
    mainPanel(
      tableOutput("drug_instructions")
    )
  )
))
{% endhighlight %}


{% highlight r %}
# server.R

library(shiny)
library(dplyr)
library(xtable)

drugs_server <- read.csv("drug_instructions.csv", stringsAsFactors = FALSE)

# Define server logic required to draw a histogram
shinyServer(function(input, output) {
   
  output$drug_instructions <- renderTable({
    
    tab <- drugs_server %>% filter(Drug %in% input$drug_name)
    
    xtable(tab)
    
  })
  
})
{% endhighlight %}

Overall, it was an extremely enjoyable day, and my first Hackathon. It was fun to apply my coding skills to a clinical problem. Hopefully this app will continue to develop!


{% highlight r %}
sessionInfo()
{% endhighlight %}



{% highlight text %}
## R version 3.3.3 (2017-03-06)
## Platform: x86_64-w64-mingw32/x64 (64-bit)
## Running under: Windows >= 8 x64 (build 9200)
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
## [1] knitr_1.17
## 
## loaded via a namespace (and not attached):
## [1] magrittr_1.5    tools_3.3.3     stringi_1.1.1   stringr_1.2.0  
## [5] evaluate_0.10.1
{% endhighlight %}
