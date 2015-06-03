# ES6/Object.assign
- 検証した日：2015/6/3
- 検証ブラウザ：FireFox Developer Edition 40.0a2 (2015-06-02)

## **Object.assignとは**
- 複数のオブジェクトをマージする
  
***

**MDNにおける説明** [MDN - Object.assign](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

>１つ以上のソースオブジェクトの保有する全ての列挙プロパティの値を、ターゲットのオブジェクトへコピーします。戻り値はターゲットオブジェクトになります。

## **コードで示すと**

※`//実行結果`とします。

### クローン(コピー)

```js
var obj = {id:123, name:'yamada', livein:'japan', birthyear:'1986'};
// クローンをつくる(参照を切ったコピー)
var cpclone = Object.assign({}, obj);

console.log(cpclone);
//Object { id: 123, name: "yamada", livein: "japan", birthyear: "1986" }

// それぞれのオブジェクトのプロパティ値を変更する
obj.id = 999;
cpclone.livein = 'usa';

// 下記より参照が切れていることを確認できる
console.log(obj);
//Object { id: 999, name: "yamada", livein: "japan", birthyear: "1986" }

console.log(cpclone);
//Object { id: 123, name: "yamada", livein: "usa", birthyear: "1986" }
```

### マージ 


```js
var obj1 = {id:100, name:'yamada', livein:'japan', tel:'9991111222'};
var obj2 = {id:567, name:'tanaka', livein:'brazil', birthyear:'1986'};
var cpclone = Object.assign({}, obj1, obj2);

console.log(cpclone);
//Object { id: 567, name: "tanaka", livein: "brazil", tel: "9991111222", birthyear: "1986" }
```

`obj1`と`obj2`の差分を上書きするようなイメージ

`Object.assign({}, obj1, obj2, obj3, obj4........)`と複数まとめて実行可能

最初の引数にマージしていく為、最初の引数は`{}`としておくのが良さそう。


### 深いマージをするのかどうか

```js
var obj1 = {id:1230, ar:[100,200,300]};
var obj2 = {ar:[1,2,3,4,5]};
var cpclone = Object.assign({}, obj1, obj2);

console.log(cpclone);
//Object { id: 1230, ar: [1, 2, 3, 4, 5] }
```

深いマージはしません。浅いマージとなります。


***

今回のすべての参照：
[MDN - Object.assign](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

***
