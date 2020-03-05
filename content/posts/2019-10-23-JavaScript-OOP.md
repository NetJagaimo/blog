---
title: "JavaScript OOP"
date: "2019-10-23 12:20:00 +0800"
categories: ["JavaScript"]
tags: ["javascript"]
toc: true
---

{{% notice note %}}
參考章節: [Ch6 The Secret Life Of Objects](http://eloquentjavascript.net/06_object.html)  
Slides: https://slides.com/sirla_potato/javascript-oop  
環境: Windows10、Node.js(10.15.3)
{{% /notice %}}


![](https://i.imgur.com/ZkaDEH2.png)

## OOP介紹
### 簡介
OOP = Object Oriented Programming (物件導向程式設計)

將功能抽象化後，用程式表達出來的一種程式設計的方式，例如上面的圖，將兔子轉變為抽象化的描述方式
<!--more-->
### Class & Object
講到物件導向，最重要的兩個東西就是Class以及Object

先來解釋這兩者的關係
* Class: 設計圖
* Object: 用設計圖做出來的實際的東西

而將設計圖轉換為實際的東西，這個過程稱作「實例化」，Object亦即Class的一個實例

Class的組成包含
* Attributes(屬性): 這個class的一些資料
* Methods(方法): 這個class的動作

舉個例子來解釋上面講到的東西
![](https://i.imgur.com/NqKDHXj.png)

有一張設計圖叫做「學生」，這張設計圖包含了Name、Age、Weight、Height這些Attritubes，以及Walk、Eat、Sleep這些Method

而用這個class實例化後的Object就叫做小明，他會有自己的名字、年齡、體重與身高，而其他的Object(e.g. 小美、小華)也會有自己的這些資料。並且每個Object都有同樣的Methods。

### Encapsulation (封裝)
所謂的封裝，其實很簡單，就是將Object內的內容分為兩類
* Public: 別人看的到的且可以更動的
* Private: 別人不能看也不能更動的

在設計Object的時候就要先考慮好，這個Object的工作是什麼、需要跟別人合作的部分有甚麼、自己可以處理好的有什麼，別人需要拿到的部分就開設成public，別人不需要拿到的就設定為private

好處是分工明確，另一方面則是安全性考量，有些資料不能給別的人接觸就不要設定成public

Object在互相取得對方public的資料時，會透過interface來進行

![](https://i.imgur.com/OPBEMAr.png)

### Inheritance (繼承)
用一句話表示繼承，就是「站在巨人的肩膀上」

我們可以將原有class作為基礎，在這個基礎上新增class，這個新的class稱為子類別，而作為基礎的class則稱為父類別

父類別有的所有東西，Attritubes以及Methods，子類別都可以使用，且可在這些基礎之上定義一些擴充的東西，如下圖

![](https://i.imgur.com/MZhMFpG.png)

### Overriding
用一句比較難聽但是好記憶的方式來形容Overriding，ride代表騎，over代表超過，overriding就是「騎在你爸爸頭上」

overriding代表，在繼承的時候，如果子類別想要將父類別的某個method的行為做一些變更，則可以透過overriding的方式，取代父類別的method

要如何做，子類別只需新增一個跟父類別同名的method即可，程式在運作時，會優先使用子類別定義的method，而不會使用父類別的東西，可以看看下圖
 
![](https://i.imgur.com/OblhaEp.png)

懶學生是學生的子類別，而懶學生的走路、吃東西與睡覺的方式可能有異於一般的學生，這時候就可以將學生class的那些method override掉，變成自己定義的動作

## Class實作
接下來就直接來看要如何在JavaScript寫class

### 定義class
其實十分簡單，先來看看完整程式碼
```javascript
class Rabbit {
  constructor(type) {
    this.type = type;
  }
  speak(line) {
    console.log(`The ${this.type} rabbit says '${line}'`);
  }
}

let killerRabbit = new Rabbit("killer");
let blackRabbit = new Rabbit("black");
```

先來了解一下this到底是什麼，所謂的this指的是實例出來後的"那個"物件，例如killerRabbit是一個object，這時候this就是指killerRabbit本身，同樣的blackRabbit裡面的this也是指blackRabbit這個物件本身

接著看看內部結構，可拆成兩部分來看，constructor以及methods

* constructor
    * 這是一種特殊的method，會在class剛建立時執行一遍
        跑跑看這段程式碼，在新建出Apple物件時，constructor就會印出一段文字
```javascript
class Apple {
    constructor() {
    console.log("An apple a day keeps doctor away.");
    }
}

let a = new Apple();
```
        特別注意如果constructor有需要參數的話，在新建物件的時候，就要把給constructor的參數放入括號中，e.g. `let a = new Apple("Yummy")`

* methods
    * methods就是這個class的其他動作
        在剛剛的Apple當中加入run看看，並且去呼叫他
```javascript
class Apple {
    constructor() {
    console.log("An apple a day keeps doctor away.");
    }
    run() {
    console.log("Your apple keeps you away.");
    }
}

let a = new Apple();
a.run();
```

接著講講Attritube，目前JavaScript的Attritube只能定義在constructor或是method當中，沒有辦法定義在別的地方，以後可能會加入這個功能

### Inheritance
接著看看如何實作Inheritance
```javascript
class Apple {
    constructor() {
        console.log("You create an apple!");
    }
    run() {
        console.log("Your apple run away.");
    }
}

class PoisionApple extends Apple {
    constructor() {
        super();
        this.type = "Poision";
        console.log("This is a poision apple!");
    }
}

let a = new PoisionApple();
```
可以在定義class的後面加上extends代表這個class繼承自...
上面的例子PoisionApple是繼承自Apple的子類別

super()代表呼叫父類別的constructor，也就是初始化父類別的意思，要先進行初始化才能夠完全的使用父類別提供的東西，這個不加會出現錯誤

### Overriding
在剛剛寫的PoisionApple中定義一個跟Apple裡面一樣名稱的method
```javascript
// class Apple ...

class PoisionApple extends Apple {
    constructor() {
        super();
        this.type = "Poision";
        console.log("This is a poision apple!");
    }
    run() {
        console.log("Your apple runs away, and kill a potato with poision.");
    }

}

let a = new PoisionApple();
a.run();
```

這邊呼叫run的時候，可以發現印出的文字是PoisionApple定義的文字，而非Apple的，這就是Override

### Setter、Getter
Seeter與Getter可視為一種取得Object資料與設定Object資料的介面，方便其他人使用，使用方式為在method前面加上set或是get，看看這個例子

```javascript
class Apple {
    constructor() {
        this.first_name = "";
        this.last_name = "";
        console.log("You create an apple!");
    }
    run() {
        console.log("Your apple run away.");
    }

    get name() {
        return this.first_name + " " + this.last_name;
    }

    set name(str) {
        let temp = str.split(" ");
        this.first_name = temp[0];
        this.last_name = temp[1];
    }
}

let a = new Apple();
a.name = "John Doe";
console.log(a.first_name);
console.log(a.last_name);
console.log(a.name);
```

這個Object使用first_name以及last_name的方式儲存姓名這個資料，而使用者在設定時可以直接透過`object_name.first_name`或是`object.last_name`的方式分別設定這兩個資料

但是這有點麻煩，我們不能直接用全名去設定，所以寫了一個setter，使用者在設定時只需要使用全名進行設定，setter會自動幫我們做後續處理

再看看getter，透過getter我們可以直接獲取全名資料

### statics
來看看如何定義static的method
```javascript
class Apple {
    // ...
    static listAllSize() {
        return ["small", "medium", "big"];
    }   
}

console.log(Apple.listAllSize());
```
static可以讓你的method不需要實例化就能直接使用，之前的例子都是先有一個實例化後的object，然後去呼叫這個object裡面的method

但是上面的範例，我們沒有實例化任何object，而是直接用class的名稱去呼叫method，呼叫的這個method就是static的

要理解static就要先了解什麼是dynamic，這兩者是相對的。
所謂dynamic就是當object被建立時才load到記憶體中，而static則是一開始就load進記憶體了，所以才能直接用。

### instanceof
最後來看看`instanceof`這個operator，透過它我們可以確認某個object是不是由某個class產生的

如下例
```javascript
class Apple {
	// ...
}

class PoisionApple extends Apple {
	// ...
}

let a = new PoisionApple();
console.log(a instanceof PoisionApple);
// true
console.log(a instanceof Apple);
// true

let b = new Apple();
console.log(b instanceof PoisionApple);
// false
console.log(b instanceof Apple);
// true
```

可以看到a是PoisionApple的instance這沒有問題，但它同時也是Apple的實例，這是因為`instanceof`會將object也視為父類別的實例

而b則是從Apple實例化來的，因此不是PoisionApple的實例

## Prototype
在講Prototype之前，我必須告訴你一件事情，那就是你剛剛寫的那個其實不是class...
![](https://i.imgur.com/OPNRFnV.png)

JavaScript是沒有class這個設計的，你剛剛寫的那個class，其實是用一堆東西拼湊在一起跟class功能類似的東西

至於為什麼JavaScript沒有class這個設計，那是因為最初JavaScript的功能僅僅是用來作為表單驗證器而已，所以他老兄，這位Branden Eich
![](https://i.imgur.com/Y9CQYyu.png)
覺得沒有必要把JS設計得這麼複雜，於是就沒有設計class

但是重點來了，他老兄不想設計class，但是又想要有繼承的功能...這根本就是你不念書但又想考高分的感覺...
所以才有了prototype這個鬼玩意兒，接下來就看看到底prototype是啥，以及它是怎麼被用來實現繼承的。

### 所以什麼是prototype
首先，讓我們來跑跑看這段code
```javascript
let empty = {};
console.log(empty.toString);
console.log(empty.toString());
```
你會發現它完全可以跑，第一個print應該會跟你講toString這個property的資訊，第二行則是呼叫toString並印出回傳的結果。

但是問題來了，不覺得哪裡怪怪的嗎，明明我們就沒有在empty物件中定義任何東西，但為何卻憑空出現了toString?

這一切都是prototype的鍋XD

剛剛提到prototype是Eich他老兄為了實現繼承這個功能而做出來的東西，所以聰明如你應該猜到了，沒錯toString就是繼承來的! 
哪是從誰繼承來的呢? 這時候就要先來講prototype chain這個東西了

### Prototype Chain 原型鍊
這個東西，應該是很多學習JavaScript的人的噩夢，但我覺得用繼承的角度來看它，其實就不難理解

所謂原型鍊就是目前這個Object一路繼承下來的一連串物件，什麼意思呢? 先來看看這一條原型鍊
![](https://i.imgur.com/AVl7wcx.png)

所有的物件最頂端都會繼承Object.prototype這個物件，所以剛剛上面那個empty物件，其實是繼承了Object.prototype，而toString就是Object.prototype所帶的method

原型鍊就是，某個Object一路繼承下來的東西有哪些

為了證明我說的沒有騙你，可以來確認看看empty是否真的繼承自Object.prototype
```javascript
let empty = {};
console.log(Object.getPrototypeOf(empty) == Object.prototype);
```

如果想要知道Object.prototype這個東西到底提供了那些property，可以跑下面這段程式碼
```javascript
console.log(Object.getOwnPropertyNames(Object.prototype));
```

接著來看看當我們呼叫toString時到底發生了什麼事
![](https://i.imgur.com/2EiHBQq.png)

從這張圖可以看到，如果某個Object呼叫了一個property，JS會先從這個Object本身找起，看看它有沒有這個property，如果找不到便會往上找他的父Object，一路這樣找上去，直到找到為止，如果沒找到就會出錯誤

接下來看看更多的chain吧

#### Function
![](https://i.imgur.com/RHRzCXs.png)

上面這條是function的原型鍊，如果新建一個function，它會自動繼承Function.prototype，而Function.prototype則是繼承自Object.prototype

#### Array
![](https://i.imgur.com/kueTZDq.png)
這一條是Array的chain，新建的Array繼承自Array.prototype，這個物件提供了很多功能，包括push、pop、length...等等，而Array.protoype則繼承自Objec.prototype

由此可以看到，其實大部分的物件最頂端都是Object.prototype，而在上去是什麼呢? 答案是null

### 用自己的Object當作Prototype創建另一個Object
了解了原型鍊以後，我們來看看要怎麼把自己的object當作原型，生成其他的object

只需要用到這行程式即可`Object.create();`
來看看實際的例子
```javascript
let protoRabbit = {
    type: "none",
    speak: function(line) {
        console.log(`The ${this.type} rabbit says '${line}'`);
    }
};

let killerRabbit = Object.create(protoRabbit);
killerRabbit.type = "killer";
killerRabbit.speak("SKREEEE!");

let sleepyRabbit = Object.create(protoRabbit);
sleepyRabbit.type = "sleepy";
sleepyRabbit.speak("zzzzzzz");
```

這個範例中，我們寫了一個protoRabbit作為原型，從這個物件中，我們新建了兩個物件，分別是killerRabbit以及sleepyRabbit

這兩個物件都有type以及speak的屬性，而type裡面的value兩者不同，但是speak其實做的事情一模一樣

我們可以在上面那段程式下方，插入這段程式，跑一下來看看這個我們自己做的物件，原型鍊是否跟我上面描述的一樣
```javascript
// ...

console.log(Object.getPrototypeOf(killerRabbit) == protoRabbit);
console.log(Object.getPrototypeOf(protoRabbit) == Object.prototype);
```

應該可以發現這兩個印出結果都是true，看吧，我沒騙你XD

如果你想得夠多，你可能會問，如果我想要創建一個完全沒有繼承任何東西(包括Object.prototype)的一個Object，該怎麼做?
你可以這樣寫
```javascript
Object.create(null);
```
從null創建新的object就不會有繼承誰的問題了

## JavaScript如何實現Class
剛剛我上面講到，JS沒有class的設計，我們寫的class其實是用各種東西拼湊出來的，跟class功能很像的東西

所以具體來講到底是什麼跟什麼拼湊在一起的呢?
來跟我念一遍
JavaScript class = constructor function + prototype
直接看看程式碼
```javascript
// constructor function
function Rabbit(type) {
  console.log("You create a new Rabbit!");
  this.type = type;
}

// prototype property
Rabbit.prototype.speak = function(line) {
  console.log(`The ${this.type} rabbit says '${line}'`);
};

// create a new Rabbit object
let weirdRabbit = new Rabbit("weird");
```
以上就是JavaScript class的真面目，那為什麼我們可以用class這個關鍵字來定義class呢?
這是ES6才加入的功能，其實是一個語法糖，也就是說是設計來方便你定義class用的"捷徑"，寫起來好寫很多，但實際上它長的樣子是像上面這樣

### 他為什麼要這樣設計
上面的程式，可以看到我們定義了一個Function，然後用new function這樣的方式新建了一個物件，感覺十分神奇對吧，我們來看看他老兄到底在想什麼，怎麼會設計成這樣

首先，當時Java很火紅，Java在新增物件時，是透過`new Class_name();`這樣的方式，而他老兄看到人家透過new去新增物件，他也想要這樣的功能

但是問題來了，JS本來就沒有設計class阿，那是要new什麼?

他老兄給出的答案是，我們簡單一點，用function來new吧!

然後我內心OS:
![](https://i.imgur.com/lEIF8aH.png)

太神奇了Eich兄，原來還可以這樣玩阿

總之接下來就來講講到底是怎麼運作的

### JS的class細部講解
先看看這段程式碼
```javascript
function Dog(name) {
    this.name = name;
    this.type = "哈士奇";
    this.speak = function() {
        console.log(`我是${this.name}，我要吃罐頭`);
    }
}

let dogA = new Dog("Jack");
let dogB = new Dog("Dogy");

dogA.speak();
dogB.speak();
```
首先我們定義了一個function叫做Dog，一旦用`new function();`這種方式去呼叫function，就會被視為要新建物件，JS就會幫你透過這個function產生一個物件

function當中有看到this.xxx的部分，這些部分都會被是為新物件自己的property

所以dogA跟dogB都有了name、type以及speak這些property

這就是所謂的constructor function，可以對應到之前寫class裡面的那個construction() method

聰明如你，不知道有沒有發現一件事，speak這個東西，在每個物件做的事情都一樣，但是每個物件都有自己的一個speak，看看這段程式碼
```javascript
// ...

console.log(dogA.speak === dogB.speak);
```
可以發現每個物件的speak是不同的東西，雖然功能一樣，但是在記憶體中卻各自佔了各自的空間

這很浪費空間對吧，所以身為一個優秀的工程師，就必須解決這個問題

怎麼做? 答案是透過prototype來做
首先，每個function在被create的時候，都會自動新增一個prototype的property
```javascript
let foo = function() {
  return "nothing";
}

console.log(Object.getOwnPropertyNames(foo));
```
可以在上面的程式看到，一個新的function會被自動賦予很多個property，其中就有prototype
這個prototype是什麼呢，其實就是個空的object
```javascript
// ...

console.log(typeof(foo.prototype));
// object
console.log(foo.prototype);
// foo {}
```

這個prototype有什麼用? 為什麼我要講到它
因為當你new function時，JS會自動讓新的物件繼承這個prototype

而因為是從prototype繼承過來的，所以其實大家是共用同一個prototype，這樣就解決了重複多個相同property的問題了
所以上方程式碼可以這樣改寫，解決空間重複利用問題
```javascript
function Dog(name) {
    this.name = name;
    this.type = "哈士奇";
}

Dog.prototype.speak = function() {
    console.log(`我是${this.name}，我要吃罐頭`);
}

let dogA = new Dog("Jack");
let dogB = new Dog("Dogy");

console.log(Object.getPrototypeOf(dogA) === Dog.prototype);
console.log(Object.getPrototypeOf(dogB) === Dog.prototype);
console.log(dogA.speak === dogB.speak);
```

### 打完收工
所以再讓我們複習一次
JavaScript沒有class的設計，你寫的那個class是ES6提供的語法糖
真真正正的JavaScript要實現class，需要使用拼湊的方式，怎麼拼呢，就是用constructor function + prototype去拼
共用的東西(通常是一些method)放在prototype，不共用的屬性則放在constructor function中定義

這樣，你明白了嗎?

## Labs
這邊提供了幾個練習題，以及它們的解答，有興趣可以寫寫看，用實作來練習class的寫法

### Lab1 A Vector Type
* 題目
    寫一個二維向量的class，包含下面的property以及method
    * Properties
        * x
        * y
    * Methods
        * plus: 兩個向量相加
        * minus: 兩個向量相減
        * length: 取得向量的長度，這個要做成getter

* 解答
```javascript
class Vec {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }K

    plus(vec) {
        return new Vec(this.x + vec.x, this.y + vec.y);
    }

    minus(vec) {
        return new Vec(this.x - vec.x, this.y - vec.y);
    }

    get length() {
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }
}

// Your code here.

console.log(new Vec(1, 2).plus(new Vec(2, 3)));
// → Vec{x: 3, y: 5}
console.log(new Vec(1, 2).minus(new Vec(2, 3)));
// → Vec{x: -1, y: -1}
console.log(new Vec(3, 4).length);
// → 5
```

### Lab2 Borrowing A Method
* 題目
    之前我們使用過hasOwnProperty來檢查一個object當中有無某個property

    現在我們把hasOwnProperty override掉了，請把它修好
```javascript
let data = {one: true, two: true, hasOwnProperty: true};

// Fix this call
console.log(data.hasOwnProperty("one"));
console.log(data.hasOwnProperty("three"));
```

* 解答
```javascript
let data = {
    one: true,
    two: true,
    hasOwnProperty: function(str) {
        return Object.prototype.hasOwnProperty.call(this, str);
    }
}

console.log(data.hasOwnProperty("one"));
console.log(data.hasOwnProperty("three"));
```

### Lab3 Stack
* 題目
    製作一個stack的class，包含下面的property以及method
    * Properties
        * items: 一個array代表stack中的值
    * Methods
        * push
        * pop
        * peek: 印出最頂端的值
        * isEmpty: 這個stack是否為空
        * size: getter

* 解答
```javascript
class Stack {
    constructor() {
        this.items = [];
    }

    push(item) {
        this.items.push(item);
    } 

    pop() {
        return this.items.pop();
    }

    peek() {
        return this.items[this.items.length - 1];
    }

    get isEmpty() {
        if(this.items.length == 0) {
            return true;
        } else {
            return false;
        }
    }

    get size() {
        return this.items.length;
    }
}

let s = new Stack();
console.log(s.items);
// []
s.push(1);
s.push(2);
console.log(s.pop());
// 2
console.log(s.isEmpty);
// false
s.push("a");
s.push(true);
console.log(s.items);
// [1, 'a', true]
console.log(s.size);
// 3

```
