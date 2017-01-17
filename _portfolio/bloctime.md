---
layout: post
title: Bloctime
feature-img: "img/sample_feature_img.png"
thumbnail-path: "img/bloctime.PNG"
short-description: The time management workflow app based on the Pomodoro Time Management Technique

---

App live at: <https://bloctime-sam.herokuapp.com>

Code: <https://github.com/srosenshein/bloctime>

# Summary

Bloctime is a time management web app intended to promote workflow focus based on the Pomodoro Technique (<http://pomodorotechnique.com>). This project was my first attempt utilizing the React library as well as Webpack and Babel dependencies and built for educational purposes. It demonstrates my understanding of the Webpack-babel-React workflow, React Router, and pulling data from a Firebase API backend.

## Features

* Upon starting a new "work session", a 25-minute timer (formatted with moment.js) is initiated where the user is expected to complete a task and not have the ability to pause the timer.
	* Once the timer hits zero, an audible "ding" noise is played, signaling the user that the work session has ended.
	* Following a "work session", a 5-minute "break session" is initiated. This is accomplished by passing the appropriate pathname to react router as seen in the following code:

{% highlight javascript %}
handleSession: function() {
	window.clearInterval(this.interval)
	var newState = {isTicking: false};
	var activePath = this.props.location.pathname;
	var sessionCount = this.state.sessionCount;

	/* Extra long break every 4 work sessions */
	switch (activePath){
		case '/work':
			sessionCount++;
			if (sessionCount % 4 != 0){
				this.context.router.push({pathname: '/break'})
			} else {
				this.context.router.push({pathname: '/longbreak'})
			}
			break;
		case '/break':
		case '/longbreak':
			this.context.router.push({pathname: '/work'})
			break;
		default: 
			this.context.router.push({pathname: '/'})
	}
	newState.sessionCount = sessionCount;
	this.setState(newState);
},
{% endhighlight %}

* The app also tracks within the state the number of consecutive work sessions successfully completed. This is because after 4 sessions, a longer 30-minute break session is given to the user. The appropriate time amounts are handled by the Routes passing in the appropriate prop:

```javascript
var routes = (
	<Router history={hashHistory}>
		<Route path='/' component={Main}>
			<IndexRoute component={Home} />
			<Route path='about' component={About} />
			<Route path='work' header="Work Session" seconds={1500} component={TimerContainer} />
			<Route path='break' header="Break Time" seconds={300} component={TimerContainer} />
			<Route path='longbreak' header="Extra Break Time" seconds={1800} component={TimerContainer} />
		</Route>
	</Router>
); // 1500s = 25min work, 300s = 5min break, 1800s = 30min long break
```

```javascript
componentDidMount: function() {
	this.originalTime = this.props.route.seconds
	this.setState({
		seconds: this.originalTime
	});
},
componentWillReceiveProps: function(nextProps) {
	this.setState({seconds: nextProps.route.seconds})
	this.originalTime = nextProps.route.seconds;
},
```
* A tasklist where a user can enter a task which automatically appears on the UI due to reactfire connected with the Firebase backend. Each task is also able to be deleted upon completion.

## Other Lessons Learned

* The concept of presentaional vs functional React containers and components
* React lifecycle events
* State Management

# Conclusion

With this project, I believe I have developed a strong understanding of basic React concepts, features, and benefits as compared to other similar libraries such as Angular. For example, I prefer React over Angular because the state management concept allows for a clear understanding of data within the app as well as the workflow. Also, the modular styling of React components, although similar to Angular directives, create a very developer-friendly environment in my opinion. Finally, the concept of updating the virtual DOM through difs provide a very efficient manner of updating the UI and thus creating a user-friendly experience.

In terms of next steps, I intend to further my education by creating more complex React UIs, utilizing supporting libraries such as Redux, and moving towards the mobile space with React Native. 