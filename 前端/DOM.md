**document是一个对象，代表整个文档，它相当于在html标签外面包了一个标签**

**JS之后一切系统中给我们返回一堆的东西它都是类数组**

**就算返回这个元素只有一个你想指定返回其中一个元素你就得用类数组下标选取**

### 1.查找元素

除了ID以外任何选择元素的方式都是一组

#### 	1.1通过ID名查找	

​		因为**ID只能有一个**，所以它**返回的不是类数组**

​		在**IE8**以下**不区分大小写**，并且如果**没有ID名的话**。**name名代表ID名**

```js
docment.getElementById('id名');
```

#### 	1.2通过标签名查找

​		会把document中**所有**的这个标签名的标签**都选中**，它获取的是一个**类数组**，所以我们想**精准到一个元素**，那么我们就在**后面加下标**就好了

```js
document.getElementsByTagName('标签名')[类数组下标];
```

#### 	1.3通过class名查找

​		**在IE8和IE8以下的IE版本**中没有这个方法并且不可多个class同时作用

```js
document.getElementsByClass('class名')[数组下标];
```

#### 	1.4通过name名查找

​		**老版本浏览器**name只有在**ifrme，表单，表单元素，img才能有效**

​		**新版本都可以用**

```js
documnt.getElementsByName('name名')[数组下标];
```

#### 	1.5通过css选择器查找

​		IE7和IE7以下没有这个方法，它并不是实时的它拿的是副本，也就是像我们照相的一样，假如你人没了可是你的照片里还在，所以我们**一般情况不用他**

​		它识别的就是CSS选择器，所以你怎么写css选择器它都能给你查找出来

```js
document.querySelector('div > span strong');
```

##### 		1.5.1通过css选择器查找出一组

​			它返回的是一组，所以如果你想要精准的一个那么你得通过下标

```js
document.querySelectorAll('div > span strong')[0];
```

### 2.节点树

#### 2.0遍历节点数

##### 	2.1 parentNode

