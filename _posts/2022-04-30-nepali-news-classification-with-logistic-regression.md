---
title:  "Nepali News Classification using Logistic Regression"
date:   2022-04-30 09:29:17 +0545
categories: Project 
tags:
  - Data Analysis
  - Nepali News
  - EDA
header:
  teaser: "assets/nepali_news/eda/output_36_7.png"
  overlay_image: "assets/nepali_news/eda/output_36_7.png"
toc: true
---
## Logistic Regression for Nepali News Classification
Hello everyone, and welcome back to my news categorization blog. In this blog, I'll be looking into Logistic Regression for news in Nepali, which is our native language. I started this project almost a year ago but never finished it because I had no idea what I was doing and only knew BeautifulSoup from Datacamp. I was able to scrape a Nepali news webpage using that information.

I enrolled in Coursera's natural language processing specialization because I was interested in utilizing machine learning on a news site and was able to grasp some of the core ideas of classification algorithms such as Naive Bayes, Logistic Regression, and Decision Tree. I'll describe how I used the Logistic Regression classification method in my data in this blog because I've already written a blog about how I enable news scraping. The primary purpose of applying various types of classification algorithms to news data is to be able to categorize it. A Machine Learning classification approach called logistic regression is used to predict the likelihood of a categorical dependent variable. I followed the steps outlined below to accomplish this.


# Import Necessary Module
I loaded the modules that I needed for my news classification work here.

* os: The OS module in Python provides functions for interacting with the operating system 

* pandas: Working with DataFrame 

* numpy: For mathematical calculations

* matplotlib: For visualization 

* matplotlib.front manager: A module for finding, managing, and using fonts across platforms 

* matplotlib.front manager: A module for finding, managing, and using fonts across platforms

* matplotlib.front manager: A module for finding, managing, and using fonts across

* warnings: Warnings are provided to warn the developer of circumstances that aren't always exceptions.



```python

import os
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.pyplot import figure
from matplotlib.font_manager import FontProperties
import seaborn as sns
import warnings
warnings.filterwarnings("ignore")
import pprint

plt.style.use("seaborn-whitegrid")

```

# Open the CSV file

To integrate separate csv files, I did the following. I scraped the news on a daily basis and put it in a different csv file for each day. For the tesk, I concatenated all of the csv files.


```python
all_filenames = [i for i in os.listdir("/content/drive/MyDrive/News Scraping") if  ".csv" in i and "combined" not in i]
print(all_filenames)
```

    ['2021-03-25.csv', '2021-03-26.csv', '2021-03-27.csv', '2021-03-28.csv', '2021-03-29.csv', '2021-03-30.csv', '2021-03-31.csv', '2021-04-01.csv', '2021-04-03.csv', '2021-04-04.csv', '2021-04-05.csv', '2021-04-06.csv', '2021-04-07.csv', '2021-04-08.csv', '2021-04-12.csv', '2021-04-13.csv', '2021-04-14.csv', '2021-04-15.csv', '2021-04-16.csv', '2021-04-17.csv', '2021-04-18.csv', '2021-04-19.csv', '2021-10-09.csv', '2021-10-10.csv', '2021-10-20.csv', '2021-10-21.csv', '2021-10-22.csv', '2021-10-23.csv', '2021-10-24.csv', '2021-10-25.csv', '2021-10-26.csv', '2021-10-27.csv', '2021-11-21.csv', '2021-11-22.csv', '2021-11-25.csv', '2021-11-28.csv', '2021-11-29.csv', '2021-11-30.csv', '2021-12-05.csv', '2021-12-25.csv', '2022-01-02.csv', '2022-01-04.csv', '2022-01-11.csv', '2022-01-13.csv', '2022-01-18.csv', '2022-03-26.csv', '2022-03-27.csv', '2022-04-04.csv']
    


```python
root = "/content/drive/MyDrive/News Scraping/"
```

There are 9 columns and 9282 rows in the merged csv file. Title, URL, Date, Author, Author URL, Content, Category, Description, and so on are some of the 9 column titles.


