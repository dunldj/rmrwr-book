---
title: "A Tasting Menu"
author: "Peter Higgins"
date: "4/14/2020"
output: html_document
---


# A Tasting Menu of R
In this chapter, we will introduce you to a lot of neat things that you can do with R and RStudio, and you will publish a simple data analysis on the Internet 
that you can share with friends and family.
![tasting](images/tasting.png)    

## Setting the Table

At the end of this chapter, you will publish a data analysis to *RPubs*, a free website site where you can share your data analyses and visualizations. First you will need to set up an account on RPubs. Start by opening a new tab in your browser, and navigating to this [RPubs link](https://rpubs.com/users/new). It should look like the image below.
![rpubs1](images/rpubs1.png)    
<br>
Enter your name, email, username and password, and click on the _Register Now_ button, and you will be set up to use RPubs.    
This will bring you to this page. In the image below, we have set up an account for pdr.    
![rpubs2](images/rpubs2.png) 
Click on the _Here's How You Get Started_ link.
![rpubs3](images/rpubs3.png)    
You are now all set up and ready to go. Now you have a place on the internet to share your R creations!

## Goals for this Chapter
- Open a New Rmarkdown document
- Read in Data from a file
- Wrangle Your Data
- Visualize Your Data
- Publish your work to RPubs
- Check out Interactive Plots
- Check out Animated Graphics
- Check out a Clinical Trial Dashboard
- Check out a Shiny App

## Packages needed for this Chapter
You will need to enter this line of code into your console, to make sure that the tidyverse package is installed on your computer.
`install.packages("tidyverse")`      

In the setup chunk of your Rmarkdown document, you will need to access the tidyverse package with one line of code:
`library(tidyverse)`

## Website links needed for this Chapter
In this chapter, you will need to access the RPubs website.   
- https://rpubs.com/

## Pathway for this Chapter
This Chapter is part of the **XXX** pathway.
Chapters in this pathway include

## Open a New Rmarkdown document

Let's get started in R. Turn on your computer, and open the RStudio application. You should see the familiar panes for the Console, Environment, and Files.    
You need to open up a new document to activate the Source pane. While in RStudio, click on File/New File/R Script.
It should look like this.    
![newrmd](images/rmd1.png)
Now you will see the window below. Rename the document from "Untitled" to "Tasting", and click the OK button.
![newrmd2](images/rmd2.png)

Now the file is open, and looks like the window below. Click on the save icon (like a floppy disk in the top left), and save this document as tasting.Rmd.
![newrmd3](images/rmd3.png)
You have created a new Rmarkdown document. An Rmarkdown document lets you mix data, code, and descriptive text. It is very helpful for presenting and explaining data and visualizations. An Rmarkdown document can be converted (Knit) to HTML for a web page, Microsoft Word, Powerpoint, PDF, and several other formats.     
 
Code chunks are in a gray color, and both start and end with 3 backticks (\`\`\`).    

Text can be body text, or can be headers and titles. The number of hashtags before some header text defines what level the header is.     
You can insert links, pictures, and YouTube videos into Rmarkdown documents if it is helpful to explain your point. <br>
The first code chunk in each Rmarkdown document is named `setup`. The name comes after the left curly brace and the r (`{r`) at the beginning of the setup chunk. The letter `r` tells RStudio that what is coming on the next line is R code (RStudio can also use SQL, C++, python, and several other languages). After the comma, you can define options for this code chunk. In this case, the option `include` is set to FALSE, so that when this Rmarkdown document is knitted, this code chunk will not appear. 

## Read in Data from a file

## Wrangle Your Data

## Visualize Your Data

## Publish your work to RPubs

## The Dessert Cart

Below are some examples of neat things you can do with medical data in R. These are more advanced approaches, but completely doable when you have more experience with R.

### Interactive Plots

### Animated Graphics

### A Clinical Trial Dashboard

### A Shiny App

### An Example of Synergy in the R Community

One of the remarkable things about the open source R community is that people build all kinds of new R functions and packages that are useful to them, and then share them publicly with tools like _Github_ so that they can be useful to others. Often combining bits of several packages leads to **emergent properties**  - completely new creations that can only occur because all of the parts (packages) are present. The collaborative nature of the R community, in this case on Twitter (follow the #rstats hashtag), can lead to surprising collaborations and outcomes.     
Go ahead and play the example below, which uses rayrendering (all coded entirely in R) to show a 3D map of John Snow's cholera case data in 1854, which led him to identify the Broad Street water pump as the source of the cholera outbreak, and led to the removal of the pump handle and the end of outbreak.    
<br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/B_UsX5vfPJU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br>
 



