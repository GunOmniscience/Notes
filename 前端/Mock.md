# Mock

**作用概述：**

​	用于我们前端自己模拟数据(因为我们后端开发接口是需要一个很长的时间的)，Mock它可以随机生成我们想要的数据，然后当我们发送ajax请求时Mock会将我们的请求拦截下来并将随机生成的数据返回给我们，让我们来模拟请求到了数据

## 数据模板定义规范

 **数据模板中的每个属性由 3 部分构成：属性名、生成规则、属性值：** 

```js
// 属性名   name
// 生成规则 rule
// 属性值   value
'name|rule': value
```

**注意：**

- *属性名* 和 *生成规则* 之间用竖线 `|` 分隔。

- *生成规则* 是可选的。

- 生成规则

   

  有 7 种格式：

  1. `'name|min-max': value` 

     不同类型：

     ​	String：重复min-max次我们的属性值

     ​	Number：生成数据的取值范围为min-max(相当于随机数)

     ​	Boolean：形式为('boo|1-5' : false)意思为true和false的部分各占`min/(min + max)`

     ​	Object：形式为`('obj|1-3') : {a:1,b:2,c:3,d:4}`意思为取出1-3个随机属性作为一个对象

     ​	Array：形式为`(arr|1-3):['a','b','c','d']`意思为将数组中的元素随机重复1-3次

     案例：

     ```js
     //属性值为String
     console.log(Mock.mock({
         'name|1-4' : '郑文杰'
     }))//{
     		name : '郑文杰郑文杰'
     	 }
     意思为：当属性值为字符串时第一种格式的形式为重复min-max次数我们的属性值字符串
     字符串的属性值的意义：
     	1. 让我们的规则去给他进行重复的
     
     //属性值为Number
     console.log(Mock.mock({
         'num|1-100' : 12
     }))//{
     		num : 58(随机变的)
     	 }
     数字的属性值的意义：
     	1. 告诉我们的规则我们要生成的是什么数据
         
     //属性值为Boolean
     console.log(Mock.mock({
         'boo|1-5' : false
     }))//{
     		boo:false
     	 }
     
     //属性值为Object
     console.log(Mock.mock({
         'obj|1-3' : {a:1,b:2,c:3,d:4}
     }))//{
     		obj:{a:1,d:4,b:2}
     	 }
        
     //属性值为Array
     console.log(Mock.mock({
         'arr|1-3':['a','b','c','d']
     }))//{
     		arr:["a", "b", "c", "d", "a", "b", "c", "d"]
     	 }
     ```

     

  2. `'name|count': value`

     不同类型：

     ​	String：重复count次我们的属性值

     ​	Booleam：形式为('boo|1' : false)意思为true和false的部分各占50%

     ​	Object：形式为`('obj|3') : {a:1,b:2,c:3,d:4}`意思为取出3个随机属性作为一个对象

     ​	Array：形式为`(arr|1):['a','b','c','d']`意思为向数组中随机取出一个元素作为一个数组

     案例：

     ```js
     //属性值为String
     console.log(Mock.mock({
         'name|3' : '好帅'
     }))//{
     		name : '好帅好帅好帅'
     	 }
     字符串的属性值的意义：
     	1. 让我们的规则去给他进行重复的
     //属性值为Boolean
     console.log(Mock.mock({
         'boo|1' : false
     }))//{
         	boo : true
     	 }
     
     //属性值为Object
     console.log(Mock.mock({
         'obj|3' : {a:1,b:2,c:3,d:4}
     }))//{
     		obj:{a:1,d:4,c:3}
     	 }
      
     //属性值为Array
     console.log(Mock.mock({
         'arr|1':['a','b','c','d']
     }))//{
     		arr:['c']
     	 }
     当count的值大于1则不是随机抽取一个而是重复元素
     ```

     

  3. `'name|min-max.dmin-dmax': value`

     不同类型：

     ​	Number：它的规则形式为(1-100.1-5)意思为整数部分是1-100小数部分为随机生成1-5位的小数

     案例：

     ```js
     console.log(Mock.mock({
         'num|1-100.1-4' : 12
     }))//{
     		num : 58.123
     	 }
     ```

     

  4. `'name|min-max.dcount': value`

     不同类型：

     ​	Number：它的规则形式为(1-100.5)意思为整数部分是1-100小数部分为固定随机生成5位的小数

     案例：

     ```js
     console.log(Mock.mock({
         'num|2-20.2' : 12
     }))//{
     		num : 15.23
     	 }
     ```

     

  5. `'name|count.dmin-dmax': value`

     不同类型：

     ​	Number：它的规则形式为(100.1-5)意思为整数部分是100小数部分为固定随机生成1-5位的小数

     案例：

     ```js
     console.log(Mock.mock({
         'num|100.1-5' : 12
     }))//{
     		num : 100.4587
     	 }
     ```

     

  6. `'name|count.dcount': value`

     

  7. `'name|+step': value`

     不同类型：

     ​	Number：它的规则形式为(100.5)意思为整数部分是100小数部分为固定随机生成5位的小数

     案例：

     ```js
     console.log(Mock.mock({
         'num|100.5':12
     }))//{
     		num : 100.12345
     	 }
     ```

     案例：

     ```js
     console.log(Mock.mock({
         'num1|+1' : 100
     }))//100
     原因：我们这个规则他是可以对我们的初始值进行累加的，只不过我们现在并没有循环所以他给我们返回的是初始值
     ```

  8. 属性值为函数则不需要填写规则：

     作用将函数的返回值作为这个属性的值

     案例：

     ```js
     console.log(Mock.mock({
         'fn' : function (){ return 1 + 2 }
     }))//{
     		fn:3
     	 }
     ```

  9. 属性值为正则表达式不需要填写规则：

     作用随机生成满足正则的数据

     案例：

     ```js
     console.log(Mock.mock({
         'reg' : /[a-z][A-Z][0-9]/
     }))//{
     		reg:bA8
     	 }
          
     console.log(Mock.mock({
         'reg' : /\w\W\s\S\d\D/
     }))//{
     		reg:"a| Z1"因为\S匹配到了一个''字符
     	 }
          
     console.log(Mock.mock({
         'reg':/\d{5,10}/ //随机匹配5-10个数字
     }))//{
     		reg:12345678
     	 }
     ```

     

