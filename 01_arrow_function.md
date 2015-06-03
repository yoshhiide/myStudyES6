# ES6/アロー関数
- 検証した日：2015/5/19
- 検証ブラウザ：FireFox


アロー関数式（またはファットアロー関数）はfunction式に比べより短い構文を持ち、 this の値をレキシカルに束縛します。アロー関数は常に匿名関数です。

```js

var a = [2, 3, 4, 5];

//これを・・・
var b = a.reduce(function(m, n){ return m + n; });
console.log(b);
// 14

//アロー関数でかくと
var c = a.reduce((m, n) => m + n);
console.log(c);
// 14

//単純なfunctionの場合
var d = function(aa){ return aa[2]};

//アロー関数でかく
var e = (aa => aa[2]);
console.log(e(a));
// 4

//名前付のfunction
var addnum = (a, b) => a + b;
addnum(6, 3);
// 9

//名前なしのfunction
(() => 'sonomama')();

//15より大きい数の場合は15を返す。それ以外はそのまま返す
var simple = a => 15 > 15 ? 15 : a;
simple(16);
//15
simple(10);
//10;

//大きい方を返す
let data = [1, 2, 3, 10, 30, 28, 9, 27];
let max = (a, b) => a > b ? a : b;
let result = data.reduce(max);
console.log( result );
//30

```

引数が１つであっても`()`で囲った方が良いかと思いました。

if文中の注意したいパターン

```js
let a = 80;
if(a => (a + 120)){
  console.log(' true!! ');
}else{
  console.log(' false!! ');
}
// true!!

let a = 80;
if(a >= (a + 120)){
  console.log(' true!! ');
}else{
  console.log(' false!! ');
}
// false!!

//ES5まではif文内 => はエラー。ES6ではOK

```



*参考：* [MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/arrow_functions)

