Documentation for Cobalt-Plugin-firebaseAnalytics
# firebaseAnalytics 
This plugin allows Native & WebViews to log events with parameters to Firebase Analytics.
# Installation
Import the plugin to your project as explain [here](https://github.com/cobaltians/cobalt/wiki/Plugins-usage).

Further native steps are needed...
## Android
Follow the steps at https://firebase.google.com/docs/android/setup, except adding the following line to the `build.gradle` file of your app (it is already added as a dependency in the plugin): 

```
compile 'com.google.firebase:firebase-core:11.2.0'
```

## iOS
- Follow the steps at https://firebase.google.com/docs/ios/setup until the end of the 'Add the SDK' section,
- If you want more analytics, follow the instructions at https://firebase.google.com/support/guides/analytics-adsupport,
- In the `application:didFinishLaunchingWithOptions:` `AppDelegate`'s method, call `[FirebaseAnalyticsPlugin configure]`

# How to use
## Android
Get an instance of the plugin from the class method `getInstance(Context)`.

Then use methods `logEvent(String event)` & `logEvent(String event, Bundle parameters)` to log events with params to Firebase Analytics.
## iOS
Use class methods `logEvent:(NSString *)` & `logEvent:(NSString *) withParams:(NSDictionary *)` to log events with params to Firebase Analytics.
## Web
### Quick sample
This samples sends a view_item event as descirbed [here for android](https://firebase.google.com/docs/reference/android/com/google/firebase/analytics/FirebaseAnalytics.Event#VIEW_ITEM) and [here for iOS](https://firebase.google.com/docs/reference/ios/firebaseanalytics/api/reference/Constants#/c:FIREventNames.h@kFIREventViewItem).

```
var params = {
   item_id:  'item42',
   item_name: 'My splendid item'
   quantity: 2
}
cobalt.firebaseAnalytics.logEvent('view_item', params)

```

### logEvent
**cobalt.firebaseAnalytics.logEvent(eventName,eventParams)**
#### `eventName`
eventName is a string. 

If your event is one of the events listed in firebase documentation, the value should match the value described in firebase documentation.
For exemple we used "view_item" that is the value for Android and iOS event VIEW_ITEM as descirbed [here for android](https://firebase.google.com/docs/reference/android/com/google/firebase/analytics/FirebaseAnalytics.Event#VIEW_ITEM) and [here for iOS](https://firebase.google.com/docs/reference/ios/firebaseanalytics/api/reference/Constants#/c:FIREventNames.h@kFIREventViewItem).

You can of course send your own custom event names.
#### `eventParams`
eventName is a object. 

same idea. it should match the values of firebase constants if you want your event to be recognised as a built-in firebase event.

You can of course send your own parameters.
# Debug mode
## Android
- to enable, execute the following line in a terminal:

```
adb shell setprop debug.firebase.analytics.app <package_name>
```
- to disable, execute the following line in a terminal:

```
adb shell setprop debug.firebase.analytics.app .none.
```

## iOS
- In Xcode, select 'Product' > 'Scheme' > 'Edit scheme...'
- Select 'Run' from the left menu.
- Select the 'Arguments' tab.
- In the 'Arguments Passed On Launch' section, add `-FIRAnalyticsDebugEnabled`.
- Check/uncheck it to enable/disable Debug mode.