Step 7: アプリをビルドし JavaScript として動かそう
------

このステップでは *pub build* を使ってアプリのアセットを生成しそれらを *build* という新しいディレクトリに設置します。それらのタスクに加え、ビルドプロセスは近代的などんなブラウザでも実行できる（しかも圧縮されて軽い） JavaScript ファイルを生成します。

*one-hour-codelab* にはいくつかのディレクトリが含まれていたことを思い出してください。それぞれのステップにつきひとつづつ、それらすべてが one-hour-codelab アプリの一部です。ビルドプロセスはそれぞれのディレクトリごとにアセットをビルドします。いずれのディレクトリも個々にデプロイ可能です。

### pubspec.yaml をよく見てみよう

pubspec.yaml ファイルをダブルクリックしファイルを開きます。編集ペインの下部にある Source タブをクリックします。

```yaml
name: avast_ye_pirates
description: Write a Dart web app code lab
dependencies:
  browser: any
```

#### キーインフォメーション

* *pubspec.yaml* ファイルがあることで、そのディレクトリとコンテンツはアプリケーションであると認識されます。
* *pubspec.yaml* がアプリのメタデータを提供します。たとえばアプリ名など。
* *pubspec.yaml* はアプリが依存するライブラリをリストアップもしています。 このアプリで必要な *browser* ライブラリは、その他多くのライブラリと共に [pub.dartlang.org](https://pub.dartlang.org/) にホスティングされています。
* *any* はお使いの SDK にマッチする最新のライブラリを選択します。

### packages ディレクトリを見てみよう

ダートエディタで *packages* ディレクトリを展開してみてください。

![packagesfiles](packagesfiles.png?raw=true)

#### キーインフォメーション

* *packages* ディレクトリには *pubspec.yaml* ファイルにリストアップされた依存関係のコードがすべて格納されています。これらはダートエディタによって自動的にインストールされます。
* *browser* パッケージにはブラウザが Dart をネイティブサポートしているかどうかチェックする *dart.js* スクリプトが含まれています。
* アプリをエラーなくデプロイするためにはビルド後のアプリケーションに packages が含まれていなければなりません。

### pub build を実行しよう

*pubspec.yaml* を選択し *Tools > Pub Build* と選択していくと *one-hour-codelab* ディレクトリの下にすべてがビルドされます。ビルドログの出力はこんな感じになるでしょう。

    --- Jan 21, 2014 12:41:48 PM Running pub build ... ---
    Building avast_ye_pirates.....
    [Info from Dart2JS]:
    Took 0:00:01.704695 to compile avast_ye_pirates|web/1-blankbadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:05.535304 to compile avast_ye_pirates|web/2-inputnamebadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:02.974628 to compile avast_ye_pirates|web/3-buttonbadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:02.195714 to compile avast_ye_pirates|web/4-classbadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:01.938502 to compile avast_ye_pirates|web/5-localbadge/piratebadge.dart.
    [Info from Dart2JS]:
    Took 0:00:02.028974 to compile avast_ye_pirates|web/6-piratebadge/piratebadge.dart.
    Built 45 files!

#### キーインフォメーション

* *pub build* コマンドは *build* ディレクトリを作成し、中には各ステップごとのサブディレクトリが入っています。
* *build* ディレクトリにはこれまでの6つのステップのプロジェクトをデプロイするのに必要なものがすべて含まれています。

### *build* ディレクトリを見てみよう

*build* ディレクトリを開いてみてください。CodeLab のそれぞれのステップのサブディレクトリが入っているのが見て取れるでしょう。*6-piratebadge* ディレクトリを開いて下さい。

![builddir](builddir.png?raw=true)

* Files for deployment: 配置するべきファイル

#### キーインフォメーション

* *piratebadge.dart.js* が圧縮されて最適化された JavaScript ファイルです。デプロイ後はこのファイルがブラウザで実行されます。
* *packages* ディレクトリにパッケージの依存ファイルが含まれています。
* *piratebadge.dart* ファイルは含まれていないことに注目してください。このファイルはアプリをデプロイするのに必要ないのです。
* *build* ディレクトリのどのサブディレクトリにも個々のアプリがそれぞれ別々にデプロイ出来るように必要なファイルが含まれています。

### アプリを JavaScript として実行しよう

Firefox や Safari といったブラウザで *File > Open File…* から *one-hour-codelab/build/6-piratebadge/piratebadge.html* と選択してアプリを開きます。

#### キーインフォメーション

* アプリはローカルマシンでは *file* プロトコルで動作します。他の人にも見てもらうにはアプリをホスティングサービスにデプロイする必要があります。

[前のステップへ](../step6/step6.md) | [次のステップへ](../step8/step8.md)
