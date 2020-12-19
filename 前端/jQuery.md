### 1.jQuery介绍

1. jQuery2.X以上的不支持IE8
2. min(代码压缩版本)/未压缩版本
3. map方便于查看代码
4. jQuery Migrate Plugin向后兼容的版本

### 2.jQuery使用

1. 导入jQuery包(在script标签内导入jQuery包)
2. 当我们引入了jQuery包它会给我们生成一个jQuery对象，我们所使用的所有jQueryAPI都是在这个对象里的(“$”为jQuery对象的简写)

### 3.jQuery方法

#### 3.1ready()

1. 相当于window.onload(所以我们如果在head里面直接写ready方法同样可以获取到dom元素)
2. 底层是通过原生JS的```DOMContentLoadend```事件来执行的，不过```DOMContentLoadend```比ready函数早触发因为ready函数在触发前还做了很多操作，所以就比```DOMContentLoadend```慢了

与window.onload的区别：
1. ready方法是在dom元素加载完成时就执行的方法
2. window.onload是在所有资源加载完成后才执行的

第一种写法：
```js
$(document).ready(function (){
    //执行体
    var div = document.getElementsTagName('div')[0];
})
```
第二种写法：
```js
$().ready(function (){
    //执行体
    var div = document.getElementsTagName('div')[0];
})
```
第三种写法：
```js
$(function (){
    //执行体
    var div = document.getElementsTagName('div')[0];
})
```

html：
```html
<div></div>
```

jQuery简单应用：
html:
```html
<button id="btn">生成div</button>
```
js:
```js
$('#btn').click(function (){
    $('div').css({
        width : '100px',
        height : '100px',
        backgroundColor : 'red'
    }).appendTo('body');
})
```

#### 3.2html()

1. 相当于innerHTML属性

#### 3.3width()

1. 设置该元素的宽度

参数类型：Number

#### 3.4height()

1. 设置元素的高度

参数类型：Number

### 4.jQuery强大的选择器

```$('选择元素')```

> 获取出来的都是类数组(集合)，尽管它获取出来的只有一个元素，他也是一个类数组

1. 可以通过css选择器选中元素
2. #id名 .class名 [属性名]
3. 属性选择器使用：
   ```js
   $('[class=a]')//选择属性class值为a的元素
   $('[class!=a]')//选择属性class值不为a的元素
   $('[class|=a]')//选择属性class值的前缀以a-开头的元素，否则选择不到
   $('[class^=a]')//选择器属性class值以a开头的元素
   $('[class^=a]')//选择器属性class值以a结尾的元素
   $('[class*=a]')//选择器属性class值包含a的元素
   $('[class~=a]')//选择器属性class值包含a这个单词的元素，单词得用空格隔开
   $('[class=a][name=b]')//拥有class属性的值为a并且name属性的值为b的元素
   $('*')//选择所有元素
   ```

> css选择器中"~"表示选中当前元素后面的所有这个元素(必须是同级别)

过滤选择器：

1. ```js
   $('ul li:eq(1)')//ul下面的li中索引值为1的元素
   ```
2. ```js
   $('ul li:gt(1)')//ul下面的li中索引值大于1的元素
   ```
3. ```js
   $('ul li:lt(1)')//ul下面的li中索引值小于1的元素
   ```
4. ```js
   $('ul li:not(ul li:eq(1))')//ul下面的li中除了ul下li索引值为1的元素，它的括号里面可以放jQuery中所有的选择器
   ```
5. ```js
   $('ul li:even')//ul下li中的所有下标为偶数的元素
   ```
6. ```js
   $('ul li:odd')//ul下li中的所有下标为奇数的元素
   ```
7. ```js
   $('ul li:first')//ul下li中第一个元素
   ```
8. ```js
   $('ul li:last')//ul下li中最后一个元素
   ```
9. ```js
   $('ul li:lang(en)')//ul下li中拥有属性lang并且值为en的元素
   ```
10. ```js
    $('ul li:target(tar)')//ul下li中锚点为tar的元素(需页面地址的锚点为#tar)
    ```
    并且需要搭配：
    ```html
    <ul>
       <li id="tar"></li>
    </ul>
    ```
11. ```js
    $(':root')//获取根节点html
    ```
12. ```js
    $(':root')//获取根节点html
    ```
