---
author: "Bart"
title: "Winning probabilities in Go 19x19 (LeelaZero)"
date: 2020-08-30T12:00:06+09:00
description: "Update! Heatmap of probability for black to win for all starting positions in a 19x19 board (Leela Zero GPU V0.17)"
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

# Plotting winning probabilities in a 19x19 Go / Baduk game

From this [older post](https://thebooort.github.io/posts/baduk-go-winning-probabilities/): 


>	This morning I found [this post on Reddit](https://www.reddit.com/r/baduk/comments/7t0bd2/heatmap_of_probability_for_black_to_win_for_all/) about winning probability for black for all starting positions. 
>	I found this visualization quite interested but i couldn't find any link to a source code to generate it or the data used to generate it, so I decided to replicate it myself.


## Data
This time I run last version of [Leela Zero v.0.17](https://github.com/gcp/leela-zero) with Chinese counting and 7.5 komi (using my GPU). I use the gtp engine via [Lizzie](https://github.com/featurecat/lizzie) an try every strating position. 

I will upload the data via sfg, as Lizzie let you safe prob's data. If I haven't uploaded it yet and want to use the data, just send me a message.


## Plotting considerations

Refer to this [older post](https://thebooort.github.io/posts/baduk-go-winning-probabilities/) in order to know a little bit more about the code. 

## Results
Again, I am quite happy with the results. I think these heatmaps looks better than just adding squares to every point. It is just a matter of taste! However, I don't LOVE the colormap. It's close to the initial style, but the percentage variations are too extreme and  I haven't found a colormap that, in my opinion, reflects well the data (aesthetically). I know I could design one by hand to be better, but, for now, I think jet does its job.

<figure>
  <img src="/images/19x19_no_num.png"  />
  <figcaption>
      <h7>with colorbar</h7>
  </figcaption>
</figure>

<figure>
  <img src="/images/19x19_num.png"  />
  <figcaption>
      <h7>Explicit probabilities</h7>
  </figcaption>
</figure>
      




