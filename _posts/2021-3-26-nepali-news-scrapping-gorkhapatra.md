---
title:  "Nepali News (Gorkhapatra) Scrapping Using BeautifulSoup and Python."
date:   2021-3-29 01:29:17 +0545
categories: Project
tags:
  - Web scrapping
  - python 
  - BeautifulSoup
  - data analysis
header:
  teaser: "assets/images/Gorkhapatra.png"
---
# Scrapping News Data From Gorkhapatra News Portal
Using python and BeautifulSoup.

# Scraping News Data From Gorkhapatra
## Introduction
In this blog, I am going to write about how I was able to scrap news from Gorkhapatra news portal of Nepal. I have also written a code for scraping Ekantipur and Annapurna but I will be sharing those in another blog.

In the previous blog, I wrote how I did scrape the data from Ekantipur, now in this blog, I am going write about how I scraped from Gorkhapatra. I encourage you to look in to my other blogs also.
* [Scrapping Ekantipur News]({{site.url}}/2021/03/24/nepali-news-scrapping-ekantipur/)
* [Scrapping Annapurna Post]()

### Motivation
Even though, I completed my bachlors in mathematics I decided to persue my career in tech field. I started from Coursera's [Python For Everybody Specialization ](https://www.coursera.org/learn/python/home/welcome)and also I got [Hawkins Fellowship](https://codefornepal.org/fellowship) due to which I got access to premium courses of [DataCamp](https://learn.datacamp.com/courses/supervised-learning-with-scikit-learn). After weeks, I was able to grasp some knowledge and idea about my first ever project. My final goal is to learn concept of Natural Language Processing and Then apply scrap news to perform task like classificaton.

