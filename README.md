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


It is clear that the page contains some sort of a table that hosts the information we are trying to collect. However collecting the information will depend on the HTML code hidden behind what we can see in the browser window. In chrome to display the HTML code simply press F12. The page should look something like this  

![title](img/page_code_02.PNG)
<br/> <br/> <br/> 


Using the small inspection cursor you can point at elements of the page and find out which part of the HTML represent them. This important because we will only use the HTML to collect the data and not the displayed page in the browser. Once you have identified the part of HTML corresponds with the information we need then we will start scraping 

## 3. Let's write some python 

A standard method of using python to request internet pages is through the requests library, however in our particular case this approach will not work, because the website uses AJAX to modify the HTML of the page. This means that the HTML code which you will receive by using requests will only contain an empty template of the table and not the information we are trying to collect. To give the JS code a chance to run and populate the table with the information, we use selenium. Selenium uses browsers to request webpages and then collect the HTML after the page is fully loaded, which will allow us to collect the information we need.

```
# import standard libraries
import json
import time

# import third party libraries
import objectpath
import pandas as pd

from bs4 import BeautifulSoup as soup
from urllib.request import urlopen 
from selenium import webdriver
```

Selenium requires a webdriver to access the web browser. It can be installed or used from an executable file directly. In this example we will use the executable file directly, please edit the following code by adding the location of the webdriver. It is recommonded to place it with the code itself.

```
webdriver_location = '***please insert here webdriver location *** /chromedriver.exe'

webdriver_location = 'C:/Users/razek/Desktop/git_pages/World-University-Rankings-Table/chromedriver.exe'
# initiate webdriver
driver = webdriver.Chrome(executable_path = webdriver_location)
```

Defining which web address we are going to use for scrapping is essential for the workflow. A quick inspection of the target web address reveals that changing the length parameter from 25 to -1 will result in collecting all the available universities instead of 25 per page. This should enable us to collect the information we need in one go rather than requesting several web pages. 
Also checking the tabs available on the web page (ranking, scores) reveals more data to be collected. Therefore we will use two web adresses to collect the data, as follows: 

```
url_stats = 'https://www.timeshighereducation.com/world-university-rankings/2020/world-ranking#!/page/0/length/-1/sort_by/rank/sort_order/asc/cols/stats'
url_scores = 'https://www.timeshighereducation.com/world-university-rankings/2020/world-ranking#!/page/0/length/-1/sort_by/rank/sort_order/asc/cols/scores'
```