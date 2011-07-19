# async-ejs
ejs with the ability to add asynchronous functions

## Install 
	    
		npm install async-ejs

## Usage

Say you have 
/index.ejs
/base.ejs

If base want to load the content of index.ejs it can do

<%- load('index.ejs') %>

On the server you need to 

``` js
var aejs = require('async-js');
var common = require('common'); // has a nice step function

...function(request, response) {
	common.step([
		function(next) {
			aejs.renderFile('./base.ejs', next);
		},
		function(src) {
			response.writeHead(200, {
				'content-type': 'text/html',
				'content-length': Buffer.byteLength(src)
			});
			response.end(src);
		}
	], function() {
		response.writeHead(500);
		response.end();
	});
```	

## Interface

render a string

``` js
render(src, options, callback
```

render a file

``` js
renderFile(src, options, callback
```

add a funciton to render
``` js
add(name,func)
```

## Example

Call a unix command from a tempalte

``` js
aejs = require('async-ejs').add(exec,require('child-process').exec);
...
```

now you in your template you can call any unix porccess and render its output :-) 
``` js
...
<body>
<h1>Time: <%- exec('date') %></h1>
Load CNN: <%- exec('curl -L cnn.com') %>
</body>
...
```