​		**父节点 (最顶端的parentNode为#document，#document的上面为null);**

​		**一个元素只有一个父级**

```html
<div>
    <strong></strong>
</div>
```

```js
var strong = document.getElementsTagName('strong')[0];
cosole.log(strong.parentNode);//<div></div>
```

##### 	2.2 childNodes -> 子节点们	

他不会穿过子元素标签去把子元素里面的子元素们算进去

他算的是直系子元素

```html
<div>
    123
    <!--这是注释-->
    <strong></strong>
    <span></span>
</div>
```

```Js
var div = document.getElementsByTagName('div')[0];
var ziJieDian = div.childNodes;
console.log(div.childNodes);//总共有7个子节点
```

###### 			2.2.1如何区分节点

​				*<div>*~
​				    *123*
​				    ~这里为一个节点~*<!--这是注释-->*~这里为一个节点~
​				    ~这里为一个节点~*<strong></strong>*~这里为一个节点~
​				    ~这里为一个节点~*<span></span>*~这里为一个节点~
​				~这里为一个节点</div>

##### 	2.3第一个和最后一个子节点

```html
<div>
    123
    <span></span>
</div>
```

###### 		2.3.1第一个子节点

```js
var fist = document.getElementsByTagName('div')[0].firstChild;
```

###### 		2.3.2最后一个子节点

```js
var last = document.getElementsByTagName('div')[0].lastChild;
```

##### 	2.4后一个，前一个兄弟节点

```html
<div>
    <strong></strong>
    <span></span>
</div>
```

###### 		2.4.1nextSibling后一个兄弟节点

```js
var next = document.getElementsByTagName('strong')[0].nextSibling;//<span></span>
```

###### 		2.4.2previousSibling前一个兄弟节点

```js
var previous = document.getElementsByTagName('span')[0].previousSibling;//<strong></strong>
```

#### 2.5基于元素的遍历节点树

##### 	2.6parentElement->返回当前元素的父元素节点(IE不兼容)

​		html标签上面是null，因为他是基于元素的

##### 	2.7children->只返回当前元素的元素子节点

##### 	2.8查看子节点元素个数(IE不兼容)

​		节点元素.childElementCount === 子节点元素.children.length(推荐用这个，比较好记)

##### 	2.9第一个和第最后一个元素节点(IE不兼容)

###### 		2.9.1第一个节点

​			元素节点.firstElemntChild

###### 		2.9.2最后一个元素子节点

​			元素节点.lastElementChild

##### 	2.10后一个或前一个兄弟元素

###### 		2.10.1后一个兄弟元素

​			元素节点.nextElementSibling

###### 		2.10.2前一个兄弟元素

​			元素节点.previousElementSibling

### 3.节点的四个属性

#### 	3.1nodeName

​		元素的标签名，以大写形式表示，只读

​		比如strong标签的nodeName为"STRONG"

#### 	3.2nodeValue

​		Text(文本)节点和Comment(注释)节点的文本内容，可读写

#### 	3.3nodeType

​	该节点的类型，**只读**，返回的是数值，对应下面的节点类型

##### 		3.3.1节点的类型

​			元素节点——1

​			属性节点——2

​			文本节点——3

​			注释节点——8

​		document——9

​		DocumentFragment——11

#####  3.4attributes

​			Element节点的属性集合

​			返回的是类数组

![批注 2020-03-30 214636](F:\Typora\笔记图片(勿删)\批注 2020-03-30 214636.jpg)

​		**getAttribute("属性名")：**

​			返回这个属性的值

### 4.每一个节点都有一个方法

有没有子节点：包括文本分隔符文本

属性是自身的不是子节点

Node.hasChildNodes();

返回值：true/false

### 5.DOM结构树

![批注 2020-03-31 130926](F:\Typora\笔记图片(勿删)\批注 2020-03-31 130926.jpg)

### 6.DOM结构树的基本操作

![批注 2020-03-31 141031](F:\Typora\笔记图片(勿删)\批注 2020-03-31 141031.jpg)

### 7.DOM的增，插，删，替换

![批注 2020-03-31 153824](F:\Typora\笔记图片(勿删)\批注 2020-03-31 153824.jpg)

#### 增

#### 7.1document.createElement('');

创建元素节点

#### 7.2document.createTextNode('');

创建文本节点

#### 7.3document.createComment('');

创建注释节点

#### 7.4document.createDocumentFragment();

#### 插

#### 7.5appendChild()

它的插入是剪切，你插入了一个地方不能再插入另一个地方

它可以通过一个元素.的方式调用，谁调用它谁是父级

#### 7.6父级元素.insertBefore(a, b);

应该这么读父级元素里面的a  ，   insert  a  before    b

a标签在b前面

#### 删

#### 7.8父级.removeChild(子级)  谋杀式

其实他是把这个子级标签剪切出来了，剪切出来的东西可以拿一个变量接收

#### 7.9自杀式 自身.remove()

它不是剪切它没有了就真的没有了

####  替换

#### 7.10parent.replaceChild(new, origin);

用new的替换origin的，他是被剪切出来了 

### 8.Element属性和方法

![批注 2020-03-31 164101](F:\Typora\笔记图片(勿删)\批注 2020-03-31 164101.jpg)

#### 8.1元素.innerText(很老版本火狐不兼容)

它会去这个元素里边的文本内容，它会突破子元素把子元素里的文本内容也拿出来

innerText赋值的时候会把原本的元素及任何东西都给覆盖

#### 8.2textContent和innerText一样(IE老版本不兼容)

#### 8.3给元素设置属性名和属性值setAttribute('属性名','属性值')

#### 8.4取属性值getAttribute('属性名')

### 9.0日期

#### var date = new Date()

#### 它是时刻并不是动态的时间

#### 9.1Date()返回当日的日期和时间

#### 9.2getDate()从Date对象返回一个月中的某一天(1~31)

#### *9.3getDay()从Date对象返回一周中的某一天(0~6)

#### *9.4getMonth()从Date对象返回月份(0~11).

#### 9.5getFullYear()从Date对象以四位数返回年份

#### 9.6getHours()返回Date对象的小时(0~23)

#### 9.7getMinutes()返回Date对象的分钟(0~59)

#### 9.8getSeconds()返回Date对象的秒数(0~59)

#### 9.9getMilliseconds()返回Date对象的毫秒(0~999)

#### 9.10getTime()返回1970年1月1号至今的毫秒数

#### 9.11可以通过set时间来当*定时抢购*一样的东西使，它设置的是我们当时new这个Date的时刻

可以用我们设置的那个时间的getTime，和我们当时的的getTime的误差小于1000毫秒我们就响起来啊什么的

### 10.定时器(都是window上面的方法)

#### 10.1setInterval()搁多久时间执行一次

参数一函数，第二个参数填毫秒数1000毫秒等于1秒

你通过变量来改变秒数是不好使的，它读你的时间一次

他是window的方法

**每一个setInterval会返回一个数字作为他的唯一标识，我们像清楚它就得接收他的唯一标识，然后清除**

或者你直接写它的唯一标识哈哈哈哈

#### 10.2clearInterval(存有唯一标识的变量)

#### 10.3setTimeout()搁多少时间执行，执行完就不执行了

参数一执行操作，参数二延时时间

#### 10.4clearTimeout()

他们的唯一标识不会冲突

#### 10.5如果参数一里面填字符串它也可以执行字符串里面的代码

```js
setInterval('console.log("a")', 1000);
```

### 11.计算DOM尺寸以及滚动条位置

#### 11.1查看滚动条的滚动距离

 这些属性是只读的。 

window. **page*X*Offset/page*Y*Offset**

IE8/IE8以下不兼容



IE8/IE8以下用：document. *body/documentElement.* **scroll*Left*/scroll*Top***

**他们两个方法是冲突的**，也就是有一个方法有值有一个方法它就一定没有值，那么得去别的浏览器也许才能有值了

**最好的方法就是他的  横向或者纵向 距离我们相加就好了**

#### 11.2可视区窗口尺寸

window.innerWidth/innerHeight

IE8/IE8以下不兼容



IE8/IE8以下用：document.documentElement.clientWidth/clientHeight

混杂模式时:       document.body.clientWidth/clientHeight

标准模式下，任意浏览器都兼容

标准模式:加上<!DOCTYPE html>

删了就是**怪异模式/混杂模式**

混杂模式：向后兼容



##### 11.2.1如何查看当前模式

document.compatMode

返回:CSS1Compat  标准模式

​		 BackCompat  混杂模式

### 12.查看元素的几何尺寸

.getBoundingClientRect()

几乎返回了一切位置和宽高信息

返回的是他的padding和内容的和

![批注 2020-04-02 165316](F:\Typora\笔记图片(勿删)\批注 2020-04-02 165316.jpg)

只设置了left和top

bottom和right的值是left和top到他的方块上面的所对应的点的距离

在IE里面没有**宽和高**

我们想要在IE里面求宽和高我们就用right - left 和 bottom - top

![批注 2020-04-02 165656](F:\Typora\笔记图片(勿删)\批注 2020-04-02 165656.jpg)

***查看元素的尺寸**

dom.offsetWidth, dom.offsetHeight

返回的是他的padding和内容,border的和

***查看元素的位置**

dom.offsetLeft, dom.offsetTop

他不管自身，**返回的是他距离有定位的父级的距离**

他的这个值会加上自身的border和没有去掉的body自带的margin ： 8px而如果纵向的则因为margin塌陷变没了

横向的margin能相加，纵向的不行

position的默认值是**static**

### 13.返回最近的有定位的父级

dom.offsetParent

**返回最近的有定位的父级**，如无，返回body，body.offsetP

父级都没有的话就是body了

### 14.让滚动条滚动

window上有三个方法

scroll(),scrollTo()   scrollBy();

三个方法功能类似，用法都是将x,y坐标传入。即实现让滚动轮滚动到当前位置

区别：scrollBy()会在之前的数据基础上做**累加**

### 15.脚本化CSS

**行间样式表：**

不在行间写的样式设置不了也获取不了

没有兼容性问题

如果碰到float这种**关键字**，我们得再前面加**小写css**，然后加上关键字

复合属性建议分开写，也可以合起来写

写入的值必须是字符串的

元素.style可以返回一个类数组，里面包含了大部分可以设置的CSS属性，我们**设置相对应的值页面会有相对应的渲染**



**获取元素样式：**

IE8/IE8以下不兼容

window.getComputedStyle(ele, *null*)；

> *它的**null的值**是用来获取**伪元素**的样式表的，也就是，ele你填元素，然后null的位置填"after"/"before"，然后.样式属性，就能获取这伪元素的的样式的值了，**不过它写不进去**
>
> 如果向设置伪元素的样式，我们通常用改变CSS名字来实现，因为我可以有两个css属性同时选向伪元素



**样式只读不可以写入**

他这个方法的类数组显示的是默认值和你权重最大的那个值

**它获取元素的样式是按照权重来的，所以相对style，window.getComputedStyle(ele, *null*)；更准一些**

**它返回的是绝对值：如果你填了一个1em这种相对值它会给你返回计算后的值**



**IE8/IE8以下用：**

div.currentStyle

他返回的样式不是计算后的值

IE独有的属性

### 16.事件

**obj.addEventListener(type, fn, *false*);**

type:事件类型，**不写on直接写事件click**

**它可以写多个没并且这多个会按照你写的顺序去执行，而你如果写的是onclick那样的，下面的就会覆盖上面的**

**他不能重复绑定一个函数，那么只会执行一次这个函数**

IE9/IE9以下不兼容



IE9/IE9以下：

**obj.attachEvent('onclick'，处理函数)；**

**它如果重复绑定一个函数，他能重复执行这个函数**

***它不管怎么调用它的this指向得就是window***

### 17.解除事件程序

![批注 2020-04-03 183405](F:\Typora\笔记图片(勿删)\批注 2020-04-03 183405.jpg)

ele.removeEventListener / ele.detachEvent('on' + type, fn)(想要解除得事件名，想要接触得函数，*false*)

**它得事件名和想要解除的函数必须得是一致的**



![批注 2020-04-03 183753](F:\Typora\笔记图片(勿删)\批注 2020-04-03 183753.jpg)

如果我们写的函数是这样的**匿名的**，那么我们就**永远都无法取消**了



### 18.事件处理模型

![批注 2020-04-03 185237](F:\Typora\笔记图片(勿删)\批注 2020-04-03 185237.jpg)

**事件冒泡：**

​	父子级**结构**(结构上，不是视觉上)的元素嵌套关系，如果点击子元素，它的事件会向父级冒泡反应，也就是它子元素触发的事件会给父级，所以叫冒泡

**事件捕获：**

​	只有Googlechrome有

​	定义：一个元素要么就是冒泡，要么就是捕获，不能同时存在

​	作用：他和冒泡反着来，先父级后子级

​	如何将一个元素变成捕获：

​			将addEventListener的flase改为true

​			得加载父级上面才有效果，加在子级一样是冒泡

![批注 2020-04-03 222828](F:\Typora\笔记图片(勿删)\批注 2020-04-03 222828.jpg)

***有两种事件捕获：***

*第二种是只有**IE里面才有的**，ele.setCapture(),第一种就是我们上面讲的事件捕获了*

开启了他，它会把页面中所有的事件都给到这个元素身上

用完了最好就得取消因为对其他元素是有影响的：

ele.releaseCapture();



**一个元素又有冒泡又有捕获：**

先捕获后冒泡

如果先写的冒泡，那么只是这个元素在这个元素的捕获前面，其他的父级，还是捕获后冒泡



**并不是所有事件都能冒泡**

**冒泡是事件天生就有的**

### 19.如何取消冒泡和阻止默认事件

![批注 2020-04-03 225838](F:\Typora\笔记图片(勿删)\批注 2020-04-03 225838.jpg)

**取消冒泡：**

![批注 2020-04-03 231654](F:\Typora\笔记图片(勿删)\批注 2020-04-03 231654.jpg)

​	event.stopPropagation(): W3C标准

​		在事件函数上填一个函数，js会自动给我们传进来一个对象，这个对象包含了，我们此时的鼠标坐标啊，事件啊啥的都有，我们用这个**对象**.stopPropagation();这样我们就能把这个元素的**冒泡**给去了

​	event.cancelBubble = true; IE独有 谷歌也有

​	**不能停止捕获事件**

**阻止默认事件:**

​	document.oncontextmenu 右键出菜单事件

阻止右键出菜单栏： 句柄式

​	document.onconttextmenu = function (){

​		return false;

​	}

如果不是用句柄的方式，那么我们用obj.preventDefault(): W3C标准

​	document.oncontextmenu = function (e){

​		console.log('a');

​		e.preventDefault();

}

​	IE:

​			e.returnValue = false;



取消点击a标签滚动条回到顶部的功能

a.onclick = function (){

​	return false;

}

***最好写：**

<a href="javascript:void()"></a>

### 20.事件对象

```html
<div style="width:100px;height:100px;background:red;"></div>
```

```js
var div = document.getElementsByTagName('div')[0];
div.onclick = function (e){//在IE浏览器里面他不会给你返回e这个对象，他的对象是在window.event里面
    var event = e || window.event;//所以我们想要获取这个对象我们得写一个兼容
}
```



#### 	20.1事件原对象：

​		当我们点击子对象，他的事件冒泡到父级然后触发了父级的事件，返回的对象里面它的指向是子对象(事件原对象)，如果点击的只是父级的话，那么这个对象指向的就是你的父级这个元素

![批注 2020-04-04 103255](F:\Typora\笔记图片(勿删)\批注 2020-04-04 103255.jpg)



**获取事件原对象：**

​	event.target  火狐只有这个

​	event.srcElement IE只有这个

​	这两个chrome都有



#### 20.2事件委托

![批注 2020-04-04 104420](F:\Typora\笔记图片(勿删)\批注 2020-04-04 104420.jpg)

![批注 2020-04-04 104606](F:\Typora\笔记图片(勿删)\批注 2020-04-04 104606.jpg)



### 21.鼠标事件

#### 	21.1点击

​		click = mousedown + mouseup

​		不能区分左右键，DOM3标准：他只能识别左键

#### 	21.2按下

​		mousedown

​		可以区分鼠标左右键：		

```js
document.onmousedown = function (e){
    console.log(e);//他这个对象事件里面的button：
    				//0：左键 1：滚轮 2：右键
}
```

​		移动端：

​			touchstart

#### 	21.3放开

​		mouseup

​		可以区分鼠标左右键：

```js
document.onmousedown = function (e){
    console.log(e);//他这个对象事件里面的button：
    				//0：左键 1：滚轮 2：右键
}
```

​	移动端：

​		touchend

#### 	21.4移动

​		mousemove

​	移动端:

​		touchmove

#### 	21.5右键产生菜单

​		contextmenu

#### 	21.6移入

​		onmouseover/onmouseenter

#### 	21.7移出

​		onmouseout/onmouseleave



### 22.键盘类事件

​	keydown > keypress > keyup

​		执行优先自左向右

​	键盘类事件，按着会一直触发

​	

​	keydown与keypress的区别：

​		keydown可以响应**所有键盘类(除了Fn)**按键的事件，它有一个which属性，给键盘每一个按键排了序号然后来显示which的，所以我们大小写它的which一样，所以虽然keydown也能判断，不过他不向keypress那么精准，所以看个人需求了

​		**keypress可以通过charCode里面的ACSII码来区别**你按的什么键，不过**比如说shift，ctrl，↑↓←→等类似的键触发不了keypress,也就是ASCII码里面没有的按键他出发不了**

​		我们还可以通过它返回的ASCAII码把它又转成字符：

```js
String.fromCharCode(e.charCode);
```

### 23.文本类操作事件

#### 		23.1一个元素里面的文本发生变化就会触发的事件

​		oninput

#### 	23.2鼠标聚焦发生了内容改变然后放开就会触发

​		onchange

#### 	23.3鼠标聚焦时触发

​		onfocus

#### 	23.4鼠标取消聚焦时触发

​		onblur

### 24.窗体类事件(window上的事件)

#### 	24.1当滚动条滚动

​		onscroll

​			小知识：IE6没有flex绝对定位，我们可以用这个事件来做绝对定位

#### 	24.2当页面所有自动加载的东西都做完了他才触发

​			效率是最差的因为他要等很久，很占用资源

​		onload