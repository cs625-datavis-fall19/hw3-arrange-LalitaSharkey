Homework 3
================
**Lalita Sharkey**  
10/01/2019

CS 625, Fall 2019
## Initail data observation
Before start jumping into creating visualizations, I have done some observation in order to gain a better understanding of the datasets. There were 2 datasets given. The first dataset is a daily breakdown information of Norfolk churchs that provide shelters for adults during winter(11/29/2017 to 1/16/2018). The other dataset contains information on daily weather information in the same duration as the first dataset. There were 49 samples in both the datasets.
## Question 1: What was the breakdown of women vs. men who were provided shelter each night?  
### Part 1 - Using Application (Tableau)  
![Q1](img/Q1.png)
A few experimental designs were created to find the most effective design. The first one that was created was the dual axises bar chart. It was the first thing that came to my mind when I thought about comparing 2 numeric values. The horizontal axis represented dates and the vertical axis representing the number of both 
### Part 2 - Using Programming Language/API (R)  
![R_Q1](img/Rplot_Q1.png)
```
MyData <- read.csv(file="merged.csv", header=TRUE, sep=",")

require(ggplot2)
library(tidyverse)


names(MyData)[names(MyData) == "ï..Date"] <- "Dates"
MyData$Dates <-  as.Date(MyData$Dates, "%m/%e/%Y")

g <- ggplot(MyData, aes(x=Dates, group= 1)) 
g <- g + scale_y_continuous(limits = c(0,110), breaks=seq(0,110,10), minor_breaks=seq(0,110,10))
g <- g + geom_line(aes(y=Men), colour="#4D79A8", size=2) + 
  geom_point(aes(y=Men), colour="#4D79A8", size=4) +
  geom_text(aes(y = Men[49]+7, x = Dates[49], label = "Men"), colour="#4D79A8", size = 6) + 
  geom_smooth(method = "lm", se=FALSE, color="#4D79A8", 
              aes(x = Dates, y = Men,group=1), size= 0.8, linetype = "dashed")
g <- g + geom_line(aes(y=Women), colour="#FA9FA6", size=2) + 
  geom_point(aes(y=Women),colour="#FA9FA6", size=4) +
  geom_text(aes(y = Women[49]-7, x = Dates[49], label = "Women"), colour="#FA9FA6", size = 6)  + 
  geom_smooth(method = "lm", se=FALSE, color="#FA9FA6", 
              aes(x = Dates, y = Women,group=1), size= 0.8, linetype = "dashed")
g <- g + theme_minimal()+theme_bw()
g <- g + scale_x_date(date_labels = "%b %d, %y", date_breaks = "1 day", date_minor_breaks = "1 day")
g <- g + theme(axis.text.x = element_text(angle = 90 , hjust = 1)) 
g <- g + labs(title = "The breakdown of women vs. men who were provided shelter each night", 
              x = "Date", y = "Value") 
g <- g + theme(plot.title = element_text(color = "black", size = 22, face = "bold", hjust = 0.5))

g
```

### Extra Credit(Vega-Lite)

## Question 2: In total, how many guests were provided shelter by each church (or pair of churches)?
### Part 1 - Using Application (Tableau)
![Q2](img/Q2.png)  

### Part 2 - Using Programming Language/API (R)
### Extra Credit(Vega-Lite)


## Question 3: Is total demand for shelter affected by weather?
### Part 1 - Using Application (Tableau)
![Q3](img/Q3.png)
### Part 2 - Using Programming Language/API (R)
### Extra Credit(Vega-Lite)




## References
https://community.tableau.com/thread/195972  
https://help.tableau.com/current/pro/desktop/en-us/multiple_measures.htm  
https://community.tableau.com/thread/212845  
https://community.tableau.com/thread/212880  
http://www.sthda.com/english/wiki/ggplot2-line-plot-quick-start-guide-r-software-and-data-visualization  
https://www.datanovia.com/en/blog/ggplot-title-subtitle-and-caption/  
https://ggplot2.tidyverse.org/reference/scale_date.html  
https://stackoverflow.com/questions/29357612/plot-labels-at-ends-of-lines 
https://stackoverflow.com/questions/25015690/r-geom-smooth-what-to-write-in-aes  
https://stackoverflow.com/questions/1660124/how-to-sum-a-variable-by-group  
https://stackoverflow.com/questions/25906705/creating-horizontally-stacked-bar-chart-with-given-data-in-r
https://rstudio-pubs-static.s3.amazonaws.com/4305_8df3611f69fa48c2ba6bbca9a8367895.html  
