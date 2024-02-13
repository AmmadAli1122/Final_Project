# Final_Project
#BanoQabil2.0
import requests
import re
from bs4 import BeautifulSoup
import pandas as pd

#Artificial Intelligence

url1 = "https://en.wikipedia.org/wiki/Artificial_intelligence"
page1 = requests.get(url1)
soup1 = BeautifulSoup(page1.content,"html5")
title1 = soup1.find(class_="mw-page-title-main").text
quote1 = soup1.find(class_="hatnote navigation-not-searchable").text
l1 = []
for paragraph in soup1.select("p"):
  Content1 = re.compile(r"\[.*?\]").sub("",paragraph.text).replace("Later editions.","").replace("These were the four of the most widely used AI textbooks in 2008:","")
  l1.append(Content1)
content1 = "\n".join(l1)

#Computer Programing

url2 = "https://en.wikipedia.org/wiki/Computer_programming"
page2 = requests.get(url2)
soup2 = BeautifulSoup(page2.content,"html5")
title2 = soup2.find(class_="mw-page-title-main").text
l2 = []
for paragraph in soup2.select("p"):
  Content2 = re.compile(r"\[.*?\]").sub("",paragraph.text)
  l2.append(Content2)
content2 = "\n".join(l2)


data = [[url1,title1,quote1,content1,url2,title2,content2]]
df = pd.DataFrame(data,columns=['url1','title1','quote1','content1','url2','title2','content2',])
df.to_csv("Final_Project.csv")
