[toc]

[ES指定语言标准，不涉及语言的运行环境，正是因为ES避免了运行环境，就让ES有机会在各种环境中执行，ES成为了通用编程语言]()  

[通常把ES运行的环境称为，宿主环境]()

[ES在ES6开始以年份来标准命名，例如我们的ES6是2017年发出来的]()

[所有的输出语句都不是ES标准]()

[输入语句也不是ES标准]()

### 1.数据类型

- 基本数据类型
  1. 数组类型 number
  
     了解：
  
     ​	数字类型可以加上前缀，表示不同的进制
  
     ​	0：表示8进制
  
     ​	0x：表示16进制
  
     ​	0b：表示2进制
  
  2. 字符串类型 string
  
     单引号：''  不可换行
  
     双引号：""  不可换行
  
     esc下面的：`` 叫做模板字符串     可换行写内容
  
     ```js
     var str = `
     你好
     `;
     ```
  
  3. 布尔类型 boolean
  
  
  4. undefined 类型
  
  5. null 类型 (历史遗留问题为：引用类型)
  
- 引用数据类型

  1. 对象 object
  2. 函数 function

### 2.字面量

> 直接书写的具体的数据，叫做**字面量**

### 3.声明提升

> 在HTML文件中，一个script中的声明提升不会超出这个script标签

[当只为undefined，null时读它的属性则它会报错]()

[属性不可能是数字，如果是数字，它会把它改变为字符串]()

[我们定义的所有变量都是window对象中的属性]()

[如果变量没有被赋值，则该变量不会覆盖window对象上的同名属性]()

例如：我们定义了一个变量name，可是我们的window对象也有name属性，并且值是一个空串，如果我们没有给这个那么重新赋值的话它就还是一个空串(**window对象中的name属性不管怎么赋值他都会变成一个字符串**)



### 4.运算符

一元运算符：()  *   []

二元运算符：+ -  / * % =

三元运算符：？：

- 数学运算符
  1. `+ - * /`
  2. `+ -`
  3. `%`
  4. `++ --`
  5. `**` 幂 例如： 5**2 == 25

**在不是数字类型的前面加个 + 号，他就会给他转化成数字类型**



### 5.自动类型转化

1. 数字运算是不精确的

2. 除数为0

如果被除数是正数，得到结果 Infinity （正无穷）
如果被除数是负数，得到结果 -Infinity （负无穷）
如果被除数是0，得到结果 NaN （Not a Number，非数字）

> typeof函数返回类型为string
> isNaN函数，该函数用于判断一个数据是否是NaN，返回boolean
> isFinite函数，该函数用于判断一个数据是否是有限的，返回boolean

3. 求余

%，有的教程称之为求模

余数的符号，与被除数相同。



**其他类型使用算术运算**

1. 除加号之外的算术运算符

将原始类型转换为数字类型（自动完成转换），然后进行运算。

- boolean： true -> 1, false -> 0
- string: 如果字符串内部是一个正确的数字，直接变为数字，如果是一个非数字，则得到NaN（能识别Infinity(+"Infinity")，不能把字符串内部的东西当作表达式），如果字符串是一个空字符串（没有任何内容），转换为0. 字符串转换时，会忽略**前后**空格(不包括中间)。

> NaN虽然是数字，但它和任何数字作任何运算，得到的结果都是NaN

- null：null -> 0
- undefined: undefined -> NaN

将对象类型先转换为字符串类型，然后再将该字符串转换为数字类型

对象类型 -> "[object Object]" -> NaN

2. 加号运算符

- 加号一边有字符串，含义变为字符串拼接

将另一边的其他类型，转换为字符串

数字 -> 数字字符串
boolean -> boolean字符串
null -> "null"
undefined -> "undefined"
对象 -> "[object Object]"

- 加号两边都没有字符串，但一边有对象，将对象转换为字符串，然后按照上面的规则进行

- 其他情况和上面的数学运算一致



### 6.表达式

表达式 = 操作符 + 操作数

每个表达式都有一个运算结果，该结果叫做**返回值**，返回值的类型叫做**返回类型**

所有的表达式都可以当作数据使用。


目前学习的运算符的返回值和类型

1. ```=```：该表达式，返回赋值的结果
2. ```.```：属性访问表达式，返回的是属性的值
3. ```[]```：属性访问表达式，返回的是属性的值
4. ```()```：函数调用表达式，返回的结果取决于函数的运行
5. 如果是一个声明+赋值的表达式，返回结果为undefined。

console.log函数调用的返回结果为undefined


> chrome浏览器控制台的环境是REPL环境
> REPL：Read Eval Print Loop，读-执行-打印-循环
> 当直接在控制台书写代码时，除了运行代码之外，还会输出该表达式的返回值



### 7.自动类型转化

#### 7.1自增和自减

##### 7.1.1基本功能

一元运算符

++：将某个变量的值自增1

--：将某个变量的值自减1

##### 7.1.2细节

##### 7.1.3自增自减表达式

x++: 将变量x自增1，得到的表达式的值是自增之前的值。
++x: 将变量x自增1，得到的表达式的值是自增之后的值。
x--: 将变量x自减1，得到的表达式的值是自减之前的值。
--x: 将变量x自减1，得到的表达式的值是自减之后的值。

##### 7.1.4优先级

从高到底依次是：

1. ```++ --```
2. ```* / %```
3. ```+ -```

优先级的运算细节：

1. 从左到右依次查看
2. 如果遇到操作数，将数据的值直接取出
3. 如果遇到相邻的两个运算符，并且左边的运算符优先级大于等于右边的运算符，则直接运行左边的运算符。

#### 7.2字符串

​	比的是ASCAII码，如果一个有两位，一个一位，那么没有的那一位的ASCAII码的值为0

#### 7.3比较运算符

大小比较：>   <    >=    <=
相等比较：==   !=   ===   !==

**比较运算符的返回类型：boolean**

**算术运算符的优先级高于比较运算符**

##### 7.3.1大小比较

##### 7.3.2细节

1. 两个字符串比较大小，比较的是字符串的字符编码。

2. 如果一个不是字符串，并且两个都是原始类型，将它们都转换为数字进行比较

'1' -> 1
'' -> 0
'   ' -> 0
'  a' -> NaN
'3.14' -> 3.14

NaN与任何数字比较，得到的结果都是false

Infinity比任何数字都大

-Infinity比任何数字都小

3. 如果其中一个是对象，将对象转换为原始类型然后，按照规则1或规则2进行比较

目前，对象转换为原始类型后，是字符串 "[object Object]"



##### 7.3.3相等比较

###### == 和 != (相等比较 和 不相等比较)

==: 比较两个数据是否相等
!=: 比较两个数据是否不相等

###### **细节**

1. 两端的类型相同，直接比较两个数据本身是否相同（两个对象比较的地址）

2. 两端的类型不同

1). null 和 undefined， 它们之间相等， 和其他原始类型比较， 则不相等。
2). 其他原始类型，比较时先转换为数字，再进行比较
3). NaN与任何数字比较，都是false，包括自身
4). Infinity和-Infinity，自能和自身相等
5). 对象比较时，要先转换为原始类型后，再进行比较

**由于相等和不相等比较，对于不同类型的数据比较违反直觉，因此，通常我们不适用这种比较方式，而是使用更加接近直觉的严格相等和严格不相等比较**


###### === 和 !== （严格相等 和 严格不相等）

=== ： 两端的数据和类型必须相同
!== ： 两端的数据或类型不相同

1. 两端类型相同，规则和相等比较一致。
2. 两端类型不同，为false。

数字规则：

1). NaN与任何数字比较，都是false，包括自身
2). Infinity和-Infinity，自能和自身相等

### 8.逻辑运算符

布尔运算符

#### 8.1与（并且）

符号：&&

书写方式： 表达式1 && 表达式2

1. 将表达式1 进行 boolean 判定

以下数据均判定为false：

1) null
2) undefined
3) false
4) NaN
5) ''
6) 0

其他数据全部为真

2. 如果表达式1的判定结果为假，则直接返回表达式1，而不执行表达式2；否则，返回表达式2的结果。 （短路规则）

#### 8.2或

符号：||

写法：表达式1 || 表达式2

1. 将表达式1 进行 boolean 判定

2. 如果表达式1为真，直接返回表达式1，不运行表达式2；否则，返回表达式2

#### 8.3非

符号：!

写法: !数据

一元运算符

将数据的boolean判定结果直接取反，非运算符一定返回boolean类型。

### 9.运算符补充*

#### 9.1输出字符串拼接

传统写法:

```js
console.log("我叫" + zheng + ",今年：" + sui + "了")
```

这样子写首先表达上给我们不是很明确，其次是过于麻烦，于是我们就有了第二种写法用于简化：使用 ` `` `  飘字符串，简称**模板字符串**

```js
console.log(`我叫${zheng},今年：${sui}了`)
```

#### 9.2void运算符

和typeof一样有两种写法：

1.`void 表达式`

2.`void(表达式)`

特性：运行表达式，然后返回undefined(他不管你表达式怎么写的都返回undefined)

#### 9.3逗号运算符

例如：`表达式1,表达式2`

依次运行，然后返回最后一个表达式的结果

**逗号运算符的优先级比赋值运算符还要低，所以我们通常要用括号括起来不然就是执行完一个逗号前面的表达式就执行赋值了**

### 10.switch

比较的是严格相等

### 11.数组

#### 11.1数组的定义：

1. ```js
   var arr = new Array(数组长度);
   ```

2. ```js
   var arr = new Array(1,2,3,4);
   ```

3. ```js
   var arr = [1,2,3,4];
   ```

#### 11.2JS中数组的本质：

本质是一个对象

typeof()出来的类型就是对象(object)

例如：

```js
var obj = {
    0 : 1,
    1 : 1,
    length : 2,
}
console.log(obj[1]);//我们同样可以这样子来访问，因为 1 会自动被转化成字符串
```



**因为数组的本质是一个对象所以我们也能给数组加属性：**

```js
arr["nhjk"] = "hjgfjyh";
```

**数组的length属性的值位最大下标+1**

例如：

如果我们本来有11个数组内容：

可是我们把length的值改成5，那么我们的数组就只有前5个数组的内容了，后面的会被截断，也就是丢失了

如果我们把length的值设为200多，那么我们多余的下标就会用一个empty来表示，empty没有任何意义，意思可以理解为空，也就是这种[,,,,,]



**数组的下标的值为undefined的话这个下标值依然存在：**

```js
var arr = [undefined,undefined];

console中：
{
    0:undefined,
    1:undefined,
}
```



##### 下标不连续的数组称为稀松数组



数组在最后一个元素的后面加逗号的意义为数组的对齐，并不是添加新的元素：

```js
var arr = [1,2,3,4,];
console中:
{
    0:1,
    1:2,
    2:3,
    3:4,
}
```

所以：

```js
var a = [,,,];
```

的length为2。



**delete同样能删除数组数据，不过删除后则会变成稀松数组，删除的位置就变成empty了,其他的属性都不会变化**

#### 11.3数组的方法

##### 11.3.1添加元素：

​	**在末尾添加元素：**

​		数组.push(元素)

​	**在开头添加元素：**

​		数组.unshift(元素)

​	**在中间添加元素：**

​		数组.splice(从什么下标开始, 删除多少个数据, 要添加的数据是什么)      

​			如果我们的下标填的数字大于length那么我们splice会将我们的数据从最后一个下标开始添加

​			如果我们的下表填的数字小于0那么我们splice会将我们的数据从第一个索引开始添加

##### 11.3.2删除元素：

