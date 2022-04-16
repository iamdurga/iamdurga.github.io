---
title:  "Nepali News Classification using Naive Bayes"
date:   2022-05-07 09:29:17 +0545
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
# Naive Bayes for Nepali News Classification
Hello everyone, welcome back to our blog about news classification and in this blog, we are going to explore Naive Bayes for news in our native language Nepali. I started this project nearly a year ago but  I never finished it because I did not know anything about it and I knew only BeautifulSoup from Datacamp. From that knowledge, I was able to scrape some news from Nepali news portal. 

Having an interest in using machine learning on a news content, I enrolled in Coursera's Natural Language Processing Specialization and was able to grasp some of the fundamental concepts of classification algorithms such as Naive Bayes, Logistic Regression, and Decision Tree. Because I've already posted a blog about how I did news scraping, I'll describe how I utilized the Naive Bayes classification method in my data in this blog. The basic goal of utilizing various types of classification algorithms on news data is to be able to classify news into category. Enough of the story, lets get into the main part.

* [Nepali News Scraping] 

## Import Necessary Modules
Lets import some necessary libraries to do classification using Naive Bayes in Python.
* `os` : The OS module in Python provides functions for interacting with the operating system and file systems.
* `pandas` : Working for DataFrame
* `numpy` : For array operation.
* `matplotlib` : For visualization 
* `seaborn` : For more effictive data visualization.
* `warnings` : Warnings is used to supress the warnings.


```python
import os
import pandas as pd
import numpy as np
import warnings
warnings.filterwarnings("ignore")


```

## Load CSV file
Currently the data is in my google drive and also in [this repository](). But I am doing all these ML tasks in my Google Colab so, I will read data from my drive.


Since we have CSV files for each run, we need all of the file's content to be combined before doing a modeling task. I have done following to merge different csv files. I regularly scraped the news these were saved in different csv file in each days. And I combined all csv file for the task.


```python
all_filenames = [i for i in os.listdir("/content/drive/MyDrive/News Scraping/data") if  ".csv" in i and "combined" not in i]
print(all_filenames)
```

    ['2021-03-25.csv', '2021-03-26.csv', '2021-03-27.csv', '2021-03-28.csv', '2021-03-29.csv', '2021-03-30.csv', '2021-03-31.csv', '2021-04-01.csv', '2021-04-03.csv', '2021-04-04.csv', '2021-04-05.csv', '2021-04-06.csv', '2021-04-07.csv', '2021-04-08.csv', '2021-04-12.csv', '2021-04-13.csv', '2021-04-14.csv', '2021-04-15.csv', '2021-04-16.csv', '2021-04-17.csv', '2021-04-18.csv', '2021-04-19.csv', '2021-10-09.csv', '2021-10-10.csv', '2021-10-20.csv', '2021-10-21.csv', '2021-10-22.csv', '2021-10-23.csv', '2021-10-24.csv', '2021-10-25.csv', '2021-10-26.csv', '2021-10-27.csv', '2021-11-21.csv', '2021-11-22.csv', '2021-11-25.csv', '2021-11-28.csv', '2021-11-29.csv', '2021-11-30.csv', '2021-12-05.csv', '2021-12-25.csv', '2022-01-02.csv', '2022-01-04.csv', '2022-01-11.csv', '2022-01-13.csv', '2022-01-18.csv', '2022-03-26.csv', '2022-03-27.csv', '2022-04-04.csv']
    


```python

root = "/content/drive/MyDrive/News Scraping/data/"
```


```python
combined_csv = pd.concat([pd.read_csv(root+f) for f in all_filenames])
combined_csv
```





  <div id="df-f06ae860-a54a-400c-887a-71ebecafd90d">
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
      <button class="colab-df-convert" onclick="convertToInteractive('df-f06ae860-a54a-400c-887a-71ebecafd90d')"
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
          document.querySelector('#df-f06ae860-a54a-400c-887a-71ebecafd90d button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-f06ae860-a54a-400c-887a-71ebecafd90d');
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




In combined csv file there are 9 columns and 9162 rows. Among 9 columns columns names are Title, URL, Date, Author, Author URL, Content, Category, Description and so on.

Here I created copy of original dataframe. The main objective of doing so is, in some case if we changed some value, this value will be also changed in original data so inorder to keep our original data unchanged, we created copy of it.


```python
df = combined_csv.copy()
```

## Load stopwords file
Stop words are a group of terms that are regularly employed in any language. The words "the," "is," and "and" are all examples of stop words in English. Stop words are used in NLP and text mining applications to remove unnecessary terms, allowing programs to focus on the important words instead. I loaded stop words file in following way. Stop words contribute valueable role while doing news classification so we should remove them while doing preprocessing. And for the Nepali Stopwords, I found a text file online about it. Common repeating words in Nepali are like `आदि` I am sorry for not remembering the real author of it. Also this is in my drive as well.




