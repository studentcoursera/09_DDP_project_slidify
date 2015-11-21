---
title       : Word Cloud Generator
subtitle    : Project for DDP course
author      : Ambika J
job         : Learner
logo        : word_cloud_logo.png
#biglogo     : word_cloud_logo.png
license     : by-nc-sa
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : solarized_light      # ribbon
widgets     : [bootstrap, interactive] #{mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
ext_widgets : {rCharts: [libraries/nvd3]}
#knit        : slidify::knit2slides
--- .outfont &twocol

<style>
slide.outfont p {
    font-size: 21px ;
}
</style>

## A _Word Cloud Generator_ App



*** =left
<br/>
**Problem statement:** Given any book, article, program, news, journal, white-paper, etc. user wants to  visualise the high frequency words in a most effective way.

With a word cloud generator the high frequency words of any given text file are identified, highlighted and visually represented.

<hr/>
The key idea is to quickly build and download **word cloud** for any file you are interested in.   
<hr/>
Very simple to use. You upload a file and tweak the settings; the app generates a downloadable word-cloud and frequency-table. Also, enables analyis of the 7 top frequencies, if interested.  
  

*** =right
<br/>
![](assets/img/word_cloud_gen_anly_nav.png)
  

--- &twocol

## Applications, features and future

*** =left

### Applications:   
1. **Pitches and Presentations:** Re-use the downloaded word-cloud in presentations, pitches, etc. which saves considerable amount of time.  
2. **Further Data analysis:** The computed frequency tables can further be used in data analysis. Example: Many data analysts use excel as tool to compute. For those users, its a handy tool.  
3. **Target audience:** Content analysts, data miners, publishers, search and social media.
  
*** =right

### Features and future:  
0. Word cloud is more effective than a line/bar/point plots; when analysis is related to words and its importance.
1. Further **analyse** the top 7 frequencies.
2. Key differentiator of this app is the **flexibility to tweak** 3 features and analyse the top 7 frequenices. In the next phase, we will monitor and understand the users need and add/modify/delete/automate a few features; making it more intuitive.  
3. Future upgrade of the app will involve the ability to analyse user behavior based on machine learning and predictive analysis. This is planned in phase2 and phase 3.


--- &twocol

## Visual Features



*** =left

### Word cloud

![plot of chunk simple-plot](assets/fig/simple-plot-1.png) 


```r
library(wordcloud); library(tm)
## word_count() computes word matrix
terms <- word_count(readLines(file))
col <- brewer.pal(8, "Dark2")
wordcloud(names(terms), terms, 
    rot.per = 0.35, colors = col)
```

*** =right

### An analysis of top 7 frequencies

#### NOTE: Issue with rCharts in slidify; overlap of options and legends. To solve, click **stacked** radio button. 

<div id = 'chart' class = 'rChart nvd3'></div>
<script type='text/javascript'>
 $(document).ready(function(){
      drawchart()
    });
    function drawchart(){  
      var opts = {
 "dom": "chart",
"width":    500,
"height":    400,
"x": "grp",
"y": "freq",
"group": "wrds",
"type": "multiBarChart",
"id": "chart" 
},
        data = [
 {
 "wrds": "work",
"freq":            470,
"grp":              5 
},
{
 "wrds": "management",
"freq":            237,
"grp":              3 
},
{
 "wrds": "time",
"freq":            147,
"grp":              4 
},
{
 "wrds": "scientific",
"freq":            135,
"grp":              4 
},
{
 "wrds": "workman",
"freq":            123,
"grp":              5 
},
{
 "wrds": "workmen",
"freq":            115,
"grp":              5 
},
{
 "wrds": "day",
"freq":            109,
"grp":              1 
} 
]
  
      if(!(opts.type==="pieChart" || opts.type==="sparklinePlus" || opts.type==="bulletChart")) {
        var data = d3.nest()
          .key(function(d){
            //return opts.group === undefined ? 'main' : d[opts.group]
            //instead of main would think a better default is opts.x
            return opts.group === undefined ? opts.y : d[opts.group];
          })
          .entries(data);
      }
      
      if (opts.disabled != undefined){
        data.map(function(d, i){
          d.disabled = opts.disabled[i]
        })
      }
      
      nv.addGraph(function() {
        var chart = nv.models[opts.type]()
          .width(opts.width)
          .height(opts.height)
          
        if (opts.type != "bulletChart"){
          chart
            .x(function(d) { return d[opts.x] })
            .y(function(d) { return d[opts.y] })
        }
          
         
        
          
        

        
        
        
      
       d3.select("#" + opts.id)
        .append('svg')
        .datum(data)
        .transition().duration(500)
        .call(chart);

       nv.utils.windowResize(chart.update);
       return chart;
      });
    };
</script>

--- {tpl: thankyou, social: [{title: App, href: "https://neo-r-apps.shinyapps.io/word_cloud_gen"}]}

## Extendability  
1. This app can be extended to spam classification, do a word cloud for spam and ham.  
1. It can be further extended by grouping words; different search terms and tags, and build a new model.
1. Analysis of twitter data, can dive deeper into this as well.
1. Further, extend to project metadata and tags in word cloud form.
1. We would not limit it to only frequencies, but add weighted words as well and build it to use in prediction logic.

## References  
1. Shiny apps gallery
2. Download references are from a blog by user 'TrigonaMinima'





