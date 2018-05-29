# Roppongi.js


## supponser LT
[slide](https://speakerdeck.com/kentomoriwaki/typescript-in-wantedly)

Type Script導入しました

めっちゃ良かった
### 利点
#### 安心してコード変更
心理的安全性がめっちゃ上がった

#### 補完が効く

VSCode is good

### how Type Script in team
* ｔｓｃでビルドしない
* ビルド周りはしんどい
* バベルは結局必要

バベルだけでビルドできる
@babel/preset-typescript
.babelrcに追加するだけでいい

* babel 7(beta~)
* 完全互換はない
    * namespaceとかは使えないけどWorkaroundはあるよ


 
### ReduxのActionReducer周りのベストプラクティスがない
→TypeScript FSAでかいけつできる！

非同期周りのActionの定義
いろいろ自動で定義してくれる

---

# JSでつぶやきのオレオレ分類作ってみたい人生だった

CurApp
ヤマタツ

## やりたかったこと

Twitterで技術系のフィルターしたさ
SVM 機械学習のあれやね


## 分かち書き
日本語の自然言語処理のやつ


<!-- ここでベルが鳴る -->

教師データを作るの辛い  
Modelで来たけど制度は確認できづ  
振り分けアプリやいい出来だった  
日本語脳脳みそつかうので辛い  

DaynamoDBの気持ちがわからない

## SVM

機械学習むつがしい
JSは数字に弱い
Pythonでやったほうがいい

##Lambaで機械学習

5ふんでタイムアウト


学習済み使ったほうが良い

---

# Polymer
[slide](https://slides.com/takanorip/re-understand-polymer3#/)

ドキュメント新しくなったけど翻訳する人がぜんぜん居ない

Not  Polyfill!!

## 特徴
* 軽い！
* TypeScriptSupport
* バウワーがおなくなりに → 祝NPM化
* HTML Imports 廃止（Google しか実装しなかった）
    * →ES Modules
* ライフサイクル追加
*  2.0はVueぽさがあった
*  3.0からはClassベースに！
    *  使いやすそう
* LitElement
* PWA STARTER KIT
    * 気になるあとで試す

## まとめ
めっちゃ使いやすくなったよ！

---

# JSで対戦ゲー作った
[slide](https://yamatatsu.github.io/slides/002/#/)
## sourcer
カルネージハートっぽくしたい
* 自分で時期を実装して対戦させる
* 学生向けイベントとか
* 社内向けイベントでつかってる
* リポジトリがあるから自分で試してみて！
* Herokuでもできる
* JS仲間で対戦しよう！
* 

---

# Dartから来たBLoCの話
[slide](https://slides.com/adwd/bloc-from-dart#/)

ビジネスロジックコンポーネント
の略
* ReactとかVueとかではない
* Google AdWordsが発表
* DartConf GoogleI/Oで発表
* WebとMobileでビジネスロジックを共有したい
* 言語 プラットフォームにとらわれないビジネスロジック設計パターン
* ビジネスロジックをコンポーネントツリーと別のところに置く
* BLoCの外部インターフェースはobserverだけ
* RxJSでいうObservable.subscribe とObservable.next
* 関心をしっかり分離できる
* BLocはいいぞ
* Reduxとくらべて
    * 不満点を解消してくれる


---

# Which should I ....

* 名取さなガチ恋勢


* dependecies
* devDependenciesっぽい？
    * だめだった

## とあるRailsプロジェクト
Herokuにデプロイしようとした
Webpackでは通ってるのにおちた

react消すと動く

## 仮設
Webpacker？
Heroku?

Webpackerか？？  
dependenceにするか  
→通る   
Herokuが悪かった  
→けどWebpackはやめとけ  
https://twitter.com/murokaco/status/1001423159797604352

HerokuのYarnをみるとDependenciesしかインストールしてなさそう


----
# FromJSの黒魔術
やっていきFMの人だ！

## what fromJS
choromeのエクステンション
HTML内の文字から元のソースコードを当てる  
JSにその機能あたっけ？  
→ エラーだとコードの場所あるよね？
→あれはnew Errorでスタックで知ることができる

Babel！
文字列リテラルをバベルの静的解析で差し替えておく

なぜこんなものをつくろうとおもったのか…