​	**删除末尾元素：**

​		数组.pop()

​			它会将数组的最后一个元素删除，并将这个元素返回

​	**删除开头元素：**

​		数组.shift()

​			它会将数组的第一个元素删除，并将这个元素返回

​	**删除中间元素：**

​		数组.splice(从哪个下标开始，删除多少个元素)

​			将删除的多个元素以数组的形式返回

​			splice删除元素不会使数组变成稀松数组

​			如果想要删除元素的个数大于length，splice不管它，直到删掉最后一个元素就停止了

##### 11.3.3不改变原数组：

​	**复制元素：**

​		数组.slice(起始位置下标，结束位置下标)

​			它会将这个范围内的元素复制一份给自己并返回

​			不会改变原数组

​			如果下标填的是负数那么就是倒数

​			他只能从左往右取，不能从右往左取

​			如果不写结束下标则直接复制到最后一个元素

```js
var arr = [1,2,3,4];
var result = arr.slice(-3, arr.length);

console中：
{
    0:2,
    1:3,
    2:4,
}
```

##### 11.3.4清空数组：

​	**更改length：**

```js
arr.length = 0;
```

​	**使用splice方法：**

```js
arr.splice(0,arr.length);
```

##### 11.3.5查找元素：

​	**indexOf(查找目标)：**

​		从这个数组中去寻找这个目标，查找过程中使用严格相等

​		并返回第一个匹配的目标的下标

​		如果返回-1则并没有这个目标

​		字符串也可以用

​	**lastIndexOf(查找目标)：**

​		与indexOf的区别：

​					返回最后与其匹配的目标的下标

##### 11.3.6语法补充：

​	in关键字：

​		语法： 属性 in 对象

​		判断这个属性是否在这个对象内

​		属性的类型为“字符串”

​		返回结果：true/false

​		他判断的使属性名，不是属性值

##### 11.3.7填充数组：

​	语法：数组.fill(数据)

​	将数组的所有项，填充为指定的数据

​	数组.fill(数据，开始下标)

​	将数组从开始下标到数组末尾填充为指定数据

​	数组.fill(数据，开始下标，结束下标)

##### 11.3.8数组克隆

slice函数可以完成克隆,因为他是复制然后返回一个全新的数组

数组.slice()

##### 11.3.9将数组的每一项链接成一个字符串

数组.join(连接符)

如果不加连接符则默认为，连接

##### 11.3.10两个数组拼接

数组.concat(另一个数组)

返回一个全新的数组

### 12.foreach循环

foreach循环数组返回的是属性也就是数组的下标，他不会返回lenght



#### 12.1foreach与for循环的区别

1. for循环在访问稀松数组时是可以访问到没有的元素的，这个元素是undefined
2. 因为foreach循环访问的是属性，而稀松数组的有的元素的属性是访问不到的，那么这些访问不到属性的元素就读不出来

**类似面试题：**

```js
//创建一个长度为100的数组，给数组的每一项赋值为"abc"

var arr = new Array(100);
for(var i = 0; i < 100; i++){
    arr[i] = "abc";
}
```

此题如果使用forin循环，则无法更改，因为forin循环访问的是属性，而稀松数组没有的属性它访问不到，所以就无法改变

也可以使用数组的“fill()函数”

### 13.return

return后面没有接值，则返回的是undefined

如果没有写return则js会自动给你加一个return。

### 14.文档注释

写在函数上面

```
/**
 *两个数求和
*/
function sum(){

}
```

此时我们在调用这个函数时，就会給我们提示这个函数是做什么用的



如果我们加了参数的话则会有：

```
/**
 *@param{number}a  <-这个并不是代码也不会执行{}里面写的是提示这个参数a需要填写的类型是什么
 */
 function sum(a){
 
 }
```



@returns  {}   <-我们可以在文档注释中添加这个，意思为这个返回值的类型是什么，{}里面填写类型，{}后面写的中文是这个输出的提示

### 15.立即执行函数运行原理

因为表达式会将表达式的执行结果返回，而函数你作为表达式然后没有调用就会被当作结果直接返回，所以我们在他后面加个执行符号就可以执行了

```
(function (){})()
```

因为立即执行函数不能通过名字进行调用，所以立即执行函数的名字可以省略，而普通函数是不行的

没有名字的函数函数

### 16.构造函数

**用途：**用函数创建对象

1. 函数返回一个对象

   ```js
   function GouZao(){
       return {
           a : 1,
           b : 2
       }
   }
   var gouZao = GouZao();
   ```

2. 构造函数

   ```js
   function GouZao(){
       this.a = 1;
       this.b = 2;
   }
   var gouZao = new GouZao();
   ```

返回结果：

```
GouZao {
	a : 1,
	b : 2
}
```

**规则：**

1. 函数名使用大驼峰命名法

   ```
   GouZao(大驼峰)
   gouZao(小驼峰)
   ```

2. 构造函数内部，会自动创建一个新对象，this指向新创建的对象，并且会自动返回新对象

3. 构造函数中如果出现返回值，如果返回值是原始类型则直接忽略，如果是引用类型则使用返回结果

4. 所有的对象，最终都是通过构造函数创建的

   ```js
   var arr = [1,2,3,4];//语法糖
   //实质：
   var arr = new Array(1,2,3,4);
   
   
   var obj = {//语法糖
       name : "郑",
       age : 18
   }
   //实质：
   var obj = new Object();
   obj.name = "郑";
   obj.age = 18;
   ```

**new.target**

该表达式在构造函数中使用，如果这个函数是通过new 来调用的，则返回这个构造函数（new.target === 构造函数名，如果是直接调用，则返回undefined

**用途：**

判断这个构造函数是否确实是通过new来执行的

```js
function GouZao(){
    if(new.target){
        this.name = "郑",
        this.age = 18
    }else{
        return {
            name : "郑",
            age : 18
        }
    }
}
```

> 通常的构造函数都是用这种方法防止用户错误使用

例如，Array构造函数这些就使用了这种方法

```js
var arr = Array();
arr -> []
```

### 17.函数的本质

1. 函数的本质就是对象
2. 所有的对象都是通过关键字new出来的，new 构造函数();
3. 所有的函数，都是通过new Function创建的
4. 由于函数本身就是对象，因此函数中，可以拥有各种属性

### 18.包装类

JS为了增强原始类型的功能，为Boolean，string，number分别创建了一个构造函数：

1. Boolean
2. String
3. Number

如果语法上，讲原始类型当作对象使用时(一般是在使用属性时)，JS会自动在该位置利用对应的构造函数，创建对象来访问原始类型包装类里面的属性。

**类：**在JS中，可以认为，类就是构造函数

**成员属性(方法)、实例属性(方法)：**表示该属性是通过构造函数创建的对象调用的

```js
var num = new Number(3.1415926);
num.toFixed(2);
> "3.14"

```

**静态属性(方法)、类属性(方法) ：**表示该属性是通过构造函数本身调用的(也只能通过构造函数来调用的属性)

```js
> new Number().isNaN();//静态属性/类属性
var num = new Number();
//num中并没有isNaN()这个函数
```

### 19.尾递归

如果一个函数最后一条语句是调用函数，并且调用的函数不是表达式的一部分，则该语句称为尾调用，如果尾调用是自身函数，则称为尾递归

```js
//什么是尾递归和尾调用
function diGui(n){
    return diGui(n);//尾递归
    return n * diGui(n);//非尾递归
}
function diaoYong(){
    return diGui(1);//尾调用
}

//为什么会进行优化
function diGui(n){
    return diGui(n);
    //因为它只是一个函数调用，调用完它就已经没有任何事情需要做的了，也就没有必要留在栈内存中，所以有的语言和执行环境会对他进行优化(node.js)
    return n * diGui(n);
    //因为它是一个函数表达式，这个函数调用完还要进行表达式计算，所以它不能被优化
}
```

某些语言或执行环境会对尾递归调用进行优化，它们会理解销毁当前函数，避免执行栈空间被占用↓

在浏览器执行环境中，尾调用没有优化，但在node.js环境中有优化

### 20.标准库

标准库（标准API）

- 库：liberary
- API：应用程序编程接口，Application Programing Interface
- 标准：ECMAScript标准

#### 20.1Object

#### 20.1.1静态成员

语法：`new Object(value)`;

- 如果这个值为null/undefined，则返回一个普通对象

- 如果写的是原始类型则返回所对应属性的对象(调用该类型的包装类)

  ```js
  var a = new Object(1);
  > Number{1}
  ```

- 如果不是原始类型你传啥他给你直接返回参数

##### 20.1.1.1Object.keys()

语法：`Object.keys(obj)`

返回这个对象的属性组成的数组，如果没有属性则返回一个空数组

```js
var a = Object.keys({name:"zheng", age:18});
> a: ["name", "age"];

var a = Object.keys(1);
> a: [];
```

##### 20.1.1.2Object.values()

语法：`Object.values(obj)`

返回这个对象的属性的值组成的数组，如果没有属性和值则返回一个空数组

```js
var a = Object.values({name:"zheng",age:18});
> a: ["zheng", 18];
```

##### 20.1.1.3entries()

语法：`Object.entries(obj)`

返回这个对象的属性和属性值组成的二维数组，如果没有属性和值则返回一个空二维数组

```js
var a = Object.values({name:"zheng",age:18});
> a: [[name, "zheng"], [age, 18]];
```

#### 20.1.2实例成员

> 实例成员可以被重写

**所有对象，都拥有Object的所有实例成员**

##### 20.1.2.1toString()

- toString方法：得到某个对象的字符串格式

默认情况下，该方法返回"[object Object]";

```js
var a = [1,2,3,4];
console.log(a.toString());
> "1,2,3,4"

var a = {name:"zheng"};
console.log(a.toString());
> "[object Object]"
```

##### 20.1.2.2valueOf()

- valueOf方法：得到某个对象的值

默认情况下，返回该对象本身

```js
var a = {name:"zheng"};
console.log(a.valueOf());
> {name:"zheng"};
```

> 在JS中，当自动的进行类型转换时，如果要对一个对象进行转换，实际上是先调用对象的valueOf方法，然后调用返回结果的toString方法，将得到的结果进行进一步转换。

**当对象需要转化的时候如果调用完valueOf()后他已经得到了想要的数据类型则JS不会再toString，则直接拿valueOf()的结果进行运算**：

```JS
var a = {};
console.log(a + 1);
//转化过程：a.valueOf().toString() + 1;
//运行结果："[object Object]1"

var a = {};
a.valueOf = function (){
    return 123;
}
console.log(a + 1);
//转化过程：a.valueOf() + 1
//运行结果：124
```

#### 20.2Function

#### 20.2.1原型对象

##### 20.2.1.1属性

###### 20.2.1.1arguments关键字

> 实参数组，你传了多少个参数他就有多少个索引
>
> 它的索引位和形参产生映射

如果没有传的参数，可是函数内部又给这个形参加上了这里是没有任何关联的，因为arguments是实参数组：

```js
function arg(a, b){
    a = "abc";
    b = 123;
}
arg(1);
> arguments: [0:"abc"];
```

不过如果传了undefined的话是可以产生映射的也就是实参数组里面是有undefined的，所以你只有传了多少个实参，实参数组里面才有多少个元素：

```js
function arg(a, b){
    a = "abc";
    b = 123;
}
arg(1, undefined);
> arguments: [0:"arg", 1:123];
```

###### 20.2.1.2函数名.length

> 获取函数的形参个数

```js
function fc(a, b, c, d, e){}
> fc.length: 5
```



##### 20.2.1.2方法

