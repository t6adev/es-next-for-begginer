# 分割代入
分割代入とは、既存の配列やオブジェクトの値を取り出し、別の変数へ代入できるようになるものです。  
分割代入をする際は、既存の変数にも代入できますが(もちろんvarやletで定義された変数に対して)、新たな変数宣言時にも可能です。

## 配列の場合
シンプルな記法としては以下のようになります。
`fruits`という配列の0番目と1番目をそれぞれ`a`と`b`の変数に代入しています。（この場合、`a`と`b`は宣言も同時にされている）
また、この時`fruits`変数に変化はおきず、`['apple', 'orange', 'grape']`はそのままです。以下の例では、`a`と`b`という変数にしましたが、任意の変数名にできます。

```
const fruits = ['apple', 'orange', 'grape'];
const [a, b] = fruits;
```

`'apple'`は文字列としてなにかの変数で抜き出し、その他の要素（`'orange', 'grape'`）を配列として別変数に代入したい場合、以下のように書くことが出来ます。  

```
const fruits = ['apple', 'orange', 'grape'];
const [a, ...others] = fruits;
```
`a`は、上記と同じく`'apple'`が代入されます。  
`...`を書くことで`others`という変数に`'orange'を含むそれ以降の要素を配列として代入する`ことになります。この様に書かれたものを、`rest element`と呼びます。意味はそのままで、`残りもの`です。
注意として、rest elementは最後に書くことが出来るもので、`const [a, ...others, hoge] = fruits;`などとは書けません。

## オブジェクトの場合
シンプルな記法としては以下のようになります。
`{ color: 'red', fruit: true, popular: true }`のプロパティを持つオブジェクトの`apple`から、`color`と`fruit`のプロパティを`color`と`fruit`の変数に代入しています。（この場合、`color`と`fruit`は宣言も同時にされている）また、この時`apple`変数に変化はおきず、`{ color: 'red', fruit: true, popular: true }`はそのままです。

```
const apple = { color: 'red', fruit: true, popular: true };
const { color, fruit } = apple;
```

`color`のプロパティを`color`という変数名で分割代入し、それ以外の`fruit`と`popular`を別の変数にオブジェクトとして代入したい場合、以下のように書くことが出来ます。  

```
const apple = { color: 'red', fruit: true, popular: true };
const { color, ...others } = apple;
```

`...`を書くことで`others`という変数に`color以外のプロパティを含んだオブジェクトとして代入する`ことになります。配列の場合と同じような仕様です。  

上記まではプロパティ名を変数として代入する方法でしたが、以下のようにプロパティ名と分割代入する変数名を別のものにすることも可能です。`color`プロパティを`appleColor`という変数名で分割代入しています。

```
const apple = { color: 'red', fruit: true, popular: true };
const { color: appleColor } = apple;
```

なお、オブジェクトから取り出した値が`undefined`な場合、初期値を変数に指定できます。  
以下の`orange`オブジェクトには`popular`というプロパティは定義されていませんが(`undefined`)、分割代入の際に`{ popular = true }`と書くことで、`true`を初期値として指定しています。また、変数名を別にしたい場合、`const { popular: orangePopular = true } = orange;`のようにも書くことが出来ます。

```
const orange = { color: 'orange', fruit: true };
const { popular = true } = orange;
```
