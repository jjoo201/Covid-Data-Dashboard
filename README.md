[![Windows](https://svgshare.com/i/ZhY.svg)](https://svgshare.com/i/ZhY.svg)
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)
[![PyPI license](https://img.shields.io/pypi/l/ansicolortags.svg)](https://pypi.python.org/pypi/ansicolortags/)


# Covid-Data-Dashboard
ECM1400 Programming l ECM1400 Continuous Assessment

## Description

Creates a covid dashboard that contains the following covid data; the infection rates in the last 7 days, hospital cases and the  death total, about a specified local location and a specified national location, these default locations are _Exeter and England_. The dashboard also contains recent headlines with the specific keywords _'Covid , COVID-19, coronavirus'_. These news articles are displayed on the righthand side of the dashboard.

Users are able to interact with the dashboard by scheduling updates to the covid data as well as the news articles at specified time intervals. These updates are displayed on the lefthand side of the dashboard. Users are also about to cancel updates and delete articles by closing the widget from the dashboard.

![image](https://user-images.githubusercontent.com/95776339/145282398-2366338e-d34b-415c-b6d9-1b0d0c668336.png)

### Covid_Data-Handler Module

The logger will log the following activites in this module:
- When the covid_API_request function is actually called, this is so that one can monitor how often the covid data is updated and to verify that it is actually called when scheduled by the scheduler.
- When a _'Covid Data Update'_ has been scheduled via the dashboard, this will be logged to the covid_data_handler log and will also log the update_interval and update_name for said update. 
- When a _'Repeat Update'_ has been scheduled via the dashboard, this will be logged to the covid_data_handler log and will also log the update_interval and update_name for said update.
- If there is an instance where a user has not put in an update_interval before they have tried to submit an update, this would cause the program to crash, this instance is logged. When this occurs, the crash is avoided as I have programmed the update_interval to be set to 24 hours from the time the update is made.

The configFile holds the following sensitive infomation for this module:
- local_location; This setting the default local location displayed on the dashboard to Exeter but allowing third parties to change the location and this customize the dashboard.

_NOTE:_ Unable to test the _'time_conversion'_ function within this module as the current time is used within the function, so whatever test one may construct now will fail when another party runs it as it is not guarenteed they will be running the test at the exact same time it was constructed, making the 'current_time_total_seconds' equal.

### Covid_News_Handling Module

The logger will log the following activites in this module:
- When a user has inputted invalid 'key_terms' within the configFile, this would cause the program to crash, this instance is logged. When this occurs, the crash is avoided as I have programmed the 'main_url' to be reset to the default one with the key terms being _'Covid COVID-19 coronavirus'_.
- When the news_API_request function is actually called, this is so that one can monitor how often the news articles are updated and to verify that it is actually called when scheduled by the scheduler.
- When a _'News Article Update'_ has been scheduled via the dashboard, this will be logged to the covid_news_handling log and will also log the update_interval and update_name for said update.
- If there is an instance where a user has not put in an update_interval before they have tried to submit an update, this would cause the program to crash, this instance is logged. When this occurs, the crash is avoided as I have programmed the update_interval to be set to 24 hours from the time the update is made.

The configFile holds the following sensitive infomation for this module:
- api_key : For security purposes one should use thier own API key when it comes to running the dashboard rather than my own or one that is pre-defined within the source code
- key_terms : These are the terms that would be passed into the 'main_url' which would then return the latest articles featuring these keywords, allowing third parties to change the articles displayed and customize the dashboard.

### Main Module

The logger will log the following activites in this module:
- When the user has deleted an article from the dashboard, this will be logged to the main log and will also log the title of the article which as been deleted for more precise logging.
- When the user has deleted an scheduled update from the dashboard, this will be logged to the main log and will also log the contents of the scheduled update which as been deleted for more precise logging.
- When the dashboard is initally booted up, this will be logged.

With the section of code below found in the main module, under the main function starting from line 77; just to provide clarity to the usage of _'ARTICLE_INDEX'_. When the news articles are called from the covid_news_handling module into the main module and added to its own list 'covid_news', each article in then assigned an index, five articles are only being displayed at a time for the sake of formatting hence covid_news[0] - covid_news[4] are displayed - theyu're in the 'displayed_news' list which is the one that is actually passed into the render. However once one of these articles are removed from dashboard and effectively removed from the list 'displayed_news', covid_news[5] - the next article within 'covid_news' is appended to 'displayed_news' and thus rendered to the dashboard. Hopefully this will also explain as to why the global variable 'ARTICLE_INDEX' is initialised with the value 5.

![image](https://user-images.githubusercontent.com/95776339/145515043-2f7fd51f-f9d3-483d-aed0-671d0ba2e5f3.png)

_NOTE:_ When it came to running each module though pylint, there will be multiple occurances of _'C0301: Line too long'_, due to having long variable names, I acknowledge that I am over the limit in these line lengths however I chose to stick with the clear variable names so that it is as understandable as possible to third parties.

## Installation & Usage

### Installation

  Clone or download the repo.
  
- pip install Flask
- pip install sched
- pip install requests
- pip install uk_covid19
- pip install logging
- pip install configparser

### Usage

 - Navigate ECM1400 Covid Coursework in documents
 - Run on a python terminal/IDLE.
 - Copy and paste the server address into a web browser
  
Interacting with the dashboard; update the covid data displayed on the dashboard by specifying a time interval for when the update should occur, creating an update label which will be displayed on the update widgit and selecting the 'Update Covid Data' checkbox. Repeat the same steps but select the 'Update news articles' checkbox to update the news articles. All updates to both covid data and news articles will be displayed on the lefthand of the dashbaord.
  
![image](https://user-images.githubusercontent.com/95776339/145282223-80f1775d-9a87-4045-b0a6-e75cb7c2a236.png)
![image](https://user-images.githubusercontent.com/95776339/145332248-8e1e79fb-5d5c-47e9-9428-58ce25ebbb6c.png)

In the instance where the dashbaord keeps loading, please refresh the dashbaord manually.

Updates can be deleted from the dashboard by clicking the exit on the widgit, this will also remove the update from the scheduler and the update should not run.
Similarly with the news articles, by clicking the exit button on the article widgit, that specific news article will be deleted from the widgit and a new article will be displayed in its place.

## Technologies used 

  - Python 3.8
  - Flask
  - API

## License
  - MIT License 
 
 Link to github upload: 
## Enjoy! 😁
