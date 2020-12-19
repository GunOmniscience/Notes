#                              **Java**

## 💥存在继承关系的类加载机制

![批注 2020-03-25 104359](F:\Typora\笔记图片(勿删)\批注 2020-03-25 104359.jpg)

## 💥Java中类什么时候加载

1.创建实例

2.用类名调用静态元素时

## 💥创建类的数组

```Java
public Computer computer = new Computer[5];
```

## 💥权限符大小

public > protected(受保护的) > 默认不写 > private

## 💥解决输入异常

因为我们每一个Scanner输入的读取字节不同所以很容易导致我们有一个输入还没有输入它就跳过了，那么我们如何解决这个问题呢？

包装类：

- ​		int--Integer

- ​		char--Character

- ​		byte--Byte

- ​		其余的数据类型都形似与byte。

转化语法：

```java
int a = Integer.parseInt(input.nextLine());
```

以后我们读取数据都用这个方法就不怕不同读取方法读不读取空格的问题而烦恼了。

**异常**：

​		`NumberFormatException`

​		当我们输入的值和前面的想转化为的类型不一致就会出这个异常。

## 💥**Java中的命名规范:**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\735b88200a944cbe835982d21188a56a\5baf3e72a054407ca03900d6ea69d1da.jpg)

## 💥设计类的小机巧:

1.分析一共有几个具体的类

2.分析类和类之间的关系

## 💥设计方法小技巧:

如果是处理引用数据类型的问题时:

一般需要操作就一定要有需要操作的内容；需要参数

判断方法执行完在main方法中的数组的内容会不会改变，如果会那么不需要返回值，如果方法只是更改了方法内的数组的引用(地址)的话则需要返回值。

**一般方法都****需要返回值****。可以自己亲身体验。**

## 💥构造方法:

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\5c2f0e516a2b4d998e328f98ab5e1327\b0ae2a00614e4b9bbb7f36671e43581c.jpg)

**注**:因为如果别人不了解你的程序到时候使用的时候就会很迷茫很麻烦；而我一个如果写了原来的构造方法形成构造方法重载这样你和别人都用的舒服。

## 💥this关键字解决重名问题:

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\7ea07c7248054f98a344cdfb01db9d8e\39d7b97f8e7746b9828d28af77ddbdea.jpg)

- 当我们遇到名字重复例如:(一个我们自己传参的变量名字和类中属性的名字重复了，这个时候代码就会就近原则的选择以为我们前面的的类中的属性的名字也是我们的传参变量名，那么这个时候我们就可以使用this关键字来告诉代码我这个是一个对象的的属性。)

```java
public class P{    
    public String name;        
    public P(String name){      
        this.name = name;
        //这个时候前面的name就不会和后面的name冲突了，它就会       
        //知道我前面的name是对象里面的属性。  
    } 
}
```



## 💥方法之间互相调用会产生的小错误:

- 方法之间能互相调用的写法不会有错，但是我们的方法是在栈内存里执行的，当我们的方法在栈内存中调了另一个方法，那么我们这个方法还在等待调的那一个方法返回东西，而我们调的那一个方法又生成了另一个方法去调用也在等待那么我们全部都在等待，所以我们就出现了一个**栈内存运行时错误StackOverFlowErro**。

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\2ef433009a5c48eebabf408b9988c205\8a28a0da91114a64b646aa997d615098.jpg)

## 💥数据类型之间的转换:

- 例如引用类型转成基本数据量类型可使用包装类

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\d867e26de16e4d8395d9a17042e6ecb2\78e27a6be02e092df3ca8aa55d28e506.jpg)

- 基本类型转引用数据类型:

1. 在结果输出的时候加一个""，例如5+""结果为字符串类型的5这时他们两之间的加号就成了连接符而不是加号

**注**:仔细看19行到20行之间的变换，如果拿abc来用intneger包装类进行转换则会出现一个异常**NumberFormatException** 

## 💥如果产生运行时异常可是我们不想让错误显示出来:

