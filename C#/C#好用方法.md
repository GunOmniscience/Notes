# C#好用方法

## **1.开平方**

Math.Sqrt(要开平方的数);

名称空间:System

## **2.开任何方**

Math.Pow(要开幂的数，要开的幂的数字);

名称空间:System

## **3.如何精确保留小数点后几位**

第一种:

```c#
double a = 1.123456789; 
string b = Convert.ToDouble(a).ToString("0.0000");
Console.WriteLine(b); 
//----------------- //1.1234 //----------------- 
```

第二种：(强烈推荐)

```c#
double a = 1.1; Console.WriteLine("{0:f4}",a);
//结果：1.1000 
```



## **4.生成随机数**

```c#
Random r = new Random(); int a = r.Next(1,101) //包含1不包含100[1~100) 
```



## **5.在已有的字符串内插入字符串**

```c#
string a = "郑文杰"; a = a.Insert(0,"zheng");
// 结果zheng郑文杰 
```



## **6.查找一个字符在一个字符串内的第几下标**

```c#
string a = "郑文杰";
int b = a.IndexOf('郑'); 
// 返回0 //如果返回-1说明这个值不纯在 
```



## **7.删除从输入字符开始到结束的字符串(具有重载)**

```c#
string a = "郑文杰";
a = a.Remove(1); 
// 结果：郑 
```



## **8.将输入的字符在当前字符串中的所有这个字符替换成第二个输入的字符**

```c#
string a = "郑文杰郑"; 
a = a.Replace('郑','z');
// 结果:z文杰z 
```



## **9.判断这个字符串是不是以输入的字符开头的**

```c#
string a = "郑文杰";
bool b = StartsWith("郑文杰");
//True bool c = StartsWith("文杰"); 
//False 
//只要与它比较的字符串内有不一样的就是False。
```



## **10.判断输入的字符串在指定字符串内是否出现**

```c#
string a = "郑文杰";
bool b = Contains("p");
//False bool c = Contains("郑"); //True 
```

## 11.数组常用的方法

![](F:\Typora\笔记图片(勿删)\批注 2020-02-25 132125.jpg)

### 清除元素值：Array.Clear()

​						功能：将数组中某个区间的元素设置为默认值

​						参数列表：需要使用该方法的数组名，区间的开头(数组下标)，区间的结尾(数组下标)

​						返回值类型：void

```c#
int[] arr = new int[]{1,2,3,4};
Array.Clear(arr,1,2);
//arr中的元素值变为1,0,0,4.
```

### 复制元素：Array.Copy()

​					功能：从第一个元素开始复制到设置的长度结束，将第一个数组中的元素，复制到第二个数组中。

​					参数列表：复制数组名，粘贴数组名，长度

​					返回值类型：void

```c#
int[] arr = new int[]{1,2,3,4};
int[] second = new int[4];
Array.Copy(arr,second,4);
//second数组中的元素结果为1，2，3，4；
```

#### 				数组名.CopyTo()

​				功能：将这个数组内的元素复制到另一个数组中，它将会复制这个数组的长度大小-1次所以我们一般第二个参数写0，否则数组下标越界

​				参数列表：粘贴数组，0

​				返回值类型：void

```c#
int[] arr = new int[]{1,2,3,4};
int[] second = new int[4];
arr.CopyTo(second, 0);
//second最终的结果为:1，2，3，4
```

### 查找元素Array.IndexOf()(具有重载)

​				功能：在一维数组中查找目标内容，并返回与其第一个匹配的内容的索引

​				参数列表：数组名，查寻内容

​				返回值类型：int

```c#
int[] arr = new int[]{1,23,4};
int a = Array.IndexOf(arr, 23);
//a为1
```

#### 			Array.LastIndexOf()

​			功能：在一维数组中查找目标内容，并返回与其最后一个匹配的内容的索引

​			参数列表：数组名，查询目标

​			返回值类型：int

```c#
int[] arr = new int[]{1,2,3,1};
int a = Array.LastIndexOf(arr,1);
//a为4
```

### 排序Array.Sort()

​			功能：对一维数组进行升序排序

​			参数列表：数组名

​			返回值类型：void

```c#
int[] arr = new int[]{2,34,5689,1};
Array.Sort(arr);
//arr排序后结果为1,2,34,5689
```

### 反转数组Array.Reverse()

​			功能：将数组内容顺序反转

​			参数列表：数组名

​			返回值类型：void

```c#
int[] arr = new int[]{1,2,3,4};
Array.Reverse(arr)
//arr的最终结果为4,3,2,1;
```

### 克隆 数组名.Clone()

​		功能：克隆一个数组的副本

​		参数列表：数组名

​		返回值类型：object(如果要用数组类型接收那么要写显示转化(int[]))

```c#
int[] arr = new int[]{1,2,3};
int[] b = arr.Clone();
//b的结果为1,2,3
```

**注意：克隆的方式和直接数组之间内容相等的赋值方式不一样，它是先在栈内存里面克隆一个一模一样的数组然后再将这个克隆出来的数组给到接收这个克隆的变量里面去的，所以克隆两边的元素变化互不相影响；也就是不是指向的同一个数组而是重新开辟一个新的一模一样的数组然后指向。**

