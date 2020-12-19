### 1.你是否真的了解console对象？

1. console.log()
   它的使用方法类似于c、c++中的printf，它既可以这么输出```console.log(content)``` 也可以这么输出```console.log(content, content...)```
   他甚至可以使用占位符：%d 数字,%c CSS代码,%o 对象,%s 字符串...以至于它可以这样输出：
   ```js
   console.log('%s Love %s', 'I', 'You');
   > 'I Love You'
   console.log('智商:%d', 250);
   > '智商:250'
   var obj = {};
   console.log('The Object is %o', obj);
   > The obj is >{}
   console.log('我是%c你%c爸爸', 'color:white;background:10px;', '');
   > 我是 你(背景红色字体颜色白色) 爸爸
   ```
   
2. console.dir()
   于log()的区别在于显示元素时，dir是以对象的形式显示元素的，而log是HTML代码的形式显示的
   在dir显示的元素对象中可以实时的观察一个元素的各种属性以及子节点(属性)
   ```js
   var a = document.getElementByTagName('a')[0];
   console.log(a);
   > <a class="gb_ue gb_vc" aria-label="Google" href="/?tab=rr"></a>
   console.dir(a);
   > >a.gb_ue.gb_vc
   ```
   
3. console.warn()
   它打印出来的信息样式为“警告⚠”
   级别：警告(warn)
   
4. console.table() 

   令人惊讶的是这个并没有广为人知，但是 console.table() 方法更偏向于一 

   种方式展示列表形式的数据，这比只扔下原始的对象数组要更加整洁。 

   举一个例子，下面是数据的列表。 

   const transactions = [{ 

    id: "7cb1-e041b126-f3b8", 

    seller: "WAL0412", 

    buyer: "WAL3023", 

    price: 203450, 

    time: 1539688433 

   }, 

   { 

    id: "1d4c-31f8f14b-1571", 

    seller: "WAL0452", 

    buyer: "WAL3023", 

    price: 348299, 

    time: 1539688433 

   }, 

   { 

    id: "b12c-b3adf58f-809f", 

    seller: "WAL0012", 

    buyer: "WAL2025", 

    price: 59240, 

    time: 1539688433 

   }]; 

   如果使用 console.log 去列出以上信息，我们能得到一些中看不中用的输 

   出：

   \>(3) [{…}, {…}, {…}] 

   这小箭头允许你点击并会展开这个数组，但这并不是我们想要的「一目了 

   然」。 

   而 console.table(data) 的输出则对我们更为有帮助。 

   ![批注 2020-05-18 144309](../笔记图片(勿删)/批注 2020-05-18 144309.jpg)

   **第二个可选参数**是你想要显示列表的某列。默认是整个列表，但是我们也 

   能这样做。 

   \> console.table(data, ["id", "price"]); 

   <img src="../笔记图片(勿删)/批注 2020-05-18 144119.jpg" alt="批注 2020-05-18 144119" style="zoom:200%;" />

   我们得到这样的输出，仅仅只展示 id 和 price。在有着大量不相关信息的 

   庞杂对象中非常有用。index 列是自动生成的并且据我所知是不会消失。 

   值得一提的是在最右一列头部的右上角有个箭头可以颠倒次序。点击了它， 

   会排序整个列。非常方便的找出一列的最大或者最小值，或者只是得到不 

   同的数据展示形式。这个功能特性并没有做什么，只是对列的展示。但总 

   会是有用的。 

   **console.table() 只有处理最多 1000 行的数据的能力，所以它可能并不适用 于所有的数据集合。** 
5. Console.assert()
   console.assert(assertion, obj1 [, obj2, ..., objN]);
   console.assert(assertion, msg [, subst1, ..., substN]); // c-like message formatting

   参数
   assertion
   一个布尔表达式。如果assertion为假，消息将会被输出到控制台之中。为真则什么都不输出
   obj1 ... objN
   被用来输出的Javascript对象列表，最后输出的字符串是各个对象依次拼接的结果。
   msg
   一个包含零个或多个子串的Javascript字符串。
   subst1 ... substN
   各个消息作为字串的Javascript对象。这个参数可以让你能够控制输出的格式。
   ```js
   console.assert(false, 'a')
   > Assertion failed: a
   console.assert(true, 'a')
   > undefined//表达式返回的值其实是没有任何输出
   ```
6. console.group()
   概述在 Web控制台上创建一个新的分组.随后输出到控制台上的内容都会被添加一个缩进,表示该内容属于当前分组,直到调用console.groupEnd()之后,当前分组结束.
   

![批注 2020-05-18 231547](../笔记图片(勿删)/批注 2020-05-18 231547.jpg)

