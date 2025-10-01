---
layout: post
title: "d3js Stacked Bar Chart"
date: 2023-06-06 08:38:00
category: d3js
tags: [d3js]
---

vertical stacked bar chart  

*Note!*  Always remember to pass **Array** into `.domain()`, `.range()` and `d3.stack().keys()`;

```javascript
document.body.style = "background-color: #ccc;";

var data = [{a: 1, b: 3, c: 2, d: 7},
            {a: 2, b: 1, c: 5, d: 1},
            {a: 3, b: 3, c: 4, d: 3},
            {a: 4, b: 8, c: 5, d: 4}];

var xScale = d3.scaleBand()
  .domain(data.flatMap(d=>d.a))
  .range([0, 100])
  .padding(0.2);

var yScale = d3.scaleLinear()
  .domain([d3.max(data.flatMap(d => d.b + d.c + d.d)), 7])
  .range([0, 200]);

var colors = d3.scaleOrdinal()
  .domain(["b", "c", "d"])
  .range(d3.schemeGnBu[9].slice(3));

var stack = d3.stack()
  .keys(["b", "c", "d"]);

var svg = d3.select('body').append('svg')
  .attr('width', 200)
  .attr('height', 400);

var chartData = stack(data);

var groups = svg.append('g')
  .selectAll('g')
  .data(chartData)
  .join('g')
  .attr('fill', d => colors(d.key));

groups.selectAll('rect')
  .data(d => d)
  .join('rect')
    .attr('x', d => xScale(d.data.a))
    .attr('y', d => yScale(d[1]))
    .attr('width', xScale.bandwidth())
    .attr('height', d => yScale(d[0]) - yScale(d[1]));
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


