# Bootstrap

bootstrap的JS是依赖于jQuery的所以在我们bootstrap中的js文件上面我们得自己引入我们自备的jQuery文件

## **1.标准的bootstrap框架**

![批注 2020-08-05 101305](../笔记图片(勿删)/批注 2020-08-05 101305.png)

shrink-to-fit=no：用来适配iPhone9，iPhone9改了适配属性名

## **2.响应式所具有的特点：**

1. 网页的宽度自动调整
2. 尽量少用绝对宽度
3. 字体通常使用rem，rem的r代表root也就是html标签的字体大小，然后我们通过让html的字体大小自适应那么我们的内容的字体大小也就适应了
4. 布局要使用浮动，弹性布局，浮动我们通常可以实现一行显示多少个的效果

## **3.@规则**

1. @chartset	定义编码
2. @import      引入css文件(实现css模块化)
3. @font-face  自定义字体
4. @keyframes animation里的关键帧
5. @media       媒体查询

## **4.媒体查询 **

**根据一个或多个基于设备类型，具体特点和环境来应用样式**

**css文件中：**

```css
@media 媒体类型 媒体规则{
    css代码
}满足就会运行
```

**link标签中：**

```html
<link rel="text/css" href="./css/index.css" media="媒体类型"/>当我们的媒体查询满足我们的这个link标签的样式才会运行
```

**@import中:**

```css
@import url(./css/index.css)(media 媒体类型 媒体规则)满足时才执行导入
```



1. **媒体类型**

   all	所有设备

   print	打印机设备

   screen	彩色的电脑屏幕

   speech	听觉设备(针对视力障碍的人设计的，可将页面以语音的形式展示出来)

   **注意：tty，tv，projection，handheld，embossed，aural等几种类型在媒体查询4中被废除**

2. **媒体特性**：写在括号里 @media (媒体特性)

   width	宽度

   ​	min-width 宽度只能大于这个(意思是我们这个页面的最小宽度为这个，所以我们必需大于它)

   ```css
   @media (min-width:500px){/*当我们的宽度大于500px的时候满足，当小于500时这个样式就会应用不上了*/
       div {
           background-color:red;
       }
   }
   ```

   ​	max-width 宽度只能小于这个(意思是我们这个页面的最大宽度为这个，所以我们不能超过它)

   ```css
   @media (min-width:400px){/*当我们的宽度小于400px时满足则应用这个样式*/
       div{
           background-color:red;
       }
   }
   ```

   height	高度

   ​	min-height 高度只能大于这个(意思是我们这个页面的最小高度为这个，所以我们必需大于它)

   ​	max-height 高度只能小于这个(意思是我们这个页面的最大高度为这个，所以我们不能超过它)

   orientation	方向

   ​	landscape	横屏（宽度大于高度，计算机的理解)

   ```css
   @media (orientation:landscape){//当我们的宽度大于高度(横屏)的时候我们应用这个样式
       div{
           width:400px;
       }
   }
   ```

   ​	portrait	竖屏（高度大于宽度，计算机的理解)

   ```css
   @media (orientation:portrait){//当我们的高度大于宽度(竖屏)的时候我们应用这个样式
       div{
           height:400px;
       }
   }
   ```

   aspect-ratio	宽度比

   ```css
   @media (aspect-ratio:4/3){//4/3代表4:3，当我们的宽高满足这个比例时我们应用这个样式
       div{
           height:400px;
       }
   }
   ```

   -webkit-device-pixel-ratio	像素比(webkit内核的私有属性)

   ```css
   @media (-webkit-device-pixel-ratio:2){//一般手机的像素比都是2，当我们满足时我们应用这个样式
       div{
           height:400px;
       }
   }
   ```

   

3. **逻辑运算符**   用来做条件判断

   | `and`  |          合并多个媒体查询（并且的意思&&）          |
   | :----: | :------------------------------------------------: |
   |  `,`   |            匹配多个媒体查询（或者的意思            |
   | `not`  |              对媒体查询的结果**取反**              |
   | `only` | 仅在媒体查询匹配成功后应用样式（防范老旧浏览器的） |

   **一个括号里面只能写一条媒体规则**

   and

   ```css
   @media all and (min-width:700px) and (orientation:landscape){//all给不给都无所谓是默认的，当我们的所有媒体规则都满足时应用这个样式
       div{
           width:200px;
           height:300px;
           background-color:red;
       }
   }
   ```

   ,

   ```css
   @media (max-width:700px),(orientation:landscape){//任何满足一个媒体规则都可以应用这个样式
       div{
           width:200px;
           height:300px;
           background-color:red;
       }
   }
   ```

   not

   ```css
   @media not all and (max-width:800px){//当我们的媒体规则不满足是我们not进行取反然后应用上了这个样式
       div{
           background-color:pink;
       }
   }
   ```

   only

   ```css
   @media only screen and (min-width:800px){//旧版本浏览器不认识@media则会进行直接解析里面的样式可是我们不想要这样做，当他不认识的时候你别管我的@media就好了，这时我们就得加一个only来让他这样做了
       div{
           background-color:red;
       } 
   }
   ```

   

