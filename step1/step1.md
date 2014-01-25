Step 1: スケルトンアプリを実行しよう
------

このステップではソースファイルを開き、Dart や HTML のコードに慣れていくことにしましょう。そしてアプリを実行してみましょう。

### 1-blankbadge ディレクトリを広げてみよう
ダートエディタでディレクトリ名の左にある小さな右三角ボタンをクリックして *1-blankbadge* ディレクトリを開いてください。ディレクトリには *piratebadge.html* と *piratebadge.dart* の2つのファイルが入っています。

### ファイルを開いてみよう
ダートエディタで *piratebadge.html* と *piratebadge.dart* を両方ともダブルクリックして開いてみましよう。

### コードに目を通そう
アプリのスケルトン（骨組み）をつくるために HTML と Dart のコードに体を馴染ませていきましょう。

#### piratebadge.html
    <html>
      <head>
        <meta charset="utf-8">
        <title>Pirate badge</title>
        <link rel="stylesheet" href="../piratebadge.css">
      </head>
      <body>
        <h1>Pirate badge</h1>
        
        <div class="widgets">
          TO DO: Put the UI widgets here.
        </div>
        <div class="badge">
          <div class="greeting">
            Arrr! Me name is
          </div>
          <div class="name">
            <span id="badgeName"> </span>
          </div>
        </div>
    
        <script type="application/dart" src="piratebadge.dart"></script>
        <script src="packages/browser/dart.js"></script>
      </body>
    </html>

#### キーインフォメーション

* このコードラボを通して *piratebadge.html* ファイルに加える変更は \<div class="*widgets*"\> \</div\> タグの間だけです。
* 後のステップでは \<span id="*badgeName*"\> \</span\> タグの中身がフォーム入力の内容に応じて Dart コードを使ったプログラムで更新されるようになります。
* 最初に出てくる \<script\> タグにはこのアプリの実装のメインとなるファイルが指定されています。それが *piratebadge.dart* ファイルです。
* Dart 仮想マシン (Dart VM) は Dart のコードをネイティブに実行します。Dart VM は Dartium という特別にビルドされた Chromium ブラウザに組み込まれており、このブラウザでは Dart アプリがネイティブに動作します。
* *packages/browser/dart.js* スクリプトはブラウザが Dart をネイティブサポートしているかチェックし、されていれば Dart VM を起動し、されていなければコンパイル済みの JavaScript を代わりにロードします。

#### piratebadge.dart

    void main() {
      // Your app starts here.
    }

* このファイルはアプリのエントリポイントとなる *main()* 関数が含まれています。*piratebadge.html* ファイルの \<script\> タグはこのmain関数を呼び出すことでアプリをスタートさせます。
* *main()* 関数はトップレベル関数です。
* トップレベル変数、トップレベル関数とはクラス定義の外側に宣言されるものです。

### アプリを実行しよう

ダートエディタからアプリを実行するには *piratebadge.html* を選択して実行ボタンをクリックします。

[Image]

ダートエディタは *Dartium* という Dart 仮想マシンが組み込まれた特別なビルドの Chromium を起動し、*piratebadge.html* ファイルをロードします。*piratebadge.html* ファイルはアプリをロードし main() 関数を呼び出します。

[Image]

きっと左手に TO DO コメントと、右手に赤と白のネームバッジが見えていることでしょう。
