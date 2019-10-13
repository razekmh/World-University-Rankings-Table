## Aim
This code tries to extract information from a university ranking website. The concept of collecting data from websites is called web scraping and is used mainly to collect data from websites which do not offer an API to collect data natively. 
Several tutorials are available to explain the web scraping basics. This notebook is more of a case study. <br />
Let's start ......  

## 1. Prerequisites
This code assumes that you have python installed on your machine.  Basic knowledge of python is also assumed. Here is a full list of the prerequisites: 
* python 3.6 or above
* Jupyter notebook - or any environment that allows running python
* The following python libraries (BeautifulSoup, Selenium, urllib, objectpath and Pandas) 
* A web browser, I am using chrome 77 here, but you can use other browsers too
* Web driver for the browsers you are using, for chrome and chrome based browsers you can download it from here https://chromedriver.chromium.org/downloads

## 2. What data are you trying to get? 
This is the first question you should ask yourself, before even touching a single key. In our case, we started with the idea of collecting the list of universities with their ranking. To understand how to do so you will need to visit the website itself to understand a bit about it and its webpages. <br/>

The page we are tyring to scrap looked something like this 

![title](img/basic_page_01.PNG)
<br/> <br/> <br/> 
