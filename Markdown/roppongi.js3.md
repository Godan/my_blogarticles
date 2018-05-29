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

## sourcer
カルネージハートっぽくしたい
* 自分で時期を実装して対戦させる
* 学生向けイベントとか
* 社内向けイベントでつかってる
* リポジトリがあるから自分で試してみて！
* Herokuでもできる
* JS仲間で対戦しよう！
* 

 
