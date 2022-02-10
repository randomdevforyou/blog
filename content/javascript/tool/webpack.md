---
title: "Webpack"
date: 2022-02-08T14:32:51+05:30
draft: false
---

# Webpack 

Bundling is a process in which multiple files are combined into a single file. Webpack is a bundling tool. This blog post will guide you through the process of setting of webpack for node application.


## Write client side code

Lets create a simple node application using npm. 

```shell
mkdir webpack-starter
cd webpack-starter
npm init
```


Bundling will be done at build time so we will be installing webpack as dev dependency.

```shell
npm install --save-dev webpack webpack-cli
```

Now we are going to add some javascript files in our project which will we will bundle using webpack.

Create ***src/client/component.js*** and add following code, which just reads a root element to add some text to it.

```javascript
export default function hello(){
	const root = document.getElementById("root");
	const ele = document.createElement("div");
	ele.innerHTML = "Hello, Webpack";
	root.appendChild(ele);
}
```

Create ***src/client/index.js*** and add following code. This js file will act like registry for all the components. 

```javascript
import Hello from "./component";

Hello();

```

Now its time to specify webpack configuration which can be used by webpack to determine the bundling related configuration.

Create ***webpack.config.js*** and add following code.

```javascript
const path = require("path");
module.exports = {	
	entry: './src/client/index.js',
	output: {
		path: path.resolve(__dirname, "public", "dist"),
		filename: "bundle.js"
	}
}

```
The *entry* attribute is specifies which file is used as a starting point for bundling. The *output* attribute is used to specify the location where webpack stores the created bundle. Here we will be generating bundle in ***public/dist*** folder.

Lets see if webpack creates the bundle the way we are expecting.

```shell
npx webpack --config webpack.config.js
```

After running the command you can see the output something like this

```
 > npx webpack --config webpack.config.js

	asset bundle.js 156 bytes [emitted] [minimized] (name: main)
	orphan modules 196 bytes [orphan] 1 module
	./src/client/index.js + 1 modules 238 bytes [built] [code generated]

	WARNING in configuration
	The 'mode' option has not been set, webpack will fallback to 'production' for this value.
	Set 'mode' option to 'development' or 'production' to enable defaults for each environment.
	You can also set it to 'none' to disable any default behavior. Learn more: https://webpack.js.org/configuration/mode/

	webpack 5.68.0 compiled with 1 warning in 303 ms
```

Check in the folder ***public/dist***. You should see ***bundle.js*** which is generated by webpack.

Let's add the webpack commands in the ***package.json*** file.

```javascript
  "scripts": {
    "build": "npx webpack --config webpack.config.js --mode production",
    "build:development": "npx webpack --config webpack.config.js --mode development --watch"
  }
```

Now you can runt the npm command to trigger the bundling based on different environment i.e production or development.

```
npm run build // for production
npm run build:development // for development.
```

Running the webpack in development mode creates bundle with additional pointer which can be used for debugging. 

To see if bundles output works appropriately lets add ***index.html*** which loads our ***bundle.js***.

Add following code to ***index.html***

public/index.html
```html
<html>
	<head></head>
	<body>
	  <div id="root"></div>
	  <script src="/dist/bundle.js"></script>
	</body>
</html>
```

## Write a server code

Lets write simple express code which starts the server and serves the static content from ***public*** folder.


We will be setting up ***express*** in order to serve the client side assets.

```shell
npm install --save express
```
Create ***app.js*** and add following code to it.

```javascript

const express = require("express");

const app = express();

app.use(express.static("public"));

app.listen(8080, function(){
console.log('server started at 8080');
});

```
Update ***package.json*** to start the server.

```javascript
"scripts": {
   ...
   "start": "node app.js"
}
```

Run the server.

```javascript
npm run start
```

I hope this article will help you to get started with webpack.