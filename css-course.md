# css知识点    

* [1. css3必会技巧](#1)  
    * [2.1 认识css3](#2)   
    * [2.2 选择器，伪类伪元素和优先级](#3)   
    * [2.3 Flex弹性盒布局](#4)   
    * [2.4 垂直水平居中方法](#5)   
    * [2.5 左右栏宽度固定，中间栏宽度自适应](#6)   
    * [2.6 媒体查询](#7)   
    * [2.7 rem响应式设计](#8)   
    * [2.8 多列](#9)   
    * [2.9 Transform/Transition/Animation](#10)   
    * [2.10 常用特性](#11)   
    * [2.11 老浏览器bug](#12)     
    * [2.12 css预编译：less/sass/stylus](#13)     
   
<h2 id="1">css3必会技巧</h2>     

<h3 id="2">认识css3</h3>                 
     
CSS层叠样式表     

移动web的css3现状：     
可访问[w3c现状网站](https://www.w3.org/Style/CSS/current-work)查看。      
w3c标准和浏览器实现是个齐头并进，互相影响的过程，想知道某个css3属性在浏览器支持情况，可以访问[caniuse](https://caniuse.com/)      

ios上safari的版本与操作系统绑定，ios safari列12表示系统是ios12     
android5之前，原生浏览器与系统绑定。从5开始浏览器版本可以单独更新。       
Hybrid APP即在app内部通过webview组件访问web页面的情况， 内核即原生浏览器内核。     
ios不会有厂商定制的情况，其次所有第三方浏览器都被强制使用了ios自带的内核。    

[Modernizr](https://modernizr.com/)：      
一个用于检测用户浏览器的html5和css3特性的js库。 [中文网](http://modernizr.cn/)         

盒模型：      
box-sizing 属性     
content-box：width和height只包括内容的宽和高。在宽度和高度之外绘制元素的内边距和边框。    
border-box：width和height包括内边距和边框。为元素指定的任何内边距和边框都将在已设定的宽度和高度内进行绘制。   

个性字体：     
@font-face 允许指定在线字体。常见用途是IconFont把图标制作成字体。    

自适应布局：     
calc函数在渲染时动态计算属性值。常被用在自适应布局。     

```
.container{			
	width: 200px;
	height: 200px; /* 值发生变化时，整个布局保持不变 */
	background: green;
	}
	.header{					
	background: red;
	height: 50px;
	}
	.content{					
	background: blue;
	height: calc(100% - 50px);
}

<div class="container">				
	<div class="header"></div>		
	<div class="content"></div>			
</div>
```

其他常用css特性：      
圆角边框，字体阴影。      
响应式布局Media Queries、弹性布局Flexbox、多列布局Multi-column Layout     
过度与动画效果        

<h3 id="3">选择器，伪类伪元素和优先级</h3>      

选择器：
浏览器支持较好，比较常用的css选择器：      

[attribute^=value]	    
a[src^="https"]  选择其 src 属性值以 "https" 开头的每个a元素。     

[attribute$=value]       
a[src$=".pdf"]  选择其 src 属性以 ".pdf" 结尾的所有a元素。    

[attribute*=value]      
a[src*="abc"]  选择其 src 属性中包含 "abc" 子串的每个a元素。      

:first-of-type      
p:first-of-type  选择属于其父元素的首个p元素的每个p元素。     

:last-of-type     
p:last-of-type  选择属于其父元素的最后p元素的每个p元素。      

:only-of-type     
p:only-of-type  选择属于其父元素唯一的p元素的每个p元素。     

:only-child       
p:only-child  选择属于其父元素的唯一子元素的每个p元素。       

:nth-child(n)       
p:nth-child(2)  表示这个元素要是p标签，且是第二个子元素，是两个必须满足的条件。      

:nth-of-type(n)      
p:nth-of-type(2)  表示父标签下的子元素里边找第二个p标签。       

div+p  表示div元素之后紧跟的p元素     

div>p  选取父元素是div元素的每个p元素      

简单的一个例子：     

```
* { margin: 0; padding: 0; }				
body { background: #F0F0F0; }			
header {
	height: 48px;					
	line-height: 48px;				
	background: #2e353d;			
	color: white;				
	font-size: 16px;				
	text-align: center;				
}
header+#content { margin-top: 20px }	
#content { padding: 10px; }
input, button { width: 100%; }
input[type="text"], input[type="password"] {
	height: 35px;
	margin-top: 10px;
}
button { height: 30px; margin-top: 20px; }

<header>用户登录</header>						
<div id="content">								
	<input type="text" value="tom"><br>				
	<input type="password" value="123456">			
	<button>登录</button>						
</div>
```

伪类：     
用了指定选择器的某种特定状态或条件。伪类在DOM中不存在，对用户可见。     

动态伪类：
a:link a:visited a:hover a:active input:focus    
*顺序：a:link a:visited a:hover a:active*     

目标伪类：      
\#tab1:target 匹配活动的锚      '

语言伪类：     
p:lang(en) 匹配带有指定lang属性的元素      

UI元素状态伪类：      
input:enabled 匹配启用的元素。     
input:disabled 匹配禁用的元素。     
input:checked 匹配选中的元素。     

结构性伪类：    
:nth-child(n) :nth-of-type(n)等    
*n可以写成表达式an+b，a和b可以是0或正整数。如2n，2n+1等*     

否定伪类：    
input:not([type="text"]) 匹配所有非指定类型的其他元素      

伪元素：     
不存在文档树中的抽象内容，如元素内容的第一个字母或第一行。     

`p::first-letter{color:red;} <!--第一个字母设为红色 --> `  

::selection{color:red;}选中内容变成红色        
css3选择器 ::selection 可写属性：color、background、cursor 以及 outline。     

::first-line 文本内容的首行     
::first-letter 文本内容的首个字母     
::before 元素之前     
::after 元素之后     

*css1,2中伪元素一个冒号，css3为区分伪元素和伪类，用两个冒号。两种格式效果一样*     
*使用::before或::after必须设置content属性。可设为空。做特殊阴影一般要用到伪元素的after和before*      

```
span::before {
	display: inline-block;				
	width: 4px;				
	height: 14px;				
	margin-right: 10px;				
	background: #198be5;			
	content: "";							
}
p::first-letter { color: red }
p::first-line { font-style: italic }
p::after {
	display: block;
	height: 1px;
	content: "...";
}

<span>Pseudo-elements</span>
<p>Pseudo-elements create abstractions about the document tree beyond those specified by the document language. </p>
```

优先级和权重：      

四个级别权重由高到低0,0,0,0：     
内联样式     
ID选择器     
类，伪类，属性选择器     
元素，伪元素     

同位比较如：     
ul li： 2个元素选择器，权重0,0,0,2     
ul li.item 2个元素选择器，1个类选择器，权重0,0,1,2     
*通配符和继承的属性0,0,0,0*    

拥有相同权重的，定义在style后边的会覆盖前面与之相同属性的规则，而不是看标签中的先后。如：     

```
<style>
	.red{color:red;}
	.blue{color:blue;}
</style>

<div class="blue red">这里是蓝色</div>
```    

!important写在css规则后面，可以将对应规则提升到最高权重，想覆盖唯一做法是在此规则后面再定义一个!important     

浏览器解析选择器的时候按照从右到左的顺序进行，导致更多层级的选择器嵌套在查找时更费时，用更简短更容易被查找的选择器是一个好习惯。       

*css浏览器默认属性要大于继承属性*     

<h3 id="4">Flex弹性盒布局</h3>       

[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)          
[Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)            
[Flex 布局最简单表单](http://www.ruanyifeng.com/blog/2018/10/flexbox-form.html)              

任何一个容器都可以指定为 Flex 布局:        

`.box{display: flex;}`         

行内元素也可以使用 Flex 布局:         

`.box{display: inline-flex;}`          

设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。         

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。     

容器的属性:       

flex-direction 决定主轴的方向            
flex-wrap 定义，如果一条轴线排不下，如何换行。默认不换行         
flex-flow 是flex-direction属性和flex-wrap属性的简写形式            
justify-content 定义了项目在主轴上的对齐方式(类似水平对其方式)                          
align-items 定义项目在交叉轴上如何对齐(类似垂直对齐方式)                  
align-content 定义了多根轴线的对齐方式(类似多行垂直对其方式)               

项目的属性：           

order 定义项目的排列顺序。数值越小，排列越靠前，默认为0            
flex-grow 定义项目的放大比例，默认为0(分配剩余空间)                         
flex-shrink 定义了项目的缩小比例，默认为1           
flex-basis 定义了在分配多余空间之前，项目占据的主轴空间            
flex 是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto              
align-self 许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性            
    
<h3 id="5">垂直水平居中方法</h3>        

flex等宽垂直水平居中布局：       
     
```
.box{
	display:flex;
	justify-content:center; /*水平居中*/
	align-items:center; /*垂直居中*/
	background:#0099cc
}
h1{
	color:#fff;
	border: 1px solid #000;
	flex: 1 /*每一项目的宽度相同*/
}

<div class="box">
    <h1>flex弹性布局</h1>
    <h1>flex弹性布局</h1>
    <h1>flex弹性布局</h1>
</div>
```    

position定宽高垂直水平居中：   
   
```
.box {
	background-color: #666;
	height: 400px;
	width: 400px;
	margin-top: -200px;
	margin-left: -200px;
	position: absolute;
	left: 50%;
	top: 50%;
}

<div class="box">内容在这里</div>
```     

transform子元素不定高垂直水平居中：    

```
.box {
	background-color: #666;
	width: 400px;
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
}

<div class="box">内容在这里</div>
```    

flex父元素不定宽垂直水平居中：     

```
.container {  
	height:200px;
	display: flex;
	border: 1px solid gray;
}
.box {
	width: 60px;
	height:60px;
	background: gray;
	margin:auto;
}

<div class="container">
	<div class="box"></div>
</div>
```  

display:box定宽高垂直水平居中：       
*09年的规范，注意要加浏览器前缀*     

```
.center{ 
	width:300px; 
	height:200px; 
	padding:10px; 
	border:1px solid #ccc; 
	margin:20px auto; 
	display:-webkit-box; 
	-webkit-box-orient:horizontal; 
	-webkit-box-pack:center; 
	-webkit-box-align:center; 
	display:-moz-box; 
	-moz-box-orient:horizontal; 
	-moz-box-pack:center; 
	-moz-box-align:center; 
	display:-o-box; 
	-o-box-orient:horizontal; 
	-o-box-pack:center; 
	-o-box-align:center; 
	display:-ms-box; 
	-ms-box-orient:horizontal; 
	-ms-box-pack:center; 
	-ms-box-align:center; 
	display:box; 
	box-orient:horizontal; 
	box-pack:center; 
	box-align:center; 
} 
.text{ 
	border:1px solid #dedede; 
	padding:2px; 
} 

<div class="center">
	<img src="http://www.w3cplus.com/sites/default/files/source/webdesign.jpg" alt=""/> 
</div> 

<div class="center"> 
    <div class="text">我就一行文字</div> 
</div> 

<div class="center"> 
    <div class="text"> 
        <p>我是多行文行文字 </p>
        <p>我是多行文文字 </p>
        <p>我是多行</p>
    </div> 
</div> 
```

display:table不定宽高垂直水平居中：   

```
.wrap{ 
	height: 200px;
	width: 200px;
	text-align: center;
	border: #eee 1px solid;
	display:table;
} 
.content{ 
	vertical-align:middle; 
	display:table-cell; 
} 

<div class="wrap">
	<div class="content">
		<p>table-cell的方法兼容到ie8</p>
		<p>啊啊</p>
		<p>啊啊啊啊啊啊啊啊啊</p>
	</div>
</div>
```
   
<h3 id="6">左右栏宽度固定，中间栏宽度自适应</h3>          

左右栏宽度固定，中间栏宽度自适应的布局float:     

```
.left{float: left;width: 100px;background: #abcccc;}
.right{float: right;width: 100px;background: #ccc;}
.middle{margin:0 110px;background: #abcdef;}

<div class="left">左边内容左边内容左边内容左边内容左边内容左边内容</div>
<div class="right">右边内容右边内容右边内容右边内容右边内容右边内容</div>
<div class="middle">中间内容中间</div>
```

左右栏宽度固定，中间栏宽度自适应的布局table:      
*三栏高度统一*

```
table{width: 100%;}
.middle{background: #abcdef;padding: 0 10px;}
.left{background: #abcccc;width: 100px;}
.right{background: #ccc;width: 100px;}

<table>
<tr>
	<td class="left">左边</td>
	<td class="middle">不能对单元格td设置margin属性来调整单元格与单元格之间的距离不能对单元格td设置margin属性来调整单元格与单元格之间的距离不能对单元格td设置margin属性来调整单元格与单元格之间的距离不能对单元格td设置margin属性来调整单元格与单元格之间的距离不能对单元格td设置margin属性来调整单元格与单元格之间的距离</td>
	<td class="right">右边</td>
</tr>
</table>
```   

左右栏宽度固定，中间栏宽度自适应的布局grid：       
*三栏高度统一*       
[grid布局](http://www.css88.com/archives/8506)

```
.middle{background: #abcdef;margin: 0 10px;}
.left{background: #abcccc;}
.right{background: #ccc;}

<div style="display: grid;grid-template-columns: 100px auto 100px;">
<div class="left">左边内容</div>
<div class="middle">网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局网格布局</div>
<div class="right">右边内容右边内容右边内容右边内容右边内容右边内容右边内容</div>
</div>
```

左右栏宽度固定，中间栏宽度自适应的布局flex:      
*三栏高度统一*      

```
.wrapper{display: flex;width: 100%;}
.middle{background: #abcdef;flex:1;margin:0 10px;}
.left{background: #abcccc;width: 100px;}
.right{background: #ccc;width: 100px;}

<div class="wrapper">
	<div class="left">苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果苹果</div>
	<div class="middle">香蕉香蕉香蕉香蕉香蕉</div>
	<div class="right">水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃水蜜桃</div>
</div>
```   

<h3 id="7">媒体查询</h3>          

支持css3媒体查询polyfill： respond.js mediaqueries.js       

媒体查询定义在css中:    
`@media(max-width:320px){}`          

媒体查询定义在页面link中：      
`<link rel="stylesheet" href="a.css" madei="(min-width="640")">`        

媒体查询的条件是多个：    
`@media(max-width:320px),handled{}`     

采用not实现多个条件非的逻辑运算：     
`@media not (max-width:320px),handled{}`     

媒体查询类型：     
all：全部类型     
print：打印设备     
screen：显示器     
speech：辅助设备     

媒体属性：    
width:viewport的宽度    
height:viewport的高度    
aspect-ratio:viewport的宽高比     
orientation:设备横竖屏 portrait和landscape      
resolution:设备分辨率    

<h3 id="8">rem响应式设计</h3>          

em相对于当前元素的字体大小计量单位。     
rem相对于根元素的字体大小。    
[rem与em的使用和区别详解](http://caibaojian.com/rem-vs-em.html)     

rem布局，首先对根元素字号赋值，为了便于计算，实例中使用实际宽度除以10的大小作为根元素字号：     
*注意：并非所有单位都需要转成rem，比如字体大小仍用px。容器中元素直接使用百分比也比较常用。*       

```
<!-- 设置viewport为设备宽度 -->
<meta name="viewport" content="width=device-width" />

/* 设置页面基础字号，并清除页面的默认边距 */
body { font-size:12px; margin:0; }
/* 设置容器宽度，并居中显示 */
.btns { width:10rem; margin:0 auto; }
/* 定义每个按钮的样式 */
.btns > a { float:left; width:2.5rem; text-align:center; padding-top:0.2rem; }
/* 定义按钮的子元素圆 */
.btns > a > i { display: inline-block; width: 1.2rem; height: 1.2rem; background: gray; border-radius: 50%; }
/* 定义按钮文字样式 */
.btns > a > span { display:block; line-height:0.8rem; font-size:14px; }

(function () { 
	// 获取根元素对象，既HTML
	var de = document.documentElement;
	// 重置根元素的字号大小
	function resetFontSize() {
		// 获取浏览器宽度
		var w = de.getBoundingClientRect().width;
		// 设置一个最大宽度，避免在iPad等设备下过渡放大
		if (w > 640) w = 640;
		// 为根元素字号赋值
		de.style.fontSize = (w / 10) + 'px';
	}
	// 页面一加载就为根元素字号赋值
	resetFontSize();
	// 页面大小改变时，重新设置根元素字号
	window.addEventListener('resize', resetFontSize, false);
})();
```

<h3 id="9">多列</h3>          

多列布局是块级布局模式的扩展，必须作用在块元素上。     
多列布局是针对文本排版布局，常出现在报刊中，跟通常页面的左中右布局是两个概念：     

column-count:指定元素应该被分割的列数。         
column-fill:指定如何填充列           
column-gap:指定列与列之间的间隙            
column-rule:所有 column-rule-* 属性的简写              
column-rule-color:指定两列间边框的颜色            
column-rule-style:指定两列间边框的样式             
column-rule-width:指定两列间边框的厚度            
column-span:指定元素要跨越多少列           
column-width:指定列的宽度           
columns:设置 column-width 和 column-count 的简写                

```
#col{column-width: 200px;}/* 固定每列文本宽度为200px，具体列数不定 */

#col{column-count: 3;}/* 固定分成3列，每列宽度不固定*/

#col {
	column-width: 200px; /* 固定每列文本宽度为200px */
	column-gap: 30px; /* 列间距为30px */
	column-rule: 10px solid red; /* 设置列标记的宽度，样式，颜色 */
}

<div id="col">很多文本内容。。。</div>
```

<h3 id="10">Transform/Transition/Animation</h3>          

transform转换：    

`transform: none|transform-functions;`         

移动translate     
缩放scale     
旋转rotate     
倾斜skew      
定义2D自定义转换matrix      
定义3D自定义转换matrix3d      
定义3D转换元素定义透视视图perspective(n)    

```
/* 定义一个容器，并指定观察者距离为100像素 */
.box {width: 640px; margin: 0 auto; perspective: 100px;}

/* 定义容器中的每一项，设置背景颜色为灰色 */
.box> div {float: left; width: 120px; height: 80px; margin: 40px 20px; background-color: gray;}

/* 定义变形元素，设置背景颜色为黑色 */
.box a {display:block; height: 80px; background-color: black; text-align: center; color: white;}

/* transform的默认值：none */
.box .none {transform: none;}

/* 2D位移：向右方和下方分别移动10像素 */
.box .translate {transform: translate(10px, 10px);}

/* 3D位移：沿Z轴向内位移30像素 */
.box .translate3d {transform: translate3d(0, 0, -30px);}

/* 2D缩放：沿X轴缩小到0.8倍，沿Y轴放大到1.2倍 */
.box .scale {transform: scale(0.8, 1.2);}

/* 3D缩放：X轴和Y轴比例不变，沿Z轴放大到1.5倍（为便于观察变化，同时将元素旋转10度） */
.box .scale3d {transform: scale3d(1, 1, 1.5) rotateX(10deg);}

/* 2D旋转：将元素顺时针旋转30度 */
.box .rotate {transform: rotate(30deg);}

/* 3D旋转：在3D空间X=1，Y=0.2，Z=0的向量上，顺时针旋转30度*/
.box .rotate3d {transform: rotate3d(1, 0.2, 0, 30deg);}

/* 2D倾斜：将元素在X轴上倾斜30度 */
.box .skew {transform: skew(30deg, 0);}

<!-- 定义容器 -->
<div class="box">
<!-- 不变形 -->
<div><a class="none">none</a></div>

<!-- 2D位移变形 -->
<div><a class="translate">translate<br />(10px, 10px)</a></div>

<!-- 3D位移变形 -->
<div><a class="translate3d">translate3d<br />(0, 0, -30px)</a></div>

<!-- 2D缩放变形 -->
<div><a class="scale">scale<br />(0.8, 1.2)</a></div>

<!-- 3D位移变形 -->
<div><a class="scale3d">scale3d<br />(1, 1, 1.5)<br />rotateX(10deg)</a></div>

<!-- 2D旋转变形 -->
<div><a class="rotate">rotate<br />(30deg)</a></div>

<!-- 3D旋转变形 -->
<div><a class="rotate3d">rotate3d<br />(1,0.2,0,30deg)</a></div>

<!-- 2D倾斜变形 -->
<div><a class="skew">skew<br />(30deg,0)</a></div>
</div>
```

*注意：3d变换函数需要配合perspective使用，变形基点通过transform-origin属性修改*       
   
文档流中zoom加在任意元素都会引起整个页面重绘，transform:scale()只是当前元素上的重绘。       
scale只支持数值，根据给定的宽度（X 轴）和高度（Y 轴）参数。可以是负值。居中缩放。缩放占据原始尺寸不变。       
zoom可以是百分比，不可以是负值。缩放相对左上角，缩放改变了元素占据空间的大小。      

rotateX像笔记本，y像翻书，z像钟表。可设置旋转元素基点位置    

```
transform:rotate(45deg);
transform-origin:left;
perspective属性 ，定义3d元素距离视图的距离。加载3d元素的父元素上，都加父元素上。如：
perspective:500;距离屏幕500px
perspective-origin:50% 50%;视角正中
transform-style:perserve-3d;变成3d
backface-visibility:hidden;隐藏被旋转的元素
```   

Transition过渡：      

过渡是元素从一种样式逐渐改变为另一种的效果:            
要实现这一点，必须规定两项内容：             
规定您希望把效果添加到哪个 CSS 属性上            
规定效果的时长          

向多个样式添加过渡效果，添加多个属性，由逗号隔开:    

`transition:width 2s, height 2s;`        

`transition: property duration timing-function delay;`         

简写：`transition:width 2s ease 1s `          

transition-property 规定设置过渡效果的 CSS 属性的名称。     
transition-duration 规定完成过渡效果需要多少秒或毫秒。     
transition-timing-function 规定速度效果的速度曲线。     
transition-delay 定义过渡效果何时开始。           

transition-timing-function:     
linear 规定以相同速度开始至结束的过渡效果（等于 cubic-bezier(0,0,1,1)）。            
ease 规定慢速开始，然后变快，然后慢速结束的过渡效果（cubic-bezier(0.25,0.1,0.25,1)）。             
ease-in 规定以慢速开始的过渡效果（等于 cubic-bezier(0.42,0,1,1)）。            
ease-out 规定以慢速结束的过渡效果（等于 cubic-bezier(0,0,0.58,1)）。              
ease-in-out 规定以慢速开始和结束的过渡效果（等于 cubic-bezier(0.42,0,0.58,1)）。            
cubic-bezier(n,n,n,n) 在 cubic-bezier 函数中定义自己的值。可能的值是 0 至 1 之间的数值。             

*当css3的transition动画执行结束时，触发webkitTransitionEnd事件*      

Animation动画：      

animation和transition不同的是，animation只将定义好的动画应用到元素1次或n次。并不会对元素最初的样式造成影响。       
            
`animation: name duration timing-function delay iteration-count direction;`       
         
animation-name 规定需要绑定到选择器的 keyframe 名称               
animation-duration 规定完成动画所花费的时间，以秒或毫秒计。     
animation-timing-function 规定动画的速度曲线。     
animation-delay 规定在动画开始之前的延迟。     
animation-iteration-count 规定动画应该播放的次数。     
animation-direction 规定是否应该轮流反向播放动画。    

动画轮流反向播放              
animation-iteration-count: n | infinite;    
animation-direction: normal | alternate;      

CSS3 @keyframes 规则:           
@keyframes 规则用于创建动画。在 @keyframes 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果。              

在@keyframes中创建动画时，把它捆绑到某个选择器，否则不会产生动画效果。              
通过规定至少以下两项 CSS3 动画属性，即可将动画绑定到选择器：                  
规定动画的名称              
规定动画的时长               

```
.img { position:fixed; top:-400px; width:500px; }		
.img.show { animation:move 2s ease 1 normal; }

@keyframes move {
	0% { top:-400px; }
	50% { top:20px; }
	100% { width:1000px; }
}

帧动画：animation-timing-function规定动画曲线              
作用于每两个关键帧之间，而不是整个动画                
             
steps函数，它可以传入两个参数，第一个是一个大于0的整数，他是将间隔动画等分成指定数目的小间隔动画。             
第二个参数设置后其实和step-start，step-end同义，在分成的小间隔动画中判断显示效果。               
          
steps(1,start)等同于step-start动画分成一步，动画执行时为开始左侧端点的部分为开始        
steps(1,end)等同于step-end动画分成一步，动画执行时以结尾端点为开始，默认是end            

```
<div class="p1 page"></div>

.page{animation:name 1s steps(1,start) infinite;}
@keyframes name{
	0%{bakcground-position:0 0;}
	50%{bakcground-position:0 0;}
	100%{bakcground-position:-350px 0;}
}

.p1{background: url(abc.png) no-repeat;width: 455px;height: 329px;}
```

```
@-webkit-keyframes circle { 
0% {background: red} 
50%{background: yellow} 
100% {background: blue} 
} 
```
      
step-start ： 黄色与蓝色相互切换              
step-end ： 红色与黄色相互切换              
2个参数都会选择性的跳过前后部分，start跳过0%，end跳过100%             

<!-- 在页面加载后对img应用新的样式 -->
<body onload="document.querySelector('.img').className+=' show'">

<!-- 定义一张默认隐藏的图片 -->
<img class="img" src="http://pic.qiantucdn.com/01/37/07/67bOOOPICff.jpg" />
```

*当css3的animation动画执行结束时，触发webkitAnimationEnd事件*      

<h3 id="11">常用特性</h3>          

字体格式、背景、颜色、文字效果、边框、用户界面等     

@font-face:    

```
@font-face {
	font-family: 'fontello';
	src: url('./fonts/fontello.eot?68514474');
	src: url('./fonts/fontello.eot?68514474#iefix') format('embedded-opentype'),
		url('./fonts/fontello.woff?68514474') format('woff'),
		url('./fonts/fontello.ttf?68514474') format('truetype'),
		url('./fonts/fontello.svg?68514474#fontello') format('svg');
	font-weight: normal;
	font-style: normal;
}
.demo-icon {
	font-family: "fontello";	/*字体名*/
	font-style: normal;		/*字体样式*/
	display: inline-block;		/*行内块元素*/
	font-size: 42px;		/*字体大小*/
	margin-right: 5px;		/*元素的右外边距*/
}

<i class="demo-icon icon-glass">&#xe800;</i>
<i class="demo-icon icon-music">&#xe801;</i>
<i class="demo-icon icon-search">&#xe802;</i>
<i class="demo-icon icon-mail">&#xe803;</i>
```

background:   

css3新增background-origin/background-clip/background-size      

[background-origin](http://www.w3school.com.cn/tiy/c.asp?f=css_background-origin):       
background-origin: padding-box|border-box|content-box;                      
规定背景图片的定位区域,改变background-position的原点位置：           

```
.square-01,.square-02,.square-03 {
	color: #fff;
	text-align: center;
	line-height: 100px;
	float: left;
	margin-right: 10px;
	padding: 10px;
	width: 150px;          
	height: 100px;			
	border: 10px dashed #333; 
	background-position: 0 0;
	background-color: gray;
	background-image: url('./square.png');
	background-repeat: no-repeat;
}
.square-01 {
	background-origin: padding-box;
	-webkit-background-origin: padding-box;
}
.square-02 {
	background-origin: border-box;
	-webkit-background-origin: border-box;
}
.square-03 {
	background-origin: content-box;
	-webkit-background-origin: content-box;
}

<div class="square-01">padding-box</div>
<div class="square-02">border-box</div>
<div class="square-03">content-box</div>
```

background-clip:       
背景区域绘制剪裁background-clip:content-box padding-box border-box(默认)      
规定背景的绘制区域：      

```
.square-01,.square-02,.square-03 {
	color: #000;
	text-align: center;
	line-height: 100px;
	float: left;
	margin-right: 10px;
	padding: 10px;
	width: 150px;          
	height: 100px;			
	border: 10px dashed #333; 
	background-color: yellow;
}
.square-01 {
	background-clip: padding-box;
	-webkit-background-clip: padding-box;
}
.square-02 {
	background-clip: border-box;
	-webkit-background-clip: border-box;
}
.square-03 {
	background-clip: content-box;
	-webkit-background-clip: content-box;
}

<div class="square-01">padding-box</div>
<div class="square-02">border-box</div>
<div class="square-03">content-box</div>
```

[background-size](http://www.w3school.com.cn/tiy/c.asp?f=css_background-size):          
background-size: length|percentage|cover|contain;           
规定背景图片尺寸。       

```
.square-01,.square-02,.square-03,.square-04 {
	color: #000;
	text-align: center;
	line-height: 100px;
	float: left;
	margin-right: 10px;
	padding: 10px;
	width: 150px;           
	height: 100px;			
	border: 2px dashed #333; 
	background: url('./cccat.jpg') no-repeat;
}
.square-01 {
	background-size: 50px 50px;
}
.square-02 {
	background-size: 50%;
}
.square-03 {
	/*把背景图片扩至足够大，使图完全覆盖背景区域。图也许显示不全。*/
	background-size: cover;
}
.square-04 {
	/*把图像扩至最大尺寸，以使其狂傲完全适应内容区域*/
	background-size: contain;
}

<div class="square-01"></div>
<div class="square-02"></div>
<div class="square-03"></div>
<div class="square-04"></div>
```

css3多重背景，把不同背景放到一个元素中：     
多个url之间逗号隔开：          

```
.multiple {
	color: #000;
	text-align: center;
	line-height: 100px;
	float: left;
	margin-right: 10px;
	padding: 10px;
	width: 150px;           
	height: 100px;			
	border: 2px dashed #333;
	background: url('./cccat.jpg') no-repeat 10px 10px,url('./cccat.jpg') no-repeat 30px 30px,url('./cccat.jpg') no-repeat 50px 50px;
	background-size: 50px;
}

<div class="multiple"></div>
```

color颜色：     

颜色的取值：           
`color:red;`      

HEX:十六进制表示颜色值：     
`color:#000`     

RGB:rgb(255,255,255) = rgb(100%,100%,100%) = #ffffff = #fff        
`color:rgb(0,0,0)`     

RGBA:色彩模式与RGB相同，新增Alpha透明度:      
*ie6-8不支持rgba，需要通过滤镜实现*       
`color:rgba(0,0,0,0.5) /*黑色字体，百分之50不透明度*/`          

HSL:H为色调，取值0-360， S饱和度,L亮度，0.0%-100%，：      
`color:hsl(360,50%,50%)`     

HSLA：比HSL多透明度：      
`color:hsl(360,50%,50%,0.5)`      

transparent：指定全透明色彩：      
`color:transparent;`      

currentcolor:css3标准关键字，当前标签所继承的文字颜色：      
`color:red;border:1px solid currentcolor /*1像素的红色边框*/`     

gradient渐变：       
线性渐变 linear-gradient          
径向渐变 radial-gradient           

opacity属性：设置元素的不透明级别：       
filter:alpha(opacity=50)      

*opacity常用于改变大型单一元素，如遮罩层。而当元素的后代元素较多或结构复杂，应用rgba代替。*         
       
设置透明：`background:#000;opacity:.7;filter:alpha(opcity=70);`          
       
文字效果：     

text-shadow向文本设置阴影：     

text-shadow: h-shadow v-shadow blur color;     

h-shadow 必需。水平阴影的位置。允许负值。        
v-shadow 必需。垂直阴影的位置。允许负值。       
blur 可选。模糊的距离。      
color 可选。阴影的颜色。      

```
.demo {
	background: #666666;
	width: 440px;
	padding: 10px;
	font: bold 55px/100% "微软雅黑", "Lucida Grande", "Lucida Sans", Helvetica, Arial, Sans;;
	color: #fff;
	margin: 10px;
	}
.text-effect1 {
	text-shadow: 0 0 20px red;
}
.text-effect2 {
	color: #000;
	text-shadow: 0 1px 1px #fff;
}
.text-effect3 {
	color: #ccc;
	text-shadow: -1px -1px 0 #fff,1px 1px 0 #333,1px 1px 0 #444;
}

<p class="demo text-effect1">成为更好的自己</p>
<p class="demo text-effect2">成为更好的自己</p>
<p class="demo text-effect3">成为更好的自己</p>
```

text-overflow:规定当文本溢出包含元素时发生的事情：      

单行文本溢出省略号：     

```
div{
	width:200px;
	overflow:hidden;
	text-overflow:ellipsis;
	white-space:nowrap;
	word-break:keep-all; /*只能在半角空格或连接字符出换行*/
	display:block;/*内联对象需加*/		
}

<div>内容内容内容内容内容内容内容</div>
```  

多行文本溢出省略号(仅chrome支持)：    

```
div{
	text-overflow:ellipsis;
	overflow:hidden;
	display:-webkit-box;
	-webkit-line-clamp:2;
	-webkit-box-orient:vertical;
	width:200px;	
}

<div>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容</div>
```  

表格文字溢出显示省略号：      

```
table{ 
width:300px; 
table-layout:fixed;/* 只有定义了表格的布局算法为fixed，下面td的定义才能起作用。 */ 
} 
td{ 
word-break:keep-all;/*只能在半角空格或连接字符出换行*/ 
white-space:nowrap;/* 不换行 */ 
overflow:hidden;/* 内容超出宽度时隐藏超出部分的内容 */ 
text-overflow:ellipsis;/* 当对象内文本溢出时显示省略标记(...) ；需与overflow:hidden;white-space:nowrap;一起使用。*/ 
} 

<table>
<tr>
	<td>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容</td>
	<td>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容</td>
	<td>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容</td>
	<td>内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容</td>
</tr>
</table>
```

word-wrap:break-word;允许长单词或url地址自动换行：      

css英文数字自动换行：          

```
div{
	word-wrap:break-word;
	word-break:break-all; /*允许在单词内换行*/
	width:200px;
}

<div>aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa</div>
```       

禁止换行：        
`.nowrap{word-break:keep-all;white-space:nowrap;}`     
      
强制换行：         
`.break{word-break:break-all;white-space:normal;}`      
   
在不想换行的标记上加入样式nowrap，在需要强制换行的地方加入样式break，这样就实现了强制换行与不换行了     

border边框：     

[border-radius](http://www.w3school.com.cn/cssref/pr_border-radius.asp) ,[border-image](http://www.w3school.com.cn/cssref/pr_border-image.asp),[box-shadow](http://www.w3school.com.cn/cssref/pr_box-shadow.asp)         

`border-radius:100px/10px;` 水平100px；垂直10px；        

border-radius      
每个半径的四个值的顺序是：左上角，右上角，右下角，左下角     
            
 `box-shadow:0 1px 4px rgba(0,0,0,.3),0 0 40px rgba(0,0,0,.1) inset;` 逗号后边那套是设置内阴影        

data url就是把图片转换成base64编码的字符串。    
好处是少向服务器请求图片次数。      
缺点base64编码数据体积比普通二进制图片体积大三分之一，ie6,7不支持。    
base64编码放css的background里就能和css文件一起被缓存了。不然data url形式的图片放在页面是不被缓存的。     
移动端不建议用data url形式的图片。

overflow与text-indent(必须是块元素)隐藏文字    

```
line-height:0;font-size:0;overflow:hidden;   
display:block;font-size:0;line-height:0;text-indent:-9999px;   
```   

position:relative不脱离文档流,position:absolute;脱离文档流           

absolute : 将对象从文档流中拖出，使用left，right，top，bottom等属性进行绝对定位。而其层叠通过z-index属性定义。此时对象不具有边距，但仍有补白和边框。        
relative是相对于自己来定位的，例如：#demo{position:relative;top:-50px;},这时#demo会在相对于它原来的位置上移50px。           

想要盒子有尺寸，要不设置宽高，要不绝对定位并且设置四个值top bottom left right       

定位，不随滚动条滚动而滚动：         

```
position:fixed;
top:0;
left:0;
```       

清除浮动方法：          

```
1 .clear{clear:both;}
2 overflow属性{overflow:auto;zoom:1} 可换成 {overflow:hidden;width:100%;}
3 after伪类 .abc:after{display:block;clear:both;content:"";<-- visibility:hidden;height:0; -->}`
4 浮动所有元素，全浮动起来。
```   

置换元素(替换元素):               
        
内容不受CSS视觉格式化模型控制，且元素本身一般拥有固有尺寸（宽度，高度，宽高比）的元素，被称之为置换元素。           
替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。         

例如浏览器会根据img标签的src属性的值来读取图片信息并显示出来，而如果查看(X)HTML代码，则看不到图片的实际内容；             
例如根据input标签的type属性来决定是显示输入框，还是单选按钮等。              
HTML中的img、input、textarea、select、object都是替换元素。这些元素往往没有实际的内容，即是一个空元素。      

做横着的虚线：        

`"width:100px;height:1px;background:url(images/bg.gif) repeat-x;overflow:hidden"`        

或：      

`border-top:1px dashed #C0C0C0;`    
   
做竖着的虚线：            

`border-left:1px dashed #C0C0C0;`             
     
textarea可拖动问题， resize:none;           
        
border:none;实现全兼容：在同一选择符上添加背景属性即可      
 
写邮件需注意：      
不要用背景图      
样式用行内    
图片加alt和title    
尽量写宽度    
布局可以用table     

[css验证](http://jigsaw.w3.org/css-validator/)     
   
```   
/*全局样式*/
body,h1,h2,h3,h4,h5,h6,p,blockquote,dl,dt,dd,ul,ol,li,pre,form,fieldset,legend,button,input,textarea,img{border:none;margin:0;padding:0;}
form,fieldset,legend,button,input,textarea{outline:none;}
body,button,input,select,textarea{font:12px/1.5 '宋体', Arial, Srial, helvetica, sans-serif; color:#666;}
em{font-style:normal;}
ul,ol{list-style:none;}
.clear{line-height:0px;font-size:0px;clear:both;display:block;visibility:hidden;}
.left{float:left;}
.right{float:right;}
```       

<h3 id="12">老浏览器bug</h3>   

ie6双边距bug：元素向一侧浮动，并且给这个元素设置这侧的外边距时出现。   
解决方法：给这个元素加display:inline;    
    
ie6居中布局bug。元素margin:0 auto;不居中。   
解决方法：父元素text-align:center;子元素text-align:left;   
    
ie6内容重复bug。相邻的浮动元素中间插入一段注释。    
解决方法：去掉注释    

```
<style>
div {width:100%;float:left;}
</style>

<div>段落文字</div>
<div>段落文字</div>
<div>段落文字</div><!--引出bug的黑手-->
<div>段落文字</div>
<div>段落文字</div>
```   
   
ie6最小高度:`min-height:400px;height:auto!important;height:400px;`    
   
ie6 3像素bug 浮动元素与非浮动元素相邻时出现。   
解决方法：都浮动。 或者不浮动的加3px负外边距   
   
ie6下1像素bug    
解决办法：    

```
1.height:1px;font-size:1px;overflow:hidden;
2.border-top:1px solid #000;line-height:1px;
```   
   
ie6,7 z-index bug    
子元素设置z-index盖不住与其父元素同级别元素。    
解决方法：设置其父元素z-index      
    
ie6,7在滚动区域内标签使用了（或不使用）position，则会飘出滚动区域，且不随滚动条而滚动    
解决方法：给父级（出现滚动条的元素）加position:relative即可    
    
ie6图片空隙间距bug    

```
1.li浮动，img设block
2.ul设font-size:0
3.img的vertical-align:bottom;
4.img的mragin-bottom:-5px;
```   
   
ie6兼容负值    
解决方法：给负外边距的元素的父元素加zoom:1;   
    
ie6的一个读的问题，如果有以下这些，那么应该把给ie6写的放到最后，因为ie6会读最后一个，比如ie6下一个标签有两个高，那么就读后写的那个。    

```
position:fixed;
bottom:70px;
right:180px;
_position: absolute;
_right:150px;
_bottom: "auto";
```   
   
如果ie6和搜狗出现了显示层的问题，那么把下边这段话加到显示层里边，就行了：     

`<iframe style="background:#F0F9FB;width:100%;height:110px;filter:alpha(opacity=0);-moz-opacity:0"></iframe>`    
    
doctype后一行写条件注释，就能直接写.ie6{}了。比如：         

`<!--[if lt IE 7]><html class="ie6"><![endif]-->`      
    
ie6支持星号*、下划线_ 但是不支持！important；     
i7支持星号*、 ！important但是不支持下划线_；    
ff支持！improtant；    
    
在属性前加下划线(_)，那么此属性只会被IE6解释     
在属性前加星号(*)，此属性只会被IE7解释    
在属性值后面加"\9"，表示此属性只会被IE8解释      

<h3 id="13">css预编译：less/sass/stylus</h3>                 

[less中文网](http://lesscss.cn/)     

less最早版本采用ruby语言实现，当前版本已经换为JavaScript。     

less安装：      

命令行使用：     
nodejs下通过npm安装：       

`npm install less -g`    

命令行用法：     
option为可选参数，source为源文件less文件，destination为编译后的css文件       

`lessc [option option=parameter ...] <source> [destination]`      

less文件可以直接通过命令行进行编译：       

`$ lessc style.less style.css`     

添加-x参数，对编译后的css文件进行压缩：       

`$ lessc -x style.less style.css`       

浏览器使用：    

官网下载脚本或用CDN数据源       

```
<link rel="stylesheet/less" type="text/css" href="styles.less" /> 

<!-- 引入less.js前，定义全局的less对象参数 -->
<script>
  less = {
    env: "development",
    async: false,
    fileAsync: false,
    poll: 1000,
    functions: {},
    dumpLineNumbers: "comments",
    relativeUrls: false,
    rootpath: ":/a.com/"
  };
</script>
<script src="less.js" type="text/javascript"></script>
```

在线less编辑器：     
[http://winless.org/online-less-compiler](http://winless.org/online-less-compiler)      

less使用：        
[less快速入门](https://less.bootcss.com/)      

变量：       
通过@作为标记，less中的变量只能定义一次，可以看做编程语言的常量。     

```
@primaryColor: #44B336;

h1 {color: @primaryColor;}
.title {color: @primaryColor;}
```

生成css代码：     

```
h1 {
  color: #44B336;
}
.title {
  color: #44B336;
}
```

less中除了允许普通变量外，还允许插值变量，可叫变量用在选择器名，属性名上：     

```
@mySelector: title;
.@{mySelector} {
	color: #44B336;
	font-size: bold;
	line-height: 40px;
} 
```    

生成css代码：     

```
.title {
  color: #44B336;
  font-size: bold;
  line-height: 40px;
}
```

嵌套：      

```
#header {
	display: inline;
	float: left;
	h1 {
		font-size: 24px;
		font-weight: bold;
		a {
			color: #44B336;
	  }
	}
}
```

生成css代码：     

```
#header {
  display: inline;
  float: left;
}
#header h1 {
  font-size: 24px;
  font-weight: bold;
}
#header h1 a {
  color: #44B336;
}
```    

嵌套提供&运算符表示父选择器：      

```
<!-- 可以用来应用伪类 -->
a {
	color: #333;
	&:hover {
		color: #44B336
  }
}

<!-- 可以用来生成重复类名 -->
.button {
	&-ok {
		background-color: green;
  }
  &-warn {
    background-color: yellow;
  }
  &-danger {
    background-color: red;
  }
}
```

生成css代码：     

```
a {
  color: #333;
}
a:hover {
  color: #44B336;
}
.button-ok {
  background-color: green;
}
.button-warn {
  background-color: yellow;
}
.button-danger {
  background-color: red;
}
```

混合：    

```
.borderRadius(@radius) {
	-moz-border-radius: @radius;
	-webkit-broder-radius: @radius;
	border-radius: @radius;
}

/* 应用到元素中 */
#header {
	.borderRadius(10px);
}
.btn {
	.borderRadius(3px);
}
```   

生成css代码：     

```
#header {
  -moz-border-radius: 10px;
  -webkit-broder-radius: 10px;
  border-radius: 10px;
}
.btn {
  -moz-border-radius: 3px;
  -webkit-broder-radius: 3px;
  border-radius: 3px;
}
```   

作用域：    
查找变量顺序先局部，没有再向上一级一直到全局：    

```
@primaryColor: #44B336;

#header {
	@primaryColor: #333;
	h1 {
		color: @primaryColor;
  }
}

#footer {
	color: @primaryColor;
}
```

生成css代码：    

```
#header h1 {
  color: #333;
}
#footer {
  color: #44B336;
}
```

sass:      
[sass教程](https://sass-lang.com/guide)     
sass具有两种不同的后缀名对应两种不同的语法：      
最早sass使用缩进语法，用缩进区分代码块。用分号讲具体的样式分开，这种语法使用.sass后缀名     
另一种使用css的块语法，用.scss后缀名    
sass和scss之间可相互导入，可通过sass-convert命令行工具切换。     

sass安装：     
一种通过ruby的包管理工具gem安装ruby编译版本的sass。      
一种通过npm安装nodejs包装的c语言版本的libsass，需要配置c编译环境。     

`npm install node-sass`     

*windows下需安装visual studio或者gcc提供c语言编译环境*      

通过js使用：      
如果安装node-sass，可以选择构建工具进行自动化构建，或者直接通过js编译sass文件。     

图形界面的sass编译器可以用[koala](http://koala-app.com/index-zh.html)     

sass使用：     
和less等预编译器有一些区别，重点简单介绍下区别：     

变量：     
sass变量通过$作为标识符，除了简单变量，还提供列表和map：     

列表是一个一维数组：
`$font-stack: ('Helvetica', 'Arial', sans-serif);`    

可通过nth方法传入变量名和要取值的索引来获得，sass中索引从1开始：     
`nth($font-stack,1)`    

map可以映射任何类型的键值对，甚至可以map间相互嵌套：     
当变量作为插值变量时，要用#{}作为标识。    

```
$break:{
	small:767px,
	medium:992px,
	large:1200px
}

<!-- map-get方法来获取map中的值 -->
@media (min-width: #{map-get($break,small)}) {...}

$name: foo;
$attr: border;
p.#{$name} {
	#{$attr}-color: #44b336;
}
```

混合：    
sass需要用@mixin标记来定义Mixin，通过@include来混入一个Mixin：    

```
@mixin clearfix {
  zoom: 1;
  &:before,
  &:after {
    content: "";
    display: table;
  }
  &:after {
    clear: both;
    visibility: hidden;
    font-size: 0;
    height: 0;
  }
}
// 使用mixin
div {
	@include clearfix;
}
```

生成css代码：    

```
div {zoom: 1; }
div:before, div:after {
    content: "";
    display: table; 
  }
  div:after {
    clear: both;
    visibility: hidden;
    font-size: 0;
    height: 0; 
  }
  ```

函数：
可以使用@function来定义一个方法进行处理：    

```
$grid-width: 40px;
$gutter-width: 10px;

@function grid-width($n) {
	// 可以为不同元素设置不同的格数，间距保持统一
	@return $n * $grid-width + ($n - 1) * $gutter-width;
}

// 生成一个占据五格的sidebar
#sidebar { width: grid-width(5); }
```

生成css代码：    
`#sidebar {width: 240px;}`     

循环与条件语句：     

```
$type: abc;
// 根据type变量生成p选择器的颜色
p {
    @if $type == baidu {
      color: blue;
  } @else if $type == alibaba {
    color: orange;
  } @else if $type == abc {
    color: green;// 因为type为abc，color为green
  } @else {
    color: black;
  }
}
```

@for指令可用来生成一系列的样式：    

```
@for $i from 1 through 3 {
.item-#{$i} { width: 2em * $i;}  // 从item-1到item-3每个增加2em宽度
}
```

生成css代码：     

```
.item-1 {
width: 2em; 
}

.item-2 {
width: 4em; 
}

.item-3 {
width: 6em; 
}
```

[compass](http://compass-style.org/)：      
sass的工具库，在sass基础上，封装了大量使用的模块。包括重置浏览器默认样式，css3生成前缀模块，清除浮动，雪碧图等。      
  
[Compass入门小记](https://blog.csdn.net/qq_15096707/article/details/70216852)   

[stylus中文版参考文档之综述](https://www.zhangxinxu.com/jq/stylus/)              

[Stylus基本使用](https://www.jianshu.com/p/5fb15984f22d)               

