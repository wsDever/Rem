## rem与em
rem与em都是样式单位，也都是相对单位。其中rem是css3新引进来的。em主为局部的字体或者高度设计的，而rem更着重于全局。

## 定义（MDN）
em：
##### 做为字体font-size时，表示父元素字体大小；
##### 做为其它属性（如height，line-height）时，代表自身字体的大小，如：

----
```
<div id="div1">
    <div id="div10">10</div>
    <div id="div11">11</div>
</div>
```
```
#div1 ｛font-size : 14px; line-height : 28px;｝
#div10 { font-size : 2em; }
#div11 { font-size : 3em ; line-height : 4em; }
```
----
rem：
##### 做为根元素是，相对于它初始的字体大小（一般是16px）；
##### 做为非根元素时，相对于根元素的字体大小;

----
```
html { font-size : 3rem ;  }
/* 作用于根元素，相对于原始大小（16px），所以html的font-size为48px*/

div { font-size : 2rem ; }
/* 作用于非根元素，相对于根元素字体大小，所以为96px */
```
----
## rem布局
##### rem布局的本质，就是基于宽度的等比缩放。
##### 对于不同的终端屏幕大小，只需要将根元素的字体大小进行改变，那么其它元素的长宽大小都会随之改变。
常见的做法就是在dom ready 、resize时将屏幕宽度平均分成100份，每一份的宽度就是
*w=屏幕宽度/100*。然后设置*1rem = w  = 屏幕宽度/100*。
```
document.documentElement.style.fontSize = document.documentElement.clientWidth / 100 + 'px';
```
##### 怎么得到设计图元素的rem值呢？既然屏幕宽度除了 100，那么取元素宽度占设计图宽度的比乘以 100，就可以得到元素真正的rem了（公式：** 元素宽度/设计图宽度 * 100 **）
##### 例如，如果设计图是 750px， 一个div的宽度是 75px，根据公式
```
div { width : 10 rem ;}  // 计算方法 75 / 750 * 100
```
由此可以得到同一张设计图在不同的屏幕下展示效果了

 屏幕宽度 | 根html字体大小（1rem） | 计算后div的宽度 
---|---|--- 
 640px | 6.4px | 10 * 6.4 = 64px 
 750px | 7.5px | 10 * 7.5 = 75px
 480px | 4.8px | 10 * 4.8 = 48px 

完。
