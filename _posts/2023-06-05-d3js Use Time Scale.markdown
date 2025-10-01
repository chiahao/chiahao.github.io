---
layout: post
title: "d3js Use Time Scale"
date: 2023-06-05 09:03:00
category: d3js
tags: [d3js]
---


[D3 js bar chart with 24 hour x axis](https://stackoverflow.com/questions/28684566/d3-js-bar-chart-with-24-hour-x-axis)



```javascript
var today = new Date();
today.setHours(0, 0, 0, 0);
todayMillis = today.getTime();

data.forEach(d => {
    var parts = d.time.split(/:/);
    var timePeriodMillis = (parseInt(parts[0], 10) * 60 * 60 * 1000) +
                           (parseInt(parts[1], 10) * 60 * 1000) + 
                           (parseInt(parts[2], 10) * 1000);

    d.time = new Date();
    d.time.setTime(todayMillis + timePeriodMillis);
});
```


```javascript
d3.scaleTime()
  .nice(d3.timeDay, 1)
  .range(0, 2400);
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


