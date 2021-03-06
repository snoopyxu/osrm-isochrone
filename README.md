osrm-isochrone
---
**Warning: this is experimental**

Generate drivetime [isochrones](http://en.wikipedia.org/wiki/Isochrone_map) from [OpenStreetMap](http://www.openstreetmap.org/) data using [OSRM](http://project-osrm.org/).

![](https://dl.dropbox.com/s/r7hntimgiv5cfeq/Screenshot%202014-11-24%2017.20.32.png?dl=0)


##Install

```sh
npm install osrm-isochrone
```

##Build
An osrm file is required for routing. This can be generated using included binaries. (*Note: this will take a lot of processing power if you are planning to use the entire planet.osm file. More info [here](https://github.com/Project-OSRM/osrm-backend/wiki/Running-OSRM)*)

```sh
#first download an osm file containing the area you need
./node_modules/osrm-isochrone/osrm/lib/binding/osrm-extract mydata.osm -p ./node_modules/osrm-isochrone/osrm/test/data/car.lua
./node_modules/osrm-isochrone/osrm/lib/binding/osrm-prepare mydata.osrm -p ./node_modules/osrm-isochrone/osrm/test/data/car.lua
```

##Usage

```js
var isochrone = require('osrm-isochrone');

var resolution = 25; // sample resolution
var time = 300; // 300 second drivetime (5 minutes)
var network = './dc.osrm' // prebuild dc osrm network file
var location = [-77.02926635742188,38.90011780426885]; // center point

isochrone(location, time, resolution, network, function(err, drivetime) {
  if(err) throw err;
  // a geojson linestring
  console.log(JSON.stringify(drivetime))
});
```