```java
try{    int a = input.nextInt();   
    System.out.println(a); 
   }catch (Exception e){
    //Exception代表产生运行时异常时，而e则是自己随便取的变量名，我们通常用e来表示Exception类. 
    System.out.println("输入错误！"); 
    //当我们的try中的语句执行产生运行时异常的时候就会执行我们的catch里面的语句。 
}finally{
    //是不管怎么样都要执行的方法体。我们可写可不写看情况。这是try的一个完整体系。    
} 
```



## 💥输入字符串的时候想输入空格小技巧:

## ![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\fadb4fd7cca5422f85b97aad3a9b5522\fd32fe9e96834b67bd506b89de14cd8d.jpg)1.Java中的输入：

- 导入Scanner类的包

```java
import java.util.Scanner; 
```



- 在函数中调用Scanner类

```java
Scanner input(名字，可更改) = new Scanner(System.in); 
```



- 拿一个变量接收输入的值

```java
//int类型 
int i = input.nextInt(); 
//double类型 
double i = input.nextDouble(); 
//String类型 
String i = input.next(); 
//Boolean类型 
boolean i = input.nextBoolean(); 
```



## 2.数组的写法：

- 普通写法

```java
int[] i = new int[]{1,2,3}; 
```



- 因为前面定义过一个int类型的数组所以后面的new int[]可以省略

```java
int[] i = {1,2,3}; 
```



- 如果前面只是定义了输入i，而到后面才来赋值，则后面赋值时需要new 数据类型[]

```java
//第一种情况 
int[] i;
i = new int[]{1,2,3}; 
//第二种情况 
int[] i = new int[3];  
//new后面的int的[]里面接的时数组的长度(这么写必须加)
i = new int[]{1,2,3}; //因为前面规定了长度为3,所有后面只能存放3个元素
```



- 增强for

i

```java
nt[] a = new int[]{1,2,3,4};
for(int i//定义的变量(用来接收“:”后面数组内的所有元素) : a//需要接收的数组){   
    System.out.println("i"); } 
    //-------------------------   
    //a数组里面的所有元素    1    2    3   4 
    //-------------------------     
```



- 注意:

​            见到new关键字，相当于，在堆内存中申请开辟一块新空间

![](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\9a1b578be53c4d3e9aa08aae6d886a06\数组.png)

## **3.随机数的使用：**

- 基本语法

```java
int random = (int)(Math.random()); //Math.random()的随机数的默认范围是0~1，包括0不包括1 
```



- 随机生成1~4之间的随机数

```java
int random = (int)(Math.random()*3)+1; 
```



## **4.冒泡排序：**

```java
int[] array = new int[]{5,2,3,1,4};
for(int i = 1; i <= 4; i++){ 
    //控制循环次数(一轮比出一个比4轮)  
    for(int j = 4; j >= i; j--){ 
        //优化循环次数将 j >= 1改成 j >= i;      
        int x = array[j]; //因为比出来了所以两数进行互换       
        array[j] = array[j-1];       
        array[j-1] = array[j];  
    }
} 
```



## **5.判断字符串数组是否是空：**

- String类型new出来的是一个null空串所以不能调equals()方法进行判断只能使用==

```java
String[] a = new String[5];
//默认值为:null if(a[0] == null){    //true } 
```



## 6.二维数组：

- 基本规则

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\232d6bfd7c65478bbee792dd57b93e18\5585402341114e3e902a0d8bd4b6aeed.jpg)

- 查询二维数组内容

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\cb80664391ec4b9587aa0bc2670c2eaa\820425cd342146daa9e1083aca9fd869.jpg)

#                       Java类和对象

## **1.属性的基本语法：**

