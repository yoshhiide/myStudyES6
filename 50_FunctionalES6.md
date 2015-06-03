# Functional x ES6
- 検証した日：2015/5/22
- 検証ブラウザ：FireFox Developer Edition 40.0a2 (2015-05-21)

## **ES6を関数型で書いてみる**

- 配列に格納されたすべての数値の合計を算出する
- パターン１．「2」は計算しないこと
- パターン２．「5」は計算しないこと


※`//実行結果`とします。

まずはES5で関数型で書いた場合

```js
var sum = function sum(arr) {
  return arr.reduce(function (a, b) {
    return a + b;
  });
};
var fornum = function fornum(arr) {
  return arr.map(function (val) {
    return isFinite(val) ? Number(val) : 0;
  });
};
var check = function check(valid) {
  return function (arr) {
    return arr.map(function (val) {
      return val === valid ? 0 : val;
    });
  };
};
var check2 = check(2);
var check5 = check(5);
var list = ['1', '2', 3, '4', 5, 'end'];

//パターン１．
console.log( sum(check2(fornum(list))) ); //13
//パターン２．
console.log( sum(check5(fornum(list))) ); //10
```

そして、これをES6で書くと↓

```js
var sum = (arr) => arr.reduce((a, b) => a + b);
var fornum = (arr) => arr.map(val => isFinite(val) ? Number(val) : 0);
var check = (valid) => (arr) => arr.map(val => val === valid ? 0 : val);
var check2 = check(2);
var check5 = check(5);
var list = ['1','2',3,'4',5,'end'];

//パターン１．
console.log( sum(check2(fornum(list))) ); //13
//パターン２．
console.log( sum(check5(fornum(list))) ); //10
```

```js
//指定された値を除外しない場合
console.log( sum(fornum(list)) ); //15
```

  
**超スッキリ!!**

※ちょっと遠回りな書き方になってしまったかもしれないですが、機能をひとつひとつ分けてみました。
※１つ目のES5の方はES6で書いたものを[BABEL](https://babeljs.io/repl/)でトランスコンパイルしたものです。
BABELはLocalStorageを使用して前回書いたコードをブラウザ側に保存しておいてくれます。便利ですよ。

***