```python
stop_file = "/content/drive/MyDrive/News Scraping/News classification/nepali_stopwords.txt"
stop_words = []
with open(stop_file) as fp:
  lines = fp.readlines()
  stop_words =list( map(lambda x:x.strip(), lines))
#stop_words
```

## Load Punctuation file
Following code is for loading punctuation file. Punctuation refers to the characters used in writing to separate sentences, phrases, and clauses so that their intended meaning is clear. These characters do not give valuable meaning while doing classification so we should removed before fitting our model.


```python
punctuation_file = "/content/drive/MyDrive/News Scraping/News classification/nepali_punctuation (1).txt"
punctuation_words = []
with open(punctuation_file) as fp:
  lines = fp.readlines()
  punctuation_words =list( map(lambda x:x.strip(), lines))
punctuation_words
```




    [':', '?', '|', '!', '.', ',', '" "', '( )', '—', '-', "?'"]






```python

```

## Using Title
### Text pre-processing
I'm only going to use the titles of all the news in first part and see the outcome. In first part of this blog, I'll discuss how to classify news using Naive Bayes in title data and categorize them into category.

First, in the given code, I wrote a method called `preprocess_text` that takes data, stop words, and punctuation words as parameters. Then, I created a list called `new_cat` to hold it. As can be seen in the code, I also initialized noise as numbers. Then for each words in the each sentence, I did:
* If word is not in punctuation or stop words then,
* Do not take this word if it contains noise characters.
* Remove parenthesis



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
    

We can see in the result above that the single letter ज is removed as well as 50.

Now making a new dataframe to do processing of text and use it later on.


```python
ndf = df.copy()
cat_title = []
for i, row in ndf.iterrows():
  ndf.loc[i, "Title"]= preprocess_text([row.Title], stop_words, punctuation_words)[0]

#ndf

```

### Import Necessary module for Multinomial Naive Bayes

* `CountVectorizer` : Convert a set of text documents into a token count matrix. Using scipy, this approach generates a sparse representation of the counts.
* `train_test_split`: Sklearn model selection has a method called train test split that splits data arrays into two subsets: training data and testing data.
* `MultinomialNB`: The multinomial Naive Bayes classifier is good for discrete feature classification (e.g., word counts for text classification). Normally, integer feature counts are required for the multinomial distribution.
* `unique_labels`: Extract an ordered array of unique labels.





```python

from sklearn.feature_extraction.text import CountVectorizer
from sklearn.model_selection import train_test_split
from sklearn.naive_bayes import MultinomialNB
from sklearn.utils.multiclass import unique_labels




```

### Splitting Data into Train and Test set

Here we split our original data into train and test data. Normally data partition are done in the ratio of 70% and 30% or 80% and 20%. Train data are used for model fitting and test data are used while doing model prediction. But before that, we will merge two similar categories into one and also assign a unique label for each class.


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

### Model Fitting
 We fit MultinomialNB by using train_set of data. We get value of coefficent of determination 79.12% that means the model is able to fit only 79.12% of data.


```python
model = MultinomialNB(alpha=0.1)
model.fit(X_train_vectorized, Y_train)
model.score(X_train_vectorized, Y_train)
```




    0.7912278170538162




```python

```

### Our Hardcoded Accuracy



```python
predictions = model.predict(vectorizer.transform(X_test))
print("Accuracy:", 100 * sum(predictions == Y_test) / len(predictions), '%')
```

    Accuracy: 78.23453050627434 %
    


```python
model.classes_, classes
```




    (array([0, 1, 2, 3, 4, 5, 6, 7]),
     {'business': 1,
      'entertainment': 7,
      'international': 5,
      'national': 4,
      'news': 0,
      'sports': 3,
      'technology': 6,
      'world': 2})



In news classification there are 8 categories. Category with crossponding value is given below.

* 0 is indicating 'news'
* 1 is indicating 'business'
* 2 is indicating 'world'
* 3 is indicating 'sports'
* 4 is indicating 'national'
* 5 is indicating 'international'
* 6 is indicating 'technology'
* 7 is indicating 'entertainment'

### Prediction on Untrained Data
Following is the code for untrained data let us check given Nepali text in already build model. And observed how much well it performed.


```python
prd = model.predict(vectorizer.transform(
    [
        'कैलाली, कञ्चनपुर र सुनसरीमा ३० प्रतिशत धानबाली नष्ट',
        'जलविद्युत् आयोजना : सर्वेक्षण इजाजत रोक्नबाट पछि हट्यो सरकार',
        'राष्ट्र बैंकको हस्तक्षेपपछि निक्षेपको ब्याजदर १० प्रतिशतभन्दा कम',
        'गणेशमान सिंह राष्ट्रिय टेनिस कात्तिक ९ गतेदेखि',
        'निर्माणमैत्री कानून बनाउने मन्त्री झाँक्रीको प्रतिवद्धता',
        'टी-२० विश्वकप : पीएनजीलाई ८४ रनले हराउँदै बंगलादेश सुपर १२ मा'
        ])
            ) 
nprd = []
for k,v in classes.items():
  for p in prd:
    if v==p:
      nprd.append(k)
nprd
```




    ['news', 'business', 'business', 'business', 'business', 'international']