```python
combined_csv = pd.concat([pd.read_csv(root+f) for f in all_filenames])
combined_csv
```





  <div id="df-37195002-5e05-49a5-a8fc-a2b1704c8379">
    <div class="colab-df-container">
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
      <th>Unnamed: 0</th>
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
      <td>0</td>
      <td>स्पष्टीकरण बुझाउँदै रावलले ओलीलाई नै सोधे- पार...</td>
      <td>https://ekantipur.com/news/2021/03/25/16166859...</td>
      <td>चैत्र १२, २०७७</td>
      <td>कान्तिपुर संवाददाता</td>
      <td>https://ekantipur.com/author/author-14301</td>
      <td>काठमाडौँ — नेकपा (एमाले) का उपाध्यक्ष भीम रावल...</td>
      <td>news</td>
      <td>नेकपा (एमाले) का उपाध्यक्ष भीम रावलले पार्टी अ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>अध्ययन क्षेत्रमा नेपाल–ओमान बीच सहकार्य</td>
      <td>https://ekantipur.com/news/2021/03/25/16166848...</td>
      <td>चैत्र १२, २०७७</td>
      <td>कान्तिपुर संवाददाता</td>
      <td>https://ekantipur.com/author/author-14301</td>
      <td>काठमाडौँ — नेपाल र ओमानका विद्यार्थीहरु बीच ‘क...</td>
      <td>news</td>
      <td>नेपाल र ओमानका विद्यार्थीहरु बीच ‘कृषि र पर्यट...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>ओलीलाई नेपालको प्रतिप्रश्‍न- तपाईंमा पार्टी वि...</td>
      <td>https://ekantipur.com/news/2021/03/25/16166833...</td>
      <td>चैत्र १२, २०७७</td>
      <td>कान्तिपुर संवाददाता</td>
      <td>https://ekantipur.com/author/author-14301</td>
      <td>काठमाडौँ — नेकपा (एमाले)का वरिष्ठ नेता माधवकुम...</td>
      <td>news</td>
      <td>नेकपा (एमाले)का वरिष्ठ नेता माधवकुमार नेपालले ...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>कांग्रेस केन्द्रीय कार्यसमिति बैठक चैत २० गतेल...</td>
      <td>https://ekantipur.com/news/2021/03/25/16166770...</td>
      <td>चैत्र १२, २०७७</td>
      <td>कान्तिपुर संवाददाता</td>
      <td>https://ekantipur.com/author/author-14301</td>
      <td>काठमाडौँ — प्रमुख प्रतिपक्ष दल कांग्रेसको केन्...</td>
      <td>news</td>
      <td>प्रमुख प्रतिपक्ष दल कांग्रेसको केन्द्रीय कार्य...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>कोरोना जोखिम कम गर्न सीसीएमसीलाई स्वास्थ्य मन्...</td>
      <td>https://ekantipur.com/news/2021/03/25/16166738...</td>
      <td>चैत्र १२, २०७७</td>
      <td>कान्तिपुर संवाददाता</td>
      <td>https://ekantipur.com/author/author-14301</td>
      <td>काठमाडौँ — स्वास्थ्य तथा जनसंख्या मन्त्रालयले ...</td>
      <td>news</td>
      <td>स्वास्थ्य तथा जनसंख्या मन्त्रालयले आवश्यक तयार...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>75</th>
      <td>9</td>
      <td>प्रधानमन्त्रीका छोरासहित श्रीलङ्काका २६ जना मन...</td>
      <td>https://gorkhapatraonline.com/international/20...</td>
      <td>चैत्र २१, २०७८ सोमबार</td>
      <td>गोरखापत्र अनलाइन</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>गोरखापत्र अनलाइनकाठमाडौं, चैत २१ गते । श्रीलङ्...</td>
      <td>international</td>
      <td>श्रीलङ्कामा सबैभन्दा चरम आर्थिक सङ्कट व्यवस्था...</td>
    </tr>
    <tr>
      <th>76</th>
      <td>10</td>
      <td>खुम्बुबाट गर्भवति महिलाको उद्धार</td>
      <td>https://gorkhapatraonline.com/health/2022-04-0...</td>
      <td>चैत्र २१, २०७८ सोमबार</td>
      <td>सन्तोष राउत</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>सोलुखुम्बुको खुम्बु पासाङल्हामु गाउँपालिका ३ ब...</td>
      <td>province</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>77</th>
      <td>11</td>
      <td>गाउँठाउँमै सेवा पाउने भएपछि गौशालाबासी खुशी</td>
      <td>https://gorkhapatraonline.com/national/2022-04...</td>
      <td>चैत्र २१, २०७८ सोमबार</td>
      <td>नागेन्द्रकुमार कर्ण</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>महोत्तरी जिल्लाको पश्चिमवर्ती स्थानीय तहका वास...</td>
      <td>province</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>78</th>
      <td>12</td>
      <td>साकेला पार्कमा बाबु पोखरीको शिलान्यास</td>
      <td>https://gorkhapatraonline.com/open/2022-04-04-...</td>
      <td>चैत्र २१, २०७८ सोमबार</td>
      <td>निशा राई</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>धरान ११ स्थित साकेला सांस्कृतिक पार्कमा बाबु प...</td>
      <td>province</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>79</th>
      <td>13</td>
      <td>एकलाख बालबालिकालाई टाइफाइडविरुद्धको खोप</td>
      <td>https://gorkhapatraonline.com/health/2022-04-0...</td>
      <td>चैत्र २१, २०७८ सोमबार</td>
      <td>मुकुन्द सुवेदी</td>
      <td>https://gorkhapatraonline.com/author_news/3</td>
      <td>स्वास्थ्य कार्यालय बर्दियाले जिल्लाका एक लाख ब...</td>
      <td>province</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>9242 rows × 9 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-37195002-5e05-49a5-a8fc-a2b1704c8379')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-37195002-5e05-49a5-a8fc-a2b1704c8379 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-37195002-5e05-49a5-a8fc-a2b1704c8379');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




