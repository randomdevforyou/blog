 ---
title: "Use of defer"
date: 2022-08-22T14:32:51+05:30
draft: false
---

Generally, browser loads the page synchronosly by default, which means it loads one thing at a time. If an html page has a external scripts to load, html loading halts till the script is loaded and executed. 

![Defer](/img/normal-synchronous-execution.jpeg)


To demonstrate the synchronous behaviour of page loading by browser, create a file ***script_one.js*** as follow.

```javascript
	console.log("Script One -> Document state is: " + document.readyState);
	for(let i = 0; i < 1000000; i++){
		//NOOP
	}

	console.log("Script One -> done");
```

Add one more script file ***script_two.js*** as follow:

```javascript
	console.log("Script two -> Document state is: " + document.readyState);
```


Add a html file ***index.html*** as follow

```html
	<html>
		<head></head>
		<body>
			This is Defer Demo
			<script src="script_one.js"></script>
			<script src="script_two.js"></script>
		</body>
	</html>
```


We are adding same ***script.js*** file twice. If you open index.html, you should see following output in console

```
Script One -> Document state is: loading 
Script One -> done
Script two -> Document state is: loading 
```

The value of ***document.readystate*** is ***loading*** which means document is still loading. Refer [this](https://developer.mozilla.org/en-US/docs/Web/API/Document/readyState) for more details about readyState. Also looking at the console output, browser executed ***script_one.js*** completely before loading and executing ***script_two.js***. This also implies that both the scripts are rendering blocking. 


How can we get rid of this effect? 

There are few ways to tell browser to load the scripts asynchronously. Use ***defer*** directive to tell browser to download and execute the script without interefering with the document loading process.

![Defer](/img/normal-synchronous-execution.jpeg)

To demonstrate this, lets use ***defer*** in previous example


```html
	<html>
		<head></head>
		<body>
			This is Defer Demo
			<script defer src="script_one.js"></script>
			<script src="script_two.js"></script>
		</body>
	</html>
```

Observe the below output now.

```
Script two -> Document state is: loading
Script One -> Document state is: interactive 
Script One -> done
```

This implies that ***script_one.js*** is loaded and executed after document is loaded and it is not render blocking.





