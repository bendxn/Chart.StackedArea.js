---
title: StackedArea Chart
anchor: stacked-area-chart
---

### Introduction
A stacked area chart is a way of showing data as stacked line graphs.

<div class="canvas-holder">
	<canvas width="250" height="125"></canvas>
</div>

### Example usage
```javascript
var myStackedAreaChart = new Chart(ctx).StackedArea(data, options);
```

### Data structure

```javascript
var data = {
	labels: ["January", "February", "March", "April", "May", "June", "July"],
	datasets: [
		{
			label: "My First dataset",
			fillColor : "rgba(220,22,22,1)",
			strokeColor : "rgba(220,22,22,1)",
			pointColor : "rgba(220,22,22,1)",
			pointStrokeColor : "#fff",
			pointHighlightFill : "#fff",
			pointHighlightStroke : "rgba(220,22,22,1)",
			data : [23,32,5,100,60,7,13]
		},
		{
			label: "My Second dataset",
			fillColor : "rgba(151,187,205,1)",
			strokeColor : "rgba(151,187,205,1)",
			pointColor : "rgba(151,187,205,1)",
			pointStrokeColor : "#fff",
			pointHighlightFill : "#fff",
			pointHighlightStroke : "rgba(151,187,205,1)",
			data : [47,2,23,27,85,68,90]
		}
	]
};
```

### Chart Options

These are the customisation options specific to StackedArea charts. These options are merged with the [global chart configuration options](#getting-started-global-chart-configuration), and form the options of the chart.

```javascript
{
	//Boolean - Whether grid lines are shown across the chart
	scaleShowGridLines : true,

	//String - Colour of the grid lines
	scaleGridLineColor : "rgba(0,0,0,.05)",

	//Number - Width of the grid lines
	scaleGridLineWidth : 1,

	//Boolean - Whether to show horizontal lines (except X axis)
	scaleShowHorizontalLines: true,

	//Boolean - Whether to show vertical lines (except Y axis)
	scaleShowVerticalLines: true,

	//Boolean - Whether the line is curved between points
	bezierCurve : false,

	//Number - Tension of the bezier curve between points
	bezierCurveTension : 0.4,

	//Boolean - Whether to show a dot for each point
	pointDot : false,

	//Number - Radius of each point dot in pixels
	pointDotRadius : 4,

	//Number - Pixel width of point dot stroke
	pointDotStrokeWidth : 1,

	//Number - amount extra to add to the radius to cater for hit detection outside the drawn point
	pointHitDetectionRadius : 20,

	//Boolean - Whether to show a stroke for datasets
	datasetStroke : true,

	//Number - Pixel width of dataset stroke
	datasetStrokeWidth : 2,

	//String - A legend template
	legendTemplate : "<ul class=\"<%=name.toLowerCase()%>-legend\"><% for (var i=0; i<datasets.length; i++){%><li><span style=\"background-color:<%=datasets[i].strokeColor%>\"></span><%if(datasets[i].label){%><%=datasets[i].label%><%}%></li><%}%></ul>"

}
```

You can override these for your `Chart` instance by passing a second argument into the `StackedArea` method as an object with the keys you want to override.

For example, we could have a stacked area chart with a curved line by doing the following:

```javascript
new Chart(ctx).StackedArea(data, {
	bezierCurve: true
});
// This will create a chart with all of the default options, merged from the global config,
//  and the StackedArea chart defaults but this particular instance will have `bezierCurve` set to true.
```

We can also change these defaults values for each StackedArea type that is created, this object is available at `Chart.defaults.StackedArea`.

### Prototype methods

#### .getPointsAtEvent( event )

Calling `getPointsAtEvent(event)` on your Chart instance passing an argument of an event, or jQuery event, will return the point elements that are at that the same position of that event.

```javascript
canvas.onclick = function(evt){
	var activePoints = myStackedAreaChart.getPointsAtEvent(evt);
	// => activePoints is an array of points on the canvas that are at the same position as the click event.
};
```

This functionality may be useful for implementing DOM based tooltips, or triggering custom behaviour in your application.

#### .update( )

Calling `update()` on your Chart instance will re-render the chart with any updated values, allowing you to edit the value of multiple existing points, then render those in one animated render loop.

```javascript
myStackedAreaChart.datasets[0].points[2].value = 50;
// Would update the first dataset's value of 'March' to be 50
myStackedAreaChart.update();
// Calling update now animates the position of March from 90 to 50.
```

#### .addData( valuesArray, label )

Calling `addData(valuesArray, label)` on your Chart instance passing an array of values for each dataset, along with a label for those points.

```javascript
// The values array passed into addData should be one for each dataset in the chart
myStackedAreaChart.addData([40, 60], "August");
// This new data will now animate at the end of the chart.
```

#### .removeData( )

Calling `removeData()` on your Chart instance will remove the first value for all datasets on the chart.

```javascript
myStackedAreaChart.removeData();
// The chart will remove the first point and animate other points into place
```