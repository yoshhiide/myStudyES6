# ES6/Spread Operator
- 検証した日：2015/5/26
- 検証ブラウザ：FireFox Developer Edition 40.0a2 (2015-05-25)

## **Spread Operatorとは**
- 配列を平坦に展開してくれるようなもの
- Rest Parametersに関連
  
***

**MDNにおける説明** [MDN - Spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)
>The spread operator allows an expression to be expanded in places where multiple arguments (for function calls) or multiple elements (for array literals) are expected.
>>Google翻訳「スプレッド演算子は式がまたは（配列リテラルのための）複数の要素（関数呼び出しのための）複数の引数が期待されている箇所に展開することができます。」


## **コードで示すと**

※`//実行結果`とします。

```js
const onetwo = [1, 2];
console.log([...onetwo, 3, 4, 5]);
// Array [ 1, 2, 3, 4, 5 ]
```

ES5以前の書き方は `concat` を使って配列に結合させていました。

```js
var onetwo = [1, 2];
console.log([].concat(onetwo, [3, 4, 5]));
```

配列を平坦化してくれるイメージです

```js
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(...arr2);
// Array [ 0, 1, 2, 3, 4, 5 ]
```

上記との違い

```js
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(arr2);
// Array [ 0, 1, 2, [3, 4, 5] ]
```

もう一度イメージをおさらい

```js
var arr = [1, 2, 3, 4, 5];

console.log(arr);
// Array [1, 2, 3, 4, 5]

console.log(...arr);
// 1 2 3 4 5

// arr は 配列 [1, 2, 3, 4, 5]
// ...arr は 1 2 3 4 5
```


関数の引数とする場合

```js
function spreadoperator(a,b,c){
  console.log(a);
  console.log(b);
  console.log(c);
}
const abc = [10,200,'ccccc'];
spreadoperator(...abc);
// 10
// 20
// ccccc
```

ES5以前の書き方では↓

```js
function spreadoperator(a, b, c) {
  console.log(a);
  console.log(b);
  console.log(c);
}
var abc = [10, 200, 'ccccc'];
spreadoperator.apply(undefined, abc);
```

**ここからMDNからそのまま転載**

***

>With ES6 spread you can now write the above as:

```js
function f(x, y, z) { }
var args = [0, 1, 2];
f(...args);
```

>Any argument in the argument list can use the spread syntax and it can be used multiple times.

```js
function f(v, w, x, y, z) { }
var args = [0, 1];
f(-1, ...args, 2, ...[3]);
```

>A more powerful array literal

```js
var parts = ['shoulder', 'knees'];
var lyrics = ['head', ...parts, 'and', 'toes'];
```

>A better push
>Example: push is often used to push an array to the end of an existing array. In ES5 this is often done as:

```js
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
// Append all items from arr2 onto arr1
Array.prototype.push.apply(arr1, arr2);
```

>In ES6 with spread this becomes:

```js
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(...arr2);
```

***

かなり有効な使い方ができるということがわかりますね。

***

今回のすべての参考：
[MDN - Spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

***
