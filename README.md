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