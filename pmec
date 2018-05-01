import mechanize
import cookielib
from bs4 import BeautifulSoup
import re
import json
import pandas as pd
from pprint import pprint


# Browser
br = mechanize.Browser()

# Cookie Jar
cj = cookielib.LWPCookieJar()
br.set_cookiejar(cj)

# Browser options
br.set_handle_equiv(True)
br.set_handle_gzip(True)
br.set_handle_redirect(True)
br.set_handle_referer(True)
br.set_handle_robots(False)


# Follows refresh 0 but not hangs on refresh > 0
br.set_handle_refresh(mechanize._http.HTTPRefreshProcessor(), max_time=1)

# Want debugging messages?
#br.set_debug_http(True)
#br.set_debug_redirects(True)
#br.set_debug_responses(True)

# User-Agent (this is cheating, ok?)
br.addheaders = [('User-agent', 'Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.1) Gecko/2008071615 Fedora/3.0.1-1.fc9 Firefox/3.0.1')]


# Open some site, let's pick a random one, the first that pops in mind:
r = br.open('http://www.zaragoza.es/ciudad/cementerios/')
html = r.read()

br.follow_link(nr=12)
br.follow_link(nr=17)
br.select_form(nr=1)

# Let's search

br.form['sape1']='pascua'
br.form['sape2']='villar'

br.submit()
soup = BeautifulSoup(br.response().read(), "lxml")

table = soup.find_all('table')[0]
df = pd.read_html(str(table))
print(df[0].to_json(orient='records'))
#body_tag = soup.body
#table = soup.findChildren('table')[0]

#rows = table.findChildren('tr')

#for row in rows:
#    cells = row.findChildren('td')
#    for cell in cells:
#        cell_content = cell.getText()
#        clean_content = re.sub( '\s+', ' ', cell_content).strip()
#        print(clean_content)
