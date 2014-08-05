# Remote Image Widget [![Titanium](http://www-static.appcelerator.com/badges/titanium-git-badge-sq.png)](http://www.appcelerator.com/titanium/) [![Alloy](http://www-static.appcelerator.com/badges/alloy-git-badge-sq.png)](http://www.appcelerator.com/alloy/)

This widget for the [Appcelerator](http://www.appcelerator.com) Titanium Alloy MVC framework provides a view that supports remote image loading with full image caching. Image caching is made using a fork of [TiCachedImages](https://github.com/sukima/TiCachedImages).

## Installing
### Get it [![gitTio](http://gitt.io/badge.png)](http://gitt.io/component/com.baboonmedia.remoteimage)
Download this repository and consult the [Alloy Documentation](http://docs.appcelerator.com/titanium/latest/#!/guide/Alloy_XML_Markup-section-35621528_AlloyXMLMarkup-ImportingWidgets) on how to install it, or simply use the [gitTio CLI](http://gitt.io/cli):

`$ gittio install com.baboonmedia.remoteimage`

## Usage

Just require the widget on a view:

```xml
<Widget src="com.baboonmedia.remoteimage" id="RemoteImage">
    <View role="loadingerror">
       <ActivityIndicator id="activityIndicator" role="activityindicator" />
       <Label>Unable to load image. Tap to retry</Label>
    </View>
</Widget>
```

### Child Views

Inside the widget you can assign a couple of child views with `role` assigned to display the activity indicator and an error message.

- `loadingerror` - The view with this `role` will be shown when there was an error loading the remote image with a `singletap` listener attached to it to retry laoding of the image.
- `activityindicator` - The activity indicator to be shown while loading the image. It can be any kind of view as long as it has a `show()`and `hide()`method.

## Widget Specific Properties

Besides the common Titanium properties of a view, the widget accepts the following properties to determine it's behavior.

| Property | Type | Description |
| -------- | ---- | ------- |
| image | String | Full url of the image to load. |
| autoload | Boolean | If set to `false` the image won't be loaded until the `load` method is called. |
| gethires | Boolean |  If this property is set to `true` then the url will be parsed to include the @2x suffix. For example, if url is set to http://mysite.com/image.jpg and `gethires` is set to `true`, then the url will be converted to http://mysite.com/image@2x.jpg. |
| onDone | Function | Function to be called when the image has been loaded. The callback will be sent a `msg` string with the full details of the cached file. |
| onError | Function | Function to be called if the image has failed loading. The callback will be sent an `error` string with the error message. |

## Run-time styling

You can use `$.myId.applyProperties()` to apply any new properties to the widget after it has been automatically initialized:

```javascript
$.myId.applyProperties({
	autoload: true,
    image: 'http://mysite.com/otherimage.jpg',
    backgroundColor: 'black'
});
```

## Public Methods

| Method | Description |
| ------ | ----------- |
| applyProperties() | Method to assign new properties to the widget |
| load() | If the image hasn't been loaded start loading the image. This method has to be called manually if `autoload` is set to `false` |
| setImage() | Sets a new image and loads it if `autoload` is set to `true` |
| getImage() | Returns the url of the current image |
| clean() | It's highly recommended that you call this method before disposing from the object to prevent memory leaks. |
| gc() | Calls the garbage collector to clean any expired images. Upon initialization the garbage collector is called. |
| wipeCache() | Clear everything on the cache, regardless if it has expired or not. |

## Configuration

To set configuration set them in your `app/config.json`.

You can adjust the following variables:

| Variable | Default | Description |
| -------- | ------- | ----------- |
| remoteimage_timeout | 120000 | Sets the `http` timeout. |
| remoteimage_property_key | RemoteImage |  The `Ti.App.Property` key to use for storing the cache metadata. |
| remoteimage_directory | RemoteImageCache | The directory to save the cache files. The `applicationDataDirectory` is prefixed. |
| remoteimage_expiration | 8640000 | How long in miliseconds a cached file is considered expired since the last time it was requested. |
| remoteimage_requests | 20 | The number of simultaneous network requests allowed. |
| remoteimage_debug | 0 | Set to `1` to display debug messages. |

## Changelog

- 1.1 Fixed a bug on the debug display
- 1.0 Initial version

## Licenses

This work is released under the MIT license.

[TiCachedImages](https://github.com/sukima/TiCachedImages) released under the MIT license.

This work includes an embedded and modified version of [then/promise](https://github.com/then/promise) which is Copyright (c) 2013 Forbes Lindesay and release under the MIT license.

Appcelerator, Appcelerator Titanium and associated marks and logos are trademarks of Appcelerator, Inc.

Titanium is Copyright (c) 2008-2012 by Appcelerator, Inc. All Rights Reserved.
