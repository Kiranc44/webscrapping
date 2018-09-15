# webscrapping
import bs4
import requests
res=requests.get("https://www.newegg.com/global/in/Product/ProductList.aspx?Submit=ENE&DEPA=0&Order=BESTMATCH&Description=graphics+card&ignorear=0&N=-1&isNodeId=1")
page_soup=bs4.BeautifulSoup(res.text,'html.parser')

containers=page_soup.findAll("div",{"class":"item-container"})


filename="Brand.csv"
f=open(filename,"w")
header="Brands of graphics card\n"
f.write(header)
for container in containers:
	
	if(container.div.div.a!=None):
		brand=container.div.div.a.img["title"]
		f.write(brand)
		f.write("\n")
f.close()
