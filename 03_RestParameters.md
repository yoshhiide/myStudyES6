# ES6/RestParameters
- 検証した日：2015/5/21
- 検証ブラウザ：FireFox Developer Edition 40.0a2 (2015-05-19)

## **RestParametersとは**
- 以前は関数の引数をargumentsオブジェクトで受け取っていたが同様扱いができるシンタックス
- 関数の引数を可変長の配列で受け取ることができる
- パラメータを渡さない場合も長さ0の配列になる
  
***

**MDNにおける説明** [MDN - Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
>The rest parameter syntax allows to represent an indefinite number of arguments as an array.
>>Google翻訳「残りのパラメータの構文は、配列としての引数の不特定多数を表現することができます。」


## **コードで示すと**

※`//実行結果`とします。

```js
function rest(...arr){
  console.info(arr);
}
rest(3, 4, 5, 6, 7); //Array [ 3, 4, 5, 6, 7 ]
```

上記のように、ひとつずつの引数をまとめて一つの引数(arr)で受け取れる。

以前のargumentsではどうだったか。

```js
function arg(){
  console.info(arguments);
}
arg(3, 4, 5, 6, 7); //Arguments { 0: 3, 1: 4, 2: 5, 3: 6, 4: 7, 他 2 個... }
```


## **失敗する例など**

複数のパラメータを渡したい場合の記述

```js
function rest(func, ...arr){
  func(arr);
}
rest(function(a){console.info(a)}, 3, 4, 5, 6, 7);
// Array [ 3, 4, 5, 6, 7 ]
```

**RestParametersの順序を先にしてみると・・・**

```js
function rest(...arr, func){
  func(arr);
}
rest(3, 4, 5, 6, 7, function(a){console.info(a)});
// SyntaxError: parameter after rest parameter
```

→ SyntaxError: parameter after rest parameter
rest parameterは他の引数より前に来ちゃダメだそうです。


## **RestParametersの配列の長さ**

```js
function rest(...arr){
  console.info(arr.length);
}
rest(3, 4, 5, 6, 7);
// 5
```

```js
function rest(...arr){
  console.info(arr.length);
}
rest();
// 0
```

## **おさらいも兼ねて**


```js
var sum = function(...num){
  return num.reduce(function(p, c){
    return p + c;
  });
};
console.info(sum(1,2,3,4,5)); 
// 15
```

arrow functionで書くと

```js
var sum = (...num) => num.reduce((p, c) => p + c);
console.info(sum(1,2,3,4,5));
// 15
```

早目に見慣れておいた方が良いかもしれません。
  
## **airbnb style guide**
[airbnb style guide - 7.6 Never use arguments, opt to use rest syntax ... instead.](https://github.com/airbnb/javascript#7.6)

Never use arguments, opt to use rest syntax ... instead.

自分訳「argumentsは使わずに、...シンタックスを使ってください」
(誤訳でしたらどなたか教えてください...)

>```js
  // bad
  function concatenateAll() {
    const args = Array.prototype.slice.call(arguments);
    return args.join('');
  }
  // good
  function concatenateAll(...args) {
    return args.join('');
  }
```


***

今回のすべての参考：
[MDN - Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
[個人ブログ - 1000ch.net](https://1000ch.net/posts/2013/es6-features-2.html)
[Airbnb - JavaScript Style Guide](https://github.com/airbnb/javascript#7.6)
***