13. ```js
    $(':header')//获取所有h元素
    ```

子元素过滤器：
1. 获取ul中第一个li：(**第一个子元素必须是li标签**)
   ```js
   $('ul li:first-child')
   ```
2. 获取div中的第一个span标签:(**比第一个条件较为宽松，他指的是div中不管是不是第一个只要你有span标签就找到你第一个span标签就完事了**)
   ```js
   $('div span:first-of-type')
   ```
3. 获取ul中最后一个li：(**最后一个子元素必须是li标签**)
   ```js
   $('ul li:last-child')
   ```
4. 获取div中的最后一个span标签:(**他指的是div中不管是不是最后一个只要你有span标签就找到你最后一个span标签就完事了**)
   ```js
   $('div span:last-of-type')
   ```
5. 获取到div中的第二个子元素p标签：(**第二个子元素必须是p标签**)
   ```js
   $('div p:nth-child(2)')
   ```
6. 获取到div中的第二个子元素span标签：(**不一定第二个子元素是span他找的是span标签的第二个**)
   ```js
   $('div span:nth-of-type(2)')
   ```
7. 获取div中的唯一一个子元素span标签：(**他的子元素必须只有一个**)
   ```js
   $('div p:only-child')
   ```
8. 获取div中的唯一一个子元素span标签：(**它的可以有多个子元素但是span必须只有一个**)
   ```js
   $('div span:only-of-type')
   ```

内容过滤选择器：

1. 选择到div中的内容kai：
   ```js
   $('div:contains(kai)')
   ```
2. 选择到div中啥内容也没有的div：
   ```js
   $('div:empty')
   ```
3. 选择到div中的span标签的div：(**不管是不是子元素孙子元素也可以**)
   ```js
   $('div:has(p)')
   ```
   1. 选择到div的父级：
   
   ```js
   $('div:parent')
   ```

表单过滤器：

1. 找到所有的button：(包括button标签和input的type为button)
   ```js
   $(':button')
   ```
2. 找到input标签并且类型为checkbox的元素
   ```js
   $('input:checkbox')
   ```
3. 找到input标签类型为checkbox并且为选中状态的元素
   ```js
   $(':checked')
   ```

可见性过滤：

1. 选择所有隐藏的元素：
   ```js
   $(':hidden Selector')
   ```
2. 选择所有可见的元素：
   ```js
   $(':visible Selector')
   ```


### 5.jQuery的链式操作

原理：return this

可以多个方法一直连着调用
```js
$('div').html('郑文杰').css('color', 'red');
```

### 6.jQuery获取到的元素对象与原生JS获取到的元素对象的区别

1. jQuery获取到的元素对象为jQuery自己做的元素对象
2. 原生JS获取到的元素对象就是这个元素自己

![批注 2020-05-22 213036](../笔记图片(勿删)/批注 2020-05-22 213036.jpg)

> jQuery的所有方法只有jQuery对象能使用原生JS获取的使用不了
> jQuery的对象也无法使用原生JS的

### 7.原生JS与jQuery之间的转化

1. JS转jQuery
   ```js
   var div = document.getElementsTagName('div')[0];
   $(div).css('color', 'red');//这样我们就能使用jQuery的方法了
   ```
2. jQuery转JS
   ```js
   var $div = $('div');
   $div[0]//此时就是原生的JS元素对象了，因为jQuery虽然是函数可是他依然还是通过JS来实现的所以他的下标位其实就是原生JS的元素对象
   ```

### 8.DOM操作

关于class：

1. 给元素添加class：
   ```js
   $('p').addClass('red');//不用加.因为addClass已经表示了是class了
   ```
2. 删除元素的class：
   ```js
   $('p').removeClass('red');
   ```
   **可以不添加参数，不添加参数则消除所有class，添加指定类名表示就删除这个类名**
3. 判断一个元素是否拥有某样式名：
   ```js
   $('p').hasClass('red');
   ```
   **如果拥有则返回true，否则返回false**
4. 给一个元素切换class：
   ```js
   $('p').click(function (){
      $(this).toggleClass('red');//此时我们点击p标签它的样式会在原有的样式和red样式来回切换
   })
   ```
   **如果没有添加参数则是抹除样式和添加样式**

插入元素：

