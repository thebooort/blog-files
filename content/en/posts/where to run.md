---
author: "Bart"
title: "Where to run after confinement?"
date: 2020-04-30T12:00:06+09:00
description: "Analyzing Strava data to know where to run with less human contact"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- coding
- Data Science
tags: 
- Visualization
- Data
- Python
- Running
series:
- Data Science
libraries:
- mathjax
image: images/run.png
---

<figure>
  <img src="/images/run2.png"  />
</figure>

# We can go for a quick run, but... where?
From now on (technically May 2nd), in Spain (specifically in my city Granada), we are allowed to go for a quick run or walk in the morning. Those are really good news for every runner and trail runner I know, but with great power comes great responsability.

My main concern about going outside for a quick run is how many people will I encounter while running. The social distance that we should keep between other dramatically increase when practicing sports, [as this article of urban physiscs says](http://www.urbanphysics.net/COVID19_Aero_Paper.pdf):

*On the basis of these results the scientist advises that for walking the distance of people moving in the same direction in 1 line should be at least 4–5 meter, for running and slow biking it should be 10 meters and for hard biking at least 20 meters. Also, when passing someone it is advised to already be in different lane at a considerable distance e.g. 20 meters for biking.*

<figure>
  <img src="/images/run3.png"  />
  <figcaption>
      <h7>Image from: Towards aerodynamically equivalent COVID-19 1.5 m social distancing for walking and running. Blocken,B. et al (2019-Preprint)</h7>
  </figcaption>
</figure>

After reading all the information, next step is to enumerate all the parameters I have to take into account when designing a gps track for run training.: 

- I think it can be quite hard to take into account the running distance (10 meters can be hard to estimate while constant movement). Furthermore if you add more people to the equation, complexity increases exponentially (well, this need to be proven, but you get the point :tongue:). So my main idea is to go for a run quite early in the morning or quite late in the night, trying to minimize the number of people that can be affected by my exercises (or that can affects my health).

- Other thing to take into account is that there is not distance limit within the city, so I have the entire city to choose where to go, that is really great for me as I don't like to run in circle multiples times. The final running track then, can be reaching one point and coming back or some kinf of circular track.

- No more than 5-6 kilometers the first day (we need to take it easy those first days!).

The first point of these is the one harder to analyze:
As there is no distance limits,I really think there will be probably tons of people running along their old and known tracks (I was thinking about it myself, because running in a familiar route is easier and you can adjust your exercise according to how you feel/your pace/your goals, etc), so if I want to avoid them I just have to choose those streets with less "runner-traffic". 

How do I do that? Well well,let's use some data science on it! 

## Getting the data 

I made some research about public datasets available about mobility inside my city. However (big ironic surprise) there is not a single data about mobility. So I had to change my strategy. 

### Strava
Raw data for this task is very hard to obtain. I remembered that [Strava published a global heatmap](https://www.strava.com/heatmap#7.00/-120.90000/38.36000/hot/all) with useful information. This heatmap shows 'heat' made by aggregated, public activities over the last two years, classified by sport and it is updated monthly. This address two points: been able to use the data now, and bee able to adjust my conclusions in a month if anything changes. 

<figure>
  <img src="/images/maparun.png"  />
  <figcaption>
      <h7>Strava map (accessed April 30)</h7>
  </figcaption>
</figure>

Sadly, I only can get visual information from it. You are forced to purchase an app create by strave to get all the data, and I am not that rich (or have time to fight with bureocracy to get a deal). If any of you knows any interesting dataset related to this task, please let me know!

<figure>
  <img src="/images/mapa_granada.png"  />
  <figcaption>
      <h7>Strava map (accessed April 30)</h7>
  </figcaption>
</figure>

### Garmin

Garming offers another similar heatmap. I first talk about Strava because, as far as I am concern, to check the Garmin heatmap you need to be registered and have a Garmin dispositive. 

The map can be consulted at you personal account. The main difference (strictly for me ) is that Garmin allow me to mark a track while I am consulting the map, and upload this GPS track to my watch.
For that reason I am going to use primarly Garmin data, but in this post y also analyze Strava data-  

## Analyzing the data

### Strava 
I live near *calle San Juan de Dios* so I will set my start goal over there. I zoom into the map to see what I have near my spot:
<figure>
  <img src="/images/run71.png"  />
  <figcaption>
      <h7>Strava map (accessed April 30)</h7>
  </figcaption>
</figure>
No surprises here, common and bigger streets are often used by other runners. Taking into account where I am going to start, I should try to minimize the most "common" streets, this means that Gran Via, Avenida Fuente Nueva, Calle Reyes Católicos y Camino de Ronda mostly delimit possible tracks. 

Small streets inside the previous demarcations are very uncommon, so I should try to wander through streets like calle Buensuceso or Calle Párraga. In addition crossing hot-points like recogidas would aloow me to make a bigger circuit while minimizing my exposure. However, I have to be carefull with crossing other common routes like Camino de Ronda, as it only leads to more common spots. 
### Garmin
Let's see Garmin's data instead. One of the things I like is the way Gramin presents the information. Data don't blott street info and the detail level is very high. 
<figure>
  <img src="/images/granada1.png"  />
  <figcaption>
      <h7>Garmin map (accessed April 30)</h7>
  </figcaption>
</figure>

<figure>
  <img src="/images/granada2.png"  />
  <figcaption>
      <h7>Garmin map (accessed April 30)</h7>
  </figcaption>
</figure>

About the analysis I can make about the map, it is more or less the same as in Strava. Taking into account that both resources show the same information I am confident about the data signification (although the data may overlaps, as Garmin offers the option to upload track from strava. 

Finally I think I have enough information to make an useful track for my next running sessions. 

## Conclusions!

Taking into account the previos information I design the following track. 
<figure>
  <img src="/images/final_run.png"  />
  <figcaption>
      <h7>Garmin map (accessed April 30)</h7>
  </figcaption>
</figure>

 As it is my first running session after a long time, I limit the total distance to 5km (I introduce manually the time per kilometer, but it may change depending on my sensations, however I expect to run slowly at least the first week). Almost every meter of the track goes in "low-frequency" streets where I think I won't encounter other runner. There are 4 main points that cross "high-frequency" places, but I think the exposure (with social distance and the schedule I am planning) will be low.


Do you need to do all of this with your sessions? Obiously no. If know which street avoid, but it is not always easy to choose an alternative track. I like to make my decissions with some amount of data to be as objetive as possible. 

If you have any ideas, corrections or suggestions, let me know! 

# Images credit: 
- [Photo by Flo Karr on Unsplash](https://unsplash.com/photos/HyivyCRdz14)
- [Photo by Chander R on Unsplash](https://unsplash.com/photos/AtfA8NDgpKA)


