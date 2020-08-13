---
author: "Bart"
title: "Data Science in my last CS:GO match (1)"
date: 2020-04-23T12:00:06+09:00
description: "Analyzing data from my last Counter Strike (FPS) match and using it to improve"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- coding
- Data Science
- Gaming
tags: 
- Visualization
- Data
- Python
- Machine Learning
- CSGO
series:
- Data Science
- CSGO
libraries:
- mathjax
image: images/csgo-cover.jpg
---
Image credit: [La Tercera](https://www.latercera.com/mouse/valve-confirmo-filtracion-del-codigo-de-counter-strike-global-offensive-y-team-fortress-2/)
<figure>
  <img src="/images/csgo.svg"  />
</figure>

# Counter Strike and Data Science 1: Grenades and other utilities

Counter Strike Global Offensive (CSGO) is a first person shooter game developed by Valve and Hidden Path Entertainment. 

The game pits two teams against each other: the Terrorists and the Counter-Terrorists. Both sides are tasked with eliminating the other while also completing separate objectives. The Terrorists, depending on the game mode, must either plant the bomb or defend the hostages, while the Counter-Terrorists must either prevent the bomb from being planted, defuse the bomb, or rescue the hostages. 

In competitive mode, 30 rounds are played, first team to get 16 victories wins.

 During COVID19 quarentine some friends invite me to play for the first time, and, despite I am not even close to good at it, I have a lot of fun playing it. After my first 10 wins, when I understood the game strategies a little bit more, I began to wonder if my positioning were good or if I was able to use grenades and other utilities correctly. So I decided to approach possible answers to this question with data science. 

In this first part I'm going to analyze where and how to throw grenades, as I do not use them at all.

## Utilities
(data from [eSports team Dignitas](http://team-dignitas.net/articles/blogs/CSGO/10641/a-csgo-guide-to-your-utility) )
The grenades that I am going to analyze are:

- The Flashbang

The flashbang, or flash, has the primary use of blinding opponents. If people look directly at it, teammate or not, the person who looked at it will be blinded for a period of time, defined by how close the flash popped and how directly the person looked at it.

- The Smoke Grenade

The smoke grenade instantly creates a thick, medium-sized (288 units diameter, or 144 units radius) smoke screen that lasts for 18 seconds after the fuse expires. The smoke screen is largely opaque except at the corners, blocking players' vision. If a player enters the smoke, the player's weapon model will fade slightly and all vision will be obscured, even at zero range.


- The Molotov/Incendiary Grenade

This grenade explodes after a certain amount of time has passed after you have thrown it. If it explodes on, or close to, the ground (or any other flat surface) it will cover a good amount of space in flames. Everyone standing in those flames with 100 HP has roughly three and a half seconds left to get out of it before they die. 

- Interaction between grenades: 
It should be noted that you can put out any flames caused by an incendiary or a molotov with a smoke grenade, which may allow the CTs to survive longer than intended. There are no other interactions between any of them.

There more grenades, but I have been told that these are the ones that I should master first.

## Getting the data
The map I am currently playing in competitive CSGO is inferno. It is not the most common map, but definetly top 5 maps. There are not specific reasons for this choice: my friends know this map relatively well and they know some strategies, so when I decide to play with them they choose this map.

<figure>
  <img src="/images/de_inferno.png"  />
  <figcaption>
      <h7>de_inferno competitive map structure</h7>
  </figcaption>
</figure>

- ### Data from my game

I tried different ways to get my data from the game. But, at the end, most of the csgo stats webpages offer a huge amount of information with only the game_id. I realize that this was the easiest way to get my data. Meanwhile as I have access to other csgo datasets I can develop the code needed to plot and analyze all csgo data in case I am able to get my stats in the future. Sadly, for this part, I realize that I do not throw any grenade during the game (couple of smokes) so I will add them for visualization purpouses but they wont give as any information. 

- ### Data from professional players

With my personal data I can analyze my plays, but it is hard to judge them. I realized that comparing them with the usual plays that people in competitive mode would offer me more information. For this pourpose I find [a dataset with ~ 1400 competitive matches](https://www.kaggle.com/skihikingkevin/csgo-matchmaking-damage#esea_master_grenades_demos.part1.csv), in kaggle obiously. That data is well formated and it is quite easy to work with. 

## Location names in Inferno
In order to manage a common vocabulary and to understand my conclusions and analysis here you have the location names in the map (from (https://guides.gamepressure.com/counter_strike_global_offensive/guide.asp?ID=43283)):

<figure>
  <img src="/images/mapa.png"  />
</figure>




## Analyzing professional players data

Heatmaps: You have to take into account that "radar" or "in-game" coordinates are not useful in order to plot your whateverstats-heatmap. For that purpose you have to scale the data into your image resolution. Beware that some points are beyond your image (for example some smokes are thrown away outside the map, and that could make some data noisy. 

For de_inferno map, you have to make slighty deviations from a code I founded. Also you have to find the exact measures of your map, check the link in the code for that :

```python
# Code modified from the one used by billfreeman44 | See his kernel : https://www.kaggle.com/billfreeman44/finding-classic-smokes-by-t-side-on-mirage 
# map data: https://github.com/akiver/CSGO-Demos-Manager/tree/master/Core/Models/Maps
def pointx_to_resolutionx(xinput,startX=-2222,endX=3561,resX=1160):
    sizeX=endX-startX
    if startX < 0:
        xinput += startX *(-1.0)
    else:
        xinput += startX
    xoutput = float((xinput / abs(sizeX)) * resX);
    return xoutput-15

def pointy_to_resolutiony(yinput,startY=-1649,endY=4408,resY=1250):
    sizeY=endY-startY
    if startY < 0:
        yinput += startY *(-1.0)
    else:
        yinput += startY
    youtput = float((yinput / abs(sizeY)) * resY);
    return resY-youtput-120
```

I change a little bit the scale and exes elevation. The results were pretty good and coherent. In this situation, it is necesary to plot the map below the plots, otherwise data could not be easy to analyze: 

```python
# Code modified from the one used by billfreeman44 | See his kernel : https://www.kaggle.com/billfreeman44/finding-classic-smokes-by-t-side-on-mirage 
im = plt.imread('../input/de_inferno.png')
plt.figure(figsize=(15,15))
t = plt.imshow(im)
t = plt.scatter(csgo_sm_small['grenade_xpos'], csgo_sm_small['grenade_ypos'],alpha=0.05,c='blue')
t = plt.scatter(csgo_sm_small['att_xpos'], csgo_sm_small['att_ypos'],alpha=0.05,c='red')
# we can also plot trayectories
for i in range(1,len(grenade_number)):
    t = plt.plot([a_x[i],nade_x[i]],[a_y[i],nade_y[i]],c='y',alpha=0.25,linestyle='dashed')

```

With this simple steps we can get a lot of information about this map and how grenades are thrown. We will analyze the data from both team, as their strategies are different.

### CounterTerrorist side
In this map counterterrorist (CT) must either prevent the bomb from being planted or defuse the bomb. They can also win if they eliminate the other team and no bomb is planted. 

For that reason, CT in most cases, want to impede Terrorist(T) to enter to A o B zone (see the previous map if you are not familiar with those names). 

#### CounterTerrorist flash grenades

First we have flash grenades. Here you have two plots, one with thrower and grenade final location and one with the trajectories (intensity of color can be related to the commoness of the data, more intensity means more common to appear in the dataset):
<figure>
  <img src="/images/flash-CT.png"  />
  <figcaption>
      <h7>Flash grenades locations (blue) and Thrower location (red)</h7>
  </figcaption>
</figure>

<figure>
  <img src="/images/flash-CT-tray.png"  />
  <figcaption>
      <h7>Flash grenades locations (blue) and Thrower location (red)</h7>
  </figcaption>
</figure>

Seeing both plots, the most used flash are thrown to Middle an Banana, in order to difficult Terrorist advance. One should take into account those which are thrown in apartments from inside LongHall and from Balcony and Pit. These last positions are the most common for me, so I take note about these flashes.

Also there are some interesting flashes thrown from Garden into Sanbags and Porch, mostly to blind Terrorist if they are reaching B. There can be seen two classic postitions in the map for CT, one covering Close side, and other in Patio.

#### CounterTerrorist incendiary grenades
Again, I am using two plots, one with thrower and grenade final location and one with the trajectories (intensity of color can be related to the commoness of the data, more intensity means more common to appear in the dataset):
<figure>
  <img src="/images/molos-CT.png"  />
  <figcaption>
      <h7>Incendiary grenades locations (blue) and Thrower location (red) </h7>
  </figcaption>
</figure>

<figure>
  <img src="/images/molo-CT-tray.png"  />
  <figcaption>
      <h7>Incendiary grenades locations (blue), tajectory (yellow) and Thrower location (red) </h7>
  </figcaption>
</figure>

Most incendiary grenades are thrown in Banana to stop Terrorist to reach B. There are also some representative throws from middle, but this position is quite unsafe for CT (they are too exposed to long-range weapons in Middle ) so I am puzzle about this specific play. 

From my perspective, most incendiary grenades thrown into apartments came from Point A, and Balcony. I can't move that far during the game, so I should focus myself on thrown only when I am inside Balcony.


#### CounterTerrorist smoke grenades

<figure>
  <img src="/images/smokes-CT.png"  />
  <figcaption>
      <h7>Smokes grenades locations (blue) and Thrower location (red)</h7>
  </figcaption>
</figure>
<figure>
  <img src="/images/smokes-CT-tray.png"  />
  <figcaption>
      <h7>Incendiary grenades locations (blue), tajectory (yellow) and Thrower location (red) </h7>
  </figcaption>
</figure>

Smokes are usually thrown into middle, I guess that if Terrorist can't reach Point B, them they are forced to go Point A, and CT deploy a smoke grenade to being able to create some advantages in these situations.

In Banana, most smokes are thrown near Sandbags, which I think are mostly a late game strategy to slow down Terrorist or a deceive strategy, making Terrorist unable to see Incendiary grenade fire.


### Terrorist side
In this map terrorist (T) must plant the bomb. They can also win if they eliminate the other team and no bomb is planted. 

For that reason, T in most cases, want to access as fast as possible to either Point A or Point B (there is limited time every round and if they do not do anything in this time, they lose).
#### Terrorist flash grenades
<figure>
  <img src="/images/flash-Terror.png"  />
  <figcaption>
      <h7>Flash grenades locations (blue) and Thrower location (red)</h7>
  </figcaption>
</figure>
<figure>
  <img src="/images/flash-T-tray.png"  />
  <figcaption>
      <h7>Incendiary grenades locations (blue), tajectory (yellow) and Thrower location (red)</h7>
  </figcaption>
</figure>

Talking about Flash grenades, T usually throw a lot of these grenades on Banana. I guess that if CT do not throw any fire, T can get some advantage blinding long-range weapons that can be on porch, end of Banana, or even Logs. 
Another hot point is end of Middle, those grenades are useful to counter the common smoke used by CT. With those grenades T can try to eliminate anyone on Close or Patio. 
Finally, on apartments, there is some throws from outside to Window (but Incendiary are more common than flashes), and other throw to Pit and Balcony, as a way to enter safely into Point A. 

#### Terrorist incendiary grenades
<figure>
  <img src="/images/molos-Terror.png"  />
  <figcaption>
      <h7>Incendiary grenades locations (blue) and Thrower location (red)</h7>
  </figcaption>
</figure>
<figure>
  <img src="/images/molo-T-tray.png"  />
  <figcaption>
      <h7>Incendiary grenades locations (blue), tajectory (yellow) and Thrower location (red)</h7>
  </figcaption>
</figure>

Incendiary grenades on T side are used in different points but with similar expected outcomes. 
From balcony to Pit: those are used to kill enemys at Pit.
From AltMiddle to Window: prevent CT to enters this room and kill any T in this street.
From Banana: stop any rush from behind when T go to PointA
From Sandbags to Garden: Securing PointB and stopping any player on Garden. 


#### Terrorist smoke grenades
<figure>
  <img src="/images/smokes_terror.png"  />
  <figcaption>
      <h7>Smokes grenades locations (blue) and Thrower location (red)</h7>
  </figcaption>
</figure>
<figure>
  <img src="/images/smoke-T-tray.png"  />
  <figcaption>
      <h7>Incendiary grenades locations (blue), tajectory (yellow) and Thrower location (red)</h7>
  </figcaption>
</figure>
Finally smokes are used by T as a way to stop or slow down CT when they are on different positions. A lot of thes smokes prevent long range weapons to attack from middle. On other side, a lot of smokes are also played creating a barrier between Well  and PointB, so CT comming this way are stopped. 
On pointA there some relevant smokes too, securing pointA when T have reached it.

## Conclusions!
So far so good! I definetly have to train how to throw smokes and where to throw them, but now I have a general idea of what smokes are usually thrown (despite 1vs1 situations). Can't wait to try those in real games. 

Next steps: find hot spots in the map where I die most, and from where I am killed. See you in chapter II!




