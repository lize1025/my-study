# 移动端知识点   

Web APP：                              

移动端常用技术：    
css3图片帧动画，[拍照](https://www.cnblogs.com/apanly/p/5731086.html)，[地理定位](https://www.cnblogs.com/moyuling/p/8965192.html)，手势识别，音频支持，[重力感应](https://blog.csdn.net/tangxiujiang/article/details/78080090)，canvas图形，多屏互动，vr虚拟实现技术3d全景绑定陀螺仪。    
            
[移动端自适应适配](#1)                 
[移动端动画优化](#2)	   
[移动端常见bug](#3)            

<span id="1">移动端自适应适配</span>     

[移动前端自适应适配方法总结](http://caibaojian.com/mobile-responsive.html)               

所谓前端适配，就是为了让移动设计稿在大部分的移动设备上看起来有一致的展示效果，目前比较流行的方法:          
一种是强制meta viewport宽度为设计稿宽度。
*在某些浏览器的webview里面会出现兼容问题，而且对于1像素会无法渲染。[再谈Retina下1px的解决方案](https://www.w3cplus.com/css/fix-1px-for-retina.html)*      

一种是使用rem自适应布局的淘宝[flexible.js](https://www.jianshu.com/p/04efb4a1d2f8)。     
*在背景和字体上也会有某些问题。*         

一种是[使用vw来实现移动端的适配布局](https://www.w3cplus.com/css/vw-for-layout.html)            
*[在Vue项目中使用vw实现移动端适配](https://www.w3cplus.com/mobile/vw-layout-in-vue.html)*               
               
强制meta viewport的宽度为设计稿的宽度：           

```
// 根据设计稿的宽度来传参 比如640 750 1125
!function(designWidth){
	if (/Android(?:\s+|\/)(\d+\.\d+)?/.test(navigator.userAgent)) {
		var version = parseFloat(RegExp.$1);
		if (version > 2.3) {
			var phoneScale = parseInt(window.screen.width) / designWidth;
			document.write('<meta name="viewport" content="width=' + designWidth + ',minimum-scale=' + phoneScale + ',maximum-scale=' + phoneScale + ', target-densitydpi=device-dpi">');
		} else {
			document.write('<meta name="viewport" content="width=' + designWidth + ',target-densitydpi=device-dpi">');
		}
	} else {
		document.write('<meta name="viewport" content="width=' + designWidth + ',user-scalable=no,target-densitydpi=device-dpi,minimal-ui,viewport-fit=cover">');
	}
}(640);
```

```
<!doctype HTML>
<html>
<head>
<meta http-equiv="content-type" content="text/html; charset=utf-8"/>
<meta content="telephone=no" name="format-detection" />
<title>model</title>
<script type="text/javascript">
// 根据设计稿的宽度来传参 比如640 750 1125
!function(e){if(/Android(?:\s+|\/)(\d+\.\d+)?/.test(navigator.userAgent)){var t=parseFloat(RegExp.$1);if(t>2.3){var i=parseInt(window.screen.width)/e;document.write('<meta name="viewport" content="width='+e+",minimum-scale="+i+",maximum-scale="+i+', target-densitydpi=device-dpi">')}else{document.write('<meta name="viewport" content="width='+e+',target-densitydpi=device-dpi">')}}else{document.write('<meta name="viewport" content="width='+e+',user-scalable=no,target-densitydpi=device-dpi,minimal-ui,viewport-fit=cover">')}}(640);
</script>
<style>
body,dl,dd,ul,ol,h1,h2,h3,h4,h5,h6,pre,form,input,textarea,p,hr,thead,tbody,tfoot,th,td{margin:0;padding:0;}
ul,ol{list-style:none;}
a{text-decoration:none;}
html{-ms-text-size-adjust:none;-webkit-text-size-adjust:none;text-size-adjust:none;font-size:32px;}
body{font-size:32px;line-height:1.5;}
body,button,input,select,textarea{font-family:'helvetica neue',tahoma,'hiragino sans gb',stheiti,'wenquanyi micro hei',5FAE8F6F96C59ED1,5B8B4F53,sans-serif;}
b,strong{font-weight:bold;}
i,em{font-style:normal;}
table{border-collapse:collapse;border-spacing:0;}
table th,table td{border:1px solid #ddd;padding:5px;}
table th{font-weight:inherit;border-bottom-width:2px;border-bottom-color:#ccc;}
img{border:0 none;width:auto9;max-width:100%;vertical-align:top;}
button,input,select,textarea{font-family:inherit;font-size:100%;margin:0;vertical-align:baseline;}
button,html input[type="button"],input[type="reset"],input[type="submit"]{-webkit-appearance:button;cursor:pointer;}
button[disabled],input[disabled]{cursor:default;}
input[type="checkbox"],input[type="radio"]{box-sizing:border-box;padding:0;}
input[type="search"]{-webkit-appearance:textfield;-moz-box-sizing:content-box;-webkit-box-sizing:content-box;box-sizing:content-box;}
input[type="search"]::-webkit-search-decoration{-webkit-appearance:none;}
@media screen and (-webkit-min-device-pixel-ratio:0){
input{line-height:normal!important;}
}
select[size],select[multiple],select[size][multiple]{border:1px solid #AAA;padding:0;}
article,aside,details,figcaption,figure,footer,header,hgroup,main,nav,section,summary{display:block;}
audio,canvas,video,progress{display:inline-block;}
</style>
</head>
<body>
	<!-- 页面结构写在这里 -->
	<!-- 页面结构写在这里 -->
	<!-- 页面结构写在这里 -->
	<!-- 页面结构写在这里 -->
</body>
</html>
```

rem精简版flexible.js:           

```
(function(designWidth, maxWidth) {
	var doc = document,
		win = window;
	var docEl = doc.documentElement;
	var metaEl,
		metaElCon;
	var styleText,
		remStyle = document.createElement("style");
	var tid;

	function refreshRem() {
		// var width = parseInt(window.screen.width); // uc有bug
		var width = docEl.getBoundingClientRect().width;
		if (!maxWidth) {
			maxWidth = 540;
		};
		if (width > maxWidth) { // 淘宝做法：限制在540的屏幕下，这样100%就跟10rem不一样了
			width = maxWidth;
		}
		var rem = width * 100 / designWidth;
		// var rem = width / 10; // 如果要兼容vw的话分成10份 淘宝做法
		//docEl.style.fontSize = rem + "px"; //旧的做法，在uc浏览器下面会有切换横竖屏时定义了font-size的标签不起作用的bug
		remStyle.innerHTML = 'html{font-size:' + rem + 'px;}';
	}

	// 设置 viewport ，有的话修改 没有的话设置
	metaEl = doc.querySelector('meta[name="viewport"]');
	// 20171219修改：增加 viewport-fit=cover ，用于适配iphoneX
	metaElCon = "width=device-width,initial-scale=1,maximum-scale=1.0,user-scalable=no,viewport-fit=cover";
	if(metaEl) {
		metaEl.setAttribute("content", metaElCon);
	}else{
		metaEl = doc.createElement("meta");
		metaEl.setAttribute("name", "viewport");
		metaEl.setAttribute("content", metaElCon);
		if (docEl.firstElementChild) {
			docEl.firstElementChild.appendChild(metaEl);
		}else{
			var wrap = doc.createElement("div");
			wrap.appendChild(metaEl);
			doc.write(wrap.innerHTML);
			wrap = null;
		}
	}

	//要等 wiewport 设置好后才能执行 refreshRem，不然 refreshRem 会执行2次；
	refreshRem();

	if (docEl.firstElementChild) {
		docEl.firstElementChild.appendChild(remStyle);
	} else {
		var wrap = doc.createElement("div");
		wrap.appendChild(remStyle);
		doc.write(wrap.innerHTML);
		wrap = null;
	}

	win.addEventListener("resize", function() {
		clearTimeout(tid); //防止执行两次
		tid = setTimeout(refreshRem, 300);
	}, false);

	win.addEventListener("pageshow", function(e) {
		if (e.persisted) { // 浏览器后退的时候重新计算
			clearTimeout(tid);
			tid = setTimeout(refreshRem, 300);
		}
	}, false);

	if (doc.readyState === "complete") {
		doc.body.style.fontSize = "16px";
	} else {
		doc.addEventListener("DOMContentLoaded", function(e) {
			doc.body.style.fontSize = "16px";
		}, false);
	}
})(750, 750);
```       

demo:              

```
<!doctype HTML>
<html>
<head>
<meta http-equiv="content-type" content="text/html; charset=utf-8"/>
<meta content="telephone=no" name="format-detection" />
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1.0,user-scalable=no,viewport-fit=cover"/>
<title>lib.flexible 简化版</title>
<script type="text/javascript">
(function(e,t){var i=document,n=window;var l=i.documentElement;var r,a;var d,o=document.createElement("style");var s;function m(){var i=l.getBoundingClientRect().width;if(!t){t=540}if(i>t){i=t}var n=i*100/e;o.innerHTML="html{font-size:"+n+"px;}"}r=i.querySelector('meta[name="viewport"]');a="width=device-width,initial-scale=1,maximum-scale=1.0,user-scalable=no,viewport-fit=cover";if(r){r.setAttribute("content",a)}else{r=i.createElement("meta");r.setAttribute("name","viewport");r.setAttribute("content",a);if(l.firstElementChild){l.firstElementChild.appendChild(r)}else{var c=i.createElement("div");c.appendChild(r);i.write(c.innerHTML);c=null}}m();if(l.firstElementChild){l.firstElementChild.appendChild(o)}else{var c=i.createElement("div");c.appendChild(o);i.write(c.innerHTML);c=null}n.addEventListener("resize",function(){clearTimeout(s);s=setTimeout(m,300)},false);n.addEventListener("pageshow",function(e){if(e.persisted){clearTimeout(s);s=setTimeout(m,300)}},false);if(i.readyState==="complete"){i.body.style.fontSize="16px"}else{i.addEventListener("DOMContentLoaded",function(e){i.body.style.fontSize="16px"},false)}})(750,750);
</script>
<style>
/*
需要注意的是：
样式的reset中需先设置html字体的初始化大小为50px，这是为了防止js被禁用或者加载不到或者执行错误而做的兼容
样式的reset中需先设置body字体的初始化大小为16px，这是为了让body内的字体大小不继承父级html元素的50px，而用系统默认的16px
*/
body,dl,dd,ul,ol,h1,h2,h3,h4,h5,h6,pre,form,input,textarea,p,hr,thead,tbody,tfoot,th,td{margin:0;padding:0;}
ul,ol{list-style:none;}
a{text-decoration:none;}
html{-ms-text-size-adjust:none;-webkit-text-size-adjust:none;text-size-adjust:none;font-size:50px;}
body{line-height:1.5;font-size:16px;}
body,button,input,select,textarea{font-family:'helvetica neue',tahoma,'hiragino sans gb',stheiti,'wenquanyi micro hei',\5FAE\8F6F\96C5\9ED1,\5B8B\4F53,sans-serif;}
b,strong{font-weight:bold;}
i,em{font-style:normal;}
table{border-collapse:collapse;border-spacing:0;}
table th,table td{border:1px solid #ddd;padding:5px;}
table th{font-weight:inherit;border-bottom-width:2px;border-bottom-color:#ccc;}
img{border:0 none;width:auto\9;max-width:100%;vertical-align:top;}
button,input,select,textarea{font-family:inherit;font-size:100%;margin:0;vertical-align:baseline;}
button,html input[type="button"],input[type="reset"],input[type="submit"]{-webkit-appearance:button;cursor:pointer;}
button[disabled],input[disabled]{cursor:default;}
input[type="checkbox"],input[type="radio"]{box-sizing:border-box;padding:0;}
input[type="search"]{-webkit-appearance:textfield;-moz-box-sizing:content-box;-webkit-box-sizing:content-box;box-sizing:content-box;}
input[type="search"]::-webkit-search-decoration{-webkit-appearance:none;}
@media screen and (-webkit-min-device-pixel-ratio:0){
input{line-height:normal!important;}
}
select[size],select[multiple],select[size][multiple]{border:1px solid #AAA;padding:0;}
article,aside,details,figcaption,figure,footer,header,hgroup,main,nav,section,summary{display:block;}
audio,canvas,video,progress{display:inline-block;}


.g-doc{width:6.4rem;margin:0px auto;}

</style>
</head>
<body>
    <div class="g-doc">
        <!-- 页面结构写在这里 -->
        <!-- 页面结构写在这里 -->
        <!-- 页面结构写在这里 -->
        <!-- 页面结构写在这里 -->
    </div>
</body>
</html>
```

<span id="2">移动端动画优化：</span>     
   
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

[requestAnimationFrame](https://www.cnblogs.com/xiaohuochai/p/5777186.html)制作简单进度条：          

```
<div id="myDiv" style="background-color: lightblue;width: 0;height: 20px;line-height: 20px;">0%</div>
<button id="btn">run</button>
<script>
var timer;
btn.onclick = function(){
    myDiv.style.width = '0';
    cancelAnimationFrame(timer);
    timer = requestAnimationFrame(function fn(){
        if(parseInt(myDiv.style.width) < 500){
            myDiv.style.width = parseInt(myDiv.style.width) + 5 + 'px';
            myDiv.innerHTML =     parseInt(myDiv.style.width)/5 + '%';
            timer = requestAnimationFrame(fn);
        }else{
            cancelAnimationFrame(timer);
        }    
    });
}
</script>
```
      
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

<span id="3">移动端常见bug：</span>
            
仿app头部底部固定设置position:fixed; android2.2以上实现。ios下，当小键盘激活时（比如有点击input），回传位置浮动问题   
解决：中间部分外层加上            

`position:absolute;top:30px;bottom:38px;overflow:scroll;`      
     
页面高度渲染错误：         
在各移动端浏览器中经常会出现页面高度100%的渲染错误，页面低端和系统自带的导航条重合了，高度的不正确我们需要重置修正它，重置掉：     

`document.documentElement.style.height = window.innerHeight + 'px'`       
        
叠加区高亮：     
点击某区域出现黄色秒闪，部分机型系统默认样式，给该元素：         

`-webkit-tap-highlight-color:rgba(0,0,0,0)`       
       
屏蔽点击元素时出现的阴影：
transparent的属性值在android下无效       

`-webkit-tap-highlight-color:rgba(255,255,255,0)`      
      
同时屏蔽输入框怪异的内阴影:           

`-webkit-appearance:none;`              
    
事件无法触发：       
部分android机微信里事件不触发，表单无法输入。解决：             

`-webkit-transform-translate3d(0,0,0)`        
      
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

Hybrid APP：                  

一切使用web技术开发原生移动应用的场景都可以视为混合式开发          

原先混合开发在理念上保持使用html，css，js的体系结构在WebView中执行的概念，但现阶段，web前端技术开始深入地融入原生应用的开发体系。              

混合式开发种类：        

WebView模式：        
代表是PhoneGap和Cordova，App原生部分仅仅作为一个容器，主要业务代码通过html，css，js放置在WebView中执行。           
*对于web前端开发人员，[Cordova](https://cordova.apache.org/)开发主要需要关注插件API的使用和相关事件的监听[Cordova入门](https://blog.csdn.net/csdn100861/article/details/78585333)*              

javaScriptCore模式：              
通过js调用原生代码渲染原生控件的混合式开发。               
javaScriptCore框架原来只提供在WebView的webkit内核中，在ios7中开放了这一功能，之后在Android中也提供了类似功能，从而催生出了React Native这        
样使用js作为bridge操作原生代码来构建应用的方案。构建出的整个应用可以被理解为原生应用。            

微信小程序：       
本质仍使用WebView方案，但独立设计了一套语法对应传统的html，css，js。限制了一些可能导致问题的语法。               
依赖应用的内部设计，并非一个通用的解决方案。           

Flutter：         
除了以上方案，谷歌推出了Flutter混合跨平台开发方案，通过Dart语言直接控制完成实现了整个UI层。              

混合式开发的优势：       
跨平台       
快速发布       
功能提升            


