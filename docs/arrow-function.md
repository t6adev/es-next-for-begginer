# アロー関数
`function`と書かずに`=>`で関数を書くことが可能になりました。

```
const a = () => true;
const b = () => { return true; }; // a()と同等
const c = () => ({ some: 'obj' });
const d = () => { return { some: 'obj' }; }; // c()と同等
const e1 = (arg) => { console.log(arg); };
const e2 = arg => { console.log(arg); }; // e1()と同等。引数が1つの場合、()を省略可能
```

## thisの扱いがfunctionと違うことに注意
ES5までの仕様での`function`では、関数ごとに自身の`this`を保持していました。  
しかし、アロー関数内で`this`を使う場合、その`this`は外側の`this`を意味します。  
例えば以下のコードは同じ内容です。  
Person1関数でのsetIntervalにて、growUp関数内で`this.age++`としても、その`this`はgrowUp関数のものなので意図した結果にはなりません。そのため`var that = this;`のようにする必要があります。
Person2関数でのsetIntervalに書かれた`this`は、Person2関数の`this`になります。

```
function Person1() {
  var that = this;
  that.age = 0;

  setInterval(function growUp() {
    that.age++;
  }, 1000);
}

function Person2() {
  this.age = 0;

  setInterval(() => {
    this.age++;
  }, 1000);
}
```

もう一つ見てみましょう。  
```
var obj = {
  i: 10,
  b: () => console.log(this.i, this),
  c: function() {
    console.log(this.i, this);
  }
};

obj.b(); // 出力は、 undefined, Window {...} のようになる
obj.c(); // 出力は、 10, Object {...} となる
```

この仕様を、アロー関数は`this`を束縛しない、といいます。

## functionとthisを使わず、アロー関数のみでのコーディングを目指す
主に、`this`を使う場合はコンストラクタを定義して`new`したいことがほとんどだと思います。  
以下の`Person関数`と`createPerson関数`は同じ機能を提供します。  
`this`と`function`を撲滅できました。

```
function Person() {
  var that = this;
  that.age = 0;

  setInterval(function () {
    that.age++;
  }, 1000);

  that.howOld = function () {
    console.log(that.age);
  }
}

const newPerson1 = new Person();

const createPerson = () => {
  const person = {
    age: 0,
    howOld: () => { console.log(person.age); },
  };
  setInterval(() => {
    person.age++;
  }, 1000);
  return person;
}

const newPerson2 = createPerson();

setInterval(() => {
  newPerson1.howOld();
  newPerson2.howOld();
}, 3000);
```
