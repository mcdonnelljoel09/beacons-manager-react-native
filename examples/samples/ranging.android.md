# Fully detailed documentation for "ranging beacons in Android"

This documentation give a deeper explanation on how to monitor (*but ranging only*) beacons in Android.

This documentation is linked to the sample code [ranging.android.js](./ranging.android.js)

## 1- start detection for beacon of your choice

Before starting tell the library what kind of beacon you want to manage.

```javascript
// dealing with iBeacons:
Beacons.detectIBeacons();
```

[See matching lines in sample example]()

## 2- start ranging

Tell Android what you want to range by defining a desired `region` object.


```javascript
// start ranging beacons
Beacons
  .startRangingBeaconsInRegion(identifier, uuid)
  .then(() => console.log('Beacons ranging started succesfully'))
  .catch(error => console.log(`Beacons ranging not started, error: ${error}`));
```

[See matching lines in sample example]()

## 3- register events

Monitoring now works.

You have to register events to know and use about data from enter region and leave region events.

```javascript

// Ranging: Listen for beacon changes
DeviceEventEmitter.addListener(
  'beaconsDidRange',
  (data) => {
    console.log('beaconsDidRange data: ', data);
    this.setState({ rangingDataSource: this.state.rangingDataSource.cloneWithRows(data.beacons) });
  }
);
```

[See matching lines in sample example]()


## 4- on componentWillUnMount: unregister event and stop ranging

A good practise is to ALWAYS unregister events in `componentWillUnMount`.

Tell Android to stop ranging at the same time.

```javascript

// stop ranging beacons:
Beacons
.stopRangingBeaconsInRegion(identifier, uuid)
.then(() => console.log('Beacons ranging stopped succesfully'))
.catch(error => console.log(`Beacons ranging not stopped, error: ${error}`));

// remove ranging event we registered at componentDidMount
DeviceEventEmitter.removeListener('beaconsDidRange');
```

[See matching lines in sample example]()
