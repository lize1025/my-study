# css知识点   

[css验证](http://jigsaw.w3.org/css-validator/)     

查看浏览器兼容性，[icanuse](https://caniuse.com/)

支持css3媒体查询： respond.js mediaqueries.js  polyfill  
   
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

写邮件需注意：    
不要用背景图    
样式用行内    
图片加alt和title    
尽量写宽度    
布局可以用table    
   
当css3的animation动画执行结束时，触发webkitAnimationEnd事件   
当css3的transition动画执行结束时，触发webkitTransitionEnd事件   
   
文档流中zoom加在任意元素都会引起整个页面重绘，transform:scale()只是当前元素上的重绘。    
scale只支持数值，可以是负值。居中缩放。缩放占据原始尺寸不变。    
zoom可以是百分比，不可以是负值。缩放相对左上角，缩放改变了元素占据空间的大小。   
    
`box-shadow:0 1px 4px rgba(0,0,0,.3),0 0 40px rgba(0,0,0,.1) inset;` 逗号后边那套是设置内阴影    

想要盒子有尺寸，要不设置宽高，要不绝对定位并且设置四个值top bottom left right    

`border-radius:100px/10px;` 水平100px；垂直10px；   

background-position-x 谷歌火狐支持这么写   
   
要想border-color和border-width生效，就要有border-style     

```
border-width:10px 20px;
border-style: solid;
border-color: #f00 #0f0 #00f rgb(250,0,255);
```   
   
outline和border一样，简写只写颜色无效，要写全，如1px solid red   
   
css浏览器默认属性要大于继承属性   
   
设置透明：`background:#000;opacity:.7;filter:alpha(opcity=70);`   
   
做特殊阴影一般要用到伪类的after和before    
   
css3为了区分伪类和伪元素，伪元素采用双冒号写法。   
常见伪类:hover,:link,:active,:target,:not(),:focus。   
常见伪元素::first-letter,::first-line,::before,::after,::selection。   
   
::selection{color:red;}选中内容变成红色    
css3选择器 ::selection 可写属性：color、background、cursor 以及 outline。    
浏览器自持ie9+    
    
`p:first-letter{color:red}` 选择指定选择器下的首字母，必须是块元素下   
*单冒号(:)用于 CSS3 伪类，双冒号(::)用于 CSS3 伪元素。对于 CSS2 中已经有的伪元素，单冒号和双冒号的写法作用是一样的。*     

顺序：a:link a:visited a:hover a:active     
   
背景区域绘制剪裁background-clip:content-box padding-box border-box(默认)   

transition:width 2s ease 1s 最后一个是延时时间，ease是默认值，慢快慢    
    
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
   
ie Trident   
chrome webkit blink   
firefox Gecko   
opera插件和chrome的一样通用   
   
媒体查询引入方式：    

```
<link rel="stylesheet" href="a.css" media="screen">
<link rel="stylesheet" href="a.css" madei="screen and (min-width="640")">
```    

css里写@media(max-width:320px){}    
    
less里的&    

```
.abc{
	width:100px;
	&.def{height:100px;}
}
相当于：
.abc{width:100px;}
.abc.def{height:100px;}

.center(@w:980px,@mgt:0,@mgb:0){
	width:@w;
	margin:@mgt auto @mgb;
}
用的时候:
.head{.center()}
.head-w{.center(1000px,0,20px)}
.content{.head}
```       
   
data url就是把图片转换成base64编码的字符串。    
好处是少向服务器请求图片次数。    
缺点base64编码数据体积比普通二进制图片体积大三分之一，ie6,7不支持。    
base64编码放css的background里就能和css文件一起被缓存了。不然data url形式的图片放在页面是不被缓存的。     
移动端不建议用data url形式的图片。    
    
清除浮动方法    

```
1 .clear{clear:both;}
2 overflow属性{overflow:auto;zoom:1} 可换成 {overflow:hidden;width:100%;}
3 after伪类 .abc:after{display:block;clear:both;content:"";<-- visibility:hidden;height:0; -->}`
4 浮动所有元素，全浮动起来。
```   
    
overflow与text-indent(必须是块元素)隐藏文字    

```
line-height:0;font-size:0;overflow:hidden;   
display:block;font-size:0;line-height:0;text-indent:-9999px;   
```   

box-sizing:content-box(默认的) border-box(w3c的)    
    
textarea可拖动问题， resize:none;    
      
单行文本溢出省略号：     

```
width:300px;
overflow:hidden;
text-overflow:ellipsis;
white-space:nowrap;
word-break:keep-all;
display:block;/*内联对象需加*/ 
```    
   
多行文本溢出省略号(仅chrome支持)：    

```
overflow:hidden;
text-overflow:ellipsis;
display:-webkit-box;
-webkit-line-clamp:2;
-webkit-box-orient:vertical;
width:300px;
```    
   
css英文数字不自动换行    
解决方法：    

```
word-wrap:break-word;
word-break:break-all;
width:300px;
```   
      
div定高垂直居中：   

```
#box {
	background-color: #666;
	height: 400px;
	width: 400px;
	margin-top: -200px;
	margin-left: -200px;
	position: absolute;
	left: 50%;
	top: 50%;
}
```     

div不定高垂直居中：    

```
.box {
	background-color: #666;
	width: 400px;
	position: absolute;
	left: 50%;
	top: 50%;
	transform: translate(-50%,-50%);
```    

flex垂直水平居中：       
[Flex 布局语法教程](https://www.runoob.com/w3cnote/flex-grammar.html)     
*注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。*

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
			width: 33.3%;
		}

<div class="box">
    <h1>flex弹性布局</h1>
    <h1>flex弹性布局</h1>
    <h1>flex弹性布局</h1>
</div>
```

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
.middle{background: #abcdef;margin:0 10px;padding: 0 10px;}
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

/* 禁止换行 */   
`.nowrap{word-break:keep-all;white-space:nowrap;}`   
   
/* 强制换行 */   
`.break{word-break:break-all;white-space:normal;}`   

在不想换行的标记上加入样式nowrap，在需要强制换行的地方加入样式break，这样就实现了强制换行与不换行了    
    
定位，不随滚动条滚动而滚动。   

```
position:fixed;
top:0;
left:0;
```    

对于表格文字溢出的定义：    
以下为引用的内容：    

```
table{ 
width:300px; 
table-layout:fixed;/* 只有定义了表格的布局算法为fixed，下面td的定义才能起作用。 */ 
} 
td{ 
word-break:keep-all;/* 不换行 */ 
white-space:nowrap;/* 不换行 */ 
overflow:hidden;/* 内容超出宽度时隐藏超出部分的内容 */ 
text-overflow:ellipsis;/* 当对象内文本溢出时显示省略标记(...) ；需与overflow:hidden;一起使用。*/ 
}  
```   

border:none;实现全兼容：在同一选择符上添加背景属性即可   
   
position:relative不脱离文档流,position:absolute;脱离文档流         

absolute : 将对象从文档流中拖出，使用left，right，top，bottom等属性进行绝对定位。而其层叠通过z-index属性定义。此时对象不具有边距，但仍有补白和边框。    
relative是相对于自己来定位的，例如：#demo{position:relative;top:-50px;},这时#demo会在相对于它原来的位置上移50px。       
      
置换元素/替换元素:        
     
内容不受CSS视觉格式化模型控制，且元素本身一般拥有固有尺寸（宽度，高度，宽高比）的元素，被称之为置换元素。     
替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。     
例如浏览器会根据img标签的src属性的值来读取图片信息并显示出来，而如果查看(X)HTML代码，则看不到图片的实际内容；    
例如根据input标签的type属性来决定是显示输入框，还是单选按钮等。     
HTML中的img、input、textarea、select、object都是替换元素。这些元素往往没有实际的内容，即是一个空元素。     
   
做横着的虚线：`"width:100px;height:1px;background:url(images/bg.gif) repeat-x;overflow:hidden"`    
   
做竖着的虚线：比如左一个div，右一个div，可以先定义右边的div，然后设置border-left   
     
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
    
doctype后一行写条件注释，比如：      
`<!--[if lt IE 7]><html class="ie6"><![endif]-->`    
那么样式就能直接写.ie6{}了    
    
ie6支持星号*、下划线_ 但是不支持！important；     
i7支持星号*、 ！important但是不支持下划线_；    
ff支持！improtant；    
    
在属性前加下划线(_)，那么此属性只会被IE6解释     
在属性前加星号(*)，此属性只会被IE7解释    
在属性值后面加"\9"，表示此属性只会被IE8解释    

CSS BUG顺口溜：    
    
一、IE边框若显若无，须注意，定是高度设置已忘记；   
   
二、浮动产生有缘故，若要父层包含住，紧跟浮动要清除，容器自然显其中；   
   
三、三像素文本慢移不必慌，高度设置帮你忙；   
   
四、兼容各个浏览须注意，默认设置行高可能是杀手；   
   
五、独立清除浮动须铭记，行高设无，高设零，设计效果兼浏览；   
   
六、学布局须思路，路随布局原理自然直，轻松驾驭html，流水布局少hack，代码清爽，兼容好，友好引擎喜欢迎。   
   
七、所有标签皆有源，只是默认各不同，span是无极，无极生两仪―内联和块级，img较特殊，但也遵法理，其他只是改造各不同，一个*号全归原。   
   
八、图片链接排版须小心，图片链接文字链接若对齐，padding和vertical-align:middle要设定，虽差微细倒无妨。   
   
九、IE浮动双边距，请用display：inline拘。   
   
十、列表横向排版，列表代码须紧靠，空隙自消须铭记。    