# JavaScript教程学习笔记    

## 项目介绍：  
本项目的开启纯粹为了记录个人学习js书籍时，对相关知识点的记录。方便随时查阅。并非js入门教程。   


* [1. 快速入门](#1)
    * [1.1 基本语法和数据类型](#new2)
    * [1.2 let和const命令](#new1)  
    * [1.3 字符串](#2)
    * [1.4 数组](#3)
    * [1.5 对象](#4)
    * [1.6 条件判断](#5)
    * [1.7 Map和Set](#6)
    * [1.8 iterable](#7)
* [2. 函数](#8)  
    * [2.1 函数定义和调用](#9)
    * [2.2 变量作用域与解构赋值](#10)
    * [2.3 方法](#11)
    * [2.4 高阶函数](#12)
    * [2.5 闭包](#13)
    * [2.6 箭头函数](#14)
    * [2.7 generator](#15)
    * [2.8 惰性载入函数](#52)
    * [2.9 防抖和节流](#53)
* [3. 标准对象](#16)
    * [3.1 Date](#17)
    * [3.2 JSON](#18)
* [4. 面向对象编程](#19)
    * [4.1 创建对象和原型继承](#20)
    * [4.2 class继承](#21)
    * [4.3 设计模式](#43)
* [5. 浏览器](#22)
    * [5.1 浏览器对象](#23)
    * [5.2 操作DOM](#24)
    * [5.3 操作表单和文件](#25)
    * [5.4 AJAX](#26)
    * [5.5 Promise](#27)
    * [5.6 fetch](#51)
    * [5.7 Canvas](#28)
* [6. jQuery](#29)
    * [6.1 $.ajax()](#30)
    * [6.2 编写jQuery插件](#31)
* [7. 错误处理](#32)
* [8. 高性能JavaScript(ES5)](#33)
    * [8.1 加载和执行](#34)
    * [8.2 数据存储](#35)
    * [8.3 DOM编程](#36)
    * [8.4 算法和流程控制](#37)
    * [8.5 快速响应用户界面](#38)
    * [8.6 编程实践](#39)
    * [8.7 构建并部署高性能js应用](#40)
    * [8.8 js书写优化](#44)
    * [8.9 单元测试](#54)
* [9. 正则表达式](#41)
* [10. 事件](#42)
    * [10.1 事件概述](#55)
    * [10.2 移动端事件](#56)
* [11. 页面优化](#45)
* [12.前端与计算机基础](#46)
    * [12.1 理解WebSocket和TCP/IP](#47)
    * [12.2 0.1+0.2不等于0.3](#48)
    * [12.3 WebAssembly与程序编译](#49)
    * [12.4 js与多线程](#50)
* [13.模块化](#57)
    * [13.1 模块化发展](#58)  
    * [13.2 CommonJS/AMD/CMD](#59)  
    * [13.3 ES6模块支持](#60)  
* [14.Babel](#61)
* [14.前端工程化](#62)
    * [14.1 工程化必要性和发展史](#63)
    * [14.2 Grunt开发简易相册](#64)
    * [14.3 Gulp构建MarkDown编辑器](#65)
    * [14.4 Webpack4+vue2](#66)
                                                                                                                                               

  
<h2 id="1">快速入门</h2>          
     
<h3 id="new2">基本语法和数据类型</h3>                                                                                                                                                 
typeof typeof 任何 返回string    

按位或,按位与,异或:   

```
var a=3,b=7
a | b  //7
```   

转成2进制    
3 011   
7 111   
或运算有一个是1就是1，所以是111，再转换为10进制就是7   
a&b都是1才是1    
a^b一样是0，不一样是1     

位运算是整数运算，所以取整有简便方法：   

```
123.13234 | 0  //123
"123.13234" | 0  //123
Math.floor(123.13234) //123
```   

&&如果都是true，那么直接返回后边的。如果前边是false，那就返回前边的。如     

```
123 && 456 //456
0 && 123 //0
```    

二进制转换十进制：    
100最右边开始0*2的0次方+0*2的1次方+1*2的2次方。结果就是4    
   
十进制转换二进制：   
除以2：   
12/2为6 整除记录0   
6/2为3 整除记录0   
3/2为1 不整除记录1   
1/2 不整除记录1   
然后反过来看，12的二进制就是1100   

基本数据类型：undefined,null,string,number,boolean     
不能给基本类型添加属性和方法    
基本类型值是不可变的：     

```
var name = 'zheng'
name.toUpperCase() //ZHENG
console.log(name) //zheng
```   
    
基本类型的变量是存放在栈区的，栈区包括了变量的标识符和变量的值     
引用类型的值是可变的。    
引用类型的值同时保存在栈区（栈内存）和堆区（堆内存）中的对象。    
栈区保存变量标识符和指向堆内存中该对象的指针，也可以说该对象在堆内存中的地址。    

```
var a = {}
var b = {}
a == b //false
```  
    
引用类型的值是按引用访问的，就是比较两个对象堆内存中的地址是否相同，明显不同。    
引用类型的赋值，其实是对象保存在栈区地址指针的赋值，因此两个变量指向同一个对象，任何操作都会相互影响。     
    
变量向变量赋值引用类型时：     
   
```
var a = {}
var b = a
a.name = 'Zheng'
b.age = 1
console.log(b.name) //Zheng
console.log(a.age) //1
a = null
b //{name: "Zheng", age: 1}
```    

变量向变量赋值基本类型时：    

```
var c = 10
var d = c
c++
console.log(d) //10
console.log(c) //11
```    

x=y=z=[1,2,3]那xyz都是数组123               

<h3 id="new1">let和const命令</h3>

**ES6**新增了let命令，所有声明的变量只在let命令所在的代码块内有效：   

```
{
    let a = 10;
    var b = 1;
}
a // Uncaught ReferenceError: a is not defined
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

`const foo; // Uncaught SyntaxError: Missing initializer in const declaration`    

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
  
`str += 'one' + 'two';`  

运行会经历四个步骤：   
1.在内存中创建临时字符串   
2.连接后的字符串onetwo被赋值给临时字符串   
3.临时字符串与str当前值连接   
4.结果赋值给str  

优化方法：直接附加内容给str。避免产生临时字符串    
ie8之前版本浏览器无效,反而会慢，因为实现机制不同，ie7会每连接一对字符串就把它复制到一块新分配的内存中。    

```
str += 'one';
str += 'two';
```   

或者只用一个语句达到上边效果：    

`str = str + 'one' +'two' //附加字符串都是从左往右连接的，所以同样避免了使用临时字符串。`    

数组项合并比其他字符串连接方法更慢，但事实上，在ie7和ie6中相反。      

```
//其它浏览器更高效：
var str = 'a',
    news = '',
    time = 5000;

while( time-- ){news += str;}

//ie6,7更高效：
var str = 'a',
    arr = [],
    news = '',
    time = 5000;

while( time-- ){arr[arr.length] += str;}
news = arr.join('');	
```   

多数情况，使用concat()比使用+和+=稍慢。    

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
  
```
var name = '小明';  
var age = 20; 
var message = `你好,${name},你今年${age}岁了`;
```   

**ES6**常用字符串函数startsWith,endsWith,includes,repeat：     

```
var s = 'Hello';
s.startsWith('He'); //true，表示原字符串是否以参数字符串开始
s.endsWith('lo'); //true,表示元字符串是否以参数字符串结束   
s.includes('el'); //true,表示原字符串是否包含参数字符串
s.repeat(3); //返回'HelloHelloHello',表示将原字符串重复3次
```

**ES6**在Number对象上增加了isNaN和isInteger方法：       
[Number.isNaN](https://www.cnblogs.com/Spring-Rain/p/5722594.html)判断参数的值是否是NaN：       

```
Number.isNaN(NaN)  //true
Number.isNaN('1024') //false
Number.isNaN(true) //false
Number.isNaN(1024) //false
```

Number.isInteger判断参数的值是否是整数      

```
Number.isInteger(25) //true
Number.isInteger(25.0) //true
Number.isInteger('25') //false
Number.isInteger(true) //false
```

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

stringObject.indexOf(searchvalue,fromindex) 返回字符串首次出现的位置    
stringObject.charAt(index) 返回制定位置的字符串   
stringObject.split(separator,howmany) 用于把字符串分割成数组   
stringObject.concat(str1,str2,str3) 合并多个字符串，返回合并的结果，实际值并未改变。也可合并数组。   
   
indexOf()会搜索指定字符串首次出现的位置，也可操作数组：    
   
```
var s = 'hello, world';
s.indexOf('world'); // 返回7
s.indexOf('World'); // 没有找到指定的子串，返回-1
```   
    
indexOf()数组去重：     

```
function uniqueArray(arr){
    var retArray = [];
    for(var i=0;i<arr.length;i++){
        if(retArray.indexOf(arr[i])<0){
            retArray.push(arr[i]);
        }
    }
    return retArray
}
uniqueArray([1,1,1,1,1,2,3,4,5,6,7,3,4,5,])
```   
   
charAt() 方法可返回指定位置的字符:  
如果参数 index 不在 0 与 string.length 之间，该方法将返回一个空字符串    

```
"144253".charAt(3) //2   
"144253".charAt(6) //''
```  

字符串截取：    
slice(),substr(),substring()   
slice和substring两个参数，起始位置和结束位置（不包括结束位置）   
substr起始位置和字符串长度   
substring两个参数，较小的做起始，另一个做结束。   
参数是负数时：   
slice将字符串长度与负数相加做参数，也可理解为从字符串末尾算起，如-1就是最后一个字符。   
substring将负数变成0   
ie对substr接收负数处理有错误，返回原始字符串   
   
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

splice()数组去重：    

```
function uniqueArray(arr){
    for(var i=0; i<arr.length; i++){
        for(var j=i+1; j<arr.length; j++){
            if(arr[i]==arr[j]){
                arr.splice(j,1);
                j--;
            }
        }
    }
    return(arr);
    }

uniqueArray([1,2,2,3,3,3,3,1,2,3,5,4,2])
```
    
concat()方法把当前的Array和另一个Array连接起来，并返回一个新的Array：    
*concat()也可用于合并字符串,返回合并后的结果。*       

```
var arr = ['A', 'B', 'C'];
var added = arr.concat([1, 2, 3]);
added; // ['A', 'B', 'C', 1, 2, 3]
arr; // ['A', 'B', 'C']
```

concat()方法可以接收任意个元素和Array，并且自动把Array拆开，然后全部添加到新的Array里： 

```
var arr = ['A', 'B', 'C'];
var added = arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
```   

join()方法，它把当前Array的每个元素都用指定的字符串连接起来，然后返回连接后的字符串   
如果Array的元素不是字符串，将自动转换为字符串后再连接：   

```
var arr = ['A', 'B', 'C', 1, 2, 3];
arr.join('-'); // 'A-B-C-1-2-3'
```   

合并数组的一种方法：    

```
var arr = [1,2,3]
arr.push.apply(arr,[4,5])
```   

<h3 id="4">对象</h3>     

```
var a = {b:2}
a.b
a['b']
```    

`ele.onclick === ele['onclick']`    

如做能力检测时候，ele['on'+type]就没法用点    
  
{"a.2":2}不是变量名就要加引号   

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

避免遍历包含原型的属性：    

```
var arr = ["admin","manager","db"]
Array.prototype.name= "zhangshan"; 
for( var i in arr ){
	if( arr.hasOwnProperty(i) ){
		console.log(i+':'+arr[i])
	}
}
```   

只有hasOwnPrototype()能给出正确答案:

```
Object.prototype.bar = 1
var foo ={goo:undefined}
foo.bar //1
'bar' in foo //true
foo.hasOwnPrototype('bar') //false
foo.hasOwnPrototype('goo') //true
```    
  
凡是通过new Function()创建的对象都是函数对象，其他的都是普通对象：   

```
//f1,f2,f3为函数对象：    
function f1(){}
var f2 = function(){}
var f3 = new Function('str','console.log(str)')

//o1,o2,o3为普通对象
var o1 = new f1()
var o2 = {}
var o3 = new Object()
```    

防止篡改对象：    

Object.seal防止新增和删除属性：    

```
let person = {
    name:'yu'
};
Object.seal(person);
delete person.name //不能删
person.name // yu
person.age = 18 //不能加
person.age //undefined
```

Object.freeze冻结对象，不能改属性：     

```
let person = {
    name:'yu'
};
Object.freeze(person);

person.name = 'yuyu'
person.name // yu
```

**ES6**支持对象定义时属性和函数的简写：     

```
var p = 1;
var o = {
    p:p,
    f:function(){}
}

//es6简写：
var p = 1;
var o = {
    p,
    ['a'+p]:2 //属性名为a1
    f(){}
}
```

[判断传入对象类型](https://www.cnblogs.com/jq-melody/p/4499333.html)：      

Object.prototype.toString.call(o)能直接返回对象的类属性。         
形如"[object class]"的字符串，我们通过截取class，并能知道传入的对象是什么类型:                   

```
function isClass(o){
    if(o===null) return "Null";
    if(o===undefined) return "Undefined";
    return Object.prototype.toString.call(o).slice(8,-1);
}
```   

[克隆对象](https://www.cnblogs.com/amiezhang/p/8023731.html)：         
**es6**的Object.assign        

```
var obj = {a:1,b:2}  
var newObj = Object.assign({}, obj); 
```

JSON对象序列化方法克隆对象：          
*这个方法明显是简单得多，但是有个弊端，就是不能复制函数*            

```
var obj = {a:1,b:2}  
var newObj = JSON.parse(JSON.stringify(obj)); 
```

<h3 id="5">条件判断</h3>
js把null、undefined、0、NaN和空字符串''视为false，其他值一概视为true     
  
*0 === -0  // true*

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
  
省略一个条件：   

```
var i = 0;
for(;i<10;i++){console.log(i)}
```    
  
<h3 id="6">Map和Set</h3>     

**ES6**新数据类型 Map是一组键值对的结构，具有极快的查找速度。         
              
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
s; // 仍然是 Set {1, 2, 3,"3", 4}
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
a.length //3
```    

*for ... in每次迭代操作会同时搜索实例和原型属性，除非明确需要迭代一个属性数量未知的对象，否则避免用*           

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

函数声明：   
使用 function 关键字声明一个函数，再执行一个函数名。        

`function fnName() {...} `     
   
函数表达式：   
使用 function 关键字声明一个函数，但未给函数命名，最后将匿名函数赋予一个变量。          

`var fnName = function() { ... }`    

匿名函数：  
使用 function 关键字声明一个函数，但未给函数命名，所以叫匿名函数。   
匿名函数属于函数表达式，匿名函数有很多作用。           
赋予一个变量则创建函数，赋予一个事件则成为事件处理程序或创建闭包等。       

`function() { ... }`   

函数声明和函数表达式不同之处在于：   

JavaScript 引擎在解析 JavaScript 代码时会“函数声明提升”当前执行环境(作用域)上的函数声明，    
函数表达式必须等到 JavaScript 引擎执行到它所在行时，才会从上而下一行一行地解析函数表达式。    

函数表达式后面可以加括号立即调用该函数，函数声明不可以，只能以 fnName() 形式调用。    
   
() 、! 、+ 、- 、= 等运算符，都将函数声明转换成函数表达式,可以在后面加括号，并立即执行函数的代码:       
     
```
//因为以function开头，认为是函数声明，结果没有函数名，就报错了
function () {
  console.log("hello word!");
}();

//函数声明不能这样立即执行，报错。
function foo() {
console.log("hello word!");
}();

//函数声明传个参数就不报错了。
function a(a) {
  console.log(a);  //打印出123
}(123);

//匿名函数立即执行
(function(a) {
  console.log(a);  //使用()运算符，打印出123
})(123);

(function(a) {
  console.log(a);  //使用()运算符，打印出1234
}(1234));

!function(a) {
  console.log(a);  //使用!运算符，打印出12345
}(12345);

+function(a) {
  console.log(a);  //使用+运算符，打印出123456
}(123456);

-function(a) {
  console.log(a);  //使用-运算符，打印出1234567
}(1234567);

var fn = function(a) {
  console.log(a);  //使用=运算符，打印出12345678
}(12345678);
```   

javascript没有私有作用域的概念，你在全局或局部作用域中声明了一些变量，可能会被其他人不小心用同名的变量给覆盖掉。     
根据 javascript 函数作用域链的特性，可以使用这种技术模仿一个私有作用域：     
用匿名函数作为一个“容器”，“容器”内部可以访问外部的变量，而外部环境不能访问“容器”内部的变量，    
所以 (function(){ ... })() 内部定义的变量不会和外部的变量发生冲突，俗称“匿名包裹器”或“命名空间”。    

js的函数也是一个对象。   
下边要有分号，表示赋值结束:     

```var abs = function(x){return x}; ```   

函数传入的参数多或者少也没有问题    

arguments，它只在函数内部起作用，并且永远指向当前函数的调用者传入的所有参数。arguments类似Array但它不是一个Array
最常用于判断传入参数的个数    

**ES6**标准引入了rest参数：   

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

**ES6**可以给函数参数指定默认值：     

```
function minus (x,y=2){return x-y}
minus(5)  //3
```

*注意：return语句，由于js引擎在行末自动添加分号的机制，return不要单独一行。*    

函数里return的也可以判断。如：    

```
function a(n){return n === 2}
a(2) //true
```   

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

对象解构赋值：    

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
// passport不是变量，而是为了让变量id获得passport属性:
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

函数参数的解构赋值：    

```
function minus([x,y]){return x-y}
minus([5,3])

function minus({x,y}){return x-y}
minus({x:5,y:3})
```

数组解构赋值：     
数组解构赋值按照顺序解构，对象是按照属性名解构，除此之外两者使用方式一致     

```
var arr = ['a','b'];
var [A,B,C] = arr //A为a，B为b，C为undefined
```

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

apply(),call(),bind():      

以下代码this并不在函数作用域中查找name。a函数在全局上下文中执行，一次a内部的this指向全局对象：         

```
var name = 'tiger';
function a(){
	var name = 'aaa';
	console.log(this.name)
}
a() //tiger
```    
   
要指定函数的this指向哪个对象，可以用函数本身的apply方法。     
它接收两个参数，第一个参数就是需要绑定的this变量，第二个参数是Array，表示函数本身的参数。    

```
var name = 'tiger';
function a(){
	var name = 'aaa';
	console.log(this.name)
}
a.call({name:'bbb'}) //bbb
//a.apply({name:'bbb'}) //bbb
//a.bind({name:'ccc'})() //bbb
```

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

apply()和call()，唯一区别是：     
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

在这个例子中，我们在函数lazy_sum中又定义了函数sum，内部函数sum可以引用外部函数lazy_sum的参数和局部变量。      
当lazy_sum返回函数sum时，相关参数和变量都保存在返回的函数中，这种称为“闭包（Closure）”的程序结构拥有极大的威力。      
  
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

闭包使用场景：     
可以封装一个私有变量:    

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

闭包使用场景：      
[JavaScript闭包之Fibonacci数列](https://blog.csdn.net/u012058778/article/details/49851749)      
计算斐波那契数列：    

```
var fib = (function(){
    var arr = [0,1,1]; //前3位直接返回
    return function(n){
        var res = arr[n];
        if(res){
            return res;
        }else{
            arr[n] = fib(n-1) + fib(n-2);
            return arr[n];
        }
    }
})()

fib(10) //55
```

[函数柯里化](https://blog.csdn.net/shunfa888/article/details/80013170)     
高阶函数是可以当参数传递和返回值的。           
写一个只有一个参数的函数，而这个函数返回一个带参数的函数，就实现了能写两个参数的函数了。这就是所谓的柯里化。      
也可以理解为一种在处理函数过程中的逻辑思维方式。      

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

将函数作为其他函数的返回值或参数传递时，常会不经意创建闭包，导致内存未释放：      

```
var scope = 10;
function cal(add){console.log(scope + add)};
(function(ca){
    var scope = 100;
    ca(5) //输出15
})(cal)
```

词法作用域：函数定义时就确定了作用域，而不是函数执行时：           

```
function outer(){
    var scope = 10;
    return function inner(){
        scope += 10;
        console.log(scope)
    }
}

var scope = 100;
var fn = outer();
fn() //20
fn() //30
```

使用闭包最需要关注的性能点：   
在频繁访问跨作用域的标识符时，每次访问都会带来性能损失。   
将常用的跨作用域变量存储在局部变量中，然后直接访问局部变量。来减轻闭包对执行速度的影响。  

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
var fun = (x, y, ...rest) => {
    var i, sum = x + y;
    for (i=0; i<rest.length; i++) {
        sum += rest[i];
    }
    return sum;
}
fun(1,2,3,4,5,6,7,8,9,10) //55
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
obj.getAge(); // 28
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
generator和函数不同的是，generator由function*定义（注意多出的星号），并且，除了return语句，还可以用yield返回多次。    

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

由于生成器的特性，每次调用next方法执行一个区间代码，即生成器提供了分段执行机制。      
在生成器中使用异步调用：      
*实际项目中，需要处理异常以及类型效验，可用开源类库[co](https://github.com/tj/co)实现这一功能。*       
 
```
function* demo() {
    var a = yield Promise.resolve(1);
    var b = yield Promise.resolve(a + 2);
    var c = yield Promise.resolve(3+b);
    return c;
};


function co(generator) {
    var gen = generator();
    function nextFunc(arg) {
        var next = gen.next(arg);
        // 首先执行以下next，取到第一个Promise
        if (!next.done) {
            // 如果生成器没有完成时，执行这个Promsie
            next.value.then(function (data) {
                console.log(data);
                // 当Promise执行成功后，执行下一个
                nextFunc(data);
            }).catch(function(err){
                console.log(err);
                nextFunc();
            });
        } else if(next.value) {
            // 当生成器执行完成后，得到返回的值。
            console.log(next.value);
        }
    }
    nextFunc();
}
co(demo); //1,3,6,6
```

ES7提供了async和await关键字，是一个更优秀的异步解决方案：      

```
async function es7(){
    var a = await Promise.resolve(1);
    var b = await Promise.resolve(a * 2);
    var c = await Promise.resolve(b+3);
    return c;
}

es7().then(function(data){
    console.log(data);
})
```     

通过关键字async标注函数为异步，await等待异步调用结果。异步函数执行后，返回结果为promise对象。      

<h3 id="52">惰性载入函数</h3>       

有时需要在一些兼容判断，或一些UA的判断，如：      

```
getUAType:function(){
    let ua = window.navigator.userAgent;
    if(ua.match(/renten/i)){
        return 0;
    }else if(ua.match(/MicroMessenger/i)){
        return 1
    }else if(ua.match(/weibo/i)){
        return 2
    }
    return -1
}
```

这个函数判断用户是在哪个环境打开网页。一般结果都是死的，不管多少次判断都是一样结果。      
所以为了优化，有了惰性函数一说，可以改写：      

```
getUAType:function(){
    let ua = window.navigator.userAgent;
    if(ua.match(/renten/i)){
        pageData.getUAType = () => 0;
        return 0;
    }else if(ua.match(/MicroMessenger/i)){
        pageData.getUAType = () => 1;
        return 1
    }else if(ua.match(/weibo/i)){
        pageData.getUAType = () => 2;
        return 2
    }
    return -1
}
```

在每次判断之后，把getUaType函数重新赋值，以后每次获取就不用判断了。     
下边例子更简单实现，直接用变量存起来就好了，缺点是没使用到getUAType函数也会执行一次判断：      

```
let ua = window.navigator.userAgent;
let UAType = ua.match(/renten/i) ? 0 :
              ua.match(/MicroMessenger/i) ? 1 :
              ua.match(/weibo/i) ? 2 : -1
```   

<h3 id="53">防抖和节流</h3>       

[函数节流与函数防抖的区别](https://blog.csdn.net/qq_35585701/article/details/81392174)         
防抖是只执行重复操作的最后一次，节流是每多少单位时间内只执行一次。          
    
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
*ES6将parseInt()和parseFloat()移植到了number上*    

用String()来转换任意类型到string，或者直接调用某个对象的toString()方法；   

通常不必把任意类型转换为boolean再判断，因为可以直接写if (myVar) {...}；   
*!!这样就可以把非布尔类型转换成布尔类型了:*     

`var isArr = !!area.length //返回布尔值true或者false `       

typeof操作符可以判断出number、boolean、string、function和undefined；   
 
判断Array使用Array.isArray(arr)；//兼容ie9及以上   

判断Array，不兼容ie6：     
*在iframe里判断父窗口的变量是否为一个数组时，就不能用instanceof，要用以下方法*      

```
function isArray(o){
    return ({}).toString.call(o) === "[object Array]"
    //return Object.prototype.toString.call(o) === "[object Array]"
}

isArray([1,2,3])
```   

判断null请使用myVar === null；   

判断某个全局变量是否存在用typeof window.myVar === 'undefined'；   

函数内部判断某个变量是否存在用typeof myVar === 'undefined'。   

null和undefined没有toString()方法   

123.toString()会当作浮点数看待所以报错，要特殊处理一下：   

```
123..toString(); // '123', 注意是两个点！
(123).toString(); // '123'
var a = 123; a.toString(); //'123'
```   

instanceof通过返回一个布尔值来指出，这个对象是否是这个特定类或者是它的子类的一个实例:   
  
判断对象，一切皆对象      

`(a.instanceof Object)&&!(a.instanceof Array)&&!(a instanceof Function)`       

判断数组：     

`(a.instanceof Object)&&(a.instanceof Array)`       

判断函数：       

`(a.instanceof Object)&&(a.instanceof Function)`        
  
<h3 id="17">Date</h3>   

获取系统当前时间，用：   
  
```  
var now = new Date();
now; // Tue Sep 11 2018 16:20:08 GMT+0800 (中国标准时间)
now.getFullYear(); // 2018, 年份
now.getMonth(); // 8, 月份，注意月份范围是0~11，8表示9月
now.getDate(); // 11, 表示11号
now.getDay(); // 2, 表示星期二
now.getHours(); // 16, 24小时制
now.getMinutes(); // 20, 分钟
now.getSeconds(); // 8, 秒
now.getMilliseconds(); // 832, 毫秒数
now.getTime(); // 1536654008832, 以number形式表示的时间戳
```   

*JavaScript的月份范围用整数表示是0~11，0表示一月，1表示二月……，所以要表示9月，我们传入的是8*            

创建一个指定日期和时间的Date对象，可以用：   

```
var d = new Date(2018, 8, 1, 20, 15, 30, 123);
d; // Sat Sep 01 2018 20:15:30 GMT+0800 (中国标准时间)
```   

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

JSON定死了字符集必须是UTF-8，json里的key要加引号，value也不能是function     
json有两种表示结构 对象和数组。[验证json](http://www.bejson.com/)   

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

第二个参数用于控制如何筛选对象的键值，可以是数组也可以是函数。    
如果我们只想输出指定的属性，可以传入Array        
要输出得好看一些，可以加上参数，控制结果中的缩进和空白符:    

`JSON.stringify(xiaoming, ['name', 'skills'], '  ');`   

传入一个函数，这样对象的每个键值对都会被函数先处理：    

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
调用toJSON且能通过它取到有效值，第二个参数就无效了。        

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
把json字符串解析为原生js值        

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

在将日期字符串转换成Date对象时用：     

```
var obj = {
	a:1,
	b:2,
	c:[3,4,5,6],
	rel:new Date(2018,11,5)	
}

var str = JSON.stringify(obj) //"{"a":1,"b":2,"c":[3,4,5,6],"rel":"2018-12-04T16:00:00.000Z"}"

var objtext = JSON.parse(str,function(key,value){
	if(key == "rel"){
		return new Date(value)
	}else{return value}
}) //{a: 1, b: 2, c: Array(4), rel: Wed Dec 05 2018 00:00:00 GMT+0800 (中国标准时间)}

console.log(objtext.rel.getFullYear()) //2018
```   

eval()把json字符串转换为对象    

```
var str = "{'name':'json'}"
var obj = eval("("+str+")")
```   
      
<h2 id="19">面向对象编程</h2>   

面向对象三个主要特点：封装继承和多态    

研究下狗，关注它的咬人和叫。封装狗的类**ES6**：      

```
class Dog{
    //狗会叫
    bark(){
        music.paly('wang')
    }
    //狗会咬人
    bite(man){}
    constructor(age){
        //每只狗有年龄
        this.age = age
    }
}
```

然后研究哈士奇，继承了狗这个类，有父类的行为，也有自己的行为：     

```
class Husky extends Dog{
    constructor(age){
        super(age)
    }
    //显示奇怪的表情
    showSpecialFace(){
        show()
    }
}

var aHusky = new Husky(3)
aHusky.bite('you')
```

哈士奇也会叫，但有自己的独特声音，同样是叫的行为，哈士奇有自己的特点，这个就是多态：     

```
class Husky extends Dog{
    //有自己独特的声音
    bark(){
        music.play('wolf')
    }
    constructor(age){
        super(age)
    }
    //显示奇怪的表情
    showSpecialFace(){
        show()
    }
}

var aHusky = new Husky(3);
aHusky.bark(); // wolf
```

<h3 id="20">创建对象和原型继承</h3>   

原型链和constructor    

```
var Person = function(name){this.name = name}
Person.prototype.getName = function(){return this.name}
var zyf = new Person('zheng')
zyf.getName() //zheng
```   

js创建对象的时候，都有一个__proto__的内置对象，用于指向创建他的函数的原型对象prototype,我们把这个由__proto__串起来直到Object.prototype.__proto__为null的链条叫做原型链。    

```
zyf.__proto__ === Person.prototype //true
Person.prototype.__proto__ === Object.prototype //true
Object.prototype.__proto__ === null //true
```   
  
原型对象prototype中都有个预定义的constructor属性，用来引用他的函数对象，这是循环引用    
JavaScript对每个创建的对象都会设置一个原型，指向它的原型对象。     

```
Person.prototype.constructor === Person //true
Function.prototype.constructor === Function //true
zyf.prototype === undefined //普通对象没有prototype但有__proto__属性和costructor        
```   
  
当我们用obj.xxx访问一个对象的属性时，js引擎先在当前对象上查找该属性，如果没有找到，就到其原型对象上找。    
如果还没有找到，就一直上溯到Object.prototype对象，最后，如果还没有找到，就只能返回undefined。   

如，创建一个Array对象：       

`var arr = [1, 2, 3];`     

其原型链是：    
arr ----> Array.prototype ----> Object.prototype ----> null    
Array.prototype定义了indexOf()、shift()等方法，因此你可以在所有的Array对象上直接调用这些方法。    

当我们创建一个函数时：            
           
`function foo() { return 0; }`          
           
函数也是一个对象，它的原型链是：     
  
`foo ----> Function.prototype ----> Object.prototype ----> null`    

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

*取消原型对象上的某个属性：*`delete Object.prototype.name`    

Mixin模式：     
解决多重继承方案，将多个继承对象上的属性拷贝到原型上：      

```
// mixin方法，接收一个构造函数和一个原型对象
var mixin = function(obj, mixins) {
  var newObj = obj; // 保存构造函数等待扩展原型链
  newObj.prototype = Object.create(obj.prototype); // 原型对象实例赋给新的函数的原型
  for (var key in mixins) {
    // 遍历原型对象上的属性
    if (mixins.hasOwnProperty(key)) {
      // 如果是对象是自身属性
      newObj.prototype[key] = mixins[key]; // 拷贝给新函数的原型
    }
  }
  return newObj; // 返回新的构造函数
};

// 要混入的原型对象
var mixinObj = {
  //一个属性为函数foo
  foo: function() {
    console.log('foo');
  }
};

 // 构造函数
var MyFunc = function() {
  console.log('bar');
};

var NewFunc = mixin(MyFunc, mixinObj); // mixin出一个新的构造函数
var newFunc = new NewFunc(); // 实例化
newFunc.foo(); // 输出了mixin上的foo
```   

上述实现方法存在问题：    
如果两个继承对象拥有相同属性名，只可保留一个。这里是被Mixin对象的方法的属性覆盖前一个。    

ES7提供了装饰器语法，可以对类进行修改，下面提供一个使用装饰器实现Mixin模式的实例：      
把mixinObj混入class A中    

```
function handleClass() {
  // 处理类
  for (let i = 0, l = mixins.length; i < l; i++) {
    // 遍历混入的对象
    const descs = getOwnPropertyDescriptors(mixins[i]); // 获取mixins的属性
    for (const key in descs) {
      // 遍历原型对象上的属性
      if (!(key in target.prototype)) {
        // 如果类上没有这个属性
        defineProperty(target.prototype, key, descs[key]); // 定义一个属性
      }
    }
  }
}
export default function mixin(...mixins) {
  // 输出这个方法
  return target => {
    // 返回一个对类包装的函数
    return handleClass(target, mixins);
  };
}

//调用
@mixin(mixinObj)
class A {}
```
   
<h3 id="21">class继承</h3>   

新的关键字class从 **ES6** 开始正式被引入到JavaScript中。class的目的就是让定义类更简单:   

```
class Student {
    constructor(name) { //constructor函数必须存在，接收实例化参数。
        this.name = name;
    }

    hello() {
        alert('Hello, ' + this.name + '!');
    }
    //定义一个静态方法，不需要实例化，直接用类调用
    static sayhello(){
        alert('hello')
    }
}
```    

class的定义包含了构造函数constructor和定义在原型对象上的函数hello()     
这样就避免了Student.prototype.hello = function () {...}这样分散的代码。   

最后，创建一个Student对象代码和前面章节完全一样：    

```
var xiaoming = new Student('小明');
xiaoming.hello();

Student.sayhello(); //直接调用静态方法
```    

用class定义对象的另一个巨大的好处是继承更方便了,简化原型链代码。       
   
原型继承的中间对象，原型对象的构造函数等等都不需要考虑了，直接通过extends来实现    
从Student派生一个PrimaryStudent：     

```
class PrimaryStudent extends Student {
    constructor(name, grade) {
        super(name); // 要先用super调用父类的构造方法,继承父类this对象
        this.grade = grade;
    }

    myGrade() {
        alert('I am at grade ' + this.grade);
    }
}

var s = new PrimaryStudent('tom',20);
s.hello() //调用继承的属性
s.myGrade() //调用PrimaryStudent类的属性
```     

*注意: PrimaryStudent的定义也是class关键字实现的，而extends则表示原型链对象来自Student。   
PrimaryStudent需要通过super(name)来调用父类的构造函数，否则父类的name属性无法正常初始化。   
PrimaryStudent已经自动获得了父类Student的hello方法，我们又在子类中定义了新的myGrade方法*    

<h3 id="43">设计模式</h3>     

策略模式：      

定义一系列的算法，把它们一个个封装起来，并且使它们可以相互替换。    

策略模式利用组合，委托等技术和思想，有效的避免很多if条件语句。   
策略模式提供了开放-封闭原则，使代码更容易理解和扩展。    
策略模式中的代码可以复用。    
   
计算奖金：   

```
var calculateBouns = function(salary,level) {
    if(level === 'A') {
        return salary * 4;
    }
    if(level === 'B') {
        return salary * 3;
    }
    if(level === 'C') {
        return salary * 2;
    }
};
// 调用如下：
console.log(calculateBouns(4000,'A')); // 16000
console.log(calculateBouns(2500,'B')); // 7500
```   

以上代码缺点如下：    
calculateBouns 函数包含了很多if-else语句。    
calculateBouns 函数缺乏弹性，假如还有D等级的话，那么我们需要在calculateBouns 函数内添加判断等级D的if语句；    
算法复用性差，如果在其他的地方也有类似这样的算法的话，但是规则不一样，我们这些代码不能通用。     

使用策略模式计算奖金：   

```
var obj = {
        "A": function(salary) {
            return salary * 4;
        },
        "B" : function(salary) {
            return salary * 3;
        },
        "C" : function(salary) {
            return salary * 2;
        } 
};
var calculateBouns = function(level,salary) {
    return obj[level](salary);
};
console.log(calculateBouns('A',10000)); // 40000
```   

策略模式指的是定义一系列的算法，并且把它们封装起来。    
策略模式不仅仅只封装算法，还可以用来封装一系列的业务规则，只要这些业务规则目标一致，我们就可以使用策略模式来封装它们     

策略模式表单效验：    

```
<form action="http://www.baidu.com/s" id="registerForm" method="post">
    <p>
        <label>请输入用户名：</label>
        <input type="text" name="userName"/>
    </p>
    <p>
        <label>请输入密码：</label>
        <input type="text" name="password"/>
    </p>
    <p>
        <label>请输入手机号码：</label>
        <input type="text" name="phoneNumber"/>
    </p>
    <input type="submit" value="确定">
</form>

// 策略对象
var strategys = {
    isNotEmpty: function(value,errorMsg) {
        if(value === '') {
            return errorMsg;
        }
    },
    // 限制最小长度
    minLength: function(value,length,errorMsg) {
        if(value.length < length) {
            return errorMsg;
        }
    },
    // 手机号码格式
    mobileFormat: function(value,errorMsg) {
        if(!/(^1[3|5|8][0-9]{9}$)/.test(value)) {
            return errorMsg;
        }
    } 
};

var Validator = function(){
    this.cache = [];  // 保存效验规则
};

Validator.prototype.add = function(dom,rules) {
    var self = this;
    for(var i = 0, rule; rule = rules[i++]; ){
        (function(rule){
            var strategyAry = rule.strategy.split(":");
            var errorMsg = rule.errorMsg;
            self.cache.push(function(){
                var strategy = strategyAry.shift();
                strategyAry.unshift(dom.value);
                strategyAry.push(errorMsg);
                return strategys[strategy].apply(dom,strategyAry);
            });
        })(rule);
    }
};

Validator.prototype.start = function(){
    for(var i = 0, validatorFunc; validatorFunc = this.cache[i++]; ) {
    var msg = validatorFunc(); // 开始效验 并取得效验后的返回信息
    if(msg) {
        return msg;
    }
    }
};

// 代码调用
var registerForm = document.getElementById("registerForm");
var validateFunc = function(){
    var validator = new Validator(); // 创建一个Validator对象
    /* 添加一些效验规则 */
    validator.add(registerForm.userName,[
        {strategy: 'isNotEmpty',errorMsg:'用户名不能为空'},
        {strategy: 'minLength:6',errorMsg:'用户名长度不能小于6位'}
    ]);
    validator.add(registerForm.password,[
        {strategy: 'minLength:6',errorMsg:'密码长度不能小于6位'},
    ]);
    validator.add(registerForm.phoneNumber,[
        {strategy: 'mobileFormat',errorMsg:'手机号格式不正确'},
    ]);
    var errorMsg = validator.start(); // 获得效验结果
    return errorMsg; // 返回效验结果
};

// 点击确定提交
registerForm.onsubmit = function(){
    var errorMsg = validateFunc();
    if(errorMsg){
        alert(errorMsg);
        return false;
    }
}
```   
     
访问者模式：    
   
事件监听就是一个访问者模式，一个典型的访问者模式可以这么实现：     
首先定义一个Input的类，初始化它的访问者列表：    

```
function Input(inputDom) {
  this.visitiors = {
    'click': [],
    'change': [],
    'special': []
  };
  this.inputDom = inputDom
}
```    
    
然后提供一个对外的添加访问者的接口：     

```
Input.prototype.on = function (eventType, callback) {
  if (typeof this.visitiors[eventType] !== 'undefined') {
    this.visitiors[eventType].push(callback)
  }
};

```   
   
使用者调用on。传递两个参数，一个是事件类型，即访问类型。另一个是具体的访问者，这里是回调函数。     
同时Input提供了一个删除访问者的接口：    

```
Input.prototype.off = function (eventType,callback) {
  var visitors = this.visitiors[eventType];
  if(typeof visitors !== 'undefined'){
    var index = visitors.indexOf(callback);
    if(index > 0){
      visitors.splice(index,1)
    }
  }
};
```   
  
这样Input就和访问者建立起了关系。    
或者说访问者已经成功的向接受者订阅了消息，一旦接收者收到了消息，会向他的访问者意义传递     

```
Input.prototype.trigger = function (eventType,event) {
  var visitor = this.visitiors[eventType];
  var eventFormat = processEvent(event);
  if(typeof visitor !== 'undefined'){
    for(var i = 0;i<visitor.length;i++){
      visitor[i](eventFormat)
    }
  }
}
```
   
trigger可能是用户调用的，也可能是底层的控件调用的。一旦有人触发trigger，接收者就会一一下发消息。    

事件还可以直接用于两个模块或者组件间的通信，当两个模块关系比较紧密，共同完成一个功能时，可以require进来。    
当两个模块功能比较独立，每个模块完成自己的功能，完成后需要通知另一个模块相应地做修改，那么就可以用事件的机制通知其他模块做修改      
即一个模块trigger一个自定义事件，另外一个模块监听这个事件。    

单例模式：     

例如定义一个Task类，实现他的单例，因为全局只有一个数组存放Task，如果有任务都放到列队里，按顺序执行：      

```
class Task{
    constructor(){
        this.tasks = []
    }
    draw(){
        var that = this;
        window.requestAnimationFrame(function(){
            if(that.tasks.length){
                var task = that.tasks.shift();
                task()
            }
        })
    }
    addTask(task){
        this.tasks.push(task);
    }
}
```

实现他的单例：     

```
var mapTask = {
    get:function(){
        if(!mapTask.aTask){
            mapTask.aTask = new Task();
            mapTask.aTask.draw();
        }
        return this.aTask;
    },
    add:function(task){
        mapTask.get().addTask(task)
    }
}
```

可以拥有不同业务的Task，不同业务互不影响。还可以再写个searchTask等。     
         
工厂模式：     

把创建交给一个工厂，使用者无需关心创建细节：     

```
var taskCreator = {
    createTask:function(type){
        switch(type){
            case 'map':
            return new MapTask();
            case 'search':
            return new SearchTask();
        }
    }
}

var mapTask = taskCreator.createTask('map');
```
    
<h2 id="22">浏览器</h2>   

<h3 id="23">浏览器对象</h3>   
   
页面加载顺序，从上到下，从外到内。   
先打印head再打印body的加载顺序   
  
window对象有innerWidth和innerHeight属性,获取浏览器窗口的内部宽度和高度。     
内部宽高是指除去菜单栏、工具栏、边框等占位元素后，用于显示网页的净宽高。   

window.onload 等价于 $(window).load(function(){})   
页面包含图片，所有元素加载完毕才执行，不能编写多个。   
   
$(function(){}) DOM结构绘制完毕执行，不必等加载完毕。可编写多个   
   
outerWidth和outerHeight属性，可以获取浏览器窗口的整个宽高   

navigator.appName：浏览器名称；   
navigator.appVersion：浏览器版本；   
navigator.language：浏览器设置的语言；   
navigator.platform：操作系统类型；   
navigator.userAgent：浏览器设定的User-Agent字符串。   

*注意：navigator的信息可以很容易地被用户修改，所以JavaScript读取的值不一定是正确的*     

screen.width：屏幕宽度，以像素为单位；   
screen.height：屏幕高度，以像素为单位；  
offsetWidth获取元素宽度，包括宽度和内边距和边框，得到的是一个数值，需要自己加单位。    
offsetLeft就是这个元素离左边的距离     

location对象表示当前页面的URL信息。例如，一个完整的URL：   

http://www.example.com:8080/path/index.html?a=1&b=2#TOP     

可以用location.href获取。要获得URL各个部分的值，可以这么写：   
   
```   
location.protocol; // 'http'   
location.host; // 'www.example.com'   
location.port; // '8080'   
location.pathname; // '/path/index.html'   
location.search; // '?a=1&b=2'   
location.hash; // 'TOP'
```   
       
要加载一个新页面，可以调用location.assign()。如果要重新加载当前页面，调用location.reload()方法非常方便。    

document对象表示当前页面。由于HTML在浏览器中以DOM形式表示为树形结构，document对象就是整个DOM树的根节点。   
document的title属性是从HTML文档中的title标签读取的，但是可以动态改变        

`document.title = '努力学习JavaScript!'; `    
   
`document.URL` 获取url         

`document.referrer`  返回载入当前文档的url [移动端返回上一页详解](https://www.cnblogs.com/baiyygynui/p/6426621.html)                     

`document.cookie` [读取到当前页面的Cookie详解](http://www.w3school.com.cn/js/js_cookies.asp)         

由于JavaScript能读取到页面的Cookie，而用户的登录信息通常也存在Cookie中，这就造成了巨大的安全隐患。   
这是因为在HTML页面中引入第三方的JavaScript代码是允许的。   
为了解决这个问题，服务器在设置Cookie时可以使用httpOnly，设定了httpOnly的Cookie将不能被JavaScript读取。    
这个行为由浏览器实现，主流浏览器均支持httpOnly选项，IE从IE6 SP1开始支持。    
为了确保安全，服务器端在设置Cookie时，应该始终坚持使用httpOnly。    
     
滚动条滚走距离兼容：        
*clientWidth和clientHeight同理*          

`var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;`     

求得一个div的宽度:           

`var num = Math.floor(document.documentElement.clientWidth/iPinW)`      
   
自动刷新两种方法：    

`<meta http-equiv="refresh" content="20;http://baidu.com">`              

```
function ref(){window.location.reload()}
setTimeout(ref,1000)
```   

防止别人把页面iframe嵌走：     

```
if(this != this.parent){
	top.location.href = "http://baidu.com"
	//top.location.href = window.location.href
}
```  
  
<h3 id="24">操作DOM</h3>    

获取DOM：    

在操作一个DOM节点前，我们需要通过各种方式先拿到这个DOM节点:     
document.getElementById()和document.getElementsByTagName()，以及CSS选择器document.getElementsByClassName()。   

[使用querySelector()和querySelectorAll()](https://www.cnblogs.com/xiaohuochai/p/5798014.html)：        
*注意：ie8以下版本不支持querySelector和querySelectorAll。IE8仅有限支持*         
*selector类方法非实时和在元素上调用参数仍然在整个文章中匹配*          

通过querySelector获取ID为q1的节点：     

`var q1 = document.querySelector('#q1');`

通过querySelectorAll获取q1节点内的符合条件的所有节点。结果是NodeList：      

`var ps = q1.querySelectorAll('div.highlighted > p');`    

关于转义：    

```
document.querySelector('.foo\\:bar')
<div class="foo:bar"></div>

document.querySelector('.foo\\\\bar')
<div class="foo\bar"></div>
```    
   
更新DOM：   

直接修改节点的文本，方法有两种：   

一种是修改innerHTML属性，可以修改一个DOM节点的文本内容，还可以直接通过HTML片段修改DOM节点内部的子树    
innerHTML会直接替换掉原来的所有子节点    

第二种是修改[innerText或textContent属性](https://www.cnblogs.com/wangwg1994/p/8412866.html)，这样可以自动对字符串进行HTML编码，保证无法设置任何HTML标签   
innerText不返回隐藏元素的文本，而textContent返回所有文本。另外注意IE9以下不支持textContent    

插入DOM：   

获得了某个DOM节点，想在这个DOM节点内插入新的DOM  

appendChild，把一个子节点添加到父节点的最后一个子节点：    
*[setAttribute()](http://www.w3school.com.cn/jsref/met_element_setattribute.asp)和[getAttribute()](http://www.w3school.com.cn/jsref/met_element_getattribute.asp)*                     
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

*注意：[children属性](http://www.runoob.com/jsref/prop-element-children.html)是一个只读属性，并且它在子节点变化时会实时更新。删除多个节点时，要注意children属性时刻都在变化。*     

<h3 id="25">操作表单和文件</h3>   

操作表单：    

HTML5新增了大量标准控件，常用的包括date、datetime、datetime-local、color等。     
它们都使用input标签。不支持HTML5的浏览器无法识别新的控件，会把它们当做type="text"来显示    

form表单默认method="get"    
post请求传递数据大，慢    
get请求浏览器地址栏都能看到    
get从服务器获取数据，能被缓存，可以添加书签，有长度限制。    
post提交数据给服务器，不能被缓存，不能添加书签，没有长度限制。    
    
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
这种情况通常对应用户输入有误，提示用户错误信息后终止提交form。   

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
如果需要服务器端处理，把字符串base64,后面的字符发送给服务器并用Base64解码就可以得到原始文件的二进制内容。*[文件操作与上传详解](https://github.com/zyf711/my-study/blob/master/html%2Bps-course.md#25)*                     

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

AJAX2:     

[XMLHttpRequest Level 2 使用指南](http://www.ruanyifeng.com/blog/2012/09/xmlhttprequest_level_2.html)
AJAX老版本存在以下问题，从而导致了ajax2的出现：     

只支持文本数据的传送，无法用来读取和上传二进制文件。    
传送和接收数据时，没有进度信息，只能提示有没有完成。      
受到"同域限制"（Same Origin Policy），只能向同一域名的服务器请求数据。      

ajax2的新特性：      

可以设置HTTP请求的时限。     
可以使用FormData对象管理表单数据。     
可以上传文件。         
可以请求不同域名下的数据（跨域请求）。            
可以获取服务器端的二进制数据。            
可以获得数据传输的进度信息。       

ajax操作往往用来传递表单数据。为了方便表单处理，HTML 5新增了一个FormData对象，可以模拟表单:      

```
//首先，新建一个FormData对象:     
`var formData = new FormData();`     

//然后，为它添加表单项:     
formData.append('username', '张三');
formData.append('id', 123456);

//最后，直接传送这个FormData对象。这与提交网页表单的效果，完全一样
xhr.send(formData);
```

FormData对象也可以用来获取网页表单的值:    

```
var form = document.getElementById('myform');
var formData = new FormData(form);
formData.append('secret', '123456'); // 添加一个表单项
xhr.open('POST', form.action);
xhr.send(formData);
```

新版XMLHttpRequest对象，不仅可以发送文本信息，还可以上传文件     
假定files是一个"选择文件"的表单元素（input[type="file"]），我们将它装入FormData对象:      

```
var formData = new FormData();
for (var i = 0; i < files.length;i++) {
    formData.append('files[]', files[i]);
}
//然后，发送这个FormData对象。
xhr.send(formData);
```

接收二进制数据（方法A：改写MIMEType）:     

老版本的XMLHttpRequest对象，只能从服务器取回文本数据，新版则可以取回二进制数据。        
这里又分成两种做法。较老的做法是改写数据的MIMEType，将服务器返回的二进制数据伪装成文本数据，并且告诉浏览器这是用户自定义的字符集:      

`xhr.overrideMimeType("text/plain; charset=x-user-defined");`    

然后，用responseText属性接收服务器返回的二进制数据:     

`var binStr = xhr.responseText;`     

由于这时，浏览器把它当做文本数据，所以还必须再一个个字节地还原成二进制数据:     

```
for (var i = 0, len = binStr.length; i < len; ++i) {
    var c = binStr.charCodeAt(i);
    var byte = c & 0xff;
}
```   

最后一行的位运算"c & 0xff"，表示在每个字符的两个字节之中，只保留后一个字节，将前一个字节扔掉。      
原因是浏览器解读字符的时候，会把字符自动解读成Unicode的0xF700-0xF7ff区段。       

接收二进制数据（方法B：responseType属性）:       

从服务器取回二进制数据，较新的方法是使用新增的responseType属性。     
如果服务器返回文本数据，这个属性的值是"TEXT"，这是默认值。较新的浏览器还支持其他值，也就是说，可以接收其他格式的数据。        

可以把responseType设为blob，表示服务器传回的是二进制对象:       

```
var xhr = new XMLHttpRequest();
xhr.open('GET', '/path/to/image.png');
xhr.responseType = 'blob';
```     

接收数据的时候，用浏览器自带的Blob对象即可:    

`var blob = new Blob([xhr.response], {type: 'image/png'});`     

注意，是读取xhr.response，而不是xhr.responseText。        
还可以将responseType设为arraybuffer，把二进制数据装在一个数组里:      

```
var xhr = new XMLHttpRequest();
xhr.open('GET', '/path/to/image.png');
xhr.responseType = "arraybuffer";
```

接收数据的时候，需要遍历这个数组:     

```
var arrayBuffer = xhr.response;

if (arrayBuffer) {
    var byteArray = new Uint8Array(arrayBuffer);
    for (var i = 0; i < byteArray.byteLength; i++) {
　　}
}
```
    
进度信息:     
新版本的ajax还增加了progress事件              
它分成上传和下载两种情况。下载的progress事件属于XMLHttpRequest对象，上传的progress事件属于XMLHttpRequest.upload对象。      
先定义progress事件的回调函数：      

```
xhr.onprogress = updateProgress;
xhr.upload.onprogress = updateProgress;
```    

然后，在回调函数里面，使用这个事件的一些属性:      

```
function updateProgress(event) {
　　　　if (event.lengthComputable) {
　　　　　　var percentComplete = event.loaded / event.total;
　　　　}
　　}
```

上面的代码中，event.total是需要传输的总字节，event.loaded是已经传输的字节。如果event.lengthComputable不为真，则event.total等于0。      

还有其他与之相关的五个事件，可以查看进度信息，请求时限：         
progress事件:正在传输事件。        
load事件：传输成功完成。          
abort事件：传输被用户取消。                
error事件：传输中出现错误。                 
loadstart事件：传输开始。               
loadEnd事件：传输结束，但是不知道成功还是失败。      
    
同源策略：    

限制不同源的读，不限制不同源的写。限制读即浏览器拦截请求结果。    
   
跨域：         

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
因为跨域请求只有在浏览器才会限制，其他的运行环境是不会有这个限制的。所以     
代理服务器再把结果返回，这样就遵守了浏览器的同源策略。这种方式麻烦之处在于需要服务器端额外做开发。    

第三种方式称为JSONP，它有个限制，只能用GET请求，并且要求返回JavaScript。     
这种方式跨域实际上是利用了浏览器允许跨域引用JavaScript资源。     

JSONP通常以函数调用的形式返回，例如，返回JavaScript内容如下：     

`foo('data');`     

这样一来，我们如果在页面中先准备好foo()函数，然后给页面动态加一个script节点，相当于动态读取外域的JavaScript资源，最后就等着接收回调了。     
以163的股票查询URL为例，对于URL：http://api.money.126.net/data/feed/0000001,1399001?callback=refreshPrice  你将得到如下返回：     

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
 
如果浏览器支持HTML5，那么就可以一劳永逸地使用新的跨域策略：CORS了。*ie9以上支持cors*               
CORS全称Cross-Origin Resource Sharing，是HTML5规范定义的如何跨域访问资源。     

假设本域my.com，外域sina.com，只要响应头Access-Control-Allow-Origin为  http://my.com  或者是*，本次请求就可以成功。    
可见，跨域能否成功，取决于对方服务器是否愿意给你设置一个正确的Access-Control-Allow-Origin     

子域跨父域：    

子域跨父域是支持的，但是需要显示的将子域的域名改成父域的    
子域mail.mysite.com访问mysite.com  在mail.mysite.com写入：     

`document.domain = 'mysite.com';`   

这样就可以和父域进行交互。但向父域发请求还是会跨域，因为这种更改domain只支持client side，并不是 client to server的。         

iframe跨父窗口：    

父域无法直接读取不同源的iframe的DOM内容以及监听事件，但iframe可以调用父窗口提供的API。     
iframe通过window.parent得到父窗口的window对象，父窗口定义一个全局对象供iframe调用。    

父窗口通过window.postMessage可以向不同源的iframe传递东西，iframe监听消息事件。     
*window.postMessage也适用于window.open打开的子窗口*     

父窗口http://localhost:8000向iframe http://server.com:9000/ 传递：     

```
window.onload = function(){
    //传递两个参数，第一个数据，第二个目标窗口即iframe地址
    window.frames[0].postMessage('hello',http://server.com:9000/);
}
```    

同时iframe即9000端口的页面监听message事件：      

```
window.addEventListener('message',receiveMessage);

function receiveMessage(event){
    var origin = event.origin || event.originalEvent.origin;
    if(origin !== 'http://localhost:8000') { retrun }
    console.log('receiveMessage' + event.data);
}
```   

第三方授权登录：     

例如FB的第三方授权登录，引入它的sdk.js，然后监听单击事件调一下它的FB.login的API，传一个回调函数给它。     
然后它会调用window.open弹出一个让用户授权的页面，点同意后，sdk会执行你的回调把用户的数据返还给你，     
拿到用户id等信息就可以去自己的后端发登录或者注册的请求。      

使用window.open弹出的跨域的子页面的数据传递：     

```
var ga = function ha(){
    ea.postMessage('_FB_' + fa + ca,da);
};
if(o.ie() == 8 || o.ieCompatibilityMode()){
    setTimeout(ga,0)
}else{
    ga()
}
```   

FB还提供第二种方法，用重定向方式，重定向到FB的授权页面时带上返回的参数，用户同意后再重定向到自己的页面。      
同样把相关数据党参数带到自己页面。    
在弹一个新窗口的同时，它会发一个请求，根据cookie的token查询用户是否授权过了，如授权了使用jsonp的方法直接执行回调。      
    
高性能Ajax包括:      
   
了解项目具体需求，选择正确的数据格式和与之匹配的传输技术。    

请求数据：    
XMLHttpRequest(XHR)    
动态注入脚本    
iframes    
Comet   
Multipart XHR   
   
```
var url = '/data.php';
var params = [
    'id=123456',
    'limit=20'
];

var req = new XMLHttpRequest();
req.onreadystatechange = function(){
    if( req.readyState === 4 ){
        var responseHeaders = req.getAllResponseHeaders();
        var data = req.responseText;
        //处理数据
    }
}
req.open( 'GET',url + '?' + params.join('&'),true );
req.setRequestHeader( 'X-Requested-With','XMLHttpRequest' ); //设置请求头信息
req.send(null);
```    
 
对于那些不会改变服务器状态，只会获取数据的请求，应该使用GET，经GET请求的数据会被缓存起来。   
只有当请求的URL加上参数的长度接近或超过2048个字符时，才应该用POST获取数据。      
   
动态脚本注入，能跨域请求数据。但提供的控制有限。不能设置请求头信息，参数也只能是GET方式。请求超时也不能设置。    

```
var scrEle = document.createElement('script');
    scrEle.src = 'abc.js';
    document.getElementsByTagName('head')[0].appendChild( scrEle );
```   
   
Multipart XHR:允许客户端只用一个http请求从服务器端传送多个资源   
缺点：获取的资源无法被缓存   
ie6,7不支持data:URL 和 readyState为3的状态(正在与服务器交互，传输过程。)    

```
var req = new XMLHttpRequest();
    req.open( 'GET','abc.php',true );
    req.onreadystatechange = function(){
        if( req.readyState === 4 ){
            splitImages( req.responseText ); //接收到结果由splitImages()处理
        }
    }
    req.send(null);

    //服务器端读取图片将图片转换为base64编码的字符串，之间用Unicode编码连接，然后返回给客户端。
    function splitImages(imageString){
        var imageData = imageString.split('\u0001');
        var imageElement = '';

        for( var i=0,len=imageData.length;i<len;i++ ){
            imageElement = document.createElement('img');
            imageElement.src = 'data:image/jpeg;base64,' + imageData[i];
            document.getElementById('container').appendChild(imageElement);
        }
    }
```   

发送数据：    
XMLHttpRequest    
beacons(图片信标)   
   
XMLHttpRequest以post方式回传数据：   

```
var url = '/data.php';
var params = [
    'id=934875',
    'limit=20'
];

function xhrPost(url,params,callback){
    var req = new XMLHttpRequest();
    req.onerror = function(){
        setTimeout(function(){
            xhrPost(url,params,callback);
        },1000);
    };
    req.onreadystatechange = function(){
        if( req.readyState == 4 ){
            if( callback && typeof callback === 'function' ){
                callback();
            }
        }
    };

req.open( 'POST',url,true );
req.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
req.setRequestHeader('Content-Length',params.length);
req.send(params.join('&'));
}
```   
   
[beacons](http://www.php.cn/js-tutorial-378259.html)：向服务器回传数据最快且最有效的方式。   
缺点：能接收到的响应类型有限。如需要返回大量数据，用XHR。如果只关心数据发送到服务器，可以用信标技术    
   
并没有创建img元素或插入到DOM   
服务器接收到数据并保存，无须向客户端发送回馈，因此没有图片会实际显示。	   
  
```
var url = '/abc.php';
var params = ['step=2','time=123456'];
( new Image() ).src = url + '?' + params.join('&');
```   
   
数据格式：XML,XPath,json,jsonp,html,自定义格式    
   
XML：   

```
//把每一个值都放到标签的属性上，文件尺寸会变小，解析也容易的多
<users total="4">
    <user id="1-id001" username="alice" realname="alice smith" email="alice@sina.com" />
    <user id="2-id001" username="bom" realname="bom smith" email="bom@sina.com" />
    <user id="3-id001" username="zhe" realname="zhe smith" email="zhe@sina.com" />
</users>

//把特定XML响应解析成一个对象
function parseXML(responseXML){
    var user = [];
    var userNodes = responseXML.getElementsByTagName('user');
    for( var i=0,len=userNodes.length;i<len;i++ ){
        user[i] = {
            id:userNodes[i].getAttribute('id'),
            username:userNodes[i].getAttribute('username'),
            realname:userNodes[i].getAttribute('realname'),
            email:userNodes[i].getAttribute('email')
        }
    };
    return user;
}
```   
   
XPath即为XML路径语言，它是一种用来确定XML（标准通用标记语言的子集）文档中某部分位置的语言。   
XPath解析XML文档比getElementsByTagName快许多。    
   
json：用js对象和数组直接编写的轻量级易于解析的数据格式。json数据被当成字符串返回。    

```
//普通写法
[
    {
        "id":"1-id001",
        "username":"alice", 
        "realname":"alice smith",
        "email":"alice@sina.com"
    },
    {
        "id":"2-id001",
        "username":"bom", 
        "realname":"bom smith",
        "email":"bom@sina.com"
    }
]

//可以把属性名简写，甚至可以去掉属性名用二维数组。这样可读性差但是文件会小很多：
[
    ["1-id001","alice","alice smith","alice@sina.com"],
    ["2-id001","bom","bom smith","bom@sina.com"]
]
```   
  
jsonp:使用动态脚本注入，json数据被当成另一个js文件并作为原生代码执行，而不是字符串。   
为实现这一点，数据必须封装在一个回调函数里。解析速度快，能跨域使用。   
   
```   
// 例如查CA1998航班
var flightHandler = function(data){
    alert('你查询的航班结果是：票价 ' + data.price + ' 元，' + '余票 ' + data.tickets + ' 张。');
};

// 提供jsonp服务的url地址（不管是什么类型的地址，最终生成的返回值都是一段javascript代码）
var url = "http://flightQuery.com/jsonp/flightResult.aspx?code=CA1998&callback=flightHandler";
var script = document.createElement('script');
script.setAttribute('src', url);
document.getElementsByTagName('head')[0].appendChild(script);

//jquery实现
$(function(){
    $.ajax({
            url: "http://flightQuery.com/jsonp/flightResult.aspx?code=CA1998",
            dataType: "jsonp",
            jsonp: "callback",//传递给请求处理程序或页面的，用以获得jsonp回调函数名的参数名(一般默认为:callback)可以不写。
            jsonpCallback:"flightHandler",//自定义的jsonp回调函数名称，默认为jQuery自动生成的随机函数名，也可以写"?"，jQuery会自动为你处理数据,可以不写。
            success: function(json){
                alert('您查询到航班信息：票价： ' + json.price + ' 元，余票： ' + json.tickets + ' 张。');
            },
            error: function(){
                alert('fail');
            }
        });
    });

    $.getJSON('http://flightQuery.com/jsonp/flightResult.aspx?code=CA1998&callback=?', function(json) {
            alert('您查询到航班信息：票价： ' + json.price + ' 元，余票： ' + json.tickets + ' 张。');
    });
```   
   
html:服务器端可以构建好整个html再传回给客户端，js直接innerHTML插入页面，但html作为数据格式，既缓慢又臃肿。   
   
自定义格式：使用XHR或动态脚本注入获取，用split()解析。 解析大数据集比jsonp略快，尺寸更小，但是可读性差。   
   
缓存数据，避免发送不必要请求：   
在服务端：设置HTTP头信息以确保你的响应会被浏览器缓存    
如果希望缓存ajax，必须使用GET方式发送请求，和在响应中发送正确的http头部信息。    
在客户端：把获取到的信息存储到本地，避免再次请求。     
第一种技术使用简单好维护，第二种给前端最大控制权。    

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

<h3 id="51">fetch</h3>      

XMLHttpRequest(XHR)和Fetch是浏览器的原生API                
由于原来的XMLHttpRequest不符合关注分离原则，且基于事件的模型在处理异步上已经没有现代的Promise等那么有优势。因此Fetch出现来解决这种问题。             
使用 window.fetch 函数可以代替以前的 $.ajax、$.get 和 $.post。          

[fetch浏览器支持情况](https://caniuse.com/#search=fetch)              
[fetch相关介绍1](https://segmentfault.com/a/1190000011433064)           
[fetch相关介绍2](https://www.jianshu.com/p/35123b048e5e)              

<h3 id="28">Canvas</h3>    

Canvas是HTML5新增的组件，它就像一块幕布，可以用JavaScript在上面绘制各种图表、动画等：    
Canvas除了能绘制基本的形状和文本，还可以实现动画、缩放、各种滤镜和像素转换等高级操作。     

如果要实现非常复杂的操作，考虑以下优化方案:    
通过创建一个不可见的Canvas来绘图，然后将最终绘制结果复制到页面的可见Canvas中；    
尽量使用整数坐标而不是浮点数；    
可以创建多个重叠的Canvas绘制不同的层，而不是在一个Canvas中绘制非常复杂的图；    
背景图片如果不变可以直接用img标签并放到最底层。    

canvas简单示例：      

```
function cnvs_getCoordinates(e){
    x = e.clientX;
    y = e.clientY;
    document.getElementById("xycoordinates").innerHTML = "Coordinates: (" + x + "," + y + ")";
}
 
function cnvs_clearCoordinates(){
    document.getElementById("xycoordinates").innerHTML = "";
}

window.onload = function(){
    var c = document.getElementById("canvas");
    var cxt1 = c.getContext("2d");
    c.width = 400
    c.height = 200

    cxt1.fillStyle = "#ff0000";
    cxt1.fillRect(0,0,150,75); //上面的 fillRect方法拥有参数 (0,0,150,75)。意思是：在画布上绘制 150x75 的矩形，从左上角(0,0)开始

    cxt1.moveTo(10,18);
    cxt1.lineTo(150,50);
    cxt1.lineTo(10,50);
    cxt1.lineTo(10,18);
    cxt1.strokeStyle = "#0000ff"; //strokeStyle 控制绘出颜色
    cxt1.stroke(); //stroke()绘制出通过 moveTo() 和 lineTo() 方法定义的路径。默认颜色是黑色。

    cxt1.fillStyle = "#000";
    cxt1.beginPath();
    cxt1.arc(70,16,15,0,Math.PI*2,true); //arc() 方法创建弧/曲线（用于创建圆或部分圆） 圆中心坐标是前两个参数，这里是70,16 圆大小是第三个参数，这里是15
    cxt1.closePath();
    cxt1.fill(); // 填充背景颜色，如果换成stroke() 就是没背景颜色的圆,渐变一般用stroke()

    cxt1.font = "12px Verdana";
    // 创建渐变
    var gradient = cxt1.createLinearGradient(0,0,c.width,0);
        gradient.addColorStop("0","magenta");
        gradient.addColorStop("0.5","blue");
        gradient.addColorStop("1.0","red");
    // 用渐变进行填充
    cxt1.strokeStyle = gradient;
    cxt1.strokeText("119026244",20,96);

    var gradient2 = cxt1.createLinearGradient(0,0,170,0);
        gradient2.addColorStop("0","magenta");
        gradient2.addColorStop("0.5","blue");
        gradient2.addColorStop("1.0","red");
        cxt1.strokeStyle = gradient2;
        cxt1.lineWidth = 5;
        cxt1.strokeRect(100,80,80,16); //strokeRect(x, y, width, height) 按照指定的位置和大小绘制一个矩形的边框（但并不填充矩形的内部）线条颜色和线条宽度由 strokeStyle 和     lineWidth 属性指定。

    var gradient3 = cxt1.createLinearGradient(0,0,175,50);
        gradient3.addColorStop(0,"#ff0000");
        gradient3.addColorStop(1,"#00ff00");
        cxt1.fillStyle = gradient3;
        cxt1.fillRect(10,100,140,80);

    var img = new Image()
    img.src="http://news.baidu.com/z/resource/r/image/2014-05-21/bea6f003509e0c698bca6462dcbbaac4.jpg"
    img.onload = function(){
        cxt1.drawImage(img,190,0,100,100); //想控制图片宽高，用后边两个参数，这里是100，100  drawImage(image,sourceX,sourceY,sourceWidth,sourceHeight,destX,destY,destWidth,destHeight)
        cxt1.drawImage(img,190,130,40,40);
        cxt1.drawImage(img,240,130,40,40,240,130,40,40);
}

}

<div id="coordiv" style="width:200px;height:200px;border:1px solid #c3c3c3;" onmousemove="cnvs_getCoordinates(event)" onmouseout="cnvs_clearCoordinates()"></div>
<div id="xycoordinates"></div>

<canvas id="canvas" style="border:1px solid #c3c3c3;"></canvas>
```

<h2 id="29">jQuery</h2>     

[jquery官网](http://jquery.com/)                  
[jquery中文文档](https://www.jquery123.com/)             

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

jquery创建和加入：    

`var o = $('<div>').addClass('abc').appendTo($('#main'))`    
  
jq里outerWidth()是包含内边距和边距的    
   
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
   
<h2 id="33">高性能JavaScript(ES5)</h2>   
   
<h3 id="34">加载和执行</h3>  

浏览器执行js时，页面的下载和渲染都会等待脚本解析和执行。    
   
ie8和高版本浏览器可以并行下载js文件，但下载过程仍然会阻塞其他资源下载，比如图片。并且页面也要等待都解析和执行完才行。    

由于js会阻塞页面其他资源下载，所以建议把js放页面底部。   
   
减少页面中脚本数量，可以改善性能。    

js动态创建script。文件的下载和执行过程不会阻塞页面其他进程:    

```
var script = document.createElement('script');
script.type = 'text/javascript';
script.src = 'file.js'
doucment.getElementsByTagName('head')[0].appendChild(script);
```
   
在html5中 document.getElementsByTagName('head')[0] === document.head    
   
XHR对象下载js文件，通过创建动态script元素将代码注入页面：    
   
```
var xhr = new XMLHttpRequest();
xhr.open('get','files.js',true);
xhr.onreadystatechange = function(){
    if(xhr.readyState == 4){
        if(xhr.status >= 200 && xhr.status < 300 || xhr.status == 304){
            var script = document.createElement('script');
            script.text = xhr.responseText;
            document.body.appendChild(script);
        }
    }
}
xhr.send(null);
```  
  
css文件本身是并行下载，不会阻塞页面其他进程。   
  
LABjs文件加载器。RequireJS 和 SeaJS 模块加载器。   
    
<h3 id="35">数据存储</h3>   
  
数据存储位置会很大程度上影响其读取速度。     
4种基本数据存储位置：字面量，本地变量，数组元素，对象成员。     
   
局部变量存在于作用域链的起始位置，所以访问最快，全局变量总处在作用域链最末端，最慢。   
   
document是全局对象，引用了三次，所以先保存到局部变量里。由于数量原因，不会有太大差异，如果有几十个全局变量，性能就会改善许多:   

```
function initUI(){
    var doc = document,
        bd = doc.body,
        links = doc.getElementsByTagName('a'),
        i = 0,
        len = links.length

    while( i<len ){
        update( links[i++] )
    }

    doc.getElementById('btn').onclick = function(){
        start()
    }

    bd.className = 'active'
}
```
   
改变执行环境作用域的方法:with和try-catch   
   
访问document对象的属性非常快，而访问局部变量则变慢了，最好避免使用with:   

```
    function initUI(){
        with( document ){
            var bd = body,
                links = getElementsByTagName('a'),
                i = 0,
                len = links.length

            while( i<len ){
                update( links[i++] )
            }

            getElementById('btn').onclick = function(){
                alert('done')
            }

            bd.className = 'active'
                
        }
    }
```   
   
当try捕捉到错误，会把异常对象堆入一个变量对象，并置于作用域首位，catch内部局部变量将会放在第二个作用域对象中。    
handleError(ex)是子句中唯一执行代码，且没有局部变量访问，作用域临时改变就不会影响代码性能。    

```
    try{
        methodThat()
    }catch(ex){
        handleError(ex); //委托给错误处理器函数
    }
```   
   
动态作用域：with语句，try-catch子句，包含eval()的函数    
   
对象成员包括属性和方法：   
当一个被命名的成员引用了一个函数，该成员就被称为一个方法。   
当一个被命名的成员引用了非函数类型的成员，就被称为属性。   
   
对象两种成员类型：实例成员和原型成员   
   
解析对象成员，当school.toString()被调用时，从对象实例开始找，没有继续搜索原型，直到找到并执行。   
可以用hasOwnProperty()方法判断对象是否包含特定实例成员，对象是否包含特定属性，可以用in   

```
var school = {
    name:'zheng',
    age:'32'
}

alert(school.hasOwnProperty('name')); // true
alert(school.hasOwnProperty('toString')); // false

alert('age' in school) //true
alert('toString' in school) //true
```   
   
在同一个函数里边不要多次查找读取同一个对象成员:   

```
function hasCla(ele,cN1,cN2){
    var curcN = ele.className;
    return curcN == cN1 || curcN == cN2
}
```   
  
<h3 id="36">DOM编程</h3> 

DOM文档对象模型。用于操作XML和HTML文档的程序接口，浏览器中，主要用来与html文档打交道，在浏览器中用js实现的。   

减少访问DOM的次数，把运算尽量留给ECMAscript   

```
    function innerLoop(){
        var content = '';
        for(var count=0;count<15000;count++){
            content += 'a';
        }
        document.getElementById('here').innerHTML = content
    }

    innerLoop()
```
  
innerHTML对比DOM方法   
在对性能有苛刻要求的操作中更新一大段HTML。推荐innerHTML   
  
老版本ie下，字符串合并性能并不是最好的，可以用数组来合并大量字符串。   
      
节点克隆：克隆已有节点，用element.clone()代替document.createElement()      
先创建需要重复的元素，重复的在用clone()，这样做运行结果会稍微快一点。      

HTML集合：包含了DOM节点引用的类数组对象。底层文档对象更新时，他也会自动更新。     

```
document.getElementsByName()
document.getElementsByClassName()
document.getElementsByTagName()
document.images
document.links
document.forms
document.forms[0].elements //页面中第一个表单的所有字段
```   
  
通常情况遍历一个较小的集合，缓存length就够了：   

```
function loopLen(){
    var coll = document.getElementsByTagName('a'),
        len = coll.length;
    for( var count=0;count<len;count++ ){
        console.log(count)
    }
}
```  
  
遍历数组比遍历集合快，如果先将集合元素拷贝到数组再访问他的属性会更快。    
不过额外步骤会带来消耗。开始要遍历次集合，因此应评估在特定环境下使用数组拷贝是否有帮助。    

将HTML集合拷贝到普通数组：    

```
function HtmlToArray(coll){
    for(var i=0,a=[],len=coll.length;i<len;i++){
        a[i] = coll[i]
    }
    return a;
}
var html = document.getElementsByTagName('a')
var arr = HtmlToArray(html)	
``` 
   
使用children代替childNodes会更快，因为children能区分元素节点。集合项更少。   
  
重排和重绘可能代价非常昂贵，应合并多次对DOM和样式的修改，然后一次处理掉：    
*[cssText的使用](https://www.cnblogs.com/majingyi/p/6840818.html)*             

```
var ele = document.getElementById('mydiv');
ele.style.borderLeft = '1px';
ele.style.borderRight = '2px';
ele.style.padding = '3px';

var ele = document.getElementById('mydiv');
ele.style.cssText += '; border-left:1px;';

var ele = document.getElementById('mydiv');
ele.className = 'active';
```

批量修改DOM：    
*[cloneNode()](http://www.w3school.com.cn/tiy/t.asp?f=jsref_node_clonenode)方法克隆所有属性以及它们的值*            

```
<ul id="mylist"></ul>

var data = [
    {
        'name':'zheng',
        'url':'http://baidu.com'
    },
    {
        'name':'ji',
        'url':'http://www.sina.com.cn'
    }
];

// 更新数据函数
function appendData(appendToele,data){
    var a ='',li = '';
    for( var i=0,max=data.length;i<max;i++ ){
        a = document.createElement('a');
        a.href = data[i].url;
        a.appendChild(document.createTextNode(data[i].name));
        li = document.createElement('li');
        li.appendChild(a);
        appendToele.appendChild(li);
    }
}

// 方法一：data数组中每一个新条目附加到DOM都会导致重排
var ul = document.getElementById('mylist');
appendData( ul,data )

// 方法二：改变display属性减少重排
var ul = document.getElementById('mylist');
ul.style.display = 'none';
appendData( ul,data )
ul.style.display = 'block';	

//方法三：创建修改节点的备份
var old = document.getElementById('mylist');
var clone = old.cloneNode(true);
appendData( clone,data );
old.parentNode.replaceChild( clone,old );

// 方法四：代码片段，只触发一次重排，只访问一次实时DOM
var fragment = document.createDocumentFragment();
appendData( fragment,data );
document.getElementById('mylist').appendChild(fragment);
```     
           
<h3 id="37">算法和流程控制</h3>  

代码的组织结构和解决具体问题的思路是影响代码性能的主要因素    
  
for循环 while do-while

优化循环，减少对象成员及数组成员以及数组项的查找次数     

for循环继续执行的条件，是;;之间的这个判断要为真      

```
for( var i=0,len=items.length;i<len;i++ ){...}

var j=0;
count = items.length;
while( j<count ){...} 

var k=0;
num = items.length;
do{...} while( k<num );
```
   
倒序循环是编程语言中一种通用的性能优化方法。颠倒数组的顺序来提高性能   
倒序循环，并把减法操作放在控制条件中，每个条件只是简单和0比较，控制条件与true比较时，转化下是不是true就好了。      

```
for( var i=items.length;i--; ){...}

var j = items.length;
while( j-- ){...}

var k = items.length-1;
do{...} while( k-- );
```   

*while循环没退出条件，或打断点没打好一直运行，都有可能把浏览器搞挂了。*      
   
达夫设备：一种限制迭代次数的模式       

if-else,switch,查找表   

if-else适用于判断两个离散值或几个不同的值域   

优化if-else   
确保最可能出现的条件放在首位   
减少条件判断次数，避免判断太长。 可以把if-else嵌套起来使用。    
  
switch判断多于两个离散值时更佳   

查找表：使用数组或普通对象来构建，当单个键和值之间存在映射时，适合用。   
比如索引和值正好对应：   

```
var results = ['res1','res2'...]
return results[value]

//代替switch的
switch( value ){
    case 0:
    return res1;
    case 1:
    return res2
    ...
    default:
    return res10
}
```   
 
递归：   

```
var factorial = (function f(num){
if(num<=1){
return 1;
}else{
return num*arguments.callee(num-1);
}
})(4)
alert(factorial)//24 (4*3*2*1)    
```   

递归遇到调用栈大小限制,调用栈错误。   
检查代码中的递归实例：   
函数调用自身：function re(){re()};re()   
两个函数相互调用:function first(){second()};function second(){first()};first();   
不正确终止条件。   
算法中含太多层递归。   
递归改为用迭代实现。   

递归就是自己调自己，如：         

```
var ids = [34112,98325,68125];
(function sendRequest(){
    var id = ids.shift();
    if(id){
        $.ajax({url:'/get'data:{id}}).always(function(){
            console.log('finished');
            sendRequest();
        })
    }else{
        console.log('all finished')
    }
})()
```

递归实现一个查DOM的功能：      

```
function getElementById(node,id){
    if(!node){return null}
    if(node.id === id){return node}
    for(var i=0;i<node.childNodes.length;i++){
        var found = getElementById(node.childNodes[i],id);
        if(found){return found}
    }
    return null;
}
getElementById(document,'d-cal');
```

chrome浏览器的查DOM是使用非递归实现的：     

```
function getElementById(node,id){
    while(node){
        if(node.id === id){return node}
        node = nextElement(node)
    }
    return null
}

function nextElement(node){
    if(node.children.length){
        return node.children[0]
    }
    if(node.nextElementSibling){
        return node.nextElementSibling
    }
    while(node.parentNode){
        if(node.parentNode.nextElementSibling){
            return node.parentNode.nextElementSibling
        }
        node = node.parentNode
    }
    return null;
}
```

多次调用递归函数时，为避免重复工作，可以用一种递归算法的memoization技术:   

```
function mem(n){

if( !mem.cache ){
    mem.cache = {
        '0' : 1,
        '1' : 1
    };
}

if( !mem.cache.hasOwnProperty(n) ){
    mem.cache[n] = n * arguments.callee(n-1);					
}

    return mem.cache[n]
}

console.log( mem(6) )
console.log( mem(5) )
console.log( mem(4) )
```  

<h3 id="38">快速响应用户界面</h3>     

浏览器UI线程：   
用于执行js和更新用户界面的进程。线程的工作基于一个简单的队列系统，任务会被保存在队列中，直到进程空闲。    
一旦空闲，队列中的下一个任务就被提出运行。任务可以是js代码，UI更新，包括重绘和重排。    

单个js操作花费的总时间不应当超过100毫秒，过长运行时间会导致UI更新出现延迟，影响用户体验。         
复杂js任务不能在100毫秒完成，最理想方法是让出UI线程控制权，使UI可以更新。这时可以考虑用定时器。     

setTimeout(),setInterval()接收相同参数，要执行的函数和执行前的等待时间。     
第二个参数是多少毫秒后向UI列队插入一个函数的js任务：      
表示任务何时被添加到列队，不是一定会在这段时间后执行。会等列队其他前边任务执行完再执行。计算时间是从setTimeout()调用时开始算。     

*注意：js定时器延迟通常差几毫秒，建议最小值25毫秒，再小的延时，对一些UI更新来说不够用。*    
    
记录代码运行时间：    

```
var start = +new Date();
var stop;
(function(a) {
console.log(a);
})(123)
stop = +new Date();
alert( stop-start );
```   
   
js中可以在某个元素前使用+号，这个操作是将该元素转换成Number类型，如果转换失败，那么将得到 NaN。    
所以 +new Date将会调用 Date.prototype 上的 valueOf 方法，Date.prototype.value 方法等同于 Date.prototype.getTime() 。         
所以下列代码效果相同：     

```
console.log(+new Date);

console.log(new Date().getTime());

console.log(new Date().valueOf());

console.log(new Date() * 1);
```   
   
for循环时间过长，主要原因里边执行代码复杂，或者数组太大。    
为避免锁定浏览器给用户带来的糟糕体验，可以使用定时器处理数组:    

```
var todo = items.concat() //克隆数组items
setTimeout(function(){
    process( todo.shift() );
    if( todo.length ){
        setTimeout( arguments.callee,25 )
    }else{
        callback( items )
    }
},25)
```   

*注意：使用定时器处理数组的副作用是处理数组的总时长增加了。*

<h3 id="39">编程实践</h3>   
  
setTimeout(),setInterval()第一个参数传函数，不要传字符串。    

使用object，array直接量：    

```
var myobj = {name:'zheng',age:32};
var arr = ['zheng',32,true,null];
```    
   
避免重复工作：   
延迟加载:    
如能力监测，当一个函数在页面多次调用时，只检测一次，速度会很快。(第一次会慢一些)：    

```
function addHandler(target,eventType,handler){
        if( target.addEventListener ){
            addHandler = function(target,eventType,handler){
                target.addEventListener(eventType,handler,false);
            };
        }else{
            addHandler = function(target,eventType,handler){
                target.attachEvent("on" + eventType,handler);
            };
        }
        addHandler(target,eventType,handler)
    };

    var content = document.getElementById('content');
    addHandler(content,'click',function(){
        alert('succes')
    })
```   
   
条件预加载:   
会在脚本加载时就检测，适用于一个函数马上就要被用到，整个页面频繁出现的场合。   

```
var addHandler = document.body.addEventListener ?
                 function(target,eventType,handler){
                    target.addEventListener(eventType,handler,false);
                 }:
                 function(target,eventType,handler){
                    target.attachEvent("on" + eventType,handler);
                 };

var removeHandler = document.body.addEventListener ?
                    function(target,eventType,handler){
                        target.removeEventListener(eventType,handler,false);
                    }:
                    function(target,eventType,handler){
                        target.detachEvent("on" + eventType,handler);
                    };
```   
   
在进行数学计算时，考虑使用直接操作数字的二进制形式的位运算。   
用位操作符可提升js的速度，使用位运算代替纯数字操作：   
数字操作对2取模：   

```
for( var i=0,len=div.length;i<len;i++ ){
    if( i%2 ){ //注意索引0开始
        div[i].className = 'even'
    }else{
        div[i].className = 'odd'
    }
}	
```   

位运算操作：     
偶数最低位0，奇数最低位1，要给定数字与1进行按位与运算。此数是偶数，结果就是0，奇数结果就是1 。   

```
for( var i=0,len=div.length;i<len;i++ ){
    if( i&1 ){
        div[i].className = 'even'
    }else{
        div[i].className = 'odd'
    }
}	
```   
   
位掩码。用于处理同时存在多个布尔选项的情形。   
如果有许多选项保存在一起并频繁检查，位掩码有助提高整体性能。   

```
var oa = 1;
var ob = 2;
var oc = 4;
var od = 8;
var oe = 16;
var opt = oa | ob | oc;
if(opt & oa){...}
if(opt & od){...}
```   
   
无论js代码如何优化，都不会比js引擎提供的原生方法更快。比如如下，每个值都是预先计算好的：  

```
Math.PI // π常量值   
Math.SQRT2 // 2的平方根   
Math.abs(num) // 返回num的绝对值   
Math.sqrt(num) // 返回num的平方根   
Math.random() 方法可返回介于 0 ~ 1 之间的一个随机数。
```   

生成n到m的随机数      
`Math.random()*(m-n)+n | 0`       
要想到m就是     
`Math.random()*(m-n+1)+n | 0`      
   
<h3 id="40">构建并部署高性能js应用</h3>   

合并多个js文件减少http请求数。   
压缩js文件。   
服务器端压缩js(Gzip编码)。   
设置http响应头缓存js文件，通过文件名增加时间戳避免缓存问题。   
使用CDN内容发布网络，通过向最近的用户传输内容，极大地减少网络延时。   
    
实现前端自动化   
   
开发流程，主要是下面四点：   
开发环境初始化   
样式、脚本的依赖管理   
文件编译、压缩合并、混淆   
自动化测试 等等   
   
自动化工具：   
开发环境初始化-----------------yeoman(yo、grunt、bower)   
样式、脚本的依赖管理----------bower   
文件编译、压缩合并、混淆-----grunt，gulp及其插件   
自动化测试 等等----------------karma等   
浏览器构建JavaScript模块脚本的前端工具---Webpack   
   
版本控制 ：git   
项目模块化   
虚拟机 vargrant   
   
性能分析：在脚本运行期间定时执行各种函数和操作，找出需要优化的部分。   
   
网络分析：检查图片样式表和脚本的加载过程，以及他们对页面整体加载和渲染的影响。   
   
在浏览器上进行的优化可能适用与其他浏览器，也可能产生相反效果。   
性能分析工具确保优化的时间花费在系统最慢且影响大多数浏览器的地方，而不是去判定哪些函数或操作缓慢。   
   
使用未压缩过的脚本进行调试和性能分析。   
   
DOMContentLoaded事件触发的时刻，表示DOM树已经解析完成并准备就绪。和jq的ready()事件一样，jq也是这么做的，兼容就用，不兼容用其他方法实现       
window的load事件触发的时刻，表示DOM准备就绪后所有外部资源也已经加载完成。   
   
chrome控制台开发人员工具：     
http://user.qzone.qq.com/47935982/blog/1440062099    
   
<h3 id="44">js书写优化</h3>   
  
按强类型风格写代码：   
定义变量的时候要指明类型：   

```
var num = 0,
    str = '',
    obj = null;
```   

不要随意改变变量的类型：    

```
var num = 5;
num = '-' + num;
```   

第一行是一个整数，第二行变成了一个字符串。好的做法是再定义一个字符串变量：   

```
var num = 5;
var sign = '-' + num;
```   
   
函数的返回类型应该是确定的，不应该是：    

```
function getPrice(count){
    if( count < 0 ){
        return ''
        }else{
            return count * 100;
        }
}
```   
 
可以return ''修改为return -1 如果类型确定，解释器也不用做一些额外工作。否则可能触发“优化回滚”   
优化回滚，即编译器已经给这个函数编译成一个函数了，突然发现类型变了，又得回滚到通用的状态，再重新生成新函数。      

减少作用域查找：    
不要让代码暴露在全局作用域下：   

```
<script>
var map = document.querySelector('#my-map');
map.style.height = '600px';
</script>
```   

在一个script标签里边，代码的上下文都是全局作用域，查找属性相对比较慢。map变量第二行使用的时候，需要在全局作用域查找变量。     
假设map是在一个循环里使用，那就会涉及效率问题。应把它处理成一个局部作用域：    

```
<script>
!function(){
var map = document.querySelector('#my-map');
map.style.height = '600px';
}()
</script>
```    
    
需要频繁使用某个全局变量，可以用一个局部变量缓存一下：    

```
var url = '';
var location = window.location;
if( location.protocal === 'https:' ){
    url = 'wss://xxx.com' + location.pathname + location.search;
}
```   
   
避免 == 的使用：   
代码中的比较在用 === 的时候都是false:     

```
null == undefined
'' == 0
0 == ''
0 == '0'
'\t\r\n' == 0
new String('abc') == 'abc'
new Boolean(true) == true
true == 1
```     
    
合并表达式：    
用三目运算符取代简单的if-else：   

```
function getPrice(count){
    return count < 0 ? -1 : count * 100
}
```   
    
使用ES6简化代码：   
使用箭头函数取代小函数     
使用class    
字符串拼接     
块级作用域变量     

<h3 id="54">单元测试</h3>     

[浅谈前端单元测试](https://yq.aliyun.com/articles/610101#),[一步一步实现现代前端单元测试](https://blog.csdn.net/Frank_YLL/article/details/79058616)

前端测试：为检测特定的目标是否符合标准而采用专用的工具或者方法进行验证，并最终得出特定的结果。         
    
对于前端开发过程来说，这里的特定目标就是指我们写的代码，而工具就是我们需要用到的测试框架(库)、测试用例等。      
检测处的结果就是展示测试是否通过或者给出测试报告，这样才能方便问题的排查和后期的修正。       
            
<h2 id="41">正则表达式</h2>    

正则表达式通常被用来检索、替换那些符合某个模式(规则)的文本      

exec() 方法用于检索字符串中的正则表达式的匹配。     
返回一个类似数组的对象，其中存放匹配的结果等。如果未找到匹配，则返回值为 null。   

使用for in可以知道它的属性:     
index表示匹配在原字符串中的索引；    
input则是表示输入的字符串；     
0表示只有一个匹配结果。可以用下标0来引用这个匹配结果。这个数量可能改变。通过返回值的length属性来得知匹配结果的总数量。

```
function execReg(reg,str){
	var result = reg.exec(str);
	document.write('index:' + result.index + '<br/>' + 'input:' + result.input + '<br/>');
	for(i=0;i<result.length;i++){
		document.write('result['+i+']:' + result[i] + '<br/>')
	}
}

var reg = /\w/
var str = 'bbs.babcd.comgde'
execReg(reg,str)
```    

exec方法对正则表达式的更新     
exec方法在返回结果对象的同时，还可能会更新原来的正则表达式，这就要看正则表达式是否设置了g修饰符     
如果设置了g，那么exec执行之后会更新正则表达式的lastIndex属性，表示本次匹配后，所匹配字符串的下一个字符的索引    
下一次再用这个正则表达式匹配字符串的时候就会从上次的lastIndex属性开始匹配    

```
function execReg(reg,str){
	var result = reg.exec(str);
	document.write('index:'+ result.index + '<br/>' + 'input:' + result.input +'<br/>');
	for(i=0;i<result.length;i++){
		document.write('resutl['+i+']:' + result[i] + '<br/>')
	}
}

var reg = /\w/
var str = 'bcs.babcd.comgde'
execReg(reg,str)
execReg(reg,str)
// 以上两次结果一样，因为没有设置全局g

function execReg(reg,str){
	var result = reg.exec(str);
	document.write('index:'+ result.index + '<br/>' + 'input:' + result.input +'<br/>');
	for(i=0;i<result.length;i++){
		document.write('resutl['+i+']:' + result[i] + '<br/>')
	}
}

var reg = /\w/g
var str = 'bcs.babcd.comgde'
execReg(reg,str)
execReg(reg,str)
//以上就会不一样了
```    
   
匹配内容中指定的字母文字等:     
{1}匹配一个,{2}匹配连续的两个,{3,4}匹配连续的三个或者四个,有四个就不匹配三个，匹配最多的        
{1,} 匹配最少一个，多了不限。z+ 和 z{1,} 是一个意思    


```
function execReg(reg,str){
	var result = reg.exec(str)
	console.log(result)
}

var reg = /这{1,}/    
var str = 'zz这这这这zzzjijzk这jj'
execReg(reg,str)
```

```
var result = /z{3,4}/.exec('zjijzkjjzzzzzzz')
console.log(result)
```    
  
z? 和 z{0,1} 是一个意思。如果希望正则尽量少地匹配字符，那么就可以在表示数字的符号后面加上一个?       
组成如下的形式：{n,}?, *?, +?, ??, {m,n}?  这里匹配一个 这 如果第一个不是这 那么匹配就是空    

```
var result36 = /这?/.exec('这这这这zzzjijzk这jj') 
console.log(result36)
```   

z* 和 z{0,} 是一个意思,匹配最少零个，就是说开头第一个如果不是，匹配就是空。开头要是是，有几个匹配几个。     

```
var result37 = /这*/.exec('这这这这zzzjijzk这jj')
console.log(result37)
```    

匹配开始^，结尾$ 。/^开头,结尾$/     
  
```
var result1 = /^正/.exec('正则表达式')
console.log(result1)

var result2 = /表达式$/.exec('正则表达式')
console.log(result2)
```    

.(点)会匹配字符串中除了换行符\n之外的所有字符的第一个   

```
var result3 = /./.exec('正则表达式')
console.log(result3)
```   

.+就是匹配所有，包括一个空格，一个下滑线，和一个破折号。但是遇到换行符\n 后边的就不匹配了    

```
var result4 = /.+/.exec('正则表达式') 
console.log(result4)
```    

.点匹配除换行符以外的任意字符  *星号贪婪量词，尽可能匹配多次   

```
var str = '<p>1</p><div>啊</div><p>2</p><div>啊啊</div><p>3</p><div>啊啊啊</div>'
var reg = /<p>.*<\/p>/
var a = str.replace(reg,'abc')
console.log(a) // abc<div>啊啊啊</div>
```    

*?惰性量词,匹配尽可能少的字符。   

```
var str = '<p>1</p><div>啊</div><p>2</p><div>啊啊</div><p>3</p><div>啊啊啊</div>'
var reg = /<picture>.*?<\/p>/
var a = str.replace(reg,'abc')
console.log(a) //abc<div>啊</div><p>2</p><div>啊啊</div><p>3</p><div>啊啊啊</div>
```   
   
二选一，正则表达式中的或，"|"    
```
var result5 = /^b|^c/.exec('cblueidea')
console.log(result5)

var result6 = /^b|c.+/.exec('dcainiao')
console.log(result6)  //结果是cainiao 因为匹配的是c.+
```   
  
字符集合[] 如[abc]表示a或者b或者c中的任意一个字符   
```
var result7 = /^[abc]/.exec('bbs.abc.def')
console.log(result7)
```   

在字符集合中使用如下的表示方式:[a-z],[A-Z],[0-9]，分别表示小写字母，大写字母，数字    

```
var result8 = /^[a-zA-Z][a-zA-Z0-9_]+/.exec('tes中文t')
console.log(result8) //tes
```   

反字符集合[^abc] ^在正则表达式开始部分的时候表示开头的意思，但是在字符集合中，它表示的是类似“非“的意思。    
例如[^abc]就表示不能是a，b或者c中的任何一个。[^0-9]表示非数字，[^a-z]表示非小写字母，以此类推。    

```
var result9 = /[^abc]/.exec('ccabeebecagad')
console.log(result9)  //e
```   

边界与非边界 \b表示的边界的意思，也就是说，只有字符串的开头和结尾才算数。与\b对应\B表示非边界    
```
var result10 = /c\b/.exec('ddaacaafdsfc') //匹配开始是c,就要 /\bc/ 这么写
console.log(result10)  //c
```   

数字与非数字  \d表示数字的意思，相反，\D表示非数字   

```
var result11 = /[\d]/.exec('fasdfasf4213dfa2')  
console.log(result11) //4

var result12 = /\D/.exec('531中文fsdsr5')  //返回第一个非数字
console.log(result12)  //中
```   

\f匹配换页符，\n匹配换行符，\r匹配回车，\t匹配制表符，\v匹配垂直制表符。     
\s匹配单个空格，等同于[\f\n\r\t\v]。\S表示非空格字符   
[\s\S]匹配换行在内的任意字符     

```
var result13 = /\s.+/.exec('this is a test')
console.log(result13) //is a test

var result14 = /\S+/.exec('this is a test')
console.log(result14) //this
```   

\w表示单词字符，等同于字符集合[a-zA-Z0-9_]    
\W表示非单词字符，等效于[^a-zA-Z0-9_]    

```
var result15 = /\w+/.exec('blue123中文dd')
console.log(result15) //blue123

var result16 = /\W+/.exec('blue123中文dd啊啊')
console.log(result16) //中文

var result17 = /(\w)(\w)/.exec('blueidea')
console.log(result17) //bl,b,l
//bl是整个正则匹配的内容，b是第一个括号里的子正则表达式匹配的内容，l是第二个括号匹配的内容。
```   

"\1"是等同于“第1个括号匹配的内容”，而不是“第一个括号的内容”。      
   
```
var result18 = /(\w)\1/.exec('bbs.blueidea.com')
console.log(result18) //返回bb,b

var result19 = /(\w)(\w)\2\1/.exec('woow')
console.log(result19) //返回woow,w,o
```  

使用形如(?:pattern)的正则就可以避免保存括号内的匹配结果   
```
var result20 = /^(?:b|c).+/.exec('blue')
console.log(result20) //返回blue，就不返回b了

var result21 = /^(?:b|c)\1/.exec('blue')
console.log(result21) //返回null 由于根本就没有记录括号内匹配的内容，自然没有办法反向引用了
```    

正向预查，意思就是：要匹配的字符串，后面必须紧跟着pattern (?=pattern)      
形式(?!pattern)和?=恰好相反，要求字符串的后面不能紧跟着某个pattern    
括号里的内容并不参与真正的匹配，只是检查一下后面的字符是否符合要求而已      

```
var result22 = /cainiao(?=1)/.exec('cainiao1ef')
console.log(result22) //cainiao

var result23 = /cainiao(?!1)/.exec('cainiao1')
alert(result23) //返回null 因为紧挨着1了
```   

正则表达式的修饰符 全局匹配，修饰符g /pattern/g          
不区分大小写，修饰符i        
行首行尾，修饰符m     

```
var result24 = /b/i.exec('Bule')
console.log(result24)  //返回B

var result25 = /^b/m.exec('test\nblue')
alert(result25) //m修饰符的作用是修改^和$在正则表达式中的作用，让它们分别表示行首和行尾。 在此返回b     
```

test方法仅仅检查是否能够匹配str，并且返回布尔值以表示是否成功。    

```
var result26 = /9/.test('de9abdfde')
console.log(result26)

var result27 = /a/.test('fbfbfl')
console.log(result27)
```   

match方法:str.match(reg);与正则表达式的exec方法类似。      
返回一个类似数组的对象，有input和index属性。但是如果正则表达式设置了g修饰符，就不提供input和index    
*注意：exec方法是reg.exec(str) 而match方法是str.match(reg)*     

```
function matchReg(reg,str){
	var result = str.match(reg);
	if(result){
		document.write('index:' + result.index + '<br/>' + 'input:' + result.input +'<br/>');
		for(i=0;i<result.length;i++){
			document.write('result['+i+']:' + result[i] + '<br/>')
		}
	}else{
		alert('null:匹配失败')
	}
}
var reg = /\w/g
var str = 'bcs.babcd.comgde'
matchReg(reg,str)
matchReg(reg,str)
```    
 
replace方法: str.replace (reg,'new str');     

```
var result28 = 'baidu.com.bai'.replace(/\w+/g,'word')
console.log(result28)
```   

replace函数中使用$引用子正则表达式匹配内容。就像在正则里使用\1来引用第一个子正则表达式所匹配的内容一样。    
在replace函数的替换字符里也可以使用$1来引用相同的内容。    

```
var result29 = 'abc.def.ghi'.replace(/(\w+).(\w+).(\w+)/,'$1.$1.$1')
console.log(result29) 

var result30 = 'cainiao gaoshou'.replace(/(\w+)\s(\w+)/,'$2 $1')
console.log(result30)

var result31 = 'cainiao gaoshou'.replace(/(\w+)\s(\w+)/,'$$ $$')
alert(result31) // 想要用$这个字符的话，需要写成$$
```   

把里边的数字都替换成加1的。如果是9就变成0：      

`'312355902'.replace(/\d/g,function(k){return ((k|0)+1)%10})  //如果想9变10，就去掉对10取余`      

求余就是a除以b看余多少。如果a小于b。余数就是a本身。 一个整数对2取余，不是1就是0     

search方法 str.search(reg); 返回正则表达式第一次匹配的位置。    

```
var result32 = 'blueidea'.search(/idea/)
console.log(result32) //4

var result33 = 'abc.def.ghi'.search(/\W/)
console.log(result33) //3
```   

split返回分割后的数组:        

```
var result34 = 'abc.def.ghi'.split(/\W/)
console.log(result34) //返回abc,def,ghi

var result35 = 'http://baidu.com'.split(/\W/)
console.log(result35) //字符串被分为了有5个元素的数组，其中包括了两个为空字符串的元素。
```   

正则表达式工作原理：    
    
1.编译：   
当通过直接量或者RegExp()创建一个正则表达式对象时，浏览器会验证表达式，转化成一个原生代码程序，用于执行匹配。   
建议把正则对象赋值给一个变量，可以避免重复执行编译。   
   
2.设置起始位置：确定目标字符串的起始搜索位置。   
   
3.匹配正则表达式字元：逐个检查文本和正则表达式模式。   
当一个特定字元匹配失败，会回溯到之前尝试匹配的位置，然后尝试其他可能的路径。     
     
4.匹配成功或失败。     
       
回溯是匹配过程的基础，正则强大的根源，一不小心就会失控。     
当正则匹配目标字符串时，遇到量词(*,+?,{2,}),正则需要决定匹配更多字符。遇到分支(|操作)，需要选择一个尝试匹配。    

`/h(ello|appy) hippo/.test('hello there, happy hippo')`     

首先查找第一个h。接下来，子表达式(ello|appy)选择最左侧检查ello是否匹配字符串中下一个字符。    
匹配成功，进而匹配随后的空格，由于hippo中的h无法匹配下一个字符串中的t。匹配无法继续。此时，    
会回溯到最近的决策点（匹配完首字符h后面的位置），尝试匹配第二个分支。匹配没有成功，也没有更多可选项。    
所以正则表达式认为从第一个字符开始匹配是不能成功的，从第二个字符开始重新尝试，也就是从e。没有找到h。   
直到在第14个字符的位置匹配到happy中的h。再进入分支未匹配到ello，但是回溯到第二分支后匹配整个字符串成功。   

提高正则表达式效率方法：    
    
正则慢的原因通常是匹配失败的过程慢，而不是匹配成功的过程慢。   
   
正则最好以简单，必须的字元开始。起始标记尽可能快速测试并排除明显不匹配的位置。比如可以用：    
锚^或$ 特定字符 字符类\d等 单词边界\b 避免以分组或选择元字开头 /one|two/的顶层分支    
    
尽量具体化匹配模式   
    
减少分支(|)数量，缩小分支范围：      
   
[cb]at 替代 cat|bat   
rea?d  替代 red|read   
r(?:ed|aw) 替代 red|raw   
[\s\S] 替代 (.|\r|\n)   
    
暴露必须的字元：如锚^  /^(ab|cd)/ 而不是/(^ab|^cd)/    
   
使用合适的量词：如贪婪和惰性量词的选择使用   
   
把正则表达式赋值给变量。   
   
将复杂的正则拆分为简单的片段。   
   
不要一味使用正则，比如只是搜索字符串是否以分号结尾：      
逐个测试整个字符串，每当检测到分号，就移动到下一个$，检查是否是末尾，不匹配就继续搜索。反而效率不高。   

```
var abc = /;$/.test(str) 
var abc = str.charAt( str.length-1 ) == ';'//要快于正则
```   

<h2 id="42">事件</h2>   
   
<h3 id="55">事件概述</h3>                                                                           
  
事件就是文档或浏览器窗口中发生的一些特定的交互瞬间    
js与html之间交互便是通过事件实现的     

DOM0级事件处理程序    
传统方式，比如`btn.onclick=function(){}`                   
取消btn的onclick事件：`abc.onclick = null`    

```
<input type="text" onclick="showValue()">
function showValue(){alert(this.value)} 

//结果是undefined,因为this指向的是window。可以改写下:

<input type="text" onclick="showValue(this)">
function showValue(obj){alert(obj.value)}
```   

```
//只会弹出world
document.querySelector('#div1).onclick = function(ev){alert('hello')}
document.querySelector('#div1).onclick = function(ev){alert('world')}
```
   
DOM2级事件处理程序    
addEventListener() attachEvent()多个的时候执行顺序不同。    
addEventListener()先绑定的先执行    
attachEvent()先执行最近绑定的，并且this指向window   
还有区别就是是否加on，参数个数    
attachEvent()不支持捕获，addEventListener()第三个参数true时支持   
attachEvent绑定，想恢复this指向，用call       

addEventListener()第二个参数是函数名，不加()。并且还允许把有handleEvent方法的对象作为参数：  
removeEventListener()参数要和绑定一致      

```
var obj = {
	name:'foo',
	handleEvent:function(){
		alert('click'+this.name)
	}
}
document.body.addEventListener('click',obj,false)

var obj = {
	bind:function(){document.body.addEventListener('click',this,false)},
	handleEvent:function(){alert('123')}	
}
obj.bind()
```   
   
事件捕获：     
一个事件发生后，从window出发，不断经过下级节点直到目标节点，之间过程就是捕获阶段，而所经过的节点都会触发对应事件。      
*IE不支持捕获，但对于委托而言，冒泡已经足够了。*
window--document--body--div    

事件冒泡：     
事件到达目标节点后，会沿着捕获阶段路线返回，通过冒泡机制，所有子节点的事件都会被其父级节点所捕获。      
div-body-document-window      

当事件被触发时，事件监听函数接收一个event事件对象，包含了事件发生时相关的详细信息：      

兼容写法：      

```
event?event:window.event
event.target || event.srcElement
```  

事件委托：    
将事件交给父元素或祖先元素处理的方式，叫事件委托。     

事件委托能：    
提高性能，每一个函数都会占用内存空间，只添加一个事件处理程序，占内存空间更少。     
动态监听未来元素。          
       
从文档中删除带有事件处理程序的元素时，可通过纯粹的DOM操作，比如[removeChild](http://www.runoob.com/jsref/met-node-removechild.html)，[replaceChild](http://www.runoob.com/jsref/met-node-replacechild.html)方法。       
但更多是用innerHTML替换页面中的一部分，如果用innerHTML来删除，那么原来的事件处理程序极有可能无法垃圾回收。   

对于列表项点击触发，可以逐一对li进行处理事件绑定，但一旦li较多，就会有性能问题，可用事件委托绑定到ul上，event中的target判断来执行代码：     
[js中的事件委托或是事件代理详解](https://www.cnblogs.com/liugang-vip/p/5616484.html)

```
<input type="button" name="" id="btn" value="添加" />
<ul id="ul1">
    <li>111</li>
    <li>222</li>
    <li>333</li>
    <li>444</li>
</ul>

window.onload = function(){
    var oBtn = document.getElementById("btn");
    var oUl = document.getElementById("ul1");
    var aLi = oUl.getElementsByTagName('li');
    var num = 4;
    
    //事件委托，添加的子元素也有事件
    oUl.onmouseover = function(ev){
        var ev = ev || window.event;
        var target = ev.target || ev.srcElement;
        if(target.nodeName.toLowerCase() == 'li'){
            target.style.background = "red";
        }
        
    };
    oUl.onmouseout = function(ev){
        var ev = ev || window.event;
        var target = ev.target || ev.srcElement;
        if(target.nodeName.toLowerCase() == 'li'){
            target.style.background = "#fff";
        }
        
    };
    
    //添加新节点
    oBtn.onclick = function(){
        num++;
        var oLi = document.createElement('li');
        oLi.innerHTML = 111*num;
        oUl.appendChild(oLi);
    };
}
```  
另一个事件委托例子：    

```
<a>link</a>
<b>bold</b>
<i>italic</i>

function showMe(ev) { 
    alert(ev.target.tagName);
}
document.querySelector('body').addEventListener('click', showMe, false);
```
     
DOM3级事件处理程序    
如焦点事件，鼠标事件，键盘事件等    

鼠标事件：    
客户端坐标事件：event.clientX event.clientY     
该位置为鼠标相对于客户端视口的位置，不包括页面滚动的距离，不表示鼠标在页面上的位置。    
     
页面坐标位置：event.pageX evnet.pageY    
获取页面位置，此坐标为页面本身，而非视口左边与顶边计算的。    
在没有滚动条的时候，与client的值相等。    
*注意page在ie8和以下不兼容，可通过client和滚动信息计算出来。 scrollLeft scrollTop*    

```
if(event.pageX === undefined){
	event.pageX = event.clientX + ( document.body.scrollLeft || document.docuementElement.scrollLeft )
}
```   
   
屏幕坐标位置screenX screenY    
   
keydown keyup事件event对象的keyCode属性中包含一个代码显示所按的键盘键              

[其他一些常用事件](http://www.w3school.com.cn/jsref/dom_obj_event.asp)：       

浏览器窗口事件：    
load 页面加载完时触发      
unload 窗口关闭时触发      
resize 窗口大小改变时触发    
beforeunload 窗口关闭之前触发     

鼠标事件：    
mousedown 鼠标按钮被按下。          
mousemove 鼠标被移动。          
mouseout 鼠标从某元素移开。           
mouseover 鼠标移到某元素之上。           
mousewheel 滚动鼠标滚轮       
mouseup	鼠标按键被松开。       

键盘事件：       
keydown 某个键盘按键被按下。         
keypress 某个键盘按键被按下并松开。            
keyup 某个键盘按键被松开。           

表单事件：     
blur 在对象失去焦点时发生的事件。       
foucs在对象获得焦点时发生的事件         
change 在对象的值发生改变时触发的事件         
input 当表单元素获得用户输入时触发     
select 当元素内容被选中时触发      
submit 当提交表单时触发    

拖放事件：        
drag 当元素被拖动时触发     
dragstart 拖动操作开始时触发    
dragover 在有效拖放目标上正在被拖动时触发     
dragenter 元素已被拖到目标区域时触发    
dragleave 当元素离开有效目标时触发    
dragend 在拖动操作末端触发    
drop 当被拖元素放置在目标区域时触发     

<h3 id="56">移动端事件</h3> 

主要包括三类事件：触摸事件，手势事件，传感器事件。     

触摸事件：     

touchstart 当手指触摸屏幕时触发     
touchmove 当手指在屏幕上滑动时触发    
touchend 当手指离开屏幕时触发   
touchcancel 当系统停止跟踪触摸时触发      

通过event对象传递信息：      
触摸事件event对象是TouchEvent类型，除了包含一般事件，还有：      
touches 表示当前跟踪的触摸操作touch对象的集合。     
targetTouched 当前事件目标上touch对象的集合。     
changeTouches 表示至上次触摸发生了改变的touch对象的集合。    

每个touch对象同样包含相关事件信息：    
clientX 触摸目标在视口中的X坐标   
clientY 触摸目标在视口中的Y坐标     
pageX 触摸目标在页面中的X坐标     
pageY 触摸目标在页面中的Y坐标     
screenX 触摸目标在屏幕中的X坐标     
screenY 触摸目标在屏幕中的Y坐标     
target 触摸的DOM节点       

```
var touch0 = null;
	document.body.addEventListener('touchstart', function (ev) {
		touch0 = ev.touches[0];
		console.log('touchstart');
        console.log(ev);
	});
	document.body.addEventListener('touchmove', function (ev) {
		var touch = ev.touches[0];
		var moveX = touch.clientX - touch0.clientX;
		var moveY = touch.clientY - touch0.clientY;
		console.log('move:', moveX, moveY);
	});
```

手势事件：     
对触摸事件的高级封装。      

gesturestart 当手势开始时触发，有2根或多跟手指触摸屏幕。     
gesturechange 当手势改变时触发，有2根或多跟手指触摸屏幕且发生移动。      
gestureend 当手势结束时触发，倒数第2根手指离开。      

event对象是GestureEvent类型，除了基础的信息外，还有：     
scale 缩放比例，默认为1，手指相对初识位置分散开，scale值增大，合拢缩短，scale值减小。     
rotation 旋转角度，手指间连线旋转的角度，默认值0.0 逆时针旋转为负，顺时针为正。     

传感器事件：     
一般用于判断设备在三维空间的位置。     

deviceorientation事件：    
提供设备物理方向信息，表示为一系列本地坐标系的旋角。      

提供event对象为DeviceOrientationEvent类型：        
alpha:在围绕z轴旋转时(左右旋转),y轴的度数差。        
beta:在围绕x轴旋转时(前后旋转)，z轴的度数差。       
gamma:在围绕y轴旋转时(扭转设备),x轴的度数差。      

如果将设备放置在水平表面上，屏幕顶端指向西方，则其方向信息：    

`{alpha:90,beta:0,gamma:0}`     

devicemotion事件：      
提供设备的加速信息。    

提供event对象为DeviceMotionEvent类型：     
acceleration:设备的加速度，包含x,y,z轴的3个值。     
accelerationIncludingGravity：设备的加速度，考虑重力加速度。    
interval：事件通知的时间间隔。    
rotationRate：设备旋转的速度。     

orientationchange事件：      
提供设备的旋转方向信息。     

event对象并未包含方向信息。      
当前设备通过screen.orientation.angle对象获取，0和180表示竖屏。90和270表示横屏。                  
而ios中通过window.orientation来获取设备方向，0和180表示竖屏。90和-90表示横屏。         

<h3 id="45">页面优化</h3>    
      
避免页面卡顿：     

失帧和帧率FPS：    
window系统刷新率，60HZ就是帧率fps，即一秒钟60帧。一秒钟的动画是由60幅静态图片连在一起的。60fps是动画播放比较理想和基础的要求。            
所以卡了，就是失帧或掉帧了。这可能是因为在渲染某些帧所花的时间比较长，导致停留在这些帧的时间较长，所以画面停顿了。      
   
页面渲染流程：    
60fps就要求1帧的时间为1s/60=16.67ms。浏览器显示页面的时候，要处理js逻辑，还要做渲染。每个执行片断不能超过16.67ms。    
实际上，浏览器自身支撑体系运行也需要消耗时间。所以留给我们差不多只有10ms。
在这10ms里浏览器做一些事情：     

`JavaScript => style => Layout => paint => composite`     
    
首先js做一些逻辑，触发样式变化，style把应用的样式规则计算好，把响应到的页面元素进行重新布局layout    
再把它画到内存的一个画布里，paint成了像素，最后把这个画布刷新到页面上，叫做composite。形成一帧。     
假设一帧花了50ms，那么此时的帧率就为1s/50ms=20fps     

掉帧分析：Chrome的timeline标签，勾上js profile和paint选项，单击记录按钮。 新版是Performance标签。自动记录。    
   
优化：减少layout，如能用transform就不使用postiton/width/height做动画，另外，减少layout的影响范围。     
简化DOM结构。另外，使用flex比使用float在重绘方面会有优势，flex需要重绘的元素比float少，使用flex布局做动画更流畅。     
   
加快页面打开速度：    
评价一个页面打开速度，可以用两个指标描述：一个是ready的时间，一个是load的时间。可以从Chrome的Network看到    
     
例如百度首页某一时刻：     
一共加载90.4kb。ready时间只有621ms。 就是说621ms之后这个页面就是布局完整可交互的了。finish时间比load长，是因为load完之后又去动态加载了其他js           
    
`67 requests | 90.4KB transferred | Finish:3.5s | DOMContentLoaded:621ms | Load:847ms`     

减少渲染堵塞：   

避免head标签js堵塞：所有放在head标签的css和js都会堵塞渲染。可以给script加defer属性。但只是异步加载，      
执行还是会在readystatechange变为Interactive后按顺序依次执行。另外，dafer在老浏览器ie6-9上表现行为不一致，有兼容问题。     
所以一般把js放在body后面就行了。    
    
减少head标签里的css资源：      
不要放太多的base64在css里：例如一张3k的图片转成base64体积变成了4k。    
    
原始图片是svg格式，hover图片和字体变色，如下代码，会导致hover的时候才去加载blue.svg，第一次hover的时候要等待图片下载后变蓝,    
但如果把svg变成内联，会导致html体积过大，同时对缓存也不利。可以考虑用图标字体，将svg转成字体icon：                

```
.img{
    background:url(black.svg) 0 0 no-repeat;
}
.img:hover{
    background:url(blue.svg) 0 0 no-repeat;
}
```   
   
把css写成内联的：    
如果css只有10k或者20k。写成内联也未尝不可。谷歌搜索和淘宝PC版就是这么干的。      
这样虽然对缓存不利，但对首次加载有很大作用。因为如果把css放到CDN上，为了得到这个css，首先需要域名解析，然后建立http/https连接，其次才是下载。            
做这些的时候可能早已把html中的css下载完了。究竟哪个更好，可以在Chrome控制台查看。具体问题具体分析。             

使用响应式图片：      
*[picture标签](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/picture)*              

```
<picture>
source srcset="banner_w1000.jpg" media="(min-width:801px)">
source srcset="banner_w800.jpg" media="(max-width:800px)">
<img src="banner_w800.jpg" alt="">
</picture>
```   

以上代码如果是用js动态插进去的，mac上的chrome会加载两张图，只有写在html里面，初始化页面才会只加载一张。     
可以用js判断浏览器支不支持srcset。如果支持就不写src属性了，不支持就不用写srcset了。    
picture必须有img标签，否则无法显示。对picture的操作也都是在img上。      

延迟加载图片：     
渲染页面的时候别把图片地址放到src上，放到一个data的属性中：    

```
<picture>
<source data-srcset="photo_w350.jpg 1x,photo_w640.jpg 2x">
<img data-src="photo_w350.jpg" src="about:blank" alt="">
</picture>
```
    
接下来位置判断，监听scroll事件，回调函数如下：     

```
showImage(leftSpace = 500){
    var scrollTop = $window.scrollTop();
    var $containers = this.$imgContainers,
for(var i = 0; i < $containers.length; i++){
        //如果快要滑到图片的位置了
        var $container = $containers.eq(i);        
        if($container.offset().top - scrollPosition < leftSpace){
            this.ensureImgSrc($container);
        }   
    }   
}
```    
   
ensureImgSrc函数把图片放出来     

```
ensureImgSrc($container){
   var $source = $container.find("source");   
   if($source.length && !$source.attr("srcset")){
        $source.attr("srcset", $source.data("srcset"));
    }   
    var $img = $container.find("img:not(.loading)");   
    if($img.length && $img.attr("src").indexOf("//") < 0){ 
        $img.attr("src", $img.data("src"));
        this.shownCount++;
    }
}
```   
    
并记录已经放出来的个数，这样可以做个优化，当图片全部都加载或者开始加载了，把scroll事件取消掉：     

```
init(){
    //初始化
    var leftSpace = 0;
    this.showImage(leftSpace);
    //滑动
    $window.on("scroll", this, this.throttleShow);
}

ensureImgSrc($container){
    //如果全部显示，off掉window.scroll    
    if(this.shownCount >= this.allCount){
        $window.off("scroll", this.throttleShow);
    }
}
```    
    
HTTP/2是HTTP协议的的第二个主要版本，使用于万维网。HTTP/2是HTTP协议自1999年HTTP 1.1发布后的首个更新，主要基于SPDY协议:     
优点在于对于一个域只建立一次TCP连接，使用多路复用传输多个资源，这样就不用使用雪碧图，合并js/css等技术减少请求数了。      

DNS预读取：    
一个网站可能会加载多个域的东西，例如使用了三个自己的子域名的服务，再使用了两个第三方CDN，再使用了百度统计，谷歌统计的代码。使用别的网站图片。     
可以用DNS预读取技术，加快打开速度，方法是在head标签里写几个link：     

```
<link rel="dns-prefecth" href="https://www.google.com">
<link rel="dns-prefecth" href="https://connect.facebook.net">
<link rel="dns-prefecth" href="https://staticxx.facebook.com">
```
   
如上，对以上几个网站提前解析DNS，由于它是并行的，不会堵塞页面渲染。可以缩短资源加载的时间。    
     
增强用户体验：      
Loading效果：     
Ajax请求只有0和100%的状态，所以只能做一个假的进度条，每次都先到60-80%的一个随机位置，请求回来之后再100%    
上传文件的进度条，上传文件能够返回上传进度，这个是Ajax2的特性，所以可以做一个真的进度条。    

单击和输入：
用户单击提交的时候，可以给按钮做一个效果，让人感觉按钮被按下去：     

```
button{
    background:#249bff; /*普通的蓝色*/
}
button:active{
    padding-top:3px;
    background:#3491df; /*更深的蓝色*/
}
```    
   
记住用户使用习惯：    
可以用本地存储实现，如果用户开了隐身模式，本地存储被禁掉。可以改成cookie，为此做一个兼容：     

```
setLocalData:function(key,value){
    if(Data.hasLocalStorage){
        window.localStorage[key] = value;
    }else{
        util.setCookie(key,value);
    }
}
```   
    
检查没有用的css/js:     
Chrome打开控制台-->点击‘Sources’-->ctrl+shift+p-->在命令窗口输入coverage-->在下边新出现的窗口中点击左上角刷新按钮。      

使用chrome 浏览器自带截屏:      

方法一（鼠标拉框选择截图）    
ctrl+shift+c      
按住ctrl 后拖动鼠标     

方法二      
F12     
ctrl+shift+p     
输入“capture”     
选择以下任意          
capture full size screenshot【整个网页】            
capture node screenshot【节点网页】          
capture screenshot【当前屏幕】           
    
检查内存泄漏：   
只要存在一个引用就不会进行GC回收，有些DOM节点没有append到DOM中，但是存在引用指向它，它就是一个分离的DOM节点。     
这个时候就发生了DOM内存泄漏：    

```
var detached = null;
button.on('click',function(){
    detached = document.createElement('div');
})
```   
    
这个时候可以拍一张内存堆的快照，Chrome会把这些分离DOM节点用黄色标出来    
切到Memory标签-->profiles选择heap snapshot 点take snapshot 在summary里写detached
          
<h2 id="46">前端与计算机基础</h2>         
     
<h3 id="47">理解WebSocket和TCP/IP</h3> 

一个完整的HTTP请求过程：    
域名解析 —>     
与服务器建立连接(TCP连接) —>     
发起HTTP请求 —>     
服务器响应HTTP请求，浏览器得到html代码 —>        
浏览器解析html代码，并请求html代码中的资源（如js、css、图片） —>      
浏览器对页面进行渲染呈现给用户     

域名解析：     
以Chrome浏览器为例：      
首先会搜索浏览器自身的DNS缓存（缓存时间比较短，大概只有1分钟，且只能容纳1000条缓存）     
看自身的缓存中是否有https://www.cnblogs.com 对应的条目，而且没有过期，如果有且没有过期则解析到此结束。     
使用 chrome://net-internals/#dns 来进行查看自身缓存      

如果浏览器自身的缓存里面没有找到对应的条目，那么Chrome会搜索操作系统自身的DNS缓存,如果找到且没有过期则停止搜索解析到此结束。     
在命令行下使用 ipconfig /displaydns 来进行查看操作系统自身缓存      

如果在Windows系统的DNS缓存也没有找到，那么尝试读取hosts文件（位于C:\Windows\System32\drivers\etc），看看这里面有没有该域名对应的IP地址，如果有则解析成功。       

如果在hosts文件中也没有找到对应的条目，浏览器就会发起一个DNS的系统调用，      
就会向本地配置的首选DNS服务器（一般是电信运营商提供的，也可以使用像Google提供的DNS服务器）发起域名解析请求       

TCP连接的建立：      
客户端的请求到达服务器，首先就是建立TCP连接，三次握手：         

Client首先发送一个连接试探，ACK=0 表示确认号无效，SYN = 1 表示这是一个连接请求或连接接受报文，同时表示这个数据报不能携带数据，     
seq = x 表示Client自己的初始序号（seq = 0 就代表这是第0号包），这时候Client进入syn_sent状态，表示客户端等待服务器的回复       

Server监听到连接请求报文后，如同意建立连接，则向Client发送确认。      
TCP报文首部中的SYN 和 ACK都置1 ，ack = x + 1表示期望收到对方下一个报文段的第一个数据字节序号是x+1，同时表明x为止的所有数据都已正确收到      
（ack=1其实是ack=0+1,也就是期望客户端的第1个包），seq = y 表示Server 自己的初始序号（seq=0就代表这是服务器这边发出的第0号包）。      
这时服务器进入syn_rcvd，表示服务器已经收到Client的连接请求，等待client的确认。       

Client收到确认后还需再次发送确认，同时携带要发送给Server的数据。      
ACK 置1 表示确认号ack= y + 1 有效（代表期望收到服务器的第1个包），Client自己的序号seq= x + 1（表示这就是我的第1个包，相对于第0个包来说的），      
一旦收到Client的确认之后，这个TCP连接就进入Established状态，就可以发起http请求了。     

发起HTTP请求：    
Http是属于应用层的协议，配合TCP/IP使用。    
Http使用TCP作为它的支撑运输协议。HTTP客户机发起一个与服务器的TCP连接，一旦连接建立，浏览器（客户机）和服务器进程就可以通过套接字接口访问TCP。         

Client向Server发送请求命令   

一个HTTP请求报文由请求行（request line）、请求头部（header）、空行和请求数据4个部分组成：    
请求行分为三个部分：请求方法、请求地址和协议版本     
HTTP/1.1 定义的请求方法有8种：GET、POST、PUT、DELETE、PATCH、HEAD、OPTIONS、TRACE。     

请求地址URL：组成：<协议>：//<主机>：<端口>/<路径>/<参数> 注：端口和路径有时可以省略（HTTP默认端口号是80）有时会带参数，GET请求

协议版本的格式为：HTTP/主版本号.次版本号，有HTTP/1.0和HTTP/1.1和HTTP2.0    
  
请求头部为请求报文添加了一些附加信息，由“名/值”对组成，每行一对，名和值之间使用冒号分隔。如：User-Agent 发送请求的应用程序名称        

请求数据，可选部分，比如GET请求就没有请求数据。      
下面是一个POST方法的请求报文：    

```
请求行
POST 　/index.php　HTTP/1.1 　　  
Host: localhost     
请求头 
User-Agent: Mozilla/5.0 (Windows NT 5.1; rv:10.0.2) Gecko/20100101 Firefox/10.0.2　　
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,/;q=0.8 
Accept-Language: zh-cn,zh;q=0.5 
Accept-Encoding: gzip, deflate 
Connection: keep-alive 
Referer: http://localhost/ 
Content-Length：25 
Content-Type：application/x-www-form-urlencoded 
　　空行 
username=aa&password=1234　　请求数据
```   
    
服务器响应HTTP请求，浏览器得到html代码:      

负载均衡:接收到HTTP请求之后，负载均衡位于网站的最前端，把短时间内较高的访问量分摊到不同机器上处理。负载均衡方案有软件、硬件两种     

HTTP响应报文主要由状态行、响应头部、空行以及响应数据组成。   

状态行由3部分组成，分别为：协议版本，状态码，状态码描述。       
其中协议版本与请求报文一致，状态码描述是对状态码的简单描述              
[常见的HTTP状态码](https://blog.csdn.net/dufufd/article/details/53112184):     
1开头：信息类，表示收到web浏览器请求，正在进一步处理    
2开头：（请求成功）表示成功处理了请求的状态代码。        
3开头 （请求被重定向）表示要完成请求，需要进一步操作         
4开头 （请求错误）这些状态代码表示请求可能出错，妨碍了服务器的处理           
5开头（服务器错误）这些状态代码表示服务器在尝试处理请求时发生内部错误。 这些错误可能是服务器本身的错误，而不是请求出错。           

例：访问[http://www.baidu.com](http://www.baidu.com),自动转到https    
后端做的重定向，通常用Nginx的rewrite或者return规则，返回3开头的状态码让浏览器重定向，如307    

响应头部:与请求头部类似，为响应报文添加了一些附加信息。如：Content-Type响应正文的类型      

响应数据：用于存放需要返回给客户端的数据信息。      

下面是一个响应报文的实例：     

```
HTTP/1.1 200 OK　　状态行 
Date: Sun, 17 Mar 2013 08:12:54 GMT　　响应头部 
Server: Apache/2.2.8 (Win32) PHP/5.2.5 
X-Powered-By: PHP/5.2.5 
Set-Cookie: PHPSESSID=c0huq7pdkmm5gg6osoe3mgjmm3; path=/ 
Expires: Thu, 19 Nov 1981 08:52:00 GMT 
Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0 
Pragma: no-cache 
Content-Length: 4393 
Keep-Alive: timeout=5, max=100 
Connection: Keep-Alive 
Content-Type: text/html; charset=utf-8 
　　空行 
　　响应数据 

HTTP响应示例 


Hello HTTP! 
```
    
浏览器解析html代码，并请求html代码中的资源:     

浏览器拿到index.html文件后，就开始解析其中的html代码，遇到js/css/image等静态资源时，就向服务器端去请求下载。             
会使用多线程下载，每个浏览器的线程数不一样，这个时候就用上keep-alive特性了，建立一次HTTP连接，可以请求多个资源，      
下载资源的顺序就是按照代码里的顺序，但是由于每个资源大小不一样，而浏览器又多线程请求资源，所以查看显示的顺序并不一定是代码里面的顺序。       

浏览器在请求静态资源时（在未过期的情况下），向服务器端发起一个http请求（询问自从上一次修改时间到现在有没有对资源进行修改），      
如果服务器端返回304状态码（告诉浏览器服务器端没有修改），那么浏览器会直接读取本地的该资源的缓存文件。      

最后，浏览器利用自己内部的工作机制，把请求到的静态资源和html代码进行渲染，渲染之后呈现给用户。        
    
客户端和服务器通过三次握手建立了TCP连接以后，当数据传送完毕，四次挥手：      

第一次挥手：主机1（可以是客户端，也可以是服务器端），设置Sequence Number，向主机2发送一个FIN报文段；       
此时，主机1进入FIN_WAIT_1状态；这表示主机1没有数据要发送给主机2了；      
   
第二次挥手：主机2收到了主机1发送的FIN报文段，向主机1回一个ACK报文段，Acknowledgment Number为Sequence Number加1；      
主机1进入FIN_WAIT_2状态；主机2告诉主机1，我“同意”你的关闭请求；      

第三次挥手：主机2向主机1发送FIN报文段，请求关闭连接，同时主机2进入LAST_ACK状态；      

第四次挥手：主机1收到主机2发送的FIN报文段，向主机2发送ACK报文段，然后主机1进入TIME_WAIT状态；     
主机2收到主机1的ACK报文段以后，就关闭连接；此时，主机1等待2MSL后依然没有收到回复，则证明Server端已正常关闭，那好，主机1也可以关闭连接了。      

目前在Internet中所有的传输都是通过TCP/IP进行的，HTTP协议作为TCP/IP模型中应用层的协议也不例外，      
TCP是一个端到端的可靠的面向连接的协议，所以HTTP基于传输层TCP协议不用担心数据的传输的各种问题。       
                 
TCP/IP协议：    

TCP/IP协议模型，包含了一系列构成互联网基础的网络协议，是Internet的核心协议。      
TCP/IP协议簇是一组不同层次上的多个协议的组合，通常被认为是一个四层协议系统。HTTP协议就是基于TCP/IP协议模型来传输信息的。      

物理层：    
通常包括操作系统中的设备驱动程序和计算机中对应的网络接口卡。它们一起处理与电缆（或其他任何传输媒介）的物理接口细节。      
每个网卡都有全球唯一的物理地址。路由器向同一局域网的所有主机发送收到的数据包，本机网卡比较包里知名物理地址和自己的是否一致，一致接收不一致丢弃。     

网络层：    
处理分组在网络中的活动，例如分组的选路。在TCP/IP协议族中，网络层协议包括IP协议，ICMP协议，以及IGMP协议。      
Ping：     
Ping一下127.0.0.1可以看下本机网络协议是否工作正常     
Ping一下某个服务器，看这个服务器有没有开    
Ping一下某个域名，看它的ip地址是多少     

传输层：     
主要为两台主机上的应用程序提供端到端的通信。     
在TCP/IP协议族中，有两个互不相同的传输协议：TCP（传输控制协议）和UDP（用户数据报协议）。     

应用层：      
决定了向用户提供应用服务时通信的活动。      
TCP/IP 协议族内预存了各类通用的应用服务。包括 HTTP，FTP文件传输协议，DNS域名系统服务。       

WebSocket：     

WebSocket是HTML5开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。      
它的最大特点就是，服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话，属于服务器推送技术的一种。      
在WebSocket API中，浏览器和服务器只需要完成一次握手，两者之间就直接可以创建持久性的连接，并进行双向数据传输。        

其他特点包括：
建立在 TCP 协议之上，服务器端的实现比较容易。
与 HTTP 协议有着良好的兼容性。默认端口也是80和443，并且握手阶段采用 HTTP 协议，因此握手时不容易屏蔽，能通过各种 HTTP 代理服务器。       
数据格式比较轻量，性能开销小，通信高效。     
可以发送文本，也可以发送二进制数据。     
没有同源限制，客户端可以与任意服务器通信。      
协议标识符是ws（如果加密，则为wss），服务器网址就是 URL。     

很多网站为了实现推送技术，所用的技术都是 Ajax 轮询。     
轮询是在特定的时间间隔（如每1秒），由浏览器对服务器发出HTTP请求，然后由服务器返回最新的数据给客户端的浏览器。     
这种传统的模式带来很明显的缺点：     
即浏览器需要不断的向服务器发出请求，然而HTTP请求可能包含较长的头部，其中真正有效的数据可能只是很小的一部分，显然这样会浪费很多的带宽等资源。      

WebSocket 协议本质上是一个基于 TCP 的协议。     
为了建立一个 WebSocket 连接，客户端浏览器首先要向服务器发起一个 HTTP 请求，     
这个请求和通常的 HTTP 请求不同，包含了一些附加头信息，其中附加头信息"Upgrade: WebSocket"表明这是一个申请协议升级的 HTTP 请求，       
服务器端解析这些附加的头信息然后产生应答信息返回给客户端，客户端和服务器端的 WebSocket 连接就建立起来了，      
双方就可以通过这个连接通道自由的传递信息，并且这个连接会持续存在直到客户端或者服务器端的某一方主动的关闭连接。      

[客户端的简单示例](http://www.ruanyifeng.com/blog/2017/05/websocket.html):      

```
var ws = new WebSocket("wss://echo.websocket.org");

ws.onopen = function(evt) { 
  console.log("Connection open ..."); 
  ws.send("Hello WebSockets!");
};

ws.onmessage = function(evt) {
  console.log( "Received Message: " + evt.data);
  ws.close();
};

ws.onclose = function(evt) {
  console.log("Connection closed.");
};      
```
    
一个典型的Websocket握手请求如下：     

客户端请求    

```
GET / HTTP/1.1
Upgrade: websocket
Connection: Upgrade
Host: example.com
Origin: http://example.com
Sec-WebSocket-Key: sN9cRrP/n9NdMgdcy2VJFQ==
Sec-WebSocket-Version: 13
```

服务器回应     

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: fFBooB7FAkLlXgRSz0BT3v4hq5s=
Sec-WebSocket-Location: ws://example.com/
```    

<h3 id="48">0.1+0.2不等于0.3</h3>     

在控制台输入0.1+0.2将得到0.30000000000000004     

解决0.1+0.2等于0.3：
设置一个误差范围值，通常称为”机器精度“，而对于Javascript来说，这个值通常是2^-52。      
**ES6**中，已经为我们提供了这样一个属性：Number.EPSILON，而这个值正等于2^-52。       
这个值非常非常小，在底层计算机已经帮我们运算好，并且无限接近0，但不等于0,。这个时候我们只要判断(0.1+0.2)-0.3<Number.EPSILON       
在这个误差的范围内就可以判定0.1+0.2===0.3为true。[Math.pow()](http://www.runoob.com/jsref/jsref-pow.html)          

```
Number.EPSILON=(function(){
    //解决兼容性问题     
    return Number.EPSILON?Number.EPSILON:Math.pow(2,-52);
})();

function numbersequal(a,b){  
        return Math.abs(a-b)<Number.EPSILON;
    }

var a=0.1+0.2, b=0.3;
console.log(numbersequal(a,b));  //这里就为true了
```
     
<h3 id="49">WebAssembly与程序编译</h3>    

[WebAssembly 现状与实战](https://www.ibm.com/developerworks/cn/web/wa-lo-webassembly-status-and-reality/index.html)

JavaScript 的问题：     
语法太灵活导致开发大型 Web 项目困难；     
性能不能满足一些场景的需要。     
针对以上两点缺陷，近年来出现了一些 JS 的代替语言，例如：     

微软的 TypeScript 通过为 JS 加入静态类型检查来改进 JS 松散的语法，提升代码健壮性；     
谷歌的 Dart 则是为浏览器引入新的虚拟机去直接运行 Dart 程序以提升性能；     
火狐的 asm.js 则是取 JS 的子集，JS 引擎针对 asm.js 做性能优化。    
以上尝试各有优缺点，其中：    

TypeScript 只是解决了 JS 语法松散的问题，最后还是需要编译成 JS 去运行，对性能没有提升；    
Dart 只能在 Chrome 预览版中运行，无主流浏览器支持，用 Dart 开发的人不多；     
asm.js 语法太简单、有很大限制，开发效率低。     
三大浏览器巨头分别提出了自己的解决方案，互不兼容，这违背了 Web 的宗旨；     

WebAssembly 是一种新的字节码格式，主流浏览器都已经支持 WebAssembly。      
和JS需要解释执行不同的是，WebAssembly字节码和底层机器码很相似可快速装载运行，因此性能相对于 JS 解释执行大大提升。      
也就是说WebAssembly并不是一门编程语言，而是一份字节码标准，     
需要用高级编程语言编译出字节码放到WebAssembly虚拟机中才能运行,浏览器厂商需要做的就是根据 WebAssembly 规范实现虚拟机。      

目前能编译成 WebAssembly 字节码的高级语言有：     
AssemblyScript:语法和 TypeScript 一致，对前端来说学习成本低，为前端编写 WebAssembly 最佳选择；     
c\c++:官方推荐的方式，详细使用见文档;     
Rust:语法复杂、学习成本高，对前端来说可能会不适应。详细使用见文档;     
Kotlin:语法和 Java、JS 相似，语言学习成本低，详细使用见文档;     
Golang:语法简单学习成本低。但对 WebAssembly 的支持还处于未正式发布阶段，详细使用见文档。     
     
<h3 id="50">js与多线程</h3>
    
html5引入了Web Worker，让js支持多线程。           
Web Worker 是运行在后台的                          
引入一个接口，能使代码运行且不占用浏览器UI线程的时间，也不影响其他worker中运行的代码。     
*[Web Worker 使用教程，work轮询服务器状态，同页面worker等](http://www.ruanyifeng.com/blog/2018/07/web-worker.html)*            
   
Web Worker有着不同的全局运行环境，因此无法从js代码中创建它。需要创建一个完全独立的js文件：    

```
//a.js内容：
var worker = new Worker('b.js');
worker.onmessage = function(event){
    alert(event.data);
}
worker.postMessage('zheng')

//b.js内容：
self.onmessage = function(event){self.postMessage('hello ' + event.data + "!")}

//self指向全局worker对象
//postMessage传递数据
//onmessage接收信息 该事件event对象有一个data属性用于存放传入的数据
```   
  
worker通过importScripts()加载外部js文件：importScripts('file1.js','file2.js')     

如需终止 Web Workers，并释放浏览器/计算机资源，使用 terminate() 方法   

解析一个很大的json。假设数据量足够大。worker成为不错的解决方案。     


做一个斐波那契计算。worker.js:      

```
function fibonacci(num){
    if(num <=0){ return 0;}
    if(num === 1 || num === 2){ return 1;}
    var fn = 1,
        fn1 = 1,
        fn2 = fn + fn1;
    for(var i = 4;i <= num;i++){
        fn = fn1;
        fn1 = fn2;
        fn2 = fn + fn1;
    }
    return fn2;
}

//message函数里边监听接收主线程的数据
message = function(event){
    //主线程的数据通过event.data传进来
    var num = event.data;
    var result = fibonacci(num);
    //计算完结果，给主线程发消息
    postMessage(result);
}
```

主线程先启动一个worker，把数据发给它。同时监听onmessage，取到子线程传回的结果。     
main.js:      

```
var worker = new Worker(worker.js);
worker.onmessage = function(event){
    console.log(`recieve result: ${event.data}`);
};
var num = 1000;
worker.postMessage(num);
```
   
js的多线程是真的多线程，一口气创建500个线程，操作系统会一下子多出500个线程。js的多线程是调用系统API创建的多线程。     
js的多线程无法操作DOM，没有window对象，每个线程的数据都是独立的。     
js单线程里边的特例，如异步回调，是chrome自己的io线程处理的，每发一个请求必须要有一个线程跟着，限制了同一个域最多同时发6个请求。     

chrome的多线程：     

每开一个tab，就会创建一个进程，进程是线程的容器。如点击鼠标click事件：     
用户单击鼠标，浏览器的ui线程收到之后，把消息数据封装成一个鼠标事件发送给io线程。     
io线程再分配给具页面的渲染线程。其中io线程和ui线程是浏览器的线程，渲染线程是每个页面自己的线程。   

如果执行一段耗时的js代码，渲染线程的render线程将会被堵塞，而main线程继续接收io线程发过来的消息并排队。等待render线程处理。     
也就是说当页面卡住的时候不断单击鼠标，等页面空闲了，单击的事件会再继续触发。    

Node.js的单线程模型：      

Node.js也是单线程的，但是由于数据库连接本来就是多线程，调用操作系统的io文件读取也是多线程，所以node的异步是借助于数据库和io多线程。     

<h2 id="57">模块化</h2>    

<h3 id="58">模块化发展</h3>    

模块化：    
以功能块为单位，进行程序设计，实现其求解算法的方法称为模块化。原则是：高内聚，低耦合。     
模块化的目的是为了降低程序复杂度，使程序设计，调试和维护等操作简化。     

高内聚：尽量减少不同文件中函数的交叉引用。     
低耦合：模块与模块之间要相互独立。       

原始写法：     
既然模块化是要实现某个功能，可以把实现功能的一组函数放在同一文件     
函数a，函数b组成一个模块，其他文件先加载该模块，在对函数调用。    
一旦代码量庞大，容易发生命名冲突，容易污染全局变量，模块成员没太多必然联系。        

```
function a(){}
function b(){}
```

添加命名空间：      
添加命名空间，使用单全局变量的模式     

```
var module_speical = {
    _index:0,
    a1:function(){...},
    b2:function(){...}
}
```
a1和b2都封装在module_speical中，调用方法：      

```
module_speical.a1();
module_speical.b2();
```

通常在属性名前加下划线表示该属性是私有属性，不过只是一种开发规范，实际改属性仍然向外暴露：     

`module_speical._index = 6`    

立即执行的函数，实际就是匿名函数：     
使用立即执行匿名函数实现模块化：    

```
var module_speical = (function(){
    var _index = 0;
    var a1 = function(){...};
    var b2 = function(){...};
    return {
        a1:a1,
        b2:b2
    }
})()
```

a1和b2两个函数作为匿名函数返回并赋值给变量module_speical，调用方法：    

```
module_speical.a1();
module_speical.b2();
```

这种方法避免了命名冲突，又使得私有变量_index不能被外部访问和修改。      
如果不使用一些模块化框架，只用jq或zepto类库完成开发，匿名函数实现模块化是常用方式。            

<h3 id="59">CommonJS/AMD/CMD</h3>  

模块化规范主要有CommonJS，AMD，CMD     
CommonJS规范实现的代表是Node.js       
AMD规范实现的代表是Require        
CMD规范的实现代表是Sea.js     

CommonJS：        

Nodejs是服务端js解释器，可以用js语法编写服务端程序。      
Nodejs应用由模块组成，采用CommonJS规范，通过全局方法require来加载模块。     

一个简单的http服务器：      

```
var http = require('http'); //通过require方法引入http模块

var server = http.createServer(function(req,res) { //http模块提供的方法创建服务
    res.statsCode = 200;
    res.setHeader('Content-Type','text/plain')
    res.end('hello world\n');
});

server.listen(3000,'127.0.0.1',function () {
   console.log("开启成功");
})
```

Nodejs内部提供一个Module构建函数，所有模块都是Module的实例，每个模块内部都有一个Module对象，代表当前对象。    
包含如下属性：     

```
exports:表示模块对外输出的值，编写的关键。是对外输出的接口 
id：模块的识别服，通常是带有绝对路径的模块文件
filename：模块的文件名
loaded：返回布尔值，表示模块是否已经完成加载
parent：返回对象，表示调用该模块的模块
children：返回数组，表示该模块要用到的其他模块
```

```
//moduleA.js
module.exports = function(params){
    console.log(params)
}
```

使用方法：     

```
//假设两个文件在同一目录下：
var moduleA = require('./moduleA.js')
moduleA()
```

为了方便，Nodejs为每个模块提供一个exports变量指向module.exports：     

```
//moduleA.js
exports.moduleA = function(params){
    console.log(params)
}
```

CommonJS模块特点：             
所有模块都有单独作用域，不会污染全局。      
重复加载模块只会加载一次，后边从缓存读。     
模块加载顺序按照代码中出现顺序。     
模块加载是同步的。     

AMD：     
   
[RequireJS](https://requirejs.org/)库能够把AMD规范应用到实际浏览器web端的开发中。其主要解决两个问题：       
实现js文件的异步加载，避免网页失去响应。     
管理模块之间的依赖性，便于代码的编写和维护。     

页面底部引入requirejs：    

`<script src="js/require.js data-main="js/main"></script>`     

data-main定义主模块，这里main省略了后缀名js。主模块也称入口文件，所有代码从这儿运行。main.js文件：      

```
require(['jquery','underscore','backbone'],function($,_,Backbone){
    业务代码
});
```

requirejs依次加载jquery,underscore,backbone，然后运行回调函数。      
使用require.config()方法可以对模块加载路径自定义，假设这些文件都在和main.js同级的lib文件夹下：      

```
require.config({
    //或者使用baseUrl定义基础路径
    //baseUrl:'js/lib'
    paths:{
        'jquery':'lib/jquery.min',
        'underscore':'lib/underscore.min',
        'backbone':'lib/backbone.min'
    }
})
```

CDM:      
[CMD 模块定义规范](https://www.cnblogs.com/jiangxiaobo/p/5587234.html)      

在 CMD 规范中，一个模块就是一个文件。代码的书写格式如下：      

`define(factory);`    
    
<h3 id="60">ES6模块支持</h3>     

ES6模块功能主要有两个命令构成：     
export规定模块对外的接口       
import用于输入其他模块提供的功能     

[ES6模块详解](http://es6.ruanyifeng.com/#docs/module)           

export：    
**ES6**中，一个模块也是一个独立的文件，具有独立的作用域，通过export命令输出内部变量：      

```
//car.js
var name = 'bus';
var color = 'green';
var weight = '20顿'

export{name,color,weight};
```

还可以输出函数或类：      

```
export function run(){console.log('Bus is running')}
```

可以用as关键字对输出的变量，函数，类重命名：    

```
var name = 'bus';
var color = 'green';
var weight = '20顿'
function run(){console.log('Bus is running')}

export{
    name as busName,
    color as busColor,
    weight as busWeight,
    run as busRun
    }
```

import:      

`import {name,color,weight,run} from './car'`    

导入模块也可以使用as重命名：     

`import {name as busName} from './car'`     

没有输出也可以加载模块：    

`import lodash;`      

通过星号可以整体加载某个文件：      

```
import * as car from './car';
console.log(car.name)
console.log(car.color)
```

export default命令：    
为模块指定默认输出 export-default.js：     

`export default function(){console.log('default')}`    

加载模块可以指定任意名字：     

```
import someName from './export-default'
someName()
```

<h2 id="61">Babel</h2>          

**ES6**转码器，转为ES5在浏览器或其他环境执行。      

[Babel中文网](https://www.babeljs.cn/)        

命令行转码babel-cli：        

`npm i -g babel-cli`       

转码结果输出到标准输出：      

`babel example.js`      

转码结果写入一个文件：     

`babel example.js --out-file compiled.js`         

`babel example.js -o compiled.js`              

整个目录转码：      

`babel src --out-dir lib`        
 
`babel src -d lib`                

*在不同项目使用不同版本babel，需将babel-cli安装在项目中*                

babel-cli工具自带babel-node命令，提供一个支持**ES6**的REPL环境，可以直接运行**ES6**代码：           

`babel-node example.js`            

babel支持npm包形式安装：    

`npm install --save-dev babel babel-cli babel-preset-env`    

安装成功后，package.json文件：     

```
"script":{
    'start':'babel test.js --out-file test-compiled.js'
}
```

创建配置.babelrc文件存放在根目录：     

```
{
  "presets": ["env"]
}
```

Babel只转换语法(如箭头函数)，可以使用 babel-polyfill 支持新的API,      
例如 Promise,generator,set,maps,proxy等全局对象，和定义在全局对象上的新的原生方法如Array.from,Object.assign等。      

`npm install --save-dev babel-polyfill`      

使用它时需要在你应用程序的入口点顶部或打包配置中引入。       

babel用于浏览器环境：    
*从babel6.0开始不再直接提供浏览器版本，要用构建工具创建出来，或使用[babel-standalone](https://github.com/babel/babel-standalone#usage)模块提供的浏览器版本*           

[traceur](https://github.com/google/traceur-compiler)用于浏览器环境：       
*还可用于node和命令行转换，[详见traceur入门](https://github.com/google/traceur-compiler/wiki/Getting-Started)*                   

```
<h1 id="message"></h1>
    <script src="https://google.github.io/traceur-compiler/bin/traceur.js"></script>
    <script src="https://google.github.io/traceur-compiler/bin/BrowserSystem.js"></script>
    <script src="https://google.github.io/traceur-compiler/src/bootstrap.js"></script>
    <script type="module">
      class Greeter {
        constructor(message) {
          this.message = message;
        }

        greet() {
          var element = document.querySelector('#message');
          element.innerHTML = this.message;
        }
      };

      var greeter = new Greeter('Hello, world!');
      greeter.greet();
    </script>
```


网页实时将**ES6**代码转换为ES5代码，对性能有影响。生产环境下需要加载转码好的脚本。          

在线转换：              
babel提供一个REPL[在线编辑器](https://babeljs.io/repl)            
google提供的traceur[在线编辑器](https://google.github.io/traceur-compiler/demo/repl.html#)              

<h2 id="62">前端工程化</h2>          

<h3 id="63">工程化必要性和发展史</h3>      

必要性：     

规范代码      
进行js预处理     
进行css预处理     
自动编译     
缩减文件体积     

发展史：     

石器时代：静态html代码提供基本浏览。偶尔表单提交js实现功能。      

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>php页面</title>
</head>
<body>
<?php
  echo 'hello'
?>
</body>
</html>
```

铜器时代：    

web开发的组件化和异步加载的实现。ajax打开新局面。     

农业时代：     

为提高页面加载速度，优化用户体验。模块加载规范应运而生。 AMD，CMD依次为基础，出现很多动态加载js代码框架。      
实现AMD规范框架中，requirejs较知名。     

工业时代：     

功能日益复杂，开发难度也来越大，为降低开发难度，前端MVC，MVP，MVVM框架诞生。统称MV*框架     
其中主流有Backbone，AngularJS，React，Vue等。    
显而易见的好处：    
前后端分离，合理的分层，让代码各司其职，降低复杂度。     

同时，为提高开发效率，加强团队合作，出现很多自动化为目标的构建工具，如grunt，glup，webpack等。     
压缩，编译，单元测试，代码检查，打包发布等重复性任务，可以使用自动化工具来降低劳动成本，简化开发者工作。     

构建工具核心思想是通过一个配置文件来实现所有需要自动化的功能。     

<h3 id="64">Grunt开发简易相册</h3>     

Grunt 是基于 Node.js 的项目构建工具。它可以自动运行你所设定的任务。     
[Grunt官网](https://gruntjs.com/)        
[Grunt中文网](https://www.gruntjs.net/)       

全局安装：    

`npm install -g grunt-cli`     

此时，grunt命令已经加入系统，但并不等于安装了grunt。   
grunt-cli任务是调用与Gruntfile在同一目录的grunt。这样做好处是允许同一系统安装多个版本的grunt     

Gruntfile是grunt中最重要文件，放在项目根目录，是一个有效的javascript或coffeescript文件。         
主要作用有配置或定义任务task。加载grunt插件。      

主要组成：     
wrapper函数    
项目与任务配置    
加载grunt插件和任务   
自定义任务   

grunt使用插件：配置，加载，注册，执行。    
前三项通过gruntfile文件定义。     

项目文件夹初始化package.json：     

`npm init`    

在项目目录安装grunt和相关插件，package.json的devDependencies就会显示出插件：            

`npm install grunt grunt-contrib-concat grunt-contrib-cssmin grunt-contrib-imagemin grunt-contrib-imagemin grunt-contrib-uglify grunt-inline --save-dev`      

配置Gruntfile.js文件：      
*grunt-contrib-imagemin略*     

```
//包装函数
module.exports = function (grunt) {
    //插件配置信息
    grunt.initConfig({
        // 内联图片文件的配置
        inline: {
            page: {
                src: ['index.html']
            }
        },
        // 压缩CSS和JavaScript文件的配置
        uglify: {
            dist: {
                files: {
                    'dist/js/album.min.js': ['src/js/album.js']
                }
            }
        },
        // 压缩CSS文件的配置
        cssmin: {
            dist: {
                files: {
                    'dist/css/reset.min.css': ['src/css/reset.css'],
                    'dist/css/album.min.css': ['src/css/album.css']
                }
            }
        },
        // 合并多个文件的配置
        concat: {
            dist: {
                src: ['dist/css/reset.min.css', 'dist/css/album.min.css'],
                dest: 'dist/css/all.min.css'
            }
        }
    });
    // 加载这些任务
    grunt.loadNpmTasks('grunt-inline');
    grunt.loadNpmTasks('grunt-contrib-uglify');
    grunt.loadNpmTasks('grunt-contrib-cssmin');
    grunt.loadNpmTasks('grunt-contrib-concat');

    // 默认执行的任务列表
    grunt.registerTask('default', ['inline', 'uglify', 'cssmin', 'concat']);
};
```    

通过grunt命令来执行任务。grunt.registerTask中的default是预设参数。也可以通过 grunt default grunt uglify执行。     

目录结构：    
grunt-album文件夹：    
src文件夹：
img文件夹      
js文件夹     
css文件夹       
dist文件夹(没有自动创建):        
img文件夹      
js文件夹     
css文件夹 
         
html文件：     

```

<html>
<head>
	<title>使用Grunt开发WEB相册</title>
	<link rel="stylesheet" href="src/css/reset.css" />
	<link rel="stylesheet" href="src/css/album.css" />
</head>
<body>
    <div class="big-img-box">
		<img class="big-img" src="src/img/img1.jpg" />
	</div>
	<div class="small-img-box">
		<a href="#src/img/img1.jpg" class="hover"><img src="src/img/img1s.jpg"/></a>
		<a href="#src/img/img2.jpg"><img src="src/img/img2s.jpg" /></a>
		<a href="#src/img/img3.jpg"><img src="src/img/img3s.jpg" /></a>
		<a href="#src/img/img4.jpg"><img src="src/img/img4s.jpg" /></a>
		<a href="#src/img/img5.jpg"><img src="src/img/img5s.jpg" /></a>
	</div>
	<script src="src/js/album.js"></script>
</body>
</html>
```

album.css文件：    

```
.big-img-box {
    width:1200px;
    height:800px;
    margin:10px auto;
    text-align:center;
    border:solid 1px gray;
}
.big-img { 
    max-width:1200px;
    height:800px;
}
.small-img-box { 
    width:1200px;
    margin:0 auto;
    background:gray;
    font-size:0;
}
.small-img-box img { 
    width:200px;
    height:120px;
    margin:20px;
    border-radius:10px;
}
.small-img-box .hover>img { 
    box-shadow:white 0 0 20px;
}
```

reset.css文件:     

```
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```   

album.js文件:     

```
"use strict";
(function (window, undefined) {
    var doc = window.document;
    var arr = doc.querySelectorAll('.small-img-box a');
    var bigimg = doc.querySelector('.big-img');
    for (var i = 0; i < arr.length; i++) {
        arr[i].addEventListener('click', function (ev) {
            bigimg.src = this.getAttribute('href').substr(1);
            doc.querySelector('.small-img-box .hover').classList.remove('hover');
            this.classList.add('hover');
            ev.preventDefault();
            return false;
        }, false);
    }
})(window);
```

*grunt 合并文件之后，在html中的引用目录修改可以通过Grunt usemin，[grunt-text-replace](https://blog.csdn.net/tangxiaolang101/article/details/52788083)等插件*       
      
<h3 id="65">Gulp构建MarkDown编辑器</h3>          

使用grunt构建项目设计磁盘操作，效率低。 因此基于流的Gulp应运而生。所有操作都在内存中进行。                   
[gulp中文网](https://www.gulpjs.com.cn/)          
[gulp官网](https://gulpjs.com/)         
      
全局安装：     

`npm install gulp-cli -g`      

项目根目录安装gulp和创建package.json文件：     

```
npm init
npm install gulp --save-dev
```

根目录下创建gulpfile.js文件做配置:      

```
//gulp-connect搭服务器。不是必须要的
var gulp = require('gulp'),
    connect = require('gulp-connect');
 
gulp.task('webserver', function() {
    connect.server({
        livereload: true,
        port: 3000
    });
});
 
gulp.task('default', ['webserver']);

// es6转换es5 这里配置就不需要根目录.babelrc文件了
var babel = require("gulp-babel")
gulp.task("compile-js", function () {
    gulp.src("src/**/*.js")
        .pipe(babel({
            presets:['es2015']
        }))
        .pipe(gulp.dest("dist/js"));
});

// sass文件转css
var sass = require("gulp-sass");
gulp.task("compile-sass", function () {
    gulp.src("theme/**/*.scss")
        .pipe(sass().on('error', sass.logError))
        .pipe(gulp.dest("dist/css"));
});

//合成雪碧图
var spritesmith = require('gulp.spritesmith');
gulp.task("sprite", function () {
    gulp.src("theme/images/**.png")
        .pipe(spritesmith({
            imgName: 'images/icons.png',
            cssName: 'icons.css'
        }))
        .pipe(gulp.dest("dist/css"));
});

// js语法检测
var eslint = require("gulp-eslint");
gulp.task("eslint", function () {
    gulp.src("src/**/*.js")
        .pipe(eslint({
            useEslintrc: true
        }))
        .pipe(eslint.format())
        .pipe(eslint.failAfterError)
});

// sass语法检测
var sasslint = require("gulp-sass-lint");
gulp.task("sasslint", function () {
    gulp.src("theme/**/*.scss")
        .pipe(sasslint())
        .pipe(sasslint.format())
        .pipe(sasslint.failOnError())
});

// 文件合并
var concat = require("gulp-concat");
gulp.task("concat", ["compile-js", "compile-sass", "sprite", "copy-images"], function () {
    gulp.src("dist/css/*.css")
        .pipe(concat("style.css"))
        .pipe(gulp.dest("dist/latest"))
        .pipe(reload({
            stream: true
        }));

    gulp.src("dist/js/**/*.js")
        .pipe(concat("app.js"))
        .pipe(gulp.dest("dist/latest"))
        .pipe(reload({
            stream: true
        }));
});

gulp.task("copy-images", function () {
    gulp.src("dist/css/images/**.**")
        .pipe(gulp.dest("dist/latest/images"));
})

// 浏览器自动刷新默认3000端口，可配置里修改
var browserSync = require("browser-sync");
var reload = browserSync.reload;
gulp.task("browser-sync", function () {
    browserSync({
        server: './',
        files:['**'], //必须有，不然修改文件不刷新
        notify: false
    });
});

// 监听文件变化自动构建
gulp.task("watch", ["concat", "browser-sync"], function () {
    gulp.watch(["src/**/*.js", "theme/**/*.scss"], ["concat"]);
})

// 压缩js，css
var uglify = require("gulp-uglify");
var cssMinify = require("gulp-clean-css");
var rename = require("gulp-rename");
gulp.task("minify", ["concat"], function(){
    gulp.src("dist/latest/app.js")
    .pipe(uglify())
    .pipe(rename(function(path){
        path.basename += ".min"
    }))
    .pipe(gulp.dest("dist/latest"));
    gulp.src("dist/latest/style.css")
    .pipe(cssMinify())
    .pipe(rename(function(path){
        path.basename += ".min"
    }))
    .pipe(gulp.dest("dist/latest"));  
})

```

gulp-babel：      
将ES6编译成ES5     

```
npm install gulp-babel --save-dev
npm install babel-preset-es2015
```  

gulp-sass:
编译sass文件      

`npm install gulp-sass --save-dev`    

css sprites:
合成雪碧图     

`npm install gulp-spritesmith`       
     
[showdown类库](https://github.com/showdownjs/showdown)：开源的Markdown解析器，用于将Markdown解析为html。      

存储部分通过html5的indexedDB进行保存：     

```

<!DOCTYPE html>
<html lang="en">

<head>
    <title></title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="dist/latest/style.css" rel="stylesheet">
</head>

<body>
    <!-- 导航部分 -->
    <nav>
        <div class="buttons">
            <a class="icon icon-add" href="#"></a>
        </div>
        <div class="list-container">
            <ul class="list">
            </ul>
        </div>
    </nav>
    <!-- 编辑器部分 -->
    <main>
        <!-- 编辑区域 -->
        <div class="editor">
            <div class="title">
                <input type="text" name="title" value="" placeholder="请输入标题" id="tbTitle" />
            </div>
            <div class="md-editor">
                <textarea placeholder="请输入markdown" id="tbMarkdown"></textarea>
            </div>
        </div>
        <!-- 预览区域 -->
        <div class="preview-container">
            <div class="preview markdown-body" id="preview">

            </div>
            <div class="buttons">
                <div href="#" id='btnSave' class="btn-save">保存</div>
            </div>
        </div>
    </main>
    <script src="external/showdown.js"></script>
    <script src="dist/latest/app.js"></script>
</body>

</html>
```

db.js:      

```
(function ($window) {
    const indexedDB = $window.indexedDB
    const DB_NAME = "mkeditor"
    const STORE_NAME = "artical"
    const openDB = (version = 1) => {
        return new Promise((resolve, reject) => {
            const request = indexedDB.open(DB_NAME, version)
            request.addEventListener("error", (e) => {
                reject(e.target.error)
            })
            request.addEventListener("success", (e) => {
                resolve(e.target.result)
            })
            request.addEventListener("upgradeneeded", (e) => {
                const db = e.target.result
                if (!db.objectStoreNames.contains(STORE_NAME)) {
                    db.createObjectStore(STORE_NAME, { keyPath: "id", autoIncrement: true })
                }
            });
        });
    }

    const wrapPromise = (fn) => {
        return new Promise((resolve, reject) => {
            const request = fn()
            request.addEventListener("error", (e) => {
                reject(e.target.error)
            })
            request.addEventListener("success", (e) => {
                resolve(e.target.result)
            })
        })
    }

    const getStore = (mode = "readonly") => {
        return openDB().then((db) => {
            return db.transaction(STORE_NAME, mode).objectStore(STORE_NAME)
        })
    }

    const add = (data) => {
        return getStore('readwrite').then((store) => {
            return wrapPromise(()=>{
                return store.add(data);
            })
        });
    }

    const save = (data) => {
        const id = data.id;
        if (id) {
            return getStore("readwrite").then((store) => {
                return wrapPromise(()=>{
                    return store.get(id)
                }).then((result)=>{
                    if(result){
                        Object.assign(result, data)
                        return wrapPromise(()=>{
                            return store.put(result)
                        })
                    }else{
                        return Promise.reject(new Error(`item with id ${id} not found`))
                    }
                })
            })
        }else{
            return add(data)
        }
    }

    const getAll = () => {
        return getStore().then((store) => {
            return new Promise((resolve, reject) => {
                const request = store.openCursor()
                let resuts = []
                request.addEventListener("success", (e) => {
                    const cursor = e.target.result
                    if (cursor) {
                        resuts.push(cursor.value)
                        cursor.continue()
                    } else {
                        return resolve(resuts)
                    }
                })
                request.addEventListener("error", (e) => {
                    reject(e.target.error)
                })
            })
        })
    }

    const getById = (id) => {
        return getStore().then((store) => {
            return wrapPromise(()=>{
                return store.get(id)
            })
        })
    }

    const delData = (id) => {
        return getStore("readwrite").then((store) => {
            return wrapPromise(()=>{
                return store.delete(id)
            })
        })
    }
    $window.MKDB = {
        save: save,
        getAll: getAll,
        getById: getById,
        delete: delData
    }
}(window))
```   

main.js:      

```
(() => {
    const $title = document.getElementById("tbTitle")
    const $markdown = document.getElementById("tbMarkdown")
    const $preview = document.getElementById("preview")
    const mdConverter = new showdown.Converter()
    const $saveBtn = document.getElementById("btnSave")
    const $addBtn = document.querySelector(".icon-add")
    const $list = document.querySelector(".list")

    let artical = {}

    const bindEvents = () => {
        $markdown.addEventListener("keyup", () => {
            renderPreview()
        })
        $list.addEventListener("click", (e) => {
            const target = e.target
            if (target.matches(".icon-delete")) {
                let $li = target.parentNode
                let id = parseInt($li.getAttribute("data-id"))
                MKDB.delete(id).then(() => {
                    renderList()
                })
            } else if (target.matches(".title")) {
                let $li = target.parentNode
                let id = parseInt($li.getAttribute("data-id"))
                MKDB.getById(id).then((data) => {
                    Object.assign(artical, {
                        id: parseInt($li.getAttribute("data-id"))
                    }, data)
                    renderArtical()
                })
            }
        })
        $addBtn.addEventListener("click", (e) => {
            artical = {}
            renderArtical()
            e.preventDefault()
        })
        $saveBtn.addEventListener("click", () => {
            Object.assign(artical, {
                title: $title.value,
                content: $markdown.value
            })
            console.log(artical)
            MKDB.save(artical).then(() => {
                renderList()
            }).catch((ex) => {
                console.log(ex)
            })

        })
    }

    const renderList = () => {
        window.MKDB.getAll().then((data) => {
            const frag = document.createDocumentFragment();

            data.forEach((item) => {
                let li = document.createElement("li")
                li.innerHTML = `<a href="#" class="title">${item.title}</a><div class="btn-delete icon-delete">`
                li.setAttribute("data-id", item.id)
                frag.appendChild(li)
            })
            $list.innerHTML = ""
            $list.appendChild(frag)
            console.log(data);
        })
    }

    const renderArtical = () => {
        const {title = "", content = ""} = artical
        $title.value = title
        $markdown.value = content
        renderPreview()
    }

    const renderPreview = () => {
        const result = convertMarkdown($markdown.value);
        $preview.innerHTML = result;
    }

    const convertMarkdown = (markdownStr) => {
        return mdConverter.makeHtml(markdownStr);
    }
    bindEvents()
    document.addEventListener("DOMContentLoaded", () => {
        renderList()
    })
})();
```

代码检查任务eslint：        
sass用gulp-sass-lint        
es6用gulp-eslint      

全局安装eslint：    

`npm install eslint -g`     

项目目录初始化，创建配置文件：     

`eslint init`     

选择配置方式：use a popular style guide     
选择预设模式：standard      
选择配置内容的存储文件类型： javascript      
配置结束生成一个.eslintrc的文件。             

项目中安装：     

```
npm install gulp-eslint --save-dev
npm install gulp-sass-lint
```      

代码合并，压缩，重命名任务：     

gulp-concat插件将各个独立的文件进行合并：     

`npm install gulp-concat --save-dev`    

代码压缩，css用gulp-clean-css.js用gulp-uglify:      

`npm install gulp-clean-css gulp-uglify --save-dev`      

重命名插件gulp-rename:     

`npm install gulp-rename --save-dev`     

监听文件变化，自动刷新：      
gulp的watch方法监听文件变化自动构建     

可采用browser-sync工具实现浏览器自动刷新：     

`npm install browser-sync --save-dev`     

用 gulp 建一个服务器:     

`npm install gulp-connect --save-dev`     

<h3 id="66">Webpack4+vue2</h3>                                                                                                                                                 
配置基本webpack：    

创建一个新目录并进入该目录：      

`mkdir webpack-quick && cd $_`      

初始化 package.json：     
*加-y（代表yes），则跳过提问阶段*         

`npm init`        

安装webpack-cli,webpack-dev-server和webpack4：       
*i是install简写*      

`npm i webpack-cli webpack webpack-dev-server --save-dev`         

在package.json的script里添加快速启动：      

```
"scripts": {
    "dev": "webpack-dev-server --open --config webpack.config.js"
  }
```

webpack-quick里创建webpack.config.js文件并初始化设置：     

```
var config = {}
module.exports = config 

//支持es6后可以：
//const config = {}
//export default config
```

在webpack4中,既不必须定义entry point(入口点),也不必须定义output file(输出文件)。     
它将查找 ./src/index.js 作为默认入口点。 而且，它会在 ./dist/main.js 中输出模块包。       

如果要配置，可以在webpack.config.js配置如：         

```
var config = {
  entry: './src/index.js',
  output: {
    path:path.join(__dirname,'./dist'),
    publicPath:'/dist/', //指定资源文件引用目录，可以是CDN
    filename: 'main.js'
  }
};

module.exports = config 
```

在根目录webpack-start新建index.html文件。新建src文件夹，里边新建index.js文件：      

index.html：     

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>webpack-quick</title>
</head>
<body>
	<div id="app">hello world</div>
	<script src="/dist/main.js"></script>
</body>
</html>
```  

index.js：       

```
document.getElementById('app').innerHTML = 'hello quick !';
```
    
执行`npm run dev` 就会自动打开http://localhost:8080/    
显示hello quick !  并能修改实时刷新。      

webpack 4 引入了 production(生产) 和 development(开发) 模式：         

一个典型的项目可能有：          
用于开发的配置文件，定义 webpack dev server 和其他东西           
用于生产的配置文件，定义UglifyJSPlugin，sourcemaps 等           

打开 package.json 并填充 script 部分：     

```
"scripts": {
"dev": "webpack-dev-server --open --config webpack.config.js --mode development",
"build": "webpack-dev-server --open --config webpack.config.js --mode production"
}
```   

`npm run dev` //生成没压缩的开发版           
`npm run build` //生成压缩的生产版,默认是生产版      

production mode(生产模式) 可以开箱即用地进行各种优化。 包括压缩，作用域提升，tree-shaking 等。      
development mode(开发模式)针对速度进行了优化，仅仅提供了一种不压缩的 bundle 。      

另一种设置模式方法，在webpack.config.js里设置模式：     

```
module.exports = {
  mode: 'development' // 不设置默认production
};
```   

写css样式，用到css-loader,style-loader:     

`npm i css-loader style-loader --save-dev`           

src目录新建style.css 写入：      

```
#app{
font-size: 24px;
color:#f50;
}
```   

在index.js文件引入style.css      

`import './style.css'`    

执行`npm run dev` 会动态创建style标签写入css     

将散落在各地的css提取出来，生成main.css文件，在index.html文件link加载：       

mini-css-extract-plugin      
*注意：确保将 webpack 更新到 4.2.0 版。 否则 mini-css-extract-plugin 将无效*      
*在过去，这是 extract-text-webpack-plugin 的工作。*：      

`npm i mini-css-extract-plugin --save-dev`      

index.html写入：    

`<link rel="stylesheet" href="/dist/main.css">`     

在webpack.config.js里设置:     

```
var MiniCssExtractPlugin = require('mini-css-extract-plugin');

{
    test: /\.css$/,
    use: [ //数组形式的话，编译是从后往前。
        MiniCssExtractPlugin.loader,
        // 'style-loader',
        'css-loader'
    ]
}

plugins: [
    //重命名提取后的css文件
    new MiniCssExtractPlugin('main.css')
]
```

执行`npm run dev`不会再动态创建style，而是生成了link         

支持ES6:        

`npm i babel babel-cli babel-core babel-loader babel-preset-env --save-dev`       

通过在项目文件夹中创建名为 .babelrc 的新文件来配置 Babel ：     

```
{
	"presets":["env"]
}
```

除非要自定义entry point(入口点) ，否则无需webpack.config.js里指定babel-loader:      

```
module:{
    rules:[
        {
            test: /\.js$/,
            exclude: /node_modules/,
            use: {
                loader: "babel-loader"
            }
        }
    ]
}
```

也无需在 package.json 中配置npm scripts   

```
"scripts": {
"dev": "webpack-dev-server --open --config webpack.config.js --module-bind js=babel-loader",
"build": "webpack-dev-server --open --config webpack.config.js --module-bind js=babel-loader"
}
```      
    
安装vue,vue-loader,vue-style-loader,vue-template-compiler,vue-hot-reload-api:     

`npm i vue --save`       
          
`npm i vue-loader vue-style-loader vue-template-compiler vue-hot-reload-api --save-dev`        

更新 webpack 配置：      

```
const { VueLoaderPlugin } = require('vue-loader'); //vue-loader，15的版本需要再添加plugin的配置

{
    test:/\.vue$/,
    loader:'vue-loader',
    options:{
        loaders:{
            css:[
                'vue-style-loader',
                'mini-css-extract-plugin',
                'css-loader'
            ]
        }
    }
}

new VueLoaderPlugin() //vue-loader，15的版本需要再添加plugin的配置
```

url-loader和file-loader支持图片和字体等文件：     

`npm i url-loader file-loader --save-dev`     

更新 webpack 配置：               

```
{
    test:/\.(gif|jpg|png|woff|svg|eot|ttf)\??.*$/,
    loader:'url-loader?limit=1024' //文件小于1k就以base64形式加载
}
```    

方便开发生产环境切换，新建用于生产环境的配置文件webpack.prod.config.js       
用到webpack-merge模块，合并两个配置文件：     

`npm i webpack-merge --save-dev`     

配置webpack.prod.config.js:      

```
const webpack = require('webpack');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const { VueLoaderPlugin } = require('vue-loader');
const merge = require('webpack-merge');
const webpackBaseConfig = require('./webpack.config.js');

webpackBaseConfig.plugins = [];

module.exports = merge(webpackBaseConfig,{
	mode: 'production',
	output:{
		publicPath:'/dist/',
		filename:'[name].[chunkhash].js'
	},
	plugins:[
		new MiniCssExtractPlugin({
			filename:'[name].[chunkhash].css'
		}),
		new VueLoaderPlugin()
	]
});
```

html-webpack-plugin生成html文件：     

`npm i html-webpack-plugin --save-dev`    

通过template选项读取指定模板index.ejs，输出到指定目录。      
更新webpack.prod.config.js 配置：       

```
const HtmlWebPackPlugin = require("html-webpack-plugin");

plugins: [
new HtmlWebPackPlugin({
    template: "./src/index.html",
    filename: "./index.html"
})
]
```
 
index.ejs模板动态设置最新静态资源：     

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Webpack App</title>
    <link rel="stylesheet" href="<%= htmlWebpackPlugin.files.css[0] %>">
</head>
<body>
    <div id="app"></div>
    <script type="text/javascript" src="<%= htmlWebpackPlugin.files.js[0] %>"></script>
</body>
</html> 
```    

运行`npm run build` 生成dist文件夹和文件      

*如没有，输入`webpack -p`运行生产模式，生成dist文件*      

生产环境css压缩，用到optimize-css-assets-webpack-plugin：        

`npm i optimize-css-assets-webpack-plugin --save-dev`     

更新webpack.prod.config.js设置：        

```
const OptimizeCSSAssetsPlugin = require("optimize-css-assets-webpack-plugin");
const UglifyJsPlugin = require("uglifyjs-webpack-plugin"); //设置生产模式，所以不用npm i uglifyjs-webpack-plugin

optimization: {
    minimizer: [
        new UglifyJsPlugin({
            cache: true,
            parallel: true,
            sourceMap: true 
            }),
        new OptimizeCSSAssetsPlugin({}) 
    ]
}
```

生产环境图片压缩imagemin-webpack-plugin：    
更新webpack.prod.config.js设置：         

```
const ImageminPlugin = require('imagemin-webpack-plugin').default

new ImageminPlugin({ 
        test: /\.(jpe?g|gif|png|svg)$/i,
        optipng: {
        optimizationLevel:6
        }	
})
```

给生产环境生成的文件加chunkhash：     
*问题在于修改css文件，js文件会一同算出新chunkhash*      

```
output:{
    publicPath:'/dist/',
    filename:'[name].[chunkhash].js',
}

new MiniCssExtractPlugin({
    filename:'[name].[chunkhash].css'
})
```

最终webpack.prod.config.js：      

```
const webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const { VueLoaderPlugin } = require('vue-loader');
const merge = require('webpack-merge');
const webpackBaseConfig = require('./webpack.config.js');
webpackBaseConfig.plugins = [];

// 压缩js，css
const OptimizeCSSAssetsPlugin = require("optimize-css-assets-webpack-plugin");
const UglifyJsPlugin = require("uglifyjs-webpack-plugin");

//压缩图片
const ImageminPlugin = require('imagemin-webpack-plugin').default

module.exports = merge(webpackBaseConfig,{
	mode: 'production',
	output:{
		publicPath:'/dist/',
		filename:'[name].[chunkhash].js',
	},
	optimization: {
	    minimizer: [
			new UglifyJsPlugin({
			    cache: true,
			    parallel: true,
			    sourceMap: true 
			  }),
			new OptimizeCSSAssetsPlugin({}) 
	    ]
	},
	plugins:[
		new MiniCssExtractPlugin({
			filename:'[name].[chunkhash].css'
		}),
		new HtmlWebpackPlugin({
			filename:'./index_prod.html',
			template:'./index.ejs',
			inject:false
		}),
		new VueLoaderPlugin(),
		new ImageminPlugin({ 
				test: /\.(jpe?g|gif|png|svg)$/i,
				optipng: {
				optimizationLevel:6
				}	
    	})
	]
});
```

最终webpack.config.js：      

```
const path = require('path');
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
const { VueLoaderPlugin } = require('vue-loader'); //vue-loader，15的版本需要再添加plugin的配置

const config = {
	mode: 'development', // 不设置默认production
	// entry,output均按默认路径和文件名设置，所以可以都不写。
	entry: {
		main:'./src/index.js'
	},
	output: {
		path:path.join(__dirname,'./dist'),
		publicPath:'/dist/', //指定资源文件引用目录，可以是CDN
		filename: 'main.js'
	},
	module:{
		rules:[
			{
				test:/\.vue$/,
				loader:'vue-loader',
				options:{
					loaders:{
						css:[
							'vue-style-loader',
							'mini-css-extract-plugin',
							'css-loader'
						]
					}
				}
			},
			{
				test: /\.html$/,
				use: [
						{
							loader: "html-loader",
							options: { minimize: true }
						}
				]
			},
			{
			    test: /\.css$/,
			    use: [ //数组形式的话，编译是从后往前。
					MiniCssExtractPlugin.loader,
					// 'style-loader',
					'css-loader'
				]
      		},
			{
            	test:/\.(gif|jpg|png|woff|svg|eot|ttf)\??.*$/,
            	loader:'url-loader?limit=1024' //文件小于1k就以base64形式加载
            }
		]
	},
	plugins: [
	    //重命名提取后的css文件
		new MiniCssExtractPlugin('main.css'),
		//vue-loader，15的版本需要再添加plugin的配置
    	new VueLoaderPlugin() 
	]
};

module.exports = config
```

前端路由vue-router    

`npm i vue-router --save`      

需要在package.json的script里加入：--history-api-fallback 所有路由都指向index.html       

使用路由异步resolve后，在请求到该页面时，才去加载页面，所以自然没有必要把所有页面css自动合并到一起加载。       
此时mini-css-extract-plugin无法把每个vue页面写的style合并到一起，如还想一起加载，可以改用老插件extract-text-webpack-plugin：      

`npm i extract-text-webpack-plugin@next --save-dev`     

在webpack.config.js加入配置：        

```
var ExtractTextPlugin = require('extract-text-webpack-plugin');

new ExtractTextPlugin({
    filename:'main.css',//重命名提取后的css文件
    allChunks: true //有了chunk，需要在此配置
})

{
    test:/\.vue$/,
    loader:'vue-loader',
    options:{
        loaders:{
            css:ExtractTextPlugin.extract({
                use:'css-loader',
                fallback:'vue-style-loader'
            })
        }
    }
},
{
    test: /\.css$/,
    use: ExtractTextPlugin.extract({
        use: 'css-loader',
        fallback: 'style-loader'
    })
},
```   

路由异步实现部分代码：     

```
{
    path:'/index',
    component:(resolve) => require(['./views/index.vue'],resolve)
},
```    

改成加载时直接加载所有页面，mini-css-extract-plugin会生效css一并合并：     

```
import index from "./views/index.vue";

{
    path:'/index',
    component:index
},
```

状态管理vuex        
主要使用场景：大型单页应用，适合多人协同项目开发。      
*简单跨组件通讯可以封装vue-bus插件解决*                 

`npm i vuex --save`      

封装插件vue-bus：      
用于解决跨级和兄弟组件通信：     

```
const install = function(Vue){
	const Bus = new Vue({
		methods:{
			emit(event, ...args){
				this.$emit(event, ...args);
			},
			on(event,callback){
				this.$on(event,callback);
			},
			off(event,callback){
				this.$off(event,callback);
			}
		}
	});		
	Vue.prototype.$bus = Bus;
};

export default install;
```

index.js里引入：      

```
import VueBus from './vue-bus' //使用插件代替vuex解决通讯

Vue.use(VueBus);
```

node.js的request库，做代理：      

`npm i request --save-dev`      

新建proxy.js文件设置代理：      

```
const http = require('http');
const request = require('request');

const hostname = '127.0.0.1';
const port = 8010;
const imgPort = 8011;

// 创建一个API 代理服务器
const apiServer = http.createServer((req, res) => {
    const url = 'http://news-at.zhihu.com/api/4' + req.url;
    const options = {
        url: url
    };

    function callback (error, response, body) {
        if (!error && response.statusCode === 200) {
            // 设置编码类型，否则中文会显示为乱码
            res.setHeader('Content-Type', 'text/plain;charset=UTF-8');
            // 设置所有域允许跨域
            res.setHeader('Access-Control-Allow-Origin', '*');
            // 返回代理后的内容
            res.end(body);
        }
    }
	request.get(options, callback);
});

// 监听8010端口
apiServer.listen(port, hostname, () => {
    console.log(`接口代理运行在 http://${hostname}:${port}/`);
});

// 创建一个图片代理服务
const imgServer = http.createServer((req, res) => {
    const url = req.url.split('/img/')[1];
    const options = {
        url: url,
        encoding: null
    };

    function callback (error, response, body) {
        if (!error && response.statusCode === 200) {
            const contentType = response.headers['content-type'];
            res.setHeader('Content-Type', contentType);
            res.setHeader('Access-Control-Allow-Origin', '*');
            res.end(body);
        }
    }
    request.get(options, callback);
});

// 监听8011端口
imgServer.listen(imgPort,hostname,()=>{
	console.log(`图片代理运行在http://${hostname}:${imgPort}/`);
})
```     

node下运行 `node proxy.js` 开启代理          

接口的ajax请求：     
*可以jq的$ajax或vue-resource或推荐的axios*     

axios做异步请求：     

`npm i axios --save`      

项目中使用工具函数可以封装放到libs文件夹        
新建util.js封装axios：      

```
import axios from 'axios';
// 基本配置
const Util = {
	imgPath:'http://127.0.0.1:8011/img/',
	apiPath:'http://127.0.0.1:8010/'
}

// ajax通用配置
Util.ajax = axios.create({ //自定义配置新建一个 axios 实例
	baseURL:Util.apiPath
})

// 添加响应拦截器 在响应被 then 或 catch 处理前拦截它们。
Util.ajax.interceptors.response.use(res=>{
	return res.data;
});

export default Util;
```

使用例如：          

```
import $ from './libs/util';

$.ajax.get('news/3892357').then(res=>{
    var title = res.title;
    console.log(title)
})
```

插件concurrently用于script同时执行多个命令       

`npm i concurrently --save-dev`         
  
package.json的script里设置：       

`"start": "concurrently \"npm run dev\" \"node proxy.js\""`         

