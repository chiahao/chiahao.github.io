---
layout: post
title: "D3js Update Donut Chart"
date: 2022-03-18 08:36:00
category: javascript
tags: [d3js]
---

```javascript
function getDonutChart(chartDiv) {
   let innerRadius = 30;
   let outerRadius = 44;

   const arc = d3.arc()
      .innerRadius(innerRadius)
      .outerRadius(outerRadius)
      .cornerRadius(60);

   let svg = d3.select(chartDiv)
      .append("svg")
      .attr("preserveAspectRatio", "xMinYMin meet")
      // 不要設定大小, 以便自動放大縮小
      // .attr("width", width)
      // .attr("height", height)
      .attr("viewBox", [-50, -50, 100, 100])
      .attr("style", "max-width: 100%; height: auto; height: intrinsic;");

   const g = svg.append("g")
      .attr("stroke", "white")
      .attr("stroke-width", 1)
      .attr("stroke-linejoin", "round");

   const pie = d3.pie()
      .value(d => d.count);

   // 預設空的
   let emptyData = [{name: "SUM_REGULAR_HOUR_MAX_EIGHT", count: 0.0, color: "#DB8786"},
       {name: "SUM_EXT_HOUR_BEFORE", count: 0.0, color: "#E5C6A4"},
       {name: "SUM_EXT_HOUR_AFTER", count: 0.0, color: "#C7C7C7"},
       {name: "empty", count: 1.0, color: "#DDDDDD"}];

   const emptyArcData = pie(emptyData);
   // 先畫一個空的
   change(emptyArcData);

   function change(data) {
      const t = svg.transition().duration(10000);
      console.log(data);

      const pieArcData = pie(data);
      console.log(777)
         console.log(pieArcData);

      const slice = g
         .selectAll("path")
         .data(pieArcData);

      slice.enter()
         .insert("path")
         .style("fill", d => d.data.data.color)
         .merge(slice)
         .transition()
         .duration(t)
         .attrTween("d", function (d) {
               this._current = this._current || d;
               const interpolate = d3.interpolate(this._current, d);
               this._current = interpolate(0);
               return function (t) {
                  return arc(interpolate(t));
               };
         });

      slice.exit().remove();
   }

   return Object.assign({}, svg.node, {
         update(data) {
            change(data);
         }
   });        
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


