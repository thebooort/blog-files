---
author: "Bart"
title: "Winning probabilities in Go (leela)"
date: 2020-04-26T12:00:06+09:00
description: "Heatmap of probability for black to win for all starting positions (Leela V0.11.0)"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Bart
categories:
- coding
- Data Science
- Baduk
tags: 
- Visualization
- Data
- Python
- Machine Learning
- Go
- Baduk
series:
- Data Science
- Baduk
libraries:
- mathjax
image: images/go.png
---
photo credits: [Photo by Joe Woods on Unsplash](https://unsplash.com/photos/hY-p7aya6c8)

# Plotting winning probabilities in a 9x9 Go / Baduk game

This morning I found [this post on Reddit](https://www.reddit.com/r/baduk/comments/7t0bd2/heatmap_of_probability_for_black_to_win_for_all/) about winning probability for black for all starting positions. 
I found this visualization quite interested but i couldn't find any link to a source code to generate it or the data used to generate it, so I decided to replicate it myself.

 I am starting with a 9x9, because I am not familiar with any parser to exchange data with a go engine. Next step is to make all process via a python script and been able to replicate all boards.

This quick project take me just one hour, and I am sure everything can be automated or made better, but at the end you have the data and the code, so feel free to upgrade or change anything you want. 

## Data

For the data I just run [Leela v.0.11.0](https://sjeng.org/leela.html) with Chinese counting and 7.5 komi. I use the gtp engine with [Sabaki](https://sabaki.yichuanshen.de/) an try every strating position. 


## Plotting considerations

I get the board from [this question in stackoverflow](https://stackoverflow.com/questions/24563513/drawing-a-go-board-with-matplotlib), I simply add star points and different configurations (one for plotting with color bar and other with numbers or without them.

```python
# with colorbar
#fig = plt.figure(figsize=[13,10.5])
# with numbers
fig = plt.figure(figsize=[8,8])

fig.patch.set_facecolor((1,1,.8))

ax = fig.add_subplot(111)

# draw the grid
for x in range(9):
    ax.plot([x, x], [0,8], 'k')
for y in range(9):
    ax.plot([0, 8], [y,y], 'k')

# scale the axis area to fill the whole figure
ax.set_position([0,0,1,1])

# get rid of axes and everything (the figure background will show through)
ax.set_axis_off()

# scale the plot area conveniently (the board is in 0,0..18,18)
ax.set_xlim(-1,9)
ax.set_ylim(-1,9)

# draw star points
s1, = ax.plot([2,6,6,2,2,4],[2,2,6,2,6,4],'o',
	     markersize=10, markeredgecolor=(0,0,0), 
             markerfacecolor='k', markeredgewidth=2)

```
Also, I think data could be better but, adding points and values like array let me easily plot every point, been able to plot labels if I want and been able to add simply the colormap.


## Results
I am quite happy with the aesthetic of the results. I think these heatmaps looks better than just adding squares to every point. It is just a matter of taste! At least you have all the data and the code to make similar things or your own variations. :smile:S

<figure>
  <img src="/images/win-colorbar.png"  />
  <figcaption>
      <h7>with colorbar</h7>
  </figcaption>
</figure>

<figure>
  <img src="/images/win-nobar.png"  />
  <figcaption>
      <h7>Explicit probabilities</h7>
  </figcaption>
</figure>

## Todo

- Exchange (with a parser) data beetween python and go engine
- Replicate for 13x13 and 19x19


## Source code and Data

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Sun Apr 26 
"""

import matplotlib.pyplot as plt
import numpy as np

# create a 8" x 8" board
# with colorbar
#fig = plt.figure(figsize=[13,10.5])
# with numbers
fig = plt.figure(figsize=[8,8])

fig.patch.set_facecolor((1,1,.8))

ax = fig.add_subplot(111)

# draw the grid
for x in range(9):
    ax.plot([x, x], [0,8], 'k')
for y in range(9):
    ax.plot([0, 8], [y,y], 'k')

# scale the axis area to fill the whole figure
ax.set_position([0,0,1,1])

# get rid of axes and everything (the figure background will show through)
ax.set_axis_off()

# scale the plot area conveniently (the board is in 0,0..18,18)
ax.set_xlim(-1,9)
ax.set_ylim(-1,9)

# draw star points
s1, = ax.plot([2,6,6,2,2,4],[2,2,6,2,6,4],'o',markersize=10, markeredgecolor=(0,0,0), markerfacecolor='k', markeredgewidth=2)

b = np.array([[ 24.45,  29.95,  31.51,  32.48,  33.11,  32.48,  31.51,  29.95,
         24.45],
       [ 29.95,  37.32,  40.28,  41.36,  40.8 ,  41.36,  40.28,  37.32,
         29.95],
       [ 31.51,  40.28,  44.5 ,  45.46,  46.13,  45.46,  44.5 ,  40.28,
         31.51],
       [ 32.48,  41.36,  45.46,  48.79,  48.03,  48.79,  45.46,  41.36,
         32.48],
       [ 32.48,  41.36,  45.46,  48.79,  48.03,  48.79,  45.46,  41.36,
         32.48],
       [ 33.11,  40.8 ,  46.13,  48.03,  48.03,  48.03,  46.13,  40.8 ,
         33.11],
       [ 31.51,  40.28,  44.5 ,  45.46,  46.13,  45.46,  44.5 ,  40.28,
         31.51],
       [ 29.95,  37.32,  40.28,  41.36,  40.8 ,  41.36,  40.28,  37.32,
         29.95],
       [ 24.45,  29.95,  31.51,  32.48,  33.11,  32.48,  31.51,  29.95,
         24.45]])

y_array = np.array([[ 0,1,2,3,4,5,6,7,8],
       [ 0,1,2,3,4,5,6,7,8],
       [ 0,1,2,3,4,5,6,7,8],
       [ 0,1,2,3,4,5,6,7,8],
       [ 0,1,2,3,4,5,6,7,8],
       [ 0,1,2,3,4,5,6,7,8],
       [ 0,1,2,3,4,5,6,7,8],
       [ 0,1,2,3,4,5,6,7,8],
       [ 0,1,2,3,4,5,6,7,8]])
    
x_array = np.array([[ 0,0,0,0,0,0,0,0,0],
       [ 1,1,1,1,1,1,1,1,1],
       [2,2,2,2,2,2,2,2,2],
       [ 3,3,3,3,3,3,3,3,3],
       [ 4,4,4,4,4,4,4,4,4],
       [ 5,5,5,5,5,5,5,5,5],
       [ 6,6,6,6,6,6,6,6,6],
       [ 7,7,7,7,7,7,7,7,7],
       [ 8,8,8,8,8,8,8,8,8]])    

#plt.colorbar()
plt.title(r'Winning probabilities for black for all starting positions (Leela v0.11.0)',fontsize=18)
s1 = ax.scatter(x_array,y_array,c=b,s=3000,cmap='rainbow')  
for i in range(0,9):
    for j in range(0,9):
        s5 = ax.text(i, j, str(b[i,j]),horizontalalignment='center', fontsize=12,color='white',fontweight='bold')
        
```



