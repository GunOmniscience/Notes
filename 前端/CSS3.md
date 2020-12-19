# **CSS3**

### 预处理器

预处理器`pre-processor`

**概述：**

1. ​	在团队协作开发一个页面时，我们会有很多的CSS样式，可是在这时我们想要更改一个样式的值，可是又因为我们时团队协作的项目我们拥有特别多的CSS样式表这样我们一改值，我们就需要改很多个CSS文件的值，这样是很不方便的一个事情

   于是就有了我们的预处理器：less/sass/cssNext(插件)	cssNext插件是最为强大的，**它可以实现定义变量**，而因为这个变量的原因，我们的CSS还不能说是一个编程语言就是因为他没有变量和数据结构等等，于是CSS界大牛所说的未来CSS会变成cssNext。有可能是CSS4.0的版本

   预处理器的主要作用：

   ​	当我们在预处理器环境下编写CSS样式时，我们的预处理器有一种自己特定的语法，来方便我们写CSS：

   1. ​	比如说我们想要写一个父子关系的CSS样式：

      ​	HTML:

   ```html
   <div>
       <span></span>
       <p>
           
       </p>
   </div>
   ```

   ​			CSS:

   ```css
   div{
       background:red;
       span{
           color:white;
       }
       p{
           margin-top:10px;
       }
   }
   ```

    2. 我们可以定义一个变量：

       HTML:

       ```html
       <div>
           <span></span>
           <p>
               
           </p>
       </div>
       ```

       CSS:

       ```css
       $text-color:red;
       $block-backgroundColor:yellow;
       
       div{
           background-color:$block-backgroundColor;
           span{
               color:$text-color;
           }
           p{
               margin-top:10px;
           }
       }
       ```

       **此时我们发现我们预处理器的第二个好处做到了我们想要的效果，更改一个样式只用更改一个CSS文件的值**



### 后处理器

后处理器`post-processor`

**概述：**

​	因为我们CSS3的功能过于强大，有的功能因为技术原因，在Google的内核下才能做成，有的公司可能实现这个功能的时间过慢，而我们的大公司实现的功能过快，于是我们就会出现一下这种现象：

**现象：**

​	大公司实现快，小公司实现慢，大公司为了让我们方便认清(凸显出自己牛逼)，于是就在一个样式前面强制性的加了一个**前缀**，比如Google和Safari浏览器的**前缀**：`-webkit-`，于是我们就有了兼容性的问题，比如我们在Google的这一个版本下我们写这个样式就必需加上`-webkit-`前缀，否则这个效果显示不出来，到后面所有的公司都实现的差不多了于是我们的各大浏览器又更新了一个新版本支持不加前缀，而我们的用户有的还用老版本浏览器，可是老版本浏览器写这个样式还需要加前缀，不加前缀不行，于是我们就还要一个属性写好几个浏览器前缀的版本，这样就会导致我们的开发效率大大的降低了

​	面对这个兼容性的问题我们拥有了一些插件(例如：**autoprefixer**)用来处理我们这个兼容性的问题，简称：**后处理器**

**后处理器如何实现帮我们自动进行兼容的：**

1. 我们需要在这个后处理器插件的环境下编写CSS代码，在代码编写时我们只需按照正常编写CSS一样编写我们的CSS代码，只不过我们类似于`-webkit-border-radius:50%;`的样式，我们只需要这样写`border-radius:50%`CSS样式就好了，在我们写完CSS代码提交后我们的**后处理器`post-processor`**就会自动的根据我们CSS领域大名鼎鼎的http://caniuse.com的兼容性显示，来为我们添加**兼容其他浏览器的CSS代码**，这样我们的开发效率就得到了几何倍的增长



### 总结：

预处理器：先按照预处理器的语法去写然后生成CSS文件执行

后处理器：在后处理器的环境下，按照我们正常编写CSS去写，然后生成兼容完成的CSS文件执行



### postCSS

postCSS只是一个工具，他只做一件事，讲我们的CSS代码生成一个AST(Abstract Syntax Tree)，CSS的一个抽象语法树(用JS实现的)，剩下的事交给我们的插件去做了，**postCSS并不是一个预或后插件**

**我们的预处理器和后处理器就是基于我们postCSS生成的AST去实现自己插件的功能的(体现出来了我们postCSS的一个可拓展性)，预处理器和后处理器不可单独存在来实现功能必须搭配postCSS**

postCSS类的工具拥有200多款

**postCSS是一个我们装在webpack上的一个工具**

## 完整体系：

postCSS + 插件(cssNext、autoprefixer)



## CSS3选择器

### 1.E + F

**条件：**

​	下一个满足条件的兄弟元素节点

1. 下一个
2. 满足条件
3. 兄弟元素节点

**案例：**

HTML:

```HTML
<div>
    div
</div>
<p> <!--css-->
    1
</p>
<p>
    2
</p>
```

CSS:

```css
div + p{
    background-color:red;
}
```



### 2.E ~ F

**条件：**

​	并级的满足条件的兄弟元素节点

1. 并级
2. 满足条件

**案例：**

HTML:

```HTML
<div>div</div>
<span>span</span>
<p>1</p><!--css-->
<p>2</p><!--css-->
<p>3</p><!--css-->
<ul>
    <li>
    	<p></p>
    </li>
</ul>
```