I made a duplicate of the original dataframe here. The major goal of doing this is that in some cases, if I update a value, the value in the original data changes as well, so I produced a replica of it to keep my original data unchanged.


```python
df = combined_csv.copy()
```

# Open the stopwords.txt file.
Stop words are a collection of terms that are commonly used in any language. Stop words in English include words like "the," "is," and "and." Stop words are used in NLP and text mining applications to remove extraneous terms so that computers may focus on the important ones. The following is how I loaded the stop words file. Because stop words play an important role in news classification, we should eliminate them during preprocessing.

# Stopwords File


```python
stop_file = "/content/drive/MyDrive/News Scraping/News classification/nepali_stopwords.txt"
stop_words = []
with open(stop_file) as fp:
  lines = fp.readlines()
  stop_words =list( map(lambda x:x.strip(), lines))
#stop_words
```

# Punctuation file
# Open the Punctuation file.
The code below is for loading a punctuation file. Punctuation is a set of tools used in writing to clearly distinguish sentences, phrases, and clauses so that their intended meaning may be understood. These tools provide no useful information during categorization, thus they should be eliminated before we train our model.


```python
punctuation_file = "/content/drive/MyDrive/News Scraping/News classification/nepali_punctuation (1).txt"
punctuation_words = []
with open(punctuation_file) as fp:
  lines = fp.readlines()
  punctuation_words =list( map(lambda x:x.strip(), lines))
punctuation_words
```




    [':', '?', '|', '!', '.', ',', '" "', '( )', '—', '-', "?'"]



# Pre-processing of text
I'm only going to utilize the titles of all of my blog's categories. I'll use content to make a blog post there later, despite the enormous quantity of words in the content columns. In this blog, I'll show you how to use Naive Bayes in title data to classify news and categorize it by category.

First, I created a method named 'preprocessing text' in the provided code that accepts data, stop words, and punctuation words as parameters. I made a list called 'new cat' to keep track of the information once I processed it. I also initialized naise, as you can see in the code. Then, within cat data, I use for loop. I isolated the data on cats from the white space, linked them together, and gave them names.




```python
def preprocess_text(cat_data, stop_words, punctuation_words):
  new_cat = []
  noise = "1,2,3,4,5,6,7,8,9,0,०,१,२,३,४,५,६,७,८,९".split(",")
  
  for row in cat_data:
    words = row.strip().split(" ")      
    nwords = "" # []
    
    for word in words:
      if word not in punctuation_words and word not in stop_words:
        is_noise = False
        for n in noise:
          #print(n)
          if n in word:
            is_noise = True
            break
        if is_noise == False:
          word = word.replace("(","")
          word = word.replace(")","")
          # nwords.append(word)
          if len(word)>1:
            nwords+=word+" "
          
    new_cat.append(nwords.strip())
  # print(new_cat)
  return new_cat

title_clean = preprocess_text(["शिक्षण संस्थामा ज जनस्वास्थ्य 50 मापदण्ड पालना शिक्षा मन्त्रालयको निर्देशन"], stop_words, punctuation_words)
print(title_clean)

```

    ['शिक्षण संस्थामा जनस्वास्थ्य मापदण्ड पालना शिक्षा मन्त्रालयको निर्देशन']
    

