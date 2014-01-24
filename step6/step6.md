Step 6: Read names from JSON-encoded file
-----

In this step, you change the PirateName class to get the list of names and appellations from a JSON file. This gives you a chance to add more names and appellations to the program.

### Create piratenames.json.

Use **File > New File…** to create a JSON-encoded file named *piratenames.json* with the following content.
Put the file in *1-blankbadge* alongside the Dart and HTML files you’ve been editing.

#### piratenames.json
    { "names": [ "Anne", "Bette", "Cate", "Dawn",
                "Elise", "Faye", "Ginger", "Harriot",
                "Izzy", "Jane", "Kaye", "Liz",
                "Maria", "Nell", "Olive", "Pat",
                "Queenie", "Rae", "Sal", "Tam",
                "Uma", "Violet", "Wilma", "Xana",
                "Yvonne", "Zelda",
                "Abe", "Billy", "Caleb", "Davie",
                "Eb", "Frank", "Gabe", "House",
                "Icarus", "Jack", "Kurt", "Larry",
                "Mike", "Nolan", "Oliver", "Pat",
                "Quib", "Roy", "Sal", "Tom",
                "Ube", "Val", "Walt", "Xavier",
                "Yvan", "Zeb"],
      "appellations": [ "Awesome", "Black", "Captain", "Damned",
                "Even", "Fighter", "Great", "Hearty",
                "Irate", "Jackal", "King", "Lord",
                "Mighty", "Noble", "Old", "Powerful",
                "Quick", "Red", "Stalwart", "Tank",
                "Ultimate", "Vicious", "Wily", "aXe",
                "Young", "Zealot",
                "Angry", "Brave", "Crazy", "Damned",
                "Eager", "Fool", "Greedy", "Hated",
                "Idiot", "Jinxed", "Kind", "Lame",
                "Maimed", "Naked", "Old", "Pale",
                "Queasy", "Rat", "Sandy", "Tired",
                "Ugly", "Vile", "Weak", "Xeric",
                "Yellow", "Zesty"]}

#### Key Information

* The file contains a JSON-encoded map, which contains two lists of strings.

### Edit piratebadge.html.

Disable the input field and the button.

#### piratebadge.html
    ...
      <div>
        <input type="text" id="inputName" maxlength="15" disabled>
      </div>
      <div>
        <button id="generateButton" disabled>Aye! Gimme a name!</button>
      </div>
    ...

#### Key Information

* The Dart code enables the text field and the button after the pirate names are successfully read from the JSON file.

### Edit piratebadge.dart.

Add an import to the top of the file.

#### piratebadge.dart
    import 'dart:html';
    import 'dart:math' show Random;
    import 'dart:convert' show JSON;
    import 'dart:async' show Future;

#### Key Information

* The *dart:async* library provides for asynchronous programming.
* A *Future* provides a way to get a value in the future. (For JavaScript developers: Futures are similar to Promises.)

Replace the names and appellations lists with these static, empty lists:

#### piratebadge.dart
    class PirateName {
      ...
      static List<String> names = [];
      static List<String> appellations = [];
      ...
    }

#### Key Information

* **Be sure to remove *final* from these declarations.**
* *[]* is equivalent to *new List()*.
* A List is a generic type—a List can contain any kind of object. If you intend for a list to contain only strings, you can declare it as *List<String>*.

Add two static functions to the PirateName class:

#### piratebadge.dart
    class PirateName {
      ...
    
      static Future readyThePirates() {
        var path = 'piratenames.json';
        return HttpRequest.getString(path)
            .then(_parsePirateNamesFromJSON);
      }
      
      static _parsePirateNamesFromJSON(String jsonString) {
        Map pirateNames = JSON.decode(jsonString);
        names = pirateNames['names'];
        appellations = pirateNames['appellations'];
      }
    }

#### Key Information

* *HttpRequest* is a utility for retrieving data from a URL.
* *getString()* is a convenience method for doing a simple GET request that returns a string.
* The code uses a *Future* to perform the GET asynchronously.
* The callback function for *.then()* is called when the Future completes successfully.
* When the Future completes successfully, the pirate names are read from the JSON file.
* *readyThePirates* returns the Future so the main program has the opportunity to do something after the file is read.

Add a top-level variable.

#### piratebadge.dart
    SpanElement badgeNameElement;
    
    void main() {
      ...
    }

#### Key Information

* Stash the span element for repeated use instead of querying the DOM for it.

Make these changes to the *main()* function.

#### piratebadge.dart
    void main() {
      InputElement inputField = querySelector('#inputName');
      inputField.onInput.listen(updateBadge);
      genButton = querySelector('#generateButton');
      genButton.onClick.listen(generateBadge);
      
      badgeNameElement = querySelector('#badgeName');
      ...
    }

#### Key Information

* Stash the span element in the global variable. Also, stash the input element in a local variable.

Then, add the code to get the names from the JSON file, handling both success and failure.

#### piratebadge.dart
    void main() {
      ...
      
      PirateName.readyThePirates()
        .then((_) {
          //on success
          inputField.disabled = false; //enable
          genButton.disabled = false;  //enable
          setBadgeName(getBadgeNameFromStorage());
        })
        .catchError((arrr) {
          print('Error initializing pirate names: $arrr');
          badgeNameElement.text = 'Arrr! No names.';
        });
    }

#### Key Information

* Call the *readyThePirates()* function, which returns a Future.
* When the Future successfully completes, the *then()* callback function is called.
* Using underscore (_) as a parameter name indicates that the parameter is ignored.
* The callback function enables the UI and gets the stored name.
* If the Future encounters an error the *catchError* callback function is called and the program displays an error message, leaving the UI disabled.
* The callback functions for *then()* and *catchError* are defined inline.

### Run the app.

Save your files with **File > Save All**.
Use the Run button in Dart Editor to run the app.
If you want to see what happens when the app can’t find the *.json* file, change the file name in the code and run the program again.
Compare your app to the final version running below.

[Image]

#### Problems?

Check your code against the files in *6-piratebadge_json*.

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/6-piratebadge_json/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/6-piratebadge_json/piratebadge.dart)

### Share your pirate name.
Congratulations! You finished the pirate badge code lab.

Share your pirate name with the world.

[Tweet button]
[Google+ button]

