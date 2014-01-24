Step 4: Create a PirateName class
-----

In this step, you change only the Dart code. You create a class to represent a pirate name. When created, an instance of this class randomly selects a name and appellation from a list, or optionally you can provide a name and an appellation to the constructor.

### Edit piratebadge.dart.

Add an import to the top of the file.

#### piratebadge.dart
    import 'dart:html';
    import 'dart:math' show Random;

#### Key Information

* Using the *show* keyword, you can import only the classes, functions, or properties you need.
* *Random* provides a random number generator.

Add a class declaration to the bottom of the file.

#### piratebadge.dart
    ...
    class PirateName {
    }

#### Key Information

* The class declaration provides the class name.

Create a class-level Random object.

#### piratebadge.dart
    class PirateName {
      static final Random indexGen = new Random();
    }

#### Key Information

* *static* defines a class-level field. That is, the random number generator is shared with all instances of this class.
* Dart Editor italicizes static names.
* Use *new* to call a constructor.

Add two instance variables to class, one for the first name and one for the appellation.

#### piratebadge.dart
    class PirateName {
      static final Random indexGen = new Random();
      String _firstName;
      String _appellation;
    }

#### Key Information

* Private variables start with underscore (*_*). Dart has no *private* keyword.

Create two static lists within the class that provide a small collection of names and appellations to choose from.

#### piratebadge.dart
    class PirateName {
      ...
      static final List names = [
        'Anne', 'Mary', 'Jack', 'Morgan', 'Roger',
        'Bill', 'Ragnar', 'Ed', 'John', 'Jane' ];
      static final List appellations = [
        'Black','Damned', 'Jackal', 'Red', 'Stalwart', 'Axe',
        'Young', 'Old', 'Angry', 'Brave', 'Crazy', 'Noble'];
    }

#### Key Information

* *final* variables cannot change.
* Lists are built into the language. These lists are created using list literals.
* The *List* class provides the API for lists.

Provide a constructor for the class.

#### piratebadge.dart
    class PirateName {
      ...
      PirateName({String firstName, String appellation}) {
        if (firstName == null) {
          _firstName = names[indexGen.nextInt(names.length)];
        } else {
          _firstName = firstName;
        }
        if (appellation == null) {
          _appellation = appellations[indexGen.nextInt(appellations.length)];
        } else {
          _appellation = appellation;
        }
      }
    }

#### Key Information

* Constructors have the same name as the class.
* The parameters enclosed in curly brackets (*{* and *}*) are optional, named parameters.
* The *nextInt()* function gets a new random integer from the random number generator.
* Use square brackets (*[* and *]*) to index into a list.
* The *length* property returns the number of items in a list.
* The code uses a random number as an index into the list.

Provide a getter for the pirate name.

#### piratebadge.dart

class PirateName {
  ...
  String get pirateName =>
    _firstName.isEmpty ? '' : '$_firstName the $_appellation';
}

#### Key Information

* Getters are special methods that provide read access to an object’s properties.
* The ternary operator *?:* is short-hand for an if-then-else statement.
* String interpolation (*'$_firstName the $_appellation'*) lets you easily build strings from other objects.
* The fat arrow ( *=> expr;* ) syntax is a shorthand for *{ return expr; }*.

Modify the function *setBadgeName()* to use a PirateName instead of a String:

#### piratebadge.dart
    void setBadgeName(PirateName newName) {
      querySelector('#badgeName').text = newName.pirateName;
    }

#### Key Information

* This code calls the getter to get the PirateName as a string.

Change *updateBadge()* to generate a PirateName based on the input field value.

#### piratebadge.dart
    void updateBadge(Event e) {
      String inputName = (e.target as InputElement).value;
      
      setBadgeName(new PirateName(firstName: inputName));
      ...
    }

#### Key Information

* The call to the constructor provides a value for one optional named parameter.

Change *generateBadge()* to generate a PirateName instead of using *Anne Bonney*.

#### piratebadge.dart
    void generateBadge(Event e) {
      setBadgeName(new PirateName());
    }

* In this case, the call to the constructor passes no parameters.

###  Run the app.

Save your files with **File > Save All**.
Use the Run button in Dart Editor to run the app.
Compare your app to the one running below.
Type in the input field. Remove the text from the input field. Click the button.

[Image]

#### Problems?

Check your code against the files in *4-classbadge*.

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/4-classbadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/4-classbadge/piratebadge.dart)


