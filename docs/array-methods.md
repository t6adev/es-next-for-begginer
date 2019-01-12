# Arrayメソッド
ES2015以降、便利なArrayメソッドが多く追加されています。  
ここでは便利なメソッドをいくつか紹介したいと思います。

mapやfilterなど、基本的にはメソッドに与えられた関数の第１引数に配列の要素が渡され、第２引数に要素の順番である番号が渡されます。reduceは特殊な仕様なので注意してください。

## map()
mapは、配列の要素に対して何かしらの処理を加え、新たに配列を生成するメソッドです。  
処理したい内容は、関数で与えます。下記での`sayHello`や`sayBye`です。

```
const names = ['Alice', 'Bob', 'Tom'];

const sayHello = (name, index) => `Hello ${name}. You are ${index}.`;
const sayBye = name => `Bye ${name}.`;

const greetingList = names.map(sayHello);
const byeList = names.map(sayBye);

console.log(greetingList);
console.log(byeList);
```
[https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/map](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

## filter()
filterは、与えられた関数をパスした要素からなる新たな配列を生成するメソッドです。パスしたかどうかは、その関数の戻り値が真であるかどうかで判断されます。

```
const numbers = [0, 1, 2, 3, 4, 5, 6];

const checkOdd = num => num % 2 !== 0;
const checkEven = num => num % 2 === 0;

const oddNumbers = numbers.filter(checkOdd);
const evenNumbers = numbers.filter(checkEven);
const more100Numbers = numbers.filter(num => num > 100);

console.log(oddNumbers);
console.log(evenNumbers);
console.log(more100Numbers);
```
[https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/filter](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

## find()
findは、条件にヒットした値を返すメソッドです。条件をチェックする関数を与え、その戻り値が真である場合に配列の要素を返します。
条件にヒットした最初の値を返すことに注意しましょう。また、条件にヒットしない場合は`undefined`を返します。

```
const numbers = [6, 5, 4, 3, 2, 1, 0];

const checkOdd = num => num % 2 !== 0;
const checkEven = num => num % 2 === 0;

const oddNumber = numbers.find(checkOdd);
const evenNumber = numbers.find(checkEven);
const more100Number = numbers.find(num => num > 100);

console.log(oddNumber);
console.log(evenNumber);
console.log(more100Number);
```
[https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/find](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/find)

## findIndex()
findIndexは、findと似ています。findの場合は、条件にヒットした配列の`値`を返しましたが、findIndexは、配列の`要素番号`を返します。
  
条件にヒットしない場合、`-1`を返します。

```
const numbers = [0, 1, 2, 3, 4, 5, 6];

const checkOdd = num => num % 2 !== 0;
const checkEven = num => num % 2 === 0;

const oddNumberIndex = numbers.findIndex(checkOdd);
const evenNumberIndex = numbers.findIndex(checkEven);
const more100NumberIndex = numbers.findIndex(num => num > 100);

console.log(oddNumberIndex);
console.log(evenNumberIndex);
console.log(more100NumberIndex);
```
[https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)

## reduce()
reduceは他とはちょっと違った特殊なメソッドです。  
細かな説明はこちらのドキュメントを参照してください。  
[https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)

例を用いて説明すると、数値をもつ配列からすべてを合計した値を得る(数学の総和)処理を実現できます。

```
const numbers = [1, 2, 3, 4];
const sumFn = (amount, current) => amount + current;
const result1 = numbers.reduce(sumFn, 0);
const result2 = numbers.reduce(sumFn);
```

`reduce()`は、第一引数に`callback関数`（上記のsumFn）、第二引数にcallbackの`初期値`（上記の0）を受け取ります。

callback関数は、第一引数に`前回のcallbackの戻り値`、第二引数に`現在の配列の要素`を受け取ります。

注意として、`reduce()`の第二引数（初期値）が与えられた場合の、最初のcallback関数の引数値が変わります。

上記の例の場合で説明します。
#### 初期値が与えられた場合
`const result1 = numbers.reduce(sumFn, 0);`の場合です。  
初回、callback関数の第一引数に初期値が渡され、第二引数に配列の0番目の要素が渡されます。
|sumFn|amount|current|sumFnの戻り値|
|:-:|:-:|:-:|:-:|
|初回|0|1|1|
|2回目|1|2|3|
|3回目|3|3|6|
|4回目|6|4|10|

#### 初期値が与えられない場合
`const result2 = numbers.reduce(sumFn);`の場合です。  
初回、callback関数の第一引数に配列の0番目が渡され、第二引数に配列の1番目の要素が渡されます。
|sumFn|amount|current|sumFnの戻り値|
|:-:|:-:|:-:|:-:|
|初回|1|2|3|
|2回目|3|3|6|
|3回目|6|4|10|

### 戻り値の型は自由
上記の例では戻り値はNumber型でしたが、配列の内容に関わらず、戻り値は文字列や配列、オブジェクトでも可能です。  
例えば、数値を持つ配列から、奇数と偶数にわけた配列をプロパティとして持つオブジェクトを得る処理を考える場合、以下のように書くことが出来ます。

```
const numbers = [1, 2, 3, 4];
const result = numbers.reduce((obj, current) => {
  if (current % 2 === 0) {
    obj.even.push(current);
    return obj;
  }
  obj.odd.push(current);
  return obj;
}, { even: [], odd: [] });

console.log(result);
```
