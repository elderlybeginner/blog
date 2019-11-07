---
layout: post
title: Cp and Cpk for Target Shooters
date: 2019-11-06
tags: [Python, shooting, sport shooting, Cp, Cpk, process capability index, precision, accuracy, measuring]
---

When shooting to target there are two main indicators how good is your shooting:

1. Precision - the ability to hit the same place over and over. This gives you shot dispersion which I am going to measure with	 Cp index

![high precision](highprecision.png)
Source: public domain

2. Accuracy - is the proximity of results to the center point. I am going to measure it with Cpk index

![high accuracy](highaccuracy.png)
Source: public domain

### The Project

The project is to calculate precision and accuracy based on bullet holes on target.  
You are scanning or take photo of a target, mark holes (how about primary hole recognition?) and program calculates Cp and Cpk for you. **Centroid** (average position of all the holes) is shown on the target.

### Cp and Cpk

TODO

### Calculating centroid

Measurement is to be set as the distance from the center to default place.  
Then we calculate holes position as a table of tables: 

h1 = [x, y], h2 = [x, y], ... hn = [x,y]  
h2 = ...  
...    
hn = ...  

holes = [h1, h2, ..., hn]

and centroid is calculated:

```python
x = [h[0] for h in holes]
y = [h[1] for h in holes]  #  or x, y = zip(*holes)

centroid = [sum(x) / len(holes), sum(y) / len(holes)]
```

### Calculating Cp and Cpk

TODO

### Visualization

Centroid is marked on target. Cp and Cpk are shown.

### Data gathering

Cp and Cpk are gather and put on chart to show target shooting progress. 

I am newbie in shooting, dispersion analysis and programming. Feel free to correct my mistakes and give some constructive tips.