CSS:

```css
div ~ p{
    background-color:red;
}
```



### 3.属性选择器

#### 	1.E[属性名]

​		**条件：**

​				拥有这个属性名的元素

#### 	2.E[属性名=‘属性值’]

​		**条件：**

​				拥有这个属性名并且值为这个属性值的元素

#### 	3.E[属性名~='属性值']

​		**条件：**

​				拥有这个属性名并且值内包含独立的属性值的元素

​				1.属性名一致

​				2.属性值包含独立的属性值

​				   独立的属性值：这个值左右被空格隔开

​		**案例：**

​			HTML:	

```HTML
<div data="a"></div><!--css-->
<div data="a b"></div><!--css-->
<div data="aa b c"></div>
<div data="b"></div>
```

​			CSS:

```css
div[data~='a']{
    background-color:red;
}
```



#### 4.E[属性名|='属性值']

**条件：**

​	拥有这个属性名并且属性值为属性值或者属性值以‘属性值-’开头的元素

​	1.属性值为属性值

​	2.属性值为`属性值-`开头的

**案例：**

HTML:

```html
<div class="ab">div</div>
<div class="a">div</div><!--css-->
<div class="a-bbb">div</div><!--css-->
<div class="b-test">div</div>
```

CSS:

```css
div[class|=a]{
    background-color: red;
}
```



#### 5.E[属性名^='属性值']

**条件：**

​	属性值以属性值开头的元素



#### 6.E[属性名$='属性值']

**条件：**

​	属性值以属性值结尾的元素



#### 7.E[属性名*='属性值']

**条件：**

​	属性值中包含属性值就行

存在空格也可以选中



### 4.伪元素选择器

#### 1. input::placeholder

在H5中为input框新增了一个属性placeholder来实现我们的输入提示，可是我们根据正常的选择器选择不到它里面的文本，然后去更改它的文本颜色，于是就有了这个伪元素选择器，他只能做一件事：**更改字体颜色**



因为它的兼容性特别的差，所以我们在使用这个伪元素选择器时最好加上各大浏览器的前缀：

```css
input::-webkit-placeholder{
    color:black;
}
```



#### 2. ::selection

**作用：**

​	更改我们在页面中选中文本后的文本样式



他只能设置三个值：

​	color、background-color、text-shadow

```css
div::selection{
    
}
```



### 5.伪类选择器

**某个元素的一种状态**

#### *重要的点

伪类选择器中带child但是没有带type的伪类选择器都会考虑其他类型的子元素，我们得把他们区别开来 



**例如：**

E：nth-child(n)；

HTML:

```html
<div>
    <p>
        
    </p>
    <span></span>/*color:blue*/
    <span></span>
</div>
```

CSS:

```CSS
div span:nth-child(1){
    color:red;
}
```

此时我们的样式是没法应用上的，因为我们大多数人可能会误以为含义是div下的第一个span，其实并不然，他是讲div下的p标签考虑进去的，所以实际的含义为：div下的第一个子元素且这个子元素的类型为span

于是我们如果想要给第一个span应用上样式则得这么写：

CSS:

```css
div span:nth-child(2){
    color:blue;
}
```

**通常我们常用的C3伪类选择器都是使用带type的这样我们选择的元素就不会很乱**


#### 1. E:not()

```html
<div class="test"><!--css-->
    123
</div>
<div class="demo">
    
</div>
```



```css
div:not(.demo){
    color:white;
}
```



除了有class的div：

```html
<span class="a">a</span>
<span>b</span><!--css-->
```

```css
span:not([class]){
    background-color:black;
}
```



#### 2. :root

在HTML中代表的是html标签

在别的比如说在xml里面就不是了

```css
:root{
    
}
```

**:root设置宽高%它会向它上面的document去取，document就是我们的整个浏览器的大小**



#### 3. E:target

**什么时候触发这个样式？**

