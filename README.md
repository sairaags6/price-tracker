# price-tracker
import bs4
import urllib.request
import requests
import smtplib

Price_list=[]

def Price_check():
    url = "link"
    header = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/92.0.4515.159 Safari/537.36."}
    page= requests.get(url,headers=header )
    html = page.content
    soup=bs4.BeautifulSoup(html,'html.parser')
    prices=soup.find(id='priceblock_ourprice').get_text()
    Price = float(prices.replace("₹","").replace(",",""))
    Price_list.append(Price)
    return Price


def send_mail():
    server=smtplib.SMTP('smtp.gmail.com',587)
    server.ehlo()
    server.starttls()
    server.ehlo()
    server.login(usermail, password)
    subjet="price fell"
    body="check the link"
    #server.sendmail(from_addrs, to_addrs, msg)
    server.quit()
    
    
    
count=1    
while True:
    
    curr=Price_check()
    if count >1:
    
        if Price_list[-1]<Price_list[-2]:
            send_mail()
        
    count+=1