###### 20.2.1.2.1函数.call/apply()

通常，可以利用apply、call方法，将某个伪数组转换伪真数组:

```js
function fc(){
    var newArray = [].slice.call(arguments);
}
fc(1,2,3,4,5,6,7,8,9);

> newArray: [1,2,3,4,5,6,7,8,9];
//因为slice返回的是一个截取过后的新数组，所以现在这个数组是全新的，而且拥有数组所有的实例方法
```

###### 20.2.1.2.2函数.bind()

> 返回一个新函数，这个函数的this固定为bind()的指向，方便我们不用调用一个函数就call/apply确定它的this指向

通过bind绑定的函数的this指向如果再使用call/apply调用且调用途中试图更改 **this** 指向，是**无法改变的**，bind绑定的this是锁死的：

```js
function fc(){
    console.log(this);
}
var a = fc.bind(window);
var obj = {
    name:"zheng",
}
a.call(obj);
//运行结果：window对象
```

#### 20.3Array

##### 20.3.1静态成员

###### 20.3.1.1from方法

> 同样我们可以使用call/apply配合slice()来实现将类数组转化成真数组
>
> ```js
> function fc(){
>     var newArray = [].slice.call(arguments);
> }
> ```

语法：`Array.from(类数组)`

返回：返回一个真数组

```js
function fc(){
    var newArray = Array.from(arguments);
}
fc(1,2,3,45,6);
> newArray : [1,2,3,45,6];
```

###### 20.3.1.2isArray方法

> 真数组：通过Array构造函数创建的数组

语法：`Array.isArray(数据)`

返回：这个数据是否为真数组：true/false

```js
function fc(){
    console.log(Array.isArray(arguments));
    //运行结果：false
}
```

###### 20.3.1.3of方法

> 相当于我们写数组字面量[1,2,3,4,5,6];
>
> 和new Array()创建数组的区别：
>
> ​	new Array()如果只传一个参数代表这个数组的长度为这个参数
>
> ​	Array.of()不管传多少个参数都表示这个数组的元素

语法：`Array.of(数组元素)`

返回：这个数组

```js
var arr = Array.of(1,2,3,4,5,6);
> arr: [1,2,3,4,5,6];
//相当于我们写数组字面量[1,2,3,4,5,6];
```

##### 20.3.2实例成员

###### 20.3.2fill方法

> 将数组的所有元素填充为我们传的数据

语法：

```js
var arr = new Array(200);
// 此时的arr
> arr : [ermy×200];
arr.fill("abc");
//此时的arr
> arr : ["abc","abc","abc"....共200个];
```

返回：此this也就是这个数组

###### 20.3.3pop方法

> 删除数组的最后一位

参数：传参和不传参一样

`[1,2,3,4].pop()`

###### 20.3.4push方法

> 向数组的第length位添加元素

参数：需要向数组第length位添加的元素

`[1,2,3].push(4,5,6);`

`[1,2,3,4,5,6]`

###### 20.3.5reverse方法

> 将数组元素倒过来

参数：无

`[1,2,3,4].reverse`

`[4,3,2,1]`

###### 20.3.6shift方法

> 珊除数组的第一个元素

参数：无

和pop一样

###### 20.3.7sort方法

> 将数组按Unicode码进行排序

参数：回调函数(用于告诉sort方法如何排序)

```js
var arr = [2,8,9,78,1];
arr.sort(function (a, b){
    return a - b;
})
```
它会将元素传给形参a和b进行比较
* 返回值大于0，则a在b的后面
* 返回值等于0，则不动
* 返回值小于0，则a在b的前面

###### 20.3.8splice方法

> 将选中的范围剪切并返回，原数组被剪切的部分丢失

参数：剪切的范围

`[1,2,3,4,5].splice(1,3)`

`[2,3,4]`

###### 20.3.9unshift方法

> 像数组的第一位添加元素

参数：需要添加的元素

和push一样

###### 20.3.10纯函数/无副作用函数：

> 不会导致当前对象发生改变

###### 20.3.11concat方法

> 数组拼接

返回：一个新的拼接好的数组

```js
var arr1 = [1,2,3];
var arr2 = [2,3,4];
var arr3 = [5,6,7];
var arr4 = arr1.concat(arr2,arr3);
> arr4 : [1,2,3,2,3,4,5,6,7];
```

###### 20.3.12includes方法

> 查找你传的这个参数是否在数组中，查找从哪个下标开始是可定的

语法：`[1,2,3,4].includes(valueToFind[,index])`

比较规则：===

示例：

```js
var arr = [1,2,3,4,5];
arr.includes(2,2);
//false
//运行含义：从下标为2的地方开始往后找有没有2这个元素
arr.includes(2);
//true
//运行含义：查找这个数组内是否含有2这个元素
```

返回值：true/false

###### 20.3.13join方法

> 将一个数组以参数的形式连接成一个字符串

参数：可填可不填(填了则按参数填的内容连接数组，否则默认使用","连接)

示例：

```js
var arr = [1,2,3,4];
var result = arr.join("a");
> result : "1a2a3a4";
var result2 = arr.join();
> result2 : "1,2,3,4";
```

返回：将数组拼接成字符串并返回

###### *20.3.14forEach方法

> 可以代替for循环，并且使用方便

语法：

```js
[1,2,3,4].forEach(function ([当前遍历的元素，当前遍历的元素的下标，正在遍历的这个函数]){
    
})
```

需要哪些数据你就把对应的参数天上去然后相关操作写在回调函数里面就好了

示例：

```js
//示例一
var arr = [1,2,3,4];
arr.forEach(function (iteam, index, array){
    console.log(iteam, index, array);
})
//运行结果：
> 1 0 Array(4)[1,2,3,4]
> 2 1 Array(4)[1,2,3,4]
> 3 2 Array(4)[1,2,3,4]
> 4 3 Array(4)[1,2,3,4]

//示例二
var arr = [1,2,3,4];
arr.forEach(function (iteam){
    if(iteam % 2 == 0){
        console.log(iteam);
    }
})
//运行结果:
> 2
> 4
```

###### 20.3.15every方法

> 判断是否所有元素都满足回调函数的规则，它会全部元素都拿去判断如果有一个不行就直接返回false

返回：true/false

语法：

```js
[1,2,3,4].every(function ([当前遍历的元素，当前遍历的元素的下标，正在遍历的这个函数]){
    
})
```

示例:

```js
var arr = [1,2,3,4,5];
var result = arr.every(function (iteam){
    return iteam <= 6;
})
//运行结果：true
```

###### 20.3.16some方法

> 它会全部元素都拿去判断如果有一个元素满足条件则直接返回true

其余部分和every一样

###### 20.3.17filter方法

> 它会遍历全部元素，把满足条件的放在一个数组内，遍历结束将他返回

示例：

```js
var arr = [1,2,3,4];
var result = arr.filter(function (iteam){
   	return iteam % 2 == 0;
})
> result : Array(2)[2,4];
```

###### 20.3.18find方法

> 它会遍历这个数组，找到满足这个条件的第一个元素，并将这个元素返回

示例：

```js
var arr = [{name:"zheng",age:18}, {name:"a", age:20}, {name:"b", age:25}];
var result = arr.find(function (iteam){
    return iteam.age >= 20;
})
//运行结果：
> result : {name:"a",age:20}
```

返回：返回第一个满足条件的元素，如果没有则返回undefined

###### 20.3.19findIndex方法

> 它会遍历这个数组，找到满足条件的第一个元素的，并返回它的下标

示例：

```js
var arr = [{name:"zheng",age:18}, {name:"a", age:20}, {name:"b", age:25}];
var result = arr.findIndex(function (iteam){
    return iteam.age > 20;
})
> result : 2;
```

返回：返回第一个满足条件的元素的下标，如果没有则返回-1

###### 20.3.20keys方法

> 在Object的时候就有了一模一样

###### 20.3.21map方法

> 返回一个由回调函数的返回值组成的数组

参数：和findIndex这些方法一样

返回：返回一个由回调函数的返回值组成的数组

示例：

```js
//示例一
var arr = [{
    name:"zheng",
    age:18
}, {
    name:"guan",
    age:18
},];
var result = arr.map(function (iteam)){
    return iteam.name;
}
> result : ["zheng", "guan"];

//示例二
var score = [68,89,75,45,65];
var result = score.map(function (item, index)){
      return {
                name:"学生" + (i + 1),
    			score:item
             }                 
}
> result : [{
    name:"学生1",
    score:68
}, {
    name:"学生2",
    score:89
}, {
    name:"学生3",
    score:75
}, {
    name:"学生4",
    score:45
}, {
    name:"学生5",
    score:65
}, ]
```

###### 20.3.22reduce方法

> 我们可以拿reduce拿来做阶乘或者计算总和

参数：a, b

返回：最后一次计算的结果

计算过程：

```js
var arr = [1,2,3,4,5];
var result = arr.reduce(function (a, b){
    return a + b;
   	/*
   	一：a = 1 , b = 2;
   	二：a = 3 , b = 3;
   	三：a = 6 , b = 4;
   	四：a = 10 , b = 5;
   	运行结果：15
   	*/
});
```

示例：

```js
var arr = [1,2,3,4,5];
var result = arr.reduce(function (a, b){
    return a * b;
})
> result : 120;
```

如果调用这个方法的数组为空的话，则会报错，所以这个函数还支持一个参数“默认值”：`arr.reduce(回调函数[, 默认值])`

```js
//报错
var arr = [];
var result = arr.reduce(function (a, b){
    
})

//加上默认值
result = arr.reduce(function (a, b){
    
}, 0);//直接返回0，不执行回调函数

//这个数组有一个参数并且还有默认值
arr = [1];
result = arr.reduce(function (a, b){
   return a + b; 
}, 0)//运行结果：1
//运行过程：a = 0 , b = 1;
```

如果有两个参数且还有默认值：

```js
var arr = [1,2];
var result = arr.reduce(function (a, b){
    return a + b;
}, 1)//运行结果：4
//运行过程：
一：a = 1 , b = 1
二: a = 2, b = 2
结果：4
```

#### 20.4链式编程

> 每一次返回的结果的类型都要和这个函数所需的类型一致

示例：

```js
var arr = [11,22,33,66,77,88];

//先对数组进行随机排序
//只取及格的分数
//得到学生对象的数组(每个学生对象包含姓名和分数)

var result = arr.sort(function (a, b){
    return Math.random() - 0.5;
}).arr.filter(function (iteam){
    return iteam >= 60;
}).arr.map(function (iteam, i){
    return {
        name:"学生" + (i+1),
        score:iteam
    }
})

//运行结果(因为进行了随机排序，所以每次的运行结果顺序可能不太一样)：
> result : Array(3)[{
    name:"学生1",
    score:77
}, {
    name:"学生2",
    score:66
}, {
    name:"学生3",
    score:88
}, ]
```

### 原始类型包装类：

> new 包装类(value)返回的是一个对象
>
> 包装类(value)返回的不是一个对象而是这个包装类类型的所对应这个value的值

#### 20.5Number

##### 20.5.1静态成员

1. isNaN() 是否为非数

2. isFinite() 是否是有限的数

3. isInteger()是否为整数

4. parseFloat() 将一个数字转化为小数

   没有显示的变化是因为在JS中整数和小数都是一样的为小数的存储形式

   

   parseInt和parseFloat要求参数是一个字符串，如果不是字符串，则会先转化成字符串。从字符串开始位置进行查找，找到第一个有效的数字进行转化，如果没有，则返回NaN，左右空白字符会忽略

   ```js
   parseFloat("    3.14abc  abc");
   > 3.14
   parseFloat("abc3.14");
   > NaN
   parseFloat("3.14.1.5.2");
   > 3.14
   parseInt("3.142654abc");
   > 3
   ```

   

