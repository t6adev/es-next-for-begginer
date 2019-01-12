# 覚えておきたい構文など
## Object関連
### Shorthand property names
ES5までは、`a`, `b`, `c`からなる`obj`を定義したい場合は以下のようにしなければなりませんでしたが、`obj2`のように定義出来るようになりました。(objとobj2は同じ定義内容です)  
```
const a = 'foo';
const b = 42;
const c = {};

const obj = { 
  a: a,
  b: b,
  c: c
};
const obj2 = { a, b, c };
```

### Computed property names
プロパティ名に計算した値を使えるようになりました。(objとobj2は同じ定義内容)  
```
const obj = {
  propName: true,
};

const getPropName = () => 'propName';

const obj2 = {
  [getPropName()]: true,
};
```

## String関連
### テンプレート文字列
ES5までの文字列生成には`+`を使って文字連結したり、改行する場合は改行コードを書いていました。  
テンプレート文字列の機能を使うとより直感的に文字列を扱うことが出来ます。

```
const age = 18;
const introduction = `I am ${age + 2} years old.
How old are you?`;
```

上記のように、
```
``
```
（バッククオート）で文字列を囲みます。
改行は分かりやすく文字列内の改行が反映されます。
文字列内に変数を展開したい場合、`${}`を使います。`{}`内にはJavaScriptの式を書くことができるため、単純に変数だけではなく関数から演算まで様々な記述が可能です。  

## 関数関連
### デフォルト引数
ES5までは、例えば、引数を2つもつ関数を使う場合に1つしか引数を与えずに実行した場合、2つ目の引数は`undefined`となるしかありませんでした。
デフォルト引数では、引数が与えられなかった場合の引数のデフォルト値を関数定義時に指定できるようになります。  

```
const fn1 = (a, b) => `1st is ${a}, 2nd is ${b}.`;
const fn2 = (a, b = 'world') => `1st is ${a}, 2nd is ${b}.`;

console.log(fn1('hello'));
console.log(fn2('hello'));
```

### 分割代入とスプレッド構文の応用
[分割代入](./destructuring-assignment.md)と[スプレッド構文](./spread-syntax.md)を関数の引数を定義する際に応用できます。  

```
const anonymous = {
  name: 'anonymous',
  age: null,
  gender: null,
};
const someone = {
  name: 'someone',
  age: 30,
  gender: 'male',
};

const extract = ({ name, ...others }) => {
  if (name !== 'anonymous') return others;
  return null;
};

const result1 = extract(anonymous);
const result2 = extract(someone);
console.log(result1);
console.log(result2);
```
