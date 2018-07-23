# カスタムエレメントとは

カスタムエレメントとはweb Componentに含まれるAPI使用の一つです。  
最近のモダン Webなサイトを見るとdivの塊です。  それだけ見るととても人間
がかけるような構造にはなっていません。  
それはそのはずです。実際には独自に定義されているHTMLを定義してコーディングされています。  
その独自定義をするためのAPI群がWeb Componentと呼ばれている仕様です。  


WebComponetと呼ばれる仕様群は４つの仕様に別れています。

* Custom Elements
* HTML Templates
* Shadow DOM
* HTML Imports

また４つの仕様はそれぞれ独立していた単体でも仕様可能になっています。

## Custom Elements
Custom Elementsは独自にHTMLタグを作成するための機能です。  
またWebのライフサイクルごとにどのような振る舞いをするのかを実装することができます。

今回は以下のサンプルコードを使用してchoromeの開発者モードのコンソールを通じて操作してライフサイクルの様子を観察してみます。

```js
class originaTag extends HTMLElement {
    // 健康を取得する属性の名前を書いておく
    static get observedAttributes() {return ['name']; }

    constructor() {
    // HTMLElement Classのコンスタントを実行
    super();
    }

    connectedCallback(){
    // 要素が挿入されたときに実行されます
    // このタイミングでシャドーDOMを呼び出します
        console.log('make!')
    }

    disconnectedCallback(){
        // 要素が削除された時に呼ばれます
        console.log('remove!')
    }

    attributeChangedCallback(attributeName, oldValue, newValue, namespace){
        // 要素の属性が変更された時に呼ばれます
        console.log('chenge attribute!')

    }

    adoptedCallback(){
        // ドキュメントが変わったとき  (ownerDocumentが変更された時に)呼ばれます
        console.log('change ownerDocument!')
    }
}

// Define the new element
customElements.define('original-tag', originaTag);

```

## chorome経由で表示したとき
まず 普通にhtmlファイルを開いてみます。  
コンソールを見ると「make!」がすでに出ています。 HTMLを描写時に```connectedCallback```が呼ばれて処理されているのがわかります。

## 開発者モードのElementsのウィンドウがらタグを消す。
こんどはElementsタブでoriginal-tagを消してみます。選択してDeleteを押すと消えます。  
消したあとにコンソールを見てみると「Remove!」が表示されていますね。 消す時に``` disconnectedCallback```が呼ばれているのもここで確認することができました。

## 属性を変更してみる
またページをリロードしてElementsタグからHTMLを編集します。  
今度はタグの属性値を足してみます。  タグにname属性を足します。  
足すとコンソールに「chenge attribute!」が表示されています。ちゃんと```attributeChangedCallback```が呼ばれているのがわかります。  
試しに再度name属性を変えてみます。再度変更すると再び「chenge attribute!」が表示されています。変更があるたびに呼ばれているのがわかります。  

ちなみに変更を取得するには事前にゲッターを宣言していく必要があります。 何も設定されていなければ取得ができません。

## まとめ

* custom elementは新しいタグを自分で作ることができる。
* 生成されたとき 消されたとき 属性が変化したとき  またドキュメントオーナーが変更されたときの４つのライフサイクルに対してのコールバックが用意されている