5. parseInt() 将一个数字转化为整数

   直接舍去小数部分

   他还有第二个参数，表示这个数字是个多少进制的数，因为他要返回的必须是一个10进制的数，所以最终以这个多少进制转化为10进制,不过如果你这个数不满足你所指定的进制的话则返回NaN：

   ```js
   parseInt("101", 2);
   > 5
   
   //特殊情况
   parseInt("103", 2);
   > 2
   当他读到3的时候它就发现不满足2进制，所以就不看第三位，只看前两位"10"，所以返回2
   
   parseInt("118", 8);
   > 9
   
   parseInt("311", 2);
   > NaN
   也他第一个就是不满足进制了
   ```

##### 20.5.2实例成员

###### 20.5.2.1toFixed方法

> 作用：保留小数点后几位
>
> 无法通过字面量调用，必须是变量
>
> 会四舍五入

返回：字符串

```js
var num = 3.1415926;
var result = num.toFixed(2);
> result : "3.14"
```

###### 20.5.2.2toPrecision方法

> 保留精度

返回：字符串

```js
var a = 2514.2514;//表示8个精度
var	result = a.toPrecision(5);//只精准5位
> result : "2514.2"
```



#### 20.6String

> 是一个类数组它的每一个字符对应一个下标012...
>
> 并且有length这个属性
>
> 字符串的字面量可以和他的包装类一样调用方法

##### 20.6.1静态成员

###### 20.6.1.1fromCharCode方法

> 得到所对应Unicode码的字符

```js
String.fromCharCode(65, 66);
> "AB"
```

作用：我们可以使用循环来打印A-Z的字符

##### 20.6.2实例成员

###### 20.6.2.1length属性

> 获取字符串长度

```js
var str = "abc";
console.log(str.length);
> 3
```

###### 20.6.2.2charAt方法

> 返回指定位置的字符

```js
var str = "abcd";
str.charAt(0);
"a"
//相当于：
str[0];
"a"
```

charAt和str[]的区别：

1. 如果通过str[]获取超过这个数组长度的元素是和数组是一样的返回undefined
2. 如果通过charAt获取超过这个数组长度的元素则返回一个空字符串""

###### 20.6.2.3charCodeAt方法

> 返回指定位置所对应的Unicode码

```js
var str = "你好";
str.charCodeAt(0);
> 20320
```

如果你提供的位置没有的话则返回NaN

###### 20.6.2.4concat方法

> 可连接多个字符串并返回

```js
var str1 = "我是"
var str2 = "你"
var str3 = "爸爸"
var str4 = str1.concat(str2, str3);
str4
> "我是你爸爸"
```

###### 20.6.2.5includes方法

> 判断这个字符串在不在这个字符串内

```js
var str = "abc";
str.includes("1");
> false
```

###### 20.6.2.6endsWith方法

> 判断该字符串是否以这个字符串结尾

```js
var str = "abc你爸爸";
str.endsWith("你爸爸");
> true
```

###### 20.6.2.7indexOf方法

> 找到字符串中为这个参数的索引

如果没找到则返回-1

```js
var str = "我是你爸爸";
str.indexOf("你爸爸");
> 2
```

###### 20.6.8lastIndexOf方法

> 返回最后一个该为参数字符串的索引

```js
var str = "我是你爸你爸是我"
str.lastIndexOf("你");
> 4
```

###### 20.6.9padStart方法

> 通常用于时间填充：01：08：25

参数：(想要字符串长度为，如果字符串没有达到这个长度那么向这个字符串的前面填充什么字符)

```js
var str = "1";
var result = str.padStart(2, "0");
> result : "01"
```

###### 20.6.10padEnd方法

> 和padStart一样，只不过padEnd是向末尾填充

###### 20.6.11repeat方法

> 将该字符串重复参数次

```js
var str = "abc";
var result = str.repeat(3);
> result : "abcabcabc";
```

###### 20.6.12slice方法

> 选择一段范围，将其范围内的字符串串返回

```js
var str = "abcd";
var result = str.slice(1,2);
> b
```

###### 20.6.13startsWith方法

> 判断这个字符串是否以这个参数字符串开头

其余部分和endsWith方法一样

###### 20.6.14substr

> 它相对于slice的区别是他的第二个参数代表的是这个从第一个参数开始截取第二个参数个数的字符串

###### 20.6.15substring

> 他和slice一样

###### 20.6.16slice和substr和substring的区别

> slice和substr位置可以是负数
>
> substring位置如果是负数的话则自动转化成0
>
> slice和substring的位置不能倒着来也就是只能向右取，不能向左取，而substring可以

###### 20.6.17toLowerCase方法

> 将字符串转化成小写然后返回

参数：无需

###### 20.6.18toUpperCase方法

> 将字符串转化成大写然后返回

参数：无需

###### 20.6.19trim方法

> 去掉首尾空格
>
> 适用场景：用户在输入账号或者密码时可能不小心前面和后面打了空格我们就需要将他给去掉一下，来达成用户体验效果

参数：无需

1. trimStart()去掉左边的空格
2. trimEnd()去掉右边的空格

###### 20.6.20 split方法

> 分割字符串得到一个由字符组成的真数组

```js
"a,b,c,d,e,f".split(",");
> Array(6)["a","b","c","d","e","f"]
```



#### 20.7Boolean

##### 20.7.1实例方法

###### 20.7.1.1toString方法

> 转化成字符串"true"/"false"

返回：字符串

```js
var tf = true;
var result = tf.toString();
> result : "true"
```

#### 20.8Math对象

> 他是对象，不是构造函数

##### 20.8.1random方法

> 产生一个0~1的随机数

取不到最大值如果想取到最大值则max+1-min

```js
Math.random()*(max-min) + min
```

##### 20.8.2PI属性

> 圆周率
>
> 常量

常量：名字全部大写，如果有多个单词则用_分隔

##### 20.8.3abs方法

> 得到x的绝对值

语法：`Math.abs(x)`

##### 20.8.4floor方法

> 向下取整

向下取整：取向左方向与他最接近的那个整数

##### 20.8.5ceil方法

> 向上取整

##### 20.8.6max和min方法

max：

- 语法：`Math.max(x.....)`
- 得到这一堆数值中的最大值
- 如果没有传参则最大值为-Infinity

min：

- 语法：`Math.min(x.....)`
- 得到这一堆数值中的最小值
- 如果没有传参则最大值为Infinity

##### 20.8.5pow方法

> 求一个数字的多少次幂

语法：`Math.pow(x,y)`

##### 20.8.6round方法

> 四舍五入一个是数字

语法：`Math.round(x)`

注：-1.5四舍五入为-1

#### 20.9Date构造函数

##### UTC和GMT：

- 世界划分为24个时区，北京在东8区，格林威治在0时区
- GMT:Greenwish Mean Time 格林威治世界时。太阳时，精确到毫秒
- UTC:Universal Time Coodinated 世界协调时。以原子时间为计时标准，精确到纳秒。
- UTC和GMT之间误差不超过0.9秒
- GMT+0800 东8区

##### 时间戳：

- 1970-1-1 凌晨 到 某个时间(现在) 所经过的毫秒数
- 他是在unix操作系统的时候为了计时用的，它是32位数字
- 2的32次方 大概在68年后就不再精确
- 2038年为时间戳的最后一年
- 2039年则时间戳清零，相当于1970年

##### 方便读取且符合计算机系统的时间形式：

- toDateString方法：将日期部分转换为可读的字符串。
- toISOString方法：将整个对象转换为ISO标准的字符串格式。
- toLocaleDateString方法：根据当前系统的地区设置，将日期部分转换为可读的字符串
- toLocaleString方法：根据当前系统的地区设置，将整个日期对象转换为可读的字符串
- toLocaleTimeString方法：根据当前系统的地区设置，将时间部分转换为可读的字符串

##### 日期的运算

日期对象重写了Object中的valueOf方法，返回的是一个数字，表示时间戳

因此，日期对象可以进行数学运算

#### 20.10正则表达式

JS中是一个对象，是构造函数RegExp创建的

##### 20.10.1匹配中文

```js
\[\U4E00-\u9FA5]\g
```

##### 20.10.2量词

- {n} 匹配n个
- {n,} 匹配n或多个个
- {n,m} 匹配n~m个

量词的指向是他前面的那个规则不是该正则的所有规则

##### 20.10.3创建正则表达式

1. 字面量模式

   ```js
   var reg = /\d/;
   ```

2. 构造函数模式

   ```js
   var reg = new RegExp("\d"/存有正则规则的变量(上面那种类型));
   ```

   如果用这种形式想进入全局搜索则：

   ```js
   var reg = new RegExp("\d"/存有正则规则的变量(上面那种类型), "g");
   ```

   

他们两个是一致的，本质都是由构造函数创建的，字面量只是一个语法糖

##### 20.10.4实例成员

###### 20.10.4.1global属性

> 只读属性

返回：true/false

true：开启了全局搜索

false：关闭了全局搜索

对应规则：`//g`

###### 20.10.4.2ignoreCase属性

> 只读属性

返回：true/false

true：开启了忽略大小写

false：关闭了忽略大小写

对应规则：`//i`

###### 20.10.4.3multiline属性

> 只读属性

返回：true/false

true：开启了多行匹配

false：关闭了多行匹配

对应规则：`//m`

20.10.4.4source属性

> 只读属性

返回：这个规则(字符串类型)

###### 20.10.4.4test方法

> 传入一个字符串形参判断这个字符串是否满足规则

```js
var reg = /\d/;
reg.test("123");
```

返回：true/false

**注：**

在**开启了全局**的状态下他只要匹配了一个满足规则，它就停止了，然后下一次匹配接着上一次匹配的地方开始向后匹配，如果后面没有了则重新归到第一位

​	示例：

```js
var reg = /abc/g;
console.log(reg.test("123abc123abc123"));//匹配到第一个abc停止了123abc|123abc123 返回：true
console.log(reg.test("123abc123abc123"));//接着上一次匹配到第二个abc停止了123abc123abc|123 返回：true
console.log(reg.test("123abc123abc123"));//没有匹配到abc 返回：false
console.log(reg.test("123abc123abc123"));//匹配到第一个abc停止了123abc|123abc123 返回：true
```
###### 20.10.4.5lastIndex属性
> 返回下一次匹配开始的字符串索引位置
> 可手动更改，会对下一次字符串的查询索引有影响
```js
var reg = /abc/g;
console.log(reg.test(reg.lastIndex, "123abc123abc123", reg,lastIndex));
//0 true 6
```

判断匹配了几次：
```js
var reg = /abc/g;
var n = 0;
while(reg.test("123abc123abc123")){
    n++;
}
console.log(`共匹配了${n}次`);
//匹配了2次
```

###### 20.10.4.6正则贪婪匹配原则
> 正则表达式默认启动贪婪模式
> 如何取消贪婪模式：
>   在量词后边加上“?表示一次或多次，这样就能将这个量词的贪婪给关闭了，则只要匹配到一个满足这个规则的就直接返回则不会进行试探性判断规则

在一个正则规则进行判断时，虽然规则为1次或多次，不过它都会试探性的向后一个字符串判断，如果满足规则，则纳入匹配结果，知道他试探性的那个字符串不满足规则则不再进行向下尝试，返回匹配结果

