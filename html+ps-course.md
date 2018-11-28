# html+PS知识点        

* [1. HTML](#1)
* [2. HTML5必会特性](#2)  
    * [2.1 新元素](#3)
    * [2.2 表单、音频和视频](#4)
    * [2.3 定位当前地理位置](#5)
    * [2.4 调用摄像头拍照](#6)
    * [2.5 手机摇一摇](#7)
    * [2.6 离线和存储--随手记](#8)
    * [2.7 cookie](#28)
    * [2.8 LocalStorage与SessionStorage](#9)
    * [2.9 IndexedDB实现便签管理](#10)
    * [2.10 Canvas、SVG、WebGL](#11)
    * [2.11 PostMessage](#12)
    * [2.12 XMLHttpRequest Level 2](#13)
    * [2.13 Server Sent Event](#14)
    * [2.14 WebSocket协议](#15)
    * [2.15 WebRTC实时通讯](#16)
    * [2.16 History与单页应用](#17)
    * [2.17 Drag和Drop](#18)
    * [2.18 Web Workers](#19)
    * [2.19 Performance AIP 分析网站性能](#20)
* [3. html5优化实践](#21)  
    * [3.1 使用history改善AJAX列表请求体验](#22)
    * [3.2 使用图标字体iconfont代替雪碧图](#23)  
    * [3.3 实现前端剪裁压缩图片](#24)
    * [3.4 前端本地文件操作与上传](#25)
    * [3.5 Service Worker做一个PWA离线网页应用](#26)
* [4. PS](#27)  
                                                                             
<h2 id="1">HTML</h2>          

html:[w3c验证](http://validator.w3.org/)    

a标签target="_blank"开新标签，其实也可以不是_blank。可以随便写  
   
<base\> 标签的href属性：    
为页面中所有的元素的href属性设置了基础值（对元素href为绝对路径的元素不起作用）    
当这些元素进行跳转时，都会基于当前目录加上这个默认的URL（相对路径的情况下）再加上自己的href属性值来跳转。    
     
<base\>标签的target="_blank"可以控制全部a标签打开新页面，href可以给所有a标签的href加前缀，控制台下看a是看不到加上了的。   
   
form里`action="http://baidu.com/s"`然后input里name="wd"，这样submit提交的结果就从百度里找   
   
表单radio的name要相同，id不同。所有表单标签，需要提交数据的，都要加name    
   
label里for，关联到input里的id即可一同选中。       
      
tabindex规定tab键控制次序 几乎所有浏览器均支持 tabindex 属性。      
    
readonly="readonly"，能保留现有value，但不能往里输入。值可以通过form传递出去。           
Readonly只针对input(text / password)和textarea                  
    
[jade](https://segmentfault.com/a/1190000000357534):源于Node.js的HTML 模板引擎       
    
a里放span，然后span里再放a。就会出问题。可用控制台看。   
   
html里边如果想直接打空格叫网页显示空格。那么：空格要输入法的全角空格才管用    
    
<fieldset\>将表单内的相关元素分组。将表单内容的一部分打包，生成一组相关表单的字段。      
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

```
<video width="320" height="240" poster="/i/w3school_logo_black.gif" controls>
   <source src="/i/movie.mp4" type="video/mp4">
   <source src="/i/movie.ogg" type="video/ogg">
   Your browser does not support the video tag.
</video>
```
   
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
        
<h2 id="2">HTML5必会特性</h2>     

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
布尔值不写就是true。如:      

`<input type="checkbox" name="" id="" checked>`          

<h3 id="3">新元素</h3>      

布局采用div：      

```
<!--页头-->
<div class="header"></div>

<!--导航-->
<div class="nav"></div>

<!--主体内容-->
<div class="main">
    <!--文章-->
    <div class="artical">
        <!--节-->
        <div class="section"></div>
    </div>
    <!--边栏-->
    <div class="sidebar"></div>
</div>

<!--页脚-->
<div class="footer"></div>
```
    
html5新元素实现上述布局：      

```
<header>介绍内容的容器或者一组导航链接</header>
<nav>标签的内容主要用于导航</nav>
<div>
    <article> <--页面中的主体内容-->
        <section>标记页面重要部分。</section>
    </article>
    <aside>和主要内容相关，但不是页面的一部分</aside>
</div>
<footer>文档章节页脚</footer>
```    

<h3 id="4">表单、音频和视频</h3>      

input元素的type属性扩充：     

search:呈现一个搜索框    

tel：输入电话号码，可用pattern和maxlength限定输入格式：        

`<input type="tel" name="tel" value="" placeholder="请输入手机号码" pattern="1[3-8][0-9]{9}" title="请输入11位手机号">`        

url:输入URL地址    

email：输入邮件地址    

date：输入日期      

`<input type="date">`     

color:输入颜色        

`<input type="color">`      

number:输入数字      

`<input type="number" name="points" min="1" max="10" />`            

range：滑块输入      

`<input type=range min=20 max=100 step=2>`         

input元素属性：     

placeholder="默认内容" 属性提供可描述输入字段预期值的提示信息       
适用于以下的 <input\> 类型：text, search, url, telephone, email 以及 password。      

input中autocomplete 属性           
autocomplete="off" 规定输入字段不启用自动完成功能     
适用于 form，以及下面的 input 类型：text, search, url, telephone, email, password, datepickers, range 以及 color。  

required:input元素为必填        

`<input type="text" placeholder="此项必填" required>`    

autofocus:页面加载时，自动聚焦。            

`<input type="text" name="fname" autofocus />`        

form:将input元素和特定的form表单关联     

```
<form action="/example/html5/demo_form.asp" method="get" id="form1"></form>

<--位于 form 元素之外，但仍然是表单的一部分。-->
<input type="text" name="lname" form="form1" />
```

datalist标签定义选项列表:      

```
<input id="myCar" list="cars" />
<datalist id="cars">
  <option value="BMW">
  <option value="Ford">
  <option value="Volvo">
</datalist>
```   

progress元素表示进度条：      

`<progress value="30" max="100"></progress>`    

meter元素表示标尺：     

`<meter value="3" min="0" max="10">3/10</meter>`     

contenteditable属性：让普通元素可编辑        

`<p contenteditable="true">这里的内容是可以编辑的</p>`     

使用音频：    

controls:是否显示标准音频控件     
autoplay:是否自动播放，默认false     
loop:是否循环，默认false    
preload:预先加载方式。默认auto预加载整个音频。none不预加载。metadata只加载音频元数据。     
volum:音量，0-1之间。     

```
<audio controls>
    <source src="vincent.ogg" />
    <source src="vincent.mp3" /> 你的浏览器不支持Audio标记
</audio>

<section>
    <h3>自定义播放行为</h3>
    <audio id="audio">
        <source src="vincent.ogg" />
        <source src="vincent.mp3" /> 你的浏览器不支持Audio标记
    </audio>
    <p>
        <button id="btnPlay">Play</button>
        <button id="btnPause">Pause</button>
    </p>

<script>
    var audio = document.getElementById("audio")
    document.getElementById("btnPlay").addEventListener("click", function(){
        audio.play()
    })
    document.getElementById("btnPause").addEventListener("click", function(){
        audio.pause()
    })
</script>
</section>
```

使用视频：      

```
<video width="400" height="300" controls id="video">
<source src="dizzy.mp4#t=,15" type="video/mp4">
<source src="dizzy.webm" type="video/webm">
<source src="dizzy.ogv" type="video/ogg">
<p>你的浏览器不支持HTML5视频</p>
</video>

<p>
<input type="number" name="time" value="10" id="time">
<button id="btnSeek">GetInfo</button>
</p>

<script>
    var video = document.getElementById("video")
    var time = document.getElementById("time")
    document.getElementById("btnSeek").addEventListener("click", function () {
        //通过指定currentTime控制播放的位置,也可在source的url上指定起始和结束时间
        //<source src="dizzy.mp4#t=5,10" type="video/mp4">
        video.currentTime = time.value;
    })

    var sources =  video.querySelectorAll("source")
    var lastSource = sources[sources.length - 1]
    lastSource.addEventListener("error", function(){
        alert('No source available')
    })
</script>
```

<h3 id="5">定位当前地理位置</h3>          
   
根据用户的地理位置提供相关服务。     
Geolocation API通过navigator.geolocation全局对象进行访问。初次访问浏览器会询问用户是否允许共享位置。         

```
function showPosition(position) {
    var latlon = position.coords.latitude + ',' + position.coords.longitude;
    var img_url = 'http://maps.googleapis.com/maps/api/staticmap?center='
    + latlon + '&zoom=14&size=400x300&sensor=false';
    document.getElementById('pos').innerHTML = latlon;
    document.getElementById('map').innerHTML = '<img src="' + img_url + '" />';
}

function success(position){
    console.log('获取位置成功：', position.coords);
    showPosition(position);
}

function error(positionError){
    console.log('获取位置失败：', positionError);
}

var options = {
    enableHighAccuracy: false, //是否获取高精度的位置信息
    timeout: 30000, //定位超时时间，单位毫秒。
    maximumAge: 0 //用户位置信息缓存的最大时间。
}

if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(success, error, options);
} else {
    alert('您的浏览器不支持Geolocatioin!')
}

// var watchId = navigator.geolocation.watchPosition(success, error, options);  //用户位置变化，通过watchPosition方法监听
// navigator.geolocation.clearWatch(watchId)  //取消监听
```

<h3 id="6">调用摄像头拍照</h3>          

GetUserMedia API提供访问用户媒体设备能力。      
起初版本：navigator.getUserMedia 最新标准：navigator.mediaDevices.getUserMedia     

请求访问用户摄像头，并把视频流通过video元素显示出来。提供一个拍照按钮，通过canvas将video的画面截取并绘制：     

```
<video id="video" autoplay style="width:480px;height:320px"></video><!-- 显示MediaStream视频流 -->
<div><button id="capture">拍照</button></div>
<canvas id="canvas" width="480" height="320"></canvas>

// 访问用户媒体设备的兼容方法
function getUserMedia(constraints, success, error) {
    if (navigator.mediaDevices.getUserMedia) {
    // 最新的标准API
    navigator.mediaDevices.getUserMedia(constraints)
    .then(success).catch(error);
    } else if (navigator.webkitGetUserMedia) {
    // Webkit核心浏览器
    navigator.webkitGetUserMedia(constraints, success, error);
    } else 
    if (navigator.mozGetUserMedia) {
    // Firefox浏览器
    navigator.mozGetUserMedia(constraints, success, error);
    } else if (navigator.getUserMedia) {
    // 旧版API
    navigator.getUserMedia(constraints, success, error);
    }
}

    var video = document.getElementById("video");// video元素
    var canvas = document.getElementById("canvas");// canvas元素
    var context = canvas.getContext("2d");

// 成功的回调函数
function success(stream) {
    var CompatibleURL = window.URL || window.webkitURL
    video.src = CompatibleURL.createObjectURL(stream);//将视频流设置为video元素的源
    video.play();// 播放视频
}

// 异常的回调函数
function error(error) {
        console.log('访问用户媒体设备失败：', error.name, error.message);
    }

if (navigator.mediaDevices.getUserMedia || navigator.getUserMedia ||
    navigator.webkitGetUserMedia || navigator.mozGetUserMedia) {
    // 调用用户媒体设备，访问摄像头
    getUserMedia({ video: { width: 480, height: 320 } }, success, error);
    //移动设备上可指定使用前置摄像头video: { facingMode:'user'}
} else {
    alert('您的浏览器不支持访问用户媒体设备！');
}

// 绑定拍照按钮的点击事件
    document.getElementById("capture").addEventListener("click", function () {
        //在画布上定位图像，并规定图像的宽度和高度：context.drawImage(img,x,y,width,height);
        context.drawImage(video, 0, 0, 480, 320);// 将video画面在canvas上绘制出来
    });
```

<h3 id="7">手机摇一摇</h3>          

手机在一定时间内移动了一定距离。    
监听devicemotion事件后，判断设备x，y，z三个方向上移动的距离与前一次移动的距离差，并除以两次事件触发时间差。即为设备移动速度。      

```
<div>用力摇一摇你的手机</div>

var SHAKE_SPEED_THRESHOLD = 300;// 摇动速度阈值
var lastTime = 0;// 上次变化的时间
var x = y = z = lastX = lastY = lastZ = 0;// 位置变量初始化

function motionHandler(evt) {
    var acceleration = evt.accelerationIncludingGravity;// 取得包含重力加速的位置信息
    var curTime = Date.now();// 取得当前时间
    if ((curTime - lastTime) > 120) {// 判断
    var diffTime = curTime - lastTime;// 两次变化时间差
    lastTime = curTime;// 保存此次变化的时间
    x = acceleration.x;
    y = acceleration.y;
    z = acceleration.z;
    var speed = Math.abs(x + y + z - lastX - lastY - lastZ) / diffTime * 1000;// 计算速度
    if (speed > SHAKE_SPEED_THRESHOLD) {// 速度是否大于预设速度
        alert("你摇动了手机");
    }
    lastX = x; // 保存此次变化的位置x
    lastY = y; // 保存此次变化的位置y
    lastZ = z; // 保存此次变化的位置z
    }
}

if (window.DeviceMotionEvent) {
    //devicemotion在设备位置发生变化时触发
    window.addEventListener('devicemotion', motionHandler, false);
} else {
    alert('您的设备不支持位置感应');
}
```

<h3 id="8">离线和存储--随手记</h3>          

离线资源缓存：      
通过浏览器机制，将在线资源缓存到本地，当用户离线访问时本地资源自动加载，从而让用户可以正常使用应用。     

在线状态监测：         
有些应用需要和服务器做数据交互，开发者需要知道浏览器是否处于在线状态。提供在线状态监测。      

本地数据存储：        
应用处于离线时，程序把数据存储到本地，以便在线时同步到服务器。      

离线web比普通web应用多了一个描述文件。以备离线时使用。描述文件扩展名'.manifest'或'.appcache'。       
描述文件的mime-type类型为'text/cache-manifest'，必须使用UTF-8编码      
offline.appcache文件代码：            

```
CACHE MANIFEST
#cache之后的资源都会被缓存
CACHE:
base.css
main.js
#network之后的资源不会被缓存，总是从线上获取
NETWORK:
index.css
account/
```

在html标签上添加manifest属性后，浏览器就会自动下载offline.appcache文件并解析，然后缓存文件中那个指定的资源：      

`<html manifest="./offline.appcache">`    

入口index.html文件：     

```
<h2>随手记--实时保存</h2>
<div>
	<textarea id="content" cols="100" rows="20"></textarea>
</div>
<script src="main.js"></script>
```  

main.js文件：     

```
// 获取记录内容的文本域
var el = document.querySelector('#content');

// 为文本域DOM节点添加blur事件
el.addEventListener('blur', function(){
	// 获取文本域的内容
	var data = el.innerHTML;
	// 如果是在线状态，就直接保存到服务器
	if(navigator.onLine){
		saveOnline(data);
	}else{
		// 如果是离线状态，则保存到本地
		localStorage.setItem('data', data);
	}
});

// 监听上线事件
window.online = function(){
	// 从本地存储获取数据
	var data = localStorage.getItem('data');
	if(!!data){
		// 如果数据存在，则保存到服务器
		saveOnline(data);
		// 同时，清空本地的存储
		localStorage.removeItem('data');
	}
};

// 保存内容的具体代码
function saveOnline(data){
	var xhr = new XMLHttpRequest();
	xhr.open('POST', 'http://localhost:8000/savedata');
	xhr.send('data='+data);
}
```

离线之后资源更新--Service Worker     
Service Worker主要功能：后台消息传递 网络代理 离线缓存 消息推送     
通过手动的方式实现了两个静态资源的缓存：            

```
// main.js注册 service worker
navigator.serviceWorker.register('sw.js').then(function(registration) {
	console.log('Service Worker 注册成功');
}).catch(function (err) {
	console.log('Servcie Worker 注册失败：'+err);
});

//sw.js 需要缓存的资源列表
var cacheFiles = [
    'style.css',
    'main.js'
];

// 在install事件里缓存资源
self.addEventListener('install', function (evt) {
    evt.waitUntil(
        caches.open('mycache').then(function (cache) {
            return cache.addAll(cacheFiles);
        })
    );
});
```

<h3 id="28">cookie</h3>

数据存储：            
cookie，LocalStorage，SessionStorage，indexedDB。               
cookie大小受限，当前域所有http请求都携带数据             
LocalStorage一直存在本地            
SessionStorage存活在当前页面生命周期中            
indexedDB事务型数据库，存储大量结构化数据          

Cookie 是一些数据, 存储于你电脑上的文本文件中。           

当web服务器向浏览器发送web页面时，在连接关闭后，服务端不会记录用户的信息。     

Cookie的作用就是用于解决 "如何记录客户端的用户信息":             
当用户访问 web 页面时，他的名字可以记录在 cookie 中。            
在用户下一次访问该页面时，可以在 cookie 中读取用户访问记录。       

cookie设置第一次打开会显示：        
*需在服务器下查看*            

```
<div id="first" style="display:none;">第一次打开会显示</div>
<script>
	window.onload = function(){
		var res = document.cookie.substring(5);
		if(res!="zheng"){
			var oDate = new Date()
		    oDate.setDate(oDate.getDate() + 30)
		    document.cookie = "name=zheng;expires="+oDate
		    document.getElementById('first').style.display = 'block'
		    }
	}
```

写，读，删：        

```
//写cookies
function setCookie(name,value){
    var Days = 30; 
    var exp = new Date(); 
    exp.setTime(exp.getTime() + Days*24*60*60*1000);
    document.cookie = name + "="+ escape (value) + ";expires=" + exp.toGMTString(); 
}

//读取cookies 
function getCookie(name){
    var arr,
        reg = new RegExp("(^| )"+name+"=([^;]*)(;|$)");
 
    if(arr=document.cookie.match(reg)){
       return unescape(arr[2]);
     } 
    else{return null;} 
} 

//删除cookies 
function delCookie(name) {
    var exp = new Date(); 
    exp.setTime(exp.getTime() - 1); 
    var cval = getCookie(name); 
    if(cval! = null){ 
        document.cookie= name + "="+cval+";expires="+exp.toGMTString();
        } 
} 

//使用示例 
setCookie("name","hayden");
alert(getCookie("name"));
```

<h3 id="9">LocalStorage与SessionStorage</h3>          

将数据存储到cookie有如下弊端：     
大小受限，单个cookie允许大小是4KB     
消耗性能，当前域下所有http请求都会携带这些cookie数据     

html5本地存储为每个网站分配空间大小是5MB      
本地存储只支持存储字符串类型数据，若要存储json数据，需要先将数据转换成字符串。     

LocalStorage和SessionStorage两种API在使用上没有区别。      
不过前者会一直存储在本地，直到手动删除，后者存活在当前页面生命周期中，一旦页面关闭就自动消失。     

```
// 存储数据
localStorage.setItem('key', '需要存储的数据');

// 获取数据
var value = localStorage.getItem('key');

// 删除数据
localStorage.removeItem('key');
```

本地存储除了setItem和getItem，还可以使用索引和属性来操作：     

```
// 存储数据
localStorage['key1'] = 'value1';
localStorage.key2 = 'value2';

// 获取数据
var value1 = localStorage['key1'];
var value2 = localStorage.key2;
```

遍历和清空：      

```
// 遍历所有存储的数据
for(var i=0;i<localStorage.length;i++){
	// 获取key
	var key = localStorage.key(i);
	// 获取value
	var value = localStorage.getItem(key);
	// 打印到控制台
	console.log(key, value);
}
// 清空所有数据
localStorage.clear();
```

将数据存储到本地，确保下次打开时数据仍然存在：    

```
<div>
<textarea id="content" cols="100" rows="20"></textarea>
</div>

// 获取记录内容的文本域
var el = document.querySelector('#content');

// 页面载入时，从本地获取存储的数据
el.value = localStorage.getItem('data') || '';

// 为文本域DOM节点添加blur事件
el.addEventListener('blur', function(){
	// 获取文本域的内容
	var data = el.value;
	// 保存到本地
	localStorage.setItem('data', data);
});
```

<h3 id="10">IndexedDB实现便签管理</h3>             

[浏览器数据库 IndexedDB 入门教程](http://www.ruanyifeng.com/blog/2018/07/indexeddb.html)         

IndexedDB是一个事务型数据库系统，同时也是一个基于js的面向对象的数据库系统。     
IndexedDB可以存储大量结构化的数据，并且使用基于索引的高效API检索。     

页面加载后通过读取数据库现有的数据渲染便签列表。然后可以通过添加按钮添加新便签，也可删除按钮删除已有便签:            
*可以在浏览器开发者工具Application选项卡中，展开IndexedDB找到创建的数据库'db1'*      

```
<!--创建一个便签容器-->
<div class="notes">

<!--添加按钮-->
<div class="add">
    <p class="ic_add">+</p>
    <p>添加便签</p>
</div>

</div>

<!--为了简化代码，基于jQuery开发-->
<script src="https://cdn.bootcss.com/jquery/3.2.1/jquery.min.js"></script>

<!--自己封装的操作indexedDB的帮助类-->
<script src="indexeddb.js"></script>

<script>
// 预先定义每一个便签的HTML代码
var divstr = '<div class="note"><a class="close">X</a><textarea></textarea></div>';

// 实例化一个便签数据库、数据表
var db = new LocalDB('db1', 'notes');

// 打开数据库
db.open(function(){

    // 页面初始化时，获取所有已有便签
    db.getAll(function(data){
        var div = $(divstr);
        div.data('id', data.id);
        div.find('textarea').val(data.content);

        // 将便签插入到添加按钮前边
        div.insertBefore(add);
    });
});

// 为添加按钮注册点击事件
var add = $('.add').on('click', function(){
    var div = $(divstr);
    div.insertBefore(add);
    // 添加一条空数据到数据库
    db.set({content:''}, function(id){
        // 将数据库生成的自增id赋值到便签上
        div.data('id', id);
    });
});

// 监听所有便签编辑域的焦点事件
$('.notes').on('blur', 'textarea', function(){
    var div = $(this).parent();
    // 获取该便签的id和内容
    var data = { id: div.data('id'), content: $(this).val() };
    // 写入数据库
    db.set(data);
})

// 监听所有关闭按钮的点击事件
.on('click', '.close', function(){
    if(confirm('确定删除此便签吗？')){
        var div = $(this).parent();
        // 删除这条便签数据
        db.remove(div.data('id'));
        // 删除便签DOM元素
        div.remove();
    }
});
</script>
```
     
为了便于维护，对IndexedDB操作的逻辑封装在indexeddb.js中：     

```
// 声明一个数据库操作的构造函数
function LocalDB(dbName, tableName) {
	this.dbName = dbName;
	this.tableName = tableName;
	this.db = null;
}

// 在原型链上注册open方法，完成打开数据库的操作
LocalDB.prototype.open = function (callback) {
	var _this = this;
    // 执行打开数据库的动作
	var request = window.indexedDB.open(_this.dbName);
    // 打开成功后的回调
	request.onsuccess = function (event) {
        // 获取打开结果：数据库实例
		_this.db = request.result;
        // 如果调用方有回调函数的话，就执行回调函数
        callback && callback();
	};
    // 第一次创建数据库时触发该事件
	request.onupgradeneeded = function (event) {
        // 获取数据库实例
		var db = request.result;
        // 检查是否存在指定的表
		if (!db.objectStoreNames.contains(_this.tableName)) {
            // 如果不存在，则创建，并指定一个自增的id作为查询依据
			db.createObjectStore(_this.tableName, {
				keyPath: "id",
                autoIncrement: true
			});
		}
	};
}

// 获取数据表的实例
LocalDB.prototype.getStore = function () {
	var transaction = this.db.transaction(this.tableName, 'readwrite');
	var objStore = transaction.objectStore(this.tableName);
	return objStore;
}

// 保存一条数据：支持添加和修改
LocalDB.prototype.set = function (data, callback) {
	var objStore = this.getStore();
	var request = data.id ? objStore.put(data) : objStore.add(data);
	request.onsuccess = function (event) {
		callback && callback(event.target.result);
	};
}

// 获取一条数据
LocalDB.prototype.get = function (id, callback) {
	var objStore = this.getStore();
	var request = objStore.get(id);
	request.onsuccess = function (event) {
		callback && callback(event.target.result);
	}
}

// 获取表中所有的数据
LocalDB.prototype.getAll = function (callback) {
	var objStore = this.getStore();
    // 打开数据游标
	var request = objStore.openCursor();
	request.onsuccess = function (event) {
		var cursor = event.target.result;				
		if (cursor) {
            // 如果游标存在，执行回调并传入当前数据行
			callback && callback(cursor.value);
            // 继续下一行数据
			cursor.continue();
		}
	}
}

// 删除一条数据
LocalDB.prototype.remove = function (id) {
	var objStore = this.getStore();
	objStore.delete(id);
}
```

以上代码基本包含了如下常用的数据库操作：      
打开数据库：如果指定的数据库不存在，系统自动创建。      
创建数据表：在首次打开数据库时检测表是否存在，不存在则创建。       
保存一条数据：通过数据表对象的put和add方法实现。      
获取一条数据库：利用索引获取指定id的数据行。      
获取所有数据：使用游标机制遍历所有数据行。      
删除一条数据：可以直接通过数据表对象的delete方法删除一条数据。       

<h3 id="11">Canvas、SVG、WebGL</h3>          

Canvas绘制饼图：     

```
<!-- canvas绘制的图像在一些设备devicePixelRatio不为1的Retina屏幕中显示会出现模糊，设置transform属性缩放原有canvas元素 -->
<canvas class="pie-chart" width="850" height="500" style="transform: scale(0.5);transform-origin: 0 0"></canvas>

//创建PieChart类，获取canvas的context环境
    let PieChart = function(selector, options) {
        let canvas = "string" === typeof selector ? document.querySelector(selector) : null;
        if(canvas === null) return false;
        let defaultOptions = {
            radius: 200,
            legendParms: {
                font: "24px Arial",
                x: 30,
                y: 30,
                margin: 50,
                width: 40,
                height: 24
            }
        }
        this.context = canvas.getContext("2d");
        this.width = canvas.getAttribute("width") || 300;
        this.height = canvas.getAttribute("height") || 300;
        this.options = Object.assign(defaultOptions, options);
    };

    //用于载入饼图使用的数据，并计算饼图的数据总量
    PieChart.prototype.load = function(data) {
        data.forEach(item => this.count ? this.count += item.value : this.count = item.value);
        this.data = data;
        return this;
    };

    //对饼图进行渲染
    PieChart.prototype.render = function() {
        let _generateLegend = (item, index) => {
            this.context.fillRect(
                this.options.legendParms.x, 
                this.options.legendParms.y + index * this.options.legendParms.margin, 
                this.options.legendParms.width, 
                this.options.legendParms.height
            );
            this.context.font = this.options.legendParms.font;
            this.context.fillText(
                item.title, 
                this.options.legendParms.y + this.options.legendParms.margin, 
                (index + 1) * this.options.legendParms.margin
            );
        };
        let temparc = 0;
        this.data.forEach((item, index) => {
            item.color = `#${('00000'+(Math.random()*0x1000000<<0).toString(16)).substr(-6)}`;
            this.context.beginPath();
            this.context.moveTo(this.width / 2, this.height / 2);
            let startarc = temparc, endarc =  startarc + (item.value / this.count) * Math.PI * 2;
            this.context.arc(
                this.width / 2, 
                this.height / 2, 
                this.options.radius, 
                startarc, 
                endarc, 
                false
            );
            this.context.closePath();
            this.context.fillStyle = item.color;
            this.context.fill();
            temparc = endarc;
            if (this.options.legend) {
                _generateLegend(item, index);
            }
        });
        return this;           
    };

    //引入需要绘制的数据创建饼图对象
    const data = [
        {title: "沪江网校", value: 1024}, 
        {title: "沪江小D", value: 512}, 
        {title: "沪江学习", value: 256}, 
        {title: "开心词场", value: 920}
    ];
    let pie = new PieChart(".pie-chart", {legend: true});
    pie.load(data).render();
```  

SVG实现奥运五环：      

可缩放矢量图，基于xml，是用于描述二维矢量图形的一种图形格式。    

```
<svg width="450" height="300" xmlns="http://www.w3.org/2000/svg">
    <g stroke-width="10" fill="none">
        <circle stroke="#0085c7" r="50" cy="117" cx="105"/>
        <circle stroke="#000000" r="50" cy="117" cx="220"/>
        <circle stroke="#df0024" r="50" cy="117" cx="335"/>
        <circle stroke="#f4c300" r="50" cy="172" cx="162"/>
        <circle stroke="#009f3d" r="50" cy="172" cx="278"/>
    </g>
    <g stroke-width="10" fill="none">
        <line stroke="#000000" x1="270" y1="116" x2="268" y2="132"/>
        <line stroke="#0085c7" x1="156" y1="116" x2="153" y2="130"/>
        <line stroke="#df0024" x1="317" y1="163" x2="335" y2="168"/>
        <line stroke="#000000" x1="204" y1="165" x2="218" y2="168"/>        
    </g>
</svg>
```

WebGL带来了3D图像功能：    
3D绘图协议。可以在canvas中绘制3D图形渲染。           

three.js实现简单的正方体3D图形：    

```
<script src="./libs/three.js"></script>

var renderer = new THREE.WebGLRenderer({
    antialias:true
});

renderer.setSize(400, 300);

document.body.appendChild(renderer.domElement);
var camera = new THREE.PerspectiveCamera( 60, 400 / 300, 1, 5000 );
camera.position.z = 500;
var scene = new THREE.Scene();

var cube = new THREE.Mesh(
        new THREE.BoxGeometry( 200, 200, 200 ),
        new THREE.MeshBasicMaterial( { color: 0x6699cc, wireframe: true } )
);

cube.rotation.x = 0.5;
cube.rotation.y = 0.5;
scene.add(cube);

renderer.render( scene, camera );
```

<h3 id="12">PostMessage</h3>          

PostMessage()允许来自不同源的脚本采用异步方式进行有限的通信，可以实现跨文本文档、多窗口、跨域消息传递。     

post_page.html数据发送:     

```
;(function() {
			// 模拟数据
			var messages = [
				'今天天气不错',
				'明天的会议大家不要迟到',
				'今晚大家去吃一顿好的',
				'打车记得拿发票',
				'明天请假一天',
				'这本书干货很多，大家好好看'
			];
			// 随机获取message信息，真实环境是从服务端获取数据
			var getMessage = function() {
				var index = Math.floor(Math.random() * 10);
				// 如果数据不存在则返回null
				return messages[index] || null;
			};
			var postMessageLoop = function() {
				var randomTime = Math.floor(Math.random() * 10000);
				setTimeout(function() {
					var message = getMessage();
					if(message !== null) {
						// 如果消息不为null，则发送消息到父页面
						window.parent.postMessage(message, 'http://localhost:8080');
					}
					postMessageLoop();
				}, randomTime);
			};
			postMessageLoop();
		}());
```    

receive_page.html数据接收：    

```
<h3>消息接收端</h3>
<ul id="messageList"></ul>
<iframe id="postWindow" src="post_page.html"></iframe>

;(function(W) {
    var doc = W.document;
    var msgList = doc.querySelector('#messageList');

    // 处理新的消息
    var handler = function(msg) {
        var li = doc.createElement('li');
        li.innerText = msg;
        // 把消息显示在消息列表中
        msgList.appendChild(li);
    };

    // 监听postMessage发送的消息
    W.addEventListener('message', function(evt) {
        // 判断消息的来源是否正确
        if(evt.origin === 'http://localhost:8080') {
            // 处理新的消息
            handler(evt.data);
        }
    }, false);
}(window));
```

<h3 id="13">XMLHttpRequest Level 2</h3>          

ajax2比ajax做了大幅改进，主要包括：     
设置http请求超时    
使用formData对象管理表单数据    
用于上传文件    
请求跨域，需浏览器支持并且服务器进行对应设置     
获取服务端二进制数据     
获得数据传输进度信息    

基本用法：     
客户端8080端口 部分代码：     

```
数据：<input /><button>获取</button> <!-- 数据获取显示 -->

// 监听按钮点击事件
document.querySelector('button')
.addEventListener('click', function(e){
    // 阻止按钮默认提交事件
    e.preventDefault();
    // 实例化XMLHttpRequest对象
    var xhr = new XMLHttpRequest();
    // 判断浏览器是否支持level 2
    if(typeof xhr.withCredentials === undefined) {
        console.log('浏览器不支持html5 XMLHttpRequest Level 2的跨域请求');
    } else {
        // 监听load事件
        xhr.onload = function() {
            // 将文本转化为json数据
            var data = JSON.parse(xhr.responseText);
            // 显示返回数据
            document.querySelector('input').value = data.data;
        }
        // 监听错误事件
        xhr.onerror = function(e) {
            console.log(e);
        }
        // 请求地址和方法
        xhr.open('GET', 'http://localhost:4412', true);
        // 发送请求
        xhr.send();
    }
});
```   

nodejs服务端代码：    

```
// 引用http模块，用于创建web服务器
var http = require('http');

// 创建新服务器
http.createServer(function(req, res){
	// 设置可以跨域的域名
	res.setHeader('Access-Control-Allow-Origin', 'http://localhost:8080');
	// 服务器支持"GET POST"方法
	res.setHeader('Access-Control-Allow-Methods', 'GET,POST');
	// 设置接收数据编码格式为utf-8
	req.setEncoding('utf8');
	// 返回测试数据
	res.end(JSON.stringify({data: 'Hello World!'}));
}).listen(4412, function(){
	console.log('listening on http://localhost:4412');
});

```

<h3 id="14">Server Sent Event</h3>          

服务端主动向客户端发送数据，并更新客户端信息，让用户始终看到最新信息。     
*传统做法是客户端向服务器发送轮询请求，一旦有新数据，马上更新。*

Server Sent Event技术优点：    
轻量，相对简单。     
单向传送数据（服务端向客户端传送）     
基于HTTP协议    
默认支持断线重连    
自定义发送数据类型     

创建客户端文件sse.html初始化server sent event，并监听message、open、error：    

```
// 监听load事件，页面load完成之后进行后续操作
window.addEventListener("load", function() {
    // 缓存DOM对象
    var status = document.getElementById("status");
    var output = document.getElementById("output");
    var source;

    function connect() {
    // 向服务端建立连接,这里和sse_server.js里stream对应。
    //也可是服务端吐出数据的接口。如:demo_sse.php。目前，EventSource在大多数浏览器端不支持跨域，因此它不是一种跨域的解决方案。
    source = new EventSource("stream");

    // 监听message事件，获取服务端发送的数据
    source.addEventListener("message", function(event) {
        output.textContent = event.data;
    }, false);

    // 监听open事件，判断连接是否进行中
    source.addEventListener("open", function(event) {
        status.textContent = "连接打开了!";
    }, false);

    // 监听error事件，处理连接错误的情况
    source.addEventListener("error", function(event) {
        if (event.target.readyState === EventSource.CLOSED) {
        source.close();
        status.textContent = "连接关闭了!";
        } else {
        status.textContent = "连接关闭了!未知错误！";
        }
    }, false);
    }

    // 判断浏览器是否支持Server Sent Event
    if (!!window.EventSource) {
        connect();
    } else {
        status.textContent = "对不起，你的浏览器不支持 server-sent events";
    }
    }, false);

<span id="status">Connection closed!</span><br />
<span id="output"></span>
```

创建服务端文件用于主动发信息，用Nodejs作为服务器每隔一秒更新数据sse_server.js：     

```
// 引入http模块，创建Web服务器
var http = require("http");
// 引入fs模块，操作文件
var fs = require("fs");

http.createServer(function (req, res) {
  // 默认页面
  var index = "./sse.html";
  // 文件名
  var fileName;
  // 定时器
  var interval;
  // 判断url是什么
  if (req.url === "/")
    fileName = index;
  else
    fileName = "." + req.url;
  // 如果是Server Sent Event建立连接，则设置相应头信息
  if (fileName === "./stream") {
    res.writeHead(200, {"Content-Type":"text/event-stream", "Cache-Control":"no-cache", "Connection":"keep-alive"});
    // 过10000秒重试
    res.write("retry: 10000\n");
    // 首先发送一次时间信息
    res.write("data: " + (new Date()) + "\n\n");
    // 每隔1秒发送一次时间信息
    interval = setInterval(function() {
      res.write("data: " + (new Date()) + "\n\n");
    }, 1000);
    // 监听close事件，用于停止定时器
    req.connection.addListener("close", function () {
      clearInterval(interval);
    }, false);
  } else if (fileName === index) {
    // 判断是否为页面请求，并找到相应文件返回页面
    fs.exists(fileName, function(exists) {
      if (exists) {
        fs.readFile(fileName, function(error, content) {
          if (error) {
            // 文件查找失败返回500
            res.writeHead(500);
            res.end();
          } else {
            // 文件查找成功返回页面
            res.writeHead(200, {"Content-Type":"text/html"});
            res.end(content, "utf-8");
          }
        });
      } else {
        // 文件不存在返回404
        res.writeHead(404);
        res.end();
      }
    });
  } else {
    // 路径不存在返回404
    res.writeHead(404);
    res.end();
  }

}).listen(8080, "127.0.0.1");
console.log("Server running at http://127.0.0.1:8080/");
```

<h3 id="15">WebSocket协议</h3>          

基于TCP连接进行全双工通信。允许数据在两个方向上同时传输。可以用于开发即时聊天，互动游戏，股票信息等应用。     
[WebSocket 详解教程](https://www.cnblogs.com/jingmoxukong/p/7755643.html)              
             
[理解WebSocket和TCP/IP](https://github.com/zyf711/my-study/blob/master/js-course.md#47)         

<h3 id="16">WebRTC实时通讯</h3>          

为浏览器和移动端网页应用提供实时的语音或者视频通话功能    
从用户摄像头和麦克风获取音视频数据，并进行播放：    

```
<video id="source" autoplay muted></video>		<!-- 显示摄像头的源视频 -->
<video id="recorded" loop controls></video>	<!-- 显示已录制的视频 -->
<div>
	<button id="record" disabled>开始录制</button>	<!-- 播放按钮 -->
</div>

<!-- 提供各浏览器WebRTC相关API一致性的适配器 -->
<script src="https://webrtc.github.io/adapter/adapter-latest.js"></script>

<!-- 核心代码 -->
<script src="main.js"></script>
```

main.js代码：     

```
var mediaSource = new MediaSource();	// 创建媒体数据源
// 添加媒体数据源打开时的监听
mediaSource.addEventListener('sourceopen', handleSourceOpen, false);
var mediaRecorder, recordedBlobs, sourceBuffer;	// 声明变量
var sourceVideo = document.getElementById('source');	// 源视频
var recordedVideo = document.getElementById('recorded');	// 已录制视频
var recordButton = document.getElementById('record');	// 录制按钮
recordButton.onclick = toggleRecording;	// 设置录制按钮点击动作

// 设置媒体约束，接收声音和视频，视频宽度为320像素
var constraints = { audio: true, video: { width: 320 } };

// 成功获取用户媒体
function handleSuccess(stream) {
	recordButton.disabled = false;	// 设置录制按钮可用
	window.stream = stream;
	sourceVideo.srcObject = stream;	// 将摄像头画面显示在sourceVideo上
}

// 获取用户媒体异常
function handleError(error) {
	console.log('获取用户媒体错误: ', error);
}

// 获取用户媒体
navigator.mediaDevices.getUserMedia(constraints).
		then(handleSuccess).catch(handleError);

// 处理媒体源打开
function handleSourceOpen(event) {
	sourceBuffer = mediaSource.addSourceBuffer('video/webm; codecs="vp8"');
}

// 处理数据可用
function handleDataAvailable(event) {
	if (event.data && event.data.size > 0) {
		recordedBlobs.push(event.data);	// 将数据追加到录制记录中
	}
}

// 切换录制
function toggleRecording() {
	if (recordButton.textContent === '开始录制') {
		startRecording();	// 开始录制
	} else {
		stopRecording();	// 停止录制
		recordButton.textContent = '开始录制';
	}
}

// 开始录制
function startRecording() {
	recordedBlobs = [];	// 数据记录初始化
	var mimeTypes = ['video/webm;codecs=vp9', 'video/webm;codecs=vp8',
		'video/webm'];
	// 查找支持的视频格式
	var mimeType = mimeTypes.find(type=>MediaRecorder.isTypeSupported(type)) || '';
	try {
		// 创建媒体录制器
		mediaRecorder = new MediaRecorder(window.stream, { mimeType });
	} catch (e) {
		alert('创建媒体录制器异常');
		return;
	}
	recordButton.textContent = '停止录制';
	mediaRecorder.ondataavailable = handleDataAvailable;
	mediaRecorder.start(10);
}

// 停止录制
function stopRecording() {
	mediaRecorder.stop();
	var buf = new Blob(recordedBlobs, { type: 'video/webm' });
	// 设置已录制视频的源为录制好的视频
	recordedVideo.src = window.URL.createObjectURL(buf);
}
```

<h3 id="17">History与单页应用</h3>     

单页应用SPA，可以无刷新在不同页面间切换，并且页面访问记录会被浏览器缓存，支持前进后退等。     
html5的History对象上新增了pushState和replaceState API，配合window对象上新增的popState事件使用，实现单页应用功能     
[添加和修改历史记录中的条目](https://developer.mozilla.org/zh-CN/docs/Web/API/History_API)     

index.html：     

```
<div class="wrapper">
    <ul class="navigator">
      <li class="nav-item">
        green
      </li>
      <li class="nav-item">
        blue
      </li>
      <li class="nav-item">
        red
      </li>
    </ul>
    <div class="content">
    </div>
  </div>

  <script type="text/javascript" src="https://cdn.bootcss.com/zepto/1.2.0/zepto.min.js"></script>
  <script type="text/javascript" src="/index.js"></script>
```

index.js:     

```
var menu = $("ul.navigator > li");
var content = $("div.content");

function initPage(page) { //根据当前url初始化页面
  menu.removeClass("selected-item");
  menu.filter(function(){
	  return $(this).text().toLowerCase().trim() === page;
  }).addClass("selected-item");
  content.text("this is a " + page + " page");
}

initPage(location.pathname.substring(1));

menu.on("click", function(){
	var page = $(this).text().toLowerCase().trim();
	initPage(page);
	history.pushState("", page, page);
});

window.addEventListener("popstate", function(e) {
    initPage(location.pathname.substring(1));
});
```

<h3 id="18">Drag和Drop</h3>     

实现拖放和拖拽效果。还支持桌面文件到浏览器的拖放   

index.html：     

```
<div class="draggable">
<div draggable="true">绿色</div>
</div>
<div class="text">
<div>red</div>
<div>green</div>
</div>

<script type="text/javascript" src="https://cdn.bootcss.com/zepto/1.2.0/zepto.min.js"></script>
<script type="text/javascript" src="/index.js"></script>
```   

index.js:     

```
var draggableColor = $(".draggable > div");
var redText = $(".text > div:nth-child(2)");

draggableColor.on("dragstart", function(event){
  event.dataTransfer.setData("ele", ".draggable > div");
})

redText.on("dragover", function(event){
  event.preventDefault();
}).on("drop", function(event){
  var dragTarget = event.dataTransfer.getData("ele");
  $(dragTarget).css("visibility", "hidden");
  $(this).text("correct");
})
```

<h3 id="19">Web Workers</h3>     

[js与多线程](https://github.com/zyf711/my-study/blob/master/js-course.md#50)           

赋予js多线程运行的能力，可以将耗时的操作放在Web Workers线程里运行，防止页面出现假死。     
根据输入的值，计算对应的位置在斐波那契数列中的值，index.html:      

```
<div class="calc">
    <input type="text" />
    <input type="button" value="计算"／>
  </div>
  <div>
    计算结果：
    <div class="result"></div>
  </div>

  <script type="text/javascript" src="https://cdn.bootcss.com/zepto/1.2.0/zepto.min.js"></script>
  <script type="text/javascript" src="/index.js"></script>
```

index.js:     

```
var input = $("input[type='text']");
var cal = $("input[type='button']");
var result = $(".result");

// cal.on("click", function(){
//   console.log("clicked");
//   var initValue = input.val();
//   var resultValue = fibonacci(initValue);
//   result.text(result.text() + resultValue + " ");
// })

cal.on("click", function(){
  var initValue = input.val();
  var w = new Worker("./worker.js");
  w.postMessage(initValue);
  w.onmessage = function(event) {
    result.html(result.html() + initValue + " => " + event.data + "<br/>");
  }
})

// function fibonacci(n) {
//   return n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2);
// }
```

worker.js:     

```
function fibonacci(n) {
  return n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2);
}

this.onmessage = function(event) {
	var resultValue = fibonacci(event.data);
	this.postMessage(resultValue);
}
```

<h3 id="20">Performance AIP 分析网站性能</h3>     

html5提供可以获取页面加载详细性能指标的Performance AIP，通过window.performance对象暴露给开发者。    

打开页面，如百度首页，控制台输入window.performance.timing      
window.performance.timing对象包含完整的网页加载性能数据：      

页面加载的第一个时间点是navigationStart，表示上一个页面的unload事件触发，接下来时间点是fetchStart表示开始获取当前页面内容。     
fetchStart和navigationStart时间差是浏览器内核为加载新页面做的一些准备工作耗时。       

获取页面内容第一步是查询是否有跟页面有关的缓存，查询完毕后触发开始DNS解析的时间点domainLookupStart。它和fetchStart时间差是查询缓存消耗的时间。        

DNS解析结束的时间点是domainLookupEnd。它和domainLookupStart的时间差是DNS解析消耗的时间。    

DNS解析之后建立TCP连接。connectStart和connectEnd的时间差是建立TCP消耗的时间。      

TCP建立之后开始发送请求内容到服务器端，这个时间点是requestStart。服务端接收到完整请求并处理完毕后，会响应结果返回给客户端，      
开始发送响应结果的时间点为responseStart，浏览器收到之后，会触发responseEnd         

*没有服务器端开始收到请求和收到完整请求的时间点，因为统计是在浏览器端进行，浏览器无法获取该时间*      

浏览器接收到响应结果后，开始DOM树解析时间点是domLoading。DOM解析完成时间点是domInteractive。 解析完成指DOM树构建完成。      
页面依赖的外部资源，如图片，css，js等还未开始加载。     

*domLoading时间点不一定在responseEnd时间点之后，有可能浏览器只接收了部分相应数据就开始解析DOM树了*     

DOM树解析完之后，开始按照顺序运行页面脚本和加载依赖外部资源。一旦脚本运行完毕，会触发DOMContentLoadedEnd事件。     
时间点是domContentLoadedEventStart     

DOMContentLoadedEnd事件执行完毕后，触发domContentLoadedEventEnd时间点。    

当依赖的外部资源全部加载并解析完成之后，触发domComplete时间点，同时触发load事件。loadEventStart时间点表示load事件开始触发，      
loadEventEnd时间点表示load事件上的脚本执行完毕。至此，整个页面加载的生命周期以及性能分析方式介绍完毕。      

获取到所有依赖资源的加载性能：     
`window.performance.getEntries()`









<h2 id="21">html5优化实践</h2>      
   
<h3 id="22">使用history改善AJAX列表请求体验</h3>        
       
数据实现分页显示，最简单的做法是在网址后面加多个page的参数，点“下一页”时，让网页重定向到page+1的新地址。      
例如[新浪的新闻网](https://news.sina.com.cn/roll/#pageid=153&lid=2509&k=&num=50&page=8)就是这么做的，通过改变网址实现。      
     
但是如果这个列表并不是页面的主体部分，或者页面的其它部分有很多图片等丰富元素。再使用这样的方式，整个页面会闪烁得厉害，并且很多资源得重新加载。所以使用ajax请求，动态改变 DOM。      

但是普通动态的请求不会使网址发生变化，用户点了下一页，想要返回到上一个页面时，点浏览器的返回键，返回到上一个网址了。或者刷新页面，发现又回到了第一页。例如[央视的新闻网](http://news.cctv.com/special/china/)就是这样的。    
  
```
//当前第几页
    var pageIndex = 0;
    //请求函数
    function makeRequest(pageIndex){
        var request = new XMLHttpRequest();
        request.onreadystatechange = stateChange;
        //请求传两个参数，一个是当前第几页，另一个是每页的数据条数
        request.open("GET", "/getBook?page=" + pageIndex + "&limit=4", true);
        request.send(null);
        function stateChange(){
            //状态码为4，表示loaded，请求完成
            if(this.readyState !== 4 ){
                return;
            }
            //请求成功
            if(this.status >= 200 && this.status < 300 || this.status === 304){
                var books = JSON.parse(request.responseText);
                renderPage(books); 
            }
        }
　　　　 //避免内存泄漏
　　　　 request = null;
    }
```      
   
拿到数据后进行渲染：       

```
function renderPage(books){
        var bookHtml = 
            "<table>" +
            "   <tr>" +
            "       <th>书名</th>" +
            "       <th>作者</th>" +
            "       <th>版本</th>" +
            "   </tr>";
        for(var i in books){
            bookHtml += 
                "<tr>" +
                "   <td>" + books[i].book_name + "</td>" +
                "   <td>" + books[i].author + "</td>" +
                "   <td>" + books[i].edition + "</td>" +
                "</tr>";
        }
        bookHtml += "</table>";
        bookHtml += 
            "<button>上一页</button>" + 
            "<button onclick='nextPage();'>下一页</button>";
        var section = document.createElement("section");
        section.innerHtml = bookHtml;
        document.getElementById("book").appendChild(section); 
    }
```    
    
到此，如果不做任何处理的话，就不能够发挥浏览器返回、前进按钮的作用。     
html5增加事件：window.onpopstate，当用户点击那两个按钮就会触 发这个事件。      
但是光检测到这个事件是不够的，还得能够传些参数，也就是说返回到之前那个页面的时候得知道那个页面的pageIndex。     
通过 history的pushState方法可以达到这个目的，pushState(pageIndex)将当前页的pageIndex存起来，再返回到这个页面时获取到这个pageIndex。     
pushState的参数如下：    
    
`window.history.pushState(state, title, url);`     
          
state为一个object{}，用来存放当前页面的数据      
title标题      
url为当前页面的url，一旦更改了这个url，浏览器地址栏的地址也会跟着变化。      
    
```
function nextPage(){
        //将页面的index加1
        pageIndex++;
        //重新发请求和页面加载
        makeRequest(pageIndex);
		//存放当前页面的数据
        window.history.pushState({page: pageIndex}, null, window.location.href);
    }
```	   	  
      
然后监听popstate事件：     

```
//如果用户点击返回或者前进按钮
    window.addEventListener("popstate", function(event){
        var page = 0;
        //由于第一页没有pushState，所以返回到第一页的时候是没有数据的，因此得做下判断
        if(event.state !== null){
            page = event.state.page;
        }
        makeRequest(page); 
        pageIndex = page;
    });
```    

state数据通过event传进来，这样就可以得到pageIndex。     
但是一但用户不是在page = 0的位置刷新页面，就会出现需要点多次返回按钮才能够回到原先的页面      
所以得在刷新的时候，把当前页的state数据更新一下，用replaceState，替换队列队首指针的数据，也就是当前页的数据。方法是页面初始化时replace一下：      
    
`window.history.replaceState({page: pageIndex /*此处为0*/}, null, window.location.href);`    

需要注意，popstate事件只能监听自己调用push进去的。      
另外，这种history的缺点是点后退的时候需要发请求获取，解决办法可以手动缓存起来。      
还有页面load事件未触发之前，点后退的时候不会触发popstate事件。      
    
用户刷新，还想停在当前页，一种解决办法是用当前页的window.history.state数据       
在页面初始化时设置pageIndex时就从history.state取：      

`var pageIndex = window.history.state === null ? 0 : window.history.state.page;`     

safari里面的history.state是最近执行pushState传入的数据，因此这个办法在chrome/firefox里面行得通，但是safari行不通。        
     
第二种办法是借助h5的localStorage存放当前页数：       

```
//页面初始化，取当前第几页先从localStorage取
    var pageIndex = window.localStorage.pageIndex || 0;

    function nextPage(){
        //将页面的index加1，同时存放在localStorage
        window.localStorage.pageIndex = ++pageIndex;
        //重新发请求和页面加载
        makeRequest(pageIndex);
        window.history.pushState({page: pageIndex}, null, window.location.href); 
    }

    window.addEventListener("popstate", function(event){
        var page = 0;
        if(event.state !== null){
            page = event.state.page;
        }
        makeRequest(page); 
        //点击返回或前进时，需要将page放到localStorage
        window.localStorage.pageIndex = page;
    });
```      

将页面中所有改变pageIndex的地方，同时放到localStorage。这样刷新页面的时候就可以取到当前页的pageIndex。     

上面的方法都是将pageIndex放到了state参数里，还有一种方法是把它放到第三个参数url里，也就是说通过改变当前页网址的办法。pageIndex从网址里面取。            
这种方法的好处就是链接会带上pageIndex参数跟这变，用前端还是服务端渲染都可以。还可以把带上页数的链接分享出去：           

```
//当前第几页
    var pageIndex = window.location.search.replace("?page=", "") || 0;
    function nextPage(){
        //将页面的index加1
        ++pageIndex;
        //重新发请求和页面加载
        makeRequest(pageIndex);
        window.history.pushState(null, null, "?page=" + pageIndex);
    }
```     
   
需要注意的是，window.history.length虽然返回是的当前队列的元素个数，但不代表history本身就是那个队列。     

除了使用history之外，还有借助hash的方法，[网易新闻](http://digi.163.com/nb/#page=2)就是使用了这样的方法：    

```
//当前第几页
    var pageIndex = window.location.hash.replace("#page=", "") || 0;
    function nextPage(){ 
        makeRequest(pageIndex);
        window.location.hash = "#page=" + pageIndex;
    }
    window.addEventListener("hashchange", function(){
        var page = window.location.hash.replace("#page=", "") || 0;
        makeRequest(page);
    });
```     

关于支持性，参考[caniuse网站](https://caniuse.com/#search=history)：history IE10及以上支持，hashchange的支持性较好，IE8及以上都支持。      
虽然hashchange的支持性较好，但是history的优点是可以传数据。对一些复杂的应用可能会有很大的发挥作用，hash这么用就不能做锚点定位了。     
当想要用动态请求的同时改变浏览器的地址，并且支持前进后退，就可以用history。       
         
<h3 id="23">使用图标字体iconfont代替雪碧图</h3>        
    
雪碧图缺点：高清屏会模糊，无法动态变化如hover时候反色。    
在2×的设备像素比的屏幕上，如果达到和文字一样的清晰度，图片的宽度需要实际显示大小的两倍，否则看起来模糊。     
例如iphone x 的分辨率1125*2436，所以为了高清屏，用雪碧图可能要准备多种规格的图片。     

图标字体icon font：     
图标制作的字体，使用时和普通字体无异，可设置字号，颜色等。最大优点拥有字体的矢量无失真特点。    

图标字体的制作：     
PS打开UI图，文件->导出->illustrator。 AI执行file->Scripts->SaveDocsAsSVG 导出成svg      
或ps cc直接图层右键，选择导出来，格式svg。    

有了svg可以去第三方网站[icomoon.io](https://icomoon.io/)制作图标：      
点击右上角"icoMoon App" 按钮     
点击左上角"import icons" 按钮上传svg文件    
点击"Untitled Set"下选择上传的所有的svg文件预览图标    
点击右下角"Generate Font" 按钮    
可以点击上方"PreFerences"按钮设置相关    
点击右下角"Download"按钮下载    

制作中图标字体如果只支持单路径，可以用PS合并形状组件功能，这样子svg就是单路径。    
有些图标是多个图层组成，选中多个形状后，右键合并形状，然后合并形状组件。      
生成的svg上传上去是空的，可能是svg文件有fill:none;改成随便一个色值即可。      

阿里提供了一个[在线图标制作网站](http://www.iconfont.cn),和icomoon.io相比，没有提供编码的方式，只能使用html实体的方式。     

图标字体的使用：    
其中fonts文件夹存放字体格式：.eot,.svg,.ttf,.woff文件     

```
/*html实体的方式*/
@font-face {
        font-family: 'icomoon';
        src:  url('fonts/icomoon.eot?xmo1ez');
        src:  url('fonts/icomoon.eot?xmo1ez#iefix') format('embedded-opentype'),
        url('fonts/icomoon.ttf?xmo1ez') format('truetype'),
        url('fonts/icomoon.woff?xmo1ez') format('woff'),
        url('fonts/icomoon.svg?xmo1ez#icomoon') format('svg');
    }
    .icon-uniE900{
        font-family: 'icomoon';
        font-size:24px;
        color:red;
    }

<span class="icon-uniE900">&#xe900</span>

/*编码的方式*/
@font-face {
	font-family: 'icomoon';
	src:  url('fonts/icomoon.eot?xmo1ez');
	src:  url('fonts/icomoon.eot?xmo1ez#iefix') format('embedded-opentype'),
	url('fonts/icomoon.ttf?xmo1ez') format('truetype'),
	url('fonts/icomoon.woff?xmo1ez') format('woff'),
	url('fonts/icomoon.svg?xmo1ez#icomoon') format('svg');
}
.icon-uniE900{
	font-family: 'icomoon';
	font-size:24px;
	color:red;
}
.icon-uniE900:before {
	content: "\e900";
}

<span class="icon-uniE900"></span>
```    
    
可能出现的问题：    
        
浏览器会在图标边缘加粗一像素：   
抗锯齿渲染：      

```
-webkit-font-smoothing: antialiased; /*chrome、safari*/
-moz-osx-font-smoothing: grayscale;/*firefox*/
```
     
注意缓存：   
后续加了新的图标字体。已经加载过的浏览器可能有缓存，导致新图标字体不重新下载，最简单的解决方法就是加一个版本号参数如：        

`fonts/icomoon.eot?xmo1ez`       
   
图标字体在安卓上：      
通过外链引入的图标字体的加载经常会慢与html的加载。字体没加载好，安卓上会先使用一个默认字体来代替，而图标字体的编码，      
可能刚好就是某一个繁体字的编码。导致了刷新页面的时候先是繁体之后变成图标的问题。ios和电脑的浏览器上是先显示一个方框，       
等字体加载好了在变成正常图标。         
把图标字体转成base64可以解决。或使用内联的方式也可以避免这种问题。      
    
结合使用SVG：     
svg在ie8不支持。其他都还好。使用svg的方法：     
直接copy到页面：把一个svg当成html标签嵌入页面，当成内联的，可以直接用css控制svg样式       
缺点是html文件太大，浏览器一般不会缓存html，同时阻碍页面加载：         

```
<div>
<svg>...</svg>
<p>其他内容</p>
</div>	
```
   
使用embed/object/img:      
img兼容性比embed稍差，缺点是由于是一个外链，没法用css控制样式：      

```
<embed src="loc.svg" width="100" height="200">
<img src="loc.svg" width="100" height="200">
```
    
当小svg过多，要合并成一个svg。像雪碧图那样：    

```
<svg>
<symbol viewBow="0 0 101.5 57.9" id="active-triangle">
    <path fill="#123456" d="M100.4.5L50.5 57.1 1.1.5h99.3z"/>
</symbol>
<symbol viewBow="0 0 101.5 57.9" id="logo">
    <path fill="#123456" d="M100.4.5L50.5 57.1 1.1.5h99.3z"/>
</symbol>
</svg>
```
   
使用的时候通过外链将svg引入，通过文件名id的方式：     

```
<svg viewBox="0 0 100 100">
	<use xlink:href="icon.svg#logo"></use>
</svg>
```   

ie不支持外链，可以通过插件[SVG for Everybody](https://github.com/jonathantneal/svg4everybody)让ie支持。     
[highCharts](https://github.com/highcharts/highcharts)和[d3](https://github.com/d3/d3)也使用了SVG           
     
<h3 id="24">实现前端剪裁压缩图片</h3>          
   
支持拖拽    
压缩    
剪裁编辑    
上传和上传进度显示    

拖拽显示图片：     
读取用户拖过来的图片并把它转成base64以在本地显示：     

```
var handler={
    init:function($container){
        //需要把dragover的默认行为禁掉，不然会跳页
        $container.on("dragover",function(event){
            event.preventDefault();
        });
        $container.on("drop",function(event){
            event.preventDefault();
            //这里获取拖过来的图片文件，为一个File对象
            var file=event.originalEvent.dataTransfer.files[0];
            handler.handleDrop($(this),file);
        });
     }
}
```   
    
如果使用input，则监听input的change事件。获取File对象，同样传给handleDrop进行处理：     

```
$container.on("change","input[type=file]",function(event){
            if(!this.value)return;
            var file=this.files[0];
            handler.handleDrop($(this).closest(".container"),file);
            this.value="";
        });
```
   
在handleDrop函数里，读取file的内容，并把它转成base64的格式：    

```
handleDrop:function($container,file){
    var $img = $container.find("img");
    handler.readImgFile(file,$img,$container);
},
```   

在readImgFile里面读取图片文件内容：    

```
readImgFile:function(file,$img,$container){
    var reader = new FileReader(file);
    //检验用户是否选则是图片文件
    if(file.type.split("/")[0]!=="image"){
        util.toast("You should choose an image file");
        return;
    }  
    reader.onload=function(event){
        var base64 = event.target.result;
        handler.compressAndUpload($img,base64,file,  $container);
    }  
    reader.readAsDataURL(file);
}
```      
   
FileReader读取文件内容，调的是readAsDataURL，这个api能够把二进制图片内容转成base64的格式。     
读取完之后会触发onload事件，在onload里面进行显示和上传：     

```
//获取图片base64内容
var base64 = event.target.result;
//如果图片大于1MB，将body置半透明
if(file.size>ONE_MB){
    $("body").css("opacity",0.5);
}
//因为这里图片太大会被卡一下，整个页面会不可操作
$img.attr("src",baseUrl);
//还原
if(file.size>ONE_MB){
    $("body").css("opacity",1);
}
//然后再调一个压缩和上传的函数
handler.compressAndUpload($img,file,$container);
```
   
如果图片有几个Mb的，在上面第8行展示的时候被卡一下，采取了一个补偿措施：通过把页面变虚告诉用户现在在处理之中，页面不可操作，稍等一会    

这里还会有一个问题，就是ios系统拍摄的照片，如果不是横着拍的，展示出来的照片旋转角度会有问题:     
竖着拍的照片不管你怎么拍，ios实际存的图片都是横着放的，因此需要用户自己手动去旋转。     
旋转的角度放在了exif的数据结构里面，把这个读出来就知道它的旋转角度了，用一个[EXIF](https://github.com/exif-js/exif-js)的库读取：       

```
readImgFile:function(file,$img,$container){
    EXIF.getData(file,function(){
        varorientation=this.exifdata.Orientation,
            rotateDeg=0;
        //如果不是ios拍的照片或者是横拍的，则不用处理，直接读取
        if(typeoforientation==="undefined"||orientation===1){
            //原本的readImgFile，添加一个rotateDeg的参数
            handler.doReadImgFile(file,$img,$container,rotateDeg);
        }  
        //否则用canvas旋转一下
        else{
            rotateDeg=orientation===6?90*Math.PI/180:
                            orientation===8?-90*Math.PI/180:
                            orientation===3?180*Math.PI/180:0;
            handler.doReadImgFile(file,$img,$container,rotateDeg);
        }  
    });
}
```
   
知道角度之后，就可以用canvas处理了，在下面的压缩图片进行说明，因为压缩也要用到canvas    

压缩图片:     
canvas可以很方便地实现压缩，其原理是把一张图片画到一个小的画布，然后再把这个画布的内容导出base64，就能够拿到一张被压小的图片了：      

```
//设定图片最大压缩宽度为1500px
var maxWidth = 1500;
var resultImg=handler.compress($img[0],maxWidth,file.type);
```   
   
compress函数进行压缩，在这个函数里首先创建一个canvas对象，然后计算这个画布的大小：     

```
compress:function(img,maxWidth,mimeType){
    //创建一个canvas对象
    var cvs = document.createElement('canvas');
    var width = img.naturalWidth,
        height = img.naturalHeight,
        imgRatio=width/height;
    //如果图片维度超过了给定的maxWidth 1500，
    //为了保持图片宽高比，计算画布的大小
    if(width>maxWidth){
        width=maxWidth;
        height=width/imgRatio;
    }  
    cvs.width=width;
    cvs.height=height;
}
```
   
接下来把大的图片画到一个小的画布上，再导出：     

```
//把大图片画到一个小画布
    var ctx = cvs.getContext("2d").drawImage(img,0,0,img.naturalWidth,img.naturalHeight,0,0,width,height);
    //图片质量进行适当压缩
    var quality = width>=1500?0.5:
                  width>600?0.6:1;
    //导出图片为base64
    var newImageData = cvs.toDataURL(mimeType,quality);
 
    var resultImg=newImage();
    resultImg.src=newImageData;
    return resultImg;
```   
  
这里需要注意，有的浏览器把base64赋值给new出来的Image的src时，是异步操作，特别是safari    
所以要监听onload才能对图片进行下一步处理：    

```
var img = new Image();
img.onload = function(){
    canvas.draw(img,...);
}
img.src = base64;
```
   
ios竖着拍的照片需要旋转，在压缩的时候可以一起处理，在canvas上面旋转：    

```
var ctx = cvs.getContext("2d");
var destX = 0,
    destY = 0;
if(rotateDeg){
    ctx.translate(cvs.width/2,cvs.height/2);
    ctx.rotate(rotateDeg);
    destX=-width/2,
    destY=-height/2;
}
ctx.drawImage(img,0,0,img.naturalWidth,img.naturalHeight,destX,destY,width,height);

```
       
需要先把canvas的原点移到画布中心，然后再旋转，默认原点是在左上角。     
这样就解决了ios图片旋转的问题，得到一张旋转和压缩调节过的图片之后，再用它进行裁剪和编辑    
    
裁剪图片：     
裁剪图片，用到了一个插件[cropper](https://fengyuanchen.github.io/cropper/)      
支持裁剪、旋转、翻转，但是它并没有对图片真正的处理，只是记录了用户做了哪些变换，然后你自己再去处理。      
可以把变换的数据传给后端，让后端去处理。前端处理在此不兼容IE8：     

把一张图片，旋转了一下，同时翻转了一下得到插件信息：     

```
{
    height:319.2000000000001,
    rotate:45,
    scaleX:-1,
    scaleY:1,
    width:319.2000000000001
    x:193.2462838120872
    y:193.2462838120872
}
```
       
通过这些信息就知道了：图片被左右翻转了一下，同时顺时针转了45度，还知道裁剪选框的位置和大小。通过这些完整的信息就可以做一对一的处理      
在展示的时候，插件使用的是img标签，设置它的css的transform属性进行变换。真正的处理还是要借助canvas      

假设用户没有进行旋转和翻转，只是选了简单地选了下区域裁剪了一下，那就简单很多。     
最简单的办法就是创建一个canvas，它的大小就是选框的大小，然后根据起点x、y和宽高把图片相应的位置画到这个画布，再导出图片就可以了。      
由于考虑到需要翻转，所以用第二种方法：      
创建一个和图片一样大小的canvas，把图片原封不动地画上去，然后把选中区域的数据imageData存起来，重新设置画布的大小为选中框的大小，再把imageData画上去，最后再导出就可以了：      

```
var cvs = document.createElement('canvas');
var img = $img[0];
var width = img.naturalWidth,
    height = img.naturalHeight;

cvs.width=width;
cvs.height=height;
 
var ctx = cvs.getContext("2d");
var destX = 0,
    destY = 0;
ctx.drawImage(img,destX,destY);
 
//通过插件给的数据，把选中框里的图片内容存起来
var imageData = ctx.getImageData(cropOptions.x,cropOptions.y,cropOptions.width,cropOptions.height);
cvs.width=cropOptions.width;
cvs.height=cropOptions.height;
//然后再画上去
ctx.putImageData(imageData,0,0);
```
   
如果用户做了翻转，用上面的结构很容易可以实现，只需要在第11行drawImage之前对画布做一下翻转变化
其它的都不用变，就可以实现上下左右翻转了：       

```
//fip
if(cropOptions.scaleX===-1||cropOptions.scaleY===-1){
    destX=cropOptions.scaleX===-1?width*-1:0;      // Set x position to -100% if flip horizontal
    destY=cropOptions.scaleY===-1?height*-1:0;     // Set y position to -100% if flip vertical
    ctx.scale(cropOptions.scaleX,cropOptions.scaleY);
}
ctx.drawImage(img,destX,destY);
```   
       
两种变换叠加没办法直接通过变化canvas的坐标，一次性drawImage上去。      
还是有两种办法，第一种是用imageData进行数学变换，计算一遍得到imageData里面，从第一行到最后一行每个像素新的rgba值是多少，然后再画上去；        
第二种办法，就是创建第二个canvas，第一个canvas作翻转，把它的结果画到第二个canvas，然后再旋转，最后导到。第二种办法相对比较简单     

在第一个canvas画完之后,实现旋转、翻转结合：      

```
ctx.drawImage(img,destX,destY);
//rotate
if(cropOptions.rotate!==0){
    var newCanvas = document.createElement("canvas"),
        deg = cropOptions.rotate/180*Math.PI;
    //旋转之后，导致画布变大，需要计算一下
    newCanvas.width=Math.abs(width*Math.cos(deg))+Math.abs(height*Math.sin(deg));
    newCanvas.height=Math.abs(width*Math.sin(deg))+Math.abs(height*Math.cos(deg));
    varnewContext=newCanvas.getContext("2d");
    newContext.save();
    newContext.translate(newCanvas.width/2,newCanvas.height/2);
    newContext.rotate(deg);
    destX=-width/2,
    destY=-height/2;
    //将第一个canvas的内容在经旋转后的坐标系画上来
    newContext.drawImage(cvs,destX,destY);
    newContext.restore();
    ctx=newContext;
    cvs=newCanvas;
}
```
      
将第二步的代码插入第一步，再将第三步的代码插入第二步，就是一个完整的处理过程了。     

文件上传和上传进度：     

文件上传只能通过表单提交的形式，编码方式为multipart/form-data     
可以通过写一个form标签进行提交，也可以模拟表单提交的格式     

```
var xhr = newXMLHttpRequest();
xhr.open('POST',upload_url,true);
var boundary='someboundary';
xhr.setRequestHeader('Content-Type','multipart/form-data; boundary='+boundary);

```

并设置编码方式，然后拼表单格式的数据进行上传：     

```
var data=img.src;
data=data.replace('data:'+file.type+';base64,','');
xhr.sendAsBinary([
    //name=data
    '--'+boundary,
        'Content-Disposition: form-data; name="data"; filename="'+file.name+'"',
        'Content-Type: '+file.type,'',
        atob(data),'--'+boundary,
    //name=docName
    '--'+boundary,
        'Content-Disposition: form-data; name="docName"','',
        file.name,
    '--'+boundary+'--'
].join('\r\n'));
```

表单数据不同的字段是用boundary的随机字符串分隔的。拼好之后用sendAsBinary发出去。     
上传功能参考JIC插件，但这个API已经废弃，不推荐使用这种方式。      

调这个函数之前先监听它的事件：    

```
xhr.upload.onprogress=function(event){
    if(event.lengthComputable){
        duringCallback((event.loaded/event.total)*100);
    }
};
```    

这里凋duringCallback的回调函数，给这个回调函数传了当前进度的参数，用这个参数就可以设置进度条的过程了。     
进度条可以自己实现，或者直接上网找一个。      

对成功和失败做一些反馈处理：    

```
xhr.onreadystatechange=function(){
    if(this.readyState==4){
        if(this.status==200){
            successCallback(this.responseText);
        }elseif(this.status>=400){
            if(errorCallback&&  errorCallback instanceofFunction){
                errorCallback(this.responseText);
            }      
        }      
    }
};
```     

至此整个功能就拆解说明完了，上面的代码可以兼容到IE10，FileReader的api到IE10才兼容           
    
<h3 id="25">前端本地文件操作与上传</h3>            
    
FormData对象：     
*[FormData 对象的使用](https://developer.mozilla.org/zh-CN/docs/Web/API/FormData/Using_FormData_Objects)*            
提供一种简单的方式创建一个包含键值对的form表单结构，可以用XMLHttpRequest.send()方法很方便的提交用FormData创建的form表单数据。     
可以通过new 的方式创建一个FormData对象:     

`var fm=new FormData();`    

添加一条数据到FormData对象中如果添加的数据key值已经存在，append方法会在key值对应的values末尾添加value值：       
   
`FormData.append(name,value);`  
    
使用form表单初始化一个FormData对象     
可以用一个已有的 form 元素来初始化 FormData 对象，只需要把这个 form 元素作为参数传入 FormData 构造函数即可：    

```
var formElement = document.getElementById("myFormElement");
var oReq = new XMLHttpRequest();
oReq.open("POST", "submitform.php");
oReq.send(new FormData(formElement));
```

前端无法像原生APP一样直接操作本地文件，需要通过用户触发，用户可通过以下三种方式操作触发：     
通过input type="file" 选择本地文件       
通过拖拽的方式把文件拖过来      
在编辑框里面复制粘贴     

第一种是最常用的手段，通常还会自定义一个按钮，然后盖在它上面，因为type="file"的input不好改变样式。如下代码写一个选择控件，并放在form里面：       

```
<form>
    <input type="file" id="file-input" name="fileContent">
</form>
```
      
然后就可以用FormData获取整个表单的内容：      

```
$("#file-input").on("change", function() {
    console.log(`file name is ${this.value}`);
    let formData = new FormData(this.form);
    formData.append("fileName", this.value);
    console.log(formData);
});
```    
    
在浏览器无法获取到文件的真实存放位置。同时FormData打印出来是一个空的Objet,      
但并不是说它的内容是空的，只是它对前端开发人员是透明的，无法查看、修改、删除里面的内容，只能append添加字段。      
    
FormData无法得到文件的内容，而使用FileReader可以读取整个文件的内容。用户选择文件之后，input.files就可以得到用户选中的文件：     

```
$("#file-input").on("change", function() {
    let fileReader = new FileReader(),
        fileType = this.files[0].type;
    fileReader.onload = function() {
        if (/^image\/[jpeg|png|gif]/.test(fileType)) {
            // 读取结果在fileReader.result里面
            $(`<img src="${this.result}">`).appendTo("body");
        }
    }
    // 打印原始File对象
    console.log(this.files[0]);
    // base64方式读取
    fileReader.readAsDataURL(this.files[0]);    
});
```

使用FileReader除了可读取为base64之外，还能读取为以下格式：     

```
// 按base64的方式读取，结果是base64，任何文件都可转成base64的形式
fileReader.readAsDataURL(this.files[0]);

// 以二进制字符串方式读取，结果是二进制内容的utf-8形式，已被废弃了
fileReader.readAsBinaryString(this.files[0]);

// 以原始二进制方式读取，读取结果可直接转成整数数组
fileReader.readAsArrayBuffer(this.files[0]);

```    

其它的主要是能读取为ArrayBuffer，它是一个原始二进制格式的结果。它对前端开发人员也是透明的，不能够直接读取里面的内容，      
但可以通过ArrayBuffer.length得到长度，还能转成整型数组，就能知道文件的原始二进制内容了：      

```
let buffer = this.result;
// 依次每字节8位读取，放到一个整数数组
let view = new Uint8Array(buffer);
console.log(view);
```

第二种拖拽的方式，读取文件:      

```
<div class="img-container">
    drop your image here
</div>

```   

然后监听它的拖拽事件：     

```
$(".img-container").on("dragover", function (event) {
    event.preventDefault();
})

.on("drop", function(event) {
    event.preventDefault();
    // 数据在event的dataTransfer对象里
    let file = event.originalEvent.dataTransfer.files[0];

    // 然后就可以使用FileReader进行操作
    fileReader.readAsDataURL(file);

    // 或者是添加到一个FormData
    let formData = new FormData();
    formData.append("fileContent", file);
})
```   
    
数据在drop事件的event.dataTransfer.files里面，拿到这个File对象之后就可以和输入框进行一样的操作了，      
即使用FileReader读取，或者是新建一个空的formData，然后把它append到formData里面。     

第三种粘贴的方式，通常是在一个编辑框里操作，如把div的contenteditable设置为true：     

```
 <div contenteditable="true">
      hello, paste your image here
 </div>
```
   
粘贴的数据是在event.clipboardData.files里面：     

```
$("#editor").on("paste", function(event) {
    let file = event.originalEvent.clipboardData.files[0];
});
```    

但是Safari的粘贴不是通过event传递的，它是直接在输入框里面添加一张图片,它新建了一个img标签，并把img的src指向一个blob的本地数据。       
[blob对象详解](https://www.cnblogs.com/hhhyaaon/p/5928152.html)         

blob是一种类文件的存储格式，它可以存储几乎任何格式的内容，如json：    

```
let data = {hello: "world"};
let blob = new Blob([JSON.stringify(data)],
  {type : 'application/json'});

```

为了获取本地的blob数据，我们可以用ajax发个本地的请求:    

```
$("#editor").on("paste", function(event) {
    // 需要setTimeout 0等图片出来了再处理
    setTimeout(() => {
        let img = $(this).find("img[src^='blob']")[0];
        console.log(img.src);
        // 用一个xhr获取blob数据
        let xhr = new XMLHttpRequest();
        xhr.open("GET", img.src);
        // 改变mime类型
        xhr.responseType = "blob";
        xhr.onload = function () {
            // response就是一个Blob对象
            console.log(this.response);
        };
        xhr.send();
    }, 0);
});
```

能得到它的大小和类型，但是具体内容也是不可见的，和File一样，可以使用FileReader读取它的内容：      

```
function readBlob(blobImg) {
    let fileReader = new FileReader();
    fileReader.onload = function() {
        console.log(this.result);
    }
    fileReader.onerror = function(err) {
        console.log(err);
    }
    fileReader.readAsDataURL(blobImg);
}

readBlob(this.response);
```

它有一个slice的方法，可用于切割大文件   
网盘的断点续传有一种方法是使用blob分隔文件大小：     
[前端实现文件的断点续传](https://www.cnblogs.com/imwtr/p/5957391.html)             

```
let fileReader = new FileReader(),
    file = this.files[0];
console.log(`总共发送${file.size}字节`);
const ONE_MB = 1024 * 1024;
let sendedBytes = 0;
fileReader.onload = function(){
    //发送分隔的片断
    xhr.open(),xhr.send(this.result);
    sendedBytes += ONE_MB;
    if(sendedBytes < file.size){
        //file的slice方法继承与blob
        let blob = file.slice(sendedBytes,sendedBytes + ONE_MB);
        fileReader.readAsArrayBuffer(blob)
    }
}
let blob = file.slice(0,ONE_MB)
consloe.log(blob instanceof Blob); //true
fileReader.readAsArrayBuffer(blob;)
```



除此，还能使用window.URL读取，这是一个新的API，经常和Service Worker配套使用，因为SW里面常常要解析url：           

```
function readBlob(blobImg) {
    let urlCreator = window.URL || window.webkitURL;
    // 得到base64结果
    let imageUrl = urlCreator.createObjectURL(this.response);
    return imageUrl;
}

readBlob(this.response);
```

URL对象是硬盘（SD卡等）指向文件的一个路径，如果我们做文件上传的时候，想在没有上传服务器端的情况下看到上传图片的效果图,可以通过：      

`var url=window.URL.createObjectURL(obj.files[0]);`             

获得一个http格式的url路径，这个时候就可以设置到img标签中显示了。               

关于src使用的是blob链接的，除了上面提到的img之外，另外一个很常见的是video标签，如youtobe的视频就是使用的blob    
这种数据不是直接在本地的，而是通过持续请求视频数据，然后再通过blob这个容器媒介添加到video里面，它也是通过URL的API创建的：     

```
let mediaSource = new MediaSource();
video.src = URL.createObjectURL(mediaSource);
let sourceBuffer = mediaSource.addSourceBuffer('video/mp4; codecs="avc1.42E01E, mp4a.40.2"');
sourceBuffer.appendBuffer(buf);
```

上面，我们使用了三种方式获取文件内容，最后得到：    
FormData格式     
FileReader读取得到的base64或者ArrayBuffer二进制格式    

如果直接就是一个FormData了，那么直接用ajax发出去就行了，不用做任何处理：     

```
let form = document.querySelector("form"),
    formData = new FormData(form),
formData.append("fileName", "photo.png");

let xhr = new XMLHttpRequest();
// 假设上传文件的接口叫upload
xhr.open("POST", "/upload");
xhr.send(formData);
```

如果用jQuery的话，要设置两个属性为false：    

```
$.ajax({
    url: "/upload",
    type: "POST",
    data: formData,
    processData: false,  // 不处理数据
    contentType: false   // 不设置内容类型
});
```

因为jQuery会自动把内容做一些转义，并且根据data自动设置请求mime类型，这里告诉jQuery直接用xhr.send发出去就行了。    
这是一种区别于用&连接参数的方式，它的编码格式是multipart/form-data，就是上传文件form表单写的enctype：     

```
<form enctype="multipart/form-data" method="post">
    <input type="file" name="fileContent">
</form>
```

如果xhr.send的是FormData类型话，它会自动设置enctype，如果你用默认表单提交上传文件的话就得在form上面设置这个属性     

如果读取结果是ArrayBuffer的话，也是可以直接用xhr.send发送出去的，但是一般我们不会直接把一个文件的内容发出去，而是用某个字段名等于文件内容的方式。    
如果你读取为ArrayBuffer的话再上传的话其实作用不是很大，还不如直接用formData添加一个File对象的内容，     
因为上面三种方式都可以拿到File对象。如果一开始就是一个ArrayBuffer了，那么可以转成blob然后再append到FormData里面。     

使用比较多的应该是base64，因为前端经常要处理图片，读取为base64之后就可以把它画到一个canvas里面，然后就可以做一些处理，如压缩、裁剪、旋转等。    
最后再用canvas导出一个base64格式的图片，上传base64格式:     

第一种是拼一个表单上传的multipart/form-data的格式，再用xhr.sendAsBinary发出去:    

```
let base64Data = base64Data.replace(/^data:image\/[^;]+;base64,/, "");
let boundary = "----------boundaryasoifvlkasldvavoadv";
xhr.sendAsBinary([
    // name=data
    boundary,
        'Content-Disposition: form-data; name="data"; filename="' + fileName + '"',
        'Content-Type: ' + "image/" + fileType, '',
        atob(base64Data), boundary,
    //name=imageType
    boundary,
        'Content-Disposition: form-data; name="imageType"', '',
        fileType,
    boundary + '--'
].join('\r\n'));
```   

上面代码使用了window.atob的api，它可以把base64还原成原始内容的字符串表示     
btoa是把内容转化成base64编码，而atob是把base64还原。在调atob之前，需要把表示内容格式的不属于base64内容的字符串去掉，即上面代码第一行的replace处理。      
Base64转码的对象只能是字符串      
字符串“Hello World!”已被Base64编码和解码。但是，atob和btoa不能编码Unicode字符和不支持ie10以下：        
*叫[atob和btoa编码Unicode字符和支持ie9](https://my.oschina.net/itblog/blog/1613977)*           

```
var string = 'Hello World!';

var encodedString = btoa(string);
console.log(encodedString); // Outputs: "SGVsbG8gV29ybGQh"

var decodedString = atob(encodedString);
console.log(decodedString); // Outputs: "Hello World!"
```

使用window.encodeURIComponent和window.decodeURIComponent叫转码支持汉字:      

```
var str = "China，中国";
window.btoa(window.encodeURIComponent(str))
//"Q2hpbmElRUYlQkMlOEMlRTQlQjglQUQlRTUlOUIlQkQ="
 
window.decodeURIComponent(window.atob('Q2hpbmElRUYlQkMlOEMlRTQlQjglQUQlRTUlOUIlQkQ='))
//"China，中国"
```

这样就和使用formData类似了，但是由于sendAsBinary已经被deprecated了，所以新代码不建议再使用这种方式。    
可以把base64转化成blob，然后再append到一个formData里面，下面的函数（来自b64-to-blob）可以把base64转成blob：     

```
function b64toBlob(b64Data, contentType, sliceSize) {
    contentType = contentType || '';
    sliceSize = sliceSize || 512;

    var byteCharacters = atob(b64Data);
    var byteArrays = [];

    for (var offset = 0; offset < byteCharacters.length; offset += sliceSize) {
      var slice = byteCharacters.slice(offset, offset + sliceSize);

      var byteNumbers = new Array(slice.length);
      for (var i = 0; i < slice.length; i++) {
        byteNumbers[i] = slice.charCodeAt(i);
      }

      var byteArray = new Uint8Array(byteNumbers);

      byteArrays.push(byteArray);
    }

    var blob = new Blob(byteArrays, {type: contentType});
    return blob;
}
```   

然后就可以append到formData里面,这样就不用自己去拼一个multipart/form-data的格式数据了:          

```
let blob = b64toBlob(b64Data, "image/png"),
    formData = new FormData();
formData.append("fileContent", blob);
```

上面处理和上传文件的API可以兼容到IE10+，如果要兼容老的浏览器可以借助一个iframe      
原理是默认的form表单提交会刷新页面，或者跳到target指定的那个url，     
但是如果把ifrmae的target指向一个iframe，那么刷新的就是iframe，返回结果也会显示在ifame，然后获取这个ifrmae的内容就可得到上传接口返回的结果:       

```
let iframe = document.createElement("iframe");
iframe.display = "none";
iframe.name = "form-iframe";
document.body.appendChild(iframe);
// 改变form的target
form.target = "form-iframe";

iframe.onload = function() {
    //获取iframe的内容，即服务返回的数据
    let responseText = this.contentDocument.body.textContent 
            || this.contentWindow.document.body.textContent;
};

form.submit();
```

form.submit会触发表单提交，当请求完成（成功或者失败）之后就会触发iframe的onload事件，     
然后在onload事件获取返回的数据，如果请求失败了的话，iframe里的内容就为空，可以用这个判断请求有没有成功。     

使用iframe没有办法获取上传进度，使用xhr可以获取当前上传的进度，这个是在XMLHttpRequest 2.0引入的：      

```
xhr.upload.onprogress = function (event) {
    if (event.lengthComputable) {
        // 当前上传进度的百分比
        duringCallback ((event.loaded / event.total)*100);
    }
};
```

这样就可以做一个真实的loading进度条。    

3种交互方式的读取方式:      
通过input控件在input.files可以得到File文件对象，     
通过拖拽的是在drop事件的event.dataTransfer.files里面，     
而通过粘贴的paste事件在event.clipboardData.files里面，      

Safari这个怪胎是在编辑器里面插入一个src指向本地的img标签，可以通过发送一个请求加载本地的blob数据，然后再通过FileReader读取，      
或者直接append到formData里面。得到的File对象就可以直接添加到FormData里面，      

如果需要先读取base64格式做处理的，那么可以把处理后的base64转化为blob数据再append到formData里面。      

对于老浏览器，可以使用一个iframe解决表单提交刷新页面或者跳页的问题。       
   
<h3 id="26">Service Worker做一个PWA离线网页应用</h3>              
     
PWA和Service Worker的关系：     

PWA (Progressive Web Apps) 可以把她理解为一种模式，一种通过应用一些技术将 Web App 在安全、性能和体验等方面带来渐进式的提升的一种 Web App的模式。      
Service Worker 是一个独立于js主线程的一种 Web Worker 线程， 一个独立于主线程的 Context，      
但是面向开发者来说 Service Worker 的形态其实就是一个需要开发者自己维护的文件，我们假设这个文件叫做 sw.js。      
通过 service worker 我们可以代理 webview 的请求相当于是一个正向代理的线程      
在特定路径注册 service worker 后，可以拦截并处理该路径下所有的网络请求，进而实现页面资源的可编程式缓存，在弱网和无网情况下带来流畅的产品体验，      
所以 service worker 可以看做是实现pwa模式的一项技术实现。      

Service Worker是谷歌发起的实现PWA的一个关键角色，PWA是为了解决传统Web APP的缺点：      
没有桌面入口     
无法离线使用     
没有Push推送     

注意事项：
service worker 是一种JS工作线程，无法直接访问DOM, 该线程通过postMessage接口消息形式来与其控制的页面进行通信;      

service worker 广泛使用了Promise;        

目前并不是所有主流浏览器支持 service worker, 可以通过 navigator && navigator.serviceWorker 来进行特性探测;        
*苹果官方消息：iOS 11.3 与 macOS 10.13.4 将默认支持Service Workers*       

在开发过程中，可以通过 localhost 使用服务工作线程，如若上线部署，必须要通过https来访问注册服务工作线程的页面，     
但有种场景是我们的测试环境可能并不支持https，这时就要通过更改host文件将localhost指向测试环境ip来巧妙绕过该问题      
（例如：192.168.22.144 localhost）;     

生命周期：         
    
service worker的生命周期完全独立于网页，要为网站安装服务工作线程，我们需要在页面业务js代码中注册，     
浏览器从指定路径下载并解析服务工作线程脚本进而浏览器将会在后台启动安装步骤，      
在安装过程中，我们通常会缓存静态资源，如果所有文件都成功缓存，那么服务工程线程就安装完毕，      
如果任何文件下载失败或缓存失败，那么安装步骤将会失败，当然也不会被激活。安装后就进入激活步骤，这里是管理旧缓存的绝佳机会。      
激活后service worker将开始对其作用域内的所有页面实施控制。      
首次注册service worker线程的页面需要再次加载才会受其控制。在成功安装完成并处于激活状态之前，服务工程线程不会收到fetch和push事件;      

工作流程：注册-安装-激活-监听   

注册：    
Service Worker对象是在window.navigator里面：      

```
window.addEventListener("load", function() {
    console.log("Will the service worker register?");
    navigator.serviceWorker.register('/sw-3.js')
    .then(function(reg){
        console.log("Yes, it did.");
    }).catch(function(err) {
        console.log("No it didn't. This happened: ", err)
    }); 
});
```

在页面load完之后注册，注册的时候传一个js文件给它，这个js文件就是Service Worker的运行环境,如果不能成功注册的话就会抛异常，在catch里面处理。       
在load事件启动,因为要额外启动一个线程，启动之后你可能还会让它去加载资源，这些都是需要占用CPU和带宽的，      
我们应该保证页面能正常加载完，然后再启动我们的后台线程，不能与正常的页面加载产生竞争，这个在低端移动设备意义比较大。      

安装：     
注册完之后，Service Worker就会进行安装，这个时候会触发install事件，在install事件里面可以缓存一些资源，如下sw-3.js：     

```
const CACHE_NAME = "fed-cache";
this.addEventListener("install", function(event) {
    this.skipWaiting();
    console.log("install service worker");
    // 创建和打开一个缓存库
    caches.open(CACHE_NAME);
    // 首页
    let cacheResources = ["https://fed.renren.com/?launcher=true"];
    //let cacheResources = [
        //'/dist/index.html',
        //'/dist/js/index_async_bundle.js'
    //];
    event.waitUntil(
        // 请求资源并添加到缓存里面去
        caches.open(CACHE_NAME).then(cache => {
            cache.addAll(cacheResources);
        })
    );
});
```    

通过上面的操作，创建和添加了一个缓存库叫fed-cache,上面在安装Service Worker的时候就把首页的请求给缓存起来了。      
在Service Worker的运行环境里面它有一个caches的全局对象，这个是缓存的入口，还有一个常用的clients的全局对象，一个client对应一个标签页。       

激活：     
install完之后，就会触发Service Worker的active事件     
监听activate事件的回调函数中常见的任务是管理缓存，      
因为如果在安装步骤中清理了旧缓存，由于旧的服务工作线程仍旧控制着页面，将无法从缓存中提取文件，      
但是在 activate 时旧服务工作线程已经终止了页面控制权，所在在这里清理旧缓存再合适不过:           

```
// 新的service worker线程被激活（其实和离线包一样存在"二次生效"的机理）
this.addEventListener('activate', function (event) {
    console.log('service worker: run into activate');
    event.waitUntil(caches.keys().then(function (cacheNames) {
        return Promise.all(cacheNames.map(function (cacheName) {
            // 注意这里cacheVersion也可以是一个数组
            if(cacheName !== cacheVersion){
                console.log('service worker: clear cache' + cacheName);
                return caches.delete(cacheName);
            }
        }));
    }));
});
```

当刷新页面的时候虽然又调了一次注册，但并不会重新注册，它发现”sw-3.js”这个已经注册了，就不会再注册了，进而不会触发install和active事件，      
因为当前Service Worker已经是active状态了。当需要更新Service Worker时，如变成”sw-4.js”，或者改变sw-3.js的文本内容，就会重新注册，     
新的Service Worker会先install然后进入waiting状态，等到重启浏览器时，老的Service Worker就会被替换掉，新的Service Worker进入active状态，      
如果不想等到重新启动浏览器可以像上面一样在install里面调skipWaiting：     

`this.skipWaiting();`    
   
监听：   
通过监听fetch事件来代理响应，进而实现自定义前端资源缓存;      
在event.respondWith()中传入来自caches.match()的一个promise,此方法拦截请求并从服务工作线程所创建的任何缓存中查找缓存结果，      
如若发现匹配的响应则返回缓存的值，否则，将会调用fetch以代理发出网络请求，并将从网络中检索的数据作为结果返回;     
如果希望连续性缓存新的请求，则注意注释的代码部分，其通过cache.put来将请求的响应添加到缓存来实现;     
在fetch请求中添加对then()的回调，获得响应后执行检查，并clone响应，注意这样处理的原因是该响应是stream,主体只能使用一次，      
我们需要返回能被浏览器使用的响应，还要传递到缓存以供使用，因此需要克隆一份副本;     

```
// 拦截请求并响应
this.addEventListener('fetch', function (event) {
    console.log('service worker: run into fetch');
    event.respondWith(caches.match(event.request).then(function (response) {
        // 发现匹配的响应缓存
        if(response){
            console.log('service worker 匹配并读取缓存：' + event.request.url);
            return response;
        }
        console.log('没有匹配上：' + event.request.url);
        return fetch(event.request);
        /*var fetchRequest = event.request.clone();
        return fetch(fetchRequest).then(function(response){
            if(!response || response.status !== 200 || response.type !== 'basic'){
                return response;
            }
            var responseToCache = response.clone();
            caches.open(cacheVersion).then(function (cache) {
                console.log(cache);
                cache.put(fetchRequest, responseToCache);
            });
            return response;
        });*/
    }));
});
```      

项目快速接入service worker:     
service worker可以帮助我们解决资源缓存问题，有缓存就必须要有更新的机制，     
service-worker.js本身也会被浏览器缓存，后续产品迭代过程中如何解决该文件自身的更新问题，否则其他资源的缓存更新也就无从谈起      
无可厚非每次构建部署时service-worker.js需要携带版本号（例如?v=201801021721）,      
当然也可以在服务器运维层控制该文件的cache-control: no-cache从而规避浏览器缓存问题，但这样太麻烦；      

在业务代码中通过register的方式引入service-worker.js, 我们可以通过sw-register-webpack-plugin来解决该问题，     
其思路是将服务工作线程的注册放在一个单独的文件中（sw-register.js），      
然后自动在页面入口（例如index.html）写入一段JS脚本来动态加载sw-register.js文件，     
这里sw-3.js的加载路径是带有实时时间戳的，而生成的sw-3.js文件内容中注册service-worker.js的位置自动携带构建版本号参数     

```
let SwRegisterWebpackPlugin = require('sw-register-webpack-plugin')
...
plugins: [
    new SwRegisterWebpackPlugin({
        filePath: path.resolve(__dirname, '../src/sw-register.js')
    })
]
```     

处理后，sw-3.js文件就不会被浏览器缓存，也即每次刷新会多一次sw-3.js的文件请求，      
由于它只是用来做注册的工作，体量不会太大，可以接受，关键是前端可以自行控制     

已缓存资源文件更新:      
上述插件只是解决了sw-3.js文件本身的更新的问题（保证每次构建部署后会新启一个服务工作线程），     
但对于sw-3.js文件中定义的cacheFiles而言，当我们修改了已缓存文件后如何来更新缓存呢，     
我的项目是基于vue.js + webpack，打包后的JS文件是[name].[hash].[ext]格式,不可能每次构建后都手动去调整sw-3.js文件内容中cacheFiles的路径值，     
应该是将构建后的文件名（包括路径）直接放到service-worker.js内容中，     
sw-precache-webpack-plugin,该插件会自动在dist目录下生成service-worker.js文件，供给service worker运行，      
也就是说service-worker.js文件本身不需要我们手动添加了。     
自定义需要缓存的文件：     

```
new SwPrecacheWebpackPlugin({
    cacheId: 'attendance-mobile-cache',
    filename: 'service-worker.js',
    minify: true,
    dontCacheBustUrlsMatching: false,
    staticFileGlobs: [
        'dist/static/js/manifest.**.*',
        'dist/static/js/vendor.**.*',
        'dist/static/js/app.**.*'
    ],
    stripPrefix: 'dist/'
})
```
      
[使用了service worker网站例子：人人网FED博客](https://fed.renren.com/)      
[使用 Service Worker 做一个 PWA 离线网页应用](http://web.jobbole.com/92659/)       
[service worker在移动端H5项目的应用](https://segmentfault.com/a/1190000012701843)    
[使用 Service Workers](https://developer.mozilla.org/zh-CN/docs/Web/API/Service_Worker_API/Using_Service_Workers)      
     
<h2 id="27">PS</h2>          
    
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
 