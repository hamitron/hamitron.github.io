# GUZL Voting Spec aka 'bevmaster'
![beverage with votes](images/bev_show.png)
[Demo](http://bevmaster.herokuapp.com)
#### Created as a spec for a potential beverage brand client to show a basic voting platform.  It allows users to create and vote on beverage designs. 

## Challenges:

* Create a voting system
* Display vote breakdown using data visualization techniques
* Display can illustration with user-chosen colors
* Highlight colors chosen with responsive display

## Specs:
- Rails 4
- PostgreSQL
- Snap.svg
- D3.js

```javascript
var dataset = {
// positive votes(green), meh votes (grey), negative votes (red). defined in the beverages controller.
  states: [gon.positive, gon.meh, gon.negative]
};

var width = 400,
    height = 400,
    radius = Math.min(width, height) / 2;

// color range for pie chart. this pops each variable to a specific color.
var color = d3.scale.ordinal()
    .range(["#3ab936", "#5d5d5d",  "#ff2316"]);

// i love pie
var pie = d3.layout.pie()
    .sort(null);

// sets the inner donut hole and outer radius
var arc = d3.svg.arc()
    .innerRadius(radius - 75)
    .outerRadius(radius - 40);

// i don't really love pie, but pie charts are cool. create pie chart here.
var svg = d3.select("#piechart").append("svg")
    .attr("width", width)
    .attr("height", height)
    .append("g")
    .attr("transform", "translate(" + width / 2 + "," + height / 2 + ")");

// append the pie to put the data in it. sort of like appending the crust to put the filling in it. just a lot less tasty.
// also the attrTween pops in the data in a slick animation.
var path = svg.selectAll("path")
    .data(pie(dataset.states))
  .enter().append("path")
    .attr("fill", function(d, i) { return color(i); })
    .transition().delay(function(d, i) { return i * 800; }).duration(800)
  .attrTween('d', function(d) {
       var i = d3.interpolate(d.startAngle, d.endAngle);
       return function(t) {
           d.endAngle = i(t);
         return arc(d);
       }
  });
```