###### 20.10.4.7exec方法
> 返回的结果是一个真数组
> 它的下标会受到lastIndex的影响
> 如果没有开启全局则不会接着上一次匹配结束的下标进行开始
> 非全局匹配则每次都是从0下标开始

语法：```reg.exec("123")```
返回结果：一个真数组 / null(为匹配到)
示例：
```js
var reg = /\d+/g;
console.log(reg.exec("123abc123"));
> ["123", index:0, input:"123abc123"]
> 0:"123"      //匹配结果
  groups:undefined
  index:0     //匹配的下标起始位置
  input:"123abc123"   //匹配的字符串
  length:1 //匹配结果的个数
  __proto__:Array(0)
console.log(reg.exec("123abc123"));
> ["123", index:6, input:"123abc123"];
> 0:"123"     //匹配结果
  groups:undefined
  index:6    //匹配的下标起始位置
  input:"123abc123"  //匹配的字符串
  length:1 //匹配结果的个数
  __proto__:Array(0)
```

##### 20.10.5字符串对象中的正则
###### 20.10.5.1match方法
语法:```"123abc123".match(/\d+/g)```
返回:与这个规则匹配的字符串组成的数组：
如果并没有开启全局匹配，也就是只能匹配一个就返回了，则这个返回结果与正则对象中的exec方法返回结果一致
```js
var str = "123abc123";
var reg = /\d+/g;
console.log(str.match(reg));
> ["123", "123"]
> 0:"123"
  1:"123"
  length:2
  __proto__:Array(0)
```
如果开启了全局匹配，它则会将最后的匹配结果放在数组中给你，这样返回的数组与非全局的返回结果截然不同
```js
var str = "123abc123";
var reg = /\d+/;
console.log(str.match(reg));
> ["123", index:0, input:"123abc123"]
> 0:"123"      //匹配结果
  groups:undefined
  index:0     //匹配的下标起始位置
  input:"123abc123"   //匹配的字符串
  length:1 //匹配结果的个数
  __proto__:Array(0)
```

###### 20.10.5.2search方法
> 返回整个字符串第一个满足规则的下标，尽管开启了全局搜索也是一样的

返回：第一个满足规则的字符的下标
示例：
```js
//开启了全局搜索
var str = "123abc123";
var reg = /\d+/g;
str.search(reg);
> 0 //第一个匹配结果的下标

//非全局搜索
var reg1 = /\d+/;
str.search(reg1);
> 0
```

###### 20.10.5.3split方法
> 我们知道这个方法可以以什么字符来分割字符串，不过我们也可以在这里加上正则表达式，意思为满足这个条件的地方就被分割

示例：
```js
var str = "asfa asfa-asfa\tasfa";
str.split(/[ \-\t]/);
> ["asfa", "asfa", "asfa", "asfa"]
```
###### *20.10.5.4replace方法
> 通过正则表达式替换字符串，不会改变原数组

返回： 一个全新的字符串，不会改变原字符串
语法:```"123 123 123".replace(正则表达式，满足正则的字符串替换为什么 / 一个函数(他拿的是这个函数的返回结果))```

如果第一个参数填的是字符串它则会自动转化成new RegExp("字符串内容"),这样子写也就是没有开启全局匹配所以只会替换第一个:
```js
var str = "123 123\t123";
str.replace(" ", ",");
> "123,123  123"
```

*示例：
```js
//将空白字符转化成“,”逗号
var str = "123 123\t123\n123";
str = str.replace(/\s/g, ",");
console.log(str);
> "123,123,123,123"

//将hello world 转化成 Hello World
var str = "hello world";
str = str.replace(/\b[a-z]/g, function (match){//它会将满足规则的字符传给match
    return match.toUpperCase();//将满足条件的h，w转化成大写，并将其返回进行替换
});
> "Hello World"
```

###### *20.10.5.5捕获组
> 用小括号包裹的部分叫做捕获组
> 捕获组的位置和执行顺序是从左自右运行的

**正则中的exec方法：**
用正则的exec方法可以获取到捕获组的结果：
```js
var str = "2015-5-1, 2019-6-19, 2000-04-28";
var reg = /(\d{1,4})-(\d{1,2})-(\d{1,2})/g;
reg.exec(str)
> ["2015-5-1", "2015", "5", "1", index:0, input:"2015-5-1, 2019-6-19, 2000-04-28", groups:undefined]
> 0:"2015-5-1" //正则匹配结果
  1:"2015" //捕获组1
  2:"5" //捕获组2
  3:"1" //捕获组3
  index:0 //正则匹配字符起始位
  input:"2015-5-1, 2019-6-19, 2000-04-28"
  groups:undefined
  length:4
  __proto__:Array(0)
```

**具名捕获组：**
> 捕获组可以命名，叫做具名捕获组

语法：```/(?<year>\d{1,4})-(?<month>\d{1,2})-(?<day>\d{1,2})/g```
捕获组的结果存放在groups(组)里面
> groups以对象的形式存在
> 当我们没有具名捕获组时，groups值为undefined

示例：
```js
var str = "2015-5-1, 2019-6-19, 2000-04-28";
var reg = /(?<year>\d{1,4})-(?<month>\d{1,2})-(?<day>\d{1,2})/g;
reg.exec(str)
> ["2015-5-1", "2015", "5", "1", index:0, input:"2015-5-1, 2019-6-19, 2000-04-28", groups:undefined]
> 0:"2015-5-1" //正则匹配结果
  1:"2015" //捕获组1
  2:"5" //捕获组2
  3:"1" //捕获组3
  index:0 //正则匹配字符起始位
  input:"2015-5-1, 2019-6-19, 2000-04-28"
  groups:{
      year:"2015"
      month:"5"
      day:"1"
  }
  length:4
  __proto__:Array(0)
```

**非捕获组：**
> 非捕获组：有时我们加括号只是想把它当成一个整体来进行添加量词，并不像让他对我进行捕获(捕获是会影响执行效率的)

语法:```/(?:\d{1,4})-(?:\d{1,2})-(?:\d{1,2})/g```

**字符串中的replace方法：**
语法：```str.replace(reg, function (匹配结果, 捕获结果..))```
    ```str.replace(reg, "$1$2$3")``` $1表示第一个捕获组的结果，这样可以更加方便
```js
var str = "2015-5-1, 2019-6-19, 2000-04-28";
var reg = /(?<year>\d{1,4})-(?<month>\d{1,2})-(?<day>\d{1,2})/g;
str.replace(reg, function (match, g1, g2, g3){
    console.log(match, g1, g2, g3);
})
> "2015-5-1"
  "2015"
  "5"
  "1"
```

###### 20.10.5.6反向引用
在一个正则表达式中我们可以将捕获组的结果应用在我们的正则内：
```/(\d)\1/```表示我们这第一个数字和第二个数字必须一致 1122
如果是命名捕获组我们同样也可以使用`\1`这样来使用捕获组，我们也可以使用`\k<捕获组名字>` : ```/(?<char>\d)\k<char>/```
示例：
```js
//找出这个字符串中连续出现的字符
var str = "aaaaaabbbbbcccccceeeeeefreggggggg";
var reg = /(\w)\1+/g; //表示这个单词字母第一个和第二个必须一致且第二个有一个或多个则是连续的
var result;
while(result = reg.exec(str)){
    console.log(result[0], result[1]);
}
> "aaaaaaa" "a"
  "bbbbb" "b"
  "cccccc" "c"
  "eeeeee" "e"
  "gggggg" "g"
```

###### 20.10.5.7正向预查
检查某个字符后面的字符是否满足条件，该规则不成为匹配结果，并且不成为捕获组，只是进行一个判定
示例：
```js
var str = "asdf1asdf1safeqg2dsgqwr6";
var reg = /[a-zA-Z](?=\d+)/g; //意思为判断这个字符后面是否有一个或多个数字
var result;
while(result = reg.exec(str)){
    console.log(result[0], result[1]);
}
> "f" undefined
  "f" undefined
  "g" undefined
  "r" undefined
```
###### 20.10.5.8反向预查
正向预查找的是满足的，反向预查则不满足
语法：```(?!\d+)```

#### 20.11错误处理

| 语法错误 | SyntaxError    | 这个代码块不会运行       |
| -------- | -------------- | ------------------------ |
| 运行错误 | ReferenceError | 运行到这一行不会往下运行 |

##### 20.11.1抛出错误
当我们的用户使用我们的函数时，我们发现他的这个参数不对劲(或者其他)说明我们这里绝对要出问题，那么我们就可以给他抛出一个错误
语法：```throw new Error("错误提示信息")```
示例：
```js
function a(n){
    if(isNaN(n)){
        throw new Error("n为一个非正常的数字");
    }
}
a("asdas")
> Uapr Error : n为一个非正常的数字  index.js:36
```

错误堆栈：
```js
function a(n){
    if(isNaN(n)){
        throw new Error("n为一个非正常的数字");
    }
}
function b(){
    a();
}
b();

错误堆栈信息:  从上往下丢  a发生了错误丢给b，b解决不了丢给全局全局解决不了丢给浏览器，浏览器将错误显示出来
    at a()
    at b()
    at index.js
    浏览器
```
我们还可以抛出别的类型的错误：比如ReferenceError这些都是运行时错误

##### 捕获并解决错误
try{//捕捉到错误丢给catch的形参

}catch(错误对象){//进行解决

}finally{//必须会执行

}
如果我们用try把错误处理了，那么我们这后面的就相当于没有发生错误一样继续执行，也就是我们上面的a把错误丢给b，而我们在b的捕捉到错误并解决了，那么b的后面的语句同样能执行
尽管我们的catch想要跳出这个函数，我们的finally一样要执行，不过我们的finally return的就不是undefined了而是catch return的内容

### console.dir(对象)可以查看这个对象的结构(内容)

### 21.DOM
> 又名：WebApi
> WebApi由W3C制定,ES由ECMA制定

关于DOM：

- DOM 0
- DOM 1
- DOM 2
- DOM 3
- DOM 4  2015年(ES6也是这一年发布的)

DOM的核心理念，是将一个HTML或XML文档，用对象模型表示，每个对象称之为dom对象

dom对象又称之为节点Node

节点的类型：

- DocumentType，文档类型节点 ```<!DOCTYPE html>```
- Document，文档节点，表示整个文档
- Comment，注释节点
- Element，元素节点
- Text，文本节点
- Attribute，属性节点
- DocumentFragment，文档片段节点

dom树：文档中不同的节点形成的树形结构。

> window中有一个属性document,代表整个文档节点
> 在DOM中获取的元素数组大多数都是类数组

#### 21.1获取元素节点

> 元素节点也称为元素对象
> 浏览器控制台为了我们查看方便将元素对象以标签的形式展示给我们
> 我们可以通过console.dir(document.getElementById("a"));
> \>div#a
> 对象内由很多属性和方法

**旧的获取元素节点的方式：**
DOM 0:
- documents.body 获取body元素节点

**新的获取元素节点的方式：**
通过方法获取：
- document.documentElement 获取根元素 HTML
- document.getElementById(); 通过ID获取元素节点
- 通过标签名获取元素节点
- 通过class名获取元素节点 `IE9以下无效`
- document.getElementsByName(); 通过name属性值获取元素
- document.querySelector(); 通过CSS选择器获取元素，得到匹配元素的第一个因为他不是类数组 `IE8以下无效`
- document.querySelectotAll(); 通过CSS选择器获取元素，这个返回的就是一个类数组，所以它可以获取到满足这个CSS选择器的所有元素`IE8以下无效,且它的类数组不是实时更新的`
后期通常使用下面两个和ById其他则不会经常使用

