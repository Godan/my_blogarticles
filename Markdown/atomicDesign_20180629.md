# アトミックDesign
UIDesignは複数人が関わっている

* ディレクター 
* デザイナー

みんないろんな側面でDesignをみている
ぶ
* 分業しているときはコミュニケーションが必要  
* ワイヤーフレームだったりサイトマップだったり
* デザインカンプだったり
    * 実装前に完成イメージを合わせる
* 本当に意図した通りにユーザーが動くのか
* Designフローの見直し
    * 構造化の指針を決める
    * 情報をデザインする
    * 構造をレビューするソフトウェアを実装する
* 導入当初のフロー
    * 最初は情報Design → 実装
    * コミュニケーションコストが多い
    * それなら最初から決めに行ったほうが良い
    * デザインガイドラインを作る
        * 色
        * フォントサイズ
        * ガチガチに決めない 作り込まない
    * 命名規則を決める 
        * みんな違うこと考えがち
        * 微妙に違うことによって混乱する
    * 相談内容が属人化されるとまずい
        * 決定したことがチームに共有されづらい
        * エンジニアとデザイナーのコミュニケーションコストが増大する つらい
            * レビューするようにしよう
    * Designの造構造のレビューする
        * エンジニアのコードレビューの感じ
        * 途中経過がオープン
        * http://www.standardinc.jp/reflection/article/abstractapp/
        * storyBook
        * コンポーネントリスト化
        * テスト効率化
    * チームのコラボレーション  
    * レビューコストを下げる
        * コードレビュー
            * UIコンポーネントごとにレビュー
            * スコープが狭くなってレビューコストDOWN
            * Interface Inventory
    * オープンデザイニング
        * モブデザイニング？
            * 難易度が高いものを一気に解決する 
            * まぁ多分そうかも
            * 公開して行うことが大事
            * デザインレビューもいらない
            * デザイナの中には作業途中を公開したくない人もいる
    * 本に色々書いているのでよろしくおねがいします
    * AbemaTVは随時