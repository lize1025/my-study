# JavaScript教程学习笔记    

## 项目介绍：  
本项目的开启纯粹为了记录个人学习js书籍时，对相关知识点的记录。方便随时查阅。并非js入门教程。   


* [1. 快速入门](#1)  
    * [1.1 字符串](#2)
    * [1.2 数组](#3)
    * [1.3 对象](#4)
    * [1.4 条件判断](#5)
    * [1.5 Map和Set](#6)
    * [1.6 iterable](#7)
* [2. 函数](#8)  
    * [2.1 函数定义和调用](#9)
    * [2.2 变量作用域与解构赋值](#10)
    * [2.3 方法](#11)
    * [2.4 高阶函数](#12)
    * [2.5 闭包](#13)
    * [2.6 箭头函数](#14)
    * [2.7 generator](#15)
* [3. 标准对象](#16)
    * [3.1 Date](#17)
    * [3.2 JSON](#18)
* [参考书籍](#100)

<h2 id="1">快速入门</h2>

<h3 id="2">字符串</h3>

**ES6**多行字符串用反引号 \`... \`表示：   
```
`这是一个      
 多行   
 字符串`   
```
模板字符串：  
```
var name = '小明';  
var age = 20;    
var message = '你好, ' + name + ', 你今年' + age + '岁了!';  
```
**ES6**模板字符串：  
`var message = 你好,${name},你今年${age}岁了`   

toUpperCase()把一个字符串全部变为大写：   
```
var s = 'Hello';
s.toUpperCase(); // 返回'HELLO'
```
toLowerCase()把一个字符串全部变为小写：   
```
var s = 'Hello';
var lower = s.toLowerCase(); // 返回'hello'并赋值给变量lower  
```   
indexOf()会搜索指定字符串出现的位置，也可操作数组：   
```
var s = 'hello, world';
s.indexOf('world'); // 返回7
s.indexOf('World'); // 没有找到指定的子串，返回-1
```   
substring()返回指定索引区间的子串：   
```
var s = 'hello, world'   
s.substring(0, 5); // 从索引0开始到5（不包括5），返回'hello'   
s.substring(7); // 从索引7开始到结束，返回'world'   
```   

<h3 id="3">数组</h3> 

slice()就是对应String的substring()版本，它截取Array的部分元素，然后返回一个新的Array   
```
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // ['A', 'B', 'C']
arr.slice(3); // ['D', 'E', 'F', 'G']
```  
如果不给slice()传递任何参数，它就会从头到尾截取所有元素。利用这一点，我们可以很容易地复制一个Array：   
```
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
var aCopy = arr.slice();
aCopy; // ['A', 'B', 'C', 'D', 'E', 'F', 'G']
aCopy === arr; // false
```  
push()向Array的末尾添加若干元素，pop()则把Array的最后一个元素删除掉：  
```
var arr = [1, 2];
arr.push('A', 'B'); // 返回Array新的长度: 4
arr; // [1, 2, 'A', 'B']
arr.pop(); // 返回'B'
arr; // [1, 2, 'A']
arr.pop(); arr.pop(); arr.pop(); // 连续pop 3次
arr; // []
arr.pop(); // 空数组继续pop不会报错，而是返回undefined
arr; // []
```   
如果要往Array的头部添加若干元素，使用unshift()方法，shift()方法则把Array的第一个元素删掉：   
```
var arr = [1, 2];
arr.unshift('A', 'B'); // 返回Array新的长度: 4
arr; // ['A', 'B', 1, 2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
arr; // []
arr.shift(); // undefined
arr; // []
```   
reverse()把整个Array的元素给掉个个，也就是反转：   
```
var arr = ['one', 'two', 'three'];
arr.reverse(); 
arr; // ['three', 'two', 'one']
```   
splice()方法是修改Array的“万能方法”，它可以从指定的索引开始删除若干元素，然后再从该位置添加若干元素：   
从索引2开始删除3个元素,然后再添加两个元素:
```
var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```
只删除,不添加:
```
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
```
只添加,不删除:
```
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```   
concat()方法把当前的Array和另一个Array连接起来，并返回一个新的Array：   
```
var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
arr; // ['A', 'B', 'C']
```
concat()方法可以接收任意个元素和Array，并且自动把Array拆开，然后全部添加到新的Array里：  
```
var arr = ['A', 'B', 'C'];
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
```   
join()方法，它把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串   
如果Array的元素不是字符串，将自动转换为字符串后再连接：   
```
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'
```   

<h3 id="4">对象</h3> 
访问属性是通过.操作符完成的，但这要求属性名必须是一个有效的变量名。如果属性名包含特殊字符，就必须用引号括起来：  

```
var xiaohong = {
    name: '小红',
    'middle-school': 'No.1 Middle School'
};

xiaohong['middle-school']; // 'No.1 Middle School'
xiaohong['name']; // '小红'
xiaohong.name; // '小红'  
```

检测xiaoming是否拥有某一属性，可以用in操作符。  
*注意：也有可能是小明继承得到的，要判断是否是自身的,用hasOwnProperty：*    

```
'name' in xiaoming; // true
xiaoming.hasOwnProperty('name'); // true
```  

<h3 id="5">条件判断</h3>
js把null、undefined、0、NaN和空字符串''视为false，其他值一概视为true   

for循环的3个条件都是可以省略的，如果没有退出循环的判断条件，就必须使用break语句退出循环，否则就是死循环：   

```
var x = 0;
for (;;) { // 将无限循环下去
    if (x > 100) {
        break; // 通过if判断来退出循环
    }
    x++;
}
```  

<h3 id="6">Map和Set</h3>  
**ES6**新数据类型  
Map是一组键值对的结构，具有极快的查找速度。  
*注意：由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉*    

```
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
m.get('Michael'); // 95  
```   

```
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.set('Bob', 59);
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam' 返回 true
m.get('Adam'); // undefined
```      

Set和Map类似，也是一组key的集合，但不存储value。  
要创建一个Set，需要提供一个Array作为输入，或者直接创建一个空Set：  

```
var s1 = new Set(); // 空Set
var s2 = new Set([1, 2, 3]); // 含1, 2, 3
```     

重复元素在Set中自动被过滤：    

```
var s = new Set([1, 2, 3, 3, '3']);
s; // Set {1, 2, 3, "3"}
```   

通过add(key)方法可以添加元素到Set中，可以重复添加，但不会有效果：    

```
s.add(4);
s; // Set {1, 2, 3,"3", 4}
s.add(4);
s; // 仍然是 Set {1, 2, 3, 4}
```   

通过delete(key)方法可以删除元素：   

```
var s = new Set([1, 2, 3]);
s.delete(3);
s; // Set {1, 2}
```  

new Set()数组去重：   

```
function dedupe(array) {
    return Array.from(new Set(array)); //Array.from可以将set结构转为数组；
}
dedupe([1,1,2,3])  // [1, 2, 3]
```   

<h3 id="7">iterable</h3> 
遍历Array可以采用下标循环，遍历Map和Set就无法使用下标。  

为了统一集合类型，**ES6** 标准引入了新的iterable类型，Array、Map和Set都属于iterable类型。    

具有iterable类型的集合可以通过新的for ... of循环来遍历.for ... of循环是 **ES6** 引入的新的语法    

```
var a = ['A', 'B', 'C'];
var s = new Set(['A', 'B', 'C']);
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);

for (var x of a) { // 遍历Array
    console.log(x);
}
for (var x of s) { // 遍历Set
    console.log(x);
}
for (var x of m) { // 遍历Map
    console.log(x[1] + '=' + x[0]);
}
```   

for ... in循环由于历史遗留问题，它遍历的实际上是对象的属性名称。   
一个Array数组实际上也是一个对象，它的每个元素的索引被视为一个属性。   
当我们手动给Array对象添加了额外的属性后，for ... in循环将带来意想不到的意外效果：   

```  
var a = ['A', 'B', 'C'];

//for ... in循环将把name包括在内，但Array的length属性却不包括在内。
a.name = 'Hello';
for (var x in a) {
    console.log(x); // '0', '1', '2', 'name'
}
a.length //3

//for ... of它只循环集合本身的元素：
for (var y of a) {
    console.log(y); // 'A', 'B', 'C'
}
y.length //3
```   

然而，更好的方式是直接使用iterable内置的forEach方法。  
它接收一个函数，每次迭代就自动回调该函数。以Array为例：  

```
var a = ['A', 'B', 'C'];
a.forEach(function (element, index, array) {
    // element: 指向当前元素的值
    // index: 指向当前索引
    // array: 指向Array对象本身
    console.log(element + ', index = ' + index);
});
```   

*注意:forEach()方法是ES5.1标准引入的。*  

JavaScript的函数调用不要求参数必须一致，因此可以忽略它们    

```
var a = ['A', 'B', 'C'];
a.forEach(function (element) {
    console.log(element);
});
```  

Map的回调函数参数依次为value、key和map本身：    

```
var m = new Map([[1, 'x'], [2, 'y'], [3, 'z']]);
m.forEach(function (value, key, map) {
    console.log(value);
});
```    

Set与Array类似，但Set没有索引，因此回调函数的前两个参数都是元素本身：   

```
var s = new Set(['A', 'B', 'C']);
s.forEach(function (element, sameElement, set) {
    console.log(element);
});
```   

<h2 id="8">函数</h2>   

<h3 id="9">函数定义和调用</h3>   

js的函数也是一个对象。   
下边要有分号，表示赋值结束:   
var abs = function(x){return x};   
函数传入的参数多或者少也没有问题    

arguments，它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。arguments类似Array但它不是一个Array
最常用于判断传入参数的个数    

ES6标准引入了rest参数：   

```
function foo(a, b, ...rest) {
    console.log('a = ' + a);
    console.log('b = ' + b);
    console.log(rest);
}

foo(1, 2, 3, 4, 5);
// 结果:
// a = 1
// b = 2
// Array [ 3, 4, 5 ]

foo(1);
// a = 1
// b = undefined
// Array []
```   

rest参数只能写在最后，前面用...标识，从运行结果可知，传入的参数先绑定a、b，多余的参数以数组形式交给变量rest。    
所以，不再需要arguments我们就获取了全部参数。    
*注意：return语句，由于js引擎在行末自动添加分号的机制，return不要单独一行。*    

<h3 id="10">变量作用域与解构赋值</h3> 

JavaScript的函数在查找变量时从自身函数定义开始，从“内”向“外”查找。   

如果内部函数定义了与外部函数重名的变量，则内部函数的变量将“屏蔽”外部函数的变量。    
JavaScript引擎自动提升了变量y的声明，但不会提升变量y的赋值。      

```
function foo() {
    var x = 'Hello, ' + y;
    console.log(x);
    var y = 'Bob';
}

foo(); // Hello, undefined
```   
JavaScript默认有一个全局对象window，全局作用域的变量实际上被绑定到window的一个属性：   

```
var course = 'Learn JavaScript';
alert(course); // 'Learn JavaScript'
alert(window.course); // 'Learn JavaScript'
```    

全局变量会绑定到window上，不同的JavaScript文件如果使用了相同的全局变量，或者定义了相同名字的顶层函数，都会造成命名冲突。     
减少冲突的一个方法是把自己的所有变量和函数全部绑定到一个全局变量中。     
把自己的代码全部放入唯一的名字空间MYAPP中，会大大减少全局变量冲突的可能。     
许多著名的JavaScript库都是这么干的：jQuery，YUI，underscore等等。     

```
// 唯一的全局变量MYAPP:
var MYAPP = {};

// 其他变量:
MYAPP.name = 'myapp';
MYAPP.version = 1.0;

// 其他函数:
MYAPP.foo = function () {
    return 'foo';
};
```     

局部作用域：由于JavaScript的变量作用域实际上是函数内部，我们在for循环等语句块中是无法定义具有局部作用域的变量的：  

```
function foo() {
    for (var i=0; i<100; i++) {
            //
        }
    i += 100; // 仍然可以引用变量i
}
```    

为了解决块级作用域，**ES6**引入了新的关键字let，用let替代var可以申明一个块级作用域的变量：    

```
function foo() {
    var sum = 0;
        for (let i=0; i<100; i++) {
            sum += i;
         }
    // SyntaxError:
    i += 1;
}
```     
常量：   

如果要申明一个常量，通常用全部大写的变量来表示“这是一个常量，不要修改它的值”   
**ES6**标准引入了新的关键字const来定义常量，const与let都具有块级作用域：   

```
const PI = 3.14;
PI = 3; // 某些浏览器不报错，但是无效果！
PI; // 3.14
```    

解构赋值：    

从 **ES6** 开始，JavaScript引入了解构赋值，可以同时对一组变量进行赋值。  
   
```
var [x, y, z] = ['hello', 'JavaScript', 'ES6']; //相当于↓:     
var x = hello, y = JavaScript, z = ES6  
```   

```
let [x, [y, z]] = ['hello', ['JavaScript', 'ES6']];
x; // 'hello'
y; // 'JavaScript'
z; // 'ES6'
```   

```
let [, , z] = ['hello', 'JavaScript', 'ES']; // 忽略前两个元素，只对z赋值第三个元素
z; // 'ES'
```     
  
```  
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school'
};

var {name, age, passport} = person;  
// name, age, passport分别被赋值为对应属性:

console.log('name = ' + name + ', age = ' + age + ', passport = ' + passport);
// name = 小明, age = 20, passport = G-12345678
```     

对一个对象进行解构赋值时，同样可以直接对嵌套的对象属性进行赋值，只要保证对应的层次是一致的：    
*注意: address不是变量，而是为了让city和zip获得嵌套的address对象的属性*

```
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school',
    address: {
        city: 'Beijing',
        street: 'No.1 Road',
        zipcode: '100001'
    }
};

var {name, address: {city, zip}} = person;

name; // '小明'
city; // 'Beijing'
zip; // undefined, 因为属性名是zipcode而不是zip
address; // Uncaught ReferenceError: address is not defined
```     

如果要使用的变量名和属性名不一致，可以用下面的语法获取：     

```
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678',
    school: 'No.4 middle school'
};

// 把passport属性赋值给变量id:
let {name, passport:id} = person;
name; // '小明'
id; // 'G-12345678'
// 注意: passport不是变量，而是为了让变量id获得passport属性:
passport; // Uncaught ReferenceError: passport is not defined   
```    

解构赋值还可以使用默认值，这样就避免了不存在的属性返回undefined的问题：    

```
var person = {
    name: '小明',
    age: 20,
    gender: 'male',
    passport: 'G-12345678'
};

// 如果person对象没有single属性，默认赋值为true:
var {name, single=true} = person;
name; // '小明'
single; // true
```    

有些时候，如果变量已经被声明了，再次赋值的时候，正确的写法也会报语法错误：    

```
// 声明变量:
var x, y;
{x, y} = { name: '小明', x: 100, y: 200};
// 语法错误: Uncaught SyntaxError: Unexpected token =
```    

这是因为JavaScript引擎把{开头的语句当作了块处理，于是=不再合法。解决方法是用小括号括起来：     
`({x, y} = { name: '小明', x: 100, y: 200});`     

解构赋值在很多时候可以大大简化代码。例如，交换两个变量x和y的值，可以这么写，不再需要临时变量：   

```
var x=1, y=2;
[x, y] = [y, x]
```    

快速获取当前页面的域名和路径：     
`var {hostname:domain, pathname:path} = location;`     

<h3 id="11">方法</h3>     

在一个对象中绑定函数，称为这个对象的方法。     

```
var xiaoming = {
    name: '小明',
    birth: 1990,
    age: function () {
        var y = new Date().getFullYear();
        return y - this.birth;
    }
};

xiaoming.age; // function xiaoming.age()
xiaoming.age(); // 今年调用是28,明年调用就变成29了
```   

apply:   

要指定函数的this指向哪个对象，可以用函数本身的apply方法。     
它接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是Array，表示函数本身的参数。    

```
function getAge() {
    var y = new Date().getFullYear();
    return y - this.birth;
}

var xiaoming = {
    name: '小明',
    birth: 1990,
    age: getAge
};

xiaoming.age(); // 28
getAge.apply(xiaoming, []); // 28, this指向xiaoming, 参数为空    
```   

另一个与apply()类似的方法是call()，唯一区别是：     
apply()把参数打包成Array再传入。        
call()把参数按顺序传入。      

比如调用Math.max(3, 5, 4)，分别用apply()和call()实现如下：    
*对普通函数调用，我们通常把this绑定为null。*

```
Math.max.apply(null, [3, 5, 4]); // 5
Math.max.call(null, 3, 5, 4); // 5
```    

<h3 id="12">高阶函数</h3>

map()方法定义在JavaScript的Array中：   

```
function pow(x) {
    return x * x;
}
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
var results = arr.map(pow); // [1, 4, 9, 16, 25, 36, 49, 64, 81]
```    

```
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
arr.map(String); // ['1', '2', '3', '4', '5', '6', '7', '8', '9']
```    

reduce()把结果继续和序列的下一个元素做累积计算   

```
var arr = [1, 3, 5, 7, 9];
arr.reduce(function (x, y) {
    return x + y;
}); // 25
```   

```
var arr = [1, 3, 5, 7, 9];
arr.reduce(function (x, y) {
    return x * 10 + y;
}); // 13579
```   

filter() 用于把Array的某些元素过滤掉，然后返回剩下的元素。    

删掉偶数，只保留奇数，可以这么写：    

```
var arr = [1, 2, 4, 5, 6, 9, 10, 15];
var r = arr.filter(function (x) {
    return x % 2 !== 0;
});
r; // [1, 5, 9, 15]
```    

把一个Array中的空字符串删掉，可以这么写：     

```
var arr = ['A', '', 'B', null, undefined, 'C', '  '];
var r = arr.filter(function (s) {
    return s && s.trim(); // 注意：IE9以下的版本没有trim()方法
});
r; // ['A', 'B', 'C']
```   

filter()接收的回调函数，其实可以有多个参数。通常我们仅使用第一个参数，表示Array的某个元素。      
回调函数还可以接收另外两个参数，表示元素的位置和数组本身：     

用filter()数组去重：    

```
var r,arr = ['apple', 'strawberry', 'banana', 'pear', 'apple', 'orange', 'orange', 'strawberry'];
r = arr.filter(function (element, index, self) {
    return self.indexOf(element) === index;
});
```    

<h3 id="13">闭包</h3>

函数作为返回值：    
高阶函数除了可以接受函数作为参数外，还可以把函数作为结果值返回。     

```
function lazy_sum(arr) {
    var sum = function () {
        return arr.reduce(function (x, y) {
            return x + y;
        });
    }
    return sum;
}
```    

当我们调用lazy_sum()时，返回的并不是求和结果，而是求和函数：    

`var f = lazy_sum([1, 2, 3, 4, 5]); // function sum()`    

调用函数f时，才真正计算求和的结果：    

`f(); // 15`     

*在这个例子中，我们在函数lazy_sum中又定义了函数sum，并且，内部函数sum可以引用外部函数lazy_sum的参数和局部变量。     
当lazy_sum返回函数sum时，相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）”的程序结构拥有极大的威力。*    

当我们调用lazy_sum()时，每次调用都会返回一个新的函数，即使传入相同的参数：    

```
var f1 = lazy_sum([1, 2, 3, 4, 5]);
var f2 = lazy_sum([1, 2, 3, 4, 5]);
f1 === f2; // false
```    
   
下面的例子，每次循环，都创建了一个新的函数，然后，把创建的3个函数都添加到一个Array中返回了。    
返回的函数引用了变量i，但它并非立刻执行。等到3个函数都返回时，它们所引用的变量i已经变成了4，因此最终结果为16  

```
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push(function () {
            return i * i;
        });
    }
    return arr;
}

var results = count();
var f1 = results[0];
var f2 = results[1];
var f3 = results[2];
```    

返回闭包时要引用循环变量，或者后续会发生变化的变量:      
方法是再创建一个函数，用该函数的参数绑定循环变量当前的值，无论该循环变量后续如何更改，已绑定到函数参数的值不变：       

```
function count() {
    var arr = [];
    for (var i=1; i<=3; i++) {
        arr.push((function (n) {
            return function () {
                return n * n;
            }
        })(i));
    }
    return arr;
}

var results = count();
var f1 = results[0];
var f2 = results[1];
var f3 = results[2];

f1(); // 1
f2(); // 4
f3(); // 9
```     

注意这里用了一个“创建一个匿名函数并立刻执行”的语法：    

```
(function (x) {
    return x * x;
})(3); // 9
```     

闭包可以封装一个私有变量:    

```
function create_counter(initial) {
    var x = initial || 0;
    return {
        inc: function () {
            x += 1;
            return x;
        }
    }
}

var c1 = create_counter();
c1.inc(); // 1
c1.inc(); // 2
c1.inc(); // 3

var c2 = create_counter(10);
c2.inc(); // 11
c2.inc(); // 12
c2.inc(); // 13
```   

闭包还可以把多参数的函数变成单参数的函数。    
计算xy可以用Math.pow(x, y)函数，考虑到经常计算x2或x3。可以利用闭包创建新的函数pow2和pow3：    
返回x的n次幂：    

```
function make_pow(n) {
    return function (x) {
        return Math.pow(x, n);
    }
}
// 创建两个新函数:
var pow2 = make_pow(2);
var pow3 = make_pow(3);

console.log(pow2(5)); // 25
console.log(pow3(7)); // 343
```   

<h3 id="14">箭头函数</h3>    

**ES6**标准新增了一种新的函数：Arrow Function（箭头函数）。   
```
x => x * x  //相当于↓
function (x) {
    return x * x;
}
```   

箭头函数相当于匿名函数，并且简化了函数定义。    
箭头函数有两种格式，一种像上面的，只包含一个表达式，连{ ... }和return都省略掉了。
还有一种可以包含多条语句，这时候就不能省略{ ... }和return：    

```
x => {
    if (x > 0) {
        return x * x;
    }
    else {
        return - x * x;
    }
}
```   

两个参数:    
`(x, y) => x * x + y * y`

无参数:   
`() => 3.14`

可变参数:       

```
(x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}
```    

如果要返回一个对象，就要注意：    
`x => ({ foo: x })`   

箭头函数看上去是匿名函数的一种简写，但实际上，箭头函数和匿名函数有个明显的区别：箭头函数内部的this是词法作用域，由上下文确定:   

```
var obj = {
    birth: 1990,
    getAge: function () {
        var b = this.birth; // 1990
        var fn = () => new Date().getFullYear() - this.birth; // this指向obj对象
        return fn();
    }
};
obj.getAge(); // 25
```    

如果使用箭头函数，以前的那种hack写法就不需要了：   
`var that = this;`    

由于this在箭头函数中已经按照词法作用域绑定了，所以，用call()或者apply()调用箭头函数时，无法对this进行绑定，即传入的第一个参数被忽略：    

```
var obj = {
    birth: 1990,
    getAge: function (year) {
        var b = this.birth; // 1990
        var fn = (y) => y - this.birth; // this.birth仍是1990
        return fn.call({birth:2000}, year);
    }
};
obj.getAge(2018); // 28
```

<h3 id="15">generator</h3>

generator（生成器）是 **ES6** 标准引入的新的数据类型。一个generator看上去像一个函数，但可以返回多次：    
generator和函数不同的是，generator由function*定义（注意多出的*号），并且，除了return语句，还可以用yield返回多次。    

要编写一个产生斐波那契数列的函数，可以这么写：    

```
function fib(max) {
    var
        t,
        a = 0,
        b = 1,
        arr = [0, 1];
    while (arr.length < max) {
        [a, b] = [b, a + b];
        arr.push(b);
    }
    return arr;
}

fib(5); // [0, 1, 1, 2, 3]
fib(10); // [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
```    

函数只能返回一次，所以必须返回一个Array。但是，如果换成generator，就可以一次返回一个数，不断返回多次   

```
function* fib(max) {
    var
        t,
        a = 0,
        b = 1,
        n = 0;
    while (n < max) {
        yield a;
        [a, b] = [b, a + b];
        n ++;
    }
    return;
}
```   

直接调用一个generator和调用函数不一样，fib(5)仅仅是创建了一个generator对象，还没有去执行它。   
调用generator对象有两个方法，第一个方法是不断地调用generator对象的next()方法：   

```
var f = fib(5);
f.next(); // {value: 0, done: false}
f.next(); // {value: 1, done: false}
f.next(); // {value: 1, done: false}
f.next(); // {value: 2, done: false}
f.next(); // {value: 3, done: false}
f.next(); // {value: undefined, done: true}
```   

第二个方法是直接用for ... of循环迭代generator对象，这种方式不需要我们自己判断done：    

```
for (var x of fib(10)) {
    console.log(x); // 依次输出0, 1, 1, 2, 3, ...
}
```   

有了generator的美好时代，用AJAX时可以这么写：    

```
try {
    r1 = yield ajax('http://url-1', data1);
    r2 = yield ajax('http://url-2', data2);
    r3 = yield ajax('http://url-3', data3);
    success(r3);
}
catch (err) {
    handle(err);
}
```   

<h2 id="16">标准对象</h2>   

typeof操作符获取对象的类型，它总是返回一个字符串：   

```
typeof NaN // 'number'
typeof undefined // 'undefined'
typeof Math.abs // 'function'
typeof null // 'object'
typeof [] // 'object'
typeof true; // 'boolean'
```   

number、boolean和string都有包装对象。在JavaScript中，字符串也区分string类型和它的包装类型。包装对象用new创建：   
虽然包装对象看上去和原来的值一模一样，显示出来也是一模一样，但他们的类型已经变为object了   

```
var n = new Number(123); // 123,生成了新的包装类型
var b = new Boolean(true); // true,生成了新的包装类型
var s = new String('str'); // 'str',生成了新的包装类型
```   

不要使用new Number()、new Boolean()、new String()创建包装对象；  

用parseInt()或parseFloat()来转换任意类型到number；   

用String()来转换任意类型到string，或者直接调用某个对象的toString()方法；   

通常不必把任意类型转换为boolean再判断，因为可以直接写if (myVar) {...}；   

typeof操作符可以判断出number、boolean、string、function和undefined；   
 
判断Array要使用Array.isArray(arr)；   

判断null请使用myVar === null；   

判断某个全局变量是否存在用typeof window.myVar === 'undefined'；   

函数内部判断某个变量是否存在用typeof myVar === 'undefined'。   

null和undefined没有toString()方法   

遇到这种情况，要特殊处理一下：   

```
123..toString(); // '123', 注意是两个点！
(123).toString(); // '123'
```   

<h3 id="17">Date</h3>   

获取系统当前时间，用：   
  
```  
var now = new Date();
now; // Wed Jun 24 2015 19:49:22 GMT+0800 (CST)
now.getFullYear(); // 2018, 年份
now.getMonth(); // 8, 月份，注意月份范围是0~11，5表示六月
now.getDate(); // 1, 表示24号
now.getDay(); // 3, 表示星期三
now.getHours(); // 19, 24小时制
now.getMinutes(); // 49, 分钟
now.getSeconds(); // 22, 秒
now.getMilliseconds(); // 875, 毫秒数
now.getTime(); // 1435146562875, 以number形式表示的时间戳
```   

创建一个指定日期和时间的Date对象，可以用：   

```
var d = new Date(2018, 8, 1, 20, 15, 30, 123);
d; // Sat Sep 01 2018 20:15:30 GMT+0800 (中国标准时间)
```   
*JavaScript的月份范围用整数表示是0~11，0表示一月，1表示二月……，所以要表示9月，我们传入的是8*

创建一个指定日期和时间的方法是解析一个符合ISO 8601格式的字符串：    

```
var d = Date.parse('2015-06-24T19:49:22.875+08:00');
d; // 1435146562875
```     

但它返回的不是Date对象，而是一个时间戳。不过有时间戳就可以很容易地把它转换为一个Date：   

```
var d = new Date(1535794965416);
d; // Sat Sep 01 2018 17:42:45 GMT+0800 (中国标准时间)
d.getMonth(); // 8
```   

*使用Date.parse()时传入的字符串使用实际月份01~12，转换为Date对象后getMonth()获取的月份值为0~11。*   

获取当前时间戳:   

```
if (Date.now) {
    console.log(Date.now()); // 老版本IE没有now()方法
} else {
    console.log(new Date().getTime());
}
```   

<h3 id="18">JSON</h3>    

JSON定死了字符集必须是UTF-8，为了统一解析，JSON的字符串规定必须用双引号""，Object的键也必须用双引号""   

JSON.stringify()序列化：          
把小明这个对象序列化成JSON格式的字符串   

```
var xiaoming = {
    name: '小明',
    age: 14,
    gender: true,
    height: 1.65,
    grade: null,
    'middle-school': '\"W3C\" Middle School',
    skills: ['JavaScript', 'Java', 'Python', 'Lisp']
};
var s = JSON.stringify(xiaoming);
console.log(s);
//{"name":"小明","age":14,"gender":true,"height":1.65,"grade":null,"middle-school":"\"W3C\" Middle School","skills":["JavaScript","Java","Python","Lisp"]}
```   

第二个参数用于控制如何筛选对象的键值，如果我们只想输出指定的属性，可以传入Array   
要输出得好看一些，可以加上参数，按缩进输出:    

`JSON.stringify(xiaoming, ['name', 'skills'], '  ');`   

还可以传入一个函数，这样对象的每个键值对都会被函数先处理：    

```
function convert(key, value) {
    if (typeof value === 'string') {
        return value.toUpperCase();
    }
    return value;
}

JSON.stringify(xiaoming, convert, '  ');
```   

如果我们还想要精确控制如何序列化小明，可以给xiaoming定义一个toJSON()的方法，直接返回JSON应该序列化的数据：    

```
var xiaoming = {
    name: '小明',
    age: 14,
    gender: true,
    height: 1.65,
    grade: null,
    'middle-school': '\"W3C\" Middle School',
    skills: ['JavaScript', 'Java', 'Python', 'Lisp'],
    toJSON: function () {
        return { // 只输出name和age，并且改变了key：
            'Name': this.name,
            'Age': this.age
        };
    }
};
JSON.stringify(xiaoming); // '{"Name":"小明","Age":14}'
```   

JSON.parse() 反序列化:    

拿到一个JSON格式的字符串，我们直接用JSON.parse()把它变成一个JavaScript对象： 

```
JSON.parse('[1,2,3,true]'); // [1, 2, 3, true]
JSON.parse('{"name":"小明","age":14}'); // Object {name: '小明', age: 14}
JSON.parse('true'); // true
JSON.parse('123.45'); // 123.45
```   

JSON.parse()还可以接收一个函数，用来转换解析出的属性：    

```
var obj = JSON.parse('{"name":"小明","age":14}', function (key, value) {
    if (key === 'name') {
        return value + '同学';
    }
    return value;
});
console.log(JSON.stringify(obj)); // {name: '小明同学', age: 14}
```   

<h3 id="100">参考书籍</h3>   

[廖雪峰官网教程](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434499763408e24c210985d34edcabbca944b4239e20000)   

[JavaScript高级程序设计](http://www.wrox.com)     

[ES6标准入门](https://github.com/ruanyf/es6tutorial)    