## 5.栅格化系统

![批注 2020-08-16 093750](../笔记图片(勿删)/批注 2020-08-16 093750.png)

1. `<div class="container-fluid"></div>`

   宽度为100%，它会相对于父级进行取值，然后像html进行取值，像用户设备进行取值

2. `<div class="container"></div>`

   宽度为一个固定的值，他是会根据不同的设备进行改变的值

   **拥有导航条居中效果**

   **如果写导航栏的话可以使用.container-fluid嵌套.container进行排版，并且.container是会进行响应式的**

3. `<div class="row"></div>`

   代表栅格系统的行，一行最多容纳12行否则换行

4. `<div class="col-**-**"></div>`

   ![批注 2020-08-16 091844](../笔记图片(勿删)/批注 2020-08-16 091844.png)

   类似于.col-xl-数字，这样的代表列然后数字代表你占多少列，一行就只能有12列，如果我们一个列的类名为.col-xl-2那么这一列就占了两列，还剩10列

   **Max container width**代表当小于这个宽度时我们的列的宽度就会变成100%，竖列排列下来可以实现我们的点击按钮展开菜单效果，当我们小于所对应的宽度时我们一行只能显示一个也就是每一列的宽度都是100%

   **# of columns**代表一行可以占多少个列

   **Gutter width**边距(沟)宽度：例如这里的30px就是左右内边距各15px

   **Nestable**是否可以进行列嵌套列

   **Column ordering**表示这个盒子是可以进行排序的

   **它会通过响应式进行自动调整**

   **其他的列类名当小于宽度时一行就只能占一个列，而我们的Extra small当我们小于宽度时还是大于宽度时他永远都可以展示12列**

   **当我们越大的值满足了那么我们的覆层宽度就会变成越大的那个值得宽度，它设置的是覆层的宽度并不是单元格**

   

5. 案例

   ```html
   <div class="container-fluid">
           <div class="container">
               <div class="row">
                   <div class="col-xl-1">第1列</div> <!-- 后面的数字代表这一列占多少列类型于表格的列合并 -->
                   <div class="col-xl-1">第2列</div>
                   <div class="col-xl-1">第3列</div>
                   <div class="col-xl-1">第4列</div>
                   <div class="col-xl-1">第5列</div>
                   <div class="col-xl-1">第6列</div>
                   <div class="col-xl-1">第7列</div>
                   <div class="col-xl-1">第8列</div>
                   <div class="col-xl-1">第9列</div>
                   <div class="col-xl-1">第10列</div>
                   <div class="col-xl-1">第11列</div>
                   <div class="col-xl-1">第12列</div>
               </div>
           </div>
   </div>
   ```

   

**栅格系统类似于我们的表格，div.container-fluid==table，div.row==tr，div.xxx==td**

bs通过栅格系统将我们的页面的宽度分成12份，也就是说最多只有十二个td在一行内，当有13个时会换行

在bs4中我们的栅格系统用的是flexbox，在bs3中我们的栅格系统用的是float



**等宽列**`.col`

​	这个列会平分这一行的宽度

![批注 2020-08-6 111337](../笔记图片(勿删)/批注 2020-08-6 111337.png)![批注 2020-08-16 111337](../笔记图片(勿删)/批注 2020-08-16 111337.png)

如果我们想让他不够12行也换行那么我们给想要换行的列后面加个DIV类名为w-100这样我们的上面的列一样会自动均分宽度，我们下面的列也一样会自动均分下面的宽度，它的原理是：width:100%

```html
<div class="row">
    <div class="col">
        
    </div>
    <div class="col">
        
    </div>
    <div class="w-100">
        
    </div>
    <div class="col">
        
    </div>
    <div class="col">
        
    </div>
</div>
```

![批注 2020-08-16 165239](../笔记图片(勿删)/批注 2020-08-16 165239.png)

### 设置根据内容调整整列宽度

**我们会发现一个问题：**我们的所有的width都是固定的，例如说占两格，或者自适应等等...都是一些固定的宽度，尽管我们设置了宽度，或者说内容的宽度已经超过的盒子的宽度，可是我们的盒子依然不会发生宽度变化，而是我们的内容进行一个换行展示，可是我们不想要换行我们想要**又有栅格系统的100%特性他的宽度又可以随着我们的内容自适应**，于是就有了我们的下面这个class：

`.col-栅格系统的关键词(例如：sm,xl,lg)-auto`

