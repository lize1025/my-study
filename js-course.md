# JavaScript教程学习笔记    

## 项目介绍：  
本项目的开启纯粹为了记录个人学习js书籍时，对相关知识点的记录。方便随时查阅。并非js入门教程。   


* [1. 快速入门](#1)
    * [1.1 let和const命令](#new1)  
    * [1.2 字符串](#2)
    * [1.3 数组](#3)
    * [1.4 对象](#4)
    * [1.5 条件判断](#5)
    * [1.6 Map和Set](#6)
    * [1.7 iterable](#7)
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
* [4. 面向对象编程](#19)
    * [4.1 创建对象和原型继承](#20)
    * [4.2 class继承](#21)
* [5. 浏览器](#22)
    * [5.1 浏览器对象](#23)
    * [5.2 操作DOM](#24)
    * [5.3 操作表单和文件](#25)
    * [5.4 AJAX](#26)
    * [5.5 Promise](#27)
    * [5.6 Canvas](#28)
* [6. jQuery](#29)
    * [6.1 $.ajax()](#30)
    * [6.2 编写jQuery插件](#31)
* [7. 错误处理](#32)
* [参考书籍](#100)

<h2 id="1">快速入门</h2>   

<h3 id="new1">let和const命令</h3>

**ES6**新增了let命令，所有声明的变量只在let命令所在的代码块内有效：   

```
{
    let a = 10;
    var b = 1;
}
a // ReferenceError: a is not defined
b // 1
```   
for循环的计数器就很适合let:    

```
var a = [];
for( let i = 0;i < 10; i++ ){
    a[i] = function (){
        console.log(i);
    }
}
a[6]() //6
```   

let和const不存在变量提升：   
```
console.log(foo); // undefined
var foo = 2;
```  
```
console.log(foo); // 报错
let foo = 2;
```     

变量要在声明后使用。x默认值为y，此时y还没有声明，属于死区：   

```
function bar(x=y,y=2){
    return [x,y];
}

bar() // y is not defined
```   

var变量提升导致内层的tmp变量覆盖了外层的tmp变量：       
  
```
var tmp = new Date();
function f(){
    console.log(tmp);
    if(false){
        var tmp = 'hello'
    }
}
f() //undefined
```   

let实际上为js新增了块级作用域：   
*块级作用域的出现，使立即执行函数不再必要了*     

```
function f1(){
    let n = 5;
    if( true ){
        let n = 10;
    }
    console.log(n)
}
f1() //5
```   

const声明一个只读常量，声明就不能改变：    

```
const PI = 3.1415;
PI //3.1415
PI = 3 // 报错
```   

const声明就要立即初始化，不能留到后边赋值:       

`const foo; // 报错`    

const实际上保证的并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。        
对于复合类型(主要是对象和数组)而言,变量指向的内存地址保存的只是一个指针。    
const保证指针固定，至于它指向的数据结构是不是可变，完全不能控制：   

```
const foo = {};

//为foo添加一个属性，可以成功
foo.prop = 123;
foo.prop // 123

//将foo指向另一个对象，就会报错
foo = {} 
```   

```
const a = [];
a.push('hello') // 可执行
a.length = 0 // 可执行
a = ['Dave'] // 报错
```     

**ES6**声明变量六种方法：使用var命令、function命令、let命令、const命令、import命令、class命令    

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

*使用Date.parse()时传入的字符串使用实际月份01-12，转换为Date对象后getMonth()获取的月份值为0-11。*   

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

<h2 id="19">面向对象编程</h2>   

<h3 id="20">创建对象和原型继承</h3>   

javaScript对每个创建的对象都会设置一个原型，指向它的原型对象。   

当我们用obj.xxx访问一个对象的属性时，js引擎先在当前对象上查找该属性，如果没有找到，就到其原型对象上找。    
如果还没有找到，就一直上溯到Object.prototype对象，最后，如果还没有找到，就只能返回undefined。   

如，创建一个Array对象：    
`var arr = [1, 2, 3];`   

其原型链是：    
arr ----> Array.prototype ----> Object.prototype ----> null    
Array.prototype定义了indexOf()、shift()等方法，因此你可以在所有的Array对象上直接调用这些方法。    

当我们创建一个函数时：   
```
function foo() {
    return 0;
}
```     

函数也是一个对象，它的原型链是：   
foo ----> Function.prototype ----> Object.prototype ----> null    
由于Function.prototype定义了apply()等方法，因此，所有函数都可以调用apply()方法。    

构造函数   

除了直接用{ ... }创建一个对象外，JavaScript还可以用一种构造函数的方法来创建对象。它的用法是，先定义一个构造函数：    

```
function Student(name) {
    this.name = name;
    this.hello = function () {
        alert('Hello, ' + this.name + '!');
    }
}

var xiaoming = new Student('小明');
xiaoming.name; // '小明'
xiaoming.hello(); // Hello, 小明!
```    

关键字new来调用这个函数，并返回一个对象，如果不写new，这就是一个普通函数，它返回undefined。   
如果写了new，它就变成了一个构造函数，它绑定的this指向新创建的对象，并默认返回this，也就是说，不需要在最后写return this;     

新创建的xiaoming的原型链是：   
xiaoming ----> Student.prototype ----> Object.prototype ----> null   

也就是说，xiaoming的原型指向函数Student的原型。如果你又创建了xiaohong、xiaojun，那么这些对象的原型与xiaoming是一样的：    

xiaoming ↘    
xiaohong -→ Student.prototype ----> Object.prototype ----> null    
xiaojun  ↗    

用new Student()创建的对象还从原型上获得了一个constructor属性，它指向函数Student本身：    

xiaoming.constructor === Student.prototype.constructor; // true   
Student.prototype.constructor === Student; // true   
Object.getPrototypeOf(xiaoming) === Student.prototype; // true   
xiaoming instanceof Student; // true   

函数Student恰好有个属性prototype指向xiaoming、xiaohong的原型对象，        
但是xiaoming、xiaohong这些对象可没有prototype这个属性。不过可以用__proto__这个非标准用法来查看。    
现在我们就认为xiaoming、xiaohong这些对象“继承”自Student      

xiaoming和xiaohong各自的name不同，这是对的，否则我们无法区分谁是谁了。   
xiaoming和xiaohong各自的hello是一个函数，但它们是两个不同的函数，虽然函数名称和代码都是相同的   

要让创建的对象共享一个hello函数：     
根据对象的属性查找原则，我们只要把hello函数移动到xiaoming、xiaohong这些对象共同的原型上就可以了，也就是Student.prototype     

```
function Student(name) {
    this.name = name;
}
Student.prototype.hello = function () {
    alert('Hello, ' + this.name + '!');
};
```      

最后，我们还可以编写一个createStudent()函数，在内部封装所有的new操作。一个常用的编程模式像这样：    

```
function Student(props) {
    this.name = props.name || '匿名'; // 默认值为'匿名'
    this.grade = props.grade || 1; // 默认值为1
}

Student.prototype.hello = function () {
    alert('Hello, ' + this.name + '!');
};

function createStudent(props) {
    return new Student(props || {})
}
// 这个createStudent()函数有几个巨大的优点：一是不需要new来调用，二是参数非常灵活，可以不传，也可以这么传：

var xiaoming = createStudent({
    name: '小明'
});

xiaoming.grade; // 1
```    

现在，我们要基于Student扩展出PrimaryStudent，可以先定义出PrimaryStudent：   

```
function PrimaryStudent(props) {
    // 调用Student构造函数，绑定this变量:
    Student.call(this, props);
    this.grade = props.grade || 1;
}
```   

但是，调用了Student构造函数不等于继承了Student，PrimaryStudent创建的对象的原型是：   
`new PrimaryStudent() ----> PrimaryStudent.prototype ----> Object.prototype ----> null`   

必须想办法把原型链修改为：   
`new PrimaryStudent() ----> PrimaryStudent.prototype ----> Student.prototype ----> Object.prototype ----> null`   

这样，原型链对了，继承关系就对了。   
新的基于PrimaryStudent创建的对象不但能调用PrimaryStudent.prototype定义的方法，也可以调用Student.prototype定义的方法。    

我们必须借助一个中间对象来实现正确的原型链，这个中间对象的原型要指向Student.prototype。     
为了实现这一点，中间对象可以用一个空函数F来实现：     

```
// PrimaryStudent构造函数:
function PrimaryStudent(props) {
    Student.call(this, props);
    this.grade = props.grade || 1;
}

// 空函数F:
function F() {
}

// 把F的原型指向Student.prototype:
F.prototype = Student.prototype;

// 把PrimaryStudent的原型指向一个新的F对象，F对象的原型正好指向Student.prototype:
PrimaryStudent.prototype = new F();

// 把PrimaryStudent原型的构造函数修复为PrimaryStudent:
PrimaryStudent.prototype.constructor = PrimaryStudent;

// 继续在PrimaryStudent原型（就是new F()对象）上定义方法：
PrimaryStudent.prototype.getGrade = function () {
    return this.grade;
};

// 创建xiaoming:
var xiaoming = new PrimaryStudent({
    name: '小明',
    grade: 2
});
xiaoming.name; // '小明'
xiaoming.grade; // 2

// 验证原型:
xiaoming.__proto__ === PrimaryStudent.prototype; // true
xiaoming.__proto__.__proto__ === Student.prototype; // true

// 验证继承关系:
xiaoming instanceof PrimaryStudent; // true
xiaoming instanceof Student; // true
```     

*注意:函数F仅用于桥接，我们仅创建了一个new F()实例，而且，没有改变原有的Student定义的原型链。*     

如果把继承这个动作用一个inherits()函数封装起来，还可以隐藏F的定义，并简化代码：    

```
function inherits(Child, Parent) {
    var F = function () {};
    F.prototype = Parent.prototype;
    Child.prototype = new F();
    Child.prototype.constructor = Child;
}
```   

这个inherits()函数可以复用：    

```
function Student(props) {
    this.name = props.name || 'Unnamed';
}

Student.prototype.hello = function () {
    alert('Hello, ' + this.name + '!');
}

function PrimaryStudent(props) {
    Student.call(this, props);
    this.grade = props.grade || 1;
}

// 实现原型继承链:
inherits(PrimaryStudent, Student);

// 绑定其他方法到PrimaryStudent原型:
PrimaryStudent.prototype.getGrade = function () {
    return this.grade;
};
```   

JavaScript的原型继承实现方式就是：   
定义新的构造函数，并在内部用call()调用希望“继承”的构造函数，并绑定this；   
借助中间函数F实现原型链继承，最好通过封装的inherits函数完成；   
继续在新的构造函数的原型上定义新方法。   

<h3 id="21">class继承</h3>   

新的关键字class从 **ES6** 开始正式被引入到JavaScript中。class的目的就是让定义类更简单:   

```
class Student {
    constructor(name) {
        this.name = name;
    }

    hello() {
        alert('Hello, ' + this.name + '!');
    }
}
```    

class的定义包含了构造函数constructor和定义在原型对象上的函数hello()     
这样就避免了Student.prototype.hello = function () {...}这样分散的代码。   

最后，创建一个Student对象代码和前面章节完全一样：    

```
var xiaoming = new Student('小明');
xiaoming.hello();
```    

用class定义对象的另一个巨大的好处是继承更方便了,简化原型链代码。       
   
原型继承的中间对象，原型对象的构造函数等等都不需要考虑了，直接通过extends来实现    
从Student派生一个PrimaryStudent：     

```
class PrimaryStudent extends Student {
    constructor(name, grade) {
        super(name); // 记得用super调用父类的构造方法!
        this.grade = grade;
    }

    myGrade() {
        alert('I am at grade ' + this.grade);
    }
}
```     

*注意: PrimaryStudent的定义也是class关键字实现的，而extends则表示原型链对象来自Student。   
PrimaryStudent需要通过super(name)来调用父类的构造函数，否则父类的name属性无法正常初始化。   
PrimaryStudent已经自动获得了父类Student的hello方法，我们又在子类中定义了新的myGrade方法*    

<h2 id="22">浏览器</h2>   

<h3 id="23">浏览器对象</h3>

window对象有innerWidth和innerHeight属性,获取浏览器窗口的内部宽度和高度。     
内部宽高是指除去菜单栏、工具栏、边框等占位元素后，用于显示网页的净宽高。   

outerWidth和outerHeight属性，可以获取浏览器窗口的整个宽高   

navigator.appName：浏览器名称；   
navigator.appVersion：浏览器版本；   
navigator.language：浏览器设置的语言；   
navigator.platform：操作系统类型；   
navigator.userAgent：浏览器设定的User-Agent字符串。   

*注意：navigator的信息可以很容易地被用户修改，所以JavaScript读取的值不一定是正确的*     

screen.width：屏幕宽度，以像素为单位；   
screen.height：屏幕高度，以像素为单位；   

location对象表示当前页面的URL信息。例如，一个完整的URL：   

http://www.example.com:8080/path/index.html?a=1&b=2#TOP   
可以用location.href获取。要获得URL各个部分的值，可以这么写：   

location.protocol; // 'http'   
location.host; // 'www.example.com'   
location.port; // '8080'   
location.pathname; // '/path/index.html'   
location.search; // '?a=1&b=2'   
location.hash; // 'TOP'   

要加载一个新页面，可以调用location.assign()。如果要重新加载当前页面，调用location.reload()方法非常方便。    

document对象表示当前页面。由于HTML在浏览器中以DOM形式表示为树形结构，document对象就是整个DOM树的根节点。   
document的title属性是从HTML文档中的title标签读取的，但是可以动态改变document.title = '努力学习JavaScript!';   

用document对象提供的getElementById()和getElementsByTagName()可以按ID获得一个DOM节点和按Tag名称获得一组DOM节点   
JavaScript可以通过document.cookie读取到当前页面的Cookie   

由于JavaScript能读取到页面的Cookie，而用户的登录信息通常也存在Cookie中，这就造成了巨大的安全隐患。   
这是因为在HTML页面中引入第三方的JavaScript代码是允许的。   
为了解决这个问题，服务器在设置Cookie时可以使用httpOnly，设定了httpOnly的Cookie将不能被JavaScript读取。    
这个行为由浏览器实现，主流浏览器均支持httpOnly选项，IE从IE6 SP1开始支持。    
为了确保安全，服务器端在设置Cookie时，应该始终坚持使用httpOnly。    

<h3 id="24">操作DOM</h3>    

获取DOM：    

在操作一个DOM节点前，我们需要通过各种方式先拿到这个DOM节点:     
document.getElementById()和document.getElementsByTagName()，以及CSS选择器document.getElementsByClassName()。   

使用querySelector()和querySelectorAll()，需要了解selector语法，然后使用条件来获取节点，更加方便：   

通过querySelector获取ID为q1的节点：   
`var q1 = document.querySelector('#q1');`

通过querySelectorAll获取q1节点内的符合条件的所有节点：   
`var ps = q1.querySelectorAll('div.highlighted > p');`   

*注意：ie8以下版本不支持querySelector和querySelectorAll。IE8仅有限支持*   
   
更新DOM：   

直接修改节点的文本，方法有两种：   

一种是修改innerHTML属性，可以修改一个DOM节点的文本内容，还可以直接通过HTML片段修改DOM节点内部的子树    
innerHTML会直接替换掉原来的所有子节点    

第二种是修改innerText或textContent属性，这样可以自动对字符串进行HTML编码，保证无法设置任何HTML标签   
innerText不返回隐藏元素的文本，而textContent返回所有文本。另外注意IE9以下不支持textContent    

插入DOM：   

获得了某个DOM节点，想在这个DOM节点内插入新的DOM  

appendChild，把一个子节点添加到父节点的最后一个子节点：    

```
var d = document.createElement('style');
d.setAttribute('type', 'text/css');
d.innerHTML = 'p { color: red }';
document.getElementsByTagName('head')[0].appendChild(d);
```     

insertBefore,把子节点插入到指定的位置,子节点会插入到referenceElement之前:    
`parentElement.insertBefore(newElement, referenceElement);`    

删除DOM：   

要删除一个节点，首先要获得该节点本身以及它的父节点，然后，调用父节点的removeChild把自己删掉:         

```
var self = document.getElementById('to-be-removed');
var parent = self.parentElement;
var removed = parent.removeChild(self);
removed === self; // true
```   

*注意：children属性是一个只读属性，并且它在子节点变化时会实时更新。删除多个节点时，要注意children属性时刻都在变化。*     

<h3 id="25">操作表单和文件</h3>   

操作表单：    

HTML5新增了大量标准控件，常用的包括date、datetime、datetime-local、color等。     
它们都使用input标签。不支持HTML5的浏览器无法识别新的控件，会把它们当做type="text"来显示    

JavaScript可以以两种方式来处理表单的提交（不算ajax）   

方式一是通过form元素的submit()方法提交一个表单     
例如，响应一个button的click事件，这种方式的缺点是扰乱了浏览器对form的正常提交      

```
function doSubmitForm() {
    var form = document.getElementById('test-form');
    // 可以在此修改form的input...
    // 提交form:
    form.submit();
}
```   

二种方式是响应form本身的onsubmit事件，在提交form时作修改   
注意要return true来告诉浏览器继续提交，如果return false，浏览器将不会继续提交form     
种情况通常对应用户输入有误，提示用户错误信息后终止提交form。   

在检查和修改input时，要充分利用input type="hidden"来传递数据。   
很多登录表单希望用户输入用户名和口令，但是，安全考虑，提交表单时不传输明文口令，而是口令的MD5    

```
input type="password" id="input-password"
input type="hidden" id="md5-password" name="password"

function checkForm() {
    var input_pwd = document.getElementById('input-password');
    var md5_pwd = document.getElementById('md5-password');
    // 把用户输入的明文变为MD5:
    md5_pwd.value = toMD5(input_pwd.value);
    // 继续下一步:
    return true;
}
```   

注意到id为md5-password的input标记了name="password"    
用户输入的id为input-password的input没有name属性。没有name属性的input的数据不会被提交。    

操作文件：   

当一个表单包含input type="file"时：     
表单的enctype必须指定为multipart/form-data，method必须指定为post。     
这样浏览器才能正确编码并以multipart/form-data格式发送表单的数据。    

出于安全考虑，浏览器只允许用户点击input type="file"来选择本地文件。     
用JavaScript对input type="file"的value赋值是没有任何效果的。     
当用户选择了上传某个文件后，JavaScript也无法获得该文件的真实路径     

通常，上传的文件都由后台服务器处理，JavaScript可以在提交表单时对文件扩展名做检查，以便防止用户上传无效格式的文件：   

```
var f = document.getElementById('test-file-upload');
var filename = f.value; // 'C:\fakepath\test.png'
if (!filename || !(filename.endsWith('.jpg') || filename.endsWith('.png') || filename.endsWith('.gif'))) {
    alert('Can only upload image file.');
    return false;
}
```    
 
随着HTML5的普及，新增的File API允许JavaScript读取文件内容，获得更多的文件信息。   
HTML5的File API提供了File和FileReader两个主要对象，可以获得文件信息并读取文件。   

用户选取的图片文件，并在一个div中预览图像：   

```
var
    fileInput = document.getElementById('test-image-file'),
    info = document.getElementById('test-file-info'),
    preview = document.getElementById('test-image-preview');

// 监听change事件:
fileInput.addEventListener('change', function () {
    // 清除背景图片:
    preview.style.backgroundImage = '';
    // 检查文件是否选择:
    if (!fileInput.value) {
        info.innerHTML = '没有选择文件';
        return;
    }
    // 获取File引用:
    var file = fileInput.files[0];
    // 获取File信息:
    info.innerHTML = '文件: ' + file.name + '<br>' +
                     '大小: ' + file.size + '<br>' +
                     '修改: ' + file.lastModifiedDate;
    if (file.type !== 'image/jpeg' && file.type !== 'image/png' && file.type !== 'image/gif') {
        alert('不是有效的图片文件!');
        return;
    }
    // 读取文件:
    var reader = new FileReader();
    reader.onload = function(e) { // 当文件读取完成后，JavaScript引擎将自动调用我们设置的回调函数
        var data = e.target.result; // 'data:image/jpeg;base64,/9j/4AAQSk...(base64编码)...'            
        preview.style.backgroundImage = 'url(' + data + ')';
    };
    // 以DataURL的形式读取文件:
    reader.readAsDataURL(file); // 发起一个异步操作来读取文件内容
});
```    

上面的代码演示了如何通过HTML5的File API读取文件内容。   
以DataURL的形式读取到的文件是一个字符串，类似于data:image/jpeg;base64,/9j/4AAQSk...(base64编码)...，常用于设置图像。    
如果需要服务器端处理，把字符串base64,后面的字符发送给服务器并用Base64解码就可以得到原始文件的二进制内容。    

<h3 id="26">AJAX</h3>    

一个Form的提交，一旦用户点击“Submit”按钮，表单开始提交，浏览器就会刷新页面，然后在新页面里告诉你操作是成功了还是失败了。     
如果不幸由于网络太慢或者其他原因，就会得到一个404页面。     
这就是Web的运作原理：一次HTTP请求对应一个页面。     

如果要让用户留在当前页面中，同时发出新的HTTP请求，就必须用JavaScript发送这个新请求       
接收到数据后，再用js更新页面，这样一来，用户就感觉自己仍然停留在当前页面，但是数据却可以不断地更新。   

在现代浏览器上写AJAX主要依靠XMLHttpRequest对象:    

```
function success(text) {
    var textarea = document.getElementById('test-response-text');
    textarea.value = text;
}

function fail(code) {
    var textarea = document.getElementById('test-response-text');
    textarea.value = 'Error code: ' + code;
}

var request;
if (window.XMLHttpRequest) {
    request = new XMLHttpRequest();
} else {
    request = new ActiveXObject('Microsoft.XMLHTTP'); //低版本的IE，需要换一个ActiveXObject对象
}

request.onreadystatechange = function () { // 状态发生变化时，函数被回调
    if (request.readyState === 4) { // 成功完成
        // 判断响应结果:
        if (request.status === 200) {
            // 成功，通过responseText拿到响应的文本:
            return success(request.responseText);
        } else {
            // 失败，根据响应码判断失败原因:
            return fail(request.status);
        }
    } else {
        // HTTP请求还在继续...
    }
}

// 发送请求:
request.open('GET', '/api/categories');
request.send();

alert('请求已发送，请等待响应...');
```    

*不要根据浏览器的navigator.userAgent来检测浏览器是否支持某个JavaScript特性  
一是因为这个字符串本身可以伪造。  
二是通过IE版本判断JavaScript特性将非常复杂。*  

当创建了XMLHttpRequest对象后，要先设置onreadystatechange的回调函数。     
在回调函数中，通常我们只需通过readyState === 4判断请求是否完成     
如果已完成，再根据status === 200判断是否是一个成功的响应。     

XMLHttpRequest对象的open()方法有3个参数：     
第一个参数指定是GET还是POST   
第二个参数指定URL地址     
第三个参数指定是否使用异步，默认是true，所以不用写。

*注意千万不要把第三个参数指定为false，否则浏览器将停止响应，直到AJAX请求完成。   
如果这个请求耗时10秒，那么10秒内你会发现浏览器处于“假死”状态。*   

最后调用send()方法才真正发送请求。     
GET请求不需要参数，POST请求需要把body部分以字符串或者FormData对象传进去。     

安全限制：跨域    

默认情况下，JavaScript在发送AJAX请求时，URL的域名必须和当前页面完全一致：     
域名要相同（www.example.com和example.com不同），     
协议要相同（http和https不同），     
端口号要相同（默认是:80端口，它和:8080就不同）。    
有的浏览器口子松一点，允许端口不同，大多数浏览器都会严格遵守这个限制    

请求外域方法：     

第一种是通过Flash插件发送HTTP请求，这种方式可以绕过浏览器的安全限制：     
必须安装Flash，并且跟Flash交互。不过Flash用起来麻烦，而且现在用得也越来越少了。    

第二种是通过在同源域名下架设一个代理服务器来转发，JavaScript负责把请求发送到代理服务器：    
'/proxy?url=http://www.sina.com.cn'     
代理服务器再把结果返回，这样就遵守了浏览器的同源策略。这种方式麻烦之处在于需要服务器端额外做开发。    

第三种方式称为JSONP，它有个限制，只能用GET请求，并且要求返回JavaScript。     
这种方式跨域实际上是利用了浏览器允许跨域引用JavaScript资源。     

JSONP通常以函数调用的形式返回，例如，返回JavaScript内容如下：     
`foo('data');`     

这样一来，我们如果在页面中先准备好foo()函数，然后给页面动态加一个script节点，相当于动态读取外域的JavaScript资源，最后就等着接收回调了。     
以163的股票查询URL为例，对于URL：http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice，你将得到如下返回：     

`refreshPrice({"0000001":{"code": "0000001", ... });`

因此我们需要首先在页面中准备好回调函数：     

```
function refreshPrice(data) {
    var p = document.getElementById('test-jsonp');
    p.innerHTML = '当前价格：' +
        data['0000001'].name +': ' + 
        data['0000001'].price + '；' +
        data['1399001'].name + ': ' +
        data['1399001'].price;
}

//最后用getPrice()函数触发：

function getPrice() {
    var js = document.createElement('script'),
        head = document.getElementsByTagName('head')[0];
    js.src = 'http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice';
    head.appendChild(js);
}
```   

如果浏览器支持HTML5，那么就可以一劳永逸地使用新的跨域策略：CORS了。    
CORS全称Cross-Origin Resource Sharing，是HTML5规范定义的如何跨域访问资源。     

假设本域是my.com，外域是sina.com，只要响应头Access-Control-Allow-Origin为http://my.com，或者是*，本次请求就可以成功。    
可见，跨域能否成功，取决于对方服务器是否愿意给你设置一个正确的Access-Control-Allow-Origin    

<h3 id="27">Promise</h3>    

在JavaScript的世界中，所有代码都是单线程执行的。   
由于这个“缺陷”，导致JavaScript的所有网络操作，浏览器事件，都必须是异步执行。异步执行可以用回调函数实现    

Promise有各种开源实现，在 **ES6** 中被统一规范    

Promise最大的好处是在异步执行的流程中，把执行代码和处理结果的代码清晰地分离了：    

```
// 清除log:
var logging = document.getElementById('test-promise-log');
while (logging.children.length > 1) {
    logging.removeChild(logging.children[logging.children.length - 1]);
}

// 输出log到页面:
function log(s) {
    var p = document.createElement('p');
    p.innerHTML = s;
    logging.appendChild(p);
}

new Promise(function (resolve, reject) {
    log('start new Promise...');
    var timeOut = Math.random() * 2;
    log('set timeout to: ' + timeOut + ' seconds.');
    setTimeout(function () {
        if (timeOut < 1) {
            log('call resolve()...');
            resolve('200 OK');
        }
        else {
            log('call reject()...');
            reject('timeout in ' + timeOut + ' seconds.');
        }
    }, timeOut * 1000);
}).then(function (r) {
    log('Done: ' + r);
}).catch(function (reason) {
    log('Failed: ' + reason);
});

Log:

start new Promise...

set timeout to: 0.6378889032297219 seconds.

call resolve()...

Done: 200 OK
```   

Promise可以串行执行任务：   
比如，有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数。   
`job1.then(job2).then(job3).catch(handleError);`         

下面的例子演示了如何串行执行一系列需要异步计算获得结果的任务：    

```
var logging = document.getElementById('test-promise2-log');

while (logging.children.length > 1) {
    logging.removeChild(logging.children[logging.children.length - 1]);
}

function log(s) {
    var p = document.createElement('p');
    p.innerHTML = s;
    logging.appendChild(p);
}

// 0.5秒后返回input*input的计算结果:
function multiply(input) {
    return new Promise(function (resolve, reject) {
        log('calculating ' + input + ' x ' + input + '...');
        setTimeout(resolve, 500, input * input);
    });
}

// 0.5秒后返回input+input的计算结果:
function add(input) {
    return new Promise(function (resolve, reject) {
        log('calculating ' + input + ' + ' + input + '...');
        setTimeout(resolve, 500, input + input);
    });
}

var p = new Promise(function (resolve, reject) {
    log('start new Promise...');
    resolve(123);
});

p.then(multiply)
 .then(add)
 .then(multiply)
 .then(add)
 .then(function (result) {
    log('Got value: ' + result);
});

Log:

start new Promise...

calculating 123 x 123...

calculating 15129 + 15129...

calculating 30258 x 30258...

calculating 915546564 + 915546564...

Got value: 1831093128
```   

setTimeout可以看成一个模拟网络等异步执行的函数。     
现在，我们把上一节的AJAX异步执行函数转换为Promise对象，看看用Promise如何简化异步处理：     

```
// ajax函数将返回Promise对象:

function ajax(method, url, data) {
    var request = new XMLHttpRequest();
    return new Promise(function (resolve, reject) {
        request.onreadystatechange = function () {
            if (request.readyState === 4) {
                if (request.status === 200) {
                    resolve(request.responseText);
                } else {
                    reject(request.status);
                }
            }
        };
        request.open(method, url);
        request.send(data);
    });
}

var log = document.getElementById('test-promise-ajax-result');
var p = ajax('GET', '/api/categories');

p.then(function (text) { // 如果AJAX成功，获得响应内容
    log.innerText = text;
}).catch(function (status) { // 如果AJAX失败，获得响应代码
    log.innerText = 'ERROR: ' + status;
});
```     

Promise并行执行异步任务 Promise.all()：    
试想一个页面聊天系统，我们需要从两个不同的URL分别获得用户的个人信息和好友列表，这两个任务是可以并行执行的：    

```
var p1 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 500, 'P1');
});

var p2 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 600, 'P2');
});

// 同时执行p1和p2，并在它们都完成后执行then:
Promise.all([p1, p2]).then(function (results) {
    console.log(results); // 获得一个Array: ['P1', 'P2']
});
```    

有些时候，多个异步任务是为了容错。     
比如，同时向两个URL读取用户的个人信息，只需要获得先返回的结果即可。这种情况下，用Promise.race()实现：      

```
var p1 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 500, 'P1');
});

var p2 = new Promise(function (resolve, reject) {
    setTimeout(resolve, 600, 'P2');
});

Promise.race([p1, p2]).then(function (result) {
    console.log(result); // 'P1'
}); 

// 由于p1执行较快，Promise的then()将获得结果'P1'。p2仍在继续执行，但执行结果将被丢弃。
```    

<h3 id="28">Canvas</h3>    

Canvas是HTML5新增的组件，它就像一块幕布，可以用JavaScript在上面绘制各种图表、动画等：    
Canvas除了能绘制基本的形状和文本，还可以实现动画、缩放、各种滤镜和像素转换等高级操作。     

如果要实现非常复杂的操作，考虑以下优化方案:    
通过创建一个不可见的Canvas来绘图，然后将最终绘制结果复制到页面的可见Canvas中；    
尽量使用整数坐标而不是浮点数；    
可以创建多个重叠的Canvas绘制不同的层，而不是在一个Canvas中绘制非常复杂的图；    
背景图片如果不变可以直接用img标签并放到最底层。    

<h2 id="29">jQuery</h2>     

$这个变量不幸地被占用了，而且还不能改，那我们就只能让jQuery把$变量交出来，然后就只能使用jQuery这个变量：    

```
$; // jQuery(selector, context)
jQuery.noConflict();
$; // undefined
jQuery; // jQuery(selector, context)
```   

```
var div = $('#abc') //jq对象
var dirDom = div.get(0) //取第一个DOM元素
var another = $(divDom) //重新把DOM包为jq对象
```    

<h3 id="30">$.ajax()</h3>    

jQuery在全局对象jQuery（也就是$）绑定了ajax()函数，可以处理AJAX请求。     
ajax(url, settings)函数需要接收一个URL和一个可选的settings对象，常用的选项如下：   

async：是否异步执行AJAX请求，默认为true，千万不要指定为false；   

method：发送的Method，缺省为'GET'，可指定为'POST'、'PUT'等；   

contentType：发送POST请求的格式，默认值为'application/x-www-form-urlencoded; charset=UTF-8'     
也可以指定为text/plain、application/json；    

data：发送的数据，可以是字符串、数组或object。     
如果是GET请求，data将被转换成query附加到URL上     
如果是POST请求，根据contentType把data序列化成合适的格式；    

headers：发送的额外的HTTP头，必须是一个object；    

dataType：接收的数据格式，可以指定为'html'、'xml'、'json'、'text'等。     
缺省情况下根据响应的Content-Type猜测。     

jQuery的jqXHR对象类似一个Promise对象，我们可以用链式写法来处理各种回调：   

```
function ajaxLog(s) {
    var txt = $('#test-response-text');
    txt.val(txt.val() + '\n' + s);
}

$('#test-response-text').val('');

var jqxhr = $.ajax('/api/categories', {
    dataType: 'json'
}).done(function (data) {
    ajaxLog('成功, 收到的数据: ' + JSON.stringify(data));
}).fail(function (xhr, status) {
    ajaxLog('失败: ' + xhr.status + ', 原因: ' + status);
}).always(function () {
    ajaxLog('请求完成: 无论成功或失败都会调用');
});
```   

get:   
对常用的AJAX操作，jQuery提供了一些辅助方法。由于GET请求最常见，所以jQuery提供了get()方法，可以这么写：   

```
var jqxhr = $.get('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
});
```   

第二个参数如果是object，jQuery自动把它变成query string然后加到URL后面，实际的URL是：   
/path/to/resource?name=Bob%20Lee&check=1   
这样我们就不用关心如何用URL编码并构造一个query string了。   

post:    
post()和get()类似，但是传入的第二个参数默认被序列化为application/x-www-form-urlencoded：   

```
var jqxhr = $.post('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
});
```   

实际构造的数据name=Bob%20Lee&check=1作为POST的body被发送。    

getJSON:   
由于JSON用得越来越普遍，所以jQuery也提供了getJSON()方法来快速通过GET获取一个JSON对象：   

```
var jqxhr = $.getJSON('/path/to/resource', {
    name: 'Bob Lee',
    check: 1
}).done(function (data) {
    // data已经被解析为JSON对象了
});
```    

jQuery的AJAX完全封装的是JavaScript的AJAX操作，所以它的安全限制和前面讲的用JavaScript写AJAX完全一样。     
如果需要使用JSONP，可以在ajax()中设置jsonp: 'callback'，让jQuery实现JSONP跨域加载数据。     

<h3 id="31">编写jQuery插件</h3>     

给jQuery对象绑定一个新方法是通过扩展$.fn对象实现的。  

jQuery提供辅助方法$.extend(target, obj1, obj2, ...):     
把多个object对象的属性合并到第一个target对象中，遇到同名属性，总是使用靠后的对象的值，也就是越往后优先级越高   

```
$.fn.highlight = function (options) {
    // 合并默认值和用户设定值:
    var opts = $.extend({}, $.fn.highlight.defaults, options);
    this.css('backgroundColor', opts.backgroundColor).css('color', opts.color);
    return this;
}

// 设定默认值:
$.fn.highlight.defaults = {
    color: '#d85030',
    backgroundColor: '#fff8de'
}

//用户使用时，只需一次性设定默认值：
$.fn.highlight.defaults.color = '#fff';
$.fn.highlight.defaults.backgroundColor = '#000';

//然后就可以非常简单地调用highlight()了。
$('#test-highlight p:first-child span').highlight();
$('#test-highlight p:last-child span').highlight({
    color: '#dd1144'
});
```   

编写一个jQuery插件的原则：    
给$.fn绑定函数，实现插件的代码逻辑；   
插件函数最后要return this;以支持链式调用；   
插件函数要有默认值，绑定在$.fn.pluginName.defaults上；   
用户在调用时可传入设定值以便覆盖默认值。   

<h3 id="32">错误处理</h3>    

错误处理：try ... catch ... finally   

当代码块被try { ... }包裹的时候，就表示这部分代码执行过程中可能会发生错误   
一旦发生错误，就不再继续执行后续代码，转而跳到catch块。   
catch (e) { ... }包裹的代码就是错误处理代码，变量e表示捕获到的错误。最后，无论有没有错误，finally一定会被执行。    

catch和finally可以不必都出现   
程序也可以主动抛出一个错误，让执行流程直接跳转到catch块。抛出错误使用throw语句。    
当我们用catch捕获错误时，一定要编写错误处理语句，哪怕仅仅把错误打印出来，也不要什么也不干   

```
var r, n, s;

try {
    s = prompt('请输入一个数字');
    n = parseInt(s);
    if (isNaN(n)) {
        throw new Error('输入错误');
    }
    // 计算平方:
    r = n * n;
    console.log(n + ' * ' + n + ' = ' + r);
} catch (e) {
    console.log('出错了：' + e);
}
```    

异步错误处理：    

```
function printTime() {
    throw new Error();
}

try {
    setTimeout(printTime, 1000);
    console.log('done');
} catch (e) {
    console.log('error');
}
```    

如果printTime()函数内部发生了错误，我们试图用try包裹setTimeout()是无效的：   
原因就在于调用setTimeout()函数时，传入的printTime函数并未立刻执行！     
紧接着，JavaScript引擎会继续执行console.log('done');语句，而此时并没有错误发生。     
直到1秒钟后，执行printTime函数时才发生错误，但此时除了在printTime函数内部捕获错误外，外层代码并无法捕获。    

所以，涉及到异步代码，无法在调用时捕获，原因就是在捕获的当时，回调函数并未执行。    
类似的，当我们处理一个事件时，在绑定事件的代码处，无法捕获事件处理函数的错误。    

<h3 id="100">参考书籍</h3>   

[廖雪峰官网教程](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001434499763408e24c210985d34edcabbca944b4239e20000)   

[JavaScript高级程序设计](http://www.wrox.com)     

[ES6标准入门](https://github.com/ruanyf/es6tutorial)    

