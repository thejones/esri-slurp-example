#esri-slurp-example

The purpose of this repo is to show how to do a Dojo build with Esri JSAPI source code downloaded using [grunt-esri-slurp](https://www.npmjs.org/package/grunt-esri-slurp). The build profile and grunt configuration draw heavily from the [AGRC JavaScript Project Boilerplate](https://github.com/agrc/AGRCJavaScriptProjectBoilerPlate), which is itself based on the [Dojo Boilerplate](https://github.com/csnover/dojo-boilerplate). However, the configurations in this repo are pared down to demonstrate only what is necessary to create a custom Dojo build of a simple "app" featuring an Esri map (based on the [Create a map sample page](https://developers.arcgis.com/javascript/jssamples/map_simple.html)).

##Instructions
You must have [Node.js](http://nodejs.org/) installed as well as the [Grunt CLI](http://gruntjs.com/getting-started) prior to running the steps below.

Install Grunt tasks with npm:
```bash
npm install
```

Download Dojo and other dependencies with bower:
```bash
bower install
```

Download the AMD build of the ArcGIS API for JavaScript with [grunt-esri-slurp](https://www.npmjs.org/package/grunt-esri-slurp):
```bash
grunt slurp
```

To verify that all dependencies are in place, you can serve the unbuilt app with:
```bash
grunt connect:src
```
Then browse to `http://localhost:9000/` and verify that it works.

Finally, build the app:
```bash
grunt build
```

To verify that the build was successful, you can serve the built app with:
```bash
grunt connect:dist
```
Then browse to `http://localhost:9000/` and verify that it
 works. You can inspect the network traffic to verify that the build version of the app requests fewer and smaller scripts (see below).

##Comparing the Built App
In order to determine if our build improves the user experience, we need to verify that the built page makes fewer script requests and that the size of the scripts requested is smaller than the unbuilt version of the page. We also need to verify the same as compared to similar pages that reference the [standard and compact CDN hosted builds of the API](https://developers.arcgis.com/javascript/jshelp/inside_compactbuild.html). The "app" in this example is based on the [Create a map sample page](https://developers.arcgis.com/javascript/jssamples/map_simple.html), and for convenience, this repo includes a copy of that page as well as a copy that uses the compact build (under the `samples` folder).

I've compiled a comparison of the file requests and sizes between the different builds in [a Google Spreadsheet](http://bit.ly/1p733Q7). The results show that there's a significant improvement over an unbuilt app (no surprise), and marginal improvements over the CDN builds. However, when creating builds for more complex, real-world applications with many modules, you will see significant improvements over the CDN builds in most cases.

## Reducing the Size (on Disk) of Build Output
By default the Dojo build outputs uncompressed versions of the source files as well as source maps to aid in debugging. If you don't need the source maps or uncompressed files (e.g. if you debug using the unbuilt source), then you can save time and space while running the build by uncommenting the following line in app.profile.js:
```js
// useSourceMaps: false
```

You can further reduce the size of the output directory by 50% or more by running the following grunt commands *after* the build:
```bash
grunt clean:uncompressed
grunt clean:stripped
```

##Resources
- [grunt-esri-slurp](https://www.npmjs.org/package/grunt-esri-slurp)
- [AGRC JavaScript Project Boilerplate](https://github.com/agrc/AGRCJavaScriptProjectBoilerPlate)
- [Dojo Boilerplate](https://github.com/csnover/dojo-boilerplate)
- [Dojo Build Tutorial](http://dojotoolkit.org/documentation/tutorials/1.9/build/)
- [Dojo Build Reference Guide](http://dojotoolkit.org/reference-guide/1.9/build/index.html)
- [ArcGIS API for JavaScript Compact Build](https://developers.arcgis.com/javascript/jshelp/inside_compactbuild.html)

##Credit
There's nothging new here. The hard work has already been done by the estimable [@steveoh](https://github.com/steveoh) and [@stdavis](https://github.com/stdavis). This is just an attempt to make the great work that they've already done a bit more approachable (even though [they mock me](https://github.com/tomwayson/esri-slurp-example/issues/2#issuecomment-55122452)).