5. 内部插入，从最后一行插入元素：
   ```js
   直接写html代码：
   $('.box').append('<h2>插入成功</h2>');//讲这个h2HTML添加到.box中
   选择元素进行插入：
   $('.box').append('.box p');//此时原来.box内的p标签就被剪切到.box内了
   **与原生js的appendChild()一样**
   ```
   与他相反的插入方法:(写法相反而已，先写要插入的标签再写插入的位置)
   ```js
   $('<h2>插入成功</h2>').appendTo('.box');
   ```
6. 内部插入，从第一行插入元素：
   ```js
   $('.box').prepend('<h2>插入成功</h2>');
   ```
   与他写法相反的方法和appendTo一样：
   ```js
   $('<h2>插入成功</h2>').prependTo('.box');
   ```
7. 外部插入，插入到这个元素的下面：
   ```js
   $('.box p').after('<h2>添加到p的下一行</h2>');
   ```
   与其相反的方法：(写法相反)
   ```js
   $('<h2>添加到p的下一行</h2>').insertAfter('.box p');
   ```
8. 外部插入，插入到这个元素的前面：
   ```js
   $('.box p').before('<h2>添加到p的上一行</h2>');
   ```
   与其相反的方法：(写法相反)
   ```js
   $('<h2>添加到p的上一行</h2>').insertBefore('.box p');
   ```
9. 相当于原生JS的innerHTML：(他是一个方法可以获取内容也可以设置)
   ```js
   console.log($('.box').html());//获取.box元素的内部html
   $('.box').html('<h2>你好</h2>');//设置.box元素的内部html
   ```
10. 相当于原生JS的innerText:(他也是一个方法可以获取内容和设置)
    ```js
    console.log($('.box').text());
    ```

包裹元素：

11. 给每一个span标签外面包裹一个li标签：
    ```js
    $('span').wrap('<li>');//只需要填写<li>就好了
    ```
12. 给我们选中的所有li标签统一包裹一个ul：
    ```js
    $('li').wrapAll('<ul>');
    ```
13. 给我们选中的所有span标签里面的内容添加一个strong标签包裹起来：
    ```html
    <span>
       傻逼
    </span>
    ```
    ```js
    $('span').wrapInner('<strong>');
    ```
    ```html
    <span>
       <strong>
          傻逼
       </strong>
    </span>
    ```
    如果设置了多个则：
    ```html
    <span>
        <strong>傻逼</strong>
    </span>
    ```
    ```js
    $('span').wrapInner('<strong><em>');
    ```
    ```html
    <strong>
       <em>
        <strong>傻逼</strong>
       </em>
    </strong>
    ```

删除元素：

14. 删除自身：
    ```js
    $('span').remove();
    ```
15. 删除子元素：
    ```js
    $('ul').empty();
    ```
16. 将选中的span元素集合的父级删除：
    ```js
    $('span').unwrap();//不接收任何参数
    ```
17. 删除自身：
    ```js
    $('span').detach();
    ```
      **与remove()的区别：remove是将这个元素删了个精光，而detach则会保留这个元素得事件，他们两个都会返回这个删除的元素，当我们给这个元素绑定了一个事件时，我们remove掉了然后又将他加上这个事件就没有效果了，而如果我们时detach则这个事件依然还有效果**

元素克隆和替换：

18. 克隆一个元素：
    ```js
    $('span').clone();//浅度克隆，不会克隆这个元素的事件啥的
    $('span').clone(true);//深度克隆，将这个元素的所有信息全部克隆过来
    ```
19. 我替换一个元素：
    ```js
    创建元素替换：
    $('<h2>你好我是来替换你的</h2>').replaceAll('span');//这样span标签就没了它就被我们创建的h2标签给替换掉了
    
    已有元素替换：
    $('p').replaceAll('span');//将我们页面中的p标签替换掉我们页面中的span标签，此时我们的span标签就没了相当于剪切了一样
    ```
20. 谁替换我：
    ```js
    $('span').replaceWith('<h2>你好我是来替换你的</h2>');
    ```

属性操作-通用属性操作：

