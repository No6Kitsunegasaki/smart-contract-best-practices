# スマートコントラクトセキュリティベストプラクティス

 **訳注:本ドキュメントは https://github.com/ConsenSys/smart-contract-best-practices の日本語訳です。本家より遅れていることがあるので、必ず元のドキュメントも並べて参照してください。**

ドキュメントサイト: https://consensys.github.io/smart-contract-best-practices/

中国語版ドキュメントサイト: https://github.com/ConsenSys/smart-contract-best-practices/blob/master/README-zh.md

## コントリビューションは大歓迎！
<!-- 
<<<<<<< HEAD
小さな修正から新規セクションの追加まで、どんなプルリクエストも遠慮なくどうぞ。もし新規のコントラクトを作成するときは、スタイルのガイダンスである[コントリビューティング](https://consensys.github.io/smart-contract-best-practices/about/contributing)ページを参照してください。
======= -->
小さな修正から新規セクションの追加まで、どんなプルリクエストも遠慮なくどうぞ。もし新規のコントラクトを作成するときは、スタイルのガイダンスである[コントリビューティング](./docs/about/contributing.md)ページを参照してください。
<!-- >>>>>>> 7a827c960b9f279cd698d66f63244b83b783ef9a -->

[issues](https://github.com/ConsenSys/smart-contract-best-practices/issues)にはこれから対応しなくてはならないものやアップデートのトピックがありますのでご覧ください。もし討議したいアイデアがあれば、[Gitter](https://gitter.im/ConsenSys/smart-contract-best-practices)の方で私たちとチャットしましょう。

もしあなたが記事やブログを書かれているのならば、[bibliography](./bibliography)にそれを追加してください。


## ドキュメンテーションサイトの構築

```
$ git clone git@github.com:ConsenSys/smart-contract-best-practices.git
$ cd smart-contract-best-practices
$ pip install -r requirements.txt
$ mkdocs build 
```

`mkdocs serve`コマンドを使うとlocalhostでサイトが見れるようになり、変更を保存するたびにライブリロードされるようになるでしょう。

## ドキュメンテーションサイトの再デプロイ

```
mkdocs gh-deploy
```