那么我们的这个栅格系统盒子的宽度就是随着我们的内容进行一个自适应的了，我们所有栅格系统盒子的属性都还依然在身上。

### 设置所有尺寸下都只占我们设置的几格尺寸

因为我们的.col它的宽度会进行一个自适应剩余宽度，可是我们有时候不想让他进行一个自适应宽度我们想要他占固定的几格的一个宽度，并且所有尺寸下他都是占这几个的一个宽度，于是就有了下面这个class

`.col-占几格`

### 响应式页面内容展示

例如：此时我们有6个div，在超大屏的时候我们显示6个div在一行，在大屏的时候我们显示3个div在两行，在中屏的时候我们显示2个div在3行，在小屏的时候我们显示1个div在6行，我们想要这种真正的响应式效果怎么写呢？

```html
<div class="container-fluid">
        <div class="row">
            <div class="col-xl-2 col-lg-4 col-md-6 col-sm-12 br"></div>
            <div class="col-xl-2 col-lg-4 col-md-6 col-sm-12 br"></div>
            <div class="col-xl-2 col-lg-4 col-md-6 col-sm-12 br"></div>
            <div class="col-xl-2 col-lg-4 col-md-6 col-sm-12 br"></div>
            <div class="col-xl-2 col-lg-4 col-md-6 col-sm-12 br"></div>
            <div class="col-xl-2 col-lg-4 col-md-6 col-sm-12 br"></div>
        </div>
    </div>
```

我们可以直接对齐进行设置多个栅格系统响应层的样式，当我们前面的不满足了就则展示后面的样式了

### Bs4弹性盒特有的行内(.row)垂直对齐对齐方式

例如：当我们的.row的高度有足够的空间时，我们会发现我们的内容顶在最上面的，那么我们能不能改呢？于是就有了我们下面的这个属性：

align-items-start顶对齐

align-items-center中对齐

align-items-end底对齐

**这是写在.row上的样式**，当我们加上这些样式，我们这一行内的所有列都会根据我们设置的对齐方式进行一个对齐

**这是弹性盒模型有的属性才能做的到的效果，可是我们的Bs3使用的是流式布局，所以无法做到**

**另一个问题**

例如：我们在一行内我们有的元素想要进行顶对齐，有的元素想要进行中对齐，有的元素想要进行底对齐，那这怎么做呢？，于是就有了我们的下面这些属性:

align-self-start顶对齐

align-self-center中对齐

align-self-end底对齐

**这些事写在.col上的样式**，当我们加上这些样式时，我们引用了这些样式的列就会在这个行内进行相对应的对齐

### Bs4弹性盒特有的行内(.row)水平对齐对齐方式

1.justify-content-start水平居左

2.justify-content-center水平居中

3.justify-content-end水平居右

4.justify-content-around水平平分间距排列

5.justify-content-between水平两端对齐

**这些事加在.row上面的样式**

### 更改列在列中的排序

例如：`.order-数字`，这个数字越大排列越再后面，一行正确的排列是1234556...当我们给我们的列(.col)加上order-数字，数字越大越排在后面。

`.order-栅格(xl,sm,lg...)-数字`当我们满足这个栅格时我们的这个大小才会应用上这个样式，当我们不满足这个栅格时我们的这个属性就会失效

`.order-first`将我们这一列排在最前面

`.order-last`将我们这一列排在最后面

### 列偏移

`offset-{breakpoint}-数字`将这一列进行向右偏移几格，我们**这一列后面的列也会被挤过去**

### 间距

ml-{pointbreak}-auto将这个列的margin-left自动计算将这一列移到最右边

mr-{pointbreak}-auto将这个列的margin-right自动计算这一列移到最左边

**我们这列左边或者右边的列同样会被挤过去**

## 6.嵌套

每一个列里面可以再继续放行，那嵌套在里面的元素就会以父级的宽度为基准，再分12列

```html
<div class=".col">
    <div class=".row">
        <div class=".col">
            
        </div>
    </div>
</div>
```

## 7.重置

bootstrap4中的一些重置样式

### 7.1table

`.table`对table标签进行一个样式重置

`.talbe-bordered`给table添加一个1px的灰色边框

### 7.2:root

![批注 2020-09-01 205203](../笔记图片(勿删)/批注 2020-09-01 205203.png)

我们在**根节点伪类选择器:root**中会看到很多类似于**--值**，的这种**属性**，其实它是一个**变量**，使用我们的**nextcss**实现的，这些**变量都是bootstrap官方给我们预设好的**，那么我们要使用的话，该**如何使用呢？**

```css
a{
    color:var(--orange);
}
```

使用css属性值中的var()方法这样我们就能取到--orange这个变量的值，然后赋给我们的a标签中的color属性

