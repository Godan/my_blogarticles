# CircleCIで生成物をSlackにポストする
## はじめに

今回CircleCIで技術書を書いてるときにビルドしたPDFをSlackに投げるようにしたのでその時のメモ

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
例としてNodeのイメージを使用しています
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
      - run: slackcat --channel [投げるSlackのチャンネル名] ./[投げたいファイル]

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

最後のいちぶんで 実際にSlackにファイル送信をしています。
```yaml
- run: slackcat --channel [投げるSlackのチャンネル名] ./[投げたいファイル]
```


## 実装結果
