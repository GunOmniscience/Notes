# C#

## 1.封装字段

```c#
private string _name;
public string Name{
    get{
        return _name;
    }
    set{
        _name = value;
    }
}
```

这种方法我们可以进行一些逻辑判断，进行值约束

```c#
public string name{get; set;}
```

这种方法可以通过快捷键 `prop 属性名+tab+tab` 快捷生成

劣势：不可以进行逻辑判断只能进行普通的访问器读取

> 这种方法是在C#3.0中提出来的



## 2..NET框架的核心组成

![1607572305758](../笔记图片(勿删)/1607572305758.png)

## 3.C#中数据类型分类

![1607577004164](../笔记图片(勿删)/1607577004164.png)

## 4.结构

**标准语法：**

```c#
访问修饰符 struct 结构名
{
    //结构体
}
```

**结构体：**

1. 结构中可以有字段，也可以有方法
2. 定义时，结构中的字段不能被赋初值

```c#
public struct Student{
    public int id;
    public int age;
    public void add(){
        
    }
}
```

**结构的使用：**

1. 无需new，可直接Student stu,然后stu.结构体即可

**劣势：**

1. 因为结构是值类型，在我们每次声明一个结构时，他就会新开辟一个内存空间，所以很耗费内存空间，一般不用

## 5.装箱和拆箱

> 值分为值类型和引用类型，两者可以互相转换

**概念：**

装箱：将值类型的值转换成引用类型

拆箱：将引用类型的值转换成值类型

**示例：**

```c#
int i = 1;
object o = i;//装箱
int j = (int)o;//拆箱
```

**注意：**

1. 拆箱时，被转换的引用类型的值必须能够转换成目标值类型
2. 装拆箱因为存储形式的不同所以会消耗大量的性能，应尽量减少装拆箱，可使用`泛型`进行优化

## 6.方法参数中的ref

**使用：**

定义时：

```c#
public void test(ref a){}
```

调用时：

```c#
test(ref a);
```

**底层：**

它会将这个变量(不管是引用还是值类型)的地址传过去而并不通过赋值值

## 7.❔同一时间中多次生成随机数问题

**问题：**

为什么在极小的时间间隔中生成的随机数相同？

**解析：**

c#中的random是有跟当前时间戳有关系的，经过实验，大致在 `15毫秒` 内生成的随机数将一致

## 8.❕快速对对象属性进行赋值

在常规的对象初始化中我们也许有的时候需要这样对对象的属性值进行赋值：

```c#
class Student{
    public string name;
    public int age;
}
Student stu = new Student();
stu.name = "邱子婕";
stu.age = 17;
```

而有了我们现在的新出的语法糖了之后我们可以这么对对象进行赋值：

**语法糖：**

```c#
Student stu = new Student(){name = "邱子婕", age = 17};
```



这样我们就可以利用语法糖快速的对对象进行属性初始化

## 9.ArrayList集合

**特点：**

1. 可以通过索引访问ArrayList中的元素，索引从0开始

2. ArrayList属于 `System.Collections` 命名空间，这个命名空间包含接口和类，在使用ArrayList前必须using这个namespace

3. ArrayList可以初始指定长度也可以不指定

   ```c#
   using System.Collections;
   ArrayList Student = new ArrayList();
   ArrayList Student1 = new ArrayList(6);
   ```

4. 集合的长度是可以动态增加的，当我们指定了多长度的集合，那么未赋值的则为null，它的长度也会根据我们删除的元素然后去减少长度

5. ArrayList的常用方法及属性：

   | 属性名称 | 说明                            |
   | -------- | ------------------------------- |
   | Count    | 获取ArrayList中实际包含的元素数 |

   | 返回值类型 | 方法名称             | 说明                                                         |
   | ---------- | -------------------- | ------------------------------------------------------------ |
   | int        | Add(Object value)    | 将对象添加到ArrayList中实际包含的元素数                      |
   | void       | RemoveAt(int index)  | 移除ArrayList指定索引处的元素，`集合中删除了前面的元素，后面的元素是会进行补齐的，也就是说我们的下标会变` |
   | void       | Remove(Object value) | 从ArrayList中移除特定对象,`比较的是对象的地址，使用的是object里面的equals方法，如果我们无法获取到相同的地址则无法删除集合中的这个元素` |
   | void       | Clear()              | 从ArrayList中移除所有元素                                    |

6. 集合中是可以存放任何数据类型的

7. 存入集合的数据会被进行装箱操作，所有的数据都会变成 `Object` 类型，我们想要使用这个数据需要对其进行拆箱操作 `(数据类型)集合中的数据` 这样就可以进行拆箱成我们存入的数据的原本数据类型然后进行使用了，拆箱后的结果和装箱前没有任何区别，所以`ArrayList中的所有元素都是对象的引用`

**使用案例：**

```c#
using System.Collections;
class Student{
    public string name;
    public int age;
}
Student stu = new Student(){name = "邱子婕", age = 17};
Student stu1 = new Student(){name = "郑文杰", age = 16};
ArrayList arrList = new ArrayList();
arrList.add(stu);
arrList.add(stu1);
```

