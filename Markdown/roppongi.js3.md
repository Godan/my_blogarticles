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
[slide](https://www.slideshare.net/euxn/20180529-which-should-i-save-babel-modules-in-devdependencies-or-dependencies)

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
[slide](https://slides.com/ktsn/reading-fromjs#/)
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

# エンジニアでも気にしたい色のアクセスビリティ
アクセスビリティ領域は多岐にわたるが ここでは色
 
 yarmでCLIで色盲の人は違いがわからない

 どうすれば良い？
 Issuで提案 
 Green→Blue

 治そうとしたら第三色覚異常には問題になる

 →利用者のターミナルに設定を委ねたほうがいい

 WXAG2.0には「色が唯一の情報ソースになってはならない」

 色盲ですら他人事ではない

 まとめ  
 色がユイツの情報ソースになってはならない  
 CLIでも気にしていくべき
 Webでもね

---

# Node Security Platform nsp, npm audit
[side](https://speakerdeck.com/ohbarye/color-accessibility-that-engineers-should-care)

NPMには脆弱性の情報管理公開する組織がある
報告すると開発者に通達45日以内に改善がなければ脆弱性が公開される

## NSP
installされているNPM脆弱性を監視できる  
買収されてNPMに組み込まれた (npm audit)

npmでinstallした際にサマリが出るように

yarmには非対応
nsp… package.jsonで脆弱性表示
NPM audit…エラーで死ぬ

yarnからpackage-lock.json に変更する

yean auditを作る動きもある

メルカリケース
CIで実行週一で実行Slackに通知


## 運用してみて
コスト結構高い
Webpackの脆弱性出たらかなりでた
hackerOneで是弱正の内容発生条件が確認できる

パッチ出てないことが多い  
過ぎに対応も辛い  
NPMに入ったので頑張ってほしい

----


# なぜ私ははRudixをやめたのか

今日来日したよ！
## Memoization
関数の結果を記録してすぐ返す


--- 

# 5分でわかるivy
angulerの3代目の新しいレンダラー

incrementalDOM がベース
仮想Nodeの仕組み

