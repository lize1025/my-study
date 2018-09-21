# html+PS知识点    

## html:[w3c验证](http://validator.w3.org/)   

支持html5标签：[html5.js](http://cdn.static.runoob.com/libs/html5shiv/3.7/html5shiv.min.js)   

```
<!--[if lt IE 9]>
  <script src="http://cdn.static.runoob.com/libs/html5shiv/3.7/html5shiv.min.js"></script>
<![endif]-->
```   

html5 DOCTYPE及字符编码更简单了。   

```
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<body>
</body>
</html>
```   

html5可省略引号或者用单引号。省略结束标签，如每段都没结束p标签。     
布尔值不写就是true。如`<input type="checkbox" name="" id="" checked>` html4就要`checked="checked"`        

a标签target="_blank"开新标签，其实也可以不是_blank。可以随便写  
   
<base\> 标签的href属性：    
为页面中所有的元素的href属性设置了基础值（对元素href为绝对路径的元素不起作用）    
当这些元素进行跳转时，都会基于当前目录加上这个默认的URL（相对路径的情况下）再加上自己的href属性值来跳转。    
     
<base\>标签的target="_blank"可以控制全部a标签打开新页面，href可以给所有a标签的href加前缀，控制台下看a是看不到加上了的。   
   
form里`action="http://baidu.com/s"`然后input里name="wd"，这样submit提交的结果就从百度里找   
   
表单radio的name要相同，id不同。所有表单标签，需要提交数据的，都要加name    
   
label里for，关联到input里的id即可一同选中。   
   
input中autocomplete 属性是 HTML5 中的新属性。     
autocomplete="off" 属性规定输入字段是否应该启用自动完成功能     
适用于 form，以及下面的 input 类型：text, search, url, telephone, email, password, datepickers, range 以及 color。     
      
placeholder="默认内容" 属性提供可描述输入字段预期值的提示信息   
适用于以下的 <input\> 类型：text, search, url, telephone, email 以及 password。     
      
tabindex规定tab键控制次序 几乎所有浏览器均支持 tabindex 属性，除了 Safari。   
    
readonly="flase" 在input中加上这句，就可以变成只读，能保留现有value，并且不能往里输入。    
    
[jade](http://www.nooong.com/docs/jade_chinese.htm):高性能的模板引擎        
    
a里放span，然后span里再放a。就会出问题。可用控制台看。   
   
html里边如果想直接打空格叫网页显示空格。那么：空格要输入法的全角空格才管用    
    
<fieldset\>将表单内的相关元素分组。   
<fieldset\> 标签将表单内容的一部分打包，生成一组相关表单的字段。   
<legend\> 标签为 fieldset 元素定义标题。   

```
<fieldset>
<legend>健康信息：</legend>
<form>
<label>身高：<input type="text" /></label>
<label>体重：<input type="text" /></label>
</form>
</fieldset>
```   

ie8+ <video\>有poster属性可以带有预览图。   
   
HTML插入FLASH的全兼容解决方案：   
   
一、传统的方法   
使用 object 和 embed 标签来嵌入   
这种方法是 Macromedia 一直以来的官方方法，最大限度的保证了 Flash 的功能，没有兼容性问题   

```
<object classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" codebase="http://fpdownload.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=7,0,0,0" width="550" height="400" id="Untitled-1" align="middle">
<param name="allowScriptAccess" value="sameDomain" />
<param name="movie" value="mymovie.swf" />
<param name="quality" value="high" />
<param name="bgcolor" value="#ffffff" />
<embed src="mymovie.swf" quality="high" bgcolor="#ffffff" width="550"  height="400" name="mymovie" align="middle" allowScriptAccess="sameDomain"  type="application/x-shockwave-flash" pluginspage="http://www.macromedia.com/go/getflashplayer" />
</object>
```   
   
二、用JS嵌入的方法   
   
SWFObject利用Javascript 插入flash，不会出现IE6下的“单击此处以激活控件”的提示，并且能通过W3C验证。   
参数依次是：  
@swf文件的地址；   
@用于装入swf文件的容器(如div)的id；   
@flash的宽度；   
@flash的高度；    
@正常播放该flash所需的最低版本；   
@当版本低于要求时，执行该swf文件；   

```
<div id="swfid"></div>
<script type="text/javascript" src="swfobject.js"></script>
<script type="text/javascript">
swfobject.embedSWF("test.swf", "swfid", "300", "120", "9.0.0", "expressInstall.swf");
</script>
```   

## PS知识点    

在移动工具 v下，按住Ctrl 查看各个图层之间间距    
ctrl + shift + Alt+ N 新建图层   
shift+ctrl+] 把图层放到最上边   
Ctrl + E 选中多图层合并
Ctrl + Alt + Shift + E 盖印图层（盖印可见图层，即将下面所有图层合并，但各自原图层仍保留）   
Ctrl + Shift + Alt + s 存储为web所用格式     
Ctrl + 鼠标左键 选中图层        
在右侧图层区域(F7)按 Ctrl + 鼠标左键 点击图层，可在信息面板(F8)看图层宽高     
Ctrl + Alt + 鼠标滑轮 整体缩放   
空格 + 鼠标 拖拽整个位置    

M 选择区域      
Ctrl + Del 填充选区   
i吸颜色，g油漆桶。    
   
切带渐变里边又带图的，比如是需要横向平铺的。取平铺的时候最好可以取离图近的一条repeat-x 然后切图的时候，可以稍微切大点高度，这样效果好。    
 