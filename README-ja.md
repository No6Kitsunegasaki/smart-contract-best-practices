# スマートコントラクトセキュリティベストプラクティス

 **訳注:本ドキュメントは https://github.com/ConsenSys/smart-contract-best-practices の日本語訳です。本家より遅れていることがあるので、必ず元のドキュメントも並べて参照してください。**

ドキュメントサイト: https://consensys.github.io/smart-contract-best-practices/

中国語版ドキュメントサイト: https://github.com/ConsenSys/smart-contract-best-practices/blob/master/README-zh.md

## Contributions are welcome!
<!-- 
<<<<<<< HEAD
Feel free to submit a pull request, with anything from small fixes, to full new sections. If you are writing new content, please reference the [contributing](https://consensys.github.io/smart-contract-best-practices/about/contributing) page for guidance on style. 
======= -->
Feel free to submit a pull request, with anything from small fixes, to full new sections. If you are writing new content, please reference the [contributing](./docs/about/contributing.md) page for guidance on style. 
<!-- >>>>>>> 7a827c960b9f279cd698d66f63244b83b783ef9a -->

See the [issues](https://github.com/ConsenSys/smart-contract-best-practices/issues) for topics that need to be covered or updated. If you have an idea you'd like to discuss, please chat with us in [Gitter](https://gitter.im/ConsenSys/smart-contract-best-practices).

If you've written an article or blog post, please add it to the [bibliography](./bibliography).  


## Building the documentation site

```
$ git clone git@github.com:ConsenSys/smart-contract-best-practices.git
$ cd smart-contract-best-practices
$ pip install -r requirements.txt
$ mkdocs build 
```

You can also use the `mkdocs serve` command to view the site on localhost, and live reload whenever you save changes.

## Redeploying the documentation site

```
mkdocs gh-deploy
```

