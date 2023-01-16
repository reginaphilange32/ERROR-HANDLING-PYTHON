# ERROR-HANDLING-PYTHON

# HOW TO SOLVE ERROR DURING IMPORTING DPLYR RVEST XML FOR R WEBSCRAPING

install.packages("dplyr")
install.packages("rvest")
library(xml2)
library(dplyr)
library(rvest)




url = "https://www.imdb.com/search/title/?title_type=feature&num_votes=25000,&genres=adventure&sort=user_rating,desc"
page =read_html(url)
movie_title = page %>% html_nodes(".lister-item-header a") %>% html_text()
View(movie_title)

movie_relyear = page %>% html_nodes(".text-muted.unbold") %>% html_text()
movie_relyear

imdbdf50 = data_frame(movie_title,movie_relyear)
View(imdbdf50)

#########################################


#flipkart
from bs4 import BeautifulSoup
import requests
import csv
import pandas as pd

laptop = []
prize = []
processor = []
ram = []

pages = list(range(1,11))

for page in pages:
  req = requests.get('https://www.flipkart.com/search?q=laptops&otracker=search&otracker1=search&marketplace=FLIPKART&as-show=on&as=off&page={}'.format(page)).text
  soup = BeautifulSoup(req,'html.parser')
  #print(soup.prettify())

  lapy = soup.findAll('div',class_='_4rR01T')
  for i in range(len(lapy)):
    laptop.append(lapy[i].text)

  

  commonclass = soup.findAll('li',class_='rgWa7D')

  for i in range(0,len(commonclass)):
    details=commonclass[i].text
    if("Processor" in details):
       processor.append(details)
    elif("RAM" in details):
       ram.append(details)
  
  cost = soup.findAll('div',class_='_30jeq3 _1_WHN1')  
  for i in range(len(cost)):
    prize.append(cost[i].text)

print(len(laptop))
print(len(prize))  
print(len(processor))
print(len(ram))    

df = {'laptop':laptop[200],'prize':prize[200],'processor':processor[slice(200)],'ram':ram[slice(200)]}
dataset = pd.DataFrame(data=df)


dataset

dataset.to_csv("flipkart-laptops.csv")

df = pd.read_csv('flipkart-laptops.csv')
df.shape


