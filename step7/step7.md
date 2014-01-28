Step 7: Build the app and run as JavaScript
------

In this step, you use *pub build* to generate the assets for the app and put them into a new directory named *build*. In addition to other tasks, the build process generates minified JavaScript that can be run by any modern browser.

Note that the *one-hour-codelab* directory contains several directories, one for each step, all of which are considered part of the one-hour-codelab application. The build process builds the assets for each directory. Each directory can be individually deployed.

### Check out pubspec.yaml

Double-click the pubspec.yaml file to open it. Click the Source tab at the bottom of the editing pane.

    name: avast_ye_pirates
    description: Write a Dart web app code lab
    dependencies:
      browser: any

#### Key Information

* A *pubspec.yaml* file in a directory identifies the directory and its contents as an application.
* *pubspec.yaml* provides meta-data for the application, such as its name.
* The *pubspec.yaml* file also lists the libraries on which the app depends. The *browser* library needed by this app is hosted on [pub.dartlang.org](https://pub.dartlang.org/) along with many others.
* *any* selects the latest package that matches your SDK.

### Look at the packages directory

In Dart Editor, expand the *packages* directory.

[image]

####  Key Information

* The *packages* directory contains the code for all of the dependencies listed in the *pubspec.yaml* file. These are installed automatically by Dart Editor.
* The *browser* package contains the *dart.js* script that checks for native Dart support.
* The packages must be included in the built application in order for the app to be successfully deployed.

### Run pub build

Select *pubspec.yaml* then select *Tools > Pub Build*, which builds everything under the *one-hour-codelab* directory. The output looks something like this:

    --- Jan 21, 2014 12:41:48 PM Running pub build ... ---
    Building avast_ye_pirates.....
    [Info from Dart2JS]:
    Took 0:00:01.704695 to compile avast_ye_pirates|web/1-blankbadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:05.535304 to compile avast_ye_pirates|web/2-inputnamebadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:02.974628 to compile avast_ye_pirates|web/3-buttonbadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:02.195714 to compile avast_ye_pirates|web/4-classbadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:01.938502 to compile avast_ye_pirates|web/5-localbadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:02.028974 to compile avast_ye_pirates|web/6-piratebadge/piratebadge.dart.
    Built 45 files!

#### Key Information

* The *pub build* command creates a *build* directory that contains subdirectories for every step in the code lab.
* The *build* directory contains everything needed to deploy the entire project (all six steps).

### Look at the *build* directory

Expand the *build* directory. Note that it contains a subdirectory for each step of the code lab. Expand the *6-piratebadge* directory.

[image]

#### Key Information

* The *piratebadge.dart.js* file is a JavaScript file that has been minified. When deployed, this file runs in the browser.
* The *packages* directory contains the package dependencies.
* Note that the directory contains no *piratebadge.dart* file. It is not needed to deploy the app to JavaScript.
* Each subdirectory of *build* contains all of the files needed for the app to be deployed separately.

### Run the app as JavaScript

Open the app. Select *File > Open File…* in a browser such a Firefix or Safari and select the *one-hour-codelab/build/6-piratebadge/piratebadge.html* file.

#### Key Information

* The app runs on the local machine using the *file* protocol. To share your app with others, you need to deploy the app to a hosting service.
