---
author: "Bart"
title: "The PLot Classifier"
date: 2020-08-26T12:00:06+09:00
description: "(Summer project) Identifiying chart/plot name from images with deep learning "
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- coding
- Data Science
- Deep Learning
tags: 
- Visualization
- Data
- Python
- Machine Learning
- Deep Learning
- Transfer learning
series:
- Data Science
- Projects
libraries:
- mathjax
image: images/logoTPC.png
---
# The Plot Classifier

<figure>
  <img src="/images/logoTPC.png"  />
</figure>
(Yeah I designed the logo too! Does it count as artistic design knowledge? :P)

## Repository
All this info and more can be found [at the repo](https://github.com/thebooort/The-Plot-Classifier)

## Any serious aspect you might find in this repo is purely coincidental

Hey! the tool you don't even know you need! 

(Silly summer project to know the name of that cool plot/chart/visualization you saw on a webpage)

## Index

- [Motivation](#motivation)
- [Approach](#approach)
  - [Data Collect](#data-collect)
  - [ML Approach](#ml-approach)
	- [Neural Net architecture](#nn-architecture)
	- [Results](#results)
    - [Nets trained you can find here](#nets-trained)
  - [Streamlit](#streamlit)
	  - [Screenshots](#screenshots)
  - [Heroku](#heroku-deployment)



## Motivation 

This project was born from a personal doubt that I have come across several times: What is the name of that cool graphic? 
And I've always lost some time in finding the exact name or the way to call it of some bookstores. It is true that I talk about more complex graphics, but I decided that it could be interesting to start with the basics and perhaps at some point the tool can help some beginner to discover their first graphics. 

In addition, the main reason for this project was to try and play with the possibilities offered by streamlit as a way of providing a preliminary result in machine learning. In that aspect I think it has been a success, since I have acquired what is necessary to make an attractive and functional streamlit page with a model that I have implemented. 

## Approach

### Data collect

I didn't find anything usable on the internet. So I thought of two alternatives, one to generate my own graphics and the other to get them from some search engine. 

Generating my own graphics seemed very interesting and maybe in the future I will feed the system with randomly generated graphics, however I think that the investment of time would not be rewarded, as the options are endless.

On the contrary, I made the decision to get a group of images from the internet, using the search engines. Obiously the quality of the images (and I don't mean their quality in pixels) would decrease as the amount of images to extract from a single query search increases. I reached a middle point where most of the extracted images match the query text. 

Finally I reviewed the 14 groups of graphics selected in this initial version of the application and eliminated some of the erroneous images I found.

The final data set was not very large. During the pre-processing I tried the data augmentation, but the difference in quantity was not going to be very big. The solution for this is explained in the next section.

### ML approach

Although machine learning is essential for this project, as I explained in the motivations section, it was not the final goal.  Therefore I had to be careful with the development of it, to balance effort and result.

I decided to use Keras for this purpose. I have interest in other libraries but Keras was the one I used the most, this guaranteed familiarity with the process. 

Despite this, generating a good image multi-sorting engine is not an easy task. Even less having so many categories (with many possible options) and so little data for training. 

I decided as an intermediate solution to use a pre-trained network and perform transfer learning. That is, take a pre-trained neural network and add some final layers that classify according to my categories. 

To choose the neural network to use, I simply looked for the one that was giving better results and that was not a bestiality. I found MObilnet from Google and it was just what I was looking for: "Designed to effectively maximize accuracy while being mindful of the restricted resources for an on-device or embedded application. MobileNets are small, low-latency, low-power models parameterized to meet the resource constraints of a variety of use cases. They can be built upon for classification, detection, embeddings and segmentation similar to how other popular large scale models, such as Inception, are used".

The network weighed very little and I could retrain it very easily, to get good results with minimal effort.

#### NN architecture

You can check the neural net arcxhitecture [here](https://github.com/thebooort/The-Plot-Classifier/blob/master/images/model.png)

#### Results
First the model loss:
<figure>
  <img src="/images/loss.png"  />
</figure>

And the accuracy reached.
<figure>
  <img src="/images/accuracy.png"  />
</figure>



#### Nets Trained

In the project repo I have 3 `.h5` archives with weights for you to experiment with: 

- `keras_model.h5`: Trained with google services with no curated dataset (used at the very beginning)
- `per_trained.h5`: Trained with transfer learning, data augmentation, all images curated, and all images used(no validation).
- `per_trainedv2.h5`: Same of above, but with validation images.

### Streamlit dev

#### Screenshot

When you enter the app you a see a brief description and a menu to upload the photo

<figure>
  <img src="/images/screenshot.jpg"  />
</figure>

After that, the photo is classified (with a loading menu) an then it tells you the name, some other examples and some links to coding libraries that make it .

<figure>
  <img src="/images/screenshot2.jpg"  />
</figure>


### Heroku deployment 

I finally ended deploying this app with Heroku. I used [another repository](https://github.com/thebooort/TPC-heroku) for that task and follow [this tutorial for that](https://gilberttanner.com/blog/deploying-your-streamlit-dashboard-with-heroku). Here you can play with the app and its limits. I hope that in some near future I may have time to upgrade and improve, but in the meantime it was a funny and educative project.

Here you have! (It takes a little bit to load!)
### [THE PLOT CLASSIFIER TOOL](https://the-plot-classifier.herokuapp.com/)
