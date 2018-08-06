# 技術書典にむけてgit-bookのビルド環境を整える CircleCIとSlackで迎える楽しい(?) 執筆生活

## はじめに

技術書典5の開催が決まりましたね! プロの皆さまはすでに6割下記終わってるのではないでしょうか、私は0割です。 進捗だめです。
こういうときこそ偉人に見習って急がばまわれ本編を書かずに技術書のCI環境を充実させようと思います。

今回はマスターにマージされたGitbookのリポジトリをビルドしてビルドされたPDFをslackに統合するようにしました。


## 今回使うもの
* slackcat
    * slackに対してCUIからファイルの送信をするために使います
* gitbook
    * マークダウンからPDFなど各種フォーマットに出力するためにしよう

## slackmeの設定
まずCircleCIに設定する前にslcakのアクセストークンを得る必要とアプリケーションをSlackのワークスペースにインストールする必要があります。
今回は以上の前準備をローカルのmacで行います
### インストール
githubにslackcatのインストール方法が書いてあります。 もしbrewがインストール済みなら下のコマンドで可能です。
https://github.com/bcicen/slackcat

```bash
$ brew install slackcat
```

その後設定を行います。 設定は以下のコマンドを実行します
```bash
$ slackcat --configure
```

実行するとブラウザが立ち上がってインストールの許可を求められるので対処のワークスペースを選択して Authorizeを押します。
問題がなければトークンが表示されるのでメモします

これで前準備は終わりです。

## CircleCIの設定yaml
CircleCIの設定をしていきましょう。

まずslackのトークンをCircleCIに登録してきましょう。
CircleCIのプロジェクト設定を開いて ` Environment Variables ` を開きます。
開いたら右上にある ` Add Variable` をクリックします、
するとモーダルが表示されるのでNameに `slack_token` Valueには先程のトークンを入力しておきます。  ここにある値はYamlふぁいるで `${Name}`の形で呼び出せます。


以下が今回使用した設定Yamlです
```yml
version: 2
jobs:
  build:
    docker:
      - image: circleci/node:8
    steps:
      - checkout
      - run:
          name: npm install
          command: npm install
      - run:
          name: run textlint
          command: npm run lint
  deploy:
    docker:
      - image: node:6.10.0
    steps:
      - checkout
      - run: curl -Lo slackcat https://github.com/bcicen/slackcat/releases/download/v1.4/slackcat-1.4-$(uname -s)-amd64 && mv slackcat /usr/local/bin/ &&  chmod +x /usr/local/bin/slackcat
      - run: echo ${slack_token} > ~/.slackcat
      - run: apt-get update -y && apt-get install -y calibre
      - run: npm install
      - run: npm install -g gitbook-cli
      - run: gitbook pdf
      - run: slackcat --channel [投げるSlackのチャンネル名] ./book.pdf

workflows:
  version: 2
  build_and_deploy:
    jobs:
      - build
      - deploy:
          requires:
            - build
```

最初の下の部分はslackcatの設定ですね。Githubから落として実行可能状態にしています。また先程CercleCIに登録したSlackとトークンの情報を~/.slackcatに書き込んでいます。


``` yaml
    - run: curl -Lo slackcat https://github.com/bcicen/slackcat/releases/download/v1.4/slackcat-1.4-$(uname -s)-amd64 && mv slackcat /usr/local/bin/ &&  chmod +x /usr/local/bin/slackcat
    - run: echo ${slack_token} > ~/.slackcat
```

以下の部分はgitbookをインストールしてPDFにビルドしています。
``` yaml
    - run: apt-get update -y && apt-get install -y calibre
    - run: npm install
    - run: npm install -g gitbook-cli
    - run: gitbook pdf
```
下の最後でslackcatにビルドしたPDFを送信しています
```yaml
- run: slackcat --channel [投げるSlackのチャンネル名] ./book.pdf
```


## 得られたもの

## 最後に
ｼﾝﾁｮｸ… ｼﾝﾁｮｸｶﾞﾎｼｲ…

