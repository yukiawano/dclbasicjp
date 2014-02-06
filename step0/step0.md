Step 0: Set up
----------

このステップでは Dart をダウンロードし、サンプルコードを取得します。

### Dart を手に入れよう

まだ手に入れてないのなら Dart をダウンロードしましょう。ZIPファイルを解凍すると*dart*という名前のディレクトリが作られます。

[ダウンロードページ](https://www.dartlang.org/tools/download.html)

* Dart tools は最近のバージョンの *Windows (Vista, 7, or 8)*, *Linux*, または *Mac* で動作します．
* 現在の安定版は*Dart: 1.1.1*です．
* 訳註: Dartは常に開発されていて，新しいバージョンが登場しています．バージョンによってはSDKなどの互換性がなくなっており，このTutorialの内容が動かない可能性があります．その場合は，[原文](https://www.dartlang.org/codelabs/darrrt/)を確認していただきますようお願いいたします．また，是非，翻訳のPull Requestを送っていただけますと大変うれしいです:)

### エディタを起動しよう

*dart*ディレクトリに移動し *DartEditor* をダブルクリックします。

*質問がある？トラブった？* それなら [ダートエディタのトラブルシューティングページ](https://www.dartlang.org/tools/editor/troubleshoot.html "Troubleshooting Dart Editor") を参照しましょう。

### サンプルコードを手に入れよう

サンプルコードを[ダウンロード](https://github.com/dart-lang/one-hour-codelab/archive/master.zip)しましょう。ZIPファイルを解凍すると*one-hour-codelab-master*ディレクトリが作られます。

### サンプルの one-hour-codelab-master を開いてみよう

ダートエディタで*File > Open Existing Folder…*の順にクリックし*one-hour-codelab-master*ディレクトリを開いてください。

![DartEditor](filesanddirs.png?raw=true)

* Dependencies and installed libraries: 依存関係とインストールされているライブラリ
* Contains code for each completed steps: それぞれのステップが完了したコードを含んでいます

### キーインフォメーション

* *packages*ディレクトリ、それから*pubspec.yaml*と*pubspec.lock*ファイルはパッケージの依存関係に関連したファイルです。このプロジェクトではすべての依存関係が整っています。ダートエディタが自動的に必要なパッケージをインストールしてくれるのです。
* 先頭に番号の付いたディレクトリにはそれぞれのステップの完全なコードが入っています。*1-blankbadge*にはあなたが最初に取り掛かることになるアプリの骨組みとなるバージョンが含まれています。*6-piratebadge_json*はアプリの最期のバージョンといった具合です。
* *piratebadge.css*ファイルはアプリのすべてのステップに共通する*CSS*スタイルを提供します。このコードラボ中にこのファイルを変更することはありません。
* *Dart SDK*ディレクトリには*Dart*ソフトウェア開発キットによって提供されるすべての関数、変数、そしてクラス群が含まれています。
* *Installed Packages*ディレクトリにはアプリが依存する追加ライブラリのすべての関数、変数、そしてクラス群が含まれています。

[次のステップへ](../step1/step1.md)
