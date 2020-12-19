# es6
[toc]
## 1.变量提升问题(let)

我们使用在es6之前的版本的JS的时候我们会发现它会进行一个变量提升，而当我们的项目量一大的时候我们就很有可能会**变量名覆盖导致预期效果不同**，于是我们es6就对其进行了一个改进：

使用 `let` 声明变量：

1. 此变量不会被挂载到window上

2. 不会进行变量提升

3. 它的作用域变成了和高层语言一致的作用域了(例如：Java)

   ```js
   for(let i = 0; i < 3; i++){
      console.log(i);
   }
   console.log(i);
   ```

   ![批注 2020-09-03 161622](http://note.youdao.com/yws/public/resource/fe3310355b82edd44cc8055926dc461f/xmlnote/A836E4D4EEF44906940E7442143F2838/8447)

   **它会给我们进行报错提示了！！！！**

4. 不允许在相同作用域内重复声明一个变量名

   否则：会报错提示
   
5. 拥有**块级作用域**

   ```js
   let a = 10;
   {
       let a = 100;//在块级作用域
       console.log(a);
   }
   console.log(a);
   //-----------------------
   100
   10
   ```

   **{块级作用域开始，}块级作用域结束**

   **尽管是在if的{}中它也算是一个块级作用域，我们在if{}中定义的let变量在{}外访问不到**

6. 其实**let**也会进行一个**提升**，只不过程序会将他在**执行到定义它的那一行代码之前先放入到“暂时性死区”中**，如果我们**访问的变量在”展示性死区“中**那么就会报这个错误：”**Cannot access 'xx变量' before initialization**“，而并不是我们想象中的”**xx变量 is not defined**“(**这是底层的代码了**)，当程序**执行到定义它的那一行代码时**，才会将它从”展示性死区“中**移除**拿**出来到当前作用域中**

   ```js
   console.log(a);
   let a = 10;
   //----------------------
   Cannot access 'a' before initialization
   ```

   **反正他在定义之前你是无法访问的，所以我们可以认为它是没有提升的**

7. **let**变量对于循环的特殊处理，当他每次进行{}时会创建一个新的块级作用域然后里面有一个let声明的变量，所以就相当于每个{}块级作用域中的let变量都是一个全新的let变量

   ```js
   for(let i = 0; i < div.length; i++){//这里创建了length个块级作用域，每个块级作用域中又是一个新得let声明得变量
       div[i].onclick = function (){
           console.log(i);
       }
   }
   ```

**let变量最主要看”{}“块级作用域**

## 2.const常量

**它于let没有任何区别，唯一得区别就是const在声明时必须赋值，并且const的值不能进行更改**

**所以我们叫他常量**

**开发建议：**

​	在开发中我们尽量去使用const声明变量：

1. 因为我们一般的变量其实都是不需要进行更改的：

   ```js
   const div = document.getElementsTagName('div');
   ```

   像这种我们一般都是不进行更改的，可是我们如果设为变量那么很有可能我们会不小心的改掉了它，所以我们尽量的使用const进行常量声明，如果我们发现这个值它确实要变那么我们再将他改成let即可

2. 在后面的框架开发中都要求参数不可变，所以我们的const就起到了大作用，于是我们尽量的使用const进行声明常量是一个很好的习惯

**注意！！！！**

我们**常量声明的只是这个常量的值无法更改**，而如果我们这个值是一个**引用类型的地址**，例如他是一个**对象**，那么我们这个**对象的属性值**其实是**可以进行更改**的，不过我们不**能更改这个对象，也就是这个引用地址**

```js
//错误
const a = {};
a = {};
//正确
const a = {
    name:'aaa'
}
a.name = 'bbb';
```

**常量的命名：**

1. **特殊常量**：

   类似于圆周率，月地距离等等一些绝对不可变的值的常量名，我们使用**全大写多个单词使用下划线分割**

   ```js
   const MOON_EARTH_DISTANCE = 3245563424;
   ```

2. 普通常量：

   使用与以前一样即可！

3. 循环变量不能使用常量！因为他是变化条件否则报错哈哈！！

4. 在**forin**循环里面可以使用常量！！！！

   ```js
   //错误
   for(const i = 0; i < 10; i++){//因为我们的i++所以错误
       
   }
   //正确
   for(const prop in obj){//我们每次的作用域就是一个新的prop就直接进{}了
       
   }
   ```


## 3.更好的Unicode支持

早期，由于存储空间宝贵，Unicode使用16位使用二进制进行存储文字，我们将一个**16位**的二进制编码叫做**一个码元(Code Unit)**

后来由于技术的发展，Unicode对文字编码进行了拓展，将某些文字拓展到了**32位(占两个码元)**，并且，将**某个文字对应的二进制**数字叫做**码点(Code Point)** **两个码元的结合(不是相加)**，两个码元的代码转成16进制然后转成2进制，最后将两个二进制码元结合就是一个码点了

​	码点 = String.charCodeAt(0).toString(16)转成二进制 **连接** String.charCodeAt(1).toString(16)转成二进制 

例如：一些生僻字在我们使用 字符串.length 时它范围的长度是2，而我们命名就只有一个生僻字，**因为JS认为一个码元就是一个长度**

**因为使用的是二进制16位进行存储所以最多能够存储65,536**

```js
const text = '堃';
console.log(text.length);//2
console.log(text.charCodeAt(0));//我们可以打印第一个码元的所在Unicode中的位置
console.log(text.charCodeAt(1));//我们可以打印第二个码元的所在Unicode中的位置
```



**es6做出的优化：**

1. 提供了一个可以直接**获得码点**的方法：`String.codePointAt(下标)`，它可以直接获取到两个码元的连接结果然后**得到这个文字的码点**

**它可以通过第一个码元了解到还没完，所以会找到第二个码元，然后将其转换成码点给你输出出来；而我们如果给的是第二个码元则无法知道这个是不完整的则直接输出这个码元了**

```js
const text = '堃';
console.log(text.codePointAt(0));//返回码点
console.log(text.codePointAt(1));//返回第二个码元
```

2. 同时，es6为正则表达式添加了一个flag：u，如果添加了该配置，则匹配时，使用码点匹配 `/^.$/u`

   因为普通的正则表达式也是通过 字符串.length 来进行字符串匹配的，所以当我们有占两个码元的字时就会出现匹配不符合预期，于是就提出了u这个配置， `/^.$/u` ，此时我们这个正则使用的就是**码点**进行匹配了

   

**方便函数：**

1. 判断这个字符是否是两个码元

   ```js
   function is32bit(char){
       return char.codePointAt(0) > 0xffff;//0xffff代表16进制最大值
   }
   ```

2. 得出这个字符串地码点

   ```js
   function is32bit(char, i){
       return char.codePointAt(i) > 0xffff;//0xffff代表16进制最大值
   }
   function getLengthOfCodePoint(str){
       var len = 0;
       for(let i = 0; i < str.length; i++){
           if(is32bit(str, i)){
               i++;//如果我这个码元位置是一个32位字符，那么我跳过它后面一个码元，因为我们通过当前码元已经确定我们后一个码元是我们地第二个码元了，所以我们直接跳过，到下一个字符地码元开始进行判断，这样子就能保证一个码点地两个码元只添加一个码点
           }
           len ++;
       }
       return len;
   }
   ```

## 4.更多的字符串API

- includes

  `String.includes(子字符串)`

  判断这个子字符串是否在这个字符串中

  返回true/false

  

  我们还可以指定它从哪个下标开始往后找

  `String.includes(子字符串,指定下标)`

- startsWith

  判断字符串中是否以指定的字符串开始

  返回true/false

  

  我们可以指定下标判断我们传入在参数从指定下标开始是否是开头

- endsWith

  判断字符串是否以指定的字符串结尾

  返回true/false

  

  我们可以指定下标判断我们传入在参数从指定下标开始是否是开头

- repeat

  将我们的字符串重复指定次数，然后返回一个新的字符串

  返回字符串

  

## 5.正则中的粘黏标记[拓展]

在es6中为正则新增了一个flag：`y`，当我们的正则规则中加上了y这个flag那么我们的正则表达式就会从我们这个正则表达式的lastIndex处开始匹配，并且必须开头就匹配上这个正则规则，加上y以后相当于`/^W\w/y`

## 6.模板字符串标记[拓展]

在模板字符串书写之前，可以加上标记：

```js
标记名`模板字符串`
```

标记是一个函数，函数参数如下：

1. 参数1：被插值分割的字符串数组
2. 后续参数：所有的插值



```js
const a = 函数名`asdqwe`;
```

es6中我们可以在模板字符串前面添加一个函数名，当代码执行到这一行时会帮我们调用这个函数，并且会将这个模板字符串的参数传进来：

**那个""就是最后一个空字符串，尽管你在结尾没有写任何东西他也是有这个空字符串，如果结尾是。那么就会是"。"**

![批注 202-04 194633](http://note.youdao.com/yws/public/resource/fe3310355b82edd44cc8055926dc461f/xmlnote/17F7CBFD9E414324B164A9F6198C0830/8443)

![批注 2020-09-04 194633](http://note.youdao.com/yws/public/resource/fe3310355b82edd44cc8055926dc461f/xmlnote/5A742BA2A0584EB9B17E46CD920E8E8C/8434)

**然后我们这个text的值会变成我们这个函数的返回值**

那么这里text就会变成undefined了



**当我们想要输出\n时我们需要进行一个转义，但是转义字符多了就会很懵，于是就有了我们这么一个方法来告诉模板字符串我们这个里面全是字符串：**

```js
const text = String.row`qweqweqw\ni哦啊时间都i请问、`;
//----------------
text = qweqweqw\ni哦啊时间都i请问、
```



**适用场景：**

当我们需要用户输入一个文本然后展示到页面中去时，我们的用户很有可能会利用这么一个漏洞写一些标签然后进行一些逻辑代码的运行，这样我们就会非常的不安全，所以我们就得对用户的输入内容进行一些替换处理，那么我们就可以将用户输入的内容放入到模板字符串中，然后进行一些特殊的操作最后在返回回来，这样我们就会相对的安全

## 7.函数参数默认值

我们在编写函数时，当参数过多时我们不想传那么多的参数我们想要当我们不传参数时拥有一个默认值，那么我们以前可能需要使用对象混合，或者逻辑运算符进行对参数赋予默认值，而在es6中它为我们提供了这么一种写法，可以特别方便的给参数赋予默认值：

```js
function fn(a = 10,b = (1 + 2)){
    
}
```

那么当我们没有传参数进去时呢参数的值也就是undefined，当为undefined时我们这个参数就会使用这个我们赋予的默认值，当然，我们也可以故意传个undefined进行占位让它这个参数的值为默认值

### 7.1对arguments的影响[拓展]

只要给函数加上参数默认值，该函数的arguments会自定变成严格模式下的规则：arguments和形参脱离

arguments和形参脱离：

当我们的形参值在函数内部变化时arguments中的值不会变(而在普通模式下会跟着形参一起变)

### 7.2留意暂时性死区[拓展]

在我们给函数的参数赋予了默认值时我们的参数会和使用let和const声明的量的规则一样，会有暂时性死区：

```js
function fn(a = b, b){
    
}
fn(undefined, 2);
```

那么此时他就会报一个和let和const声明的量在声明之前使用的报错是一样的：“**Cannot access 'xx变量' before initialization**”不能在某某变量声明之前进行使用这个变量，因为他还在暂时性死区

## 8.剩余参数

当我们不确定用户必须得传多少个参数时，我们之前可能会使用arguments进行处理：

arguments的缺陷：

1. 如果和形参配合使用，会有一个是否是严格模式的问题，很容易混乱
2. 从语义上，使用arguments获取参数，由于形参缺失，无法从函数定义上理解函数的真实意图，比如用户在调用你这个参数时，他看到你这里都不需要参数我为什么要传呢？实则你内部使用的时arguments，可是你又不能写形参告诉用户，这时就会很不好



于是es6就出了一个剩余参数来提供我们使用

```js
function fn(...形参名){
    
}
```

剩余参数就会收集它往后的所有参数，然后变成一个数组



**细节：**

1. 一个函数，仅能出现一个剩余参数：

   因为剩余参数是收集他往后的所有参数，当我们拥有两个剩余参数时，它们就无法确认我收哪里你收哪里了，就会报错：“**Rest parameter must be last formal parameter**”

   ​											剩余参数后面不能接形参

2. 剩余参数只能是最后一个形参：

   如果剩余参数后面还有形参的话他也会报上面的这个错误“剩余参数后面不能接形参”

**因为我们的剩余参数他是一个形参，所以我们就可以给他打注释了，这样用户使用起来也会清晰明了，而且剩余参数不会拥有arguments不确定的问题，所以我们以后尽量使用剩余参数！！！！**

## 9.展开运算符

在**函数中给形参前面加上“...“会变成剩余参数**，而在**别的地方加上"...“则会变成展开运算符**

### 9.1展开数组[es6]

**展开运算符的作用：**

1. 比如说我们给函数中的剩余参数传递一个数组进去那么它的结果则会是这样的：

   ```js
   const arr = [1,2,3,4,5,6];
   function fn(...args){
       
   }
   fn(arr);
   //--------------------------------
   [arr]
   
   [
       0:[1,2,3,4,5,6]
   ]
   ```

   可是我们想要的结果是将我们这个数组的内容变成剩余参数的内容：

   args:[1,2,3,4,5,6]

   那么我们就得这么写：

   ```js
   const arr = [1,2,3,4,5,6];
   function fn(...args){
       
   }
   fn(...arr);
   //--------------------------------
   [1,2,3,4,5,6];
   ```

   此时我们会发现args的内容就变成了我们的数组参数arr的内容了

   当然我们也还可以传别的形参：

   ```js
   const arr = [1,2,3,4,5,6];
   function fn(...args){
       
   }
   fn(0,...arr,7,8);
   //--------------------------------
   [0,1,2,3,4,5,6,7,8];
   ```

2. 快速克隆一个新数组：

   在展开符之前我们想要克隆一个数组可能会使用Array.prototype.slice.apply(要克隆的数组),或者我们自己编写一个数组然后将他的元素一个一个的放进我们克隆后的目标，而我们使用了展开符则无需如此：

   ```js
   const arr = [1,2,3,4];
   const arrTarget = [...arr];
   console.log(arr === Target);
   //-----------------------------
   arrTarget[1,2,3,4]
   false
   ```

   当然同样的我们还可以添加自己的元素：

   ```js
   const arr = [1,2,3,4];
   const arrTarget = [0, ...arr, 5, 6];
   console.log(arr === Target);
   //-----------------------------
   arrTarget[0, 1, 2, 3, 4, 5, 6]
   false
   ```

### 9.2展开对象[es7]

在es7中我们还可以使用展开符进行展开对象

1. 展开的对象是个浅度克隆(里面的引用类型克隆不了)

   ```js
   const obj1 = {
       name:'郑文杰',
       love:'邱子婕'
   }
   const obj2 = {
       ...obj1
   }
   console.log(obj2);
   //------------------------
   obj2{
       name:'郑文杰',
       love:'邱子婕'
   }
   ```

   我们知道写在下面的属性会覆盖上面的重名属性，所以我们可以利用这一点进行对象混合的功能：

   ```js
   const obj1 = {
       name:'郑文杰',
       love:'邱子婕'
   }
   const obj2 = {
       ...obj1,
       name:'邱子婕',
       love:'郑文杰'
   }
   console.log(obj2);
   //------------------------
   obj2{
       name:'邱子婕',
       love:'郑文杰'
   }
   ```

   因为我们自己知道展开符是**进行的浅度克隆**，所以我们可以这么来解决：**将他的这个引用类型展开**

   ```js
   const obj1 = {
       name:'郑文杰',
       love:'邱子婕',
       family:{
           staster:'郑文静',
           borther:'郑文杰'
       }
   }
   const obj2 = {
       ...obj1,
       name:'邱子婕',
       love:'郑文杰',
       family:{
           ...obj1.family
       }
   }
   console.log(obj2);
   console.log(obj2.family === obj1.family);
   //------------------------
   obj2{
       name:'邱子婕',
       love:'郑文杰',
       family:{
           stater:'郑文静',
           borther:'郑文杰'
       }
   }
   false
   ```

**这种使用展开运算符进行对象和数组克隆的方式在后面的react中会经常看到！！！！**

## 10.利用剩余参数和展开运算符简化柯里化函数

```js
function curry(fn, ...args){
    return function (...subArgs){
        const allArgs = [...args,...subArgs];
        if(allArgs >= fn.length){//判断当前参数列表是否蛮足该函数需要的参数
            fn(...allArgs);
        }else{
            curry(fn, ...allArgs);
        }
    }
}
```

## 11.明确函数的双重用途

函数分为：构造函数和普通函数

而我们有时候用户不使用new关键字进行调用构造函数，进行一些恶意操作，于是我们此时就想要解决这个问题：

在以前我们只能通过判断它的原型上有没有我们这个函数，可是这种方法可以通过call来进行破解，这样我们就可以不使用new关键词来调用这个构造函数了

于是在es6中为我们提供了这么一个API进行判断我们这个函数是否是使用new关键词进行调用，如果不是这个API返回的则是undefined,如果是的话它返回的则是这个函数本身

`new.target`

```js
function Fn(a){
    if(!new.target){
        throw new Error('该函数没有通过new关键词进行调用')
    }
    this.a = a;
}
const fn = Fn.call(Fn, 'qwrtqw');//报错
const fn2 = new Fn('qweqwr');//正确
```

## 12.箭头函数

箭头函数是一个函数表达式，**理论上**，任何使用函数表达式的场景都可以使用箭头函数

完整语法：

```js
(参数1, 参数2, 参数3...) => {
    
}
```

适用场景：

```js
const obj = {
    count : 1,
   	fn : function (){
        setTimeOut(function (){
            this.count ++;
        },1000);
    }
}
```

我们一眼就可以看出来这里绝对是NaN，因为我们此时setTimeOut是浏览器帮我们调用的，所以此时this指向的是window，而window上并没有count，所以就是undefined++，故等于NaN

我们可能会这么解决：

```js
const obj = {
    count : 1,
   	fn : function (){
        const self = this;
        setTimeOut(function (){
            self.count ++;
        },1000);
    }
}
```

利用我们函数的闭包进行创建变量，可是如果我们的函数嵌套过多呢？，那么我们就需要些特别多的self这样的变量进行保存最初this。

**于是我们es6就出了箭头函数来进行解决这样的问题：**

细节：

1. 箭头函数的this指向，**取决于**执行箭头函数**定义时**的**this指向**

   ```js
   const obj = {
       count : 1,
      	fn : function (){
           setTimeOut(() => {
               this.count ++;
           },1000);
       }
   }
   obj.fn();
   ```

   此时我们在定义setTimeOut这个函数时得执行fn这个函数，而fn这个函数我们是通过 对象. 的方式调用的，此时的this是obj，所以setTimeOut这个箭头函数的this指向就是obj，**因为箭头函数的this并不取决于谁调用它而是取决于定义它时的this**

   于是我们此时这个箭头函数内的this.count++就是可以进行++的没有任何错误，因为它这个箭头函数的this正是obj，而count也正是在obj这个对象内。

2. 因为箭头函数的this取决于定义它时的this是谁，于是就有了以下问题：

   ```js
   const obj = {
       count : 1,
       fn : () => {
           console.log(this);
       }
   }
   obj.fn();
   //--------------------------------
   window{}
   ```

   为什么我们此时的this是window对象？因为我们JS的预编译会看obj这个对象里面的所有内容，而刚刚好执行到fn这个属性时看到这个箭头函数时是我们的window对象，所以我们这个箭头函数的this就是window对象了！！！！

   那么这个问题我们怎么解决呢？

   不解决！

   **因为我们通常在函数嵌套时使用箭头函数，来方便我们不需要使用闭包效果就能够取到我们预期的this！！**

**箭头函数通常在函数嵌套时使用！！！！**

3. 我们的箭头函数它并没有this,arguments,new.target，用的也是外层函数的this,arguments,new.target，所以我们箭头函数不管嵌套多少层因为没有this,arguments,new.target所以他们用的一样是最外层函数的！！

   **那不还是有闭包那味吗？所以懂得都懂（滑稽）**

   ```js
   const obj = {
       fn (){
           const a = () => {
               console.log(this);
               console.log(arguments);
               console.log(new.target);
           }
           a();
       }
   }
   obj.fn(234);
   //------------------------------------
   obj
   [234]
   undefined
   ```

   **箭头函数在JS看来就是零时用一下就丢了的东西**

4. 箭头函数没有原型：

   ```js
   const fn = () => {
       
   }
   console.log(fn.prototype);
   //-------------------------------
   undefined
   ```

   **所以他不能当成构造函数使用（滑稽，估计也没有这种傻逼哈哈哈~）**



**简便写法：**

1. 当我们只有一个参数时我们可以这么写：

```js
参数 => {
    
}
```

```js
const fn = a => {
    console.log(a);
}
fn(1);
```

2. 如果箭头函数只有一条返回语句，那么可以省略大括号和return关键字

   ```js
   const fn = a => a+1;
   console.log(fn(1));
   ```

   如果我们要返回一个对象怎么办？因为我们的对象也是{}

   ```js
   const fn = a => {a:1};//报错了
   //他理解成为：
   const fn = a => {
       a:1,
   }
   //相当于
   function fn (){
       a:1,
   }
   ```

   所以我们得让js知道他是一个表达式，则加上括号即可()

   ```js
   const fn = a => ({a:1});
   ```

**适用场景：**

1. 临时性使用的函数，并不会可以调用它，比如：
   1. 事件处理函数
   2. 异步处理函数
   3. 其他临时性函数

2. 为了绑定外层this的函数

3. 在不影响其他代码的情况下，保持代码的简洁，最常见的，数组方法中的回调函数

   ```js
   const arr = [1,2,3,4];
   arr.forEach(item => {
       console.log(item);
   })
   ```



**对象属性千万不要使用箭头函数！！！！为什么上面已经说过了！如果还是要写的话出this问题别说我们认识！**

## 13.对象新增的对象字面量语法

1. 成员速写：

```js
function fn(a,b,c){
    return {
        a,
        b,
        c
    }
}
```

es6会知道你这个属性的值和方法的名字重复然后赋予到一起去

2. 计算属性名

   我们有时希望我们这个属性的名字是通过计算得来的，而并不是我们直接写死的，因为我们当前自己也不知道要叫什么，而我们以前只能通过 对象[属性名] 这个这个属性名才能被更改是个，而在es6中允许了我们这么去写：

   ```js
   const prop = 'name';
   const prop2 = 'wife';
   const obj = {
       [prop] : '郑文杰',
       [prop2] : '邱子婕'
   }
   console.log(obj);
   //----------------------------
   obj{
       name:'郑文杰',
       wife:'邱子婕'
   }
   ```
   
   我们也可以直接写表达式：
   
   ```js
   const obj = {
       ["qweqw" + "a"]:"qweqw"
   }
   for(let prop in obj){
        console.log(prop);
   }
   //qweqwa
   ```
   
   

## 14.Object的新增API

### 1. Object.is()

用于进行判断两个内容是否相等，与===一样，**不过它与===有区别**：

```js
Object.is(NaN,NaN);//true
Object.is(+0,-0);//false
```

其他都是一样的

### 2.Object.getOwnPropertyNames()

获取这个对象原型上自己的属性，继承过来的不看，然后打包成一个数组返回给你

这个方法以前就有了，只不过他返回的属性名的顺序以前没有任何规定，而是由浏览器厂商自己规定，后来es6就提出说做一个规则，于是现在的Object.getOwnPropertyNames()就是由排序规则的了

1. 先排数字(升序)
2. 在排其他(没有任何顺序上的排序你怎么写的它就怎么给你什么顺序展示)

### 3.Object.setPrototypeOf()

该函数用于设置某个对象的隐式原型

比如：

```js
Object.setPrototypeOf(obj1, obj2);
相当于：obj1._proto_ = obj2
```

## 15.类

**标准写法**

```js
class 类名{
    constructor (属性参数1...){//构造函数
        this.属性名 = 属性参数;
        ...
    }
    方法名 (){
        
    }
}
```

**传统构造函数的问题：**

1. 属性和原型方法定义分离，降低了可读性

   ```js
   function Fn(prop){
       this.prop = prop;
   }
   //中间很可能隔了100行代码，这样就导致我们的可读性会特别的差
   Fn.prototype.print(){
       console.log(this.prop);
   }
   ```

2. 原型成员可以被枚举

   ```js
   function Fn(prop){
       this.prop = prop;
   }
   //中间很可能隔了100行代码，这样就导致我们的可读性会特别的差
   Fn.prototype.print(){
       console.log(this.prop);
   }
   var a = new Fn("asdas");
   for(var prop in a){
       console.log(prop);
   }
   //----------------------------------
   prop
   print(){}//我们会发现我们属于原型上面的东西也是可以被枚举出来的，可是这样我们写的构造函数就给用户看的一清二处了，就特别的不好
   ```

   

3. 默认情况下，构造函数仍然可以被当作普通函数使用

   ```js
   function Fn(){
       
   }
   Fn();
   ```

**类的特点**

1. 类声明不会被提升，与 let 和 const 一样，存在暂时性死区

   ```js
   const fn = new Fn("郑文杰");//此时会报错 原因：暂时性死区
   class Fn{
       constructor(name){
           this.name = name;
       }
       print (){
           console.log(this.name);
       }
   }
   //”Uncaught ReferenceError: Cannot access 'Fn' before initialization“
   ```

   

2. 类中的所有代码都在严格模式下执行

   1. 变量名不能重复等等

3. 类的**所有方法**都是**不可枚举的**

   ```js
   class Fn{
       constructor(name){
           this.name = name;
       }
       print (){
           console.log(this.name);
       }
   }
   const fn = new Fn("郑文杰");//此时会报错 原因：暂时性死区
   for(let prop in fn){
       console.log(prop);
   }
   //------------------------------
   name
   ```

   

4. 类内部的所有方法都无法被当作构造函数使用

   ```js
   class Fn{
       constructor(name){
           this.name = name;
       }
       print (){
           console.log(this.name);
       }
   }
   const print = new Fn.print();
   //-----------------------------------
   "Uncaught TypeError: Fn.print is not a constructor"
   ```

   

5. 类的构造器必须使用 new 来调用

   ```js
   class Fn{
       constructor(name){
           this.name = name;
       }
       print (){
           console.log(this.name);
       }
   }
   const fn = Fn();
   //--------------------------------------
   "Uncaught TypeError: Class constructor Fn cannot be invoked without 'new'"
   ```

## 16.类的其他简便书写方式

1. 方法名可以和我们的对象一样使用不确定时的变量方法名

   ```js
   const propName = "qqq";
   class Fn{
       constructor(name){
           this.name = name;
       }
       [propName] (){
           console.log(this.name);
       }
   }
   Fn.qqq();
   Fn[propName]();//都可以
   ```

2. 我们之前使用访问器属性来约束这个属性值，那么我们在类里面有没有更好的方法呢？或者说在类里面如何做到这个效果呢？

   ```js
   class Fn{
               constructor (age){
                   this._age = age;
               }
               get age(){
                   return this._age;
               }
               set age(value){
                   this._age = value;
               }
           }
           const fn = new Fn(1);
   //----------------------------------------------------
   Fn {_age: 2}
   _age: 2
   age: 2
   __proto__: Object
   ```
   
   **我们千万不要直接给this.age赋值，因为我们的getter和setter在设置或获取时就会触发，那么我们每次触发了然后又去触发一直循环下去就会栈溢出了**
   
3. 静态成员

   例如我们在做棋盘游戏时，我们想要创建一个棋盘，那么需要知道一个棋子的宽高，可是如果我们把这个吃春写在了我们的**实例成员**里面就相当于我们在创建一个棋盘我们还得有一个棋子，所以我们就不想这样，于是我们的es6就给我们推出了**static**用来创建我们的静态成员

   ​	静态成员的特点：

   1. 直接在这个构造函数上的属性或方法
   2. 通过构造函数.属性或方法可以直接调用，无需进行实例化

   ```js
   class Fn{
               constructor (){
   
               }
               static name = "郑文杰";
           }
           console.dir(Fn);
           const fn = new Fn();
           console.log(fn);
   //------------------------------------------
   class Fn
   name: "郑文杰" //*
   arguments: (...)
   caller: (...)
   length: 0
   prototype: {constructor: ƒ}
   __proto__: ƒ ()
   [[FunctionLocation]]: index.html:20
   [[Scopes]]: Scopes[2]
   
   Fn {}
   __proto__: Object
   ```

   **方法也可以！！！！**

4. 字段初始化器（es7）

当我们这个类的属性的值不需要来自构造函数参数，那么我们无需编写构造函数，我们不写构造函数就相当于构造函数里面什么都没有并不代表我们**不能进行实例化**：

```js
class Fn{
    static a = 1;
	b = 2;
	c = 3;
}
const fn = new Fn();
console.log(fn);
//----------------------------
{
    b:2,
    c:3,
    __proto__{
        a:1
    }
}
```

**注意这里的a因为时静态属性所以他是在这个类上面的并不是我们进行实例化出来的**

**a，b，c并不会有暂时性死区**



形如一下代码的属性我们称之为字段初始化器：

```js
class Fn{
    a = 1;
	print (){
        
    }
}
```

使用字段初始化器的属性相当于我们这么去写：

```js
class Fn{
    constructor (){
        this.a = 1;
        this.print = function (){
            
        }
    }
}
```

**字段初始化器的属性会在构造函数的最上行代码执行**

所以我们这样会有一个问题：

```js
class Fn{
    constructor (){
        this.a = 1;
        this.print = function (){
            console.log(this.a);
        }
    }
}
const fn = new Fn();
const print  = fn.print;
print();
//-------------------------------------------
"a is not defined"
```

那么我们此时应该怎么解决呢？

使用我们的**箭头函数**:

```js
class Fn{
    a = 1;
    print = () => {
        console.log(this.a);
    }
}
```

**因为在前面我们讲了字段初始化器相当于在构造函数的第一行进行执行我们的属性，我们还知道箭头函数最主要的就是他在哪里定义的，所以我们此时print函数的this就和Fn绑定到一起去了**

5. 类表达式

   我们的类的底层就是一个函数，所以我们可以将类作为值，参数，函数返回值

   ```js
   const Fn = class{
       a = 1;
   }
   const fn = new Fn();
   ```


## 17.类的继承

两个关键字：```extends```，```super()```

标准写法：

```js
class Person{
    constructor (age, name){
        this.age = age;
        this.name = name;
    }
    say (){
        Console.log("说话");
    }
}
class Man extends Person{
    constructor (talk){
        super(18, "郑文杰");
        this.talk = talk;
    }
    eat (){
        Console.log("吃东西方法");
    }
}
```



super注意：

1. super相当于父级的构造函数进行调用

2. 子类如果写了constructor那么则必须在**第一行代码调用super方法**并将需要的参数传进入，**否则报错**

3. 如果**子类没有写constructor**那么es6会**自动把父类的constructor放到子类中执行**，那么这时我们在**创建子类时给构造函数传的参数的参数列表**就会是**父类的constructor的参数列表了**

   ```js
   class Person{
       constructor (age, name){
           this.age = age;
           this.name = name;
       }
       say (){
           Console.log("说话");
       }
   }
   class Man extends Person{
       eat (){
           Console.log("吃东西方法");
       }
   }
   const man = new Man(180);
   ```

   ![批注 2020-09-10 211423](../笔记图片(勿删)/批注 2020-09-10 211423.png)

4. 如果把**super当作对象**来调用那么它代表**父类**，**我们可以通过super.父类的成员，在子类中进行调用**



【冷知识】：

用JS模拟抽象类：(因为我们目前JS还没有抽象类这个东西，所以我们只能通过特殊代码手段进行模拟)

```js
class Person{
    constructor (type){
        if(new.target === Person){
            throw new Error("我是抽象类不能进行实例，请调用我的子类！");
        }
        this.type = type;
    }
}
class Man extends Person{
    constructor (name, age){
        super("人类");
        this.name = name;
        this.age = age;
    }
}
```

**利用new.target的值为使用new的是谁值就是谁的特性**

## 18.解构

### 18.1对象解构

语法：

```js
const user = {
    name:"郑文杰",
    age:18,
    address:'上海'
}
let {name, age, addresss} = user;//意思为：我声明了name，age，address这三个变量，然后到对象user里面去找同名的属性，再把同名属性的值赋给我们的变量，这就是我们的对象解构
```

老式写法：

```js
const user = {
    name:"郑文杰",
    age:18,
    address:'上海'
}
let name = user.name;
let age = user.age;
let address = user.address;
```

**这两个写法完全相等，语法部分他是一个对象结构语法+语法糖的形式**



注意：

1. 没有同名属性的变量的值为undefined

   **可是我们想要有一个默认值，不想要undefined怎么办？**

   ```js
   const user = {
       name:"郑文杰",
       age:18,
       address:'上海'
   }
   let {name, age, addresss, abc = 123} = user;
   ```

   这样子abc因为没有读到同名属性，所以它使用的是默认值：123，当然如果abc读到了同名属性，那么它的值就是同名属性的值了，并不是默认值了

2. 非同名属性

   我们不想要使用它的同名属性，可是我又想读到那个属性的值怎么办？

   ```js
   const user = {
       name:"郑文杰",
       age:18,
       address:'上海'
   }
   let {name, age : old, addresss} = user;//意思为：先声明三个变量：name，old，address，然后去对象里面读同名属性，其中old读的是age这个同名属性的值
   //相当于：我拿age这个同名属性去对象里面读值，读到了之后把值给old，(age是相当于没有定义的)
   console.log(age);//"age is not defined"
   console.log(name, old, address);//"郑文杰" 18 '上海'
   ```

   如果我们想要使用非同名属性又想要拥有默认值怎么办？

   ```js
   const user = {
       name:"郑文杰",
       age:18,
       address:'上海'
   }
   let {name, age : old = 123, addresss} = user;
   ```

   这样子当我们的age读不到值时，我们的非同名属性old就会使用默认值123

3. 解构对被解构的对象不会有任何影响

4. 深层解构：

   如果我们的同名属性他是一个对象我们想要的不是这个对象而是这个对象里面的属性，我们能不能有更简便的写法呢？

   ```js
   const user = {
       name : '郑文杰',
       family : {
           wife : '邱子婕',
       }
   }
   const {name, family : {wife}} = user;//意思为：我们先声明两个变量name，wife，我们先拿到name的同名属性值，然后拿到family的同名属性值这个对象，然后在对family这个对象进行解构wife这个同名属性然后拿到wife这个属性的值，(我们这里并没有family这个变量了)
   console.log(family);//"family is not defined"
   console.log(name, wife);//郑文杰 邱子婕
   ```

   想要再往里面嵌套就这么嵌套就好了

### 18.2数组解构

语法：

```js
const arr = [1,2,3,4];
const [n1,n2] = arr;
console.log(n1, n2);//1 2

const [n1, , , n4] = arr;
console.log(n1, n4);//1 4










const arr2 = ['a', 'b', 'c', 'd', [1, 2, 3, 4]];
//得到numbers下标为4的数组中的下标为2的数据，放到变量n中
const [ , , , , [ , , n]];
console.log(n);//3








const arr3 = ['a', 'b', 'c', 'd', {
    a:1,
    b:2
}]
//得到numbers下标为4的数组的属性a，赋值给变量A
const [ , , , , { a : A }];
console.log(A);//1

const { a : A} = arr[4];
console.log(A);//1









const object = {
    name : '郑文杰',
    age : 18,
    sex : '男',
    family : {
        wife : '邱子婕'
    }
}
//我们将name取出来，然后将剩余的属性全部放到obj中
const {name, ...obj} = object;
console.log(name, obj);//郑文杰 {age : 18, sex : '男', family : {wife : 邱子婕}}
//展开运算符在解构中起收集作用，将剩余的属性全部收集起来放到obj这个对象中





//展开运算符在数组解构中收集的结果是数组
```



**解构的骚操作：**

```js
let a = 1, b = 2;
[b, a] = [a, b]
console.log(a, b);//2, 1
//步骤：
[b, a] = [1, 2];
解构：将第一项给b，第二项给a
这样b = 1， a = 2就完成了
```

### 18.3参数解构

```js
function print({name,family : {wife}}){
    console.log("丈夫:" + name);
    console.log("夫人:" + wife);
}
const user = {
    name : '郑文杰',
    family : {
        wife : '邱子婕'
    }
}
print(user);
```

ajax参数解构:

我们曾经可能还需要进行对象混合，而我们这里则直接进行对象结构完事了

```js
function ajax({
    method = 'get',
    url = '/'
}){
    console.log(method, url)
}
ajax({url : '/abc'})//get /abc
```

**我们在解构方面用到的最多的就是参数解构，用来调配配置**

### 当对undefined和null进行解构时会报错

于是我们就可以这么解决：

```js
//会报错
function ajax({
    method = 'get',
    url = '/'
}){
    console.log(method, url)
}
ajax()


//解决方案
function ajax({
    method = 'get',
    url = '/'
} = {}){//我们给这个解构来个默认值，如果用户没有传参数，那么我们默认对{}进行解构
    console.log(method, url)
}
ajax()
```

## 19.符号
### 普通符号

符号是es6新增的一个数据类型，它通过使用函数 ==Symbol("符号描述")== 来创建

符号设计的初衷是为了给对象设置==私有属性==

私有属性：只能在对象内部使用，外面无法使用


```js
const sym = Symbol("这是一个简单的符号");
console.log(sym);
```
![image](http://note.youdao.com/yws/public/resource/fe3310355b82edd44cc8055926dc461f/xmlnote/661AD20AAA694BC88AD94C496ED50F70/8514)

**符号具有以下特点：**

1. 没有字面量
2. 使用typeof得到的类型是symbol

```js
const sym = Symbol();
console.log(typeof (sym));
-------------------------------------
symbol
```

3. ==每次调用 Symbol 函数得到的符号永远不会相等，无论符号名是否相同==

```js
const sym = Symbol();
const sym2 = Symbol();
console.log(sym == sym2);
-------------------------------------
false
```
4. 符号可以作为对象的属性名存在，这种属性称之为符号属性
   
    开发者可以通过精心的设计，让这种属性无法通过常规方式被外界访问
    
    ```js
    const obj = (() => {
        const sym = Symbol("name");
        return {
            [sym] : '郑文杰',
            age : 18,
            wife : '邱子婕'
        }
    })()
    console.log(obj.sym);//undefined
    ```
    
    ```js
    const Person = (() => {
            const sym = Symbol("name");
            return class {
                constructor (){
                    
                }
                print (){
                    this[sym]();
                }
                [sym] (){
                    console.log("我只能在函数里面调用")
                }
            }
        })()
        const person = new Person();
        person.print();
    ```

    符号属性是不能被枚举的，因此在 for-in 循环中无法读取到符号属性，Object.keys 方法也无法读取到符号属性

    Object.getOwnPropertyNames 尽管可以得到所有无法枚举的属性，但是仍然无法读取到符号属性
    
    **Es6 新增 Object.getOwnPropertySymbol 方法，可以读取符号**
    
    ==使用特殊方法获取私有的方法(封装起来的)然后进行调用，这种是无法避免的==
    
    ```js
        const Person = (() => {
            const eatRandom = Symbol("吃多少的随机值");
            return class{
                constructor (){
                }
                eat (){
                    console.log(this[eatRandom]());
                }
                [eatRandom] (){
                    return Math.random();
                }
            }
        })()
        const person = new Person();
        console.log(person);
        const personSyms = Object.getOwnPropertySymbols(Person.prototype);
        console.log(personSyms);
        console.log(person[personSyms[0]]());
        person.eat();
    ```
    
    ![image](http://note.youdao.com/yws/public/resource/fe3310355b82edd44cc8055926dc461f/xmlnote/E56085431DC24E7587E26E3B40E51C76/8694)
    
5. 符号==无法被隐式转换==，因此不能用于数学运算，字符串拼接或其他隐式转换场景，但符号==可以显示转换为字符串==，通过 String 构造函数进行转换即可，console.log 之所以可以输出符号，因为它其实是先将 符号 转换成了字符串，然后用一种特别的颜色给我们打印了出来

### 共享符号

创建共享符号:

```Symbol.for("符号描述");```

```js
const sym = Symbol.for("abc");
const sym2 = Symbol.for("abc");
console.log(sym === sym2);//true
```

注意：

```js
const sym = new Symbol("abc");
const sym2 = Symbol.for("abc");
console.log(sym === sym2);//false
```

因为我们的共享符号底层代码其实是这样的：
```js
const SymbolFor = (() => {
    const symArr = {};//将我们所有通过我们这个函数创建符号放在一个对象里边，然后我们用户需要的时候再去从这里面拿，如果有的话就直接返回出来了，所以就是一样的
    return function (name){
        if(!symArr[name]){
            symArr[name] = Symbol(name);
        }
        return symArr[name];
    }
})()
```

**适用场景：**

当我们的符号想要被轻易获取到则使用共享符号：

```js
const obj = {
    [(Symbol.for("abc")] : 1
}
console.log(obj[(Symbol.for("abc"))]);//1
```

## 20.ES6的新队列-微队列

**JS其实不仅有事件队列还有微队列这两个队列**

微队列和事件队列做的事情是一样的，只不过里面放的事件函数不同，且微队列相当于队列中的VIP**(先执行微队列再执行事件队列)**

队列中存放的函数不同：

事件队列
1. 我们在学习ES6之前的所有异步函数

微队列
1. HTML5中新增的函数：MutationObserver


```js
let ul = document.getElementsByTagName('ul')[0];
const observer = new MutationObserver(function (){
    //当监听的dom元素发生变化时运行的回调函数
    console.log('ul元素发生了变化')
})
observer.observe(ul,{
    attributes:true,//监听属性的变化
    childList:true,//监听子元素的变化
    subtree:true//监听子树的变化(子元素发生变化他也会执行-称之为子树)
})

//取消监听
observer.disconnect();
```


2. ES6中新增的异步函数：promise


## 21.Promise

**面试问如何理解Promise可回答这个：**

**==++Promise并没有消除回调，只是让回调变得可控++==**

### Promise解决的问题：
- 邓哥心中有20个女神，他决定用更加高效的方法同时给二十个女神表白，如果有女神同意，就拒绝其他的女神，并且当所有的女神回复完成后，他要把所有的回复都记录到日志进行分析
<br>
难解决的问题:
    1. 我们的操作是异步的，因为我们无法确定女神的回复速度，所以我们无法判断当前是否已经有女神同意了
    2. 我们如何判断什么时候全部女神回复完毕，因为我们所有的回复都是异步的所以无法判断
- 数据库中有3个表，学生，班级，老师，通过ajax请求获取到学生信息，并取其中一个然后通过它的班级id找到他对应的老师
<br>
通常写法：
<br>
此时我们会发现我们每次想要进行下一轮判断我们则需要再嵌套一层ajax请求然后进行判断我们会发现它的一个代码层级关系会非常的复杂，而我们的逻辑其实也就一点点，我们下次一定不想再看这个代码！
```js
success:function (){
    if(当前学生是我们指定的学生){
        success:function (){
            if(通过我们的班级编号找到了我们的班级){
                success:function (){
                    if(通过所对应的老师找到了老师){
                        
                    }
                }
            }
        }
    }
}
```

### Promise模型

[Promise模型](https://note.youdao.com/web/#/file/51C51A20B6974F0FB266E5EC84002F1F/markdown/WEBe559b5a222ad9d556916cfbabeb85b24/)

### Promise的基本使用

#### 创建一个Promise对象

**标准语法：**

```js
const pro = new Promise((resolve, reject)=>{
    // 未决阶段的处理
    // 通过调用resolve函数将Promise推向已决阶段的resolved状态
    // 通过调用reject函数将Promise推向已决阶段的rejected状态
    // resolve和reject均可以传递最多一个参数，表示推向状态的数据
})
```

**注意：**
1. promise的回调函数回立即执行
2. 我们可以在任何需要异步的地方使用promise，它会立即执行

**例子：**

**标准例子：**

```js
const pro = new Promise((resolve, reject)=>{//在我们创建这个promise函数时它会立即执行这个回调函数
    //未决阶段要做的事情
    if(当我们未决阶段要做的事情满足了某个条件){
        resolve(true);//传入true或者false用于方便知道我们是满足了还是未满足
    }else{//未满足
        resolve(false);
    }
})
```

**当我们在它执行resolve或者reject函数前查看pro这个对象：**

![image](http://note.youdao.com/yws/public/resource/fe3310355b82edd44cc8055926dc461f/xmlnote/WEBRESOURCE8d15e2eb92c00e86bd9ae46998d51b76/9126)

[[PromiseState]]->当前这个promise的状态

我们会发现此时它处在未决阶段，且是一个挂起的状态

**当我们在它执行resolve或者reject函数之后查看pro这个对象：**

![1602920778243](../笔记图片(勿删)/1602920778243.png)

我们会发现它此时就是成功的状态了，`fulfilled=resolve，因为promise是按照promise A+规范来的所以变成了fulfilled，两个意思是一样的`

**[[PromiseState]]的三种状态：**

1. pending 注册挂起状态(还未推向已决阶段)
2. resolveed/fulfilled 已决成功状态
3. rejected 已决失败状态

`当描述状态的时候我们采用过去式，写代码时我们不使用过去式`

#### 未决阶段代码

```js
const pro = new Promise((resolve,reject) => {
    //未决阶段代码
})
```

#### 已决阶段

**resolved/fulfilled：**

```js
const pro = new Promise((resolve,reject) => {
    //未决阶段代码
    resolve(true);//此时状态变成已决状态的resolved/fulfilled状态
})
pro.then(data => {//当状态变成resolved则立即执行这个函数
    //已决阶段代码
})
```

我们之前不是说可以注册多个thenable嘛？

```js
pro.then(data => {//当状态变成resolved则立即执行这个函数
    //已决阶段代码
})
pro.then(data => {//当状态变成resolved则立即执行这个函数
    //已决阶段代码
})
pro.then(data => {//当状态变成resolved则立即执行这个函数
    //已决阶段代码
})
```

我们这样子多写几个它就注册了多个了

执行顺序自上而下

**rejected:**

```js
const pro = new Promise((resolve,reject) => {
    //未决阶段代码
    reject(true);//此时状态变成已决状态的resolved/fulfilled状态
})
pro.catch(err => {//当状态变成reject则立即执行这个函数
    //已决阶段代码
})
```



```js
const pro = new Promise((resolve,reject) => {
    //未决阶段代码
    reject(true);//此时状态变成已决状态的resolved/fulfilled状态
})
pro.then(data => {//当状态变成resolved则立即执行这个函数
    //已决阶段代码
},err => {//当状态变成reject则立即执行这个函数
    //已决阶段代码
})
```



### 最优代码案例

```js
function biaobai(god) {
        return new Promise(resolve,reject => {
             console.log(`邓哥向${god}发出了表白短信`);
             setTimeout(() => {
             	if (Math.random() < 0.1) {
                  	//女神同意拉
                  	resolve(true)
             	} else {
                  	//resolve
                  	resolve(false);
             	}
             }, 3000);
       })
}

biaobai("女神1").then(result => {
       console.log(result);
})
```



**Ajax最优**

这样我们就不需要判断传入上面回调函数然后去调用了，我们直接返回一个promise然后用户在这个函数后面写.then成功时和失败时的代码就好了

```js
// 辅助函数,把传进来的对象拼接成url的字符串
        function toData(obj) {
            if (obj === null) {
                return obj;
            }
            let arr = [];
            for (let i in obj) {
                let str = i + "=" + obj[i];
                arr.push(str);
            }
            return arr.join("&");
        }
        // 封装Ajax
        function ajax(obj) {
            return new Promise((resolve, reject) => {
                //指定提交方式的默认值
                obj.type = obj.type || "get";
                //设置是否异步，默认为true(异步)
                obj.async = obj.async || true;
                //设置数据的默认值
                obj.data = obj.data || null;
                // 根据不同的浏览器创建XHR对象
                let xhr = null;
                if (window.XMLHttpRequest) {
                    // 非IE浏览器
                    xhr = new XMLHttpRequest();
                } else {
                    // IE浏览器
                    xhr = new ActiveXObject("Microsoft.XMLHTTP");
                }
                // 区分get和post,发送HTTP请求
                if (obj.type === "post") {
                    xhr.open(obj.type, obj.url, obj.async);
                    xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
                    let data = toData(obj.data);
                    xhr.send(data);
                } else {
                    let url = obj.url + "?" + toData(obj.data);
                    xhr.open(obj.type, url, obj.async);
                    xhr.send();
                }
                // 接收返回过来的数据
                xhr.onreadystatechange = function() {
                    if (xhr.readyState === 4) {
                        if (xhr.status >= 200 && xhr.status < 300 || xhr.status == 304) {
                            resolve(JSON.parse(xhr.responseText))//无需判断是否有成功时候的回调函数了
                        } else {
                            reject(xhr.status)//无需判断是否有失败时候的回调函数了
                        }
                    }
                }
            })
        }

        ajax({
            url: "./data/students.json?name=李华"
        }).then(resp => {
            console.log(resp)
        }, err => {
            console.log(err)
        })//直接返回回来一个promise对象，然后我们直接给他注册resolve和reject状态事件
```

**强强强！！！！！！！！**

### 细节

1. 在我们创建promise对象时它的回调函数时立即执行的，是同步的不是异步的

   ```js
   const pro = new Promise((resolve, reject) => {
       console.log("a")
   })
   console.log("b");
   //输出：a 
   //   	b
   ```

2. thenable和catchable函数是异步的，它会立即加入到微队列

   ```js
   const pro = new Promise((resolve, reject) => {
       console.log("a")
       resolve(true);
       settimeout(() => {
           console.log("1")
       },1000)
   })
   pro.then(data => {
       console.log(data);
   },err => {
       console.log(err)
   })
   console.log("b");
   //输出：
   a
   b
   true
   1
   ```

    

3. catch也可以单独添加

   ```js
   pro.catch(err => {
       console.log(err);
   })
   ```

4. 当我们在未决函数内部抛出了一个错误，它会导致我们的promisestatus变成reject

   前提条件：未捕获的错误，如果我们使用trycatch捕获了则正常执行代码

   ```js
   const pro = new Promise((resolve,reject) => {
       throw new Error("123")//未捕获的错误
   })
   pro.then(data => {
       console.log(data);
   },err => {
       console.log(err);
   })
   //输出结果：
   new Error抛出的错误，说明我们执行了catchable函数
   ```

5. promisestatus状态一旦确定则不可逆

   ```js
   const pro = new Promise((resolve,reject) => {
       resolve(1);
       reject(1);//无效
   })
   pro.then(data => {
       console.log(data);
   },err => {
       console.log(err);
   })
   //输出结果：
   1
   ```

   因为我们的状态已经确定了是resolved了所以我们后面执行的任何resolve和reject都是无效的，这就是我们之前说的状态不可逆

6. **promise并没有消除回调，只是让回调变得可控**

### Promise的串联操作

**适用场景：**

当我们这一次的promise操作要用到上一次promise的操作的结果时我们就得用到promise的串联操作

例如：我们有三个json数据文件，学生,班级,老师，我们要通过学生json查到班级json然后查出这个班级的老师是谁，这是我们就需要通过promise版的ajax进行处理，然后首先拿到名字叫李华的学生的班级ID，可是promise中的值是无法拿到的，这个怎么办呢？就得用到我们的promise串联了

#### promise的特点：

Promise对象中，无论是then方法还是catch方法，它们都具有返回值，返回的是一个全新的Promise对象，它的状态满足下面的规则：

1. 如果当前的Promise是未决的，得到的新的Promise是挂起状态

   ```js
   const pro = new Promise((resolve, reject) => {
       
   })
   //在控制台中：
   > pro
   > [[PromiseStatus]]:pending
   ```

   

2. 如果当前的Promise是已决的，会运行响应的后续处理函数，并将后续处理函数的结果（返回值）作为resolved状态数据，应用到新的Promise中；如果后续处理函数发生错误，则把返回值作为rejected状态数据，应用到新的Promise中。

   ```js
   //理解代码
   const pro = new Promise((resolve,reject) => {
       resolve(1);
   })
   const pro2 = pro.then(data => {
       console.log(data);//1
       return data * 3;
   })
   pro2.then(data => {
       console.log(data);//3
   })
   //在控制台内：
   > pro2
   > [[PrimiseStatus]]:resolved
   > [[PrimiseValue]]:3
   
   
   //最优代码
   new Promise((resolve,reject) => {
       resolve(1);
   }).then(data => {
       console.log(data);//1
       return data * 2;
   }).then(data => {
       console.log(data);//2
       throw new Error("抛出错误");
   }).then(data => {//不执行
       console.log(data);
   },err => {
       cosole.log(err);//打印抛出错误的文本
   })
   ```

### Promise的API

#### 实例对象成员

1. then
2. catch
3. finally：[ES2018]注册一个后续处理函数（无参），当Promise为已决时运行该函数

注意：因为他们的回调函数都是放到微队列中执行的，所以谁的回调函数先定义谁的就先执行回调函数



#### 构造函数成员

\- resolve(数据)：该方法返回一个resolved状态的Promise，传递的数据作为状态数据



```js
const pro = new Primise((resolve,reject) => {
    resolve(1);
})
//等价于
const pro = Primise.resolve(1);
```

  \- 特殊情况：如果传递的数据是Promise，则直接返回传递的Promise对象

```js
const pro = new Primise((resolve,reject) => {
    resolve(1);
})
const pro1 = new Primise((resolve,reject) => {
    resolve(pro);
})
console.log(pro1 === pro);//true
//等价于
pro1 = pro;
```



\- reject(数据)：该方法返回一个rejected状态的Promise，传递的数据作为状态数据

![1603017777284](../笔记图片(勿删)/1603017777284.png)

![1603017962174](../笔记图片(勿删)/1603017962174.png)



\- all(iterable)：这个方法返回一个新的promise对象，该promise对象在iterable参数对象里所有的promise对象都成功的时候才会触发成功，一旦有任何一个iterable里面的promise对象失败则立即触发该promise对象的失败。这个新的promise对象在触发成功状态以后，会把一个包含iterable里所有promise返回值的数组作为成功回调的返回值，顺序跟iterable的顺序保持一致；如果这个新的promise对象触发了失败状态，它会把iterable里第一个触发失败的promise对象的错误信息作为它的失败错误信息。Promise.all方法常被用于处理多个promise对象的状态集合。



当数组内的所有promise对象状态全部变成已决就将promise数组里所有的已决状态返回值放到一个数组内返回

![1603018434336](../笔记图片(勿删)/1603018434336.png)

![1603018450901](../笔记图片(勿删)/1603018450901.png)

当途中出现一个reject那么这个数组就不会返回了，它会进入catch

![1603019335512](../笔记图片(勿删)/1603019335512.png)

![1603019423724](../笔记图片(勿删)/1603019423724.png)



\- race(iterable)：当iterable参数里的任意一个子promise被成功或失败后，父promise马上也会用子promise的成功返回值或失败详情作为参数调用父promise绑定的相应句柄，并返回该promise对象

第一个完成的promise成功它就进入then，否则就catch，他只看第一个完成的promise

### async和await

> es2017发布

#### async

> 通过后边即将学到的生成器(ES2015)实现的promise语法糖

我们想要使一个函数返回一个promise我们使用常规的方式需要写一大堆的promise代码，于是就有了我们async的出现

使用async修饰的函数都会返回一个promise:

```js
async function fn(){
    
}
const pro = fn();
```

![1604408056730](../笔记图片(勿删)/1604408056730.png)

情况:

1. 无返回值

   promise的值为：**undefined**

2. 有返回值

   promise的值为：**return的值**

3. 返回一个promise

   ```js
   async function fn (){
       return new Promise((resolve,reject) => {
           resolve(1);
       })
   }
   const pro = fn();
   //结果：
   [PromiseResult]:1
   ```

   它会直接执行我们返回的promise然后将我们这个promise的结果当作我们这个promise的结果

   所以如果我们这么写相当于：

   ```js
   function fn (){
       return new Promise((resolve, reject) => {
           resolve(1);
       })
   }
   ```

   **所以这么写是没有意义的**
   
4. 如何范围rejected状态

   在函数内部抛出一个错误，我们可以给这个错误赋值那么这个值就是rejected的promisevalue

   ```js
   async function fn(){
       throw 2;
   }
   ```

   

**注意我们返回的是promise并不是这个函数return的数据那个是then数据**

##### 总结

解决的问题：

1. 方便我们去获取一个异步函数的结果，将他的异步放到promise中让我们使用promise更方便的去处理异步函数的结果

#### await

我们之前一直拿到的都只是promise如果我们想要使用resolve时的值怎么办呢？之前只能写在then里边然后使用data参数

现在呢我们拥有了await就可以直接拿到它为resolve时then中的data数据

```js
async function fn(){
    return 1;
}
const result = await fn();//等待我们fn这个异步函数执行完,我们的result的值就是fn返回的promise的then的值了***有个小问题：我们怎么知道它什么时候执行完呢？
```

我们上面提到了一个问题，我们无法知道这个promise什么时候执行完，所以我们则需要使用async配合await使用：

```js
async function fn(){
    return 1;
}
async function result(){
    const result = await fn();//因为我们这个result没有拿到值那么这个函数就永远没有执行完成得等他执行完成，这样我们就能拿到fn这个promise的then值了
    console.log(result);//1
}
```

我们为什么不在普通函数内使用await呢？

![1604409930559](../笔记图片(勿删)/1604409930559.png)

哈哈！！！！！！！

**它规定死了** 哈哈其实不是，是因为如果我们如果不适用async的函数或者别的地方则会**阻塞整个JS代码**的执行，如果使用了async这个函数就变成了**异步的**所以await只能使用在async函数中

##### **await做的特殊处理：**

1. 当await在循环内部使用，当前promise不resolved不执行下一次循环

   ```js
   function biaobai(god) {
               return new Promise(resolve => {
                   console.log(`向${god}发出了表白短信`);
                   setTimeout(() => {
                       if (Math.random() < 0.3) {
                           //女神同意拉
                           resolve(true)
                       } else {
                           //resolve
                           resolve(false);
                       }
                   }, 500);
               })
           }
   //一直向女神邱子婕表白直到她同意(特别简写版)
   async function fn(){
       const gods = ['邱子婕','邱子婕','邱子婕','邱子婕'];
       for(let i = 0; i < gods.length; i++){
           //当前promise不到resolved不执行下一次循环
           const result = await biaobai(gods[i]);
           if(result){
               console.log(`${gods[i]}同意了不用再表白了`);
               break;
           }
       }
   }
   ```

2. 如果await后面的表达式不是一个promise则会将它变成Promise.resolve(表达式)然后等待

   ```js
   async function fn(){
       const result = await 1;//1
       console.log(result);
   }
   //相当于
   function fn(){
       return Promise((resolve,reject) => {
           Promise.resolve(data => {
               const result = data;//1
               console.log(result);
           });
       })
   }
   ```

   

##### 特殊场景

1. 如果我们await的promise返回回来的是一个异常，那么我们此时代码会说我们这个函数存在一个未处理的异常

   ```js
   async function test(){
       throw 2;
   }
   async function fn(){
       const result = await test();
       console.log(result);
   }
   fn();
   ```

![1604815318746](../笔记图片(勿删)/1604815318746.png)

那么我们想要拿到这个异常的结果值怎么办呢？包裹在try-catch中

```js
		async function test(){
            throw 2;
        }
        async function fn(){
            try{
                const result = await test();
                onsole.log(result);
            }catch(e){
                console.log(e);
            }
        }
        fn();
```

![1604815477259](../笔记图片(勿删)/1604815477259.png)

相当于我们这么区编写：

```js
		async function test(){
            throw 2;
        }
        async function fn(){
            test().then(data => {
                const result = test();
                onsole.log(result);
            },err => {
                console.log(e);
            })
        }
        fn();
```

##### 总结：

解决的问题：

1. 方便我们拿到promise异步处理的结果，无需我们再使用传统的promise语法进行大量的代码处理

更优解：

###### 🔴改良计时器函数

解决的问题：延迟一段时间当延迟完成promise完成resolve我等到resolve时我再做事情，这就是一个延迟的效果

错误方案：

```js
async function fn(){
    settimeout(() => {
        //此处无法返回这个promise如果返回则是返回这个settimeout的返回
    }, 400);
}
```

解决方案：

```js
function delay(duration){
            return new Promise((resolve,reject) => {
                setTimeout(() => {
                    resolve()
                }, duration);
            })
        }
```

应用到邓哥表白题目中：

```js
function delay(duration){
            return new Promise((resolve,reject) => {
                setTimeout(() => {
                    resolve()
                }, duration);
            })
        }
        async function biaobai(){
            console.log(`邓哥向女神发短信`);
            await delay(2000);//等待2秒
            if(Math.random() < 0.5){
                return true;//返回resolve的结果为true表示表白成功！
            }else{
                return false;//返回结果为false
            }
        }
        async function sendBiaoBai(){
            for(let i = 0; i < 10; i++){
                if(await biaobai()){
                    console.log("表白成功！");
                }else{
                    console.log("没有成功！");
                }
            }
        }
        sendBiaoBai();
```

![1604924792313](../笔记图片(勿删)/1604924792313.png)

## 22.Fetch Api

### 22.1概述

在以前我们想要发送网络请求需要使用XMLHttpRequest对象进行网络请求，而XMLHttpRequest存在很多问题：

#### 22.1.1XMLHttpQuest的问题：

1. 编写繁琐：编写请求头，请求体，数据源等等...
2. 所有的功能全部集中在同一个对象上，容易书写出混乱不易维护的代码
3. 采用传统的事件驱动模式，无法适配新的Promise Api

> jq相对处理较好，不过jq底层同样使用的是这个对象

于是在我们的H5中我们的浏览器对象提出了一个新的Api：Fetch Api

#### 22.1.2Fetch Api的特点：

> 底层使用ajax

1. 并非取代Ajax，而是对Ajax传统API的改进
2. 精细的功能分割：头部信息，请求信息，响应信息等均分布到不同的对象，更利于处理各种复杂的ajax场景
3. 使用PromiseApi，更利于异步代码的书写
4. FetchApi并非ES6的内容，属于HTML5新增的WebApi
5. 需要掌握网络通信的知识

### 22.2参数

#### 22.2.1示例代码

```js
fetch("http://101.132.72.36:5100/api/local",{
    配置内容...
})
```

该函数有两个参数：

1. 必填，字符串，请求地址
2. 选填，对象，请求配置

**请求配置对象**

- method：字符串，请求方法，默认值GET
- headers：对象，请求头信息
- body: 请求体的内容，必须匹配请求头中的 Content-Type
- mode：字符串，请求模式
  - cors：**默认值**，配置为该值，会在请求头中加入 origin 和 referer
  
    **(可用于解决跨域请求问题，fetch自带了，并且自动帮我们填上了“origin”“referer”)**
  
    当我们跨域对服务器进行请求时，我们可以填写cors这个参数并且值为origin和referer，这样服务器就可以知道是哪个地址在向我请求然后去判断要不要给我请求结果
  
  - no-cors：配置为该值，不会在请求头中加入 origin 和 referer，跨域的时候可能会出现问题
  
  - same-origin：指示请求必须在同一个域中发生，如果请求其他域，则会报错
- credentials: 如何携带凭据（cookie）
  - omit：默认值，不携带cookie
  - same-origin：请求同源地址时携带cookie
  - include：请求任何地址都携带cookie
- cache：配置缓存模式
  - default: 表示fetch请求之前将检查下http的缓存.
  - no-store: 表示fetch请求将完全忽略http缓存的存在. 这意味着请求之前将不再检查下http的缓存, 拿到响应后, 它也不会更新http缓存.
  - no-cache: 如果存在缓存, 那么fetch将发送一个条件查询request和一个正常的request, 拿到响应后, 它会更新http缓存.
  - reload: 表示fetch请求之前将忽略http缓存的存在, 但是请求拿到响应后, 它将主动更新http缓存.
  - force-cache: 表示fetch请求不顾一切的依赖缓存, 即使缓存过期了, 它依然从缓存中读取. 除非没有任何缓存, 那么它将发送一个正常的request.
  - only-if-cached: 表示fetch请求不顾一切的依赖缓存, 即使缓存过期了, 它依然从缓存中读取. 如果没有缓存, 它将抛出网络错误(该设置只在mode为”same-origin”时有效).
### 22.3返回值

**fetch 函数返回一个 Promise 对象**

- 当收到服务器的返回结果后，Promise 进入resolved状态，状态数据为 Response 对象

  **不管是200，还是403，500...他都是resolved状态**

- 当网络发生错误（或其他导致无法完成交互的错误）时，Promise 进入 rejected 状态，状态数据为错误信息

  **无法发送请求时变成rejected状态,也就是网络请求完全就到不了服务器**

#### 22.3.1示例代码



```js
fetch("http://101.132.72.36:5100/api/local").then(resp => {
            console.log(resp);
        }, err => {
            console.log(err);
        })
```

有网的状态：

![1604993304645](../笔记图片(勿删)/1604993304645.png)

无网的状态：

![1604993369589](../笔记图片(勿删)/1604993369589.png)

### 22.4Response对象（响应对象）

- ok：boolean，当响应消息码在200~299之间时为true，其他为false
- status：number，响应的状态码

**服务器结果处理api：**

- text()：用于处理文本格式的 Ajax 响应。它从响应中获取文本流，将其读完，然后返回一个被解决为 string 对象的 Promise。

  **因为我们返回回来的可能是类似于一本书一样多的文本结果，那么他解析也需要一定的时间，而如果是同步代码的话则会卡代码，所以浏览器把它做成了promise返回，resolvevalue为string**

- blob()：用于处理二进制文件格式（比如图片或者电子表格）的 Ajax 响应。它读取文件的原始数据，一旦读取完整个文件，就返回一个被解决为 blob 对象的 Promise。

- json()：用于处理 JSON 格式的 Ajax 的响应。它将 JSON 数据流转换为一个被解决为 JavaScript 对象的promise。

- redirect()：可以用于重定向到另一个 URL。它会创建一个新的 Promise，以解决来自重定向的 URL 的响应。

  例如我们的请求为302结果码，并且服务器给了我们一个新的地址，那么我们无需解析出来然后在进行请求，而是可以直接调用这个方法，则会自动拿到服务器给我们的结果进行重定向

**使用new response 来模拟服务器数据**

```js
new Response('[{"id" : 1}]', ok : ture, status : 200)
```

就可以自己创建一个response对象了

### 22.5request对象(请求对象)

除了使用基本的fetch方法，还可以通过创建一个Request对象来完成请求（实际上，fetch的内部会帮你创建一个Request对象）

```js
fetch(url,{
    配置对象
})
//等价于
const req = new request(url,{
    配置对象
})
fetch(req)
```

 

**注意点：**

尽量保证每次请求都是一个新的Request对象

​	如果我们请求的是个get请求那没事，而如果是post请求，那么需要发送数据体，而有时候数据体过大，我们可能会需要使用流的一个方式进行传输，流是可以监控当前文件流的一个状态的，而你如果重新调用了之前发送流的request对象，那么这个流也会重新开始，这是你就会发现明明快要完成的东西重新开始了

如果我们想要一个全新的一模一样的request对象可是不想写那么多同样的代码配置，于是这里request它就给我们提供了这么一个api：“Clone()”,我们可以通过`req.clone();`这样我们就能获得到一个全新的配置一模一样的request对象了

### 22.6Headers对象

在Request和Response对象内部，会将传递的请求头对象，转换为Headers

```js
//fetch中
fetch(url,{
    headers:{
        
    }
})

//request中
new Request(url,{
    headers:{
        
    }
})

//Response中
Response{
    headers:{}
    state:'OK'
}
```

![1605839846954](../笔记图片(勿删)/1605839846954.png)

我们会发现headers我们看不了里面的内容，可是我们需要拿到headers里面的键值对做一些操作要怎么办呢？

**headers为我们提供了一些可操作headers的api**

Headers**对象中**的方法：

\- has(key)：检查请求头中是否存在指定的key值

\- get(key): 得到请求头中对应的key值

\- set(key, value)：修改对应的键值对

​	如果修改一个不存在的键值，那么会新增这个键值

\- append(key, value)：添加对应的键值对

​	如果添加的键值已存在，那么值则会用逗号进行分割存储

​	例如：a：1已存在，此时我append一个2进入`headers.append('a',2)`，则a的值变成：1,2







**以下三个方法的得到的时一个可迭代的对象，并不是一个可查看的数组**

\- keys(): 得到所有的请求头键的集合

\- values(): 得到所有的请求头中的值的集合

\- entries(): 得到所有请求头中的键值对的集合

如果我们想要进行遍历则使用for-of循环(与for-in循环有不同，需学习**遍历机制**)

```js
const head = new Headers({
    a : 1,
    b : 2
})
for(let data of head.entries()){
    console.log(data);
}
```

![1605849037348](../笔记图片(勿删)/1605849037348.png)

当我们多个请求想要配置的内容大体一致时，我们可以通过创建Headers对象然后多次获取它的值即可

### 22.7文件上传(ajax无刷新上传)

流程：

1. 客户端将文件数据发送给服务器

----------------------------------------------------------------以下是服务器端的操作---------------------------------------------------------

1. 服务器保存上传的文件数据到服务器端
2. 服务器响应给客户端一个文件访问地址

> 测试地址：http://101.132.72.36:5100/api/upload
> 键的名称（表单域名称）：imagefile

请求方法：POST
请求的表单格式：multipart/form-data（这种表单格式数据体必须是键值关系，所以我们这里需要使用键名称imagefile值为图片数据）
请求体中必须包含一个键值对，键的名称是服务器要求的名称，值是文件数据

> HTML5中，JS仍然无法随意的获取文件数据，但是可以获取到input元素中，被用户选中的文件数据
> 可以利用HTML5提供的FormData构造函数来创建请求体

HTML5之前浏览器不允许js代码读取用户文件数据，因为它认为这个侵犯用户隐私了，到了HTML5之后它相通了，用户既然都选择了文件想要发送给服务器，那么为什么这个不能读呢？于是在HTML5它就可以读取用户选择的图片了(未选择的不允许读取图片数据)

获取文件数据：在HTML5中当input的type值为file时，它拥有一个特殊的属性files，用户选择的图片的数据数组，加上boolean属性multiple可选择多个文件上传，用户选择了多少个文件files里面就有多少个元素

```html
<input type='file' multiple name='image'><!--用户选择了多个文件-->
<script>
	const image = document.getElementsByTagName('input')[0];
    console.log(image.files);
</script>
```

![1605858787735](../笔记图片(勿删)/1605858787735.png)

这些元素就是文件数据



文件上传案例步骤：

1. 在HTML中创建两个标签“img”“input”，其中input的type值为file

   ```html
   <img src='' alt=''/>
   <input type='file'/>
   ```

2. 编写JS代码

   ```js
   //创建处理函数
   async function upload(){
       const input = document.getElementsByTagName('input')[0];//获取上传文件的input标签
       const img = document.getElementsByTagName('img')[0];//获取服务器返回回来的我们上传的图片的保存地址的图片展示位置
       const dataBody = new FormData();//创建数据体
       dataBody.append('imagefile',input.files[0]);//获取文件类型的input中用户选择的文件数据体
       const url = 'http://101.132.72.36:5100/api/upload';//创建url地址字符串
       //--------------------------------第一种写法---------------------------------------------
       fetch(url, {
           	   
                   method: 'POST', //发送方式为postmoshi1
                   body: dataBody //绑定数据体
               }).then(async function (data){
                   console.log(await data.json());
               }, err => {
   
       })
       //------------------------------------------------------------------------------------------
       //--------------------------第二种写法----------------------------
       const fetPro = await fetch(url, {
                   method: 'POST', //发送方式为postmoshi1
                   
                   body: dataBody //绑定数据体
               })
               const result = await fetPro.json();
       //-----------------------------------------------------------------
   }
   ```

   这里不用配置head中content-type是因为fetch它会根据我们的数据体自动确认content-type

   fetch部分的流程：

   1. fetch返回一个promise，我们await这个promise执行完(等待请求操作执行完)
   2. 返回一个异步的response对象，所以我们还需要await response对象的，可是我们想要获取服务器返回回来的数据则await response.json()这样就能拿到json转换后的服务器结果了

**最简版：**

![1605925318571](../笔记图片(勿删)/1605925318571.png)

## 23.迭代

### 23.1迭代的概念

1. 什么是迭代？

从一个数据集合中按照一定的顺序，不断取出数据的过程

2. 迭代和遍历的区别？

迭代强调的是依次取数据，并不保证取多少，也**不保证把所有的数据取完**

遍历强调的是要**把整个数据依次全部取出**

3. 迭代器

**对迭代过程的封装**，在不同的语言中有不同的表现形式，通常为**对象**

4. 迭代模式

一种设计模式，用于统一迭代过程，并规范了迭代器规格：

- 迭代器应该具有得到下一个数据的能力
- 迭代器应该具有判断是否还有后续数据的能力

**类似于C#中的DataReader对象通过read()去读取下一条数据，并且知道是否拥有下一条数据，迭代器就是这个原理**

#### 23.1.1JS中的迭代器

JS规定，如果一个对象具有next方法，并且该方法返回一个对象，该对象的格式如下：

```js
{value: 值, done: 是否迭代完成}
```

则认为该对象是一个迭代器

含义：

- next方法：用于得到下一个数据
- 返回的对象
  - value：下一个数据的值
  - done：boolean，是否迭代完成

### 23.2迭代小案例(体验迭代)

![1606007356636](../笔记图片(勿删)/1606007356636.png)

### 23.3可迭代协议与for-of循环

#### 23.3.1可迭代协议

**概念回顾**

- 迭代器(iterator)：一个具有next方法的对象，next方法返回下一个数据并且能指示是否迭代完成
- 迭代器创建函数（iterator creator）：一个返回迭代器的函数

**可迭代协议**

ES6规定，如果一个对象具有知名符号属性```Symbol.iterator```，并且属性值是一个迭代器创建函数，则该对象是可迭代的（iterable）

> 思考：如何知晓一个对象是否是可迭代的？
>
> ![1606007631384](../笔记图片(勿删)/1606007631384.png)
>
> ​	其实数组也是一个可迭代对象(在es6的时候改的)：
>
> 
>
> ​	![1606007740671](../笔记图片(勿删)/1606007740671.png)
>
> ​		所以说我们的数组其实是可以迭代的：
>
> ​		![1606007859755](../笔记图片(勿删)/1606007859755.png)
>
> ​		![1606007879212](../笔记图片(勿删)/1606007879212.png)
>
> ​	Es6以后他还将很多类数组也变成了可迭代对象：
>
> ​		例如：
>
> ​			NodeList：
>
> ​					![1606008343567](../笔记图片(勿删)/1606008343567.png)
>
> ​		![1606008362887](../笔记图片(勿删)/1606008362887.png)
>
> ![1606008419098](../笔记图片(勿删)/1606008419098.png)
>
> ![1606008431197](../笔记图片(勿删)/1606008431197.png)
>
> 思考：如何遍历一个可迭代对象？
>
> ![1606008831973](../笔记图片(勿删)/1606008831973.png)
>
> ![1606008849791](../笔记图片(勿删)/1606008849791.png)

#### 23.3.2for-of循环

我们会发现按照上面遍历可迭代对象的代码是否过多，于是es6就给我们提出了一个更快捷的语法糖：for-of循环

![1606012230874](../笔记图片(勿删)/1606012230874.png)

![1606012247146](../笔记图片(勿删)/1606012247146.png)

只要它是一个可迭代对象那么我们就可以使用for-of循环把它这个迭代对象遍历出来## 展开运算符与可迭代对象

#### 23.3展开运算符与可迭代对象

展开运算符可以作用于可迭代对象，这样，就可以轻松的将可迭代对象转换为数组。

如果迭代的对象不是一个可迭代对象则会**报错**

![1606013747545](../笔记图片(勿删)/1606013747545.png)

![1606013760160](../笔记图片(勿删)/1606013760160.png)

## 24.生成器

为什么要生成器？

为了简化编写迭代器

1. 什么是生成器？

生成器是一个通过构造函数Generator创建的对象（不过我们无法通过new Generator()来创建generator对象，它是js内部使用的），生成器既是一个迭代器(拥有next方法)，同时又是一个可迭代对象(拥有[Symbol.Iterator]迭代器生成函数)

2. 如何创建生成器？

生成器的创建，必须使用生成器函数（Generator Function）

3. 如何书写一个生成器函数呢？

   必须写在function 和 函数名之间


```js
  //这是一个生成器函数，该函数一定返回一个生成器
  function* method(){}//类似于我们在async来修饰一个函数时必定返回一个promise一样
```

4.为什么我们执行生成器函数可是里面的代码没有运行呢？

因为我们生成器函数内部是给我们生成器返回来的迭代器提供数据的，每次调用这个生成器返回的迭代器的next()则这个函数会**执行到下一个yield关键词(为返回来的迭代器提供迭代数据的)处**，直到**整个函数执行完done变为true**，不调用返回的迭代器的next()函数内部是不会执行的

yield只能在生成器函数中出现并使用，语法：`yield 数据表达式`  英文意思为：“产生”一个数据

例如：

![1606029744055](../笔记图片(勿删)/1606029744055.png)

![1606029758716](../笔记图片(勿删)/1606029758716.png)

![1606029804750](../笔记图片(勿删)/1606029804750.png)

生成器的方便案例：

![1606030305182](../笔记图片(勿删)/1606030305182.png)

![1606030328936](../笔记图片(勿删)/1606030328936.png)

**注意点：**

1). 生成器函数可以有返回值，返回值出现在第一次done为true时的value属性中

![1606031403898](../笔记图片(勿删)/1606031403898.png)

![1606031414542](../笔记图片(勿删)/1606031414542.png)

2). 调用生成器的next方法时，可以传递参数(他是生成器特属的)，传递的参数会交给yield表达式的返回值

![1606032049047](../笔记图片(勿删)/1606032049047.png)

![1606032072457](../笔记图片(勿删)/1606032072457.png)

![1606032296552](../笔记图片(勿删)/1606032296552.png)

**从而得出第三条注意的点**

3). 第一次调用next方法时，传参没有任何意义

4). 在生成器函数内部，可以调用其他生成器函数，但是要注意加上*号

![1606033213716](../笔记图片(勿删)/1606033213716.png)

相当于这么写：

![1606033253999](../笔记图片(勿删)/1606033253999.png)

也就是将别的生成器函数内部的迭代部分拿到我的参与进了我的迭代流程



生成器的其他API：

- return方法：调用该方法，可以提前结束生成器函数，从而提前让整个迭代过程结束

  可以传递一个参数当作这一次迭代的值

  ![1606032602746](../笔记图片(勿删)/1606032602746.png)

  ![1606032620229](../笔记图片(勿删)/1606032620229.png)

- throw方法：调用该方法，可以在生成器中产生一个错误

![1606032827212](../笔记图片(勿删)/1606032827212.png)

## 25.生成器-异步处理

在es6时提出了promise可以进行异步操作了，可是当时并没有async和await，可是我们想要类似于async和await那样的效果怎么办呢？

于是就有聪明人这么去写代码去模拟async和await的效果

![1606098990405](../笔记图片(勿删)/1606098990405.png)

## 26.Set集合

> set集合是一个可迭代对象

**set集合的作用：**

​	set集合用于存放不重复的数据

**如何创建set集合:**

```js
new Set();//创建一个没有任何内容的set集合
new Set(可迭代对象);//创建一个具有初始内容的set集合，内容来自于可迭代对象每一次迭代的结果
它会去迭代这个可迭代对象然后将它每次迭代的结果去重作为这个set集合的初始内容
```

**案例：**

​	1. 给字符串去重：

![1606100222899](../笔记图片(勿删)/1606100222899.png)

![1606100236814](../笔记图片(勿删)/1606100236814.png)

​		 执行步骤：

1. 字符串常量我们都知道他是通过new String()去创建的，因为在es6之后浏览器将**string对象也变成了可迭代对象(拥有[Symbol.Iterator]**)
2. 一个一个的将字符串传入set集合中，然后因为set集合不允许值重复，所以就达到了字符串去重的效果

**同理，数组等可迭代对象皆可使用此种方式进行去重**



**set集合的后续操作(API):**

- add(数据): 添加一个数据到set集合末尾，如果数据已存在，则不进行任何操作
  - set使用Object.is的方式判断两个数据是否相同，但是，针对+0和-0，set认为是相等（object.is()是认为不相等的，set对这个使用的是 == 进行判断，做了特殊处理的）（**Set集合内所有的判断都是通过Object.is进行判断的,Object.is(第一个值，第二个值)**）
  - `注意：`add(值)和new Set(值)完全不一样的意义，我们在new时加入的值它会去迭代它，而我们通过add加的值它会把它看成一个整体，然后通过Object.is去判断它
- has(数据): 判断set中是否存在对应的数据
- delete(数据)：删除匹配的数据，返回是否删除成功
- clear()：清空整个set集合
- size: 获取set集合中的元素数量，只读属性，无法重新赋值



**set集合如何转换为数组：**

因为set集合本身也是一个可迭代对象，所以我们可以使用展开运算符进行展开给数组

![1606102842808](../笔记图片(勿删)/1606102842808.png)

![1606102853874](../笔记图片(勿删)/1606102853874.png)

从上得出的数组去重面试题(超级简化版)：

​	去重数组：

![1606103051450](../笔记图片(勿删)/1606103051450.png)

![1606103078600](../笔记图片(勿删)/1606103078600.png)

​	去重字符串：

![1606103361852](../笔记图片(勿删)/1606103361852.png)

![1606103376910](../笔记图片(勿删)/1606103376910.png)

**如何遍历set集合：**

1. 使用for-of循环

2. 使用set中的实例方法forEach

   

   注意：set集合中不存在下标，因此forEach中的回调的第二个参数和第一个参数是一致的，均表示set中的每一项，第三个参数是这个set对象本身

   ```js
   new Set("asdwqesad").forEach((item,item2,s){
                                
   })
   ```

**注意点：**

1. 我们这种去重方式的优势在哪里？
   1. 对象属性的去重方式只能去重字符串类型的数据
   2. set集合的内容甚至可以是一个set集合，去重数据的全面性

## 27.用set集合解一些面试题

![1606120060856](../笔记图片(勿删)/1606120060856.png)

## 28.手写set集合

`遗漏了一个点：`我们得在这里给iterator赋个初始值否则我们在new MySet时，我们去typeof时对undefined[]此时就会报错了，所以我们得在constructor的iterator处改成`iterator = []`

![1606123095216](../笔记图片(勿删)/1606123095216.png)

## 29.Map集合

键值对（key value pair）数据集合的特点：**键不可重复**

map集合专门用于存储多个键值对数据。

在map出现之前，我们使用的是对象的方式来存储键值对，键是属性名，值是属性值。

**使用对象存储有以下问题：**

1. 键名只能是字符串
2. 获取数据的数量不方便
3. 键名容易跟原型上的名称冲突

**map和对象适用场景的区别：**

map：

​	它更像是一个集合，当我们的键值对可以随便增加一个或者删除一个他依然没有任何意义上的影响，那么我们就适用map集合

对象：

​	它是一个整体，例如一个人，有名字，年龄，身高等等，如果少了一个那可能就不是一个完整的整体从意义上可能就出现了影响，这个时候我们就只能使用对象，而不是使用map集合

**初始化Map:**

创建一个空的map集合：`new Map()`

创建一个有初始值的map集合：`new Map(可迭代对象)` 

​	规则：将这个可迭代对象每一次迭代出来的结果作为它的值，**注意：这个可迭代对象每次迭代出来的值必须是一个 长度为2的数组 代表 键和值 (也可不为数组其他迭代对象也行不过必须是这个形状的，拥有 键和值 的)** 最好就是它是一个二维数组 ：`[['a',1],['b',2]]`

![1606790653825](../笔记图片(勿删)/1606790653825.png)

![1606790627071](../笔记图片(勿删)/1606790627071.png)

**更多操作：**

1. `size`

   和set集合的size一样

2. `set(键，值)`

   - `map集合的键和值可以是任意类型的就算对象也可以`

   - 如果已存在则对其进行修改

   - 如果未存在则进行新增

   - 判断方式和set集合一样

3. `get(键)`

   根据键去获取对应的值，如果未找到则返回undefined

4. `has(键)`

   判断这个键是否存在返回Boolean 是否找到

5. `delete(键)`

   删除指定键，返回Boolean 是否删除成功

6. `clear()`

   清空map集合



**如何与数组进行转换：**

> map集合是一个可迭代对象

set集合可以如何迭代map集合就可以如何迭代

**不过迭代出来的结果形式不一样：**

`map：`

![1606794606648](../笔记图片(勿删)/1606794606648.png)

![1606794619008](../笔记图片(勿删)/1606794619008.png)

**map集合的foreach:**

![1606794837771](../笔记图片(勿删)/1606794837771.png)

![1606794853758](../笔记图片(勿删)/1606794853758.png)

## 30.手写Map集合

![1606829125606](../笔记图片(勿删)/1606829125606.png)

## 31.WeakSet和WeakMap

### 31.1WeakSet

使用该集合，可以实现和set一样的功能，不同的是：

1. **它内部存储的对象地址不会影响垃圾回收**
2. `只能添加对象`
3. 不能遍历（不是可迭代的对象）、没有size属性、没有forEach方法

`简而言之：weakset里面的东西虽然存有东西但是垃圾回收器并不看它的，所以只要其他的任何东西都对这个对象没有指向了的时候这个对象就被垃圾回收器回收了，那么weakset里面的这个对象也就没有了`

![1606873490214](../笔记图片(勿删)/1606873490214.png)

![1606873501860](../笔记图片(勿删)/1606873501860.png)

**vWeakSet的作用：**

​	我们通常会写一个对象就往WeakSet里面放，然后我们去观察WeakSet是否有该释放的对象没有释放占有资源呢？

### 31.2WeakMap

类似于map的集合，不同的是：

1. **它的键存储的地址不会影响垃圾回收**
2. 它的键只能是对象
3. 不能遍历（不是可迭代的对象）、没有size属性、没有forEach方法

**WeakMap适用场景：**

我们通常会去用一个dom绑定一个对象，这个可是如果我们将dom放在数组，这时当我们的dom移除了之后我们的代码还拽着，这时就特别的占用资源，于是我们这里就可以适用我们的WeakMap去实现这个需求

![1606875195385](../笔记图片(勿删)/1606875195385.png)

此时我们wm原来的第一项就没了

## 32.存储器属性绑定dom内容

存贮器属性会在我们设置或获取时调用我们的set/get函数，那么既然是函数我们就可以在这个函数里面干很多的事情，所以我们就可以利用存储器函数将一个对象与页面中的dom绑定起来，当我们更改对象内容时，我们的页面也会跟着更改

![1606896648588](../笔记图片(勿删)/1606896648588.png)

![1606896692795](../笔记图片(勿删)/1606896692795.png)

**其实我们经常使用的innerHTML他们都是domlist或者node原型上的一个存储器属性，当我们对其赋值时它才会相对应的更改页面或者当我们读取时他才会给我们返回回来**

![1606896960817](../笔记图片(勿删)/1606896960817.png)

## 33.属性描述符

Property Descriptor 属性描述符  是一个普通对象，用于描述一个属性的相关信息

通过```Object.getOwnPropertyDescriptor(对象, 属性名)```可以得到一个对象的某个属性的属性描述符

- value：属性值
- configurable：该属性的描述符是否可以修改
- enumerable：该属性是否可以被枚举
- writable：该属性是否可以被重新赋值

> ```Object.getOwnPropertyDescriptors(对象)```可以得到某个对象的所有属性描述符

如果需要为某个对象添加属性时 或 修改属性时， 配置其属性描述符，可以使用下面的代码:

```js
Object.defineProperty(对象, 属性名, 描述符);
Object.defineProperties(对象, 多个属性的描述符)
```

因为`defineProperty`是针对一个对象的一个属性进行描述的，所以当我们去配置一个对象里面的属性的时候，使用defineProperty是**一次只能描述一个属性的**

而我们如果使用`defineProperties`因为它能获取这个对象里面的所有属性，所以我们可以利用它的特性，一次性对多个属性进行描述：

![1606955409051](../笔记图片(勿删)/1606955409051.png)

### 33.1存取器属性

属性描述符中，如果配置了 get 和 set 中的任何一个，则该属性，不再是一个普通属性，而变成了存取器属性。

get 和 set配置均为函数，如果一个属性是存取器属性，则读取该属性时，会运行get方法，将get方法得到的返回值作为属性值；如果给该属性赋值，则会运行set方法。

存取器属性最大的意义，在于可以控制属性的读取和赋值。

### 33.2总结

1. 存取器属性与属性描述符无法共存

   因为存取器属性的值并不存在与内存，而是通过函数计算得出；而属性描述符描述的属性还是一个函数它的值确实得在内存中存在的，所以他们两个是存在天差地别的

   如果两个同时配置则会报错

## 34.Reflect反射

> Reflect是一个对象，而这个对象**无法进行修改**，因为Reflect是**使用底层C/C++代码编写的**，也是因为如此，Reflect是在**ES6**的时候才被提出，所以它有**兼容性问题**，如果我们去**模拟**它的话也是**有差异的**因为底层的C/C++代码你无法使用JS完全模拟出来

1. Reflect是什么？

Reflect是一个内置的JS对象，它提供了一系列方法，可以让开发者通过调用这些方法，访问一些JS底层功能

由于它类似于其他语言的**反射**，因此取名为Reflect

2. 它可以做什么？

使用Reflect可以实现诸如 属性的赋值与取值、调用普通函数、调用构造函数、判断属性是否存在与对象中  等等功能

3. 这些功能不是已经存在了吗？为什么还需要用Reflect实现一次？

有一个重要的理念，在ES5就被提出：**减少魔法、让代码更加纯粹（使用API，函数式编程）**

这种理念很大程度上是受到函数式编程的影响

ES6进一步贯彻了这种理念，它认为，对属性内存的控制、原型链的修改、函数的调用等等，这些都属于底层实现，属于一种魔法，因此，需要将它们提取出来，形成一个正常的API，并高度聚合到某个对象中，于是，就造就了Reflect对象

因此，你可以看到Reflect对象中有很多的API都可以使用过去的某种语法或其他API实现。

4. 它里面到底提供了哪些API呢？

- Reflect.set(target, propertyKey, value): 设置对象target的属性propertyKey的值为value，等同于给对象的属性赋值

  ![1606956300182](../笔记图片(勿删)/1606956300182.png)

  ![1606956311147](../笔记图片(勿删)/1606956311147.png)

- Reflect.get(target, propertyKey): 读取对象target的属性propertyKey，等同于读取对象的属性值

- Reflect.apply(target, thisArgument, argumentsList)：调用一个指定的函数，并绑定this和参数列表。等同于函数调用

  ![1606956515409](../笔记图片(勿删)/1606956515409.png)

  ![1606956531845](../笔记图片(勿删)/1606956531845.png)

- Reflect.deleteProperty(target, propertyKey)：删除一个对象的属性

- Reflect.defineProperty(target, propertyKey, attributes)：类似于Object.defineProperty，不同的是如果配置出现问题，返回false而不是报错

- Reflect.construct(target, argumentsList)：用构造函数的方式创建一个对象

- Reflect.has(target, propertyKey): 判断一个对象是否拥有一个属性

- 其他API：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect

## 35.Proxy代理

> Proxy代理不会占用内存空间，它就相当于一个不存在的东西，只是一层壳子

代理：提供了修改底层实现的方式

```js
//代理一个目标对象
//target：目标对象
//handler：是一个普通对象，其中可以重写底层实现
//返回一个代理对象
new Proxy(target, handler)
```

![1607141041462](../笔记图片(勿删)/1607141041462.png)

![1607141070455](../笔记图片(勿删)/1607141070455.png)

**代理概念：**

![1606958469690](../笔记图片(勿删)/1606958469690.png)

代理就像当于一个律师，我们想要目标对象怎么样，首先必须得去先经过代理才能实现对对象的修改

**代理的用法：**

因为我们代理改写的就是底层实现(Reflect里的所有API)

![1606959071130](../笔记图片(勿删)/1606959071130.png)

//因为我们想要改写的就是reflect里面的底层API，所以我们在代理里面加上我们想要实现的代码然后再调用reflect的API这样代码阅读起来也更底层，就类似于继承了父级的方法然后我们把父级的方法重写了一样

![1606958885822](../笔记图片(勿删)/1606958885822.png)

**那我们直接对目标对象赋值呢？**

![1606959108867](../笔记图片(勿删)/1606959108867.png)

那么我们的代理就不会起到任何作用，这一点**待解决**

## 36.Proxy应用

### 36.1观察者模式

> 在vue3.0中很多效果都是使用观察者模式这种做法去实现的

**观察者模式的概念：**

有一个对象，是观察者，它用于观察另外一个对象的属性值变化，当属性值变化后会收到一个通知，可能会做一些事。

**在ES6的Proxy代理出来之前老版本如何模拟代理特有的观察者模式的：**

![1607140077815](../笔记图片(勿删)/1607140077815.png)

![1607140143924](../笔记图片(勿删)/1607140143924.png)

![1607140194361](../笔记图片(勿删)/1607140194361.png)

![1607140218361](../笔记图片(勿删)/1607140218361.png)

![1607140241237](../笔记图片(勿删)/1607140241237.png)

​	**缺点：**

		1. 因为我们原来无法参与到底层代码的一个实现中，所以当我们对obj赋值时就真正的是给obj赋值了，并没有让我们这个模拟的代理对象的目标进行一个值增加等等，因为我们这是一个新的属性我们没有办法在这个时候进行执行相对应的代码，所以**我们之前对于proxy代理的模拟其实是无法完全实现的**![1607140278676](../笔记图片(勿删)/1607140278676.png)
  		2. 实现一个代理就要创建两个对象如果我的页面一大**对于浏览器资源的占用也就特别大**

**使用es6新增的proxy代理完成完整的观察者模式：**

​	**优点：**

1. proxy不会占用内存，因为proxy实则并不是一个真正的数据，他只是一层壳子用于代理它的目标对象
2. 当我们对proxy创建的代理对象赋值时我们可以捕获到用户什么时候赋值，所以我们就可以在那时做一些自己想做的事，于是就有了我们现在的版本

![1607140742586](../笔记图片(勿删)/1607140742586.png)

这时我们再去对obj新增属性时，target也会相对应的新增属性，做到了真正意义上的观察者模式(对我的操作和在我观察的目标身上也会有一样的操作)

### 36.2偷懒型构造函数

![1607146770910](../笔记图片(勿删)/1607146770910.png)

![1607146808340](../笔记图片(勿删)/1607146808340.png)

### 36.3可限制参数类型的函数

![1607148086324](../笔记图片(勿删)/1607148086324.png)

![1607148100132](../笔记图片(勿删)/1607148100132.png)

## 37.新增的数组API

**静态方法：**



\- Array.of(...args): 使用指定的数组项创建一个新数组

\- Array.from(arg): 通过给定的类数组 或 可迭代对象 创建一个新的数组。



**实例方法： **



\- find(callback): 用于查找满足条件的第一个元素

\- findIndex(callback)：用于查找满足条件的第一个元素的下标

\- fill(data)：用指定的数据填充满数组所有的内容

\- copyWithin(target, start?, end?): 在数组内部完成复制

\- includes(data)：判断数组中是否包含某个值，使用Object.is匹配

![1607221377360](../笔记图片(勿删)/1607221377360.png)

![1607221402028](../笔记图片(勿删)/1607221402028.png)

## 38.[拓展]类型化数组

**数字存储的前置知识**

1. 计算机必须使用固定的位数来存储数字，无论存储的数字是大是小，在内存中占用的空间是固定的。

2. n位的无符号整数能表示的数字是2^n个，取值范围是：0 ~ 2^n - 1

3. n位的有符号整数能表示的数字是2^n个，取值范围是：-2^(n-1) ~ 2^(n-1) - 1

4. 浮点数表示法可以用于表示整数和小数，目前分为两种标准：
   1. 32位浮点数：又称为单精度浮点数，它用1位表示符号，8位表示阶码，23位表示尾数
   2. 64位浮点数：又称为双精度浮点数，它用1位表示符号，11位表示阶码，52位表示尾数

5. JS中的所有数字，均使用双精度浮点数保存

**类型化数组**

类型化数组：用于优化多个数字的存储

具体分为：

- Int8Array： 8位有符号整数（-128 ~ 127）
- Uint8Array： 8位无符号整数（0 ~ 255）
- Int16Array: ...
- Uint16Array: ...
- Int32Array: ...
- Uint32Array: ...
- Float32Array:
- Float64Array

1. 如何创建数组

```js

new 数组构造函数(长度)

数组构造函数.of(元素...)

数组构造函数.from(可迭代对象)

new 数组构造函数(其他类型化数组)

```


2. 得到长度

```js
数组.length   //得到元素数量
数组.byteLength //得到占用的字节数
```

3. 其他的用法跟普通数组一致，但是：

- 不能增加和删除数据，类型化数组的长度固定
- 一些返回数组的方法，返回的数组是同类型化的新数组

