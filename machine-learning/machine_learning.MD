# Machine Learning

## Data Preprocessing

### Reading Data

#### Files
```python
import pandas as pd

df = pd.read_excel("/path/to/excel.xlsx")
df = pd.read_csv("/path/to/csv_file.csv")
```
#### Database
```python
import pandas as pd
from sqlalchemy import create_engine

engine = create_engine("mysql+mysqldb://user:password@localhost/database_name")
connection = engine.connect()

df = pd.read_sql_query("SELECT * FROM table_name", connection)

connection.close()
```

### Cleaning Data

```python
import pandas as pd
import re
import nltk
nltk.download('stopwords')

### Clean text columns

stop_words = nltk.corpus.stopwords.words('english')
porter_stemmer = nltk.PorterStemmer()

def clean_data(text):
    text = text.lower().strip()
    text = re.sub("[^0-9A-Za-z ]","", text)
    clean_text = ""
    for word in text.split(" "):
        if(word not in stop_words):
            clean_text += porter_stemmer.stem(word) + " "
    return clean_text[:-1]

df = pd.read_excel("/path/to/excel.xlsx")
df['text_col'] = df['text_col'].apply(clean_data)

### Remove rows with null values

df.dropna(inplace=True,ignore_index=True)

### Normalizing Numeric Columns

df['num_col'] = (df['num_col']-df['num_col'].min())/df['num_col'].std()                         # Mean Normalization
df['num_col'] = (df['num_col']-df['num_col'].min())/(df['num_col'].max()-df['num_col'].min())   # MinMax Normalization
```

## Data Modeling and Evaluation

### Supervised Learning

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
from sklearn.metrics import f1_score

df = pd.read_excel("/path/to/excel.xlsx)")
classifier = DecisionTreeClassifier(criterion='entropy', max_depth=5)

## Preprocessing done here ...

X_train, X_test, y_train, y_test = train_test_split(df.drop(['label'], axis=1), df['label'], test_size=0.33)
classifier.fit(X_train, y_train)

## Prediction
y_pred = classifier.predict(X_test)

## Evaluation
accuracy = accuracy_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)
```

### Unsupervised Learning

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.cluster import DBSCAN
from sklearn.metrics import silhouette_score

df = pd.read_excel("/path/to/excel.xlsx)")

## Preprocessing done here ...

clustering = DBSCAN(eps=3, min_samples=2).fit(df)

labels = clustering.labels_

## Evaluation
silhouette = silhouette_score(df, labels)
```

## Data Visualization

```python
import panads as pd
import matplotlib.pyplot as plt

df = pd.read_excel("/path/to/excel.xlsx")

## Preprocessing done here ...

df.plot()
# df.plot.bar()
plt.show()
```

## HyperParameter Optimization

### Supervised Learning

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
from sklearn.metrics import f1_score

df = pd.read_excel("/path/to/excel.xlsx)")

## Preprocessing done here ...

X_train, X_test, y_train, y_test = train_test_split(df.drop(['label'], axis=1), df['label'], test_size=0.33)

optimal_f1 = None
optimal_depth = None

for depth in range(0,10):
    classifier = DecisionTreeClassifier(criterion='entropy', max_depth=depth)
    classifier.fit(X_train, y_train)

    y_pred = classifier.predict(X_test)
    f1 = f1_score(y_test, y_pred)

    if(optimal_f1 is None):
        optimal_f1 = f1
        optimal_depth = depth
    else:
        if(f1 > optimal_f1):
            optimal_f1 = f1
            optimal_depth = depth

optimal_model = DecisionTreeClassifier(criterion='entropy', max_depth=optmal_depth)    
```

### Unsupervised Learning
```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.cluster import DBSCAN
from sklearn.metrics import silhouette_score

df = pd.read_excel("/path/to/excel.xlsx)")

## Preprocessing done here ...

max_silhouette_score = None
optimal_eps = None
optimal_min_samples = None

for eps in range(0,10):
    for min_samples in range(0,10):
        clustering = DBSCAN(eps=eps, min_samples=min_samples).fit(df)
        labels = clustering.labels_
        silhouette = silhouette_score(df, labels)

        if(max_silhouette_score is None):
            max_silhouette_score = silhouette
            optimal_eps = eps
            optimal_min_samples = min_samples
        else:
            if(silhouette > max_silhouette_score):
                max_silhouette_score = silhouette
                optimal_eps = eps
                optimal_min_samples = min_samples

optimal_model =  DBSCAN(eps=optimal_eps, min_samples=optimal_min_samples).fit(df)
```