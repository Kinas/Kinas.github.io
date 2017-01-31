Leaflet.HeightProfile
=====================

![preview](https://cloud.githubusercontent.com/assets/10322094/22474104/472bcc88-e7db-11e6-8c9e-7e1d53cd0b57.png)

1. [What is this?](https://github.com/GIScience/Leaflet.Heightgraph#what-is-this)
2. [How to use this library](https://github.com/GIScience/Leaflet.Heightgraph#how-to-use)

### What is this?

This plugin is under development and is inspired by [MrMufflon/Leaflet.Elevation](https://github.com/MrMufflon/Leaflet.Elevation). You may use this plugin to view an interactive height profile of polylines and its segments using d3js. The input data may consist of different types of attributes you wish to display.

Supported Browsers:
- Chrome
- Firefox

### Supported data:
Input data has to be of type [GeoJSON-Format](http://geojson.org/). This may consist of feature collections corresponding to a certain attribute which could - as an example - be surface or gradient information. Each `FeatureCollection` comprises to a certain `attribute` in its `properties` (e.g. `'summary': 'steepness'`) and has a list of variable length of `LineString` features with coordinates (including height values) and the `attributeType` corresponding to the certain type of attribute within this segment (in this case an index of steepness) declared in its `properties`. 

[Demo](https://giscience.github.io/Leaflet.Heightgraph)

```javascript
var FeatureCollections = [{
    "type": "FeatureCollection",
    "features": [{
        "type": "Feature",
        "geometry": {
            "type": "LineString",
            "coordinates": [
                [8.6865264, 49.3859188, 114.5],
                [8.6864108, 49.3868472, 114.3],
                [8.6860538, 49.3903808, 114.8]
            ]
        },
        "properties": {
            "attributeType": "3"
        }
    }, {
        "type": "Feature",
        "geometry": {
            "type": "LineString",
            "coordinates": [
                [8.6857921, 49.3936309, 114.4],
                [8.6860124, 49.3936431, 114.3]
            ]
        },
        "properties": {
            "attributeType": "0"
        }
    }],
    "properties": {
        "Creator": "OpenRouteService.org",
        "records": 2,
        "summary": "Steepness"
    }
}];
```

### Optional:
You may add a mappings object to customize the colors and labels in the height graph. Without adding custom mappings the segments and labels within the graph will be displayed in random colors created with chroma.js. Each key of the object must correspond to the `summary` key in `properties` within the `FeatureCollection`.

```javascript
colorMappings.Steepness = {
    '3': {
        text: '1-3%',
        color: '#F29898'
    },
    '0': {
        text: '4-6%',
        color: '#E07575'
    }
};
```

### How to use:

```javascript
// all used options are the default values
var hg = L.control.heightgraph({
    width: 800,
    height: 280,
    margins: {
        top: 10,
        right: 30,
        bottom: 55,
        left: 50
    },
    position: "bottomright",
    mappings: undefined || colorMappings
});
hg.addTo(map);
hg.addData(geojson);
L.geoJson(geojson).addTo(map);
    
