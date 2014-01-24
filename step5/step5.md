Step 5: Save to local storage
-----

In this step, you give the app some persistence by saving the badge name to local storage each time it changes. When you restart the app, it initializes the badge from the saved name.

###  Edit piratebadge.dart.

Import the JSON converter from the *dart:convert* library.

#### piratebadge.dart
    import 'dart:html';
    import 'dart:math' show Random;
    import 'dart:convert' show JSON;

#### Key Information

* *JSON* provides convenient access to the most common JSON use cases.

Add a named constructor to the PirateName class.

#### piratebadge.dart
    class PirateName {
      ...
      PirateName.fromJSON(String jsonString) {
        Map storedName = JSON.decode(jsonString);
        _firstName = storedName['f'];
        _appellation = storedName['a'];
      }
    }

#### Key Information

* The constructor creates a new PirateName instance from a JSON-encoded string.
* *PirateName.fromJson* is a named constructor.
* *JSON.decode()* parses a JSON string and creates Dart objects from it.
* The pirate name is decoded into a *Map* object.

Add a getter to the PirateName class that encodes a pirate name in a JSON string.

#### piratebadge.dart
    class PirateName {
      ...
      String get jsonString => '{ "f": "$_firstName", "a": "$_appellation" } ';
    }

#### Key Information

* The getter formats the JSON string using the map format.

Declare a top-level string.

#### piratebadge.dart
    final String TREASURE_KEY = 'pirateName';
    
    void main() {
      ...
    }

#### Key Information

* You store key-value pairs in local storage. This string is the key. The value is the pirate name.

Save the pirate name when the badge name changes.

#### piratebadge.dart
    void setBadgeName(PirateName newName) {
      if (newName == null) {
        return;
      }
      querySelector('#badgeName').text = newName.pirateName;
      window.localStorage[TREASURE_KEY] = newName.jsonString;
    }

#### Key Information

* Local storage is provided by the browser’s *Window*.

Add a top-level function called *getBadgeNameFromStorage()*.

#### piratebadge.dart
    void setBadgeName(PirateName newName) {
      ...
    }
    PirateName getBadgeNameFromStorage() {
      String storedName = window.localStorage[TREASURE_KEY];
      if (storedName != null) {
        return new PirateName.fromJSON(storedName);
      } else {
        return null;
      }
    }

#### Key Information

* The function retrieves the pirate name from local storage and creates a PirateName object from it.

Call the function from the main() function.

#### piratebadge.dart
    void main() {
      ...
      setBadgeName(getBadgeNameFromStorage());
    }

#### Key Information

* Initialize the badge name from local storage.

### Run the app.

Save your files with **File > Save All**.
Use the Run button in Dart Editor to run the app.
Compare your app to the one running below.
Click the button to put a name on the badge. Start the app again by duplicating this window.

[Image]

#### Problems?
Check your code against the files in *5-localbadge*.

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/5-localbadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/5-localbadge/piratebadge.dart)


