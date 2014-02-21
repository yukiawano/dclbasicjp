Step 3: ボタンの追加
-----

このステップでは，アプリケーションにボタンを追加します．ボタンはテキストフィールドに文字が含まれていない時に有効化されます．ユーザーがボタンをクリックすると，アプリケーションはバッジに*Anne Bonney*の名前を表示します．

### piratebadge.htmlの編集

\<button\>タグを入力フィールドの下に追加します．

#### piratebadge.html

```html
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
```

* 訳註: Aye! Gimme a name! (名前をください!)

#### キーインフォメーション

* Dartのコードが要素にアクセスすることができるようにボタンは *generateButton* id属性を持っています．

### piragebadge.dartの編集

import文の下で，ButtonElement(ボタン要素)を持つためのトップレベル変数を宣言します．

#### piratebadge.dart

```dart
import 'dart:html';
ButtonElement genButton;
```

#### キーインフォメーション

* ButtonElementはdart:htmlライブラリが提供する数多くの種類のDOM要素の中の一つです．

ボタンにイベントハンドラを設定します．

#### piratebadge.dart

```dart
void main() {
  querySelector('#inputName').onInput.listen(updateBadge);
  genButton = querySelector('#generateButton');
  genButton.onClick.listen(generateBadge);
}
```

#### キーインフォメーション

* onClickはマウスクリックハンドラを登録します．

バッジの名前を変更するトップレベル関数を追加します．

#### piratebadge.dart

```dart
void setBadgeName(String newName) {
  querySelector('#badgeName').text = newName;
} 
```

#### キーインフォメーション

* この関数は新しい名前でHTMLページを更新します．

ボタンのクリックハンドラを実装します．

#### piratebadge.dart

```dart
...
void generateBadge(Event e) {
  setBadgeName('Anne Bonney');
}
```

#### キーインフォメーション

* この関数はバッジの名前を*Anne Bonney*に設定します．

*updateBadge()*を*setBadgeName()*を呼び出すように変更します．

#### piratebadge.dart

```dart
void updateBadge(Event e) {
  String inputName = (e.target as InputElement).value;
  setBadgeName(inputName);
}
```

#### キーインフォメーション

* 入力フィールドの値をローカル変数(文字列)に割り当てます．

*updateBadge()*にif-else文の骨組みを追加します．

#### piratebadge.dart

```dart
void updateBadge(Event e) {
  String inputName = (e.target as InputElement).value;
  setBadgeName(inputName);
  if (inputName.trim().isEmpty) {
    // TODO: ここにコードを追加
  } else {
    // TODO: ここにコードを追加
  }
}
```

#### キーインフォメーション

* *String*クラスは*trim()*や*isEmpty*など文字列データを取り扱うのに便利な関数やプロパティを持っています．
* Stringは*dart:core*ライブラリに含まれます．*dart:core*ライブラリはすべてのDartプログラムで自動的にインポートされます．
* Dartは*if-else*のような一般的なプログラミングの言語概念を持っています．

必要に応じてボタンを変更するif-else文の残りを完成させます．

#### piratebadge.dart

```dart
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
```

#### キーインフォメーション

* カスケードオペレーター(*..*)によって，単一のオブジェクトのメンバーに対して複数の操作を行うことができます．
* *updateBadge()*コードはボタン要素の2つのプロパティを設定するのにカスケードオペレーターを利用しています．これは下の冗長なコードと同じ実行結果をもたらします．

```dart
genButton.disabled = false;
genButton.text = 'Aye! Gimme a name!';
```

### アプリを実行しよう!

**File > Save All**からファイルを保存してください．
Dartエディタの実行ボタン(Run Button)を利用してアプリケーションを実行しましょう！
自分のアプリケーションを下の実行中の画像と比較してください．
入力フィールドに値を入力して，その後入力フィールドのテキストを削除してください．そして，ボタンをクリックしてください．

![Step3Complete](step3_completed.png?raw=true)

* [実行可能な形式](https://www.dartlang.org/codelabs/darrrt/#i-classfa-fa-anchor-i-run-the-app-2)

#### 問題がおきましたか?

*3-buttonbadge*のコードと確認をしてください．

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/3-buttonbadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/3-buttonbadge/piratebadge.dart)

[前のステップへ](../step2/step2.md) | [次のステップへ](../step4/step4.md)
