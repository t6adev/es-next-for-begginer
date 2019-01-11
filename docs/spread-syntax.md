# スプレッド構文
スプレッド構文とは、ArrayやObjectの変数名の前に`...`を書くことで展開できます。  

```
const numbers = [1, 2, 3];
const moreNumbers1 = [...numbers]; // [1, 2, 3]
const moreNumbers2 = [-3, -2, -1, 0, ...numbers]; // [-3, -2, -1, 0, 1, 2, 3]
const moreNumbers3 = [...numbers, 4, 5, 6]; // [1, 2, 3, 4, 5, 6]
const moreNumbers4 = [...numbers, ...moreNumbers1]; // [1, 2, 3, 1, 2, 3]

const obj = { a: 1, b: 2, c: 3 };
const extendObj1 = { ...obj }; // { a: 1, b: 2, c: 3 }
const extendObj2 = { ...obj, d: 4 }; // { a: 1, b: 2, c: 3, d: 4 }
const extendObj3 = { d: 4, ...obj }; // { a: 1, b: 2, c: 3, d: 4 }
const extendObj4 = { a: 100, ...obj }; // { a: 1, b: 2, c: 3 }
const extendObj5 = { ...obj, a: 100 }; // { a: 100, b: 2, c: 3 }
const any = { z: 100 };
const extendObj6 = { ...obj, ...any }; // { a: 1, b: 2, c: 3, z: 100 }
```

※ObjectのスプレッドはES2018の仕様です
