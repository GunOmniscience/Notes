# C#语法

## 1.输出语句：

```c#
Console.WriteLine("Hello,World!!!"); //独占一行输出 
Console.Write("Hello,World!!!"); //不独占一行输出 
```



## 2.不同于Java的变量类型：

字符串：string

布尔型：bool

## **3. 不同于Java的语法：**

foreach循环：

```c#
int[] a = new int[]{1,2,3,4};
foreach(int lookOver in a) 
{    
    Console.WriteLine(lookOver); 
} 
```



## **4.不同于Java的关键词:**

导包关键词：using

## **5.C#的输入方法：**

Console.ReadLine()方法：   从控制台窗口读取一行文本，返回string值

Console.ReadKey()方法：   监听键盘事件，可以理解为按任意键执行

**如果想输入int类型的数字则需要转化:**

Convert.ToInt32(Console.ReadLine()); //int类型

Convert.ToInt64(Console.ReadLine()); //long类型

Convert.ToInt16(Console.ReadLine()); //short类型

Convert.ToDouble(Console.ReadLine()); //double类型

Convert.ToSingle(Console.ReadLine()); //char类型

## **6.关于控制台的属性:**

Console.Title = "我的小程序"; //这样控制台的左上角标题就是我的小程序了 

## **7.C#中的数据类型**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\2f7b489da0224ed8937dca3378b745c2\9efd015717ac42c4abd3dad078a2f236.jpg)

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\2b6d8e466a934d9a86eb6940df366e5c\cc8dd3d6147f4f18844bf29259be6ff7.jpg)

**Unity整数一般用int 小数一般用float**

**folat和double类型在0.1的时候会出错，所以我们如果想要特别精确则用decimal。**

## **8.输出的第二种方法/标准数字字符串格式化**

```c#
int b = 10; string a = string.Format("小明今年{0}岁了",b); //Format里面的索引不能大于参数列表否则报错 
//也可以这样 Console.WriteLine("小明今年{0}岁了",b);
//这种方法有个好处可以标准化字符串
//1.货币标准化“:c” 
Console.WriteLine("{0:c}",b); 
//货币标准化 
//------------------------ 
//￥10.00 
//------------------------- 
//2.数字标准化“:dn” n表示想是几位数 
Console.WriteLine("{0:d2}",b); 
//表示这个结果必须是两位
//如果是1则会变成01
//而如果是10则就是10              可以用来做时间 
//3.小数保留标准化        :fn，n表示想保留多少位小数 
double c = 1.1; Console.WriteLine("{0:f4}",c); 
//结果:1.1000 
//4.百分率标准化  :pn，n表示要保留多少个小数不写的话默认保留两位
Console.WriteLine("0:p",0.1); 
//则会输出10.00%，而我们不想要两个0的话我们在p后面加0 
```



## **9.转义字符**

想要输出的符号报错时在前面加\

如果想要字符串存一个空的东西则里面填\0

回车换行\r\n

## **10.一个.NET特别重要的部内原理**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\da607eabbd724926a7e7d4a1114da719\49a159d9fd824adeae7a83f5edb20a2a.jpg)

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\7e4ef47e03d4423bb2e84226045333de\e2cf5bbce5454dc89a624785f72a565b.jpg)

CLR实现跨平台，哪个平台就用哪个平台的标准

## **11.定义数组和Java一样**

```c#
int[] a = new int[]{1,2,3}; 
```

**foreach循环:**

```c#
foreach(int b in a) 
{    
    Console.WriteLine(b); 
} 
```



## **12.数据类型转换**

1.parse转换: string类型转其他数据类型，其值必须像；

```c#
string a = "123"; 
int b = int.parse(a); 
```

2.ToString()转换:	其他类型转string类型；

```c#
int a = 123; 
string b = a.ToString(); 
```

3.获取字符串中的每个字符:

```c#
string a = "123"; 
char b = a[0];
//'1'
string c = b.ToString(); 
//"1",这个时候就可以用parse转换成int或者别的数据类型了 
int d = int.parse(c); 
//简便方法 int d = int.parse(a[0].ToString()) 
```



## **13.C#数组各类型的默认值**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\44fec2cf075748059b307f3623ea1ea3\21fa0cf9cce345239f417197d2624ca0.jpg)

## **14.var类型(适用于类型名特别长的时候我们为了简洁可以使用var代替)**

根据值来判断数据类型

```c#
var a = false //a是bool类型 
```



## 15.父类与子类(例:Array)

当方法的参数为Array这个父类的参数那么只要传过来的这个值是它这个父类的子类都可以传过来，Array只是一个例子，我们还会有很多父类。我们也可以用Array＋变量名＝new 数据类型[]数组。

## 16.object类型

object类型是包含所有数据类型，所以当我们声明一个object数据类型的变量我们可以放任意的值。它得出来得类型不会根据值去改变，他的类型就是object类型