21. 获取属性内容并设置属性内容：
    获取属性内容：
    ```js
    console.log($('img').attr('src'));//获取图片的src属性内容
    ```
    **获取只获取到第一个img的src内容**

    设置属性内容：
    ```js
    $('img').attr('title', '这是一张正经的图片');
    ```
    **设置的时候会将所有的img都加上title属性并且值为我们设置的值**
    
    他和css函数一样可以进行多值配置：
    ```js
    $('img').attr({
       width : '100px',
       alt : '正经的图片'
    })
    ```

    和attr一样的prop他们之间的区别：
    1. prop获取的img的src1地址为绝对地址，而attr获取到的是相对地址也就是我们写的是啥她获取出来就是啥
       ```js
       console.log($('img').prop('src'));
       > img/1.jpg
       ```
    2. attr可以获取标签身上的自定义属性，而prop无法获取标签圣上的自定义属性：
       ```js
       console.log($('img').attr('jie'), $('img').prop('jie'));
       > jiejiejie undefined
       ```
    3. attr设置的属性啥都能设置并且都会添加到标签内，而prop设置的属性自定义属性无法添加到标签上，而是只能添加到dom对象上
22. 删除一个属性：
    ```js
    $('img').removeAttr('kai');
    $('img').removeProp('id');//他删的不是标签上的，而是dom对象上的
    ```
23. 获取或设置表单元素的value属性：
    ```js
    console.log($('input').val());//获取到input标签的value属性的值
    $('input').val('这是一个正经的输入框');//此时的input的value值为这是一个正经的输入框
    ```

属性操作-css类属性操作

24. 获取和设置css样式：
    ```js
    console.log($('div').css('border'));//他获取到的是计算后的值
    ```
25. 宽度：
    ```js
    console.log($('div').width());//内容区域的宽度
    console.log($('div').innerWidth());//内边距盒的宽度
    console.log($('div').outerWidth());//边框盒的宽度
    $('div').innerWidth(200)//设置内边距的宽度，它会不更改你的内边距，然后将200-去内边距剩下的值赋给div的内容宽度
    padding(保持我们设置的不变) + contentWidth(将outerWidth的值减掉border和padding得出来的值) = outerWidth(我们设置的outerWidth)
    $('div').outerWidth(300);//设置边框盒它会不更改边框和内边距将我们设置的宽度减去边框和内边距的宽度然后就是我们的width了
    border(保持我们设置的不变) + padding(保持我们设置的不变) + contentWidth(将outerWidth的值减掉border和padding得出来的值) = outerWidth(我们设置的outerWidth)
    ```
26. 位置信息：
    相对于document的定位：(他只有left和top)
    html:
    ```html
    <div class="css">
       <div></div>
    </div>
    ```
    获取定位：
    js：
    ```js
    $('.css div').offset().left;
    $('.css div').offset().top;
    ```
    设置定位：
    ```js
    $('.css div').offset({
       left : 100,
       top : 1000,//他父级如果有定位的话他是先将document到父级的位置算出来然后再算这个元素相对于这个父级的定位，然后再将这个算出来的定位赋给这个div
    })
    ```
    相对于拥有定位的父级的定位：
    ```js
    console.log($('.css div').position().top)
    console.log($('.css div').position().left)
    ```
27. 滚动条信息：
    ```js
    $(document).scrollTop();//获取document的滚动条高度
    $(document).scrollLeft();//获取document的滚动条的横向度

    设置：
    $(document).scrollTop(1000);
    $(document).scrollLeft(200);
    ```

### 9.遍历

获取后代元素：

1. 获取**直系后代**元素:
```js
$('ul').children();//选中了ul下面的所有子元素不包含孙子元素
```
children可以添加一个选择器参数，用于过滤：
```js
$('ul').children(':eq(1)');//这样就过滤出了ul下面下标为1的li，其他的就不要了
```
2. 获取**所有后代**元素：
```js
$('ul').find();
```
```js
$('ul').find('span');
```

获取祖先元素：

