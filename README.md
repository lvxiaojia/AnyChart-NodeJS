[<img src="https://cdn.anychart.com/images/logo-transparent-segoe.png?2" width="234px" alt="AnyChart - Robust JavaScript/HTML5 Chart library for any project">](https://anychart.com)

# AnyChart NodeJS module.

AnyChart NodeJS module provides an easy way to generate SVG, JPG and PNG images of the charts on the server side.
Consider it for reporting systems that send charts by email or social networks sharing applications.

## Table of Contents

* [Download and install](#download-and-install)
* [Quick start](#quick-start)
* [Export Module API](#export-module-api)
* [Examples](#examples)
* [Contacts](#contacts)
* [Links](#links)
* [License](#license)

## Download and install
You can install AnyChart NodeJS export module using **npm**, **bower** or **yarn**:

* `npm install anychart-nodejs`
* `bower install anychart-nodejs`
* `yarn add anychart-nodejs`

AnyChart NodeJS module requires [ImageMagic](https://www.imagemagick.org) to create JPG and PNG images.
Visit Image Magic [install](https://www.imagemagick.org/script/index.php) page for details.
**Note for Windows users:** you have to create environment variable as described in [Image Magic: Advanced Windows Installation](https://www.imagemagick.org/script/advanced-windows-installation.php) article.

## Quick start 
To generate JPG image a chart, create index.js file with the following content:
```javascript
// require file system and jsdom
var fs = require('fs');
var jsdom = require('jsdom').jsdom;

// create default jsdom view
var d = jsdom('<body><div id="container"></div></body>');
var w = d.defaultView;

// require anychart and anychart export modules
var anychart = require('anychart')(w);
var anychartExport = require('anychart-nodejs')(anychart);

// create and a chart to the jsdom defaultView 
var chart = anychart.pie([10, 20, 7, 18, 30]);
chart.container('container');
chart.bounds(0, 0, 800, 600);
chart.draw();

// generate JPG image and save it to a file
anychartExport.exportTo(chart, 'jpg').then(function(image) {
  fs.writeFile('anychart.jpg', image, function(fsWriteError) {
    if (fsWriteError) {
      console.log(fsWriteError.message);
    } else {
      console.log('Complete');
    }
    process.exit(0);
  });
}, function(generationError) {
  console.log(generationError.message);
  process.exit(1);
});
```

Run the following command in the command line:
```
$ node index.js
>> Complete
```


## Export Module API
### `exportTo(target, options, callback):Promise`
Generate an image asynchronously.  
**Parameters:**  

Name | Type | Description
--- | --- | ---
`target` | SVG string, a chart or a stage instance | Object to be exported.
`outputType` | string | Output type, possible values are: svg, jpg, png.
`callback` | Function | The result callback.

**Returns:**  
Promise if no callback passed.

### `exportToSync(target, options):Object`
Generate an image synchronously.  

**Parameters:**

Name | Type | Description
--- | --- | ---
`target` | SVG string, a chart or a stage instance | Object to be exported.
`outputType` | string | Output type, possible values are: svg, jpg, png.

**Returns:**  
ArrayBuffer

### `loadFont(path, callback):Promise`
Loads the specified font asynchronously.

**Parameters:**

Name | Type | Description
--- | --- | ---
`path` | string | Path to the font.
`callback` | Function | The result callback.

**Returns:**  
Promise if no callback passed.


### `loadFontSync(path):Object`
Loads the specified font synchronously.

**Parameters:**

Name | Type | Description
--- | --- | ---
`path` | string | Path to font.
**Returns:**  
Object

### `loadDefaultFonts(callback):Promise`
Asynchronously loads default fonts. Gets result as an array of resulting
font objects that are available in the callback, returns Promise.

**Parameters:**

Name | Type | Description
--- | --- | ---
`callback` | Function | The result callback.


### `loadDefaultFontsSync():Array.<Object>`
Loads default fonts synchronously.  
**Returns:**  
Array.<Object>

## Examples 
Please, take a look at examples:
* [Report Generation Utility](https://github.com/anychart-integrations/nodejs-report-generation-utilily)
* [Image Generation Utility](https://github.com/anychart-integrations/nodejs-image-generation-utility)
* [Export Server Application](https://github.com/anychart-integrations/nodejs-export-server-application)

## Contacts

* Web: [www.anychart.com](www.anychart.com)
* Email: [contact@anychart.com](mailto:contact@anychart.com)
* Twitter: [anychart](https://twitter.com/anychart)
* Facebook: [AnyCharts](https://www.facebook.com/AnyCharts)
* LinkedIn: [anychart](https://www.linkedin.com/company/anychart)

## Links

* [AnyChart Website](http://www.anychart.com)
* [Download AnyChart](http://www.anychart.com/download/)
* [AnyChart Licensing](http://www.anychart.com/buy/)
* [AnyChart Support](http://www.anychart.com/support/)
* [Report Issues](https://github.com/AnyChart/AnyChart-NodeJS/issues)
* [AnyChart Playground](http://playground.anychart.com)
* [AnyChart Documentation](http://docs.anychart.com)
* [AnyChart API Reference](http://api.anychart.com)
* [AnyChart Sample Solutions](http://www.anychart.com/solutions/)
* [AnyChart Integrations](http://www.anychart.com/integrations/)

## License

[© AnyChart.com - JavaScript charts](http://www.anychart.com). AnyChart NodeJS module is released under the [Apache 2.0 License](https://github.com/AnyChart/AnyChart-NodeJS/blob/master/LICENSE).
