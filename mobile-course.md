# 移动端知识点   

移动端常用技术：    
[css3图片帧动画](#3)，[拍照](https://www.cnblogs.com/apanly/p/5731086.html)，[地理定位](https://www.cnblogs.com/moyuling/p/8965192.html)，手势识别，音频支持，[重力感应](https://blog.csdn.net/tangxiujiang/article/details/78080090)，canvas图形，多屏互动，vr虚拟实现技术3d全景绑定陀螺仪。    
       
[移动端动画优化](#1)	   
[移动端常见bug](#2)
	   
css3边框：   
border-radius   
每个半径的四个值的顺序是：左上角，右上角，右下角，左下角       
   
border-shadow    
可以设置一个或多个下拉阴影的框。     
   
border-image   
可以使用图片来创建边框       
   
css3背景：       
background-size    
规定背景图片的尺寸,调整大小，进行拉伸。             

background-origin    
规定背景图片的定位区域。背景图片可以放置于 content-box、padding-box 或 border-box 区域         

为元素使用多个背景图像   
`background-image:url(bg_flower.gif),url(bg_flower_2.gif);`   
   
css3文本效果：    
text-shadow   
向文本应用阴影。能够规定水平阴影、垂直阴影、模糊距离，以及阴影的颜色        

word-wrap    
允许您允许文本强制文本进行换行        

text-overflow    
规定当文本溢出包含元素时发生的事情。       
clip：修剪文本       
ellipsis：显示省略符号来代表被修剪的文本。        

css3字体：   
@font-face 规则   

```
@font-face
{
font-family: myFirstFont;
src: url('Sansation_Light.ttf'),
     url('Sansation_Light.eot'); /* IE9+ */
}

div
{
font-family:myFirstFont;
}
```    

css3 2D转换 transform：    
translate()    
元素从其当前位置移动，根据给定的 left（x 坐标） 和 top（y 坐标）        
*translate(50px,100px) 把元素从左侧移动 50 像素，从顶端移动 100 像素。*      

rotate()   
元素顺时针旋转给定的角度。允许负值，元素将逆时针旋转。     
*rotate(30deg) 把元素顺时针旋转 30 度*    

scale()   
元素的尺寸会增加或减少，根据给定的宽度（X 轴）和高度（Y 轴）参数   
只支持数值，可以是负值。居中缩放。缩放占据原始尺寸不变。        
*scale(2,4) 把宽度转换为原始尺寸的 2 倍，把高度转换为原始高度的 4 倍*       
   
skew()     
元素翻转给定的角度，根据给定的水平线（X 轴）和垂直线（Y 轴）    
*skew(30deg,20deg) 围绕 X 轴把元素翻转 30 度，围绕 Y 轴翻转 20 度*     

css3 3D转换 transform：    
rotateX() 方法，元素围绕其 X 轴以给定的度数进行旋转    
`transform: rotateX(120deg);`   

rotateY() 方法，元素围绕其 Y 轴以给定的度数进行旋转    
`transform: rotateY(130deg);`    

css3过渡 transition:   
CSS3 过渡是元素从一种样式逐渐改变为另一种的效果:    
要实现这一点，必须规定两项内容：    
规定您希望把效果添加到哪个 CSS 属性上    
规定效果的时长    

效果开始于指定的 CSS 属性改变值时。如果时长未规定，则不会有过渡效果，因为默认值是 0。    
`transition: width 2s;`   

向多个样式添加过渡效果，添加多个属性，由逗号隔开:    

```
div
{
width:100px;
height:100px;
background:yellow;
transition:width 2s, height 2s;
-moz-transition:width 2s, height 2s, -moz-transform 2s; /* Firefox 4 */
-webkit-transition:width 2s, height 2s, -webkit-transform 2s; /* Safari and Chrome */
-o-transition:width 2s, height 2s, -o-transform 2s; /* Opera */
}

div:hover
{
width:200px;
height:200px;
transform:rotate(180deg);
-moz-transform:rotate(180deg); /* Firefox 4 */
-webkit-transform:rotate(180deg); /* Safari and Chrome */
-o-transform:rotate(180deg); /* Opera */
}
```    
   
transition:简写属性，用于在一个属性中设置四个过渡属性。     
transition-property:规定应用过渡的 CSS 属性的名称。可以是all        
transition-duration:定义过渡效果花费的时间。    
transition-timing-function:规定过渡效果的时间曲线。默认是 "ease"。
transition-delay:规定过渡效果何时开始。默认是 0。    
      
transition-timing-function:    
linear:规定以相同速度开始至结束的过渡效果    
ease:规定慢速开始，然后变快，然后慢速结束的过渡效果    
ease-in:规定以慢速开始的过渡效果    
ease-out:规定以慢速结束的过渡效果    
ease-in-out:规定以慢速开始和结束的过渡效果     

<span id="3">css3动画：</span>    

CSS3 @keyframes 规则:    
@keyframes 规则用于创建动画。在 @keyframes 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果。    

在@keyframes中创建动画时，把它捆绑到某个选择器，否则不会产生动画效果。    
通过规定至少以下两项 CSS3 动画属性，即可将动画绑定到选择器：     
规定动画的名称   
规定动画的时长   

```
div
{
width:100px;
height:100px;
background:red;
animation:myfirst 5s;
-moz-animation:myfirst 5s; /* Firefox */
-webkit-animation:myfirst 5s; /* Safari and Chrome */
-o-animation:myfirst 5s; /* Opera */
}

@keyframes myfirst
{
from {background:red;}
to {background:yellow;}
}

@-moz-keyframes myfirst /* Firefox */
{
from {background:red;}
to {background:yellow;}
}

@-webkit-keyframes myfirst /* Safari and Chrome */
{
from {background:red;}
to {background:yellow;}
}

@-o-keyframes myfirst /* Opera */
{
from {background:red;}
to {background:yellow;}
}
```   

animation所有动画属性的简写属性，除了 animation-play-state 属性。   
animation-name	规定 @keyframes 动画的名称。    
animation-duration	规定动画完成一个周期所花费的秒或毫秒。默认是 0。    
animation-timing-function	规定动画的速度曲线。默认是 "ease"。     
animation-delay	规定动画何时开始。默认是 0。     
animation-iteration-count	规定动画被播放的次数。默认是 1。     
animation-direction	规定动画是否在下一周期逆向地播放。默认是 "normal"。	     
animation-play-state	规定动画是否正在运行或暂停。默认是 "running"。     
animation-fill-mode	规定对象动画时间之外的状态。      

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
 
CSS3 多列属性:   
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


<span id="1">移动端动画优化：</span>     
   
尽量用css3       
不占用js主线程  
可利用硬件加速    
浏览器可对动画做优化   
不支持中间状态监听    
    
适当使用canvas绘图：    
可避免渲染树的计算，渲染更快   
开发成本高    
维护较麻烦   
    
合理使用RAF解决脚本引起的丢帧，支持中间状态监听，android4.3以下不兼容    
requestAnimationFrame好处是js可以和css3动画同步发生，动画更流畅。       
在浏览器标签页运行动画，如果标签页不可见，浏览器会暂停动画。减少cpu，内存压力，节省电池电量。      
      
GPU加速实际上是大幅减少了合成绘制时间，提高页面速度。        
缺点：过多使用GPU层会带来性能开销。主要原因GPU加速利用了GPU层的缓存，一旦多了，就会引起别的性能问题。       

有可能影响性能动画以及替代：   
位移动画：   
top left right bottom    
translate3d(x,y,z)    
边框动画：   
border 1-1000   
scale(0.1)-scale(1)   
放大缩小动画   
zoom 1-10   
scale(0.9)-scale(1)   
图片背景动画   
background-position   
translate(x,y)   
即时显示动画  
visibility:hidden visible   
keyframes name{0%{opacity:0} 100%{opacity:1}}   
飞入飞出动画   
translateZ(0px)-translateZ(50px)   
scale(1)-scale(1.1)   
    
改变border的动画在低端机上会产生性能问题，看情况用其他方式代替。     
      
背后的动画可能会影响到当前动画的播放，在android4.0系统，会产生渲染异常问题      
因此应把不在当前页的动画停掉，背后动画设display:none;或animation-play-state:pause;        

<span id="2">移动端常见bug：</span>
            
仿app头部底部固定设置position:fixed; android2.2以上实现。ios下，当小键盘激活时（比如有点击input），回传位置浮动问题   
解决：中间部分外层加上`position:absolute;top:30px;bottom:38px;overflow:scroll;`    
   
页面高度渲染错误：         
在各移动端浏览器中经常会出现页面高度100%的渲染错误，页面低端和系统自带的导航条重合了，高度的不正确我们需要重置修正它，重置掉：     
`document.documentElement.style.height = window.innerHeight + 'px'`       
        
叠加区高亮：     
点击某区域出现黄色秒闪，部分机型系统默认样式，给该元素：        
`-webkit-tap-highlight-color:rgba(0,0,0,0)`       
       
屏蔽点击元素时出现的阴影：`-webkit-tap-highlight-color:rgba(255,255,255,0)`      
transparent的属性值在android下无效       
      
`-webkit-appearance:none;`可以同时屏蔽输入框怪异的内阴影。       
    
事件无法触发：       
部分android机微信里事件不触发，表单无法输入。         
解决：`-webkit-transform-translate3d(0,0,0)`        
      
:active效果不兼容:     
android4以下，active效果不兼容，给touch绑个空方法即可      

```
var tar = docuemnt.getElementById('tar');
tar.addEventListener('touchstart',function(){},false);
```   
   
解绑函数写在事件处理中，导致小米手机微信崩溃：   

```
var act = function(){
	window.removeEventlistener('devicemotion',act);
}
window.addEventListener('devicemotion',act,false);
```   
       
错误出现滚动条：        
在游戏里内嵌页中出现了不应该出现的滚动条，而且内容没有超出内容区宽度:     
经过测试overflow:hidden;无效。可以用古老的方式`<body scroll="no">`解决    
     
预加载，自动播放无效：        
预加载自动播放的有效性受操作系统，浏览器webview，版本等的影响    
苹果官方规定必须由用户手动触发才会载入音频，那么我们可以捕捉一次用户操作，让音频实现预加载：     

```
document.addEventListener('touchstart',function(){
	document.getElementsByTagName('audio')[0].play()
	document.getElementsByTagName('audio')[0].pause()
})
```    

无法同时播放多音频：     
在android设备中，播放后一音频会打断前一音频，而不会同步播放:   
这个是目前系统自身决定的，我们只能采取优雅降级的方法让android选择不一样风格的音频前后切换播放而不是同时播放。    
    
怪异悬浮的表单：     
在部分android机型中的输入框可能会出现怪异的多余的浮出表单:    
经过观察与测试发现，只有input:password类型的输入框存在    
那么我们只要使用input:text类型的输入框，并通过`-webkit-text-security:dics;`隐藏输入密码从而解决。     
     
ios关闭键盘首字母大写：input元素中提供了属性`autocapitalize="off"`       
     
ios禁止设备弹出列表按钮（禁止保存图片）img标签`-webkit-touch-callout:none;`    
    
ios禁止用户选中文字-webkit-user-select:none;可能导致个别android无法输入，解决：   

```
*:not(input,textarea){
	-webkit-touch-callout:none;
	-webkit-user-select:none;
}
```    
   
点透问题：   
弹出层关闭按钮，点击后下边内容也会执行点击事件。比如下边有input，那键盘就弹出了。    
老版zepto的tap是通过监听绑定在document上的touch事件完成tap事件的,tap事件冒泡到document上触发，     
而在这之前，用户手接触屏幕并离开时候是会触发click事件的。click有延时300ms，导致弹出层关闭了才执行。如果下方有input，就出现了点透。     
解决：    
用fastclick.js     
用touchend代替tap事件，并阻止掉默认e.preventDefault()    
用延时处理，加定时器320 setTimeout()    

click300ms延时：     
2014年的chrome32版本，ie，firefox/safari ios9.3已经把延时去掉了，如果viewport设置成设备实际像素，就不会有延时：     

`<meta name="viewport" content="width=device-width">`    

或者设置css取消掉延时：    

`html{touch-action:manipulation;}`    

click最后触发：     

touchstart-touchend-mouseover-mousedown-mouseup-click     
    
鬼点击：点击一次执行两次。     
解决：在touchend处阻止默认事件`e.preventDefault()`        
     
如动画过程有闪烁，可以：    

```
backface-visibility:hidden;
perspective:1000;
```    

swiper.js设置左右滑动时，阻止了上下滑动事件的情况，可以用如下方法：    

```
-webkit-overflow-scrolling:touch;
overflow-y:scroll;
```    

touchend事件不触发，android4.04以下，按住一个dom元素滑动后放手，只触发一次touchmove而touchend不触发     
解决：在touchstart的时候调用`e.preventDefault()`       
    
`.game{position:absolute;top:0;bottom:0;left:0;right:0;overflow:hidden;}`    
以上代码决定定位后，叫上下左右都与手机屏幕紧贴，做到适配各个屏幕，在用background-size:cover;让背景图覆盖全屏。    
然后内部元素根据其所接近的边缘做动态布局    
`.ranbox{position:absolute;bottom:110px;left:0;width:100%;overflow:hidden;padding-bottom:10px;}`     
bottom基于底边定位，100宽，保证从屏幕边缘出现。    
    
iphone5,5s在safari上，当前页后边有全屏视频，即使不显示，位置也不在视窗内，页面上任何触屏事件也都捕获不到，全被看不见的video抢去了。    
解决：video隐藏时设宽高都为1px。等播放时候在设回去。     
    
播放视频1之后，无用户操作无法继续播视频2（另个video标签）   
当用户有触发行为，初始化两个视频，视频1添加end事件，但是android提示解析错误或弹出框让你选打开方式。    
解决：用到timeupdate(当播放位置改变时触发)，currentTime(当前位置)，当有了currentTime>0时，就说明播放过了，然后暂停，等再次被play()    
安卓下不能同时存在两个初始化视频，没有用户主动触发行为，第二个视频play()是无效的。但在视频已经播放过的情况下，是可以play()操作的。   
如果一个video标签，可以通过动态改变src方法，改变src后的play()是可以播放的。    
    