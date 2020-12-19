### 1.属性和特性

特性：天生自带的，你不设置他也是有的
    例：id,class,type,value
属性(自定义属性):自己设置的，天生不会自带的，你没写他就是没有

区别：
1. 在js中一个元素只能访问到自己的特性(也就是通过对象.的方式)，如果我们在js中对他进行赋值，那么这个特性的值也会随着更改(映射关系)
2. 属性(自定义属性)是无法获取的，获取一个没有的属性就会在其对象上新创建一个对象所以返回undefined，如果我们想设置自定义属性的话，只能通过getAttriBute/setAttriBute、或者通过```data-```开头的自定义属性可以通过setdate(遵循标准的自定属性可以通过js自带的方法获取到这个属性，并给他赋值，这样自定义属性就是和特性一样的了，同样会产生映射关系)

### 2.图片的预加载和懒加载

**预加载**
场景:当我们网速不好时，我们的图片加载会变成从上往下的一点点的显示(加载)出来，这样对用户的体验就不是很好，于是我们就有了预加载来解决这个问题

```html
<div id='a'></div>
```

```js
var img = document.createElement('img');//或者可以这么写:var img = new Image();
//在我们给图片的src赋值之前我们就给他添加一个事件：当他加载完我们再将img插入到div中，这样我们用户看到图片时就是一下子全部展示出来的了
img.onload = function (){
    a.appendChild(img);
}
img.src = 'www.baidu.com/?wd=nba&1234.jpg';//为什么不将onload事件代码写在src的后面，因为我们的js引擎执行代码是单线程的当我们给img标签添加src图片地址的时候他就会直接去拿这个图片了，有可能还没有读到我们这个onload事件的时候它就加载完了，那么我们img的onload事件就无法触发了，所以我们得先将onload事件绑定到img元素上然后当他加载完成我们这个onload事件触发我们再将img插入div中给用户一次性将图片展示出来，这就是预加载
```

**懒加载**
原理：
    1. 监控滑轮事件
    2. 不断判断当前div的位置
    3. 采取预加载
    4. 把图片正式的添加到页面当中

### 3.文档碎片提高页面效率
场景：因为我们每次向页面中进行添加元素的话，页面都需要进行一次重构，所以我们每次的性能消耗是很大的，以至于我们想要解决这个问题

解决方法：
    1. 文档碎片
    2. 字符串拼接
```js
var ul = document.getElementByTagName('ul')[0];
var htmlStr = '';
for(var i = 0; i < 10; i ++){
    htmlStr += '<li>' + i +'</li>';
}
ul.innerHTML = htmlStr;
```

### 4.加速运动

公式:v = v + at
    - t:时间(定时器)
    - v:速度
    - a:每次时间增加的速度

示例代码：
**html**
```html
<style>
div {
    width : 100px;
    height : 100px;
    position : absoult;
    left : 0;
    top : 0;
}
</style>
<div></div>
```
**js**
```js
var div = document.getElementTagName('div')[0];
var timer = null;
div.onclick = function (){
    speed(this);
}
function speed(dom){
    var a = 2;
    var initV = 20;
    clearInteval(timer);
    timer = setInteval(function (){
        dom.style.left = initV + a;
    }, 20)
}
```

### 5.匀速运动

s = vt

### 6.缓冲运动

speed = (路程 - 当前位置) / 7(任意数)

### 7.重力场

参数: g(重力加速度) speedX横向初始速度 speedY纵向滚动条 rub阻力(通常为0.8)
每次纵向(重力的方向) + g重力加速度

### 8.变速运动
v = v(速度) + a(加速度)t(时间)