**细节问题：**
1. 上面得到类数组的方法中，querySelectorAll的类数组不是实时更新的
2. 浏览器会将带有id属性的元素放到window对象里面，而且这个属性是实时的，所以就会导致污染全局变量，如果我们使用这种方式来获取元素的话，如果我们重新定义了一个和这个同名的变量的时候我们就会出现问题
3. getElementsByTagName,getElementsByClassName,querySelector,querySelectorAll,可以作为其他元素节点对象的方法使用 ```var ul = document.getElementsByTagName("ul"); ul.getElementsByTagName("li")```

通过**节点**获取**节点**：
1. 节点.parentNode 获取这个节点的**父节点** `（元素，文档类型）`
2. 节点.previousSibling 获取这个节点的**上一个兄弟节点** `注意文本节点`
3. 节点.nextSibling 获取这个节点的**下一个兄弟节点**
4. 节点.childNodes 获取这个节点的所有子节点 `包含文本节点`
5. firstChild 获取第一个子节点 `包含文本节点`
6. lastChild 获取最后一个子节点 `包含文本节点`

***获取元素节点：**
1. parentElement 获取这个节点的父元素 `他获取不到文档类型 <!DOCTYPE html>`
2. 节点.previousElementSibling 获取上一个兄弟元素
3. nextElementSibling 获取下一个兄弟元素
4. children 获取子元素
5. firstElementChild 获取第一个子元素
6. lastElementChild 获取最后一个子元素
7. attributes 获取某个元素的属性节点 `返回值为 类数组`

#### 21.2获取节点信息
> 文档类型的nodeName为“html”表示我们这个文档类型是html文档
> 元素的nodeName通常为全大写“HTML”“BODy”

1. nodeName 获取这个节点的名字
2. tagName 获取元素名称
3. nodeValue 获取节点的值 `通常拿来获取属性的值`
4. nodeType 获取这个节点的类型

#### 21.3DOM元素操作

> 可识别属性：```<input type="text" value="avas"/>``` 在input标签中添加的value属性是他这个input标签里面本来就有的属性
> 自定义属性：```<div value="afsf"/>``` 在div这个元素对象中并没有value这个属性而是你自己给他加上的，这个就叫自定义属性

##### 21.3.1可识别属性

> 没有给可识别属性赋值他也有默认值，类似input的value属性你没有赋值它的默认值为""空串
> 布尔属性在DOM对象中得到的是Boolean类型的值 类似于复选框的cheacked="cheacked"他得到的是true
> 获取下拉列表的内容值的方法：通过节点获取
> select.value 可以获取选中的option的value
> 某些表单元素可以获取未设置的属性的值
> 某些属性与保留字或者关键字相冲突，我们则在他前面加个html然后加属性名就好了
类似于class值 和 label标签里面的for 都需要使用className 或者htmlfor

可以通过 `元素对象.属性` 的方式获取这个属性的值
示例：
```html
<input type="text" value="afa"/>
```
```js
console.log(input.value);
> "afa"
```

##### 21.3.2自定义属性

> 自定义属性的值无法和可识别属性一样通过元素对象.的方式获取
> 自定义属性执行使用通用获取属性的方法获取值.
> H5建议自定义属性前面以“data-”开头

**强烈推荐使用：**
**如果遵从了H5的建议的话，我们可以通过 ```元素对象.dataset``` 返回由自定义属性组成的类数组，我们可以通过这个获取自定义属性的值也可以设置值**

通用获取属性方法：
- getAttribute("属性名"); 获取属性值
- setAttribute("属性名"); 设置属性值

示例：
```html
<div value="data-afa"></div>
```
```js
console.log(div.value);
> undefined
console.log(div.getAttribute("value"));
> "afa"
```

**删除自定义属性：**
1. 元素对象.removeAttribute("data-abc");
   那么这个元素对象的自定义属性就被删除掉了
2. delete ul.dataset.自定义属性名
   那么这个自定义属性就没了 `强烈推荐`


##### 21.3.3获取和设置元素内部内容

- innerText 只能获取元素显示出来的文本，如果在他的内部写入Html代码的话它会自动给你转化成&lt这种类型的html实体化 
- innerHTML 获取元素内部HTML代码
- textContent 获取和设置元素内部源代码的纯文本

##### 21.3.4元素结构重构

###### 21.3.4.1appendChild方法
语法：```父元素对象.appendChild(元素对象b)```
作用：将**元素对象b剪切**到**父元素对象**的**最后一个子元素处**
> 不能一次性添加多个元素对象

###### 21.3.4.2insertBefore方法
语法：```父元素对象.insertBefore(待插入的元素对象, 哪个子元素之前(也可以是节点))```
作用：将**待插入的元素对象**插入到**父元素对象**的**哪个子元素之前(也可以是节点)**

插入到哪一个元素之后：
```父元素对象.insertBefore(待插入的元素对象, 哪个子元素之前.nextElementSibling(也可以是节点))```

> 如果第二个参数为null则插入到最后

###### 21.3.4.3replaceChild方法
语法：```父元素对象.replaceChild(待替换的元素对象, 替换哪个子元素)```
作用：会将**待替换的元素对象**与**父元素对象**中的**替换哪个子元素**进行替换，替换之后**替换哪个子元素**会销毁

**细节：**
元素结构重构效率较低

##### 21.3.5创建和删除元素

###### 21.3.5.1创建元素

- document.createElement("标签名") : 创建一个元素对象
- document.createTextNode("文本内容") : 创建一个纯文本
- document.createDocumentFragment() : 创建文档片段
  因为我们如果创建一个元素我们就往页面里面加的话这样相当于重构了创建个次数，所以我们为了提高页面效率，我们可以把创建好的元素添加到fragment文档片段中，它就相当于是一个来装我们即将要添加到页面中的元素的**容器**一样，然后我们再一次将fragment添加到页面中这样我们就才只重构了1一次页面，效率提高了创建个数-1倍呢
  示例:
  ```js
  var fragment = document.createDocumentFragment();
  for(var i = 1; i <= 100; i++){
      var li = document.createElement("li");
      li.innerText = "这是第" + i + "个li";
      fragment.appendChild(li);
  }
  ul.appendChild(fragment);
  ```
  这样我们就一次把创建的元素就都加进去了

###### 21.3.5.2克隆元素
- dom对象.cloneNode(是否深度克隆) : 复制一个新的对象返回
  如果不填参数则是浅度克隆也就是生成一个一模一样的元素对象内容不会被克隆到
  如果传了true则是深度克隆，它的所有内容都会克隆过来

> childNodes也是实时的

###### 21.3.5.3删除元素

谋杀：
父元素.removeChild(想要谋杀的子元素对象); `他只是在页面上没有了不过这个变量还是拿着这个元素对象的，再想的时候可以再加回去`

自杀：
想要删除的元素.remove();

#### 21.4DOM元素样式

##### 21.4.1控制DOM元素的类样式

- classList : 类样式组成的类数组
  - contain : 用于判断一个类样式是否存在
  - toggle : 用于添加/删除一个类样式 ```div.classList.toggle("类名")```如果已经拥有这个元素，那么将其删除，如果没有则添加进去

##### 21.4.2DOM元素的类样式

- getComputedStyle(元素对象) : 获取最终计算后的结果的对象 我们需要接收
  - 可以填第二个参数，获取伪元素样式 ```getComputedStyle(div, "before").content       >""```
- 元素对象.style : 获取的结果是我们在style标签中声明的样式，并不是计算后的结果
- 如果getComputedStyle兼容不了则使用这个：dom.currentStyle[样式属性]

#### 21.5DOM事件

##### 21.5.1事件流

> 事件流看的事元素结构，并不是视觉效果

**事件冒泡**：先触发最里面的元素，然后再触发外层元素
**事件捕获**：先触发外层的元素，然后再往里面触发元素，触发直到我们点击的那个元素为止，不再往里触发

> 目前标准规定，默认情况下为事件冒泡
> 事件源、事件目标：我们点击的那个元素，如果是事件冒泡则是最开始的那个元素，如果是事件捕获则是最后面的那个元素

![事件流流程图](C:/Users/Administrator/Desktop/桌面/干/袁老师/袁老师js源码/JavaScript/8. dom事件/1. 基础概念/事件流.jpg)

##### 21.5.2事件绑定/事件注册

DOM 0:
元素对象.on事件名称 = function (){}

移除：给事件重新赋值 `null/undefined`

DOM 2:
dom对象.addEventListener("事件名 `click` 无需添加on", 事件函数, 是否在捕获阶段触发) : 注册事件

与DOM 0的区别：

1. dom2可以为某个元素的同一个事件，添加多个处理程序，按照注册的先后顺序来依次执行
2. dom2允许开发者控制事件流类型是冒泡还是捕获 `true则是在捕获阶段触发` 则该函数在事件捕获时就会触发
3. 如果将其变成事件捕获的这个元素是事件目标阶段，则没有必要添加事件捕获了，因为执行到他的时候剩下的只有事件冒泡了

移除: dom对象.removeEventListener("事件 `click`", 需要移出的函数, [如果时捕获的函数则需要添加true]);

我们移出函数需要时命名函数否则无法获取就无法删除

细节：

- dom2在IE8及以下不兼容
- 我们可以在DOM2的第三个参数传入一个对象来配置一些东西
  ```js
  div.addEventListener("click", function (){}, {
      once : true; //表示这个处理函数只执行一次
      captrue : true; //表示这个函数在捕获阶段运行
  })
  ```

#### 21.6事件对象
事件对象封装了事件的相关信息

##### 21.6.1获取事件对象
1. 通过事件处理函数的参数获取
   语法：```div.onclick = function (e){}```浏览器会自动给你传一个这个事件触发时的事件对象
2. 旧版本IE使用```window.event```获取
   我们通常这样来进行兼容：
   ```js
   div.onclick = function (e){
       e = e || window.event;
   }
   ```

##### 21.6.2事件对象的通用成员

- target & srcElement(IE)
  事件目标(事件源对象)，也就是事件目标阶段的那个元素
  事件委托：
  通过给祖先元素注册事件，在程序处理程序中判断事件源对象，执行不同的处理
  通常用于：
  动态生成元素的区域，因为你这个区域的子元素是动态生成的。那么如果你用循环去给他一个一个绑定，只要你新添加了一个你就得重新绑定，所以我们这里用事件源对象会方便和快捷很多
- currentTarget
  当前目标，获取绑定事件的元素 **和事件处理函数里的this是同一个东西**
  ```js
  div.onclick = function (e){
      console.log(this === e.currentTarget);// true
  }
  ```
- type 获取事件的类型 点击事件：`click`
  ```js
  div.onclick = function (e){
      console.log(e.type);//click
  }
  ```
- preventDefault方法 & returnValue(IE)(非标准) 阻止浏览器默认行为
  例如：a元素你给他一个地址它会进行页面跳转，而我们如果在点击事件把它的默认行为给阻止了那么它就无法跳转了：
  ```js
  a.onclick = function (e){
      e.preventDefault();
      console.log("此时页面不会进行跳转");
  }
  ```
  DOM 0方式绑定事件可以通过 `return false` 来取消它的默认行为 **必须return false**
  因为a元素的href为功能型链接所以我们可以添加Javascript代码来阻止它的默认行为 ```<a href="javascript:;"></a>```
- *stopPropagation方法 : 阻止事件**冒泡到当前元素时不再继续往上冒泡**
  ```html
  <div id="div1">
      <div id="div2">
          <div id="div3">
              <div id="div4">

              </div>
          </div>
      </div>
  </div>
  ```
  ```js
  div1.onclick = div3.onclick = div4.onclick = function (e){
      console.log(this);
  }
  div2.onclick = function (e){
      e.stopPropagation();
  }
  > div4 div3
  ```
