# ES6/let, const
- 検証した日：2015/5/20
- 検証ブラウザ：FireFox Developer Edition

### **let, constとは**
- 新しく追加された変数宣言の型
(従来は変数宣言はvarのみだった)
- ブロックスコープ
- 巻き上げしない

let: block scope　←！
const: block scope　←！
var: function scope

### **let**

**MDNにおける説明** [MDN - let](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/let)
>局所変数を宣言します。任意で値を代入して初期化できます。
>
>let を使用することで、変数のスコープをそれが使用されたブロック、文または式に限定することができます。
>これは var （ブロックスコープに関係なく、グローバルな、もしくはある関数全体でのローカルな変数を定義する）とは異なります。

>ブロックスコープ
>let で宣言された変数はそれを取り囲んでいるブロックの先頭へ引き上げられます。

>同じブロック内で同じ変数を再宣言すると TypeError が発生します。

#### **(1)ブロックスコープであることの意味**

```js
var language = 'javascriptdayo';
if(true){
  var team = 'SystemTeam';
  let company = 'iw';
}
console.info(language);
console.info(team);
console.info(company);
```

実行結果(consoleのところ)

```js
console.info(language); //'javascriptdayo'
console.info(team); //'SystemTeam'
console.info(company); //Exception: ReferenceError: company is not defined
```

#### **(2)非同期処理に変数を渡す例**

従来

```js
for(var i=1; i<6; i++){
  setTimeout(function(){
    console.info(i)
  }, 500);
}
//実行結果
//6
//6
//6
//6
//6
```

500ms後にそのタイミングの`i`を出力することになります。

**この場面で`let`を使ってみる**

```js
for(var i=1; i<6; i++){
  let z = i;
  setTimeout(function(){ console.info(i, z)}, 500);
}
```

↑をarrow functionで書くと↓

```js
for(var i=1; i<6; i++){
  let z = i;
  setTimeout(() => console.info(i, z), 500);
}
//実行結果
//6 1
//6 2
//6 3
//6 4
//6 5
```

`let z`で宣言した変数について、`setTimeout`に渡したタイミングの値が出力される。

では、`let`を使用してループ中に非同期処理に渡したタイミングの変数を使わせる為の今後の書き方はこちら。

```js
for(let i=1; i<6; i++){
  setTimeout(() => console.info(i), 500);
}
//実行結果
//1
//2
//3
//4
//5
```

※MDNでも上記`for(let i=1...`のような使用例の記載あり



#### **(3)多重宣言**

```js
let php = 'これはPHPです';
var ruby = 'これはRubyです';
if(true){
  let php = 'そろそろ7がでるかもしれません';
  var ruby = 'Railsって知っていますか';
  console.info(php);
}
console.info(php);
console.info(ruby);
//実行結果
//そろそろ7がでるかもしれません
//これはPHPです
//Railsって知っていますか
```

#### **(4)letは巻き上げない**

```js
if(true){
  console.info(a);
  console.info(b);
  var a;
  let b;
}
//実行結果
//undefined
//ReferenceError: can't access lexical declaration `b' before initialization
```

下記例でも↑と同様の結果

```js
if(true){
  console.info(a);
  console.info(b);
  let b;
}

```

**参考：** [slideshare](http://www.slideshare.net/ewingryan/let-46242299)

***

### **const**

定数宣言ではあるが、プロパティ値の変更は可能。

**MDNにおける説明** [MDN - const](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/const)
>読み取り専用の名前付き定数を宣言します。

#### **いろいろ試してみた**

コンソール実行してみましたので、`//`が実行結果になります。

```js
const max_count = 50;
//undefined
max_count -= 1;
//49
max_count;
//50
max_count = 30;
//30
max_count;
//50
```

```js
const c = {id: 10000, no: 22222, age:20};
//undefined
c;
//Object { id: 10000, no: 22222, age: 20 }
c.id
//10000
c.no
//22222
c.age
//20
c.name = 'yamada';
//"yamada"
c;
//Object { id: 10000, no: 22222, age: 20, name: "yamada" }
c.name = 'tanaka';
//"tanaka"
c;
//Object { id: 10000, no: 22222, age: 20, name: "tanaka" }
c.id = 999;
//999
c;
//Object { id: 999, no: 22222, age: 20, name: "tanaka" }
```

留意しておきたいところ
下記のようなif文内に変数の代入を行うことについて、そもそもがバッドパターンである可能性があるかもしれないと思い、スタイルガイドを探してみたのですが見当たりませんでした。
MDNでは２重括弧にしてほしいとの記述がありました。
[MDN - if...else](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/if...else)
ES6ではバッドパターンとなるのかどうか今後のスタイルガイドの動向も見守りたいと思います。

```js
const v = true;
if((v = false)){ // ここでエラーとなる為実行不可
  console.info('true!!');
}else{
  console.info('false!!');
}
//undefined
//SyntaxError: invalid assignment to const
v
//true
```

***

今回のすべての参考：
[MDN - let](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/let)
[slideshare](http://www.slideshare.net/ewingryan/let-46242299)
[MDN - const](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Statements/const)
[airbnb - JavaScript Style Guide](https://github.com/airbnb/javascript)
[個人のブログ - AirbnbのES6スタイルガイドを読んで](http://blog.h13i32maru.jp/entry/2015/04/14/204223)