3. 获取**直系父级**元素：
```js
$('ul li').parent();//获取出来是ul
```
parent还可以传一个选择器：
```js
$('ul li').parent('div');//此时li的直系父级不为div所有它就没有选择到任何元素
```
4. 获取**所有父级**元素：
```js
$('div ul li').parents();//此时li上面的所有父级都给选出来了，ul和div和body和html
```
他一样可以传参来过滤获取到的父级：
```js
$('div ul li').parents('ul');//此时就只获取到了ul标签
```
5. *获取**直到什么元素以内的所有父级**：
```js
$('div li ul li').parentsUntil('li');//此时获取到的只有ul,它的意思是我找到父级li就往上走了，然后返回li下面的相对于我们这个元素的父级
```
6. 获取离自己最近的有定位的祖先元素：
此时我们的ul和li都有定位:
```js
$('div li ul li').offsetParent();//获取到的是ul
```
**如果都没有则获取到的是html**
7. 获取祖先元素包括自己：
```js
$('div li ul li').closest('li')//此时获取到的是li自己，因为它的父级包括自己
```

获取后面的兄弟元素：

8. 获取自己后面的第一个兄弟元素：
span下面一个兄弟元素为div：
```js
$('div span').next();//获取到的就是div
```
**如果传参了并且它后面的第一个兄弟元素并不是这个参数选择器的类型则获取不到任何东西**
9. 获取自己后面的所有兄弟元素：
```html
<div>
   <span></span>
   <div></div>
   <div>
      <span></span>
   </div>
</div>
```
```js
$('div span').nextAll();//此时我们获取到了span后面的所有兄弟元素那两个div
```
10. 获取我们参数选择器之前的相对于我们这个元素的所有兄弟元素：
```html
<div>
   <span></span>
   <div></div>
   <p></p>
   <i></i>
</div>
```
```js
$('div span').nextUntil('i');//获取到div，p标签
```

获取前面的兄弟元素：

11. 和next相对的：
```js
$('div span').prev();
```
12. 和nextAll相对的：
```js
$('div span').prevAll();
```
13. 和nextUntil相对的：
```js
$('div span').prevUntil();
```

获取所有的兄弟元素：(不分前后)

14. 获取所有的兄弟元素部分前后：
```html
<div>
   <p></p>
   <a></a>
   <div></div>
   <span></span>
   <div></div>
</div>
```
```js
$('div span').siblings();//获取到p，a，div，div
```
我们还可以传参来过滤获取到的元素集合：
```js
$('div span').siblings('div');//此时获取到了两个div
```

### 10.事件

#### 10.1绑定事件

**原生事件，通过事件名添加的事件：**

1. 鼠标移入
```js
$('div').onmouseover();
```
2. 鼠标移出
```js
$('div').onmouseover().onmouseout();//我们可以进行一个链式操作就特别的方便
```

**通过on添加的事件：**
```js
$('选择器').on('事件名',[ '触发这个事件的后代元素的选择器'(如果有后代元素的话，类似于事件委托，如果我们添加了这个参数则此时的this指向的是这个后代元素), {color : 'red'}(这里我们可以传递一些数据给我们绑定的这个事件函数，如果添加了这个参数对象则我们的事件函数得接收一个参数event，然后我们这个对象是放在event的data这个对象里面的),] function ([如果我们添加了第三个参数对象我们需要添加这么一个参数来接收这个传进来的对象，然后我们在函数内部就可以使用了]){})
```
例如：
html：
```html
<div>
   <h2>点击我触发事件</h2>
   <p>点击我不会触发事件</p>
</div>
```
js:
```js
$('div').on('click', 'h2', {color : 'red'}, function (event){
   //this指向h2
   $(this).css({
      color : event.data.color,
   })
})
```
**on可以绑定多个事件：**
```js
$('div').on({
   事件名1:function (){},
   事件名2:function (){}
})
```
例如：
html:
```html
<button>我是一个按钮</button>
```
js:
```js
$('button').on('click', function (){
   $(this).css('backgroundColor', 'blue');
})
$('button').on({
   mouseover : function (){
      $(this).css('backgroundColor', 'pink');
   },
   mouseout : function (){
      $(this).css('backgroundColor', 'yellow');
   }
})
```
**此时我们就给button绑定了三个事件click，mouseover，mouseout，当我们触发时它会产生相对应得操作**

**通过one绑定事件:**

> 通过one绑定的事件只触发一次即被取消

它的参数和on一样

#### 10.2取消事件：

off()：
```js
$('div').off();//没传参则取消所有事件
$('div').off('mouseover');//只取消mouseover事件
```

#### 10.3手动触发事件：

**```trigger('事件名')```**
```js
$('div').trigger('click');//当读到这段代码则执行div的click事件，我不需要去点击就可以手动触发
```