- eventPhase
  1:事件捕获
  2:事件阶段
  3:事件冒泡
  ```js
  div.onclick = function (e){
    console.log(e.eventPhase);// 2
  }
  ```

#### 21.7事件类型

##### 21.7.1鼠标事件
- click：用户单击主鼠标按钮（一般是左键）或者按下在聚焦时按下回车键时触发
- dblclick：用户双击主鼠标按键触发（频率取决于系统配置）
- mousedown：用户按下鼠标任意按键时触发
- mouseup：用户抬起鼠标任意按键时触发
- mousemove：鼠标在元素上移动时触发
- mouseover：鼠标进入元素时触发
- mouseout：鼠标离开元素时触发
- mouseenter：鼠标进入元素时触发，该事件不会冒泡
- mouseleave：鼠标离开元素时触发，该事件不会冒泡

*区别：

- over和out，不考虑子元素，从父元素移动到子元素，对于父元素而言，仍然算作离开
- enter和leave，考虑子元素，子元素仍然是父元素的一部分
- mouseenter和mouseleave不会冒泡
  e.bubbles返回这个事件是否冒泡

###### 21.7.2MouseEvent事件对象
所有的鼠标类型的事件，触发的事件对象都是MouseEvent


`e.altkey` 
- altKey：触发事件时，是否按下了键盘的alt键
- ctrlKey：触发事件时，是否按下了键盘的ctrl键
- shiftKey：触发事件时，是否按下了键盘的shift键
- button：触发事件时，鼠标按键类型 (如果是鼠标移动事件的话则一直都是0)
  - 0：左键
  - 1：中键
  - 2：右键
  

位置：
`e.pageX`
- page：pageX、pageY，当前鼠标距离页面的横纵坐标(鼠标坐标，鼠标相对于整个页面的坐标)
- client: clientX、clientY，鼠标相对于视口的坐标(鼠标相对于单频页面的坐标，不管滚动条)
- offset：offsetX、offsetY，鼠标相对于**事件源**的内容区域的坐标(注意观察当前事件源(e.target)是谁)
- screen: screenX、screenY，鼠标相对于屏幕
- x、y，等同于clientX、clientY
- movement：movementX、movementY，只在鼠标移动事件中有效，相对于上一次鼠标位置，偏移的距离

拖拽效果：
```js
var div = document.querySelector("div");
var style = getComputedStyle(div);
var divLeft = parseFloat(style.left);
var divTop = parseFloat(style.top);
div.onmousedown = function (e){
    if(e.button != 0){
        return;
    }
    window.onmousemove = function (e){
        divLeft += e.movementX;
        divTop += e.movementY;
        div.style.left = divLeft + "px";
        div.style.top = divTop + "px";
    }
    window.onmouseup = window.onmouseleave = function (e){
        if(e.button == 0){
            window.onmousemove = null;
        }
    }
}
```
##### 21.7.3键盘类型事件
keydown、keypress 如果阻止了事件默认行为，文本不会显示：
在键盘类事件的keydown/keypress的结尾加上return false可以阻止这个字母的打出，通常我们用来制作只能输入数字或者字符的效果
```js
input.onkeydown = function (e){
    return false;/e.preventDefault();
}//此时这个文本框无法输入任何东西
```
###### 21.7.4keyboardEvent事件对象
keyboardEvent:
- code：得到按键字符串，适配键盘布局。
  ```js
  input.onkeypress = function (e){
      console.log(e.code);//当我按下a > KeyA(不区分大小写都是KeyA)
      //如果是shift键则返回ShiftLeft
  }
  ```
- key：得到按键字符串，不适配键盘布局。能得到打印字符。
  ```js
  input.onkeypress = function (e){
      console.log(e.key);//当我按下a > a(区分大小写)
      //如果是A键则返回A
      //如果是ctrl键则返回ctrl的全称
  }
  ```
- keyCode、which：得到键盘编码
  他不管你按的是大写还是小写返回的就是这个按键的编码

##### 21.7.5表单事件
- focus：元素聚焦的时候触发（能与用户发生交互的元素，都可以聚焦），该事件不会冒泡
- blur：元素失去焦点时触发，该事件不会冒泡。
- submit：提交表单事件，仅在form元素有效。
  通常用于表单验证，我们加上这个事件当表单要提交的时候只要不满足我们里面的条件我们就把它的默认事件给他取消掉，这样他就提交不了了
  ```js
  form.onsubmit = function (e){
      不满足条件：return false;
  }
  ```
- change：文本改变事件
  Select下拉列表的属性：
  - selectedIndex ：获取当前选项的下标
  - sel.options ：返回一个伪数组，这个伪数组内装有所有的option选项
  他们两个可以组合起来用:```sel.potions[selectedIndex]```
- input: 文本改变事件，即时触发
  只要我们输入一个东西他就会触发
  通常用来做用户输入提示，只要不满足我们就直接进行相关性操作
  他是在文本改变后才触发的

##### 21.7.6window全局对象
- load、DOMContentLoaded、readystatechange

window的load：页面中所有资源全部加载完毕的事件
图片的load：图片资源加载完毕的事件

> 浏览器渲染页面的过程：
> 1. 得到页面源代码
> 2. 创建document节点
> 3. 从上到下，将元素依次添加到dom树中，每添加一个元素，进行预渲染
> 4. 按照结构，依次渲染子节点

图片资源和音频等资源是异步的，而js资源和css资源是同步的

- document的DOMContentLoaded: dom树构建完成后发生(JQ就是用的这个事件)
  - 此事件无法使用DOM0的事件注册绑定，因为这个事件比较新，只能使用DOM2的事件注册方法addEventListener("DOMContentLoaded", function (){})
  - dom树构建完成只是dom树构建完成并不是图片和一些外部资源全部加载完成

- *readystate: **返回：** interactive(dom树全部构建完成,触发DOMContentLoaded)、loading(正在加载其他资源)、complete(全部加载完成，触发load事件) **: 网页的三种状态**

- readystatechange : 当状态发生改变时触发

- interactive：触发DOMContentLoaded事件

- complete：触发window的load事件

**js代码应该尽量写到页面底部**

1. css应该写到页面顶部：避免出现闪烁（如果放到页面底部，会导致元素先没有样式，使用丑陋的默认样式，然后当读到css文件后，重新改变样式）
2. JS应该写到页面底部：避免阻塞后续的渲染，也避免运行JS时，得不到页面中的元素。




- **unload、beforeunload**

beforeunload: window的事件，关闭窗口时运行，可以阻止关闭窗口(新版谷歌已经不允许阻止关闭窗口了，所以我们通常用来告诉服务器我们这个窗口已经关闭了)：
如何使用(现在都不行了)：
```js
window.onbeforeunload = function (){
    return "你确定要关闭此页面吗？" // 浏览器就会自动弹出一个框框来现实你的话，并且拥有取消和确定
}
```

unload：window的事件，关闭窗口时运行

- **scroll**

> 可以给出现滚动条的元素添加这个样式也会触发这个事件


窗口发生滚动时运行的事件

通过scrollTop和scrollLeft，可以获取和设置滚动距离。

获取浏览器的滚动条距离：
```js
拥有兼容性问题(一个为滚动条距离一个为0，不同浏览器不同)：
document.documentElement.scrollTop / document.body.scrollTop
通常我们将两个相加：
window.onscroll = function (){
    console.log(document.documentElement.scrollTop + document.body.scrollTop);
}
```

- resize

窗口尺寸发生改变时运行的事件，监听的是视口尺寸

- contextmenu

右键菜单事件

我们可以通过阻止这个事件的默认行为来阻止产生菜单
```js
div.oncontextmenu = function (e){
    e.preventDefault();
}
```

- paste

粘贴事件

- copy

复制事件

**用于防止用户复制和粘贴，这两个事件是在复制和粘贴时触发的，我们只要把它的默认事件阻止掉它就无法进行复制和粘贴了**

- cut

剪切事件

获取复制白板的文本内容：
```var text = e.clipboardDate.getDate("text/plain");```

![尺寸1](../笔记图片(勿删)/尺寸1.png)

![尺寸2](../笔记图片(勿删)/尺寸2.png)

![尺寸3](../笔记图片(勿删)/尺寸3.png)

![尺寸4](../笔记图片(勿删)/尺寸4.jpg)

##### 21.7.7补充知识
**元素位置**

- offsetParent

获取某个元素第一个定位的祖先元素，如果没有，则得到body

body的offsetParent为null

- offsetLeft、offsetTop

相对于该元素的offsetParent的坐标

如果offsetParent是body，则将其当作是整个网页

- getBoundingClientRect方法

  ![rect](../笔记图片(勿删)/rect.png)

该方法得到一个对象，该对象记录了该元素相对于视口的距离![批注 2020-05-10 133535](../笔记图片(勿删)/批注 2020-05-10 133535.jpg)

案例：
1. 获取这个元素在整个浏览器内的位置：
   ```js
   function getPagePosition (dom){
       var left = dom.offsetLeft;
       var top = dom.offsetTop;
       var prent = dom.offsetParent;
       while(prent){
           left += parent.offsetLeft;
           top += parent.offsetTop;
           prent = prent.offsetParent;
       }
       return {left : left, top : top};
   }
   ```

**事件模拟**
模拟事件触发
方法：
- click
- sumbit
  ```js
  form.submit();
  ```
- dispatchEvent
  给DOM元素添加一个事件对象,就相当于触发了这个事件
  ```js
  var event = new MouseEvent("mouseenter", {
      bubbles:false
  })
  div.dispatchEvent(event);
  ```

**其他补充**

- window.scrollX、window.pageXOffset、window.scrollY、window.pageYOffset

window.scrollX、window.pageXOffset: 相当于根元素的scrollLeft

window.scrollY、window.pageYOffset: 相当于根元素的scrollTop

- scrollTo、scrollBy
  ```js
  scrollTo(x,y) : scrollTo(100, 100);
  scrollBy(100, 100);
  ```
scrollTo: 设置滚动条位置 绝对的位置
scrollBy: 相对于原来的滚动条位置加多少

- resizeTo、resizeBy

### 22.BOM

详情BOM请看BOM(2).pdf文档

 [BOM(2).pdf](E:\渡一\渡一\渡一前期公益课资料\BOM(2).pdf) 

#### 22.1递归settimout
```js
function setIntval(callBack, time){
    stm = setTimeOut(function (){
        callBack();
        setIntval(callBack, time);
    }, time);
}
```
#### 22.2window对象
##### 自身方法
window.open()
- open

打开一个新窗口

open("页面路径", "打开目标(_self/_blank)", "配置")

- alert
- confirm
- prompt


##### 对象属性

- document
  document.write
  在当前文档流中写入内容，如果当前文档流不存在，则新开一个文档流

- location：地址栏对象![location](../笔记图片(勿删)/location.jpg)

**search部分也就是?后面的东西也就是表单提交的数据**

href属性：得到目前地址
其他属性参考location.jpg

reload方法：刷新当前页面

- navigator
  
  ![navigator](../笔记图片(勿删)/navigator.jpg)
  
  他都是骗你的，因为这些触犯了用户隐私了
  
- history：历史记录

  go方法 让页面前进
  back方法 让浏览器后退
  forword方法 正数是前进，负数是后退

- console

  log方法：打印对象的valueOf的返回值
  dir方法：打印对象结构
  tiem方法和timeEnd方法：用于计时   某一段代码的运行时间
  他们可以加一个参数表示名字，这样就能表示他们是一对的

