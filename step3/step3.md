Step 3: ボタンの追加
-----

このステップでは，アプリケーションにボタンを追加します．ボタンはテキストフィールドに文字が含まれていない時に有効化されます．ユーザーがボタンをクリックすると，アプリケーションはバッジに*Anne Bonney*の名前を表示します．

### piratebadge.htmlの編集

<button>タグを入力フィールドの下に追加します．

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

* 訳註: Aye! Gimme a name! (名前をください!)

#### キーインフォメーション

* Dartのコードが要素にアクセスすることができるようにボタンは*generateButton*IDを持っています．

### piragebadge.dartの編集

import文の下で，ButtonElement(ボタン要素)を持つためのトップレベル変数を宣言します．

#### piratebadge.dart

    import 'dart:html';
    ButtonElement genButton;

#### キーインフォメーション

* ButtonElementはdart:htmlライブラリが提供する数多くの種類のDOM要素の中の一つです．

ボタンにイベントハンドラを設定します．

#### piratebadge.dart

    void main() {
      querySelector('#inputName').onInput.listen(updateBadge);
      genButton = querySelector('#generateButton');
      genButton.onClick.listen(generateBadge);
    }

#### キーインフォメーション

* onClickはマウスクリックハンドラを登録します．

バッジの名前を変更するトップレベル関数を追加します．

#### piratebadge.dart
    ...
    void setBadgeName(String newName) {
      querySelector('#badgeName').text = newName;
    } 

#### キーインフォメーション

* この関数は新しい名前でHTMLページを更新します．

ボタンのクリックハンドラを実装します．

#### piratebadge.dart
    ...
    void generateBadge(Event e) {
      setBadgeName('Anne Bonney');
    }

#### キーインフォメーション

* この関数はバッジの名前を*Anne Bonney*に設定します．

*updateBadge()*を*setBadgeName()*を呼び出すように変更します．

#### piratebadge.dart
    void updateBadge(Event e) {
      String inputName = (e.target as InputElement).value;
      setBadgeName(inputName);
    }

#### キーインフォメーション

* 入力フィールドの値をローカル変数(文字列)に割り当てます．

*updateBadge()*にif-else文のひな形を追加します．

#### piratebadge.dart
    void updateBadge(Event e) {
      String inputName = (e.target as InputElement).value;
      setBadgeName(inputName);
      if (inputName.trim().isEmpty) {
        // やること: ここにコードを追加
      } else {
        // やること: ここにコードを追加
      }
    }

#### キーインフォメーション

* *String*クラスは*trim()*や*isEmpty*など文字列データを取り扱うのに便利な関数やプロパティを持っています．
* Stringは*dart:core*ライブラリに含まれます．*dart:core*ライブラリはすべてのDartプログラムで自動的にインポートされます．
* Dartは*if-else*のような一般的なプログラミングの言語概念を持っています．

必要に応じてボタンを変更するif-else文の残りを完成させます．

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

#### キーインフォメーション

* カスケードオペレーター(*..*)によって，単一のオブジェクトのメンバーに対して複数の操作を行うことができます．
* *updateBadge()*コードはボタン要素の2つのプロパティを設定するのにカスケードオペレーターを利用しています．これは下の冗長なコードと同じ実行結果をもたらします．

    genButton.disabled = false;
    genButton.text = 'Aye! Gimme a name!';

### アプリを実行しよう!

Save your files with **File > Save All**.
Use the Run button in Dart Editor to run the app.
Compare your app to the one running below.
Type in the input field. Remove the text from the input field. Click the button.

**File > Save All**からファイルを保存してください．
Dartエディタの実行ボタン(Run Button)を利用してアプリケーションを実行しましょう！
自分のアプリケーションを下の実行中の画像と比較してください．
入力フィr−づおに値を入力して，その後入力フィールドのテキストを削除してください．そして，ボタンをクリックしてください．

[Image]

#### 問題がおきましたか?

*3-buttonbadge*のコードと確認をしてください．

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/3-buttonbadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/3-buttonbadge/piratebadge.dart)