Here I only take title from our data and apply stops words and punctuations.


```python
ndf = df.copy()
cat_title = []
for i, row in ndf.iterrows():
  ndf.loc[i, "Title"]= preprocess_text([row.Title], stop_words, punctuation_words)[0]

#ndf

```

# Importing Necessary Module for Logistic Regression

* `LogisticRegression` :  We import LogisticRegression from sklearn.linear_model. 
* `CountVectorizer` : Convert a set of text documents into a token count matrix. Using scipy, this approach generates a sparse representation of the counts.

* `train_test_split`: Sklearn model selection has a method called train test split that splits data arrays into two subsets: training data and testing data.


```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import CountVectorizer
```

# Data is split into two sets: train and test.

Our original data was separated into train and test data at this point. Normally, data is partitioned in the proportions of 70% to 30% or 80% to 20%. Model fitting is done with train data, and model prediction is done with test data.


```python

data = pd.DataFrame()

data["text"]=ndf.Title
data["label"]=ndf.Category
data["target"] = data["label"].apply(lambda x: "news" if x=="prabhas-news" else "national" if x=="province" else x)
classes = {c:i for i,c in enumerate(data.target.unique())}
data["target"] = data.target.apply(lambda x: classes[x])


X_train, X_test, Y_train, Y_test = train_test_split(data['text'], 
                                                    data['target'], 
                                                    random_state=0)

vectorizer = CountVectorizer(ngram_range=(1, 2)).fit(X_train)
X_train_vectorized = vectorizer.transform(X_train)
```

.transform(X) creates a 2-D feature matrix from any dict X (mapping feature name to feature values). According to vector math, the 2D matrix is the correct way to enter entries to a classifier.


```python
t = vectorizer.transform(
    [
        'कैलाली, कञ्चनपुर र सुनसरीमा ३० प्रतिशत धानबाली नष्ट',
        'जलविद्युत् आयोजना : सर्वेक्षण इजाजत रोक्नबाट पछि हट्यो सरकार',
        'राष्ट्र बैंकको हस्तक्षेपपछि निक्षेपको ब्याजदर १० प्रतिशतभन्दा कम',
        'गणेशमान सिंह राष्ट्रिय टेनिस कात्तिक ९ गतेदेखि',
        'निर्माणमैत्री कानून बनाउने मन्त्री झाँक्रीको प्रतिवद्धता',
        'टी-२० विश्वकप : पीएनजीलाई ८४ रनले हराउँदै बंगलादेश सुपर १२ मा'
        ])
t
```




    <6x7383 sparse matrix of type '<class 'numpy.int64'>'
    	with 41 stored elements in Compressed Sparse Row format>




# Model Fitting
 We fit Logistic Regression by using train_set of data. We get value of coefficent of determination 92.94% that means model is able to fit only 92.94% of data.


```python

clf = LogisticRegression(random_state=0).fit(X_train_vectorized, Y_train)
prd=clf.predict(t)
predictions = clf.predict(vectorizer.transform(X_test))
clf.score(X_train_vectorized, Y_train)

```




    0.9294440289204687



# Prediction on trained data



```python
nprd = []
for k,v in classes.items():
  for p in prd:
    if v==p:
      nprd.append(k)
nprd
```




    ['news', 'news', 'news', 'news', 'business', 'business']



# Accuracy of Model
Our model accuray is only 77.41% while using Logistic Regression algorithms.


```python

print("Accuracy:", 100 * sum(predictions == Y_test) / len(predictions), '%')
```

    Accuracy: 77.41211667913238 %
    

# Fit Decision Tress


```python
from sklearn import tree
from sklearn.ensemble import RandomForestClassifier

clf = tree.DecisionTreeClassifier()
clf = RandomForestClassifier()
clf.fit(X_train_vectorized, Y_train)

prd=clf.predict(t)
predictions = clf.predict(vectorizer.transform(X_test))
print("Accuracy:", 100 * sum(predictions == Y_test) / len(predictions), '%')
```

    Accuracy: 75.39267015706807 %
    


```python
nprd = []
for k,v in classes.items():
  for p in prd:
    if v==p:
      nprd.append(k)
nprd
```




    ['news', 'news', 'news', 'news', 'news', 'entertainment']




```python

```
