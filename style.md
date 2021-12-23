#                                                    各种css样式



#### 1，css居中的几种方法

##### 1.text-align:center方式

代码：

```
.center{
　　text-align:center;
}
center_text{
　　display:inline-block;
　　width:500px
}
```

##### 2.margin:0 auto方式

```
<div class="center">
　　<span class="center_text">
    我是块级元素，我是块级元素，我给自己设了display：block
　　</span>
</div>

.center_text{
　　display:block;
　　width:500px<br>　　margin：0 auto；
}
```

##### 3.脱离文档流的居中方式。

```html
 <div class="mask">
            <div class="mask_bg"></div>   
            　　<div class="content">
                <div class="center"></div>
            　　</div>
        </div>
```

```
    .mask_bg{
        display: block;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: #000;
        filter: alpha(opacity=30);
        -ms-filter: "alpha(opacity=30)";
        opacity: .3;
        z-index: 10000;
}
.center{
    display: block;
    position: fixed;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 80%;
    height:10rem;
    margin-left: -40%;
    margin-top: -200px;
    z-index: 10001;
    box-shadow: 2px 2px 4px #A0A0A0, -2px -2px 4px #A0A0A0;
    background-color: #fff;
}
```

4.display:table-cell

```

<div class="center">
　　<div class="center_text">
　　　　1111111<br>　　</div>
</div>
```

```
.center {
　　display: table;
　　width: 100%;
}
.center_text {
　　display: table-cell;
　　text-align: center;
　　vertical-align: middle;
}
```

##### 5.垂直居中

行内元素的垂直居中把height和line-height的值设置成一样的即可。

```
<div class="center">
　　<span class="center_text">
　　　　我是要居中的内容<br>　　</span>
</div>
```

```
<div class="center">
　　<span class="center_text">
　　　　我是要居中的内容<br>　　</span>
</div>
```

##### 6.使用css3的translate水平垂直居中元素 

```
<div class="center">
　　<div class="center_text">
　　　　我是要居中的内容<br>　　</div> <br></div>
```

```
.center {
    position: relative;
    height: 500px;}
.center_text{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 300px;
    height: 600px;
}
```

这种方式将脱离文档流的元素，设置top：50%，left：50%，然后使用transform来向左向上便宜半个内元素的宽和高。

##### 7.使用css3计算的方式居中元素calc

```

<div class="center">
　　<div class="center_text">
　　　　我是要居中的内容<br>　　</div>
</div>
```

```
center {
    position: relative;
    height: 300px;
    width: 1000px;
    border: 1px solid #ccc;
}
.center_text{
    position: absolute;
    top: calc(50% - 50px);
    left: calc(50% - 150px);
    width: 300px;
    height: 100px;
    border: 1px solid #000;
}
```

#### 2.手机端初始化

```
html {
    box-sizing: border-box;
}

/*Yes, the universal selector. No, it isn't slow: https://benfrain.com/css-performance-revisited-selectors-bloat-expensive-styles/*/
* {
    /*This prevents users being able to select text. Stops long presses in iOS bringing up copy/paste UI for example. Note below we specifically switch user-select on for inputs for the sake of Safari. Bug here: https://bugs.webkit.org/show_bug.cgi?id=82692*/
    user-select: none;
    /*This gets -webkit specific prefix as it is a non W3C property*/
    -webkit-tap-highlight-color: rgba(255,255,255,0);
    /*Older Androids need this instead*/
    -webkit-tap-highlight-color: transparent;
    /* Most devs find border-box easier to reason about. However by inheriting we can mix box-sizing approaches.*/
    box-sizing: inherit;
}

*:before,
*:after {
    box-sizing: inherit;
}

/* Switching user-select on for inputs and contenteditable specifically for Safari (see bug link above)*/
input[type],
[contenteditable] {
	user-select: text;
}

body,
h1,
h2,
h3,
h4,
h5,
h6,
p {
    /*We will be adding our own margin to these elements as needed.*/
    margin: 0;
    /*You'll want to set font-size as needed.*/
    font-size: 1rem;
    /*No bold for h tags unless you want it*/
    font-weight: 400;
}

a {
    text-decoration: none;
    color: inherit;
}

/*No bold for b tags by default*/
b {
    font-weight: 400;
}

/*Prevent these elements having italics by default*/
em,
i {
    font-style: normal;
}

/*Mozilla adds a dotted outline around a tags when they receive tab focus. This removes it. Be aware this is a backwards accessibilty step!*/
a:focus {
    outline: 0;
}

input,
fieldset {
    appearance: none;
    border: 0;
    padding: 0;
    margin: 0;
    /*inputs and fieldset defaults to having a min-width equal to its content in Chrome and Firefox (https://code.google.com/p/chromium/issues/detail?id=560762), we may not want that*/
    min-width: 0;
    /*Reset the font size and family*/
    font-size: 1rem;
    font-family: inherit;
}

/* For IE, we want to remove the default cross ('X') that appears in input fields when a user starts typing - Make sure you add your own! */
input::-ms-clear {
    display: none;
}

/*This switches the default outline off when an input receives focus (really important for users tabbing through with a keyboard) so ensure you put something decent in for your input focus instead!!*/
input:focus {
    outline: 0;
}

input[type="number"] {
    /*Mozilla shows the spinner UI on number inputs unless we use this:*/
    -moz-appearance: textfield;
}

/*Removes the little spinner controls for number type inputs (WebKit browsers/forks only)*/
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
    appearance: none;
}

/*SVG defaults to inline display which I dislike*/
svg {
    display: inline-flex;
}

img {
    /*Make images behave responsively. Here they will scale up to 100% of their natural size*/
    max-width: 100%;
    /*Make images display as a block (UA default is usually inline)*/
    display: block;
}
```

