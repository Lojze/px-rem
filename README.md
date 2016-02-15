# 在线px转换成rem

#这个工具是干什么的
在使用px这种单位写移动页面的时候，自适用所有浏览器
#帮你节省时间
如果你直接适用rem来写页面的话，下面就可以不用看了，这个工具是专门为懒人准备的。  
#习惯使用了px转换费时间
您只需要按照平时的px为单位写页面，媒体查询也不需要，动态的计算当前屏幕，让您写的页面自适应
#如何使用
正常按照psd的尺寸写，切图的时候直接用px，然后页面切完后，将样式丢到工具中进行转换，秒秒中就能把样式中所有px单位转成rem。

# 使用方法
```JavaScript
//页面加入一段JavaScript代码
(function (doc, win) {
    var docEl = doc.documentElement,
    resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
    recalc = function () {
        var clientWidth = docEl.clientWidth;
        if (!clientWidth) return;
        docEl.style.fontSize = 100 * (clientWidth / 320) + 'px';
    };
     if (!doc.addEventListener) return;
     win.addEventListener(resizeEvt, recalc, false);
    doc.addEventListener('DOMContentLoaded', recalc, false);
    })(document, window);
```

动态的计算显示器的宽度，存在一个移动端在pc端打开显示100%的问题，后来把js稍微修改了一下，最大宽度640px，居中显示
```javascript
// JavaScript Document
!(function(win, doc){
    function setFontSize() {
        // 获取window 宽度
        // zepto实现 $(window).width()就是这么干的
      var docEl = doc.documentElement;
   var clientWidth = docEl.clientWidth;
    if(clientWidth<=640){
         docEl.style.fontSize = 100 * (clientWidth / 640) + 'px';
	}else{
		 docEl.style.fontSize =100 +"px";
		}
    }
   resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize';
    var timer = null;
    win.addEventListener(resizeEvt, function () {
        clearTimeout(timer);
        timer = setTimeout(setFontSize, 300);
    }, false);  
    win.addEventListener("pageshow", function(e) {
        if (e.persisted) {
            clearTimeout(timer);
            timer = setTimeout(setFontSize, 300);
        }
    }, false);
    // 初始化
    setFontSize();
}(window, document));
  var trueheight=0;
  var truescroll=0;
  var docEl = document.documentElement;
   var clientWidth = docEl.clientWidth;
    if(clientWidth<=640){
       trueheight = 60 * (clientWidth / 640);
	   truescroll=100*(clientWidth / 640);
	}else{
		trueheight =60;
		truescroll=100;
		}
window.onscroll = function(){
var t = document.documentElement.scrollTop || document.body.scrollTop;
var top_div = document.getElementById( "top_tel" );
top_div.style.transition='height 500ms';
top_div.style.overflow='hidden';
if( t >= truescroll ) {
	top_div.style.height=trueheight+"px";
top_div.style.display="block";
} else {
top_div.style.height='0';
}
}
```
> * 两种解决方式，可以轮换使用
> * 有点借鸡生蛋的嫌疑，勿怪底部会附上原文地址
> * [【原文】在线转换说明](http://www.520ued.com/article/study-px-rem-tools)

### 操作流程 
1.写好的css文件放入->[放入在线转换中](http://520ued.com/tools/rem)  

2.服务器只会保存1分钟，自动销毁  

3.点击download  

4.直接替换原来的css文件就可以了  

5.因为是动态的计算网页，所以，在任何手机上都可以试用的  


> * 建议：全局使用 box-sizing: border-box，有些移动浏览器对rem不友好


[原文地址说明文档](http://www.520ued.com/article/study-px-rem-tools)  

[原文工具地址](http://520ued.com/tools/rem)  

该网址对我这种小白启发特别的大，非常感谢该作者，分享精神