如果我们的事件函数拥有参数：
```js
$('div').on({
   onmouseout : function (event, name, age){
      console.log(name + ' : ' + age);
   }
})
$('div').trigger('onmouseout', ['郑文杰'(对应name), 18(对应age)](这个数组类似于apply一样));

> 郑文杰 : 18
```

我们还可以自定义事件，因为自定义事件js是无法直到你什么时候触发的，所以你只有自己通过trigger()来触发

```js
$('div').on({
   onmouseout : function (event, name, age){
      console.log(name + ' : ' + age);
   },
   end : function (){
      console.log('触发自定义事件')
   }
})
$('div').trigger('end')
```

**```triggerHandler()```**

trigger()和triggerHandler()的区别：

1. trigger触发事件会触发默认事件，triggerHandler触发事件不会触发默认事件
```html
<input type="text">
<button>使文本框聚焦并会触发默认事件</button>
<button>使文本框聚焦并不会触发默认事件</button>
```
```js
$('button:eq(1)').click(function (){
   $('input').trigger('focus');//当点击时光标会跑到文本框内
})
$('button:eq(2)').click(function (){
   $('input').triggerHandler('focus');//当点击时光标不会跑到文本框内
})
```
2. trigger会执行所有选中元素的事件，triggerHandler只会执行所选中的所有元素中的第一个
3. trigger会冒泡，triggerHandler不会冒泡
4.trigger可以进行链式操作，triggerHandler不可以进行链式操作
```js
$('div').trigger('click').trigger('mouseover');
```

#### 10.4事件对象
```js
$('div').click(function (e){
   console.log(e);//返回jq自己的事件对象
})
```
**具体内容查看jQuery中文文档**

### 11.特效

#### 11.1显示隐藏特效
```html
<button>隐藏div</button>
<button>显示div</button>
<button>隐藏/显示切换div</button>
<div>操作目标</div>
```

1. 隐藏
```js
$('button:eq(0)').click(function (){
   $('div').hide();
})
```
传参动画：
- 快一点('fast'):
```js
$('div').hide('fast');
```
- 标准('nomal'):
```js
$('div').hide('nomal');
```
- 慢一点('slow'):
```js
$('div').hide('slow');
```
- 动画毫秒数:
```js
$('div').hide(4000);//此时隐藏动画将在4秒完成
```
- 添加回调函数(在动画结束时执行):
```js
$('div').hide(4000, function (){
   console.log('动画完成了')
});
```


2. 显示
```js
$('button:eq(0)').click(function (){
   $('div').show();
})
```
**参数与hide一致**


3. 隐藏/显示切换
```js
$('button:eq(0)').click(function (){
   $('div').toggle();
})
```
**参数与hide，show一致，不过他不管是显示还是隐藏他都会触发回调函数**

#### 11.2滑动特效

1. 向上滑动隐藏('slideUp'):
```js
$('div').slideUp();//它默认为'nomal'
```
**参数和显示隐藏一致**

2. 向下滑动显示('slideDown'):
```js
$('div').slideDown();//它默认为'nomal'
```
**参数和显示隐藏一致**

3. 上下滑动切换('slideToggle'):
```js
$('div').slideToggle();
```
**参数一致**

#### 11.3渐变特效

1. 淡出隐藏(fadeOut):
```js
$('div').fadeOut();//默认nomal
```
**参数一致**
2. 淡入显示(fadeIn):
```js
$('div').fadeIn();//默认nomal
```
**参数一致**
3. 淡入淡出切换(fadeToggle):
```js
$('div').fadeToggle();//默认nomal
```
**参数一致**
4.淡入透明度(fadeTo):
```js
$('div').fadeTo('nomal', 0.5, function (){})
```
**它的参数拥有变化：第一个填速度，第二个填变化到的透明度值**

#### 11.4自定义动画

1. animate():

参数：{配置(1.可以添加toggle值，表示从0到当前值来回切换 2.可以添加字符串'+=50'表示每次点击当前的值+50)}, 和隐藏那些一致(通常使用数值), 回调函数(运动完成时执行)
```{width:200(将宽度变化到200), height:toggle}, 1000(一秒内执行完), function (){}```

