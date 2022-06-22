## TEXT PROCESSING

Text processing adalah suatu proses pengubahan bentuk data yang tidak terstruktur menjadi data yang terstruktur. Dalam proses ini dapat menggunakan case folding, tokenisasi, removal, dan stopword. 

## IMPORT LIBRARY

Untuk melakukan sebuah proses text processing, kita harus mengimport library pandas, numpy, string, dan regex dengan code sebagai berikut.

```python
import pandas as pd
import numpy as np
#Import Library untuk Tokenisasi
import string 
import re #regex library

# import word_tokenize & FreqDist dari NLTK
from nltk.tokenize import word_tokenize 
from nltk.probability import FreqDist
from nltk.corpus import stopwords

from sklearn.feature_extraction.text import CountVectorizer
from sklearn.feature_extraction.text import TfidfVectorizer
```

## READ DATA PTA

Untuk melakukan read data PTA dengan menggunakan code sebagai berikut

```python
dataPTA = pd.read_excel('PTAscrawl.xlsx')
```

## CASE FOLDING

Case folding adalah sebuah proses yang ada di text processing yang berfungsi untuk mengubah seluruh huruf menjadi huruf kecil. 

```python

# gunakan fungsi Series.str.lower() pada Pandas
dataPTA['Abstrak'] = dataPTA['Abstrak'].str.lower()

print('Case Folding Result : \n')

#cek hasil case fold
print(dataPTA['Abstrak'].head(5))
print('\n\n\n')
```

## TOKENIZING

Tokenizing adalah sebuah proses untuk memotong sebuah kata, spasi dan membuang karakter tanda baca.

## STOPWORD REMOVAL

Stopword removal merupakan tahap untuk memilih kata yang dianggap penting. Berikut adalah code nya

```python
def remove_PTA_special(text):
    # menghapus tab, new line, dan back slice
    text = text.replace('\\t'," ").replace('\\n'," ").replace('\\u'," ").replace('\\',"")
    # menghapus non ASCII (emoticon, chinese word, .etc)
    text = text.encode('ascii', 'replace').decode('ascii')
    # menghapus mention, link, hashtag
    text = ' '.join(re.sub("([@#][A-Za-z0-9]+)|(\w+:\/\/\S+)"," ", text).split())
    # menghapus incomplete URL
    return text.replace("http://", " ").replace("https://", " ")
                
dataPTA['Abstrak'] = dataPTA['Abstrak'].apply(remove_PTA_special)

#menghapus nomor
def remove_number(text):
    return  re.sub(r"\d+", "", text)

dataPTA['Abstrak'] = dataPTA['Abstrak'].apply(remove_number)

#menghapus punctuation
def remove_punctuation(text):
    return text.translate(str.maketrans("","",string.punctuation))

dataPTA['Abstrak'] = dataPTA['Abstrak'].apply(remove_punctuation)

#menghapus spasi leading & trailing
def remove_whitespace_LT(text):
    return text.strip()

dataPTA['Abstrak'] = dataPTA['Abstrak'].apply(remove_whitespace_LT)

#menghapus spasi tunggal dan ganda
def remove_whitespace_multiple(text):
    return re.sub('\s+',' ',text)

dataPTA['Abstrak'] = dataPTA['Abstrak'].apply(remove_whitespace_multiple)

# menghapus kata 1 abjad
def remove_singl_char(text):
    return re.sub(r"\b[a-zA-Z]\b", "", text)

dataPTA['Abstrak'] = dataPTA['Abstrak'].apply(remove_singl_char)

print('Result : \n') 
print(dataPTA['Abstrak'].head())
print('\n\n\n')
```

## STEMMING

Stemming merupakan sebuah tahapan yang berfungsi untuk memetakan bentuk dari suatu kata menjadi bentuk kata dasarnya. 

