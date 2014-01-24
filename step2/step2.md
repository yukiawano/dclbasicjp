Step 2: Add an input field
-----

> **Note**: Throughout this code lab, continue to edit the files in *1-blankbadge*. You can use the files in the other directories to compare to your code or to recover if you get off track.

In this step, you add an input field to the app. As the user types into the text field, the Dart code updates the badge from the value of the text field.

### Edit piratebadge.html.

Add the <input> tag to the HTML code within the *widgets* <div>.

#### piratebadge.html

    ...
    <div class="widgets">
      <div>
        <input type="text" id="inputName" maxlength="15">
      </div>
    </div>
    ...

#### Key Information

* The ID for the input element is *inputName*. Dart uses CSS selectors, such as *#inputName*, to get elements from the DOM.

### Edit piratebadge.dart.

Import the *dart:html* library at the top of the file (below the copyright).

#### piratebadge.dart
    import 'dart:html';

* This imports *all* classes and other resources from dart:html.
* Don’t worry about bloated code. The build process performs tree-shaking to help minimize code.
* The dart:html library contains the classes for all DOM element types, in addition to functions for accessing the DOM.
* Later you’ll use import with the *show* keyword, which imports only the specified classes.
* Dart Editor helpfully warns you that the import is unused. Don’t worry about it. You’ll fix it in the next step.

Register a function to handle input events on the input field.

#### piratebadge.dart
    void main() {
      querySelector('#inputName').onInput.listen(updateBadge);
    }

* The *querySelector()* function, defined in dart:html, gets the specified element from the DOM. Here, the code uses the selector *#inputName* to specify the input field.
* The object returned from *querySelector() is the DOM element object.
* onInput registers an event handler for input events.
* An input event occurs when the user presses a key.
* You can use either single or double quotes to create a string.
* Dart Editor warns you that the function doesn't exist. Let’s fix that now.

Implement the event handler as a top-level function.

#### piratebadge.dart
    ...
    void updateBadge(Event e) { 
      querySelector('#badgeName').text = e.target.value;
    }

* This function sets the text of the *badgeName* element from the value of the input field.
* *Event e* is the argument to the updateBadge function. The argument’s name is *e*; its type is *Event*.
* You can tell that *updateBadge()* is an event handler because its parameter is an *Event* object.
* The element that generated the event, the input field, is *e.target*.
* Note the warning symbol next to this line of code in Dart Editor. *e.target* is typed as an *EventTarget* which does not have a *value* property.

Fix the warning message.

#### piratebadge.dart
    ...
    void updateBadge(Event e) { 
      querySelector('#badgeName').text = (e.target as InputElement).value;
    }

* In this example, *e.target* is the input element that generated the event.
* The *as* keyword typecasts *e.target* to an *InputElement* to silence warnings from Dart Editor.

### Run the app

Save your files with **File > Save All**.
Use the Run button in Dart Editor to run the app.
Compare your app to the one running below.
Type in the input field.

[Image]

#### Problems?

Check your code against the files in *2-inputbadge*.

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/2-inputnamebadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/2-inputnamebadge/piratebadge.dart)

