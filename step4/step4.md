Step 4: PirateName クラスを作ろう
-----

このステップでは Dart のコートだけを変更します。海賊の名前を表すクラスを作成し、作り終わったらこのクラスのインスタンスはリストから名前と称号をランダムに選び出します。また、オプションとしてコンストラクタに名前と称号を自分で渡すこともできます。

### piratebadge.dart を編集しよう

ファイルのトップに import 文を追加してください。

#### piratebadge.dart

```dart
import 'dart:html';
import 'dart:math' show Random;
```

#### キーインフォメーション

* *show* キーワードでクラス、関数、またはプロパティの中から必要なものだけを import できます。
* *Random* クラスはランダムな数値を生成する機能を提供します。

ファイルの一番下にクラス定義を追加してください。

#### piratebadge.dart

```dart
...
class PirateName {
}
```

#### キーインフォメーション

* クラス定義はクラス名を提供します。

Random オブジェクトをクラスレベルの（訳注：インスタンスごとではないクラスで共通の）オブジェクトとして作成します。

#### piratebadge.dart

```dart
class PirateName {
  static final Random indexGen = new Random();
}
```

#### キーインフォメーション

* *static* キーワードはクラスレベルのフィールドを定義できます。つまり、ランダム数値生成器はこのクラスのすべてのインスタンス間で共用されます。
* ダートエディタは static な変数名をイタリック体で表現します。
* *new* キーワードでコンストラクタ呼び出しを行います。

2つのインスタンス変数を追加します。１つ目は名前を、2つ目は称号を表します。

#### piratebadge.dart

```dart
class PirateName {
  static final Random indexGen = new Random();
  String _firstName;
  String _appellation;
}
```

#### キーインフォメーション

* プライベート変数はアンダースコア(*_*)で始まります。Dart に *private* キーワードはないのです。

名前と称号を提供する2つの小さなリストをクラス内に static に定義します。

#### piratebadge.dart

```dart
class PirateName {
  ...
  static final List names = [
    'Anne', 'Mary', 'Jack', 'Morgan', 'Roger',
    'Bill', 'Ragnar', 'Ed', 'John', 'Jane' ];
  static final List appellations = [
    'Black','Damned', 'Jackal', 'Red', 'Stalwart', 'Axe',
    'Young', 'Old', 'Angry', 'Brave', 'Crazy', 'Noble'];
}
```

#### キーインフォメーション

* *final* で宣言された変数は変更が出来ません。
* リストは言語に組み込みで提供されています。これらのリストはリストリテラル（訳注：\[\]のこと）を使って作られています。
* *List* クラスはリスト操作のAPIを提供します。

クラスにコンストラクタを追加しましょう。

#### piratebadge.dart

```dart
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
```

#### キーインフォメーション

* コンストラクタはクラスと同名です。
* 中括弧 (*{* と *}*) で囲まれた引数はオプショナルな名前付き引数です。
* *nextInt()* 関数はランダム数値生成器から新しいランダムな整数をひとつ取り出します。
* カギ括弧 (*[* and *]*) は配列の添字として使います。
* *length* プロパティはリストの要素数を返します。
* このコードはランダムな数値をリストの添字として使用しているわけです。

海賊の名前のゲッターメソッドを追加しましょう。

#### piratebadge.dart

```dart
class PirateName {
  ...
  String get pirateName =>
    _firstName.isEmpty ? '' : '$_firstName the $_appellation';
}
```

#### キーインフォメーション

* ゲッターとはオブジェクトのプロパティに読み込みアクセスを提供する特別なメソッドです。
* 三項演算子 *?:* は if-then-else 文の簡略表記です。
* 文字列補間 (*'$\_firstName the $\_appellation'*) を使うと他のオブジェクトから文字列を簡単に作成できます。
* ファットアロー ( *=> expr;* ) 構文は *{ return expr; }* の簡略形です。

*setBadgeName()* 関数を String 型の代わりに PirateName 型を受け取るように修正しましょう。

#### piratebadge.dart

```dart
void setBadgeName(PirateName newName) {
  querySelector('#badgeName').text = newName.pirateName;
}
```

#### キーインフォメーション

* このコードは海賊名を String で取得するためにゲッターを呼んでいます。

*updateBadge()* input フィールドの値に応じて海賊名を生成するように修正しましょう。

#### piratebadge.dart

```dart
void updateBadge(Event e) {
  String inputName = (e.target as InputElement).value;
  
  setBadgeName(new PirateName(firstName: inputName));
  ...
}
```

#### キーインフォメーション

* このコンストラクタ呼び出しでは名前付きパラメータを1つ渡しています。

海賊名を *Anne Bonney* 決め打ちにならないように *generateBadge()* を修正してみましょう。

#### piratebadge.dart

```dart
void generateBadge(Event e) {
  setBadgeName(new PirateName());
}
```

* このケースではコンストラクタには何も引数を渡していません。

###  アプリを実行しよう

ファイルを **File > Save All** で保存します。
ダートエディタの Rub ボタンでアプリを実行します。
下で動いているものを自分のアプリをくらべてみましょう。
input フィールドに入力したり、今度は input を空にしてみたりしてボタンを押してみましょう。

![Step4Complete](step4_completed.png?raw=true)

* [実行可能な形式](https://www.dartlang.org/codelabs/darrrt/#i-classfa-fa-anchor-i-run-the-app-3)

#### 困り事が？

自分のコードを *4-classbadge* と比べてみましょう。

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/4-classbadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/4-classbadge/piratebadge.dart)

[前のステップへ](../step3/step3.md) | [次のステップへ](../step5/step5.md)
