 ---
title: "Webpack + react + babel"
date: 2022-02-19T14:32:51+05:30
draft: false
---

In the previous [article](/posts/javascript/tool/react/), we saw how to setup a Webpack and React application. We wrote the React components in plain javascript, wherein we created  HTML elements using javascript. See the below code, how we created ***div*** element.


```javascript

import React  from "react";

export default class Hello extends React.Component {
	render() {
	  return React.createElement('div', null, `Hello ${this.props.toWhat}`);
	}
  }

```

Isn't it be cool if we write the same component in a better way? Like Below

```javascript

import React  from "react";

export default function(props){
	return <div>Hello {props.toWhat}</div>
}

```

Yes, it is possible with the use of [JSX](https://reactjs.org/docs/introducing-jsx.html). This article is about how to set up JSX with the help of [babel](https://babeljs.io/).

We will start from where we left in a previous [article](/posts/javascript/tool/react/). You can use [react-starter repositroy](https://github.com/randomdevforyou/react-starter) as starting point.

## Setup babel

Firstly, install following dev dependencies.

```shell
npm install --save-dev babel-loader @babel/core @babel/preset-react

```

Add .babelrc file 

```javascript
{
	"presets": [
		[
			"@babel/preset-react"
		]
	]
}
```


Update webpack.config.js to use ***babel-loader***.

```javascript
const path = require("path");
module.exports = {	
	entry: './src/client/index.jsx',
	output: {
		path: path.resolve(__dirname, "public", "dist"),
		filename: 'bundle.js'
	},
	module: {
		rules: [
		  {
			test: /\.jsx/,
			exclude: /(node_modules|bower_components)/,
			use: {
			  loader: 'babel-loader'
			}
		  }
		]
	  }
}
```

Update ***src/client/hello.jsx*** with following code to use JSX syntax.
```javascript
import React  from "react";

export default function(props){
	return <div>Hello {props.toWhat}</div>
}

```

Update ***src/client/index.jsx*** with following code:

```javascript
import Hello from "./hello.jsx";
import ReactDOM from "react-dom";
import React from "react";

ReactDOM.render( <Hello toWhat="World"/>, document.getElementById("root"));

```

Now we are ready to see the effect of our changes.

Run the build first.

```shell
npm run build
```

And start the server .

```shell
npm run start
```

Go to [http://localhost:8080](http://localhost:8080) and you should see your component rendered.

See the code [here](https://github.com/randomdevforyou/webpack-react-babel)