​	当我们地址栏(location.hash)里的锚点为(#xx)你的id时我们这个元素应用上这个样式

**案例：**

当我们点击相对应的a标签出现相对应的div

HTML：

```html
<a href="#box1">box1</a>
<a href="#box2">box2</a>
<div id="box1">a</div>
<div id="box2">b</div>
```

CSS：

```css
div{
    display:none;
}
div:target{
    display:block;
}
```

#### 4. E:first-child

**容易产生的误区：**

​	我们会认为它选中的是一个父元素下面的第一个子元素，其实并不是，因为我们说了伪类选择器他选择的是元素的一种状态，所以我们first-child选择的是E这个元素并且E是一个父元素的第一个子元素的E。



**条件：**

1. E是一个E的父元素的第一个子元素



**案例：**

HTML:

```html
<div>
    <span></span><!--css-->
    <span></span>
</div>
```

CSS:

```css
span:first-child{
    background-color:red;
}
```

#### 5. E:last-child

与first-child的选择情况相反

#### 6. E:only-child

**条件：**

​	他没有任何的兄弟元素



**案例：**

HTML:

```HTML
<div>
    <span></span><!--css-->
</div>
```

CSS:

```css
span:only-child{
    background-color:red;
}
```



#### 7. E:nth-child():

**条件**：

1. 这个E必须是子元素
2. ()里面必须填写内容，否则无法选中	
3. 在()内填写公式时不可以敲空格



**技巧：**

1. 它可以填写公式来达到我们想要的一些效果

   例如：2n+1选择到的是奇数位置的子元素(odd)

   ​			2n选择到的是偶数位置的的子元素(even)

   > css并不是一个编程语言所以它的数数方式和我们一样从1开始，
   >
   > 可是我们这里面的**n代表的是自然数他是从0开始的**

2. 它可填的最小值为1



**案例：**

HTML:

```html
<div>
    <span>1</span><!--2n+1-->
    <span>2</span><!--2n-->
    <span>3</span><!--2n+1-->
    <span>4</span><!--2n-->
    <span>5</span><!--2n+1-->
    <span>6</span><!--2n-->
</div>
```

CSS:

```css
div span:nth-child(2n+1){//odd
    color:red;
}
div span:nth-child(2n){//even
    color:blue;
}
```

**注意：**

1. 他在进行选择时是将别的元素算入下标的

   p:nth-child(1)：子元素的第一个元素为p，如果不是则无法选中

#### 8. E:nth-last-child()

**与nth-child的区别：**

1. nth-last-child是倒着找的，nth-child是正着找的



#### 9. E: first-of-type

**条件：**

1. E这个类型的第一个元素



**注意：**

1. 他只会考虑E这个类型，并不会将别的类型带入进来筛选



#### 10. E：last-of-type

一切与last的中文意思来

#### 11. only-of-type
**条件：**

1. 这个元素是一个父级中的唯一这个类型的子元素

#### 11.E：nth-of-type(n)
**条件：**
1. E这个类型中的第几个元素

**注意：**
1. 他不会受到别的类型的影响，只在自己这个类型里面进行查找

**技巧：**

1. 它也可以填写nth-child内可以填的值：公式，2n+1，odd，even...

#### 12.E：nth-of-last-type(n)

**条件：**

​	nth-of-type是正着查，nth-of-last-type是倒着查

#### 13. :empty

**条件：**

1. 这个元素没有任何节点，**他会把注释不算做节点**



**案例：**

HTML:

```HTML
<div></div>/*color*/
<div><!--在CSS中注释不算节点--></div>/*color*/
<div>
    <a></a>
</div>
<div>
    
</div>
```

CSS:

```CSS
div:empty{
    color:red;
}
```

#### 14. :checked

**条件：**

1. 这个元素处于选中状态，我们可以使用tab进行切换选中，浏览器有默认的选中样式，不同浏览器样式不同

#### 15. :enabled

**条件：**

1. 只能选中表单元素
2. 这个表单元素不处于禁用状态

#### 16. :disabled

**条件：**

1. 只能选中表单元素

2. 这个表单元素必需处于选中状态

   表单元素可以通过属性disabled来进行禁用此元素

#### 17. :read-only

**条件：**

1. 只能选中表单元素

2. 这个元素必需处于只读状态

   表单元素可以通过属性readonly来进行只读此属性

#### 18. :read-write

**条件：**

1. 正常的状态的表单元素



**注意：**

​	这个元素被禁用了它也可以选中

## CSS3新增属性

### 1.border-radius And box-shadow

#### 1.1border-radius

**简写：**

正常的写法：

```css
border-radius: 50%;
```

复杂一点的写法：

```css
border-radius: 10px 10px 10px 10px;
```

or

```css
border-top-top-radius: 10px;
border-top-left-radius: 10px;
border-top-right-radius: 10px;
border-top-bottom-radius: 10px;
```

**其实我们的border-radius属性到这里它依然是简写状态，因为我们的border-radius是分别有两边切割的第一个是横轴方向，第二个是纵轴方向具体代码如下：**

**完全写法：**

```css
border-radius: 10px 20px 30px 40px / 50px 60px 70px 80px;
```

其中10对应50代表左上角，20对应60代表右上角，以此类推

#### 1.2box-shadow

**标准写法：**

```css
box-shadow: x偏移量 y偏移量 模糊程度 阴影拉伸 阴影颜色;
```

其中阴影拉伸的值拉伸的是宽度和高度一起拉伸

模糊程度相当于将颜色一个向外一个向内的拨开来，外面拨出去了多少里面就会拨进来多少

**box-shadow可以进行阴影重叠，其中写在前面的z值越大**

```css
box-shadow: 0px 0px 10px #fff,
			10px 0px 50px #f0f,
			-10px 0px 50px #0ff;
```

#### 1.3border-image

作用：给border区域填充图片

1. border-image-source:url("图片地址")/ linear-gradient( 渐变颜色）...

2. border-image-slice

   他代表如何切割这个图片，切割顺序为上右下左，切割出来中心的位置舍去其他的地方则显示在border区域

   它的值不能带px，只能直接填数字和填百分数，不过在这里不填px也代表像素

   ![border-img](../笔记图片(勿删)/border-img.png)

3. border-image-width

   边框图片在这个图片内占多少像素

   默认为：1也就是全部占满

4. border-image-outset

   边框图片出去多少像素

   为负值则没有任何效果

5. border-image-repeat

   边框图片的平铺区域

   值：

   ​	 **stretch** 拉伸图片来填充剩余区域

   ​	 **repeat**  重复图片来填充剩余区域不管这个图片玩不完整哪怕只够显示一个角的像素它也平铺进去

   ​	 **round** 当剩余区域无法放下这一整个图片(他平铺平铺一整张图片)则拉伸图片，如果够了则平铺这个图片

   ​	 **space** 当剩余区域不够平铺一张图片时则以空白填充剩余区域直到空间够平铺一张图片则平铺这张图片

#### 1.4border-color

如果border-color没有设置颜色的话他是会拿到字体的颜色赋给自己

**它的默认值为currentColor这个属性回去计算color的值是什么，border-color的默认值并不是等于color**

### 2.background

#### 2.1background-image

**它也可以填渐变工具**

其实我们可以填写两或多个背景图然后进行定位这样我们的一个背景就可以展示多张背景图

```css
background-image:url('图片地址'),url('图片地址')...;
```

> 这个概念是在C3中才提出来的

我们可以利用这个实现一个页面好像切换了背景图的效果(具体可以看CSS案例文件夹里的案例)

#### 2.2background-repeat

**值：**

> repeat 平铺：只要有剩余空间就平铺背景
>
> no-repeat 不平铺
>
> repeat-x x方向平铺
>
> repeat-y y方向平铺
>
> round 如果剩余区域不够平铺一张图片则拉伸图片，直到足够时再平铺
>
> space 当剩余区域不够平铺一张图片时则用空白填充，直到足够时再平铺

**技巧:**

带repeat的值只能写一个

round和space可以同时写用逗号分开，分别代表上下round，左右space：

```css
background-repeat:round, spaze;
```

#### 2.3background-origin

**作用：**

控制背景图片的左上角(起始位置)从哪里开始

**值：**

> border-box 默认值
>
> padding-box
>
> content-box

他控制的只是背景图片的起始位置(左上角)从哪里开始，它的右下角还是可以往下延伸出去的

#### 2.4background-clip

**作用：**

控制背景图片到哪个盒子就截断不显示

**值：**

> border-box 默认值
>
> padding-box
>
> content-box
>
> text **这个值只有再webkit内核下才有效果**，他让背景颜色或者背景图片显示的区域仅局限于文本区域

**我们通常用background-origin和background-clip组合起来实现效果**



**background-clip和color:transparent组合起来可以实现很好看的效果：(具体效果看CSS案例文字背景)**



**因为text这个值只有再webkit内核下才有效果所以我们使用时得加上厂商前缀-webkit-`-webkit-background-clip:text`**

#### 2.5background-size

因为C3提出了多张背景图概念所以background-size也可以设置多个值用于控制每一个背景图的大小中间只用逗号隔开

```css
background-size:100px 200px, 300px 500px;
```

#### 2.6background-attachment

**作用：**

用于控制背景图的显示状态

**背景图的显示状态：**

> scroll 相对于元素视口进行定位，当我们滚动元素区域时这个背景图不会动
>
> local 相对于元素内容进行定位，当我们滚动元素区域时这个背景也会被滚上去
>
> fixed 相对于整个浏览器的视口进行定位，当我们滚动整个浏览器窗口时这个图片也会跟着保持定位，但是**这个背景图片不会超出这个元素的区域，当超出时则溢出隐藏**

(关于fixed属性的效果具体看CSS案例中背景fixed)

#### 2.7渐变颜色

> 渐变颜色相当于是个工具，所以我们只能在带image的属性里面使用，使用渐变颜色类似于调用函数

**属性：**

1. linear-gradient():

   线性渐变

   填值顺序：[to] (角度则不用填写to，方向则需要填写to) 方向（可以填写方向或者角度）, 颜色 颜色截至区域, 颜色 颜色截至区域...

   案例：（具体案例观看CSS案例渐变颜色）

   ```css
   //角度
   background-image:linear-gradient(80deg,#f00 60px, #fff);
   //方向
   border-image:linear-gradient(to top left, #f00 60px, #fff);
   ```

2. radial-gradient()

   镜像渐变

   效果：

   ![镜像渐变](../笔记图片(勿删)/镜像渐变.PNG)

   [具体参数观看](http://css.doyoe.com/values/image/radial-gradient().htm)

3. repeating-linear-gradient()

   重复线性渐变组成背景

   效果：

   ![批注 2020-07-02 103556](../笔记图片(勿删)/批注 2020-07-02 103556.jpg)

   [具体参数观看](http://css.doyoe.com/values/image/repeating-linear-gradient().htm)

4. repeating-radial-gradient()

   重复镜像渐变组成背景

   效果：

   ![批注 2020-07-02 103726](../笔记图片(勿删)/批注 2020-07-02 103726.jpg)

   [具体参数观看](http://css.doyoe.com/values/image/repeating-radial-gradient().htm)

### 3.text-shadow

**作用：**

​	为文字添加阴影

**书写规范：**

```css
text-shadow: 左偏移量, 右偏移量, 模糊程度;
```

**注意：**

当我们通过使用-webkit-background-clip:text剪切了背景，那么其实我们的字也就成了背景，所以当我们此时添加text-shadow时我们的shadow会把我们整个字变成text-shadow的颜色，也就是我们的text-shadow就变成了字，于是我们添加上text-shadow时我们还想要看到背景的话我们得将颜色设为rgba半透明就可以看到了

### 4.@font-face

**作用：**

引用特定字体包，来展示我们想要展示的特定字符

**字体类型：**

.ttf,.eot,.woff,.svg,.otg...

浏览器通过自己内置的MIME协议去下载相对应的内容然后打开，可是我们每一个版本浏览器的MIME协议版本都不一样很有可能导致下载错误内容然后导致网页404，所以我们得使用format告诉浏览器们我们这个是什么文件，然后让浏览器去下载，不然浏览器会有可能不认识然后下载错误

**MIME:**

一种邮件传输协议，MIME内帮我们做映射，比如我们.pdf文件用哪个文件打开等等，这也是浏览器打开pdf文件的原因

**书写规范：**

```css
@font-face{
    font-family: 为我们这个字体取个类型名字;
    /*对各大版本浏览器的兼容*/
    src: url('diyfont.eot'); /* IE9+ */
	src: url('diyfont.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */
		 url('diyfont.woff') format('woff'), /* chrome、firefox */
		 url('diyfont.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/
		 url('diyfont.svg#fontname') format('svg'); /* iOS 4.1- */
}
```

**一般推荐拥有.eot,.woff,.ttf这三个字体文件，这样就能兼容大部分的浏览器了**

### 5.-webkit-text-stroke

**作用：**

给文本描边

我们可以配合simsun字体实现类似于手写字体的效果(具体效果看CSS3案例的字体描边)

**标准写法：**

```css
-webkit-text-stroke:描边像素 描边颜色;
```

### 6.white-space

**值：**

1. normal 正常
2. pre 保留我们输入的所有内容原封不动的展示到网页上

### 7.word-break

**值：**

1. normal 默认值，按照默认的换行规则进行换行
2. break-word 尽量保证一个单词的完整性去换行

### 8.columns多列

#### 8.1columns-width

**作用：**

设置每一列的宽度

**注意：**

它的宽度是会跟着父元素变化的。所以尽量不要设置宽度。而是设置列数

#### 8.2columns-count

**作用：**

设置这个元素内容的文本列数，它会平分内容的宽度然后进行分列

#### 8.3columns-gap

**作用：**

设置列于列之间的空隙

#### 8.4columns-rule

**作用：**

设置列于列之间的边框

**标准写法:**

```css
columns-rule:1px solid red;
```



#### 8.5column-span

**作用：**

设置该元素是否横跨所有列

#### 8.6column-fill

**作用：**

设置该元素内的所有列数是否高度统一

**值：**

1. auto自适应(默认)
2. balance 每一列的高度与最高一列高度保持一致

#### 8.7元素是否换行效果属性

[具体参数查看](http://css.doyoe.com/properties/multi-column/column-break-before.htm)

#### 9.box-sizing

**使用场景：**

当我们的边框或者内边距固定时，可是我们的内容区域不固定时我们使用box-sizing是最适合的

#### 10.resize

**作用：**

可以让用户自己变化dom元素的大小

**注意：**

resize属性必需搭配overflow属性才能生效，不管overflow填写的是啥都行

我们要慎重让用户更改，因为会产生重构和重绘

**值：**

1. none

2. both

   水平垂直都可以修改

3. horizontal

   水平可以修改

4. vertical

   垂直可以更改

### 9.flex

flex(弹性盒子)分为主轴和交叉轴,如果我们的主轴是横轴，那么我们的纵轴就是交叉轴。

#### 9.1设置在父级身上的属性

##### 1.将元素变成弹性盒子

1. display:flex;

   将元素设置成块级的弹性盒子

2. display:inline-flex;

   将元素设置成行级的弹性盒子

##### 2.flex-direction

设置主轴

**值：**

1. row 主轴与行内轴方向作为默认的书写模式，即横向从左到右排列(左对齐)
2. row-reverse  对齐方式与row相反。 
3. column  主轴与块轴方向作为默认的书写模式。即纵向从上往下排列（顶对齐）。 
4. column-reverse  对齐方式与column相反。 

##### 3.flex-wrap

1. nowrap 不换行，通过压缩盒子宽度来放在同一行
2. wrap 换行
3. wrap-reverse 换行并且排列方式反转变成对齐最底下

##### 4.交叉轴多行对齐align-content

> 这个弹性盒子内的内容必需是多行的否则无效

1. flex-start 与主轴的起始位置对齐
2. flex-end 与主轴的结束位置对齐
3. center 与主轴的中间位置对齐
4. space-between 两端与主轴的最两边对齐，中间平分间距
5. space-around 两端与主轴两边的间距为中间的间距的一半
6. stretch 如果子元素设置了高度那么和flex-start效果一致，如果子元素没有设置高度那么它会帮我们的高度自动拉伸填充满整个弹性盒子

##### 5.交叉轴单行对齐align-items

1. flex-start
2. flex-end
3. center
4. baseline 如果这个弹性盒子是个行内弹性盒子并且周围有行内元素那么则与基线对齐，如果没有则于flex-start一致
5. stretch

##### 6.主轴对齐justify-content

1. flex-start
2. flex-end
3. center
4. space-between
5. space-around

#### 9.2加在儿子身上的属性

##### 1.order

默认值：`0`

> 一般我们设置负值

在弹性盒子中是一个2D平面我们通过设置order用来设置元素里主轴起始位置的位置

**谁的值越小谁离主轴起始位置越近**

##### 2.align-self

它自己相对于交叉轴进行定位

**它的权重高于align-items,低于align-content,所以当我们通过align-items对弹性盒子的子元素进行定位时我们还可以通过align-self再次进行定位，不过他们的主轴位置不变，如果是通过align-content进行定位的那么我们无法再通过align-self进行重新定位**

**值:**

1. `auto`
2. flex-start
3. flex-end
4. center
5. baseline
6. stretch

##### 3.flex-grow

将自己的宽度设置成相对于父级的比例宽度

**它的权重比我们的width要高，当我们设置了flex-grow那么width无效**

**值:**整数，例如：0123...

1就代表1:1:1...

他们会按这个比例平分父级剩余的宽度

##### 4.flex-shrink

按比例相对于溢出父级的宽度进行缩减宽度

**值：**整数，例如：0123...

**缩减的计算公式：**

假设有三个子元素宽度分别为200px 200px 400px ，父级宽度为600px

前两个子元素的缩减比例为1

第三个子元素的缩减比例为3

加权值：200 * 1 + 200 * 1 + 400 * 3 = 1600

溢出宽度：(200 + 200 + 400)-600=200

前两个子元素缩减的宽度： 

200 * 1

`---------` * 200 = 25px

1600

第三个子元素缩减的宽度：

400 * 3

`-----------` * 200 = 150px

1600

**注意：**

shrink拿来计算的是子元素的真实内容宽度(content-box),不管是border-box还是标准盒子都是这么计算的

如果这个盒子里面拥有内容并且这个内容不换行那么这个盒子不参与压缩，除非把它变成自动换行的

**我们在写元素时最好都给他写上word-break:break-word;因为我们不知道后端给我们传来的数据是啥？**

##### 5.flex-basis

**值：**

设置这个元素的宽度，它会覆盖width

**注意：**

如果我们设置了basis也设置了width并且basis < width那么我们这个这个盒子的最小宽度为我们设置的basis的宽度，最大宽度为我们设置的width的宽度

如果我们设置了basis也设置了width并且basis > width那么我们这个盒子的最小宽度为basis，没有最大宽度

如果我们只设置了basis那么我们这个盒子的最小宽度为basis，没有最大宽度

**最大宽度和最小宽度是这个盒子拉伸的底线**

### 10.transition

**值：**参与过渡的属性 过渡的时间 过渡的变化曲线 等多久执行动画

```css
transition:all 2s ease-in-out 1s;
```

**技巧：**

我们可以这么设置：

```css
transition: width 2s, height 3s;
```

这样我们可以不同属性设置不同的过渡时间

### 11.@keyframes定义动画

> keyframes的兼容性不是很好所以我们尽量写上厂商前缀@-webkit-keyframes{}

**标准写法：**

```css
@keyframes 动画名{
    0%{/*动画开始时的状态*/ 0%我们可以写成from
        样式:
        left: 0;
    }
    25%{
        
    }
    50%{
        
    }
    75%{
        
    }
    100%{/*动画完成时的状态*/ 100%我们可以写成to
        
    }
}
```

**只有100%和0%有简写写法，其他的帧没有简写写法**

### 12.animation 调用动画

**标准写法：**

```css
animation: 动画名 动画时间 贝塞尔曲线(运动状态) 动画的延时时间 动画的执行次数(infinite正无穷次) 动画的运动方向 动画暂停或者开始 设置元素执行动画状态[, 设置多个动画];
```

```css
animation: animation-name animation-duration animation-timing-function animation-delay animation-iteration-count animation-direction animation-play-state animation-fill-mode;
```

**值：**

1. animation-name:

   通过@keyframes设置的动画名字

2. animation-duration

   指定动画的时常

   单位：s

3. animation-timing-function

   linear：

   线性过渡。等同于贝塞尔曲线(0.0, 0.0, 1.0, 1.0)

   ease：

   平滑过渡。等同于贝塞尔曲线(0.25, 0.1, 0.25, 1.0)

   ease-in：

   由慢到快。等同于贝塞尔曲线(0.42, 0, 1.0, 1.0)

   ease-out：

   由快到慢。等同于贝塞尔曲线(0, 0, 0.58, 1.0)

   ease-in-out：

   由慢到快再到慢。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0)

   step-start：

   等同于 steps(1, start)

   step-end：

   等同于 steps(1, end)

   steps(<integer>[, [ start | end ] ]?)：

   接受两个参数的步进函数。第一个参数必须为正整数，指定函数的步数。第二个参数取值可以是start或end，指定每一步的值发生变化的时间点。第二个参数是可选的，默认值为end。

   **我们通常写step-end加上forwards使用**

   **效果：可以做成打字效果，时钟效果，在C3案例中有**

   cubic-bezier(<number>, <number>, <number>, <number>)：

   特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内

4. animation-delay

   动画延迟时常

   单位：s

5. animation-iteration-count

   动画的循环次数(动画执行完后我们的元素会回到原来的状态)

   infinite 无限循环

   循环次数：123...

6. animation-direction

   动画执行的方向

   normal：

   正常方向

   reverse：

   反方向运行

   alternate：

   动画先正常运行再反方向运行，并持续交替运行

   alternate-reverse：

   动画先反运行再正方向运行，并持续交替运行

7. animation-play-state

   让动画暂停或开始

   running：

   运动

   paused：

   暂停

8. animation-fill-mode

   none：

   默认值。不设置对象动画之外的状态

   forwards：

   设置对象状态为动画结束时的状态

   **结束动画后保持100%时的状态**

   backwards：

   设置对象状态为动画开始时的状态

   **动画开始前等待的动画延迟时的状态为0%的状态，得搭配延迟才看得出来**

   both：

   设置对象状态为动画结束或开始的状态

   相当于结合体，在动画开始之前是0%动画结束之后是100%

### 13.transform

> 当元素旋转后它的坐标系也跟着元素旋转，所以我们旋转的先后不同旋转出来的效果也会不同

#### 13.1rotate

**作用：**

对元素进行旋转，**元素的坐标是跟着元素的，所以元素旋转时坐标轴也跟着旋转**

##### 13.1.1rotate()

将元素以中心点(transform-origin)旋转起来

##### 13.1.2rotateX()

将元素围绕x轴旋转起来

##### 13.1.3rotateY()

将元素围绕y轴旋转起来

![rotateX](../笔记图片(勿删)/rotateX.png)

##### 13.1.4rotateZ()

将元素围绕z轴旋转起来(类似于围绕圆心转风车一样)

##### 13.1.5rotate3d()

将元素围绕我们自己定义的轴旋转

正确填值：

```css
rotate3d(x, y, z, 元素围绕这个轴的旋转度数)
```

例子：

```css
rotate3d(1,1,0, 80deg)
```

![rotate3d](../笔记图片(勿删)/rotate3d.png)

![rotate3d效果](../笔记图片(勿删)/rotate3d效果.jpg)

**如果加上Z轴我们就会是一个3d的轴了**

#### 13.2transform-origin

更改这个元素的旋转中心

```css
transform-origin: 横向, 纵向;
```

默认值：

```css
transform-origin: center, center;
```

左上角：

```css
transform-origin: 0, 0;
```

#### 13.3scale

伸缩物体坐标轴以达到放大或者缩小的效果

伸缩坐标轴：

![scale](../笔记图片(勿删)/scale.png)

**他改变之后对其他的transform属性拥有影响**

**其他的transform属性改变了坐标值之后同样对scale有影响**

他是可以有3d变换的：

```css
transform: scale();
```

```css
transform: scaleX();
```

```css
transform: scaleY();
```

```css
transform: scaleZ();
```

```css
transform: scale3d();
```

**它的值没有任何单位直接填数字有点类似于百分比**

#### 13.4skew

对元素进行倾斜

**它会保持元素的宽高不变，可是我们学过几何都知道物体倾斜会更改宽高，可是我们这里并没有所以它其实更改了元素的坐标，而且这个坐标它的增长是不为整数倍的，所以如果我们需要使用到skew并且需要精确的数字时要注意skew的特点**

##### 13.4.1skewX()

变化y轴对元素进行倾斜

##### 13.4.2skewY()

变化x轴对元素进行倾斜

**因为它的坐标被倾斜了所以当我们使用拉伸的时候我们的效果就会沿着我们改变后的坐标去拉伸**

#### 13.5translate

元素按照自己原来的位置进行位移

**技巧：**

我们想要居中一个元素我们通常会使用left加上calc进行计算，可是这种方法我们需要知道元素本身的尺寸，当我们不知道元素自身的尺寸时我们如何进行居中呢？

此时我们就可以通过translate进行代替要减去的值

```css
元素{
    position:absolute;
    left: 50%;
    top: 50%;
    translateX: -50%;
    translateY: -50%;
}
```

**这样我们就可以在不确定元素尺寸的情况下对元素进行居中对齐**

##### 13.5.1translateX()

将自己按照原来的位置进行x位移

##### 13.5.2translateY()

将自己按照原来的位置进行y位移

##### 13.5.3translateZ()

将自己按照原来的位置进行z位移

##### 13.5.4translate3d()

将自己按照原来的位置进行3d组合位移

### 14.perspective

意思：景深(远大进小)(投影效果)

我们通常将他放在需要进行3d展示的元素的父级身上，相当于我们给他们的父级身上添加了一个眼睛，我们可以控制我们的眼睛离这个元素的距离，**这个距离就是perspective的值**

我们也可以将他写在transform里这样就相当于这个眼睛加在了这个元素身上

**加上眼睛的意思为我看这个元素的效果就是这个眼睛看到的效果**

**正确书写:**

```Css
perspective: 眼睛离元素的距离;
```

![perspective](../笔记图片(勿删)/perspective.jpg)

Screen就是我们的屏幕，其实我们看到的元素都是它投影到Screen上的成像，所以我们通过图中可得当我们的元素没有设置translateZ时我们更改perspective的距离看元素的没有任何变化的，因为我们的元素就在屏幕上，而当我们给我们的元素设置translateZ为负值时当我们离元素越进我们看元素越小，这是因为我们的元素是通过投影到屏幕上的，而离我们的眼睛越进它的夹角就越小所以我们的投影也就越小，而如果我们给元素设置translateZ越大时我们的元素在我们眼前越大是因为我们的元素此时是向后投影的离屏幕越远我们的元素看起来就越大所以我们设置perspective时应注意视角问题

### 15.perspective-origin

用来调整我们眼睛的左右看的

**默认值：**`50% 50%/center center`

用百分比指定透视点坐标值，相对于元素宽度。可以为负值。

**length**(我们通常使用这个来进行设置值)

用长度值指定透视点坐标值。可以为负值。

left：

指定透视点的横坐标为left

center①：

指定透视点的横坐标为center

right：

指定透视点的横坐标为right

top：

指定透视点的纵坐标为top

center②：

指定透视点的纵坐标为center

bottom：

指定透视点的纵坐标为bottom

### 16.transform-style

因为我们的元素它在页面中是一个2D平面无法模拟出3D的效果，而我们又想要3D的效果怎么办呢？此时就需要用到我们的transform-style的一个值preserve-3d，它可以自己变成一个三维的空间然后子元素只能在这个三维空间里然后我们可以设置多个子元素在这个空间内就拥有了3D的效果

**值：**

flat默认值

preserve-3d

### 17.transform-origin

设置transform的中心点，也就是xyz交叉的那个点，我们可以通过这个属性做出图片围绕一个中心旋转的效果(要设置3个值一个xyz)

**默认值：**`50% 50%/center center`

**技巧：**它其实可以设置z轴的值

### 18.GPU加速优化

当我们要进行一些拥有复杂操作的属性时我们尽量在他要开始之前使用will-change:属性名;来让浏览器新开一个层去给他进行加载，记住不要一上来就加因为他加面是会等的，知道你这个属性触发时才有的，所以我们尽量不能让他等

例如：

```css
div{
    width:100px;
    height:100px;
}
div:hover{
    will-change:transform;
}
div:active{
    transform:rotate(45deg);
}
```

**我们还可以使用csshack进行优化**

因为我们的translateZ时浏览器会将我们新建一个层出来，所以我们在使用transform进行复杂处理时我们尽量都在最后面加上一个translateZ(0)进行优化

### 19.响应式页面

#### 19.1`<meta name="viewport" content="width=device-width, initial-scale=1.0"/>`

<meta name="viewport" content="width=device-width, initial-scale=1.0"/>

**width=device-width：**将页面的尺寸设成设备的尺寸

**initial-scale：**将页面的缩放比例按1.0展示(1.0也就是不缩放，我们移动端看页面是自动会缩放的)

**width**：可视区宽度

**device-width**：设备宽度

**minimum-scale**：最小缩放比

**maximum-scale**：最大缩放比

**user-scalable**：是否允许用户缩放

**CSS像素根据设备像素进行计算1CSS像素 == 1设备像素 设备分辨率      dpi值来计算CSS像素真正展现的大小   dpi规定了我们这个设备一像素可以有多少个像素点，dpi知道一个像素点占多大位置**

1. 我们为什么要又设置width又设置initial？

   因为width=device-width在iPhone端上会出现横屏时与竖屏宽高一致的问题

   initial-scale=1.0则是在移动端上的IE浏览器会出现横屏时与竖屏宽高一致的问题

#### 19.2user-scalable=no

`<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no"/>`

我们移动端无法缩放页面(固定的死死的)

#### 13.3媒体查询

媒体查询的使用方法：

1. 在标签内部使用：

   ```html
   <link rel="css/text" href="css文件地址" media="(max-width:360px)">
   ```

   意思为当我们设备的最大宽度为360px时我们执行这一行代码，将CSS文件导入

   注意：

   我们必需加括号

2. 在CSS里使用

   ```css
   @media (max-width: 360px){
       html{
           background-color:red;
       }
   }
   ```

   意思为当我们的设备的最大宽度为360时我们的html背景颜色为红色

   注意：

   我们的@media是没有任何权重的，权重都是他内部的CSS自己的，然后按照正常的权重进行覆盖

**使用技巧：**

1. 我们可以通过**and**表示符表示并且的意思

   ```css
   @media screen and (max-width: 360px) and (min-width: 300px){
       html{
           background-color:red;
       }
   }
   ```

   意思为我们的设备是屏幕并且最大宽度为360px最小宽度为300px我们就将html的背景颜色改编成红色

2. 我们可以通过**,**来表示或者的意思

   ```css
   @media screen and (max-width: 360px), (min-width: 600px){
       
   }
   ```

   意思为我们的设备是屏幕并且我们的最大宽度为360px或者我们的最小宽度为600px我们就执行这个媒体查询

3. 我们可以通过**not**来表示非的意思

   ```css
   @media not screen and (max-width: 360px), (min-width:600px){
       
   }
   ```

   意思为当我们的设备不是屏幕并且最大宽度不为360px时或者最小宽度为min-width为600px时我们就执行这个媒体查询

   注意：

   我们的not与，会进行隔开not只会作用，前面的条件，后面的代表或者

   #### 19.3单位值

   rem：rem是css3新增的一个相对单位(root em, 根em) **相对的只是HTML根元素**

   em：em是相对长度单位。相对于当前对象内文本的字体尺寸。如当前对行内文本的字体尺寸未被人为设置，则相当于浏览器的默认字体尺寸

   px：px像素，相对长度单位，像素px是相对于显示器屏幕分辨率而言的

   vw：相对于视口的宽度，并不是设备。视口被均分为100单位的vw

   vh：相对于视口的高度。视口被均分为100单位的vh

   Vmax：相对于视口的宽度或高度中较大的那个，其中最大的那个被均分为100单位的vmax

   Vmin：相对于视口的宽度或高度中较小的那个，其中最小的那个被均分为100单位的vmin

