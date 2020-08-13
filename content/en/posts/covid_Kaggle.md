---
author: "Bart"
title: "COVID19 research paper recommendation engine"
date: 2020-03-28T12:00:06+09:00
description: "COVID19 Kaggle Challenge: Construyendo un recomendador de artículos sobre COVID19"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- Kaggle
- Data Science
- RecSys
- coding
tags: 
- Kaggle
- Coding
- Data Science
- COVID19
- Python
- Machine Learning
- Recommedation Systems
series:
- RecSys
libraries:
- Flourish
- mathjax
image: images/covid_plot/kaggle.png
---

# COVID19 Kaggle Challenge

Dentro de los challenges lanzados por Kaggle para usar los datos publicados del COVID19, los doctorandos que compartimos directora de tesis nos juntamos para probar ideas y aprender lo que pudiésemos en el camino. 

Había varios retos o tareas en las que podíamos embarcarnos, pero como nuestro interés era más bien académico, decidimos empezar haciendo un análisis exploratorio de datos y clusterización. Y desde ahí, lo que quisiésemos o nos diese tiempo. 

Los resultados que véis aquí corresponden a un enfoque muy sencillo y básico de aplicación de técnicas de machine learning para crear un recomendador de artículos científicos relacionados con uno seleccionado por el usuario. 

El objetivo es usar los titulos y abstracts de los artículos para extraer "de qué van". Una vez obtenido esto, se buscan artículos que traten temas similares.

Para ello seguimos estos pasos: 
- EDA
- Text Preprocessing
- Tokenization
- vectorization
- LDA and Topic Extraction
- Recommendation system

Si quereis echarle un vistazo a el notebook (aunque esta desordenado): https://www.kaggle.com/thebooort/covid19-exploration-and-paper-recommendation

Este post pretende presentar los principales resultados del notebook (hasta que encuentre una forma de subir los notebooks enteros), omitiré trozos de código que considere poco importantes. 

## EDA

En este aspecto, trabajando con abstract y texto, tendremos que saber cuantas palabras realmente van a entrar a nuestro sistema. Para ello una diagramas de cajas puede sernos útil:

``` python
df[['abstract_word_count']].plot(kind='box', title='Boxplot of Word Count', figsize=(10,6))
plt.show()

df[['body_word_count']].plot(kind='box', title='Boxplot of Word Count', figsize=(10,6))
plt.show()
```


![Example image](/images/covid_plot/boxq.jpg)

![Example image](/images/covid_plot/box1.jpg)

Además, una nube de palabras tambien puede darnos una idea aproximada de qué palabras tienen importancia (tanto aquellas que son importante como las que no).



``` python
for key in ['abstract','title','full_text']:
    total_words = df[key].values
    wordcloud = WordCloud(width=1800, height=1200).generate(str(total_words))
    plt.figure( figsize=(30,10) )
    plt.title ('Wordcloud' + key)
    plt.imshow(wordcloud)
    plt.axis("off")
    plt.show()
```


![Example image](/images/covid_plot/cloud1.png)
![Example image](/images/covid_plot/cloud2.png)
![Example image](/images/covid_plot/cloud3.png)


## Tokenización
Para esta seccion siguiendo un código de ajrwhite, usamos scapy. La idea es tokenizar el texto, no solo para esta parte, si no para cualquier analisis o algoritmo posterior, quedandonos con un texto depurado y palabras que realmente sean importante para etiquetar, clasificar, o mdelizar estos textos. 


``` python
# importamos scispacy un paquete para trabajar spaCy con textos científicos y usamos el modelo
# en_core_sci_md que contine pipeline de spacy especifica para textos biomédicos (50k palabras)
import en_core_sci_md
nlp = en_core_sci_md.load(disable=["tagger", "parser", "ner"])
nlp.max_length = 2000000
```

Del word cloud tenemos algunas sugerencias de stop words que no son relevantes en nuestro análisis.
Añadiéndolas lanzamos finalmente la tokenizacion y la aplicamos sobre nuestras columnas de texto.


``` python
customize_stop_words = [
    'doi', 'preprint', 'copyright', 'peer', 'reviewed', 'org', 'https', 'et', 'al', 'author', 'figure', 
    'rights', 'reserved', 'permission', 'used', 'using', 'biorxiv', 'fig', 'fig.', 'al.',
    'di', 'la', 'il', 'del', 'le', 'della', 'dei', 'delle', 'una', 'da',  'dell',  'non', 'si','elsevier',
    'unrestricted', 'grant', 'repository', 'original', 'acknowledgement', 'permission', 'centre']
for w in customize_stop_words:
    nlp.vocab[w].is_stop = True
    
stop_words = nlp.Defaults.stop_words
# definimos el tokenizador con las stopwords 
def spacy_tokenizer(sentence):
    return [word.lemma_ for word in nlp(sentence) if not (word.like_num or word.is_stop or word.is_punct or word.is_space or len(word)==1)]
# aplicar tokenizacion
df['full_text'] = df['full_text'].apply(spacy_tokenizer)
df['abstract'] = df['abstract'].apply(spacy_tokenizer)
df['title'] = df['title'].apply(spacy_tokenizer)
# eliminar espacios
df['full_text'] = df['full_text'].apply(lambda x: ' '.join(x))
df['abstract'] = df['abstract'].apply(lambda x: ' '.join(x))
df['title'] = df['title'].apply(lambda x: ' '.join(x))

```



## Vectorización

