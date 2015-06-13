# ES6/Array.from
- 検証した日：2015/5/23
- 検証ブラウザ：FireFox Developer Edition 40.0a2 (2015-05-19)

## **Array.fromとは**

**MDNにおける説明** [Array.from](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
> array-likeオブジェクトやiterableオブジェクトから新しいArray インスタンス を生成します。

## **コードで示すと**

※`//実行結果`とします。


文字列

```js
Array.from("foo");
// Array [ "f", "o", "o" ]
```

複数の引数

```js
function f() {
  return Array.from(arguments);
}
f(1, 2, 3); 
// Array [ 1, 2, 3 ]
```

Map

```js
var m = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(m);
// Array [ Array[1, 2], Array[2, 4], Array[4, 8]] 
```
Set

```js
var s = new Set(["foo", window]);
Array.from(s);
// Array ["foo", window]
```




第２引数は `.map()` と同じ

```js
Array.from([1, 2, 3, 4], x => x + x);
// [2, 4, 6, 8]
```

```js
[1, 2, 3, 4].map(x => x + x);
// [2, 4, 6, 8]
```

arrow functionを使わなかった場合の記述は

```js
Array.from([1, 2, 3, 4], function(x){ return x + x; });
// [2, 4, 6, 8]
```
  
    
  参照：[ECMAScript.next: Array.from() and Array.of()](http://www.2ality.com/2011/07/array-from.html)

```js
var divs = document.querySelectorAll("div");
Array.from( divs ).forEach(function( node ) {
    console.log( node );
});
```

***

今回のすべての参照：
[MDN - Array.from()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
[ECMAScript.next: Array.from() and Array.of()](http://www.2ality.com/2011/07/array-from.html)

***
