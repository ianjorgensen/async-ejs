# async-ejs
ejs with the ability to add asynchronous functions

## Install 
	    
npm install async-ejs

## Usage
Say you have
 
```
/index.ejs
/base.ejs
```

If base wants to load the content of index.ejs it can do

``` js
Template stuff here
<%- load('index.ejs') %>
more template stuff
```	

On the server you need to 

``` js
var aejs = require('async-js');
var common = require('common'); //this has a nice step function

aejs.renderFile('./base.ejs', function(err, result) {
	// yay async!
}
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

add a function to render
``` js
add(name,func)
```

## Example
Call a unix command from a template and 

``` js
aejs = require('async-ejs').add(exec,require('child_process').exec);

```

now you in your template you can call any unix process and render its output

```	
Template stuff
Time: <%- exec('date') %>
Load CNN: <%- exec('curl -L cnn.com') %>
Load another template: <%- load('filename') %>
More template stuff
```