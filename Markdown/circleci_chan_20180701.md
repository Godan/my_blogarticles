# CIでも可愛い子に叱られたい ~Google Apps Scriptを添えて~

本来はカノジョできないエンジニアアドベントカレンダーとかに上げるようなノリの記事をこの時期に書いてしまった…  
最近ちょいちょいと個人的な日曜プロジェクトでCircleCIを導入しているのですが、標準のSlackBOTでは味気がなくただただビルドが失敗したという事実しか通知してくれません。  

これは由々しき事態です。  
また、Slack以外のChatworkなどの公式対応がないツールや別ツールと連携できるようにWebhookの仕組みとGoogleAppsScript(以下GAS)を使って通知をできるようにします。

## SlackのAPI トークンを取得する
まずはSlack APIのページにアクセスして```start build```を押します。  
[https://api.slack.com/](https://api.slack.com/)  
サービス名とインストール先を入力します。  
```Add features and functionality > OAuth & Permissions > Scopes```でサービスに対して権限を付与します。  
今回はチャンネルにポストするための権限を付与します。  
saveしたら```Install App to Workspace``` を押して対象ワークスペースにアプリケーションを適用します。  
インストール後にはOAuth Access Tokenが発行されます。このアクセストークンはSlackにポストする際に使用します。

# とりあえずソースコード

GASでは公開ウェブアプリケーションとして公開すると ```doPost()``` でPOSTメゾットを扱うことができます。  
今回はSlackにPostするにあたって [Qiita | Slack BotをGASでいい感じで書くためのライブラリを作った
](https://qiita.com/soundTricker/items/43267609a870fc9c7453)をお借りしました。



```js
function doPost(e) {
  var json = JSON.parse(e.postData.getDataAsString());
  var msg = ""
  var icon = null
  msg += "circleCIが起動したよ！\n"
  
  if(json.payload.status == "success"){
    msg += ":success_circleci: テストは成功したみたいだよ！ \n"
  }else{
    msg += ":failed_circleci: テスト失敗しちゃった… \n"
  }
  msg += "ブランチ名:" + json.payload.branch + "\n" + json.payload.build_url
  postSlackMessage(msg)
}

// メッセージを投げる
function postSlackMessage(msg) {
  var token = ’Slack Tokenをここにはる’;
  var slackApp = SlackApp.create(token); //SlackApp インスタンスの取得
  var options = {
    channelId: "#hoge", //チャンネル名
    userName: "ユニティちゃん", //投稿するbotの名前
    message: msg //投稿するメッセージ
  };
 
  Logger.log(slackApp.postMessage(options.channelId, options.message, {username: options.userName, icon_url: options.icon_url}));
}


```

## CircleCIのWebhookを追加する
まずはテストが回ったあとにPOSTする先を取得します。  
Googleの上部メニューバーの公開>ウェブアプリケーションとして公開を押します。  
そうするとモーダルウィンドウでURLとアプリケーションにアクセスできるユーザー、アプリケーション実行するユーザーなどが設定できます。  
今回はアプリケーションにアクセスできるユーザーは全員にします。  
更新を押すとURLが生成されるので控えておきます。

URLを控えたら対象とするプロジェクトの```.circleci/config.yml```を開きます。  
Yamlの中に以下の文を書きます。  
```yml
notify:
  webhooks:
    # A list of hook hashes, containing the URL field
    - url: 生成されたGASURL
```