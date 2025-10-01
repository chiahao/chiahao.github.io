---
layout: post
title: "d3js Bar Chart Updator With exit Animation"
date: 2023-07-11 14:58:00
category: d3js
tags: [d3js]
---

The key function in [selection.data([data, key])](https://github.com/d3/d3-selection/blob/v3.0.0/README.md#selection_data) is for `.join()`.  

> In conjunction with selection.join (or more explicitly with selection.enter, selection.exit, selection.append and selection.remove), selection.data can be used to enter, update and exit elements to match data.  

```javascript
function drawChart(data) {
  const margins = {'width': 120, 'height': 200};

  let svg = d3.select('#chart')
    .append('svg')
    .attr('width', margins.width)
    .attr('height', margins.height);

  var xScale = d3.scaleBand()
    .domain([...Array(4).keys()])
    .range([0, 100])
    .padding(0.2);

  var yScale = d3.scaleLinear()
      .domain([0, 10])
    .range([0, 180]);

  let bar = svg
    .selectAll('rect');

  return (data) => {
    const t = svg.transition().duration(750);

    bar = bar.data(data, d => d)
      .join(
        enter => enter.append('rect')
          .attr('x', 0 - xScale(1))
          .attr('y', (d) => 200 - yScale(d))
          .attr('height', d => yScale(d))
          .attr('width', xScale.bandwidth()),
        update => update,
        exit => exit
          .call(bar => bar.transition(t).remove()
                .attr('x', margins.width))
      )
      .call(bar => bar.transition(t)
          .attr('x', (_, i) => xScale(i))
          .attr('y', (d) => {
            console.log(d);
            return 200 - yScale(d)
          })
          .attr('height', d => yScale(d))
          .attr('width', xScale.bandwidth())
          .attr('fill', '#008765')
      );
  }
}

var chart = drawChart();

function getRandomData() {
  const result = [];
  for(i = 0; i < 4; i ++) {
    const obj = {};
    obj.a = Math.floor(Math.random() * 10);
    // result.push(obj);
    result.push(Math.floor(Math.random() * 10));
  }
  return result;
}

document.querySelector('#updateBtn').addEventListener('click', function() {
  chart(getRandomData());
});

```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


