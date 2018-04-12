# AR_Navigation
AR Navigation

## Introduction
The Design Interactive AR Navigation (DI-ARN) application is an ARCore enabled application that reads in a GeoPackage file and provides AR navigation assistance and displays the following information:
  * Pre-defined routes: Layer name must begin with route_
  * Critical navigation points: Layer name must begin with cnp_
  * Points of Interests: Layer name must begin with poi_
The DI-ARN application is designed to run on Android platforms version 7.0+ and requires ARCore support. To see a list of ARCore supported devices please visit: https://developers.google.com/ar/discover/

#### About
The DI-ARN application was developed using Unity 3D 2017.3.1f1 with utilizing the following technologies:
  * Mapbox/Mapbox AR SDKs (https://www.mapbox.com/)
  * GeoPackage Android ( https://github.com/ngageoint/geopackage-android )
  * ARCore (https://developers.google.com/ar/discover/)
DI-ARN has been tested locally on the Galaxy S7, Galaxy S8 and Google Pixel devices. The accuracy of the navigation is greatly dependent on GPS accuracy the device has. 

#### Install Instructions
The included .apk file will allow you to install the application on an Android phone without needing to build from source.

#### Build Instructions
##### Unity Application
To build the Unity Application you will need Unity 3D 2017.3.1f1 or higher as well as a development environment setup for building Android projects. Please see the following to get started:
  * https://docs.unity3d.com/Manual/android-GettingStarted.html
  * https://developer.android.com/studio/index.html
  
Open the AR_Navigator project in Unity located under Unity App/Unity. Once the import has been completed change the output platform to Android. The project should be ready to be built.

##### Android Library
There is a native integration layer that communicates with the GeoPackage Android library from within Unity. This is located under the AndroidPlugin folder. Open the project in Android Studio (or run Gradle from the command line directly) and run the :arnavigationplugin-->Tasks-->build-->build task. This will generate an AAR located under /AndroidPluginarnavigationplugin/build/outputs/aar. Place the AAR in the following location to update the AAR library: /Unity App/Unity/AR_Navigator/Assets/Plugins/Android

#### Usage Instructions
After installing the application run the "AR Navigation" application once. Upon first launch it will request permissions. If location and storage permissions are not requested automatically please set them under the App Info menu in the Android Settings. Upon first launch you should see a pass through video feed, a Compass and Lat/Lon indicator in the top middle of the screen. If the Lat/Lon indicator stays at 0,0 this means that the app does not have location permissions and it needs to be set. Without any GeoPackage files loaded into the system you have the ability to Switch Modes which will display a top down view of the devices current location.

To add GeoPackage files to the system navigate to the following folder on the Android device: Android/data/com.designinteractive.AR_Navigation/files and create a folder titled "GeoPackage". Place the geopackage files that you would like to view in this folder. The application currently will load all GeoPackage files loaded in this folder. Points are loaded into the system following this pattern: layer name + id + fid. At this point it will also not do naming deconfliction between names and will not load a second apperance correctly into the scene.

Once the data has been loaded into the system restart the application. For best results face north when loading the GeoPackage data and load the GeoPackage Data before pressing the Switch Mode button. Once the data has been loaded into the scene, you can press the Switch Mode button to see the top down view of the map. If major issues occur with the placement or orientation, an app restart is the best way to resolve at this time.

Some Notes:
  * Rotating the map with your fingers in the Table Top Mode will update your position and rotation.
  * When rotating or moving the map any routes or area of interests lines will rotate and move with the camera, to fix this issue tap the screen once to reset the lines to their correct orientations.
  * As you move through the environment, if the ARCore tracking is interrupted it can cause issues. In my testing this mostly occured with the Galaxy S7.
  * As you move through the environment, the accuracy can shift of your position in relation to objects.
  * For more information on the Mapbox AR integration and other issues that are currently present in their SDK please visit: https://github.com/mapbox/mapbox-unity-sdk/blob/develop/README-AR.md
