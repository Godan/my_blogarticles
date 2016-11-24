
先日参加したABC2016aの懇親会でじゃんけんの死闘の末ChromeCastを頂きました。  
[f:id:gakusei200709:20161124234037p:plain]

…本当に頂いてよかったのだろうか。    
しかし、色々やってる身としては頂いたものはHackして差し上げ投げればならない！（ニンジャスレイヤー風に）
というわけで早速ChromeCastのアプリ開発準備としてサンプルを動かして行きたいと思います。  
日本語情報が少ない＋情報が古いなどもあったので何かの手助けになれば。  
  
セットアップは購入時の指示に従ってください。  
今回はChromeから文字列を書き込みそれをChoromeChastへキャストするHello world的なサンプルアプリを試してみます。  
必要なのは  
  ・ChromeChast本体  
  ・5＄が支払い出来るクレカorデビットカード  
  ・Webサーバー   
です。  


<!-- more -->


## Chast開発者登録
個人的には一番の壁なきがします…


[https://cast.google.com/publish/#/overview:embed:cite]


一番最初にgoogleに対し開発者登録として5$を支払います。クレジットの利用項目を見ると572円でした。(2016/11/22現在)  
某ゲームでスタージュエルに課金するようなモーダルウィンドウが出てくるのでそれに従っていけば大丈夫です。  
支払うとすぐにDeveloper Consoleが使用可能になります。
  
[f:id:gakusei200709:20161124234644p:plain]

  
## デバイス登録  
実機でデバッグするためにデバッグ可能端末として登録する必要があります。  
「ADD NEW DEVICE」のボタンを押して出てくるフォームにシリアルナンバーを記入します。  
Descriptionは任意です。もし複数端末を登録する際はどの端末かわかるよう記入しておくと良いです。  
シリアルナンバーの確認方法にはいくつかあります。  
  ・箱に貼ってあるシリアルナンバーを確認する。  
[f:id:gakusei200709:20161124235057j:plain] 
  ・DeveloperConsole->Add New DEVICEに出てくるフォームにあるスピーカーのアイコンを押すとネットワーク上にあるキャストにシリアルナンバーを出力してくれます。  
[f:id:gakusei200709:20161124235205p:plain]
登録後「Status」に「Ready For Testing」が表示されていればテスト可能です。  

## アプリケーション登録
デプロイするアプリケーションを登録します。  
「Add New Application」を押します。幾つかアプリケーションの形式を問われますが、今回は「Custom Reciver」で登録します。  
Nameにはアプリ名をReceiverApplication URLにはアプリをデプロイするURLをファイル名込みで記入します。  
登録後Developer ConsoleにApplicationIDが表示されればConsole上での作業は終了です。  
  
## サンプルをデプロイ 
今回はChromeからキャストをテストできるCastHelloText-chromeを試します。  
  
[https://github.com/googlecast/CastHelloText-chrome:embed:cite]

  
下のリポジトリからファイルを落として「receiver.html」、「chromehellotext.html」を自分でホスティングしているWebサーバーにデプロイします。  
前者はChromeChastで表示するもの、後者がユーザーがアクセスするファイルです。  
  
  
現状でも動きますが、このままではテストソースに記入されているApplicationIDサーバーにアクセスが流れてしまいます。今回はアプリケーション登録をしているので「chromehellotext.html」の下の部分を書き換えましょう。  
```  
<script type="text/javascript" src="//www.gstatic.com/cv/js/sender/v1/cast_sender.js"></script>
<script type="text/javascript">
var applicationID = 'ここをConsoleで表示されたApplicationIDに変更';
```

このApplicationIDを変更することによって自分がホスティングしている「receiver.html」にアクセスが流れるようになります。  
これで問題がなければ無事起動します！ ホストしたサーバーにアクセスしてフォームに書き込んでEnterを押してみてください！  

  
[f:id:gakusei200709:20161124235359p:plain]

ChromeChastのアプリはHTMLで作れるのを考えると非常に簡単に作れます。ただ、入力デバイスがないなど普通のアプリケーションとは違う考え方をしないといけないのはなかなか難しいところ…  
何かアイディアを考えて面白いキラーアプリを作りたいですねー  

