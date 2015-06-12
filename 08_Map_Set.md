# ES6/Map_Set
- 検証した日：2015/6/12
- 検証ブラウザ：FireFox Developer Edition 40.0a2 (2015-06-06)

## **Map,Setとは**
- Map : key-value形式で格納されるオブジェクト
- Set : valueを格納するオブジェクト

***

## **コードで示すと**

※`//実行結果`とします。

### **Map**

```js
let maps = new Map();

const chnm = 'firefoxdevedition';
const numb = 2460;
const func = function(arr) { arr.reduce((a, b) => a + b)};
const obj  = {};

maps.set(chnm, 'これは名前です');
maps.set(numb, 'これは数値です');
maps.set(func, 'これは関数です');
maps.set(obj,  'これはオブジェクトです');
```

```js
maps.size
//4

maps.get(chnm);
//"これは名前です"

maps.get(numb);
//"これは数値です"

maps.get(func);
//"これは関数です"

maps.get(obj);
//"これはオブジェクトです"

maps.get({});
//undefined

maps.get(2460);
//"これは数値です"

maps.get('firefoxdevedition');
//"これは名前です"

maps.get(function(arr) { arr.reduce((a, b) => a + b)});
//undefined
```

他にも、`.clear()`, `.delete()`, `.has()`, `.keys()`, `values()`などが使える。
Setでも上記が使えるが、Setの場合は`.set()`の代替が`.add()`となる。`.get()`はない。


### **Set**

```js
var s = new Set();
s.add('s100');
s.add('s200');
s.add('s300').add('s400');

console.log(s.has('s10'));
// false

console.log(s.has('s100'));
// true

s.forEach(function(val) {
  console.log(val);
});
// s100
// s200
// s300
// s400
```


DOMでもいける！

```js
let s = new Set();

s.add(document.body);
console.log(s.has(document.querySelector('body')));
// true

s.add(document.querySelector('#container'));
console.log(s.has(document.querySelector('#container')));
// true

```


***

今回のすべての参照：
[MDN - Map](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Map)
[MDN - Set](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Set)

***