- ===***生成规则\* 的 含义 需要依赖 \*属性值的类型\* 才能确定。**===

- *属性值* 中可以含有 `@占位符`。

- *属性值* 还指定了最终值的初始值和类型。



**总结：**

- String

  重复字符串

- Number

  随机生成数字

- Object

  随机取出属性

- Array

  随机取出元素、重复数组元素

- Function

  执行函数

- RegExcel

  随机生成满足这个正则的数据



## Mock.Random

**概述：**

​	他是一个工具类，里面拥有很多封装好的方法



### Basic 基础方法(共7个)

#### Mock.Random.boolean()

**概述：**

​	随机生成一个Boolean值



**参数：**

- 不传参

  各50%

- 传参 (min，max，current)

  意思为current的概率为`min/(min+max)`，然后来随机生成Boolean值



#### Mock.Random.natural()

**概述：**

​	随机生成一个自然数(0<=的数)



**参数：**

- 不传参

  默认为：0~JS最大安全整数

- 传参(min，max)

  随机生成min-max位数字

  min默认值为：0

  max默认值为：JS最大安全整数



#### Mock.Random.integer()

**概述：**

​	随机生成整数(有正整数和负整数)



**参数：**

- 不传参

  范围为：-JS安全最大值~JS安全最大值

- 传参(min，max)



#### Mock.Random.float()

**概述：**

​	随机生成一个浮点数



**参数：**

- 不传参

  随机生成一个浮点数

