Step 2: 入力欄を追加しよう
-----

> **Note**: このコードラボでは引き続き *1-blankbadge* ファイルを編集していきます。自分のコードと比較するためやどうすべきか分からなくなってしまった時のために他のディレクトリを参照することもできます。

このステップではアプリに入力欄を追加します。テキストフィールドに文字を入力するごとに Dart のコードが入力されたテキストでバッジを更新します。

### piratebadge.html を編集しよう

\<div class="*widgets*"> \</div\> タグ内に \<input\> タグを追加しましょう。

#### piratebadge.html

    ...
    <div class="widgets">
      <div>
        <input type="text" id="inputName" maxlength="15">
      </div>
    </div>
    ...

#### キーインフォメーション

* input タグの id は *inputName* にすること。Dart は DOM から要素を取得する際に *#inputName* といった CSS セレクタを利用するからです。

### piratebadge.dart を編集しよう

ファイルのトップ（著作権表示の下）で *dart:html* ライブラリを import します。

#### piratebadge.dart
    import 'dart:html';

* これは dart:html の *すべての* クラスその他のリソースを import します。
* コードが肥大化するのを恐れないで。ビルドプロセスが tree-shaking (訳注：木を揺すって枝葉を振り落とす) してコードの最小化を助けます。
* dart:html ライブラリは DOM にアクセスする関数群に加え、すべての DOM エレメントタイプのクラス群を含んでいます。
* 後で *show* キーワードを使った import を利用することになりますが、こうすることで特定のクラスのみを import できます。
* ダートエディタは親切なことに使用していない import には警告を出しますが心配しないで。次のステップで修正しますから。

入力欄にイベントを処理する関数を登録します。

#### piratebadge.dart
    void main() {
      querySelector('#inputName').onInput.listen(updateBadge);
    }

* *querySelector()* 関数は dart:html に定義されており、DOM から特定の要素を取り出します。ここでは *#inputName* セレクタを使って input を特定しています。
* *querySelector() 関数から返されるのはDOMエレメントオブジェクトです。
* onInput は入力イベントに対するイベントハンドラを登録します。
* 入力イベントはユーザーがキーを押すと発生します。
* 文字列はシングルクォートでもダブルクォートでも大丈夫です。
* ダートエディタが the function doesn't exist（そんな関数は存在しない）と警告を出すことでしょう。これからそれを修正していきます。

イベントハンドラをトップレベル関数として実装します。

#### piratebadge.dart
    ...
    void updateBadge(Event e) { 
      querySelector('#badgeName').text = e.target.value;
    }

* この関数は入力欄の文字列を *badgeName* 要素のテキストとしてセットします。
* *Event e* とは updateBadge 関数の引数です。仮引数の名前が *e* で、型が Event です。
* パラメータが *Event* オブジェクトであることから *updateBadge()* がイベントハンドラだと言える訳です。
* イベントが発生した要素（ここでは入力欄）を特定しているのが *e.target* の部分です。
* ダートエディタでこの行のすぐ隣りに出ている警告にお気付きでしょうか。*e.target* は *EventTarget* 型であり *value* というプロパティは持たないと書いてあります。

警告が出ないように修正してみましょう。

#### piratebadge.dart
    ...
    void updateBadge(Event e) { 
      querySelector('#badgeName').text = (e.target as InputElement).value;
    }

* この例では *e.target* はイベントを発生させた input 要素です。
* *as* キーワードは *e.target* を *InputElement* に型変換します。これでダートエディタの警告は静かになったでしょう。

### アプリを実行しよう

**File > Save All** と操作しファイルを保存してください。
ダートエディタの Run ボタンを押してアプリを実行してください。
下で動いているものとあなたのアプリを比較してください。
入力欄に何か打ち込んでみてください。

![Step2Complete](step2_completed.png?raw=true)

* [実行可能な形式](https://www.dartlang.org/codelabs/darrrt/#i-classfa-fa-anchor-i-run-the-app-1)

#### 何か問題が？

自分のコードを *2-inputbadge* と比較してみよう。

* [piratebadge.html](https://github.com/dart-lang/one-hour-codelab/blob/master/web/2-inputnamebadge/piratebadge.html)
* [piratebadge.dart](https://github.com/dart-lang/one-hour-codelab/blob/master/web/2-inputnamebadge/piratebadge.dart)

[前のステップへ](../step1/step1.md) | [次のステップへ](../step3/step3.md)