In above 6 titles, a best category to each are, Business, Business, Business, Sports, News, Sports. And the model is not performing well but still we can make some analogy out of it.

## Using News Content
Lets repeat above steps for the content rather than title.


```python
ndf = df.copy()
cat_title = []
for i, row in ndf.iterrows():
  try:
    ndf.loc[i, "Content"]= preprocess_text([row.Content], stop_words, punctuation_words)[0]
  except:
    print(row.Content)
ndf=ndf[~pd.isna(ndf.Content)]

```

    nan
    nan
    


```python
data = pd.DataFrame()

data["text"]=ndf.Content
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


```python
model = MultinomialNB(alpha=0.1)
model.fit(X_train_vectorized, Y_train)
model.score(X_train_vectorized, Y_train)
```




    0.7776655605251768




```python
predictions = model.predict(vectorizer.transform(X_test))
print("Accuracy:", 100 * sum(predictions == Y_test) / len(predictions), '%')
```

    Accuracy: 76.11423626135871 %
    


```python
prd = model.predict(vectorizer.transform(
    [
        'कैलाली, कञ्चनपुर र सुनसरीमा ३० प्रतिशत धानबाली नष्ट',
        'जलविद्युत् आयोजना : सर्वेक्षण इजाजत रोक्नबाट पछि हट्यो सरकार',
        'राष्ट्र बैंकको हस्तक्षेपपछि निक्षेपको ब्याजदर १० प्रतिशतभन्दा कम',
        'गणेशमान सिंह राष्ट्रिय टेनिस कात्तिक ९ गतेदेखि',
        'निर्माणमैत्री कानून बनाउने मन्त्री झाँक्रीको प्रतिवद्धता',
        'टी-२० विश्वकप : पीएनजीलाई ८४ रनले हराउँदै बंगलादेश सुपर १२ मा'
        ])
            ) 
nprd = []
for k,v in classes.items():
  for p in prd:
    if v==p:
      nprd.append(k)
nprd
```




    ['news', 'business', 'world', 'sports', 'sports', 'national']



The results using Content is even poorer than the title so lets see if it is happening because of the categories being similar to each others. Next we will try to use only 2 categories.


```python

```

## What Happens if we take only two categories?


```python

ndf = df.copy()
cat_title = []
for i, row in ndf.iterrows():
  try:
    ndf.loc[i, "Content"]= preprocess_text([row.Content], stop_words, punctuation_words)[0]
  except:
    print(row.Content)
ndf=ndf[~pd.isna(ndf.Content)]


data = pd.DataFrame()

data["text"]=ndf.Content
data["label"]=ndf.Category
data = data[data.label.isin(["business", "sports"])]
data["target"] = data["label"].apply(lambda x: "news" if x=="prabhas-news" else "national" if x=="province" else x)
classes = {c:i for i,c in enumerate(data.target.unique())}
data["target"] = data.target.apply(lambda x: classes[x])



X_train, X_test, Y_train, Y_test = train_test_split(data['text'], 
                                                    data['target'], 
                                                    random_state=0)

vectorizer = CountVectorizer(ngram_range=(1, 2)).fit(X_train)
X_train_vectorized = vectorizer.transform(X_train)

model = MultinomialNB(alpha=0.1)
model.fit(X_train_vectorized, Y_train)
print(f"Score is {model.score(X_train_vectorized, Y_train)}")

predictions = model.predict(vectorizer.transform(X_test))
print("Accuracy:", 100 * sum(predictions == Y_test) / len(predictions), '%')

prd = model.predict(vectorizer.transform(
    [
        'कैलाली, कञ्चनपुर र सुनसरीमा ३० प्रतिशत धानबाली नष्ट',
        'जलविद्युत् आयोजना : सर्वेक्षण इजाजत रोक्नबाट पछि हट्यो सरकार',
        'राष्ट्र बैंकको हस्तक्षेपपछि निक्षेपको ब्याजदर १० प्रतिशतभन्दा कम',
        'गणेशमान सिंह राष्ट्रिय टेनिस कात्तिक ९ गतेदेखि',
        'निर्माणमैत्री कानून बनाउने मन्त्री झाँक्रीको प्रतिवद्धता',
        'टी-२० विश्वकप : पीएनजीलाई ८४ रनले हराउँदै बंगलादेश सुपर १२ मा'
        ])
            ) 
nprd = []
for k,v in classes.items():
  for p in prd:
    if v==p:
      nprd.append(k)
nprd
```

    nan
    nan
    Score is 0.9772055719712959
    Accuracy: 96.9620253164557 %
    




    ['business', 'business', 'business', 'business', 'sports', 'sports']




```python

```
