#����
�ռ�url��url.txt
python google.py

��xray��ʼ����
python xray.py

�Զ�����ҳ�����ռ�����
python scan.py


#ע��
1.��Ҫ��װseleniumģ��
2.��װchrome�������chromedriver����
3.chromedriver��Ҫ���û�������
4.��Ҫ���֤����chrome
5.�����ű�ǰ��ɾ����ת��myscan_report.html�Լ�url_spider.txt

#����
python main.py

#���л���
python3.7

#PIP
pip install

selenium
urllib
requests
pyquery
threading

`from selenium import webdriver  # ���������������
from selenium.webdriver.chrome.options import Options
from selenium.common.exceptions import TimeoutException
from selenium.webdriver.support.wait import WebDriverWait
import time
import os
from faker import Factory
import random

#����Ƿ��в���url.txt�ļ�
'''
if os.path.exists('url/url_0.txt'):
	os.remove('url/url_0.txt')
else:
	print("û��url/url_0.txt�ļ�����")
'''

pages = int(input("������ɨ����ȣ�ҳ����:"))

with open('keyword.txt', 'r') as x:
	for line in x:
		word = line.replace('\n', '')
		print("�����ؼ��ʣ�"+word)
		for page in range(0,pages):
			print("������ȡ��"+str(page+1)+"ҳ")
			page = page*10
			#����ȸ�����������
			domain=random.choice(['www.google.com'
			,'www.google.gl'
			,'www.google.com.sv'
			,'www.google.hn'
			,'www.google.co.cr'
			,'www.google.com.jm'
			,'www.google.ht'
			,'www.google.com.pr'
			,'www.google.vg'
			,'www.google.com.ag'
			,'www.google.dm'
			,'www.google.com.vc'
			,'www.google.tt'
			,'www.google.com.ar'
			,'www.google.com.br'
			,'www.google.com.co'
			,'www.google.co.ve'
			,'www.google.com.ec'
			,'www.google.com.uy'
			,'www.google.no'
			,'www.google.is'
			,'www.google.dk'
			,'www.google.lv'
			,'www.google.lt'
			,'www.google.ru'
			,'www.google.pl'
			,'www.google.sk'
			,'www.google.at'
			,'www.google.ie'
			,'www.google.nl'
			,'www.google.be'
			,'www.google.fr'
			,'www.google.it'
			,'www.google.es'
			,'www.google.ro'
			,'www.google.gr'
			,'www.google.ba'
			,'www.google.sm'
			,'www.google.com.au'
			,'www.google.co.nz'
			,'www.google.co.ck'
			,'www.google.com.sb'
			,'www.google.ws'
			,'www.google.as'
			,'www.google.to'
			,'www.google.co.il'
			,'www.google.com.sa'
			,'www.google.com.eg'
			,'www.google.ae'
			,'www.google.com.bh'
			,'www.google.jo'
			,'www.google.com.ly'
			,'www.google.co.ma'
			,'www.google.com.et'
			,'www.google.mu'
			,'www.google.ci'
			,'www.google.dj'
			,'www.google.cd'
			,'www.google.cg'
			,'www.google.gm'
			,'www.google.co.ke'
			,'www.google.com.gi'
			,'www.google.co.bw'
			,'www.google.co.zm'
			,'www.google.com.na'
			,'www.google.co.ls'
			,'www.google.sh'
			,'www.google.mw'
			#,'www.google.cn'
			,'www.google.co.kr'
			,'www.google.mn'
			,'www.google.co.jp'
			,'www.google.com.hk'
			,'www.google.com.tw'
			,'www.google.com.vn'
			,'www.google.com.my'
			,'www.google.co.id'
			,'www.google.com.pk'
			,'www.google.com.bd'
			,'www.google.com.np'
			,'www.google.az'
			,'www.google.am'
			,'www.google.tm'
			,'www.google.co.uz'
			,'www.google.kg'
			,'www.google.com.tj'])
			print('ʹ�ùȸ�������'+domain)
			url = 'https://www.google.com.hk/search?q='+word+'&hl=zh&start='+str(page)+'&safe=images'#Ӣ��en����zh
			#url = 'https://'+domain+'/search?q='+word+'&hl=zh&start='+str(page)+'&safe=images'#Ӣ��en����zh
			#chromedriver��ָ��url
			option=Options()
			option.add_argument("--headless")#û�д���
			option.add_argument('�Cdisable-javascript')
			#option.add_argument('--window-size=300,200')
			option.add_argument('--blink-settings=imagesEnabled=false')#����ʾͼƬ
			#ʹ�����ua����Ȼ��ip��Ҫ�˻���֤
			f = Factory.create()
			ua = f.user_agent()
			print('ʹ��UA��'+ua)
			option.add_argument('--user-agent="'+ua+'"')
			
			driver =webdriver.Chrome(options=option)
			driver.get(url)
	
			#��ǩ����
			nodelist = driver.find_elements_by_xpath("//a")
			for url in nodelist:
				url1=str(url.get_attribute("href"))
				
				if url1!='None' and url1[0:18]!='https://www.google' and url1[0:15]!='https://support' and url1[0:20]!='https://accounts.goo' and url1[0:19]!='https://maps.google' and url1[0:20]!='https://translate.go' and url1[0:23]!='https://policies.google' and url1[0:23]!='https://webcache.google'and url1[0:22]!='http://webcache.google'and url1[8:21]!=domain[0:13]:
					print(url1)
					fp=open("url/url_0.txt","a+",encoding="utf-8")
					fp.write(url1+'\n')
					fp.close()
			driver.quit()
			#time.sleep(random.randint(5,10))

print("\n\n\n\n--------------------\n------�ռ����------\n--------------------\n")



def spider(url,num):
	option=Options()
	option.add_argument("--headless")#û�д���
	option.add_argument('�Cdisable-javascript')
	#option.add_argument('--window-size=300,200')
	option.add_argument('�Cno-sandbox')
	#option.add_argument('--blink-settings=imagesEnabled=false')#����ʾͼƬ
	option.add_argument('--proxy-server=http://127.0.0.1:23333')
	#ʹ�����ua����Ȼ��ip��Ҫ�˻���֤
	f = Factory.create()
	ua = f.user_agent()
	print('ʹ��UA��'+ua)
	option.add_argument('--user-agent="'+ua+'"')
	driver =webdriver.Chrome(options=option)
	driver.get(url)
	#��ǩ����
	nodelist = driver.find_elements_by_tag_name('a') + driver.find_elements_by_tag_name('script') + driver.find_elements_by_tag_name('img') + driver.find_elements_by_tag_name('link') + driver.find_elements_by_tag_name('iframe')
	for url in nodelist:
		print(url)
		if url.get_attribute("src"):
			url1 = url.get_attribute("src")
			if str(url1)[0:4]=='http':
				print(str(url1))
				file = 'url/url_'+str(num)+'.txt'
				fp=open(file,"a+",encoding="utf-8")
				fp.write(url1+'\n')
				fp.close()
		if url.get_attribute("href"):
			url2 = url.get_attribute("href")
			if str(url2)[0:4]=='http':
				print(str(url2))
				file = 'url/url_'+str(num)+'.txt'
				fp=open(file,"a+",encoding="utf-8")
				fp.write(str(url2)+'\n')
				fp.close()
	driver.quit()

number = int(input("������ɨ�����������"))
num = 1
while num <= number:
	txt = 'url/url_'+str(num-1)+'.txt'
	print(txt)
	with open(txt, 'r') as x:
		for line in x:
			if line and line[0:4]=='http':
				print(line)
				spider(line,num)
	time.sleep(10)
	num = num+1`