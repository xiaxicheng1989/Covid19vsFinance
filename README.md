# Covid19vsFinance
In this repository, I am looking at some analysis on covid19 and its impact on the financial market.

It includes: 
1) Predictive analysis on new cases of Covid-19
2) Impact of the new cases on the global market (indices (SP500, DAX, Hang Seng, ...) specific)
3) Impact of Covid-19 related news (Reuters and Bloomberg) on the market - WebScrapping

These are used sofar by myself to make better investment decisions.

## Covid data
To look at the financial impact, I mainly looked at the COVID cases developement in G20 contries.  
The COVID data are obtained from [here](https://covid.ourworldindata.org/). 

### Covid data illustration
In the notebook, I used different way to illustrate the developement of the new cases. As a illustration, I use loglog plot to illustrate the exponential dependence between new cases and the total cases. The figure below shows the the cases developement from March to July for the G10 countries. The data are averaged over 5 days to reduce daily fluctuations.  
<img src="https://github.com/xiaxicheng1989/Covid19vsFinance/blob/master/plots/covid.gif" width="80%">  
In countries, where the growth of cases still follows the exponential trend, the data points will follow the clear straight line. In contrast, once the situation improved, the data points will move away from the straight line and move downwards, as illustrated by the majority of countries. This is a clearer way to show the situation of a given country.  

## Modeling the new case
At the time of the notebook, China and South Korea were the only countries recovered desently from the virus. Hence, I use these countries to model the case spread. These are the assumptions I made:
- Cases develop close to a skewed gaussian
- The skewness is the same for all nations
- Policy from goverment influences the width of the gaussian
- The population density at the epicentre influences the peak of the gaussian

Based on these emiphirical findings, I estimated the skewness from China and South Korea to be 2.3, as shown below:
<img src="https://github.com/xiaxicheng1989/Covid19vsFinance/blob/master/plots/skewModel.png" width="50%">  
To varify the correctness, I fixed the skewness and applied the fit on the other contries as shown below:  
<img src="https://github.com/xiaxicheng1989/Covid19vsFinance/blob/master/plots/modeltest.png" width="32%"> <img src="https://github.com/xiaxicheng1989/Covid19vsFinance/blob/master/plots/modeltest1.png" width="32%"> <img src="https://github.com/xiaxicheng1989/Covid19vsFinance/blob/master/plots/modeltest2.png" width="32%">  
The simple model seems to do the job.  
To find the estimation of the new case overall, I estimate the fit for each country and summed them up to illustrate the case overall as shown below:  

<img src="https://github.com/xiaxicheng1989/Covid19vsFinance/blob/master/plots/MarketVSCOVID.png" width="60%">   
The dash-dotted lines show the market changes over the course of the corona virus. The black solid line shows the overall new cases development and the dashed lines are the fit estimation.  

This was initially used to estimate when the new cases reach the peak, which could be a opportunity to invest into the crushed market.


## Web scarping 
It is believed that the daily market sentiment is heavity dependent on the news. To illustrated this, I use web scraping (beautifulsoup library) to extract all corona virus related news headlines and articles.  
The idea is very simple. The code effectively looks for keywords, which the user can define. Words connected to improving corona cases will be labeled positive and illustrated in green, otherwise labeled as negative and in red.  
This script is sofar only adapted on [reuters](https://reuters.com). Slightly modification is required to adapt it to FT and bloomberg, which all depends on the html of the webpage.

The following graph shows the new article distribution, plotted together with SP500 index.  
<img src="https://github.com/xiaxicheng1989/Covid19vsFinance/blob/master/plots/Webscrapping.png" width="60%">  
