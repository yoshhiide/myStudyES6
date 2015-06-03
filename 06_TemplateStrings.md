# ES6/TemplateStrings
- 検証した日：2015/5/29
- 検証ブラウザ：FireFox Developer Edition 40.0a2 (2015-05-28)

## **TemplateStringsとは**
- 変数を展開して表示する
  
***

**MDNにおける説明** [MDN - TemplateStrings](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/template_strings)


## **コードで示すと**

※`//実行結果`とします。


```js
var a = 'yamada';
console.log(`my name is ${a} desu!`);
```

## **便利そうだけどこれまでのやり方でも良くない？**

[airbnb - StyleGuide](https://github.com/airbnb/javascript#6.4)

以下、引用

```js
// bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

// good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

AirbnbのStyleGuideによると、Template strings 使っていきましょうとのこと。


# **便利だからといって油断は禁物な例**

```js
var x = 'ＰＨＰ';
var y = '大好き';
var z = `ぼくたちは${x}が${y}です`;

console.log(z);
//ぼくたちはＰＨＰが大好きです

x = 'JavaScript';
y = '趣味';

console.log(z);
//ぼくたちはＰＨＰが大好きです
```

x, y に代入後の出力でも前回と同じ文字列となりました。
動的に値を更新してくれるわけではないです。


解決策

```js
var x = 'ＰＨＰ';
var y = '大好き';
var z = () => `ぼくたちは${x}が${y}です`;
x = 'JavaScript';
y = '趣味';

console.log(z());
//ぼくたちはJavaScriptが趣味です
```

もっと丁寧に書くとするとこんな感じでしょうか。

```js
let temps = {};
temps.lang = 'PHP';
temps.think = '大好き';

let z = (obj) => {
  if(obj && obj.lang && obj.think){
    return `ぼくたちは${obj.lang}が${obj.think}です`;
  }else{
    return '';
  }
};
temps.lang = 'JavaScript';
temps.think = '趣味';

console.log(z(temps));
//ぼくたちはJavaScriptが趣味です
```


***

今回のすべての参照：
[MDN - TemplateStrings](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/template_strings)
[airbnb - StyleGuide](https://github.com/airbnb/javascript#6.4)

***