Vamos a vectorizar nuestra información textual ( esto es, transformar las palabras en vectores numéricos). Para ello podemos usar CountVectorizer o TF-IDF entre otros. Usé estos dos por simpleza, pero CountVectorizer me dió mejores resultados (CountVectorizer esencialmente vectoriza la palabra contando la frecuencia de repetición de esa palabra en los títulos o en los abstracts).

Importando sklearn usar cualquiera de estos dos algoritmos es muy sencillo. Además, podemos añadir el tokenizador que queramos, en este caso el que hemos construido con spacy.

``` python
features  = 10000
tf_vectorizer = CountVectorizer(max_features=features,tokenizer = spacy_tokenizer, min_df=10)
X_tf = tf_vectorizer.fit_transform(df['abstract'])
tf_feat_name = tf_vectorizer.get_feature_names()
```

## LDA
LDA es  basciamente un método estadístico que busca encontrar una combinación lineal de rasgos que caracterizan o separan dos o más clases de objetos o eventos. La combinación resultante la podemos utilizar para separar nuestros textos en grupos y obtener qué palabras aparecen con más frecuencia dentro de esos grupos, a fin de caracterizarlos. 

``` python
topics = 7
lda_model = LatentDirichletAllocation(learning_method='online',random_state=20,n_components=topics)
lda_output =lda_model.fit_transform(X_tf)
```

## Resultado final del LDA
Para visualizar LDA a parte de obtener los topics, usé pyLDAvis. pyLDAvis es una biblioteca de Python para visualización interactiva de topic models (basada en el paquete R de Carson Sievert y Kenny Shirley).

Como dicen en su web pyLDAvis está diseñado para ayudar a los usuarios a interpretar los topics en un modelo de topics que se ha ajustado a un corpus de datos textuales. El paquete extrae la información de un modelo de topics LDA ajustado, para ofrecer una visualización interactiva.

Os lo recomiendo.

``` python
# preparing for plotting pyLDAvis
%matplotlib inline
pyLDAvis.enable_notebook()
```


La visualización está diseñada para ser utilizada en cualquier notebook, pero también se puede guardar en un archivo HTML independiente para compartir fácilmente:
``` python
pyLDAvis.sklearn.prepare(lda_model, X_tf, tf_vectorizer)
# if you want to save it 
# P=pyLDAvis.sklearn.prepare(lda_model, X_tf, tf_vectorizer)
# pyLDAvis.save_html(p, 'lda.html')
```

<iframe width="100%" height="700" src="/images/covid_plot/lda.html">
</iframe>

Podéis consultar el resultado como una página aparte aqui: https://thebooort.github.io/covizzz19/ , así os quitáis de problemas si estáis viendo este blog como theme oscuro. 

## Visualizando las temáticas

Las temáticas finales obtenidas fueron: 

```
Topic 0 ['protein', 'rna', 'proteins', 'activity', 'cell', 'replication', 'antiviral']
Topic 1 ['infection', 'cell', 'immune', 'infected', 'mice', 'response', 'induced', 'expression']
Topic 2 ['respiratory', 'pcr', 'samples', 'detection', 'viruses', 'assay', 'using', 'positive']
Topic 3 ['diseases', 'disease', 'review', 'development', 'health', 'research', 'based', 'new', 'use', 'infectious']
Topic 4 ['patients', 'calves', 'il', 'group', 'associated', 'days', 'cats', 'clinical', 'age']
Topic 5 ['cov', 'sars', 'protein', 'coronavirus', 'sequence', 'mers', 'human', 'genome', 'viruses']
Topic 6 ['health', 'influenza', 'risk', 'data', 'cases', 'disease', 'outbreak']
```

Podemos estudiar las correlaciones entre las puntuaciones de los topics de cada paper:

```python
# plotting results
import seaborn as sns
sns.heatmap(abs(ldadf[columns].corr()),annot=True)
plt.title(" Correlation Plot")
```
Obtenemos una correlación baja entre topics, lo que implica que nuestra clusterizacion (si bien mejorable) no es mala. 


## Recomendaciones


Para obtener la recomendacion final, bastará con comparar las componentes que identifican a cada paper. Seleccionado uno cualquiera, calcularemos la distancia con el resto de papers y devolveremos los mas cercanos. Esta distancia la podemos definir como queramos: RMSE, Cosine similarity, etc. 

```python
from sklearn.metrics.pairwise import cosine_distances
from math import sqrt
def paper_recommendation_tool(selected_paper_id):
    selected_paper = df_total[(df_total['paper_id']==selected_paper_id)]
    dominant_topic = int(selected_paper['Major_topic'])
    # we create another df with papers evaluation
    recommended_papers = df_total
    recommended_papers = recommended_papers.drop(selected_paper.index)
    x= selected_paper[columns].values.tolist()
    y= recommended_papers[columns].values.tolist()
    for indice_fila, fila in recommended_papers.iterrows():
        distance = cosine_distances(x[0],y[indice_fila-1])
    recommended_papers['distance'] = distance
    recommended_papers = recommended_papers[['paper_id','title','distance','Major_topic']].sort_values('distance').head(10)
    return dominant_topic, recommended_papers

```




Probamos un caso concreto
```python
# Example: we are interested in 4602afcb8d95ebd9da583124384fd74299d20f5b, because his use of SPINT2
dominant_topic, recommended_papers = paper_recommendation_tool('4602afcb8d95ebd9da583124384fd74299d20f5b')
print(dominant_topic)
print(recommended_papers)
```