**集合初始化器：**

可是我们会发现我们这样一个一个的往集合里面进行添加是否拥有太过于效率低下，那我们能不能和对象初始化语法糖一样进行快速赋值呢？当然是可以的，我们拥有一个叫做 `集合初始化器` 的东西类似于对象初始化器：

```c#
ArrayList arrList = new ArrayList(){
  new Studnet(){name = "邱子婕", age = 17},
  new Student(){name = "郑文杰", age = 16}
};
```

**遍历ArrayList：**

for：

```c#
using System.Collections;
ArrayList arrList = new ArrayList(6);
for(int i = 0; i < arrList.Count; i++){
    Console.WriteLine((int)arrList[i]);
}
```

foreach:

![1607613584075](../笔记图片(勿删)/1607613584075.png)

## 10.Hashtable

**问题：**

当ArrayList中的元素变化频繁是，要跟踪某个元素的下标就比较困难了。那么，能不能给集合中的每个元素分别起一个有意义的关键字，然后通过关键字来访问其中的元素呢？

**Hashtable概述：**

Hashtable通常称为哈希表，也成为字典，因为它的存储方式很像我们字典中的通过关键词找到一大堆的相关信息

**Hashtable的存储形式：**

| key  | value |
| :--: | :---: |
| key  | value |

**Hashtable的特点：**

1. Hashtable也属于System.Collections命名空间，它的每个元素都是以键值对的形式存储

2. Hashtable的常用方法及属性

   ![1607615381745](../笔记图片(勿删)/1607615381745.png)

3. 键的类型是字符串，所以我们存值和读值都是这么写的

   存值：hashTable.add("001", 值)

   取值：hashTable["001"]

   通过键取值取的是value，而通过foreach遍历出来的东西就不是了

4. 因为Hashtable没有下标可言，所以Hashtable只能通过foreach进行遍历

   因为我们遍历出来的是一个键值对，可是我们并没有任何一个数据类型是键值对形式的，于是C#就出来了这个一个结构类型的类型 `DictionaryEnty` 类型，我们通过它来遍历我们的Hashtable可以通过 `de.key` 来获取键然后通过 `de.value` 来获取值

   ![1607615981834](../笔记图片(勿删)/1607615981834.png)

   如果我们不使用DictionaryEnty那么我们则只能foreach Hashtable的keys或者values了然后将其打印出来

## 11.List`<T>`(代替ArrayList)

**ArrayList存在的问题：**

因为ArrayList存入的数据全部都会变成Object类型，且传入的数据也并没有类型的限制，也就是说我可以传入多种类型的数据，可是这样一来当我在遍历ArrayList集合时我们得对其进行拆箱，可是我们ArrayList集合中都是Object类型我们无从判断，那么我们此时如果对拥有多种类型的ArrayList集合进行遍历则会触犯拆箱的规则 "即将拆箱的类型必须是被拆箱数据可转换的类型" 所以我们此时就会报错了，那么我们能不能对集合可填入的类型限制一下呢？

**泛型集合List```<T>```：**

1. 存在于 `System.Collections.Generic` 命名空间中，这个命名空间中定义了许多泛型集合类，这些类可以代替我们之前所学习的ArrayList,Hashtable

2. 基本语法：

   ```c#
   List<指定的类型> 集合名 = new List<指定的类型>(); 
   ```

3. 对指定类型进行约束：

   ```c#
   using System.Collections.Generic;
   List<Computer> comList = new List<Computer>(){
   	new Computer(){name = "qwqweq"},
   	new Computer(){name = "oxhhso"},
       new Student(){name = "邱子婕"}//此时会报错，无法将List.Computer类型转换成List.Student类型
   };
   ```

4. List<指定类型>与ArrayList的区别：

   不同点：

   1. List<指定类型>对填入的元素进行类型约束

   2. 添加/读取值类型无需拆箱，装箱：`这说明List<指定类型>泛型集合的不仅仅是语法上在效率上也高出了ArrayList集合一大截`

      ```c#
      using System.Collections.Generic;
      List<Computer> comList = new List<Computer>(){
          new Computer(){name = "fqwfq"}
      };
      Computer com = comList[0];
      Console.WriteLine(com.name);
      ```

   相同点：

   1. 两者的API完全相同，ArrayList拥有的List全都有

   

## 12.Dictionary```<K,V>```(代替Hashtable)

k代表键的类型约束，v代表值得类型约束

**语法：**

```c#
Dictionary<键的指定类型，值的指定类型> 泛型集合名 = new Dictionary<键的指定类型，值得指定类型>();
```

**用法：**

![1607696512789](../笔记图片(勿删)/1607696512789.png)

**与Hashtable的区别：**

和List泛型集合一样

**泛型集合Dictionary`<K,V>`比传统Hashtable多出来的一种foreach遍历方式：**

![1607697594786](../笔记图片(勿删)/1607697594786.png)



## 13.泛型类

当我们方法的返回值不确定时，我们就可以让类变成泛型类

![1607993938780](../笔记图片(勿删)/1607993938780.png)