#### 3，超出一行多行用点表示

**1，css超出一行用点表示**

```
white-space:nowrap;

overflow:hidden;

text-overflow:ellipsis;
```

 

**2，css超出二行用点表示**

```
overflow:hidden;

text-overflow:ellipsis;

display:-webkit-box;

-webkit-box-orient:vertical;

-webkit-line-clamp:2;
```

#### 4，css三角形生成器

http://tool.uis.cc/sjmaker/

#### 5.显示隐藏下往上，上往下显示动画

```
@keyframes scaleUp {
  0% {
    transform: scale(0.8) translateY(1000px);
    opacity: 0;
  }
  100% {
    transform: scale(1) translateY(0px);
    opacity: 1;
  }
}
@keyframes scaleDown {
  0% {
    transform: scale(1) translateY(0px);
    opacity: 1;
  }
  100% {
    transform: scale(0.8) translateY(1000px);
    opacity: 0;
  }
}
.modal {
  animation: scaleUp 0.5s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
}
.modal-out {
  animation: scaleDown 0.5s cubic-bezier(0.165, 0.84, 0.44, 1) forwards;
}
```

#### 6,树形关系图 css

```
https://www.17sucai.com/pins/demo-show?id=31940
```

#### 7，网页全屏功能

```js
        <div id="alarm-fullscreen-toggler"></div>
        <script>
// 设置全屏：目前这个方法无法监听 ESC 键盘按键
$('#alarm-fullscreen-toggler').on('click', function (e) {
	var element = document.documentElement;		// 返回 html dom 中的root 节点 <html>
	if(!$('body').hasClass('full-screen')) {
		$('body').addClass('full-screen');
		$('#alarm-fullscreen-toggler').addClass('active');
		// 判断浏览器设备类型
		if(element.requestFullscreen) {
			element.requestFullscreen();
		} else if (element.mozRequestFullScreen){	// 兼容火狐
			element.mozRequestFullScreen();
		} else if(element.webkitRequestFullscreen) {	// 兼容谷歌
			element.webkitRequestFullscreen();
		} else if (element.msRequestFullscreen) {	// 兼容IE
			element.msRequestFullscreen();
		}
	} else {			// 退出全屏
		console.log(document);
		$('body').removeClass('full-screen');
		$('#alarm-fullscreen-toggler').removeClass('active');
		//	退出全屏
		if(document.exitFullscreen) {
			document.exitFullscreen();
		} else if (document.mozCancelFullScreen) {
			document.mozCancelFullScreen();
		} else if (document.webkitCancelFullScreen) {
			document.webkitCancelFullScreen();
		} else if (document.msExitFullscreen) {
			document.msExitFullscreen();
		}
	}
});



        </script>
```

#### 8，css实现梯形

```
.badges{
    position: absolute;
    display: inline-block;
    padding: 12px 0px;
    font-size: 34px;
    color: white;
    width: 28px;
    top: -2px;
    left: -4px;
    transform: rotate(315deg);
}
.badges::before{
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background:rgb(84, 64, 8);
    transform: perspective(0.5em) rotateX(51deg);
}
```

#### 9.字体渐变

```
       font-size: 30px;
        background: linear-gradient(to left, #fca636,#f5ce1f);
        -webkit-background-clip: text;
        color: transparent;
```

#### 10.h5打包成app

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title></title>
    <script type="text/javascript">
    	
   		// document.addEventListener('plusready', function(){ 
   			//console.log("所有plus api都应该在此事件发生后调用，否则会出现plus is undefined。")
   		// }); 
   		// Window.location.href="http://jp.shuxiaoliu.cn/app/index.php?i=1&c=entry&m=ewei_shopv2&do=mobile&r=jp_home"
   
   var plusReady = function (callback) {
   			if (window.plus) {
   				callback();
   			} else {
   				document.addEventListener('plusready', callback);
   			}
   		};
    
   		plusReady(function () {
   			var firstBack = 0;
   			var handleBack = function () {
   				var currentWebview = plus.webview.currentWebview();
   				var topWebview = plus.webview.getTopWebview();
   				var now = Date.now || function () {
   					return new Date().getTime();
   				};
    
   				currentWebview.canBack(function (evt) {
   					/**  
   					 * 有可后退的历史记录，则后退。  
   					 * 否则，关闭当前窗口。  
   					 * 如果当前窗口是入口页，那么执行退出的逻辑。  
   					 */  
   					if (currentWebview.id === plus.runtime.appid) {  
   						if (!firstBack) {
   							firstBack = now();
   							plus.nativeUI.toast('再按一次退出应用');
    
   							setTimeout(function () {  
   								firstBack = 0;
   							}, 2000);
   						} else if (now() - firstBack < 2000) {
   							plus.runtime.quit();
   						}
   					} else {
   						if (evt.canBack) {
   							history.back();
   						} else {
   							currentWebview.close('auto');
   						}
   					}
   				});
   			};
    
   			plus.key.addEventListener('backbutton', handleBack);
   			plus.webview.open("http://jp.shuxiaoliu.cn/app/index.php?i=1&c=entry&m=ewei_shopv2&do=mobile&r=jp_home")
   		});
	</script> 
