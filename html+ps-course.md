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
    
## html5优化实践    
   
### 使用history改善AJAX列表请求体验：    
    
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
   
### 使用图标字体iconfont代替雪碧图：      
   
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
可能刚好就是某一个繁体字的编码。导致了刷新页面的时候先是繁体之后变成图标的问题。ios和电脑的浏览器上是先显示一个方框，等字体      
加载好了在变成正常图标。         
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
   
使用的时候通过外链jiangsvg引入，通过文件名id的方式：     

```
<svg viewBox="0 0 100 100">
	<use xlink:href="icon.svg#logo"></use>
</svg>
```   

ie不支持外链，可以通过插件[SVG for Everybody](https://github.com/jonathantneal/svg4everybody)让ie支持。     
highCharts和d3js也使用了SVG           
     
###实现前端剪裁压缩图片：     
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
    var reader = newFileReader(file);
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
vardata=img.src;
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

### Service Worker做一个PWA离线网页应用：     

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
 