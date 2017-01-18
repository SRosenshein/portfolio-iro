---
layout: post
title: Blocmetrics
feature-img: "img/sample_feature_img_2.png"
thumbnail-path: "img/blocmetrics_chart.PNG"
short-description: The real-time analytics dashboard for BlocJams

---

App live at: <https://blocmetrics-sam.herokuapp.com>

Code: <https://github.com/srosenshein/blocmetrics> 

# Summary

Blocmetrics is an analytics dashboard paired with BlocJams, a Spotify-replica music player app. The code for BlocJams can be found [Here](https://github.com/SRosenshein/bloc-jams-angular/tree/master "BlocJams Github"). The primary purpose for this project was to gain experience utilizing [D3](https://d3js.org/ "D3js.org") Data Visualization Javascript library. This project also demonstrates my understanding of adding event listeners in order to track various metrics as well my ability to transform the raw data into useful information through visual aids.

## Features

* Blocmetrics was built utilizing the Angular framework and incorporating the [Angular-nvD3](https://krispo.github.io/angular-nvd3/#/ "Angular-nvD3 home") module in order to seamlessly include the D3 library as an Angular directive.
* Within BlocJams, event listeners were attached to trackable metrics such as individual page views and song play counts as seen here:

```
run.$inject = ['$rootScope', '$state', 'Metric'];
	function run($rootScope, $state, Metric) {
		$rootScope.$on('$stateChangeSuccess', function(event){
			Metric.registerPageView($state.current);
		});
	}
```
The Metric directive would then update the database stored online in Firebase to be fetched and formatted by Blocmetrics.

* Blocmetrics takes this raw data stored on Firebase and applies it towards relevant charts and graphs utilizing D3 and [Moment.js](http://momentjs.com/ "Moment JS home"). For example, the following is a code snippet of a pure function that receives a custom date and generates the x-axis of dates for the line chart displaying number of page views:

```
// Generate array of dates between first date in pageViews array and current date to populate x-axis
var getDateRange = function(startDate) {
  var s = moment(startDate, "MM/DD/YYYY").format();
  var e = moment().format(); //end date (now)
  var a = [];
  var days = moment(e).diff(s, "days");
  
  for(var i = 0; i <= days; i++){
    a.push(s);
    s = moment(s).add(1, "days").format();
  }
  return a;
};
```

* With this function, the accompanying line chart can always display up-to-date and relevant information.
* The charts featured on Blocmetrics, due to the usage of D3, are also interactive and consist of various options in order to improve both readability and quality of information. For example, the page views line chart consists of an interactive tooltip option to compare the number of views on different pages each day by simply hovering over the data point.

```
interactiveLayer: {
  tooltip: {
    headerFormatter: function(d) {
    	return moment(d, 'x').format('MM/DD/YYYY');
    }
  }
```
![Blocmetrics tooltip](/img/tooltip.png)

# Conclusion

D3 is a powerful tool to create informative and useful charts and graphs in order to display data in various unique ways. When working on this project, the main issue I faced was converting raw data into the appropriate formatted pieces of information to be accepted by the D3 library. However, after searching through the robust documentation as well as consulting the developer community, I was able to handle the data effectively and focus on exploring the power of the Javascript library. As a developer with a background and passion in marketing research and consumer insights, I aspire to continue to challenge myself with this flexible and functional technology and build further informative and innovative visuals.