## Importing  Dependencies 
For this news portal, I have used below python packages. If you are in hurry to get these code then please go to my repository [Nepali News Scrapper.](https://github.com/iamdurga/Nepali-News-Portal-Scrapping)
* `numpy`: for array operations.
* `Matplotlib`: for visualization
* `Pandas`: for data analysis
* `BeautifulSoup`: for parsing HTML content and extracting information 
* `urllib3`: for HTTP GET request



```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from bs4 import BeautifulSoup as BS
import urllib3

urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
```

## Scraping data of particular category
There are different categories like `national`, `international`, `society`,`provience` of the news. But first of all, I am going to scrap the news from the `national` itself.


```python
#Define url, which will be scraped
url = "https://gorkhapatraonline.com/national"
# extract a category
category = url.split("/")[-1]
category
```




    'national'



### Read a URL's content
First we will make a client i.e. using urllib3 and then using that client, we will make a GET request to the above url. Then we will parse the response given by server. The response will be parsed as HTML.


```python
http = urllib3.PoolManager()
http.addheaders = [('User-agent', 'Mozilla/61.0')]
web_page = http.request('GET', url)
soup = BS(web_page.data, 'html5lib')
```

If we see what the variable `soup` is holding, then we can see the entire page source of an webpage. After going to that URL from browser, we can see many contents including ads and the valuable content is only on the center of the page. Now our target is to find the best HTML element that can give us the exact content of that portion.

![img]({{site.url}}/assets/images/Gorkhapatra.PNG)

### Find the Title of each national news
In order to find the exact HTML element which holds the titles of each national news, we have to do inspect element and hover the webpage. Which is boring task though. In this news portal `p` element holds the title and its some properties like exact URL to the news. But the `p` is in `business` class and inside that business class we can find `trending2` first find the `.business` class and then find `.trending2` after that we can find 'p` inside that class content.


```python
 # loop through all the divs with '.business` class found in the webpage
 for content in soup.select(".business"):
   #newsurl is in `a` tag
    newsurl=content.find('a').get('href')
    trend2 = content.select_one(".trending2")
    # tile is inside `.trending2` calss in `p` tag
    # get p text
    title = trend2.find("p").text 
    title = title.strip()

    description = trend2.select_one(".description").text.strip()
    break
 newsurl,title,description
```




    ('https://gorkhapatraonline.com/national/2021-03-28-34551',
     'कोरोनाको ख्याल नगरी वसन्तपुरमा होली पर्व मनाइयो (फाेटाे फिचर)',
     'रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ ।\nविभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भिडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ ।')



The reason I used break on above code is that I want to only try on the first news. After a code can handle the scrapping on that code then I will be using that code for all other news. Now is the time to scrape the news's url and in above block it is defined as `newsurl`.


```python
news_page = http.request('GET', newsurl)
news_soup = BS(news_page.data, 'html5lib')
```

Now we have a URL of a particular news, we can goto that link and search for the valuable contents. All the news contents will be on the `news_page` so we will be using the soup of it. We need author name, author url, date of this news published, news title, description, and contents.


```python
# find the date and time
date = trend2.find('small').text
date = date.strip()
date = date.split('\xa0\xa0\xa0\xa0\n')[1]
date=date.strip()
date
```




    'चैत्र १५, २०७७ आईतवार'



**Finding Author Details**
* Author URL: Inside newsurl select `.post-author-name` and then find `a` tag there we get authorurl on `href`.
* Author Can be found on main page.


```python
#find the author url and author name
author = trend2.find('small').text
author = author.strip()
author = author.split('\xa0\xa0\xa0\xa0\n')[0]
author_url = news_soup.select_one(".post-author-name").find("a").get("href")
author_url,author
```




    ('https://gorkhapatraonline.com/author_news/3', 'गोरखापत्र अनलाइन ')



**News Content**
> Inside newsurl select `.newstext` class and then find all the `p` tags. First clean the text and then concatenate it with previously written text.


```python
content=""
for p in news_soup.select_one(".newstext").findAll("p"):
  content+="\n"+p.text
  content = content.strip()
content
```




    'गोरखापत्र अनलाइनकाठमाडौं, चैत १५ गते । रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ । विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भीडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ । तर सरकारी सूचनालाई बेवास्ता गर्दै उपत्यकासहित देशभर यस पर्व भिडभाडमा नै मनाइएको पाइएको छ ।फागु पर्वको मुख्य केन्द्र राजधानीको बसन्तपुरमा अध्याधिक मात्रामा युवाको सम्लग्नतामा यस पर्व मनाइएको छ ।बच्चादेखि युवायुवतीहरु त्यहाँ पुगेर सामाजिक दुरीको पालना नगरी रङ्गहरुको होली पर्व मनाएका छन् ।\nफाेटाे–मनाेजरत्न शाही / केशव गुरूङ्ग'





Now the news is scraped for a single URL. Our task is to use this concept for all the URLs of this category.

# Combining It All


```python
# loop through all the divs with '.business` class found in the webpage
for content in soup.select(".business"):
  #newsurl is in `a` tag
  newsurl=content.find('a').get('href')
  trend2 = content.select_one(".trending2")
  # tile is inside `.trending2` calss in `p` tag
  # get p text
  title = trend2.find("p").text 
  title = title.strip()
  #description is inside `.small` tag
  # we get by taking text only
  date = trend2.find('small').text
  date = date.strip()
  date = date.split('\xa0\xa0\xa0\xa0\n')[1]
  date=date.strip()
  description = trend2.select_one(".description").text.strip()

  news_page = http.request('GET', newsurl)
  news_soup = BS(news_page.data, 'html5lib')

  date = trend2.find('small').text
  date = date.strip()
  date = date.split('\xa0\xa0\xa0\xa0\n')[1]
  date=date.strip()
  content=""
  for p in news_soup.select_one(".newstext").findAll("p"):
    content+="\n"+p.text
    content = content.strip()
    print(f"""
        Title: {title}, URL: {newsurl}
        Date: {date}, Author: {author},
        Category :{category} ,
        Author URL: {author_url}, 
        Description: {description},
        Content: {content}
          """)
  
```

    
            Title: कोरोनाको ख्याल नगरी वसन्तपुरमा होली पर्व मनाइयो (फाेटाे फिचर), URL: https://gorkhapatraonline.com/national/2021-03-28-34551
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ ।
    विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भिडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ ।,
            Content: गोरखापत्र अनलाइनकाठमाडौं, चैत १५ गते । रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ । विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भीडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ । तर सरकारी सूचनालाई बेवास्ता गर्दै उपत्यकासहित देशभर यस पर्व भिडभाडमा नै मनाइएको पाइएको छ ।फागु पर्वको मुख्य केन्द्र राजधानीको बसन्तपुरमा अध्याधिक मात्रामा युवाको सम्लग्नतामा यस पर्व मनाइएको छ ।बच्चादेखि युवायुवतीहरु त्यहाँ पुगेर सामाजिक दुरीको पालना नगरी रङ्गहरुको होली पर्व मनाएका छन् ।
              
    
            Title: कोरोनाको ख्याल नगरी वसन्तपुरमा होली पर्व मनाइयो (फाेटाे फिचर), URL: https://gorkhapatraonline.com/national/2021-03-28-34551
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ ।
    विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भिडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ ।,
            Content: गोरखापत्र अनलाइनकाठमाडौं, चैत १५ गते । रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ । विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भीडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ । तर सरकारी सूचनालाई बेवास्ता गर्दै उपत्यकासहित देशभर यस पर्व भिडभाडमा नै मनाइएको पाइएको छ ।फागु पर्वको मुख्य केन्द्र राजधानीको बसन्तपुरमा अध्याधिक मात्रामा युवाको सम्लग्नतामा यस पर्व मनाइएको छ ।बच्चादेखि युवायुवतीहरु त्यहाँ पुगेर सामाजिक दुरीको पालना नगरी रङ्गहरुको होली पर्व मनाएका छन् ।
    फाेटाे–मनाेजरत्न शाही / केशव गुरूङ्ग
              
    
            Title: कोरोनाको ख्याल नगरी वसन्तपुरमा होली पर्व मनाइयो (फाेटाे फिचर), URL: https://gorkhapatraonline.com/national/2021-03-28-34551
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ ।
    विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भिडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ ।,
            Content: गोरखापत्र अनलाइनकाठमाडौं, चैत १५ गते । रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ । विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भीडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ । तर सरकारी सूचनालाई बेवास्ता गर्दै उपत्यकासहित देशभर यस पर्व भिडभाडमा नै मनाइएको पाइएको छ ।फागु पर्वको मुख्य केन्द्र राजधानीको बसन्तपुरमा अध्याधिक मात्रामा युवाको सम्लग्नतामा यस पर्व मनाइएको छ ।बच्चादेखि युवायुवतीहरु त्यहाँ पुगेर सामाजिक दुरीको पालना नगरी रङ्गहरुको होली पर्व मनाएका छन् ।
    फाेटाे–मनाेजरत्न शाही / केशव गुरूङ्ग
              
    
            Title: कोरोनाको ख्याल नगरी वसन्तपुरमा होली पर्व मनाइयो (फाेटाे फिचर), URL: https://gorkhapatraonline.com/national/2021-03-28-34551
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ ।
    विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भिडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ ।,
            Content: गोरखापत्र अनलाइनकाठमाडौं, चैत १५ गते । रङ्गहरुको पर्वको रुपमा परिचित होली (फागु) देशभर हर्षाेल्लासका साथ मनाइएको छ । विभिन्न रङ्ग एक आपसमा लगाएर मनाउने यस पर्वमा कोरोना भाइरसको जोखिम रहेको बताउँदै सरकारले सामाजिक दुरी (भौतिक) अवलम्बन गर्दै भीडभाड गरेर नमनाउन सार्वजनिक सूचना प्रकाशित गरेको छ । तर सरकारी सूचनालाई बेवास्ता गर्दै उपत्यकासहित देशभर यस पर्व भिडभाडमा नै मनाइएको पाइएको छ ।फागु पर्वको मुख्य केन्द्र राजधानीको बसन्तपुरमा अध्याधिक मात्रामा युवाको सम्लग्नतामा यस पर्व मनाइएको छ ।बच्चादेखि युवायुवतीहरु त्यहाँ पुगेर सामाजिक दुरीको पालना नगरी रङ्गहरुको होली पर्व मनाएका छन् ।
    फाेटाे–मनाेजरत्न शाही / केशव गुरूङ्ग
              
    
            Title: काठमाडौँको तुवाँलो अझै केही दिनसम्म रहने, URL: https://gorkhapatraonline.com/national/2021-03-28-34545
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: शुक्रबारदेखि काठमाडौँ उपत्यकाको आकाशमा एक्कासि बाक्लो तुवाँलाले ढाकेको छ । जल तथा मौसम विज्ञान विभागका अनुसार नेपालका अधिकांश जिल्लामा डढेलो लागिरहेको र लामो समय खडेरी पर्नुका साथै हावा नचेलेका कारणले सोबाट सिर्जित प्रदूषणका कण वायुमण्डलमा नै जम्मा भएकाले धेरैजसो स्थानमा प्रदूषण बढ्न गई पारदर्शिता घटेको छ ।,
            Content: काठमाडौँ, चैत १५ गते । शुक्रबारदेखि काठमाडौँ उपत्यकाको आकाशमा एक्कासि बाक्लो तुवाँलाेले ढाकेको छ । जल तथा मौसम विज्ञान विभागका अनुसार नेपालका अधिकांश जिल्लामा डढेलो लागिरहेको र लामो समय खडेरी पर्नुका साथै हावा नचलेका कारणले सोबाट सिर्जित प्रदूषणका कण वायुमण्डलमा नै जम्मा भएकाले धेरैजसो स्थानमा प्रदूषण बढ्न गई पारदर्शिता घटेको छ ।           स्थिर रहेको वायुमण्डल आगामी दुई–तीन दिनसम्म सुधार हुने सम्भावना कम रहेको मौसमविद् विभूति पोखरेलले बताउनुभयो । उहाँका अनुसार पछिल्लो समय अधिकांश जिल्लामा डढेलो लागिरहेको, लामो समय पानी नपरेको र हावा नचेलेका कारण वायुप्रदूषण बढेको हो । प्रदूषित वायुमण्डल सफा हुनका लागि कित वर्षा हुनुपर्छ वा हावा चल्नुपर्छ अहिले त्यो भएको छैन । धेरै किसिमको प्रदूषण मिसिएका कारणले सर्वसाधारणले आँखा पोलेको महसुस गरेका छन् ।           यसबाट हुने प्रदूषणका कारण स्वास्थ्यमा पर्ने नकारात्मक असर आँखा पोल्ने र श्वासप्रश्वासमा समेत समस्या आदिबाट बच्न आवश्यक कार्यबाहेक घर बाहिर ननिस्किन र निस्किनु परेमा मास्क लगाउन हुन तथा आवश्यक सतर्कता अपनाउन विभागले आग्रह गरेको छ ।           हाल देशमा स्थानीय वायुसँगै पश्चिमी वायुको समेत आंशिक प्रभाव छ । दिउँसो देशको पहाडी भू–भागमा आंशिक बदली रही अपराह्नपश्चात् देशका पहाडी भू–भागका एक–दुई स्थानमा मेघगर्जन, चट्याङसहित फाट्टफुट्ट वा हल्का वर्षाको सम्भावना  छ ।           मौसम पूर्वानुमान महाशाखाको पछिल्लो विवरणअनुसार आज काठमाडौँ उपत्यकाको न्यूनतम तापक्रम १० दशमलव छ डिग्री र अधिकतम तापक्रम २६ दशमलव चार डिग्री सेल्सियस छ । त्यस्तै आज सबैभन्दा कम जुम्लाको  तापक्रम एक दशमलव नौ डिग्री र सबैभन्दा धेरै नेपालगञ्जको अधिकतम तापक्रम ३४ दशमलव पाँच डिग्री सेल्सियस छ ।
              
    
            Title: उपत्यकामा ठाउँ ठाउँमा ट्राफिक जाँच  (फाेटाे फिचर), URL: https://gorkhapatraonline.com/national/2021-03-28-34541
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: होली पर्व (फागु)का अवसरमा उपत्यकामा ट्राफिङ चेकिङ बढाएको छ ।
    यातायातको दुरुपयोग गरी अवाञ्चित कार्य रोकथाम गर्नको लागि उपत्यकाका चोक चोकमा समेत ट्राफिङ चेकिङ भएका छन् ।
    उपत्यकामा होली पर्वको दिनमा समेत मोटरसाइकलमा तीनजना यात्रु नचढुन् भन्ने उद्देश्यमा यसअघि नै चोकचोकमा ट्राफिङ सचेतना बढाएको थियो । फाेटाे – सुजन गुरूङ,
            Content: गोरखापत्र अनलाइनकाठमाडौं, चैत १५ गते । होली पर्व (फागु)का अवसरमा उपत्यकामा ट्राफिङ चेकिङ बढाइएको छ । यातायातको दुरुपयोग गरी अवाञ्छित कार्य रोकथाम गर्नका लागि उपत्यकाका चोक चोकमा ट्राफिङ चेकिङ भएका छन् ।उपत्यकामा होली पर्वको दिनमा समेत मोटरसाइकलमा तीनजना यात्रु नचढुन् भन्ने उद्देश्यमा यसअघि नै चोकचोकमा ट्राफिङ सचेतना बढाएको थियो । फाेटाे – सुजन गुरूङ
              
    
            Title: उपत्यकामा ठाउँ ठाउँमा ट्राफिक जाँच  (फाेटाे फिचर), URL: https://gorkhapatraonline.com/national/2021-03-28-34541
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: होली पर्व (फागु)का अवसरमा उपत्यकामा ट्राफिङ चेकिङ बढाएको छ ।
    यातायातको दुरुपयोग गरी अवाञ्चित कार्य रोकथाम गर्नको लागि उपत्यकाका चोक चोकमा समेत ट्राफिङ चेकिङ भएका छन् ।
    उपत्यकामा होली पर्वको दिनमा समेत मोटरसाइकलमा तीनजना यात्रु नचढुन् भन्ने उद्देश्यमा यसअघि नै चोकचोकमा ट्राफिङ सचेतना बढाएको थियो । फाेटाे – सुजन गुरूङ,
            Content: गोरखापत्र अनलाइनकाठमाडौं, चैत १५ गते । होली पर्व (फागु)का अवसरमा उपत्यकामा ट्राफिङ चेकिङ बढाइएको छ । यातायातको दुरुपयोग गरी अवाञ्छित कार्य रोकथाम गर्नका लागि उपत्यकाका चोक चोकमा ट्राफिङ चेकिङ भएका छन् ।उपत्यकामा होली पर्वको दिनमा समेत मोटरसाइकलमा तीनजना यात्रु नचढुन् भन्ने उद्देश्यमा यसअघि नै चोकचोकमा ट्राफिङ सचेतना बढाएको थियो । फाेटाे – सुजन गुरूङ
              
    
            Title: तत्काल बन्दाबन्दी हुँदैन : श्रेष्ठ, URL: https://gorkhapatraonline.com/national/2021-03-28-34527
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: शिक्षा विज्ञान तथा प्रविधिमन्त्री कृष्णगोपाल श्रेष्ठले कोरोनाको सङ्क्रमण बढ्दै गए पनि तत्काल बन्दाबन्दी नगरिने बताउनुभएको छ । कोरोना सङ्क्रमणबाट बच्नका लागि आवश्यक स्वास्थ्य सुरक्षाका मापदण्ड अपनाएर अगाडि बढिने उहाँले स्पष्ट गर्नुभयो ।,
            Content: गोरखापत्र समाचारदाता
              
    
            Title: तत्काल बन्दाबन्दी हुँदैन : श्रेष्ठ, URL: https://gorkhapatraonline.com/national/2021-03-28-34527
            Date: चैत्र १५, २०७७ आईतवार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: शिक्षा विज्ञान तथा प्रविधिमन्त्री कृष्णगोपाल श्रेष्ठले कोरोनाको सङ्क्रमण बढ्दै गए पनि तत्काल बन्दाबन्दी नगरिने बताउनुभएको छ । कोरोना सङ्क्रमणबाट बच्नका लागि आवश्यक स्वास्थ्य सुरक्षाका मापदण्ड अपनाएर अगाडि बढिने उहाँले स्पष्ट गर्नुभयो ।,
            Content: गोरखापत्र समाचारदाता
    काठमाडौँ, चैत १५ गते । शिक्षा विज्ञान तथा प्रविधिमन्त्री कृष्णगोपाल श्रेष्ठले कोरोनाको सङ्क्रमण बढ्दै गए पनि तत्काल बन्दाबन्दी नगरिने बताउनुभएको छ । कोरोना सङ्क्रमणबाट बच्नका लागि आवश्यक स्वास्थ्य सुरक्षाका मापदण्ड अपनाएर अगाडि बढिने उहाँले स्पष्ट गर्नुभयो । मध्यपुर थिमि नगरपालिकाको २५औँ स्थापना दिवसको अवसरमा शनिबार आयोजित कार्यक्रममा मन्त्री श्रेष्ठले दुई सिफ्टमा विद्यालय सञ्चालन गरेर भए पनि बन्दाबन्दी भने नगरिने बताउनुभयो । उहाँले कोरोनाबाट बच्नका लागि स्वास्थ्य सुरक्षाका मापदण्ड अपनाउन सबैमा आग्रह गर्नुभयो । सरकारले भारतसँग सिमाना जोडिएका नाकामा कडाइ गरिरहेको भन्दै उहाँले कोरोनालाई हेल्चेक्र्याइँ भने नगर्न सबैमा आग्रह गर्नुभयो । स्थानीय तहमा विभिन्न दलको प्रतिनिधित्व भएकाले विकासको नाममा राजनीति गर्न नहुने भन्दै निर्वाचनका क्रममा मात्र दलीय प्रतिस्पर्धा गर्नुपर्नेमा मन्त्री श्रेष्ठले जोड दिनुभयो । मध्यपुर थिमि नगरपालिकाका प्रमुख मदनसुन्दर श्रेष्ठले स्थानीय सरकारको हैसियतमा करिब चार वर्षमा नगरपालिकाको मुहार परिवर्तन हुने गरी काम गरिएको बताउनुभयो । बागमती प्रदेशका सभामुख सानुकुमार श्रेष्ठले तीनै तहको समन्वयमा नेपालमा भौतिक विकासले गति लिएको बताउनुभयो । २०५३ साल चैत १४ गते साबिकका चपाचो, बोडे, बालकुमारी, नगदेश, दिव्यश्वरी गाविस समेटिएर मध्यपुर थिमि नगरपालिका घोषणा गरिएको थियो ।
              
    
            Title: शीर्ष नेताहरुद्वारा जोशीप्रति श्रद्धाञ्जली (फोटो फिचर), URL: https://gorkhapatraonline.com/national/2021-03-27-34507
            Date: चैत्र १४, २०७७ शनिबार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: नेपाली काँग्रेसका नेता तथा पूर्वमन्त्री नविन्द्रराज जोशीको निधनमा विभिन्न नेताहरुले श्रद्धाञ्जली व्यक्त गर्नु भएको छ ।,
            Content: गोरखापत्र अनलाइन काठमाडौं, चैत १४ गते । नेपाली काँग्रेसका नेता तथा पूर्वमन्त्री नविन्द्रराज जोशीको निधनमा विभिन्न नेताहरुले श्रद्धाञ्जली व्यक्त गर्नुभएको छ । नेपाली काँग्रेस केन्द्रीय कार्यालयमा राखिएको उहाँको पार्थिव शरीरमा विभिन्न राजनीतिक पार्टीका नेता तथा कार्यकर्ताले पुष्पगुच्छा अर्पण गरी श्रद्धाञ्जली व्यक्त गर्नुभएको थियो । उहाँको शुक्रवार राती निधन भएको थियाे ।
              
    
            Title: शीर्ष नेताहरुद्वारा जोशीप्रति श्रद्धाञ्जली (फोटो फिचर), URL: https://gorkhapatraonline.com/national/2021-03-27-34507
            Date: चैत्र १४, २०७७ शनिबार, Author: गोरखापत्र अनलाइन ,
            Category :national ,
            Author URL: https://gorkhapatraonline.com/author_news/3, 
            Description: नेपाली काँग्रेसका नेता तथा पूर्वमन्त्री नविन्द्रराज जोशीको निधनमा विभिन्न नेताहरुले श्रद्धाञ्जली व्यक्त गर्नु भएको छ ।,
            Content: गोरखापत्र अनलाइन काठमाडौं, चैत १४ गते । नेपाली काँग्रेसका नेता तथा पूर्वमन्त्री नविन्द्रराज जोशीको निधनमा विभिन्न नेताहरुले श्रद्धाञ्जली व्यक्त गर्नुभएको छ । नेपाली काँग्रेस केन्द्रीय कार्यालयमा राखिएको उहाँको पार्थिव शरीरमा विभिन्न राजनीतिक पार्टीका नेता तथा कार्यकर्ताले पुष्पगुच्छा अर्पण गरी श्रद्धाञ्जली व्यक्त गर्नुभएको थियो । उहाँको शुक्रवार राती निधन भएको थियाे ।
    तस्बिर:  मनोजरत्न शाही
              
    

# Working with other category
Now our above code can handle the top news of national category. Now we have to do the same for other category also


```python

ndict = {'Title': [], "URL": [], "Date":[],
      "Author":[], "Author URL":[], "Content":[],"Category": [], "Description":[]}

categories={"national":"https://gorkhapatraonline.com/national",
            "international":"https://gorkhapatraonline.com/international",
           "society":"https://gorkhapatraonline.com/society", 
            "province": "https://gorkhapatraonline.com/province"
          }

show=False
http = urllib3.PoolManager()
http.addheaders = [('User-agent', 'Mozilla/61.0')]

for category, url in categories.items():
  web_page = http.request('GET', url)
  soup = BS(web_page.data, 'html5lib')
  if category in ["national", "international"]:

    for news in soup.select(".business"):
      newsurl=news.find('a').get('href')
      trend2 = news.select_one(".trending2")
      try:
        title = trend2.find("p").text 
        title = title.strip()

        author = trend2.find('small').text
        author = author.strip()
        author = author.split('\xa0\xa0\xa0\xa0\n')[0]

        # author
        date = trend2.find('small').text
        date = date.strip()
        date = date.split('\xa0\xa0\xa0\xa0\n')[1]
        date=date.strip()
        description = trend2.select_one(".description").text.strip()
        
        # now got to this news url
        http.addheaders = [('User-agent', 'Mozilla/61.0')]
        web_page = http.request('GET',newsurl)
        news_soup = BS(web_page.data, 'html5lib')
        author_url = news_soup.select_one(".post-author-name").find("a").get("href")
        content=""
        for p in news_soup.select_one(".newstext").findAll("p"):
          content+="\n"+p.text
          content = content.strip()
        
        catagory = url.split("/")[-1]
        ndict["Title"].append(title)
        ndict["URL"].append(newsurl)
        ndict["Author"].append(author)
        ndict["Author URL"].append(author_url)
        ndict["Content"].append(content)
        ndict["Category"].append(category)
        ndict["Date"].append(date)
        ndict["Description"].append(description)
        if show:
          print(f"""
            Title: {title}, Title URL: {newsurl},
              Date: {date}, Author: {author},
              Author URL: {author_url}, 
              Category :{category} ,
            
              Content: {content},
              Description : {description}
                """)
        
      except:
        pass
  else:
    for feature1 in soup.select(".feature1"):
      # feature1 = soup.select_one(".feature1")
      newsurl = feature1.a.get("href")
      # news_url
      # title = 
      date=feature1.select_one(".feature-text").small.text.strip()
      title = feature1.select_one(".feature-text").text.strip().split("\n")[0]
      description = None

      category = url.split('/')[-1]

      news_page = http.request('GET', newsurl)
      news_soup = BS(news_page.data, "html5lib")
      # print(news_url)
      author_url = news_soup.select_one(".post-author-name").a.get("href")
      try:
        if len(news_soup.select_one(".newstext").find("p").find("strong").text.split(" ")) < 6:
          author =  news_soup.select_one(".newstext").find("p").find("strong").text
        else:
          author = None
        # print(author)
        # break
        content=""
        for p in news_soup.select_one(".newstext").findAll("p"):
          content+=p.text.split("गते । ")[-1]+"\n"

        ndict["Title"].append(title)
        ndict["URL"].append(newsurl)
        ndict["Author"].append(author)
        ndict["Author URL"].append(author_url)
        ndict["Content"].append(content)
        ndict["Category"].append(category)
        ndict["Date"].append(date)
        ndict["Description"].append(description)
        if show:
          print(f"""
            Title: {title}, Title URL: {newsurl},
              Date: {date}, Author: {author},
              Author URL: {author_url}, 
              Category :{category} ,
            
              Content: {content},
              Description : {description}
                """)
      
        
      except:
        pass


gorkhapatra_df = pd.DataFrame(ndict,columns = ndict.keys())    
gorkhapatra_df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Title</th>
      <th>URL</th>
      <th>Date</th>
      <th>Author</th>
      <th>Author URL</th>
      <th>Content</th>
      <th>Category</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>थरुहट थारुवानको धर्नामा गृहमन्त्री थापा</td>
      <td>https://gorkhapatraonline.com/national/2021-03...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>गोरखापत्र अनलाइनकाठमाडौं, चैत १२ गते । माइतिघर...</td>
      <td>national</td>
      <td>माइतिघरमा थरुहट थारुवान संयुक्त संघर्ष समितिको...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>अर्को निर्वाचनसम्म यही सरकारले निरन्तरता पाउँछ...</td>
      <td>https://gorkhapatraonline.com/national/2021-03...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>गोरखापत्र अनलाइनकाठमाडौं, चैत १२ गते । सञ्चार ...</td>
      <td>national</td>
      <td>सञ्चार तथा सूचना प्रविधिमन्त्री पार्वत गुरुङले...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>एमाले संसदीय दलको बैठक शुक्रबार ३ बजे बालुवाटा...</td>
      <td>https://gorkhapatraonline.com/national/2021-03...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>गोरखापत्र अनलाइनकाठमाडौं, चैत १२ गते । नेपाल क...</td>
      <td>national</td>
      <td>नेपाल कम्युनिष्ट पार्टी (एमाले) संसदीय दलको बै...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>निर्माणस्थल खाली गरेर आयोजना अघि बढाउन निर्देशन</td>
      <td>https://gorkhapatraonline.com/national/2021-03...</td>
      <td>चैत्र ११, २०७७ बुधबार</td>
      <td>रासस</td>
      <td>https://gorkhapatraonline.com/author_news/2</td>
      <td>सञ्चिता घिमिरे\nकाठमाडौँ, चैत १ गते । प्रतिनिध...</td>
      <td>national</td>
      <td>प्रतिनिधिसभा, विकास तथा प्रविधि समितिले कुनै प...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>पार्टी मोडालिटीको बारेमा छलफलमा छौँ –अध्यक्ष प...</td>
      <td>https://gorkhapatraonline.com/national/2021-03...</td>
      <td>चैत्र ११, २०७७ बुधबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>केदार तिमल्सिना (बनेपा समाचारदाता) बनेपा, चैत ...</td>
      <td>national</td>
      <td>नेपाल कम्यूनिष्ट पार्टी माओवादी केन्द्रका अध्य...</td>
    </tr>
    <tr>
      <th>5</th>
      <td>भारतमा एकै दिनमा ५३ हजार भन्दा बढी संक्रमित थपिए</td>
      <td>https://gorkhapatraonline.com/international/20...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>नयाँदिल्ली, चैत्त १२ गते। भारतमा पछिल्लो चौबीस...</td>
      <td>international</td>
      <td>भारतमा पछिल्लो चौबीस घण्टामा ५३ हजार ४७६ जनामा...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>बङ्गलादेश स्थापनाको ५० वर्ष, अर्थतन्त्रमा व्या...</td>
      <td>https://gorkhapatraonline.com/international/20...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>गाजीपुर, बङ्गलादेश, चैत १२ गते। शफिकुल आलम बङ्...</td>
      <td>international</td>
      <td>“मेरो वार्षिक कारोबार अहिले झण्डै १० करोड डलर ...</td>
    </tr>
    <tr>
      <th>7</th>
      <td>सुरक्षाबलको कारबाहीमा परी बाह्र तालिबानी लडाकू...</td>
      <td>https://gorkhapatraonline.com/international/20...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>काबुल, चैत १२ गते। अफगानिस्तानको दक्षिण प्रान्...</td>
      <td>international</td>
      <td>अफगानिस्तानको दक्षिण प्रान्त कान्दाहारमा आतङ्क...</td>
    </tr>
    <tr>
      <th>8</th>
      <td>अमेरिकामा कोभिड १९का संक्रमितको संख्या तीन करो...</td>
      <td>https://gorkhapatraonline.com/international/20...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>न्युयोर्क, चैत १२ गते। अमेरिकामा कोभिड १९ का स...</td>
      <td>international</td>
      <td>अमेरिकामा कोभिड १९ का संक्रमितहरुको संख्या तीन...</td>
    </tr>
    <tr>
      <th>9</th>
      <td>रोहिङ्ग्या शिविरमा भिषण आगलागी, कम्तीमा १५ शरण...</td>
      <td>https://gorkhapatraonline.com/international/20...</td>
      <td>चैत्र ११, २०७७ बुधबार</td>
      <td>रासस / एपी</td>
      <td>https://gorkhapatraonline.com/author_news/6</td>
      <td>कक्स बजार, बंगलादेश, चैत्त ११ गते। दक्षिणी बंग...</td>
      <td>international</td>
      <td>दक्षिणी बंगलादेशको रोहिङ्ग्या शरणार्थी शिविरमा...</td>
    </tr>
    <tr>
      <th>10</th>
      <td>चार सन्तानसहित आत्महत्या गरेकी सुकीका श्रीमानव...</td>
      <td>https://gorkhapatraonline.com/province/2021-03...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>कमल शर्मा</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>दैलेखको आठबीस नगरपालिका–३ निमायलकी ३५ वर्षीया ...</td>
      <td>province</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11</th>
      <td>भारतीय जेलमा ४० वर्ष बिताएका दुर्गाप्रसादले पा...</td>
      <td>https://gorkhapatraonline.com/province/2021-03...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>प्रेम अधिकारी</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>इलामको माई नगरपालिका १० का दुर्गाप्रसाद तिम्सि...</td>
      <td>province</td>
      <td>None</td>
    </tr>
    <tr>
      <th>12</th>
      <td>त्रियुगाका सामुदायिक वनमा डढेलो: सनुवागाउँ उच्...</td>
      <td>https://gorkhapatraonline.com/province/2021-03...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>उदयपुर, चैत १२ गते ।</td>
      <td>https://gorkhapatraonline.com/author_news/2</td>
      <td>उदयपुरको त्रियुगा नगरपालिका–११ स्थित नवउदय साम...</td>
      <td>province</td>
      <td>None</td>
    </tr>
    <tr>
      <th>13</th>
      <td>लाप्चामा कैलाश दर्शन गर्न पर्यटकका लागि  प्रती...</td>
      <td>https://gorkhapatraonline.com/province/2021-03...</td>
      <td>चैत्र १२, २०७७ बिहीबार</td>
      <td>राजन रावत</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>पवित्र धार्मिक स्थल मानसरोवर कैलाशको दर्शन गर्...</td>
      <td>province</td>
      <td>None</td>
    </tr>
  </tbody>
</table>
</div>



## Finally
Thank you for reading my blogs and please leave me some comments to improve myself. I am still beginner on this field.