#### 22.3浏览器嗅探

```js
navigator.appVersion
> "5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36"
```

### 23.原型和原型链

**Function函数是JS引擎在运行的时候就被放到内存里面了的，并不是别人构造出来的**

**其他所有的函数也就是对象都是通过new Function()来创建的，因为Object他也就是一个构造函数**

**Object也是Function创建的，所以它的__proto__是Function.prototype，又因为prototype是一个对象也就是new Object()，所以Function的prototype的__proto__是Object的prototype，Object的prototype的__proto__为null**

**因为Function是JS引擎给的所以他的__proto__没有办法指向别人所以它就指向自己自己是自己的父亲**

![链条的全貌](../笔记图片(勿删)/链条的全貌.jpg)

![函数是通过new Function创建的](../笔记图片(勿删)/函数是通过new Function创建的.jpg)

![每个函数都有原型对象](../笔记图片(勿删)/每个函数都有原型对象.jpg)

![普通对象是通过new 函数创建的](../笔记图片(勿删)/普通对象是通过new 函数创建的.jpg)

![原型中的constructor指向函数本身](../笔记图片(勿删)/原型中的constructor指向函数本身.jpg)

![隐式原型的指向](../笔记图片(勿删)/隐式原型的指向.jpg)

- 所有对象都是通过```new 函数```创建
- 所有的函数也是对象
  - 函数中可以有属性
- 所有对象都是引用类型

```js
function A(){}
var obj = new A();
obj.__proto__ === obj.prototype
```

#### 23.1原型

所有函数都有一个属性：prototype，称之为函数原型

默认情况下，prototype是一个普通的Object对象

默认情况下，prototype中有一个属性，constructor，它也是一个对象，它指向构造函数本身。

#### 23.2隐式原型__proto__

所有的对象都有一个属性：```__proto__```，称之为隐式原型

默认情况下，隐式原型指向创建该对象的函数的原型。

当访问一个对象的成员时：

1. 看该对象自身是否拥有该成员，如果有直接使用
2. 在原型链中依次查找是否拥有该成员，如果有直接使用

猴子补丁：在函数原型中加入成员，以增强起对象的功能，猴子补丁会导致原型污染，使用需谨慎。

#### 23.3原型链

特殊点：

1. Function的__proto__指向自身的prototype
2. Object的prototype的__proto__指向null

#### 23.4原型链的应用

##### 23.4.1基础方法

W3C不推荐直接使用系统成员__proto__

**Object.getPrototypeOf(对象)**  ```=== 对象.__proto__```

获取对象的隐式原型

**Object.prototype.isPrototypeOf(对象)**

判断当前对象(this)是否在指定对象的原型链上

任何对象的最终父亲都是Object.prototype所以返回```true```

```js
var obj = {};
Function.prototype.isPrototypeos(obj);
> false
```

**对象 instanceof 函数**

判断函数的原型是否在对象的原型链上

```js
var obj = {};
obj instanceof Object
> true
```

**Object.create(对象)**

创建一个新对象，其隐式原型指向指定的对象

```js
var p = {x:1,y:33}
var obj = Object.create(p);//相当于就是obj的隐式原型(```__proto__```)为p
Object.getPrototypeOf(obj) === p
> true
Object.getPrototypeOf(p) === Object.prototype
> true
```

> 因为我们这是将p这个对象直接作为obj的```__proto__```而p这个对象内并没有constructor,所以我们这么操作的后果就是这个obj的```__proto__```没有constructor

```js
var obj = Object.getPrototypeOf(null);
```
这样我们的obj就相当于Object.prototype一样了,obj就没有任何继承
**所以不一定每一个对象的隐式原型最终都指向Object.prototype，因为有了Object.getPrototypeOf()的出现它的隐式原型```__proto__```可以为null了**

**Object.prototype.hasOwnProperty(属性名)**

判断一个对象**自身**是否拥有某个属性

```js
var p = {x:1,y:33}
var obj = Object.create(p);
obj.a = 123
for(var prop in obj){
    console.log(prop);
}
> x y a
for(var prop in obj){
    if(obj.hasOwnProperty(prop)){
        console.log(prop);
    }
}
> a
```

##### 23.4.2应用

**类数组转换为真数组**

```js
Array.prototype.slice.call(类数组);
```

**实现继承**

默认情况下，所有构造函数的父类都是Object

现在(es5,es6)的圣杯模式写法:
```js
Object.prototype.inherit = function (father, son){
    son.prototype = Object.create(father.prototype);//此时由father.prototype创建的对象内并没有constructor，所以我们自己创建一个constructor指向son
    son.prototype.constructor = son;
    son.prototype.uber = father.prototype;
}
```
### 24.属性描述符(访问器属性)

属性描述符的配置参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty

属性描述符：它表达了一个属性的相关信息（元数据），它本质上是一个对象。

1. 数据属性
   我们在这之前使用的都是数据属性
   ```js
   var obj = {
       a:1//数据属性
   }
   obj.b = 1;//数据属性
   ```
   
   1. 存取器属性(访问器属性)	
   2. 当给它赋值，会自动运行一个函数
   3. 当获取它的值时，会自动运行一个函数

默认情况下对象的属性为数据属性
如何赋值存取器属性：**Object.defineProperty(obj,prop,配置)**

![批注 2020-05-12 141122](../笔记图片(勿删)/批注 2020-05-12 141122.jpg)

```js
var obj = {};

//第一种错误情况
Object.defineProperty(obj,"x", {
    x : 1,//这样子写依然是数据属性，相当于：obj.x = 1;
})

//第二种错误情况
Object.defineProperty(obj,"x",{
    x : 1,
    get : function (){

    },
    set : function (){

    }
})
//加上了get和set属性就表示这个属性x为存储器属性了，存储器属性是不能被 x:1 这样直接赋值的，如果这样子写就会报错

//正确情况
Object.defineProperty(obj, "x", {
    get : function (){

    },
    set : function (val){

    }
    //当我们获取x属性的值时，他就会执行get这个函数，将get函数的返回值变为属性x的值展示给用户，当我们设置x属性的值时，它会执行set函数，通常我们都会加上一个参数val，这样我们写obj.x = 3时就相当于set (3)
})
```

**应用场景：**
**1.**
处理细节：
1. 防止我们的用户直接将这个构造函数构造出来的对象的age属性直接进行赋值，user.age = 10000;这样就会避开我们在构造对象时的判断，所以我们就会使用Object.defineProperty()，来将age属性变成一个存储器属性，这样就算你直接对构造出来的对象的age属性进行赋值他也会执行set函数进行判断
```js
function User(name, age){
    this.name = name;
    //年龄的取值范围是0~100
    //如果年龄的值小于了0，则赋值为0，如果年龄的值大于了100，则赋值为100
    var _age;
    Object.defineProperty(this, "age", {
        get : function (){
            return _age;
        },
        set : function (val){
            if(val < 0){
                val = 0;
            }else if(val > 100){
                val = 100;
            }
            _age = val;
        }
    })
}
```

**2.**
我们在写一个DOM元素时，为什么我们只要填了一个值给他，它就进行了相关的页面变化，并且如果我们的值给错了他还不给我们变化，因为这些属性其实是一个存储器属性，当我们在给他赋值时，他在set函数内就做了一大堆操作，而我们只要轻轻设置一下属性就好了,还有我们获取值的时候为什么是实时的值，而不是静态的值，也正是因为我们也设置了get函数

相关属性:DOM.innerText、DOM.style.background.color = "green"...

**其他的属性描述符：**
**configurable**
当且仅当该属性的 configurable 键值为 true 时，该属性的描述符才能够被改变，同时该属性也能从对应的对象上被删除。
默认为 false。

> 默认为false时这个属性无法delete
> 我们得把这个属性的配置内加上configurable : true此时这个属性则可以被删除

**writable**
当且仅当该属性的 writable 键值为 true 时，属性的值，也就是上面的 value，才能被赋值运算符改变。
默认为 false。

将这个属性变为无法赋值的常量:
```js
var obj = {};
//第一种方法
Object.defineProperty(obj, "a", {
    get : function (){
        return "abc";
    }
})
//第二种方法
Object.defineProperty(obj, "a", {
    value : "abc",
    writable : false//默认也为false
})

如何设置为可赋值的变量：
Object.defineProperty(obj, "a", {
    value : "abc",
    writable : true//默认也为false
})
```

**enumerable**
当且仅当该属性的 enumerable 键值为 true 时，该属性才会出现在forin循环的属性中。
默认为 false。

```js
var obj = {
    x : 1,
    y : 2
}
Object.defineProperty(obj, "a", {
    value : 3,
    enumerable : false
})
for(var prop in obj){
    console.log(prop);
}
> x y

这也就是为什么Object里面有那么多的东西，我们遍历不出来的原因
```

**Object.getOwnPropertyDescriptor**

获取某个对象的某个属性的属性描述符对象（该属性必须直接属于该对象）获取的也就是我们Object.defineProperty()的第三个参数内容(配置系统会有給我们设置默认值，尽管我们没有给他进行配置)
他只能找自身的属性

```js
var obj = {
    x:1,
}
Object.defineProperty(obj, "name", {
    value : 2,
    enumerable : false,
})
console.log(Object.getOwnPropertyDescriptor(obj, "name"));
> Object
  configurable: false
  enumerable: false
  value: 2
  writable: false
  __proto__: Object
console.log(Object.getOwnPropertyDescriptor(obj, "x"));
> configurable: true
  enumerable: true
  value: 1
  writable: true
  __proto__: Object
```

### 25.事件循环

异步：某些函数不会立即执行，需要等到某个时机成熟后才会执行，该函数叫做异步函数。 (事件函数、定时器函数...)

浏览器的线程：

1. JS执行引擎：负责执行JS代码
2. 宿主环境：
3. 渲染线程：负责渲染页面
4. 计时器线程：负责计时
5. 事件监听线程：负责监听事件
6. http网络线程：负责网络通信

事件队列：一块内存空间，用于存放执行时机到达的异步函数。当JS引擎**空闲**（执行栈没有可执行的上下文），**它会从事件队列中拿出第一个函数执行**。

事件循环：event loop，是指函数在执行栈、宿主线程、事件队列中的循环移动。

**JS代码在执行时时不可能被别的异步代码打断的，它会被放在事件队列中去，然后当JS空闲时才会来依次执行事件队列中的事件**

### 26.对象混合
```js
{
    a:1,
    b:2
}
{
    c:"asda",
    a:"asdas"
}
第二个混合到第一个
{
    a:"asdas",
    b:2,
    c:"asda"
}
```
**Object.assign()静态方法**
可以将我们的对象进行混合，他支持多个参数(obj1, obj2, obj3);
从右往左混合
它有一个缺陷，就是最终的结果返回的是第一个参数，也就是它会更改第一个参数的内容
所以我们通常这么写({}, obj1, obj2);

**属性 in 对象判断这个属性是否在这个对象中**

使用场景：
设置默认值
```js
//我们要传一个对象进来，可是这个对象可能有些配置没有给值，那么我们就得给他设置默认值，这个时候就用到我们的对象混合
function complicate (option){
    var default = {
        a:"default-a",
        b:"default-b",
        c:"default-c",
        d:"default-d"
    }
    console.log(Object.assign(default, option));
}
complicate({
    a:1,
    b:2,
})
> {
    a:1,
    b:2,
    c:"default-c",
    d:"default-d"
}
```

### 26.函数防抖和节流
Date.now()可以快速获得当前的时间戳