- **属性的基本语法(权限修饰符 【特征修饰符】 数据类型 【=值】，“【】”表示可省略）。** 

```java
public class a{   
    public int a;
} 
```



## **2.如何在main方法中使用自己定义出来的类：**

```java
//在第一个类中
public class a{   
    public int a;    
    //因为类是一个引用类型所以它有返回值(与数组一样) } 
    //在第二个类中 
    public class b{  
        public static void main(String[] args){   
            a a = new a();     
            a.a = "Hello,World";   
            System.out.println(a.a);     
            /*        
            ------------------------------       
            Hello,World       
            ------------------------------       
            */    } } 
```

因为类也是一个引用类型，所以也有默认值；

## **3.类与数组的特性一致：**

```java
//第一个类中
public class Demo1{ 
    public int a; 
} 
//第二个类中
public class Demo2{   
    public static void main(String[] args){      
        a a = new a(); //a变量指向了一个新的空间       
        a.a = 1; //给空间里面的a赋值为1        
        a b = a; //b变量指向了变量a指向的空间       
        b.a = 2; //给b变量指向的空间(a变量指向的空间)中的a赋值为2    
        System.out.println("a:" + a.a + ",b:" + b.a);       
        /*      
        ----------------------------------       
        a:2,b:2     
        ----------------------------------      
        */    } 
```



## **4.方法：**

- 方法的结构(“【】”为可省略部分）:

  权限修饰符 【特征修饰符】 返回值类型 方法名字 (参数列表) 【抛出异常】 【{

​                     方法体       

​              }】

```java
//第一个类中 
//权限修饰符 返回值类型 方法名 (){     } 
public class Demo1{ 
    public void a(){     
        System.out.println("你好");    
    } 
} 
//第二个类中 
public class Demo2{    
    public static void main(String[] args){      
        Demo1 a = new Demo1();      
        a.a();       
        /*      
        --------------------------------------------       
        你好      
        --------------------------------------------       
        */   
    }
} 
```



### **返回值类型的区别：**

- **类型: void 基本和引用数据类型**
- **如果void代表没有返回值类型所以不能有返回值并且不能接收；想要接受返回值得在返回值类型写明你想要返回的值的数据类型。**

### **方法重载：**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\4dd7017cf8814e9180619a07adfea38f\e57ef92ecdfd4466bc91d84086b326e8.jpg)

### **方法重载之动态参数列表：**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\9e1d118b0f39471a9a7c60281158108b\32a4da88bde8499b8ca2601b3685248b.jpg)

**注**:动态参数列表在方法的参数中只能存在一份，且放置在参数的末尾。

### **构造方法：**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\2ae1c4b5e58148308be5cc9f5f465f3d\e87b90412a3c420b9495b6a757593ee0.jpg)

**最大的用处**:我们在main里创建对象的时候我们就可以直接给属性赋值而不需要进行一些麻烦类似与多写一行代码来赋值的现象。

**最优写法**:

```java
/*
*如不了解this请看笔记最前面的小技巧大爆料 
**/ 
public class Person; 
public String name; 
public int age; 
public String sex;
//构造方法 
public Person(){} 
public Person(String name,int age,String sex){   
    this.name = name;    
    this.age = age;   
    this.sex = sex;
}
//主方法 
public static void main(String[] args){  
    Person p = new Person(name:"郑文杰",age:15,sex:"男");   
    System.out.println(p.name + "年龄" + age + "性别是" + b);   
    //---------------------------------------   
    //郑文杰年龄15性别是男   
    //--------------------------------------- } 
```



### **程序块：**

- **语法:	{**

​                              **}**

**没有任何东西甚至返回值以及重载不过我们****可以写很多个**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\4cb14fb5c6ce4ac383ee6fd6248ecd7a\4f38c0158bc5422e8c83b6d75d086490.jpg)

​                                                                                                      **⬇**

![img](F:\有道云笔记\qq31BDEC0D05E5A1626E555CD1BA33D617\5fd016fe65804dff8e821e8cf26e24db\40d13ad999604211a584da50a64b925d.jpg)

 

## 5.位运算符

当我们要使用乘或除时我们可以用位运算符

`变量 >> 1`代表这个变量值除以2

`变量 << 1`代表这个变量值乘以2

- 如果是>>2的话那么也就是再多除以一次2
- <<2就相当于再多乘以一次2

## 6.类和类之间的关系

![批注 2020-03-05 140343](F:\Typora\笔记图片(勿删)\批注 2020-03-05 140343.jpg)

### 6.1继承(A is-a B)

如何让一个子类继承一个父类：

1.在子类的后面添加一个关键字`extends`+想要集成的父类

```java
//父类
public class A{
    
}
//需要集成A这个类的子类
public class B extends A{
    
}
```

2.子类可以调用由`public`和`protected`修饰的父类中的属性和方法，当做自己的来使用

```java
//父类
public class A{
    public String name;
    
    public void eat(){
        System.out.println("吃了炖饭");
    }
}
//集成了A这个类的子类
public class B extends A{
    
}
//主方法类
public class C{
    public static void main(String[] args){
        B b = new B();
        b.name = "小杰";
        b.eat();
        System.out.println(b.name);
        //-----------------------
        //结果:吃了炖饭
       // 	  小杰
        //-----------------------
    }
}
```

3.当然孩子也可以拥有自己独特的属性或方法，类似于我会Java而我爸爸不一定会，我爸爸的性格不好而我的性格好等等...

```java
//父类
public class A{
    public String name;
    
    public void eat(){
        System.out.println("吃了炖饭");
    }
}
//集成了A这个类的子类
public class B extends A{
    public boolean xingGe;
    //true好 false不好
    
    public void studyJava(){
        System.out.println("我学习了Java");
    }
}
//主方法类
public class C{
    public static void main(String[] args){
        B b = new B();
        b.name = "小杰";
        b.xingGe = true;
        b.eat();
        b.studyJava();
        System.out.println(b.name);
        System.out.println("子类的性格:" + b.xingGe);
        //-----------------------
        //结果:吃了炖饭
       // 	  学习了Java
        //	  小杰
        //    子类的性格true
        //-----------------------
    }
}
```

4.子类从父类中继承过来的方法不能满足子类需要，可以在子类中重写(覆盖)父类的方法(更多重要的是内容)

![批注 2020-03-05 144440](F:\Typora\笔记图片(勿删)\批注 2020-03-05 144440.jpg)

```java
//父类
public class A{
    public void eat(){
        System.out.println("我吃了饭");
    }
}
//子类
public class B extends A{
    public void eat(){
        System.out.println("我不但吃了饭还喝了汤");
    }
}
//主方法
public class C{
    public static void main(String[] args){
        B b = new B();
        b.eat();
        //输出为：我不但吃了饭还喝了汤
    }
}
```

5.每一个类都有继承类，如果不写extends关键字，默认继承Object，如果写了extends则继承后面那个父类，可以理解为obje类是任何一个引用类型的父类(直接或间接地继承object)。

个人总结:当你继承了一个父类那么你继承的就是这个父类，而你的父类又默认的继承了object这个类所以object类相当于人类的祖先和人之间的关系。

#### object类中的方法：

![批注 2020-03-05 183946](F:\Typora\笔记图片(勿删)\批注 2020-03-05 183946.jpg)

![批注 2020-03-05 184019](F:\Typora\笔记图片(勿删)\批注 2020-03-05 184019.jpg)

`toString()方法后面没写完的是hascode()`

6.Java中继承是单个存在的(单继承) 每一个类只能有一个继承类 (在extends关键字后面只能写一个类)

可以通过传递的方式实现多继承的效果 后续还会有多实现

*7.继承的底层内存图

![批注 2020-03-05 190104](F:\Typora\笔记图片(勿删)\批注 2020-03-05 190104.jpg)

*8.关于this和super的使用

this代替的**是谁调用的它**，并不是当前类

this和super都是指代词：

this指代的是调用他的那个**对象**

super指代的是调用他的那个**对象的父类**

`都能调用一般属性和方法`

`注`：

![批注 2020-03-05 194358](F:\Typora\笔记图片(勿删)\批注 2020-03-05 194358.jpg)

#### 注:

![批注 2020-03-05 165401](F:\Typora\笔记图片(勿删)\批注 2020-03-05 165401.jpg)

### 6.2聚合(A has a B)

1.聚合

将一个类的对象当作另一个类的属性来存储

```java
/*
假设车和轮子的关系
*/

//轮子
public Wheel{
    public String color;//颜色
    public String pinPai;//品牌
    
    //构造方法
    public Wheel(){}
    public Wheel(String color, String pinPai){
        this.pinPai = pinPai;//品牌
        this.color = color;//颜色
    }
    //轮子跑的方法
    public void run(){
        System.out.println("轮子在跑");
    }
}

//车
public Car{
    public String xingHao;//型号
    public String pinPai;//品牌
    public String color;//颜色
    public Wheel wheel = new Wheel;//轮子(类与类之间的关系：聚合)
    
    //构造方法
    public Car(){}
    public Car(String xingHao, String pinPai, String color, Wheel wheel){
        this.xingHao = xingHao;
        this.pinPai = pinPai;
        this.color = color;
    }
    //展示车子
    public void showCar(){
        System.out.println("车子的品牌是" + pinPai + "型号:" + xingHao + "颜色为" + color + "轮子的品牌是:" + wheel.pinPai + "颜色为:" + wheel.color);//引用数据类型的默认值为Null可以作为输出没有问题，但是Null不能使用，所以这里直接使用的话会出现"NullPointException"空指针异常
        wheel.run();
    }
}

//测试
public class Test{
    //主方法
    public static void main(String[] args){
    	Car car = new Car("X6", "宝马", "亮白色", new Wheel("米其林", "浅粉"));
        car.showCar();
        /*
        ----------------------------------------
        车子的品牌是宝马型号:X6颜色为亮白色轮子的品牌是米其林颜色为:浅粉
        轮子在跑
        ----------------------------------------
        */
	}
}
```

### 6.3依赖(use-a/need-a)

一个**类的方法中**使用到了**另一个类的对象**

​	第一个可以在方法中传递参数

​	第二个可以在方法中自己创建

```java
//猪
public class Pig{
    private int weight = 20;//刚出生的小猪的重量
    private String name;//名字
    
    //构造方法
    public Pig(){}
    public Pig(String name){
        this.name = name;
    }
    //小猪被杀方法
    public void beKilled(){
        System.out,println("被杀了，好惨呀！");
    }
    //小猪成长方法
    public void growUp(int month){
        for(int i = 1; i <= month; i++)
        {
            weight = weight * 2;
        }
    }
    //返回小猪重量的方法
    public int zhongLiang(){
        return weight;
    }
    //返回小猪名字的方法
    public String mingZi(){
        return name;
    }
}

//农民(养猪)
public class Farmer{
    
    //养猪
    public Pig yangZhu(){
        Pig pig = new Pig("小花");
        pig.growUp(5);
        return pig;
    }
}

//屠夫
public class tuFu{
    
    //杀猪
    public void killPig(Pig pig){
        Systme.out.println("屠夫执行了杀猪");
        String name = pig.name;
        int weight = pig.weight;
        System.out.println(name + "重量为:" + weight);
        pig.beKilled();
    }
}

//测试
public class Test{
    public static void main(String[] args){
        //创建农夫的实例
        Farmer farmer = new Farmer();
        //创建猪的实例
        Pig pig = new Pig();
        pig.killPig(farmer.yangZhu());
        /*
        ----------------------------------------
        屠夫执行了杀猪
        小花重量为:640
        被杀了，好惨呀！
        ----------------------------------------
        */
    }
}
```



## 7.修饰符

### 	7.1权限修饰符

​		**public 公有的**

​			只要有对象都能访问，不过不能出了这个工程

​		**protected 受保护的**

​			类似于是保护自己子孙利益的修饰符，其他人侵犯不了自己子孙的利益

​			不在同一个包调不到

​			包：只要package后面的名字不一样就代表不同包

​			只有子类能调用，尽管你继承了我，如果你通过创建我父类的对象去访问你也访问不到。

​		**默认不写 默认的**

​			不在同一个包调不到

​			包：只要package后面的名字不一样就代表不同包

​		**private 私有的**

​			不在本类调不到

​		**权限大小从上往下**



#### 		7.1.1修饰类

​			**只有public和默认不写，能修饰类。用public修饰的类名和.java的文件名必须一致**

​			**一个Java文件里面只能有一个被public修饰的类**

​			如果我们一个源码文件里面写了两个类		

```Java
public class A{
    
}
class B{
    
}
```

​			那么我们编译之后我们会生成两个.class的字节码文件，一个A.class 一个B.class

​			**强烈不推荐这么写**



#### 		7.1.2还能修饰什么

​			除了块以外都能修饰



### 	7.2特征修饰符

​		final 最终的 不可更改的

​			**修饰变量**

​				用final修饰的变量如果赋值了就不能再改变了

​				如果没有赋值，则它会给一次赋值的机会给你赋值

​				**类似于常量，或者给这个栈内存空间上了锁**

​				引用类型

​					如果修饰的是引用类型，那么我们锁住的只是那个地址也就是我们的锁只是在栈内存里面，而我们的指向的对内存的内容是可以改变的，而我们的栈内存中存的地址就不能改了，因为被我们锁住了，也就是用final修饰的引用类型都不能在去指向一个新的地址了，如果我们刚开始没有赋值那么我们一样可以有一次机会赋值

​				方法的参数

​					我们只能传参进来，在方法内部不能更改这个值

​			**修饰属性**

​				因为我们的属性它会有初始值，所以Java就规定了用final修饰的属性必须赋初值

​			**修饰方法**

​				final修饰的方法不可以被子类**重写**！！！

​			**修饰类**

​				final修饰的类相当于太监类，也就是不可以被**继承**了！！！

​		**static 静态的**

​				1.可以修饰什么？

​						修饰属性

​						修饰方法

​						修饰块

​						修饰类(内部类)

​				2.特点

​						2.1 静态元素在类加载时就初始化了 创建的非常早 此时没有创建对象

​						2.2 静态元素存储在静态元素区中 每一个类有自己的静态元素区 不冲突

​						2.3 静态元素只加载一次(只有一份)，全部类对象及类本身共享

​						2.4 由于静态元素区加载的时候可能没有创建对象 可以通过类名字直接访问

​						2.5 可以理解为静态元素不属于任何一个对象 它属于类

​						2.6 内存管理 栈内存用完即回收 堆内存程序运行完被GC(垃圾回收器)回收 静态元素区GC无法管理 可以粗暴的理解为静态元素区是常驻内存

​						2.7 非静态成员(堆内存)可以访问静态元素(静态元素区) 我们通常这么调用它(类名.静态元素名)

​						2.8 静态元素可以访问静态元素(都存在静态元素区)

​						2.9 静态成员无法访问非静态成员 (个数 一个出发访问一堆名字 说不清 不知道找谁) (静态元素属于类 非静态成员属于对象自己)

​						2.10 静态元素中是不可以出现this或super关键字(静态元素属于类)

![批注 2020-03-16 203947](F:\Typora\笔记图片(勿删)\批注 2020-03-16 203947.jpg)

​		abstract 抽象的

​		native 本地的

​		transient 瞬时的 短暂的---->序列化

​		synchronized 同步的

​		volatile 不稳定的



## 8.Java面向对象的四个特征

​	继承 封装 多态 (抽象)

​	

### 	8.1封装

​		其实一个方法也是一个封装，一个类也是一个封装

​		方法里面封装了我完成这个操作的源码

​		类里面封装了我的属性和方法等等...

​		**通常因为安全性我们的属性都是私有的用方法来修改和获取属性值，那么我们都会遵循一个公约，设置属性值的方法名叫set属性名，获取属性值的方法叫get属性名**

## 9.设计模式

![批注 2020-03-18 194258](F:\Typora\笔记图片(勿删)\批注 2020-03-18 194258.jpg)

​		

### 		9.1单例模式（Singleton)

![批注 2020-03-18 204411](F:\Typora\笔记图片(勿删)\批注 2020-03-18 204411.jpg)

​							1.私有的构造方法   不能让别人去多次创建对象因为我们单例对象的初衷就是只创建一个对象，减少创建对象占用的空间

​							2.私有的静态的当前类对象作为属性	因为我们有很多的操作都是基于它进行操作的不能被别人进行修改，所以我们得将他设为私有的

​							3.公有的静态的方法返回当前类对象	因为我们的初衷时只创建一个对象，而我们的方法只有对象能访问到，所以我们就将它设为静态的我们只加载类就能拿到它

​							这样我们每次用它只是加载类就可以了不会进行多次创建对象而导致空间不足



主方法:

```java
public class Test{
    public static void main(String[] args){
        Singleton singleton = Singleton.getSingle();
    }
}
```

​							饿汉式(立即加载)

​									没有使用到的我也一次性丢给服务器去加载，这样会导致服务器承载压力过大

```java
public class Singleton{
    private static Singleton single = new Singleton();
    
    public static Singleton getSingle(){
        return single;
    }
}
```

​							懒汉式(用到再加载 且只加载一次)

​									如果我这个单例没有用到我就不丢给服务器进行加载，当我用到的时候我再去加载，而我第二次用到的时候因为我第一次已经有了所以我就不用再创建了，直接拿来用就可以了

```java
public class Singleton{
    private static Singleton single;
    
    public static Singleton getSingle(){
        if(single == null){
            single = new Singleton();
        }
        return single;
    }
}
```

​							生命周期托管(单例对象别人帮我们处理)

​									对象加载过程交给别人

## 10.abstract抽象的

(很不具体 没有具体的执行 只是个概念)

**1.可以修饰什么？**

​			修饰方法

​				用abstract修饰符修饰的方法 只有方法的结构 没有方法执行体叫做抽象方法

​				注意native修饰的方法虽然也没有方法体，但是不是抽象方法 只是执行过程是调用其他语言写的我们看不到

​			修饰类

​				用abstract修饰符修饰的类 叫做抽象类



**2.修饰后有什么特点？**

​			抽象类中必须有抽象方法嘛？

​					不是必修含有抽象方法

​			抽象方法必须放在抽象类中么？

​					目前来看必须放在抽象类中(或接口中) 普通类是不能有抽象方法的



**3.研究一下什么教抽象类 抽象类有什么特点？**

​			和其他类没有任何区别，只不过抽象类可以含有抽象方法，普通类不行

​			抽象类含有构造方法但是我们不能通过构造方法直接创建对象

​			抽象类只能通过子类单继承来做事

​			为什么不让我们调用构造方法创建对象？可以是他为什么还有呢？

​					因为你抽象方法新建出来是不能用的所以从逻辑上就否定了；我们的构造方法是用于子类在执行构造方法是super()来创建我们的对象的



​		类和类的关系

​			抽象类 单继承 抽象类 可以

​			抽象类 单继承 具体类 可以(用法通常不出现因为不符合逻辑)

​			具体类 单继承 抽象类 不可以 因为我们的抽象类有抽象方法所以我们得实例化这个方法不然没有任何意义，除非我们自身也是抽象类就可以不用

​			

**4.小问题**

​			抽象类中能不能没有抽象方法全是具体成员 可以

​			抽象类中能不能没有具体成员 全部都是抽象方法 可以--->抽象类抽象到极致 质的变化 ---> 接口

​			接口可以理解为是抽象类抽象到极致--->还是一个类的结构 不能用class修饰 改用interface修饰



#### 5.什么是接口

​		接口也是一个类的结构 只不过用 interface修饰 替换原有的class

​		public interface A{}

​		接口里边的东西全是抽象的

​		1.有什么成员

​					属性		不能含有一般属性 只能含有公有的静态的常量 public static final(接口自带的)(帮我们写好的所以可以省略)

​					方法		不能含有一般方法 只能含有公有的抽象的方法(1.8 defualt修饰具体方法)

​					块			不能含有一般程序块 也不能含有static块(块本身就是具体的 接口中不让有具体的东西)

​					构造方法  不能含有构造方法

​		2.如何使用	创建对象

​					不能创建对象

​					只能通过子类多实现(implement)来做事

​					public class A implement B, C, D{

​					

​					}

​		3.与别的类结构关系

​					抽象类 ---直接多实现---接口  可以

​					具体类 ---直接多实现---接口  不可以(必须将接口中的抽象方法具体化 或者自己变成抽象类)

​					接口不能继承别的类 最抽象

​					*接口---多继承---接口  可以实现多实现

![批注 2020-03-25 125428](F:\Typora\笔记图片(勿删)\批注 2020-03-25 125428.jpg)

![批注 2020-03-25 125406](F:\Typora\笔记图片(勿删)\批注 2020-03-25 125406.jpg)