- 传参(min，max，dmin，dmax)

  - Random.float()
  - Random.float( min )
  - Random.float( min, max )
  - Random.float( min, max, dmin )
  - Random.float( min, max, dmin, dmax )

  返回一个随机的浮点数。

  **min**

  可选。

  整数部分的最小值。默认值为 -9007199254740992。

  **max**

  可选。

  整数部分的最大值。默认值为 9007199254740992。

  **dmin**

  可选。

  小数部分位数的最小值。默认值为 0。

  **dmax**

  可选。

  小数部分位数的最大值。默认值为 17。

  ```js
  Random.float()
  // => -1766114241544192.8
  Random.float(0)
  // => 556530504040448.25
  Random.float(60, 100)
  // => 82.56779679549358
  Random.float(60, 100, 3)
  // => 61.718533677927894
  Random.float(60, 100, 3, 5)
  // => 70.6849
  ```



#### Mock.Random.character()

**概述：**

​	随机生成一个字符



**参数：**

- 不传参

  随机生成可打印的所有字符

- 传参(pool)

  pool：字符池(可选)

  如果传入了 `'lower'` 或 `'upper'`、`'number'`、`'symbol'`，表示从内置的字符池从选取：

  ```js
  {
      lower: "abcdefghijklmnopqrstuvwxyz",
      upper: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
      number: "0123456789",
      symbol: "!@#$%^&*()[]"
  }
  ```

  如果未传入该参数，则从 `lower + upper + number + symbol` 中随机选取一个字符返回。

  ```js
  Random.character()
  // => "P"
  Random.character('lower')
  // => "y"
  Random.character('upper')
  // => "X"
  Random.character('number')
  // => "1"
  Random.character('symbol')
  // => "&"
  Random.character('aeiou')
  // => "u"
  ```

  **我们还可以自己写字符池：**

  ```js
  console.log(Mock.Random.character('abc123'));
  此时它随机生成出来的就只有abc123这里面选了
  ```



#### Mock.Random.string()

**概述：**

​	随机生成一个字符串



**参数：**

- 不传参

  随机生成一个3-7位的字符串

- 传参(pool，min，max)

  pool字符池，同上，我们可以自己设置

  min默认值为：3

  max默认值为：7

  ```js
  Random.string()
  // => "pJjDUe"
  Random.string( 5 )
  // => "GaadY"
  Random.string( 'lower', 5 )
  // => "jseqj"
  Random.string( 7, 10 )
  // => "UuGQgSYk"
  Random.string( 'aeiou', 1, 3 )
  // => "ea"
  Random.string( '壹贰叁肆伍陆柒捌玖拾', 3, 5 )
  // => "肆捌伍叁"
  ```



#### Mock.Random.range()

**概述：**

​	返回一个整形数组



**参数：**

- 不传参

  返回一个空数组

- 传参(start，stop，step)

  **start**

  必选。

  数组中整数的起始值。

  **stop**

  可选。

  数组中整数的结束值（不包含在返回值中）。

  **step**

  可选。

  数组中整数之间的步长。默认值为 1。

  每次递增的值，默认为每次加1，我们可以设置成每次加2

  

  只传一个参数指的是**stop**

  ```js
  Random.range(10)
  // => [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
  Random.range(3, 7)
  // => [3, 4, 5, 6]
  Random.range(1, 10, 2)
  // => [1, 3, 5, 7, 9]
  Random.range(1, 10, 3)
  // => [1, 4, 7]
  ```



### Date	日期类方法(共4个)

#### Mock.Random.date()

**概述**：

​	随机生成一个日期，形如：2020-6-16



**参数：**

- 不传参

  随机生成一个形如2020-6-16的日期

