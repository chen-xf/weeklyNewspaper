# 周报2

标签（空格分隔）： 周报

---
## $符号的实质

`console.log(typeof $);//function`
$其实就是一个函数，后面记得要跟小括号$()；

参数不同，功能就不同，3种用法：
参数是一个function，入口函数
`$(function(){});`
$(domobj) 把DOM对象转换成jQuery对象
`$(document).ready(function(){});`
    参数是一个字符串，用来找对象
`$("div"); $("#btn"); $(".current");`
## 1. jQuery基本操作
### 1.1 jQuery操作样式
#### 1.11 css操作
功能：设置或修改样式，操作的是style属性
**操作单个样式**
css(name,value)   name:样式名、value:样式值
**设置多个样式**
**获取样式**
css(name)        name:想要获取的样式
#### 1.12 class操作
addClass()：添加一个类
removeClass()：移除一个类
hasClass()：判断一个类存不存在
toggleClass()：切换类，先判断这个类存不存在，若存在就移除，若不存在就添加
### 1.2 jQuery操作属性
#### 1.21 attr操作
样式：在style里面写的，用css来操作
属性：在标签里面写的，用attr方法操作
#### 1.22 prop操作
对于布尔类型的属性，不要用attr方法，应该用prop()方法，prop方法用法跟attr一样
### 1.3 jQuery动画
#### 1.31 三维基本动画
显示：show(speed)   隐藏：hide speed:动画的持续时间，可以是毫秒值，还可以是固定字符串（fast：200，normal：400，slow：600）
滑入：slideDown    滑出：slideUp    切换：slideToogle
淡入：fadeIn    淡出：fadeOut    切换：fadeToggle
#### 1.32 自定义动画
animate()
第一个参数：对象，里面可以传需要动画的样式（必选）
第二个参数：speed，动画执行的时间
第三个参数：动画执行的效果
第四个参数：回调函数
动画队列：将动画连续的写就会形成一个动画队列，从上至下挨个执行
stop(clearQueue,jumpToEnd)：停止当前正在执行的动画（注：要在动画前面写）
第一个参数：是否清除队列 true/false
第二个参数：是否跳转到最终效果 true/false
### 1.4 jQuery节点操作
#### 1.41 创建节点
创建jQuery对象  
`$("<a href='http://www.baidu.com' target='_blank'>百度</a>");`
#### 1.42 添加节点
添加到子元素的最后面  appendTo()与append()效果相同，只是谁调用谁的问题，推荐使用appendTo()
添加到子元素的最前面  prepend()/prependTo()
添加到本节点的后面作为兄弟节点  after()
添加到本节点的前面作为兄弟节点  before()
#### 1.43 清空节点与删除节点
清除节点empty()
删除节点remove()
#### 1.44 克隆节点
clone(boolean)
false/不传参数而是深度复制，不会复制事件
true：也是深复制，会复制事件

---
## 2. jQuery方法、事件
### 2.1jQuery特殊属性操作
val方法、html方法与text方法、width方法与height方法、scrollTop与scrollLeft、offset方法与position方法
### 2.2 jQuery事件机制
#### 2.21on注册事件
on注册简单事件
`$(selector).on( "click", function() {});`
表示给$(selector)绑定事件，并且由自己触发，不支持动态绑定。

on注册委托事件
`$(selector).on( "click",“span”, function);`
表示给$(selector)绑定代理事件，当必须是它的内部元素span才能触发这个事件，支持动态绑定

on注册事件的语法：
`$(selector).on(events[,selector][,data],handler)`;
第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
第四个参数：handler，事件处理函数

#### 2.22事件解绑
解绑匹配元素的所有事件
`$(selector).off();`
解绑匹配元素的所有click事件
`$(selector).off("click");`
#### 2.23 触发事件
触发 click事件
`$(selector).click();`
`$(selector).trigger("click");`
#### 2.24 jQuery事件对象
*jQuery事件对象其实就是js事件对象的一个封装，处理了兼容性。*
screenX和screenY    对应屏幕最左上角的值
clientX和clientY    距离页面左上角的位置（忽视滚动条）
pageX和pageY    距离页面最顶部的左上角的位置（会计算滚动条的距离）
event.keyCode    按下的键盘代码
event.data    存储绑定事件时传递的附加数据
event.stopPropagation()    阻止事件冒泡行为
event.preventDefault()    阻止浏览器默认行为
return false:既能阻止事件冒泡，又能阻止浏览器默认行为。
### 2.3 jQuery补充
#### 2.31 链式编程
通常情况下，只有设置性操作才能把链式编程延续下去。因为获取操作的时候，会返回获取到的相应的值，无法返回 jQuery对象。
end();>>>筛选选择器会改变jQuery对象的DOM对象，想要回复到上一次的状态，并且返回匹配元素之前的状态。
#### 2.32 each方法
作用：遍历jQuery对象集合，为每个匹配的元素执行一个函数
参数一表示当前元素在所有匹配元素中的索引号
参数二表示当前元素（DOM对象）
`$(selector).each(function(index,element){});`
#### 2.33 多库共存
jQuery使用$作为标示符，但是如果与其他框架中的$冲突时，jQuery可以释放$符的控制权
释放$的控制权,并且把$的能力给了c,之后用c代替$
`var c = $.noConflict();`
在`<script src="jquery-1.12.4.js"></script>`放在其他引入库之后时使用,否则冲突时可以直接用jQuery代替$

---
## 3. 插件
### 3.1 常用插件
插件：jquery不可能包含所有的功能，可以通过插件扩展jquery的功能。
jQuery有着丰富的插件，使用这些插件能给jQuery提供一些额外的功能。

#### jquery.color.js
animate不支持颜色的渐变，但是使用了jquery.color.js后，就可以支持颜色的渐变了。

使用插件的步骤
1. 引入jQuery文件
2. 引入插件（如果有用到css的话，需要引入css）
3. 使用插件

### 3.2 jquery.lazyload.js

懒加载插件

### 3.3 jquery.ui.js插件

jQueryUI专指由jQuery官方维护的UI方向的插件。

官方API：[http://api.jqueryui.com/category/all/](http://api.jqueryui.com/category/all/)

其他教程：[jQueryUI教程](http://www.runoob.com/jqueryui/jqueryui-tutorial.html)

基本使用:
2.	1.	引入jQueryUI的样式文件
2.	引入jQuery
3.	引入jQueryUI的js文件
4.	使用jQueryUI功能

### 3.4制作jquery插件
原理：jquery插件其实说白了就是给jquery对象增加一个新的方法，让jquery对象拥有某一个功能。

通过给$.fn添加方法就能够扩展jquery对象
`$.fn. pluginName = function() {};`
手风琴案例[https://github.com/chen-xf/jQuery-case/tree/jQuery-incident](https://github.com/chen-xf/jQuery-case/tree/jQuery-incident)





