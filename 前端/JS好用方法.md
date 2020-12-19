### 1.保留小数点后几位

​		toFixed(3)

​		它会对小数点后面的第3位进行四舍五入

​		

### 2.获取字符串的每一位

​		charAt(0)//获取第一位字符串

​		或者直接 变量名[0]//获取第一位字符串

​		js的**字符串**底层是基于数组的

### 3.向上取整

```js
Math.ceil(123.234)//124
```

### 4.向下取整

```js
Math.floor(123.9999)//123
```

### 5.生成随机数

取不到最大值如果想取到最大值则max+1-min

```js
Math.random()*(max-min) + min
```

```js
var = Math.floor(Math.Random() * 100);
0~99
```

### 6.前16位相加可以精准，小数点后的16位精准

### **7.将对象和属性拼接：**

obj.name ---> obj['name'] 系统内部其实是这个来进行一个隐式转化的，这样我们就可以进行属性拼接也就是[]里面可以放变量这样就更灵活了

![批注 2020-03-25 145414](F:\Typora\笔记图片(勿删)\批注 2020-03-25 145414.jpg)

### 8.对象名.hasOwnProperty(属性名string)：返回这个属性是不是属于这个对象的true/false

### 9.查找这个字符串在不在这个元素内

str.indexOf(txt)

有的话返回对应下标

没有返回-1

### 10.替换这个字符串内的内容

str.replace(需要替换的字符串， 替换成什么)

### 11.写拖拽时要去掉的默认事件

一、前面的话

HTML5提供专门的拖拽与拖放的API，以后实现这类效果就不必乱折腾了。但是，考虑到Opera浏览器似乎对此不感冒，在通用性上有待商榷，所以这里也就简单说一说。

二、相关重点

- DataTransfer 对象：退拽对象用来传递的媒介，使用一般为Event.dataTransfer。

- draggable 属性：就是标签元素要设置draggable=true，否则不会有效果，例如：

  <div title="拖拽我" draggable="true">列表1</div>

- ondragstart 事件：当拖拽元素开始被拖拽的时候触发的事件，此事件作用在被拖曳元素上

- ondragenter 事件：当拖曳元素进入目标元素的时候触发的事件，此事件作用在目标元素上

- ondragover 事件：拖拽元素在目标元素上移动的时候触发的事件，此事件作用在目标元素上

- ondrop 事件：被拖拽的元素在目标元素上同时鼠标放开触发的事件，此事件作用在目标元素上

- ondragend 事件：当拖拽完成后触发的事件，此事件作用在被拖曳元素上

- Event.preventDefault() 方法：阻止默认的些事件方法等执行。在ondragover中一定要执行preventDefault()，否则ondrop事件不会被触发。另外，如果是从其他应用软件或是文件中拖东西进来，尤其是图片的时候，默认的动作是显示这个图片或是相关信息，并不是真的执行drop。此时需要用用document的ondragover事件把它直接干掉。

- Event.effectAllowed 属性：就是拖拽的效果。

```js
content.ondragenter = function (e){
    e.preventDefault();
}
content.ondragover = function (e){
    e.preventDefault();
}
content.ondrop = function (e){
    e.preventDefault();
}
content.ondragend = function (e){
    e.preventDefault();
}
content.ondragstart = function (e){
    e.preventDefault();
}

document.ondragenter = function (e){
    e.preventDefault();
}
document.ondragover = function (e){
    e.preventDefault();
}
document.ondrop = function (e){
    e.preventDefault();
}
document.ondragend = function (e){
    e.preventDefault();
}
document.ondragstart = function (e){
    e.preventDefault();
}
```

### 12.页面重新加载

window.location.reload();