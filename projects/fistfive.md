# Fist Five
![Chart](images/five_chart.png)
#### Fist of five gathers feedback from a classroom and generates a visual representation for the instructor. While following along with a lesson, each student rates their comprehension of a subject on a scale of zero to five.  This data is available in real time, allowing on-the-fly pivots in teaching styles to improve lesson efficiency. Working as part of a group, I was tasked with using the D3 javascript framework and apply it to the data being generated. 

## Challenges:

* Graph numerical data with javascript data visualization framework: D3.js
* Adjust visualization to accomodate for real-time shifting sample size (amount of users) and user rating values
* Graph data for values from individual users

## Specs:
- Rails 4
- PostgreSQL
- D3.js

```javascript
var x = d3.scale.linear().domain([0, data.length]).range([20, width+20]);
var y = d3.scale.linear().domain([0, 5]).range([12, height]);
var yScale = d3.scale.linear().domain([0,5]).range([height - 8, 8]);

// add the svg canvas to the DOM
var vis = d3.select("#Aratings")

// select rectangle elements in svg.
var bars = vis.selectAll("rect")
  .data(data)

// show the bars.
bars.enter().
  append("rect").
  attr("fill", randomed()).
  attr("x", function(datum, index) { return x(index); }).
  attr("width", barWidth);

  bars.transition().
  duration(2000).
  attr("height", height +  margin.bottom).
    attr("y", function(datum) { return height - y(datum.value); }).
    attr("height", function(datum) { return y(height); });

d3.select("#Aratings")
.call(yAxis);
```