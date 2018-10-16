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
 