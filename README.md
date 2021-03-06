# React-Native-Map-Clustering

Simple module that adds map clustering for both iOS and Android.


### Pre requirements:

  - Install 'react-native-maps' module. You can find all information here:
 https://github.com/airbnb/react-native-maps

In general all you have to do to start:

```sh
npm install react-native-maps --save
react-native link react-native-maps
```
  - Minimum versions you need for this module:

        react: >=15.4.0
        react-native >=0.40
        react-native-maps >=0.15.0

### Installation
All you have to do:
```sh
npm install react-native-map-clustering --save
```
### Usage

Usage is very simple:
1. Import MapView
```javascript
import MapView from 'react-native-map-clustering';
```
- Import Marker
```javascript
import Marker from 'react-native-maps';
```
2. Add this to your render method (you can put your own markers and region):
```javascript
<MapView
    region={{latitude: 52.5, longitude: 19.2,
             latitudeDelta: 8.5, longitudeDelta: 8.5}}
    style={{width: mapWidth, height: mapHeight}}>
    <Marker coordinate={{latitude: 52.0, longitude: 18.2}} />
    <Marker coordinate={{latitude: 52.4, longitude: 18.7}} />
    <Marker coordinate={{latitude: 52.1, longitude: 18.4}} />
    <Marker coordinate={{latitude: 52.6, longitude: 18.3}} />
    <Marker coordinate={{latitude: 51.6, longitude: 18.0}} />
    <Marker coordinate={{latitude: 53.1, longitude: 18.8}} />
    <Marker coordinate={{latitude: 52.9, longitude: 19.4}} />
</MapView>
```
3. **That's all!**.

### Demo
![Alt Text](https://raw.githubusercontent.com/venits/react-native-map-clustering/master/demo.gif)

### Advanced Usage

- **For things like animateToRegion or animateToCoordinate and other methods, all you have to do is to refer to _root in your MapView reference**.

Example:
- Create reference to your main MapView.
```javascript
    <MapView
            ref = {(ref)=>mapView=ref}
            ...
    </MapView>
```
- With this reference you can for example animateToRegion like this:
```javascript
    animate(){
       let r = {
            latitude: 42.5,
            longitude: 15.2,
            latitudeDelta: 7.5,
            longitudeDelta: 7.5,
        };
        mapView._root.animateToRegion(r, 2000);
    }
```
### Advanced Usage #2

**If you want to control cluster on click event, here is example of zooming in to your cluster position:**
1. Define you zoom animation function:
```javascript
    animate(coordinate){
       let newRegion = {
            latitude: coordinate.latitude,
            longitude: coordinate.longitude,
            latitudeDelta: mapView.state.region.latitudeDelta - mapView.state.region.latitudeDelta/2,
            longitudeDelta: mapView.state.region.longitudeDelta - mapView.state.region.longitudeDelta/2,
        };
        mapView._root.animateToRegion(newRegion, 1000);
    }
```
2. Add **onClusterPress** prop to your MapView.
```javascript
    <MapView
        ref = {(ref)=>mapView=ref}
        onClusterPress={(coordinate)=>{
            this.animate(coordinate);
        }}
       ...
    </MapView>
```
3. **That's all, now press you cluster and enjoy your zoom animation ;)**
### Advanced Usage #3

**Adding custom cluster design:** (Added in version 1.1.5)

You can pass prop called **customClusterMarkerDesign** with you HTML element that will be used as background for cluster.

Example:
```javascript
    <MapView
        customClusterMarkerDesign =
        {(<Image style = {{width: imageWidth, height:imageHeight}}
        source = {require('./customCluster.png')}/>)}
           ...
    </MapView>
```

**That's all!**

### Extra props to control your clustering
----
| Name               | Type   | Default | Note                                                           |
|--------------------|--------|---------|----------------------------------------------------------------|
| clustering         | bool   | true    | Set true to enable and false to disable clustering.            |
| clusterColor       | String | #F5F5F5 | Background color of cluster.                                         |
| clusterTextColor   | String | #FF5252 | Color of text in cluster.                                      |
| clusterBorderColor | String | #FF5252 | Color of border. Set to transparent if you don't want borders. |
| clusterBorderWidth | Int    | 1       | Width of border. Set to 0 if you don't want borders.           |
| onClusterPress | Function    | null       | Allows you to control cluster on click event.  Function returns coordinate of cluster.         |
| customClusterMarkerDesign | HTML element    | null       | Custom background for your clusters.           |

Example of using props:
```javascript
<MapView
    clustering = {true}
    clusterColor = '#000'
    clusterTextColor = '#fff'
    clusterBorderColor = '#fff'
    clusterBorderWidth = {4}
    region={{latitude: 52.5, longitude: 19.2,
             latitudeDelta: 8.5, longitudeDelta: 8.5}}
    style={{width: mapWidth, height: mapHeight}}>
</MapView>
```

### Some important notes!

**1. Use MapView as you would normally use MapView from react-native-maps (you can use all props). Same for markers.**

**2. Is you pass array of markers make sure it is [] not Set.**

**3.** Module overwrites **onRegionChangeComplete** prop so you will not be able to use it.

**4. Module takes care of region change so you don't have to store region in your component state.**

### Support and donations ;)

If you need help or more customized solution email me: tomasz.przybyl.it@gmail.com

**I am a student so any donations will help me to create more cool modules ;)**

**Thanks for any donations, have a great day and Happy Coding ;)**

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=XN8LRKQRBZJ86)


License
----
MIT
