## TOPIC MODELLING - LSA

Topic Modelling merupakan suatu proses yang berfungsi untuk menganalisis sekumpulan data teks dan mengelompokkannya menjadi beberapa topik. 

LSA merupakan sebuah cara yang berfungsi untuk mengekstraksi tulisan dari dokumen teks.

## TAHAPAN - TAHAPAN LSA

Berikut adalah tahapan-tahapan dari LSA

### TF-IDF

Dalam tf-idf menggunakan matrix dimana mxn yang digunakan dalam kata pada sebuah dokumen. Berikut adalah rumus dari tf-idf
$$
W_{i,j}=tfi,j\times \log \dfrac{N}{dF}
$$
tfi,j= term dari dokumen

N=Total dokumen

Df j= Dokumen

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

## MENAMPILKAN SVD

SVD merupakan suatu pemfaktoran yang dilakukan dengan cara melakukan penguraian suatu matriks kedalam dua matriks. Berikut adalah implementasi SVD kedalam python sebagai berikut.

```python
from sklearn.decomposition import TruncatedSVD
lsa_model = TruncatedSVD(n_components=10, algorithm='randomized', n_iter=10, random_state=42)

lsa_top=lsa_model.fit_transform(vect_text)
```

```python
l=lsa_top[0]
print("Document 0 :")
for i,topic in enumerate(l):
  print("Topic ",i," : ",topic*100)
```

```python
print(lsa_model.components_.shape) # (no_of_topics*no_of_words)
print(lsa_model.components_)
```

## MENGEKSTRAK TOPIC DAN TERM

Dalam proses ini kita melakukan ekstrak topic sebanyak 10 topik dengan code sebagi berikut.

```python
print(lsa_model.components_.shape) # (no_of_topics*no_of_words)
print(lsa_model.components_)
```