animate可以进行链式操作：
```js
$('div').animate({width : 'toggle'}, 500).animate({height : 'toggle'}, 500);//执行完第一个animate然后再执行第二个animate
```

2. 暂停当前动画(stop):
```js
$('button').click(function (){
   $('div').stop();
})
```

3. 完成当前动画(finish):
```js
$('button').click(function (){
   $('div').finish();
})
```

4.停顿动画(delay):
**让后面的动画停顿1秒后在执行**
```js
$('div').delay(1000).animate({
   width : 'toggle'
})
```

### 12.Ajax

使用get还是post请求根据后端要求，否则会报错

1.get请求：

```js
$.get('请求的网络地址', {请求的账户}(发送给网络地址的数据，网络地址通过这些数据给我们想要的数据), 回调函数(data(如果请求成功则接收数据)){

}, '请求过来的数据想要变成的文件类型(json,xml,html,script)')
```
例如：
```js
$('button').click(function (){
   $.get('http://api.duyiedu.com/api/student/findAll', {appkey : 'kaivon_1574822824764'}, function (data){
      console.log(data);
   }, 'json')
})
```
**jQuery封装的Ajax方法都是可以跨域请求的**
**跨域：不同站点请求数据**

2. jQuery的Ajax方法:

```js
$.ajax({
   url : '请求地址',
   type : '请求数据方式get/post',
   data : { 发送给请求端的数据，请求端通过我们的数据来给我们想要的数据
      appkey : 'kaivon_1574822824764'
   },
   dataType : 'json', 请求回来的数据类型
   success : function (data){请求成功后的回调函数
      console.log(data);
   }
})
```


例如：
```js
$.ajax({
   url : 'http://api.duyiedu.com/api/student/findAll',
   type : 'get',
   data : {
      appkey : 'kaivon_1574822824764'
   },(也可以这样写：data : 'appkey=kaivon_1574822824764')
   dataType : 'json',
   success : function (data){
      console.log(data);
   }
})
```

**我们还可以添加一个对象error:function (stuats){}用于捕获错误信息**

3. post请求：
```html
<input type='text' name='userName'>
<input type="password" name='userPsw'>
```
```js
var name = $('input[name=userName]').val();
var psw = $('input[name=userPsw]').val();
$.post('http://api.duyiedu.com/api/student/findAll', {appkey : 'kaivon_1574822824764', name : name, psw : psw}, function (data){
   console.log(data);
}, 'json');
```

4.JSONP请求：

**为什么交JSONP因为他可以跨域**

原理：
通过script标签将数据引入进来然后再通过一个方法进行处理就实现了跨域

```js
$.getJSON('http://api.duyiedu.com/api/student/findAll', {appkey : 'kaivon_1574822824764'}, function (data){
   console.log(data);
})
```

**不需要传获取文件类型因为他本身就是getJSON了，所以获取出来一定就是JSON**

### 13.jQuery插件

jQuery插件站点：
https://plugins.jquery.com/
http://www.jq22.com/
https://alvarotrigo.com/fullPage/zh/
https://github.com/alvarotrigofullPagejs/tree/master/langchinese#fullpagejs

**使用jQuery插件必需要先导入jQuery包因为他是jQuery插件所以他是依赖jQuery包的**

### 14.自定义插件

> 1.在jQuery对象上添加方法 $.xxx()
> 2.在jQuery DOM对象上添加方法 $('h2').xxx()
> jQuery为我们写了添加函数的函数

1. 使用extend方法为jQuery对象添加函数：
```js
$.extend({
   函数名 : function ([函数参数]){
      执行操作
   }
})
```
例如：
```js
$.extend({
   iii (){
      cosole.log('执行成功');
      return $(this);
   }
})
console.log($.add(1, 2));//3
```

1. 给jQuery DOM对象添加函数：
```js
$.fn.extend({
   函数名 : function ([函数参数]){
      执行操作
      return $(this);
   }
})
```

**给DOM对象添加时我们通过$(this)获取到这个DOM对象**
例如：
```js
$.fn.extend({
   con (){
      console.log($(this));
      return $(this);
   }
})
$('div').con();//jQuery [.....]
```

我们还可以这么为jQuery DOM添加函数：
```js
$.fn.函数名 = function (){
   
}
```

**我们自定义的方法也通常要return $(this),为了jQuery的链式操作**