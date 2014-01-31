Step 6: JSON ファイルから名前を読み込もう
-----

このステップでは JSON ファイルから名前と称号を取得するように PirateName クラスを変更します。こうすることでアプリにもっと多くの名前や称号を追加できます。

### piratenames.json を作成しよう

**File > New File…** と操作して以下の内容で JSON ファイルを作成し *piratenames.json* という名前で保存してください。
このファイルをいま編集している Dart や HTML ファイルと平行して *1-blankbadge* ディレクトリに置いておいてください。

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

#### キーインフォメーション

* このファイルには JSON の連想配列が記述されており、2つのキーにそれぞれ文字列の配列が値として格納されています。（訳注：訳しづらかったのでやや意訳したが JSON の構造を見れば明らかだと思う）

### piratebadge.html を編集しよう

input フィールドとボタンを無効化します。

#### piratebadge.html
    ...
      <div>
        <input type="text" id="inputName" maxlength="15" disabled>
      </div>
      <div>
        <button id="generateButton" disabled>Aye! Gimme a name!</button>
      </div>
    ...

#### キーインフォメーション

* JSON ファイルから海賊名を首尾よく取得できたら Dart のコードがテキストフィールドとボタンを有効化します。

### piratebadge.dart を編集しよう

ファイルの先頭に import を追加してください。

#### piratebadge.dart
    import 'dart:html';
    import 'dart:math' show Random;
    import 'dart:convert' show JSON;
    import 'dart:async' show Future;

#### キーインフォメーション

* *dart:async* ライブラリは非同期プログラミング機能を提供します。
* *Future* クラスは将来値を取得するための手法を提供します。(JavaScript開発者へ：Future は Promise と似ています。)

名前と照合の一覧を static な空のリストで置き換えます。

#### piratebadge.dart
    class PirateName {
      ...
      static List<String> names = [];
      static List<String> appellations = [];
      ...
    }

#### キーインフォメーション

* **宣言から *final* キーワードを取り除くのを忘れないで下さい。**
* *[]* リテラルは *new List()* と等価です。
* List 型はどんなオブジェクトでも格納できるリストですが、もし明示的に「文字列しか含めない」と意図した場合は *List<String>* のように宣言できます。（訳注：Javaでいう総称型）

PirateName クラスに static 関数を2つ追加してください。

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

#### キーインフォメーション

* *HttpRequest* は URL からデータを取得するためのユーティリティクラスです。
* *getString()* はシンプルな GET リクエストを送って結果を文字列で返す便利なメソッドです。
* このコードでは非同期な HTTP GET のために *Future* を利用します。
* *.then()* 関数に渡すコールバック関数は Future が首尾よく完了した際に呼び出されます。
* Future が完了すると海賊名が JSON ファイルから読み込まれます。
* *readyThePirates* はファイルが読み込まれた後メインプログラムが何かする際の便宜のために Future を戻します。

トップレベルに変数を追加してください。

#### piratebadge.dart
    SpanElement badgeNameElement;
    
    void main() {
      ...
    }

#### キーインフォメーション

* 何度も利用するのでその都度 DOM を読み込まなくていいように span 要素を変数につっこんでおきましょう。

*main()* 関数に以下の変更を加えてください。

#### piratebadge.dart
    void main() {
      InputElement inputField = querySelector('#inputName');
      inputField.onInput.listen(updateBadge);
      genButton = querySelector('#generateButton');
      genButton.onClick.listen(generateBadge);
      
      badgeNameElement = querySelector('#badgeName');
      ...
    }

#### キーインフォメーション

* span 要素をグローバル変数に、input フィールドをローカル変数に入れておきましょう。

それから、JSON ファイルから名前を取得するコードを追加し、成功パターンと失敗パターンの両方をハンドリングします。

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

#### キーインフォメーション

* *readyThePirates()* 関数を呼び出すと Future オブジェクトが返ってきます。
* Future がエラーなく返ってきたら *then()* コールバック関数が呼ばれます。
* パラメータにアンダースコア (_) を渡しているのはパラメータが無視されることを示唆しています。
* コールバック関数が UI を有効化し、保存された名前を取得します。
* Future が何らかのエラーに遭遇したら *catchError* コールバックが呼ばれ、UI は無効化されたままで画面にエラーメッセージを表示します。
* *then()* や *catchError* といったコールバック関数はインライン定義されます。

### Run the app.

ファイルを **File > Save All** で保存します。
ダートエディタの Rub ボタンでアプリを実行します。
もし *.json* ファイルが見つからなかった場合にどうなるか知りたければファイル名を変更してプログラムをもう一度実行してみましょう。
下で動いている最終版のアプリと自分のアプリを比べてみましょう。

[Image]

#### 困り事が？

自分のコードを *6-piratebadge_json* と比べてみましょう。

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/6-piratebadge_json/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/6-piratebadge_json/piratebadge.dart)

### 海賊名をシェアしよう
おめでとう！海賊バッジCode Labは完了です！

君の海賊名を世界にシェアしよう！

[Tweet button]
[Google+ button]