- 传参(format)

  **format**

  可选。

  指示生成的日期字符串的格式。默认值为 `yyyy-MM-dd`。

  可选的占位符参考自 [Ext.Date](http://docs.sencha.com/ext-js/4-1/#!/api/Ext.Date)，如下所示：

  | Format | Description                                              | Example      |
  | ------ | -------------------------------------------------------- | ------------ |
  | yyyy   | A full numeric representation of a year, 4 digits        | 1999 or 2003 |
  | yy     | A two digit representation of a year                     | 99 or 03     |
  | y      | A two digit representation of a year                     | 99 or 03     |
  | MM     | Numeric representation of a month, with leading zeros    | 01 to 12     |
  | M      | Numeric representation of a month, without leading zeros | 1 to 12      |
  | dd     | Day of the month, 2 digits with leading zeros            | 01 to 31     |
  | d      | Day of the month without leading zeros                   | 1 to 31      |
  | HH     | 24-hour format of an hour with leading zeros             | 00 to 23     |
  | H      | 24-hour format of an hour without leading zeros          | 0 to 23      |
  | hh     | 12-hour format of an hour without leading zeros          | 1 to 12      |
  | h      | 12-hour format of an hour with leading zeros             | 01 to 12     |
  | mm     | Minutes, with leading zeros                              | 00 to 59     |
  | m      | Minutes, without leading zeros                           | 0 to 59      |
  | ss     | Seconds, with leading zeros                              | 00 to 59     |
  | s      | Seconds, without leading zeros                           | 0 to 59      |
  | SS     | Milliseconds, with leading zeros                         | 000 to 999   |
  | S      | Milliseconds, without leading zeros                      | 0 to 999     |
  | A      | Uppercase Ante meridiem and Post meridiem                | AM or PM     |
  | a      | Lowercase Ante meridiem and Post meridiem                | am or pm     |
  | T      | Milliseconds, since 1970-1-1 00:00:00 UTC                | 759883437303 |

  ```
  Random.date()
  // => "2002-10-23"
  Random.date('yyyy-MM-dd')
  // => "1983-01-29"
  Random.date('yy-MM-dd')
  // => "79-02-14"
  Random.date('y-MM-dd')
  // => "81-05-17"
  Random.date('y-M-d')
  // => "84-6-5"
  ```



#### Mock.Random.time():

**概述：**

​	随机返回一个形如06：21：12的时间



**参数：**

- 不传参

  随机返回一个形如06：21：12的时间

- 传参(format)

  **format**

  可选。

  指示生成的时间字符串的格式。默认值为 `HH:mm:ss`。

  > 可选的占位符参考自 [Ext.Date](http://docs.sencha.com/ext-js/4-1/#!/api/Ext.Date)，请参见 Random.date( format? )。

  ```
  Random.time()
  // => "00:14:47"
  Random.time('A HH:mm:ss')
  // => "PM 20:47:37"
  Random.time('a HH:mm:ss')
  // => "pm 17:40:00"
  Random.time('HH:mm:ss')
  // => "03:57:53"
  Random.time('H:m:s')
  // => "3:5:13"
  ```



#### Mock.Random.now()

**概述：**

​	返回当前的日期和时间字符串  2020-06-16 14:33:00

**参数：**

- 不传参

  返回形如2020-06-16 14:33:00的当前时间

- 传参

  **unit**

  可选。

  表示时间单位，用于对当前日期和时间进行格式化。可选值有：`year`、`month`、`week`、`day`、`hour`、`minute`、`second`、`week`，默认不会格式化。

  

  **如果设置了unit的值则表示unit的这个数据才是当前的数据，其他的则为默认数据**

  

  week返回的是离我们当前最近的星期天的日期

  

  

  **format**

  可选。

  指示生成的日期和时间字符串的格式。默认值为 `yyyy-MM-dd HH:mm:ss`。可选的占位符参考自 [Ext.Date](http://docs.sencha.com/ext-js/4-1/#!/api/Ext.Date)，请参见 [Random.date(format)](https://github.com/nuysoft/Mock/wiki/Date#date)。

  > `Random.now()` 的实现参考了 [Moment.js](http://momentjs.cn/docs/#/manipulating/start-of/)。

  ```js
  Random.now()
  // => "2014-04-29 20:08:38 "
  Random.now('day', 'yyyy-MM-dd HH:mm:ss SS')
  // => "2014-04-29 00:00:00 000"
  Random.now('day')
  // => "2014-04-29 00:00:00 "
  Random.now('yyyy-MM-dd HH:mm:ss SS')
  // => "2014-04-29 20:08:38 157"
  
  Random.now('year')
  // => "2014-01-01 00:00:00"
  Random.now('month')
  // => "2014-04-01 00:00:00"
  Random.now('week')
  // => "2014-04-27 00:00:00"
  Random.now('day')
  // => "2014-04-29 00:00:00"
  Random.now('hour')
  // => "2014-04-29 20:00:00"
  Random.now('minute')
  // => "2014-04-29 20:08:00"
  Random.now('second')
  // => "2014-04-29 20:08:38"
  ```



### Image 图片类方法(共2个)

#### Mock.Random.image()

**概述：**

​	随机生成一个图片地址(是可打开的)



## 使用Mock拦截Ajax

条件：url地址和ajax请求的地址一致

# Mock.mock()

mozhi.gyy edited this page on 16 Dec 2015 · [4 revisions](https://github.com/nuysoft/Mock/wiki/Mock.mock()/_history)

### Mock.mock( rurl?, rtype?, template|function( options ) )

根据数据模板生成模拟数据。

### Mock.mock( template )

根据数据模板生成模拟数据。

[JSFiddle](http://jsfiddle.net/nuysoft/Y3rg6/7/)

### Mock.mock( rurl, template )

记录数据模板。当拦截到匹配 `rurl` 的 Ajax 请求时，将根据数据模板 `template` 生成模拟数据，并作为响应数据返回。

[JSFiddle](http://jsfiddle.net/nuysoft/BeENf/6/)

### Mock.mock( rurl, function( options ) )

记录用于生成响应数据的函数。当拦截到匹配 `rurl` 的 Ajax 请求时，函数 `function(options)` 将被执行，并把执行结果作为响应数据返回。

[JSFiddle](http://jsfiddle.net/nuysoft/2s5t5/15/)

### Mock.mock( rurl, rtype, template )

记录数据模板。当拦截到匹配 `rurl` 和 `rtype` 的 Ajax 请求时，将根据数据模板 `template` 生成模拟数据，并作为响应数据返回。

[JSFiddle](http://jsfiddle.net/nuysoft/Eq68p/3/)

### Mock.mock( rurl, rtype, function( options ) )

记录用于生成响应数据的函数。当拦截到匹配 `rurl` 和 `rtype` 的 Ajax 请求时，函数 `function(options)` 将被执行，并把执行结果作为响应数据返回。

[JSFiddle](http://jsfiddle.net/nuysoft/6dpV5/5/)

### rurl

可选。

表示需要拦截的 URL，可以是 URL 字符串或 URL 正则。例如 `/\/domain\/list\.json/`、`'/domian/list.json'`。

### rtype

可选。

表示需要拦截的 Ajax 请求类型。例如 `GET`、`POST`、`PUT`、`DELETE` 等。

### template

可选。

表示数据模板，可以是对象或字符串。例如 `{ 'data|1-10':[{}] }`、`'@EMAIL'`。

### function(options)

可选。

表示用于生成响应数据的函数。

#### options

指向本次请求的 Ajax 选项集，含有 `url`、`type` 和 `body` 三个属性，参见 [XMLHttpRequest 规范](https://xhr.spec.whatwg.org/)。

> 从 1.0 开始，Mock.js 通过覆盖和模拟原生 XMLHttpRequest 的行为来拦截 Ajax 请求，不再依赖于第三方 Ajax 工具库（例如 jQuery、Zepto 等）。



### 案例

```js
Mock.mock('js/data.json',{
    'status' : 'success',
    'msg' : '查询成功',
    'data|100' : [{
        'id|+1' : 1,
        剩下的json内容同理
    }]
})
```



## 数据占位符

```js
console.log(Mock.mock('@random里面的方法名'))
console.log(Mock.mock('@EMAIL'))//随机生成一个邮箱地址
console.log(Mock.mock('@CITY(true)'))//随机生成一个邮箱地址
```

可使用大写也可使用小写



## 拓展Mock的方法

```js
Random.extend({
    constellation: function(date) {
        var constellations = ['白羊座', '金牛座', '双子座', '巨蟹座', '狮子座', '处女座', '天秤座', '天蝎座', '射手座', '摩羯座', '水瓶座', '双鱼座']
        return this.pick(constellations)
    }
})
Random.constellation()	
```

