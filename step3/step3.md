Step 3: Add a button
-----

In this step, you add a button to the app. The button is enabled when the text field contains no text. When the user clicks the button, the app puts the name *Anne Bonney* on the badge.

### Edit piratebadge.html.

Add the <button> tag below the input field.

#### piratebadge.html
    ...
    <div class="widgets">
      <div>
        <input type="text" id="inputName" maxlength="15">
      </div>
      <div>
        <button id="generateButton">Aye! Gimme a name!</button>
      </div>
    </div>
    ...

#### Key Information

* The button has the ID *generateButton* so the Dart code can get the element.

### Edit piragebadge.dart.

Below the import, declare a top-level variable to hold the ButtonElement.

#### piratebadge.dart

    import 'dart:html';
    ButtonElement genButton;

#### Key Information

* ButtonElement is one of many different kinds of DOM elements provided by the dart:html library.

Wire up the button with an event handler.

#### piratebadge.dart

    void main() {
      querySelector('#inputName').onInput.listen(updateBadge);
      genButton = querySelector('#generateButton');
      genButton.onClick.listen(generateBadge);
    }

#### Key Information

* onClick registers a mouse click handler.

Add a top-level function that changes the name on the badge.

#### piratebadge.dart
    ...
    void setBadgeName(String newName) {
      querySelector('#badgeName').text = newName;
    } 

#### Key Information

* The function updates the HTML page with a new name.

Implement the click handler for the button.

#### piratebadge.dart
    ...
    void generateBadge(Event e) {
      setBadgeName('Anne Bonney');
    }

#### Key Information
* This function sets the badge name to *Anne Bonney*.

Modify *updateBadge()* to call *setBadgeName()*.

#### piratebadge.dart
    void updateBadge(Event e) {
      String inputName = (e.target as InputElement).value;
      setBadgeName(inputName);
    }

* Assign the input field’s value to a local string.

Add a skeleton if-else statement to *updateBadge()*.

#### piratebadge.dart
    void updateBadge(Event e) {
      String inputName = (e.target as InputElement).value;
      setBadgeName(inputName);
      if (inputName.trim().isEmpty) {
        // To do: add some code here.
      } else {
        // To do: add some code here.
      }
    }

#### Key Information
* The *String* class has useful functions and properties for working with string data, such as *trim()* and *isEmpty*.
* String comes from the *dart:core* library, which is automatically imported into every Dart program.
* Dart has common programming language constructs like *if-else*.

Now fill in the if-else statement to modify the button as needed.

#### piratebadge.dart
    void updateBadge(Event e) {
      String inputName = (e.target as InputElement).value;
      setBadgeName(inputName);
      if (inputName.trim().isEmpty) {
        genButton..disabled = false
                 ..text = 'Aye! Gimme a name!';
      } else {
        genButton..disabled = true
                 ..text = 'Arrr! Write yer name!';
      }
    }

#### Key Information
* The cascade operator (..) allows you to perform multiple operations on the members of a single object.
* The *updateBadge()* code uses the cascade operator to set two properties on the button element. The result is the same as this more verbose code:

    genButton.disabled = false;
    genButton.text = 'Aye! Gimme a name!';

### Run the app.

Save your files with **File > Save All**.
Use the Run button in Dart Editor to run the app.
Compare your app to the one running below.
Type in the input field. Remove the text from the input field. Click the button.

[Image]

#### Problems?
Check your code against the files in *3-buttonbadge*.

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/3-buttonbadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/3-buttonbadge/piratebadge.dart)
