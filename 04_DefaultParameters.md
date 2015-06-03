# ES6/DefaultParameters
- 検証した日：2015/5/22
- 検証ブラウザ：FireFox Developer Edition 40.0a2 (2015-05-19)

## **DefaultParametersとは**
- 関数の引数に初期値を設定することができる
  
***

**MDNにおける説明** [MDN - Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
>Default function parameters allow formal parameters to be initialized with default values if no value or undefined is passed.
>>自分翻訳「functionの引数に初期値を与えることを許す。引数に値がなかったり引数が与えられなかった場合に指定した初期値になる」


## **コードで示すと**

※`//実行結果`とします。

```js
function func(a = 2){
  console.info(a);
}
func(); //2
```

```js
function func(a = 2){
  console.info(a);
}
func(50); //50
```

```js
function func(a = 2){
  console.info(a);
}
func(0); //0
```

```js
function func(a = 2){
  console.info(a);
}
func('test'); //test
```

```js
function func(a = 2){
  console.info(a);
}
var b;
func(b); //2
```

```js
function func(a = 2){
  console.info(a);
}
var b = null;
func(b); //null
```

```js
function func(a = 2){
  console.info(a);
}
var b = [];
func(b); //Array [ ]
```

```js
function func(a = 2){
  console.info(a);
}
var b = (...num) => num.reduce((a, b) => a + b);
func(b); //function b()
```

上記のように、関数の引数に初期値を設定することができる。

引数に初期値を設定できなかったとき(~ES5)の書き方。

```js
function func() {
  var a = arguments[0] === undefined ? 2 : arguments[0];
  console.info(a);
}
var b = null;
func(b);
```
  
**超便利!!**


***

今回のすべての参考：
[MDN - Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

***
