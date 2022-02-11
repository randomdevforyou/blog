 ---
title: "Webpack + react"
date: 2022-02-10T14:32:51+05:30
draft: false
---

 In this article we will see how to do basic react setup. We will be using webpack for bundling the client code. Please see [article](/posts/javascript/tool/webpack/) to set up webpack. You can download webpack-starter repo from [here](https://github.com/randomdevforyou/webpack-starter)

 Firsly we will be installing ***react*** and ***react-dom*** as dev dependencies.

 ```shell
 npm install --save-dev react react-dom
 ```

Create a simple hello component in ***src/client/hello.js*** and add following code to it

```javascript

import React  from "react";

export default class Hello extends React.Component {
	render() {
	  return React.createElement('div', null, `Hello ${this.props.toWhat}`);
	}
  }

```

Now we will be adding ***src/client/index.js*** which will import ***Hello*** component to render it on the page. To do that add following code

```javascript

import Hello from "./hello";
import ReactDOM from "react-dom";
import React from "react";

ReactDOM.render(
	React.createElement(Hello, {toWhat: 'World'}, null),
	document.getElementById('root')
);

```

Let's do the bundling by running the following command

```shell
npm run build
```

And start the server 

```shell
npm run start
```

Go to [http://localhost:8080](http://localhost:8080) and you should see your component rendered.

See the code [here](https://github.com/randomdevforyou/react-starter)






