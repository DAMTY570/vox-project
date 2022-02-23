# vox-project
programming project APE

#Projet cinéVox

import requests
from bs4 import BeautifulSoup


url='https://www.cine-vox.com/films-a-l-affiche/'
url

req= requests.get(url)
soup= BeautifulSoup(req.text,'html.parser')
str(soup)

films = soup.find_all('a' ,class_= 'vignette')
films

films =re.findall('<a class="vignette url"(.*?)/></a>', str(soup))
len(films)
films_test = re.findall('https://www.cine-vox.*?"',films[0])
films_test

films2 ='https://www.cine-vox.*?"'
films_link = re.findall(films2, str(films))
films_link

names = 'Voir la fiche du film .*?">'
names_list = re.findall(names, str(films))
names_list
liste_des_film=[]
for i in range (0,len(names_list)):
    print(names_list[i][22:-2])
    liste_des_film.append(names_list[i][22:-2])
liste_des_film

from selenium import webdriver

PATH = "C:\Program Files (x86)\chromedriver.exe"
driver = webdriver.Chrome(PATH)

driver.get(films_link[2])

print(driver.title)
driver.find_element_by_class_name("didomi-continue-without-agreeing").click()
driver.find_element_by_id("close").click()


titre=(driver.find_element_by_class_name('ff_titre').text)
print(titre)

jour=[]
date=[]
for i in range(0,5):
     if (driver.find_elements_by_class_name('hr_jour')[i].text) !='':
        jour.append(driver.find_elements_by_class_name('hr_jour')[i].text[:4])
        date.append(driver.find_elements_by_class_name('hr_jour')[i].text[-2:])
print(jour)
print(date)


genre=(driver.find_element_by_xpath('//*[@id="maincontent-large"]/div/div[1]/p[4]/span[2]/strong').text)
genre


heure=[]
for i in range(0,7):
    if (heure.append((driver.find_elements_by_class_name('hor')[i].text))
print(heure)

lst = []
for i in range(1,6):
    driver.find_element_by_xpath('//*[@id="horaires"]/div/div[1]/div/div[{}]'.format(str(i))).click()
    lst.append({
    'titre' : titre,
    'genre' : genre,
    'jour' : jour[i-1],
    'date' : date[i-1],
    'hor' : [hor.text for hor in driver.find_elements_by_class_name('hor') if hor.text != '']
    })
    

import pandas as pd
pd.DataFrame(lst).explode('hor')