</head>
<body>
	
</body> 
</html>

```

#### 11.自动换行

```
word-wrap:break-word;
```

#### 12.自动换行

```
.item {
    background-color: #fff;
    width: 46%;
    padding-bottom: 10px;
    float: left;
    margin-left: 2.7%;
    margin-top: 10px;
}  
```

#### 13.等待框

```
        <div id="loading" class="loading">
                <!-- <div class="iconfont icon-loading_" id="xuanzhun" style="width: 30px; height: 30px; background-color: aquamarine;"> -->
            
       <div class="iconfont icon-loading_" id="xuanzhun" style="color: #ff0000"></div>
       <!-- <div class="loading_text">玩命加载中...</div> -->
        </div> 
        
        .loading{  
    width:80px;  
    height:80px;  
    position: fixed;  
    top: 43%;
    left: 37%;
    line-height:56px;  
    color:#fff;  
    padding-left:60px;  
    font-size:15px;  
    background: #000 ;  
    opacity: 0.5;  
    z-index:9999;  
    -moz-border-radius:5px;  
    -webkit-border-radius:5px;  
    border-radius:5px;  
    filter:progid:DXImageTransform.Microsoft.Alpha(opacity=70);  
} 

#xuanzhun{
    position: fixed;  
    top: 45%;
    left: 43%;
    font-size: 1.3rem;
 -webkit-transition-property: -webkit-transform;
    -webkit-transition-duration: 1s;
    -moz-transition-property: -moz-transform;
    -moz-transition-duration: 1s;
    -webkit-animation: rotate 3s linear infinite;
    -moz-animation: rotate 3s linear infinite;
    -o-animation: rotate 3s linear infinite;
    animation: rotate 3s linear infinite;
}
@-webkit-keyframes rotate{from{-webkit-transform: rotate(0deg)}
    to{-webkit-transform: rotate(360deg)}
}
@-moz-keyframes rotate{from{-moz-transform: rotate(0deg)}
    to{-moz-transform: rotate(359deg)}
}
@-o-keyframes rotate{from{-o-transform: rotate(0deg)}
    to{-o-transform: rotate(359deg)}
}
@keyframes rotate{from{transform: rotate(0deg)}
    to{transform: rotate(359deg)}
}

```

#### 14.点击链接标签激活

```
 $(document).ready(function(){
        $(".wz-nav-li li a").each(function(){ 
            $this = $(this);
            if($this[0].href==String(window.location)){
                $this.addClass("hover");  
            }  
        });  
    });  

```

#### 15.箭头右

```
.mui-navigate-right:after, .mui-push-right:after {
    right: 15px;
    content: '\e583';
}
mui.min.css:5
.mui-navigate-right:after, .mui-push-left:after, .mui-push-right:after {
    font-family: Muiicons;
    font-size: inherit;
    line-height: 1;
    position: absolute;
    top: 50%;
    display: inline-block;
    -webkit-transform: translateY(-50%);
    transform: translateY(-50%);
    text-decoration: none;
    color: #bbb;
    -webkit-font-smoothing: antialiased;
}
```

#### 16.输入框自适应高度

```
function readyNumber() { 

  $('#textarea').each(function () {
     this.setAttribute('style', 'height:' + (this.scrollHeight) + 'px;overflow-y:hidden;');
  }).on('input', function () {
  this.style.height = 'auto';
  this.style.height = (this.scrollHeight)-10 + 'px';
  this.style.width = 95+'%';

console.log(this.scrollHeight)
  })
}

readyNumber()

```

#### 17.常用字体

```
中文网  http://www.googlefonts.cn/
常用安全 font-family: Arial, Helvetica, sans-serif;
显示器中最清晰的字体。CSS 写法：font-family: Verdana, Geneva, sans-serif;
```

#### 18.自适应头像

```
.store_logo{
    float: left;
      width: 15%;
    padding-top: 15%;
    margin-right: 2.8%;
    border-radius: 50%;
    -webkit-border-radius: 50%;
 -moz-border-radius:50%;
    position: relative;
}

.store_logo image{

    position: absolute;
    left: 16%;
    top: 3px;
    border-radius: 50%;
    -webkit-border-radius: 50%;
    -moz-border-radius: 50%;
    width: 100%;
    height: 100%;


}

```

