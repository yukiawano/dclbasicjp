Step 5: ローカルストレージに保存しよう
-----

このステップでは、違う名前を入力するごとに海賊バッジをローカルストレージに保存してアプリに永続性を持たせましょう。アプリを再起動すると保存した名前を使ってバッジが作り直されます。

### piratebadge.dart を編集しよう

*dart:convert* ライブラリから JSON コンバータをインポートします。

#### piratebadge.dart
    import 'dart:html';
    import 'dart:math' show Random;
    import 'dart:convert' show JSON;

#### キーインフォメーション

* *JSON* ライブラリは JSON の一般的なユースケースにとても便利な機能を提供します。

PirateName クラスに名前付きコンストラクタを追加しましょう。

#### piratebadge.dart
    class PirateName {
      ...
      PirateName.fromJSON(String jsonString) {
        Map storedName = JSON.decode(jsonString);
        _firstName = storedName['f'];
        _appellation = storedName['a'];
      }
    }

#### キーインフォメーション

* このコンストラクタは JSON エンコードされた文字列から新しい PirateName インスタンスを生成します。
* *PirateName.fromJson* が名前付きコンストラクタです。
* *JSON.decode()* は JSON 文字列を解析して Dart オブジェクトを生成します。
* 海賊名は *Map* オブジェクトにデコードされます。

PirateName クラスに海賊名を JSON 文字列にエンコードするゲッターメソッドを追加しましょう。

#### piratebadge.dart
    class PirateName {
      ...
      String get jsonString => '{ "f": "$_firstName", "a": "$_appellation" } ';
    }

#### キーインフォメーション

* ゲッターはマップフォーマットを使って JSON 文字列をフォーマットします。

String 型の変数 TREASURE_KEY をトップレベルに宣言しましょう。

#### piratebadge.dart
    final String TREASURE_KEY = 'pirateName';
    
    void main() {
      ...
    }

#### キーインフォメーション

* これからキー・値のペアをローカルストレージに保存します。この文字列がそのキーになります。値は海賊名です。

バッジの名前が変更されたときに海賊名を保存しましょう。

#### piratebadge.dart
    void setBadgeName(PirateName newName) {
      if (newName == null) {
        return;
      }
      querySelector('#badgeName').text = newName.pirateName;
      window.localStorage[TREASURE_KEY] = newName.jsonString;
    }

#### キーインフォメーション

* ローカルストレージはブラウザの *Window* オブジェクトから提供されます。

トップレベル関数 *getBadgeNameFromStorage()* を追加しましょう。

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

#### キーインフォメーション

* この関数はローカルストレージから海賊名を取得し PirateName オブジェクトを生成して返します。

main() 関数からこの関数を呼んでください。

#### piratebadge.dart
    void main() {
      ...
      setBadgeName(getBadgeNameFromStorage());
    }

#### キーインフォメーション

* ローカルストレージのバッジ名を初期値として使います。

### アプリを実行してみよう

ファイルを **File > Save All** で保存します。
ダートエディタの Rub ボタンでアプリを実行します。
下で動いているものと自分のアプリをくらべてみましょう。
ボタンをクリックしてバッジに名前を表示してみたりブラウザのウィンドウをもう一つ開いてこのアプリを再度起動してみたりしましょう。

![Step5Complete](step5_completed.png?raw=true)

* [実行可能な形式](https://www.dartlang.org/codelabs/darrrt/#i-classfa-fa-anchor-i-run-the-app-4)

#### 困り事が？
自分のコードを *5-localbadge* と比べてみましょう。

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/5-localbadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/5-localbadge/piratebadge.dart)

[前のステップへ](../step4/step4.md) | [次のステップへ](../step6/step6.md)
