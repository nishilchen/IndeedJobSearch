# Indeed Job Search
As an international student, keywords like "US citizen required" or "Security Clearance" are the most unwanted requirement in the job search. This project aims at filtering out jobs with these keywords, and automatically send list of job links through email.

[Indeed](https://www.indeed.com/) is chosen as the first search engines in this application. Here's the demo:

### Define Parameters:

* "what" and "where" are two keywords used in Indeed search.
* Since only 10 results will appear in a search page, "num_pages" control the number of searches.
* Jobs with keywords in "unwanted" will be filtered out.
```
what, where = 'Statistics','Arlington, VA'
num_pages = 3
unwanted = ['US citizen', "TS", "SCI", "DoD", "TOP SECRET", "Top secret"]
```

### Obtain list of URLs from Indeed search

```
import jobapp
url = jobapp.IndeedSearch(what, where)
joblist = jobapp.Indeedjoblistpage(url)
urllist = joblist.geturls(num_pages)
urllist
```
```
Out[426]: 
['https://www.indeed.com/viewjob?jk=e19e553bdb828d6d&fccid=1544766d4c2915b0&vjs=3',
 'https://www.indeed.com/viewjob?jk=e2e95376b900c048&fccid=44a12684003d5fec&vjs=3',
 'https://www.indeed.com/company/BENNETT-AEROSPACE/jobs/Mathematician-Statistician-f77593548fbe1a5b?fccid=1c32fa3240b0d415&vjs=3',
 'https://www.indeed.com/viewjob?jk=45dadf5aff219212&fccid=1c32fa3240b0d415&vjs=3',
 'https://www.indeed.com/viewjob?jk=ee25252762fde374&fccid=f9e3ea7c39ef1b1d&vjs=3',
 'https://www.indeed.com/viewjob?jk=b56599558f6327e0&fccid=9c5c8ea47ff967bb&vjs=3',
 'https://www.indeed.com/viewjob?jk=c932057a25870ef6&fccid=cb8355041fe4a920&vjs=3',
 'https://www.indeed.com/viewjob?jk=a82622b17cf5a70e&fccid=066a6183ab9ba375&vjs=3',
 'https://www.indeed.com/viewjob?jk=44aa288390e8d991&fccid=662289e1e3aea148&vjs=3',
 'https://www.indeed.com/viewjob?jk=d5cc5426cbd61fcb&fccid=f19a0ec392b9790f&vjs=3',
 'https://www.indeed.com/viewjob?jk=a4a2d81617c214b1&fccid=cb8355041fe4a920&vjs=3',
 'https://www.indeed.com/viewjob?jk=50915a5e8a0929e8&fccid=e9870e3159e9c6ac&vjs=3',
 'https://www.indeed.com/viewjob?jk=7d93f6938f660cb4&fccid=11619ce0d3c2c733&vjs=3',
 'https://www.indeed.com/viewjob?jk=76ee9bc8421662e9&fccid=21b33f0a5e04c7d7&vjs=3',
 'https://www.indeed.com/viewjob?jk=09b18c936917b05e&fccid=c5ebc61e02eb4bac&vjs=3',
 'https://www.indeed.com/viewjob?jk=8ed20318e19a9efb&fccid=a60bccc99303faa8&vjs=3',
 'https://www.indeed.com/viewjob?jk=dcb9b75395d03d56&fccid=1acd48d27bfeb1e9&vjs=3',
 'https://www.indeed.com/viewjob?jk=b48093d26dd8e2e9&fccid=bebf9775d7d3bca8&vjs=3',
 'https://www.indeed.com/viewjob?jk=b9f28a841202564d&fccid=e86212ad9b1d3808&vjs=3',
 'https://www.indeed.com/viewjob?jk=947b3f7e3bd852c6&fccid=c5ebc61e02eb4bac&vjs=3',
 'https://www.indeed.com/company/Manthan-Systems/jobs/Data-Scientist-c6f9ef770aa4521f?fccid=2819abf8c4d99a07&vjs=3',
 'https://www.indeed.com/company/PYRAMID-SYSTEMS,-INC./jobs/Data-Scientist-cd4f0be5c2bb41c0?fccid=c4901ef258edc468&vjs=3',
 'https://www.indeed.com/viewjob?jk=1b6a68955ede1ccd&fccid=4e69f24625edd7db&vjs=3',
 'https://www.indeed.com/viewjob?jk=bfeb882f19f77cdd&fccid=9e215d88a6b33622&vjs=3',
 'https://www.indeed.com/viewjob?jk=ee3fbec8cef57717&fccid=2b15774e43d42233&vjs=3',
 'https://www.indeed.com/viewjob?jk=b66266be09e60ffa&fccid=b66d146def7286d2&vjs=3',
 'https://www.indeed.com/viewjob?jk=2aac34dd92cffccb&fccid=fe2d21eef233e94a&vjs=3',
 'https://www.indeed.com/viewjob?jk=3fa7ae24b7480b79&fccid=6d96c13c41c1672b&vjs=3',
 'https://www.indeed.com/viewjob?jk=83a2bfe349523407&fccid=bb384ca0a6d3d491&vjs=3',
 'https://www.indeed.com/viewjob?jk=76ff2f6dc1352a25&fccid=4e041af1d0af1bc8&vjs=3']
```

Since the num_pages equals 3 in this demo, geturls returns 30 results.
```
len(urllist)
Out[427]: 30
```

### Filter out jobs with unwanted keywords

```
urlresult = jobapp.CheckWordsIn(unwanted,urllist)
urlresult
```
```
Out[431]: 
['https://www.indeed.com/viewjob?jk=e19e553bdb828d6d&fccid=1544766d4c2915b0&vjs=3',
 'https://www.indeed.com/viewjob?jk=e2e95376b900c048&fccid=44a12684003d5fec&vjs=3',
 'https://www.indeed.com/company/BENNETT-AEROSPACE/jobs/Mathematician-Statistician-f77593548fbe1a5b?fccid=1c32fa3240b0d415&vjs=3',
 'https://www.indeed.com/viewjob?jk=45dadf5aff219212&fccid=1c32fa3240b0d415&vjs=3',
 'https://www.indeed.com/viewjob?jk=ee25252762fde374&fccid=f9e3ea7c39ef1b1d&vjs=3',
 'https://www.indeed.com/viewjob?jk=b56599558f6327e0&fccid=9c5c8ea47ff967bb&vjs=3',
 'https://www.indeed.com/viewjob?jk=a82622b17cf5a70e&fccid=066a6183ab9ba375&vjs=3',
 'https://www.indeed.com/viewjob?jk=44aa288390e8d991&fccid=662289e1e3aea148&vjs=3',
 'https://www.indeed.com/viewjob?jk=d5cc5426cbd61fcb&fccid=f19a0ec392b9790f&vjs=3',
 'https://www.indeed.com/viewjob?jk=76ee9bc8421662e9&fccid=21b33f0a5e04c7d7&vjs=3',
 'https://www.indeed.com/viewjob?jk=09b18c936917b05e&fccid=c5ebc61e02eb4bac&vjs=3',
 'https://www.indeed.com/viewjob?jk=8ed20318e19a9efb&fccid=a60bccc99303faa8&vjs=3',
 'https://www.indeed.com/viewjob?jk=dcb9b75395d03d56&fccid=1acd48d27bfeb1e9&vjs=3',
 'https://www.indeed.com/viewjob?jk=947b3f7e3bd852c6&fccid=c5ebc61e02eb4bac&vjs=3',
 'https://www.indeed.com/viewjob?jk=bfeb882f19f77cdd&fccid=9e215d88a6b33622&vjs=3',
 'https://www.indeed.com/viewjob?jk=ee3fbec8cef57717&fccid=2b15774e43d42233&vjs=3',
 'https://www.indeed.com/viewjob?jk=2aac34dd92cffccb&fccid=fe2d21eef233e94a&vjs=3',
 'https://www.indeed.com/viewjob?jk=3fa7ae24b7480b79&fccid=6d96c13c41c1672b&vjs=3']
```

12 jobs are filtered out in this example. 
```
len(urlresult)
Out[432]: 18
```

### Send the List to mail box

Several build-in packages can help us send the email through python. Here's the [tutorial](http://naelshiab.com/tutorial-send-email-python/)
```
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
```
Basic settings for email:
```
sender = "sender_email@gmail.com"
receiver = "receiver_email@gmail.com"
password = "sender_password"

msg = MIMEMultipart()
msg["From"] = sender
msg["To"] = receiver
msg["Subject"] = "Indeed - " + what + " in "+ where

# Body
unwanted_words = ", ".join(unwanted)
urls = "\n".join(urlresult)
body = "Jobs below have has no following words: " + unwanted_words + "\n" + urls
msg.attach(MIMEText(body))
```

Send the mail:
```
server = smtplib.SMTP('smtp.gmail.com', 587)
server.starttls()
server.login(sender, password)
server.sendmail(sender,receiver,msg.as_string())
server.quit()
```
