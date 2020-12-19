# lodash

> js的一个封装函数库
> 使用前需要导入lodash.js包

## lodash对象:
简写为```_```,调用方法```_.方法名()```

### lodash的注意点：

1. lodash中有很多方法有两种拓展方法，例如：difference(), differenceBy(), differenceWith(),他们的拓展方法By和With方法的拓展内容都是一致的

### lodash Array方法:

1. chunk():
   作用：将一个数组的内容参分成指定长度的数组，最终形成一个二维数组
   参数：(数组, 拆分数组长度)
   案例：
   ```js
   console.log(_.chunk(['a', 'b', 'c', 'd'], 2);//[['a', 'b'], ['c', 'd']];
   ```
2. compact():
   作用：过滤掉数组中的非真元素，非真元素：转化成Boolean为false的元素
   参数：(数组)
   案例：
   ```js
   console.log(_.compact([1, 2, null, undefined, 3]));//[1, 2, 3];
   ```
3. difference():
   作用：干掉所选数组中的某个指定元素
   参数：(数组, [想要干掉的元素值])
   案例：
   ```js
   console.log(_.difference([1, 3, 5 ,6 , 7], [1, 6]));//[3, 5, 7];
   ```
4. differenceBy():
   作用：比difference可多填一个参数用于遍历
   参数：(数组, [想要干掉的元素值], 想要用谁遍历这些数组)
   案例：
   ```js
   console.log(_.difference([1.1, 3.1, 5.2, 6.7, 7.9], [1.5, 6.4], Math.floor));//[3.1, 5.2, 7.9];
   执行过程:
   - 先用第三个参数将数组遍历执行一遍然后再执行difference的操作,他返回的结果并不会因为第三个参数而发生改变,第三个参数只是为了更好的比较而产生的比如说我们想要将第一个数组中的个位数为1，6的数给他干掉那么我们就添加Math.floor让在比较时只比较个位数的数字，找到与第二个参数数组相符的元素将他干掉，然后将剩余的元素数组以原来的方式返回,所以就的出了我们这个结果
   ```
5. differenceWith():
   作用：比difference可多填一个参数用于比较
   参数：(数组，[想要干掉的元素值]， 想要用谁来比较这两个数组的元素是否相等);
   案例：
   ```js
   console.log(_.differenceWith([{a:1,b:1}, {a:2,b:1}], [{a:1,b:1}], _.isEqual));//[{a:2,b:1}];
   执行过程：
   - 用第三个参数来对第一第二参数进行比较，如果比较相同，则将第一个参数内的相同元素干掉，然后返回剩余元素组成的第一个参数的数组
   ```
6. drop():
   作用：将数组中的前指定长度的元素删掉
   参数：(数组，前面几个元素);
   案例：
   ```js
   console.log(_.drop([1, 3, 5, 2, 6], 3));//[2, 6];
   ```
7. dropRight():
   作用：将数组中的后指定长度的元素删掉
   参数：(数组，后几个元素);
   案例
   ```js
   console.log(_.dropRight([1, 3, 5, 2, 6], 3));//[1, 3];
   ```
8. take():
   作用：从左边开始,提取数组中我们指定长度的n位
   参数：(数组，提取元素的指定长度)
   案例：
   ```js
   console.log(_.take([1, 3, 5, 7], 2));//[1, 3];
   ```
9. takeRight():
    和dropRight一样
10. flatten():
    作用：去掉数组嵌套
    参数：(数组)
    案例：
    ```js
    console.log(_.flatten([[1,[2,[3,[4]]]]]));//[1,2,[3,[4]]];
    ```
11. flattenDeep():
    作用：去掉数组嵌套
    参数：(数组)
    案例：
    ```js
    console.log(_.flattenDeep([[1,[2,[3,[4]]]]]));//[1,2,3,4];
    ```
12. flattenDepth():
    作用：去掉指定层数的数组嵌套
    参数：(数组, 指定去层数)
    案例：
    ```js
    console.log(_.flattenDepth([[1,[2,[3,[4]]]]], 2));//[1,2,[3,[4]]];
    ```
13. intersection():
    作用：取到多个数组中的交集以数组形式返回
    参数：(数组, 数组, [数组,...]);
    案例：
    ```js
    console.log(_.intersection([1,2,3],[2,4,8],[2,9,7]));//[2]
    ```
    > 他还有By,With方法和我们其他拥有By,With的函数一致
14. union():
    作用：取到多个数组的并集,重复的会被去掉
    参数：(数组,数组,[数组,...])
    案例：
    ```js
    console.log(_.union([1,2],[2,3]));//[1,2,3]
    ```
    它也拥有By和With的形式
15. xor():
    作用：删除多个数组中的交集以数组形式返回
    参数：(数组，数组，[数组,...])
    案例：
    ```js
    console.log(_.xor([1,2,3],[2,3,4,5]));//[1,4,5];
    ```
16. nth():
    作用：通过下标访问数组内容，特点它的下标可以传负数(没有负0)，而正常js不行
    参数：(数组，下标)
    案例：
    ```js
    var arr = [1,2,3,4];
    _.(arr, 1);//2
    _.(arr, -1)//4
    ```
17. pull():
    作用：删除数组中的元素
    参数：(数组，想要删除的数据)、
    案例：
    ```js
    _.pull([1,2,3,1,2,3], 2, 3);//[1,1];
    ```
    pullAll():
    参数：(数组，想要删除的数据数组)
          ([1,2,3,1,2,3], [2,3]);
18. 与pull相似并且比pull方便的remove():
    作用：删除数组中的元素
    参数：(数组，function (item, index, array){
       return true;//true删除 flase不删除
    })
19. without():
    作用：与remove一样，不过它不会更改原数组，而remove会更改原数组
20. uniq():
    作用：数组去重
    参数：(数组)
    案例：
    ```js
    _.uniq([1,2,2,1]);//[1,2];
    ```
21. zip()；
    作用：将索引值相同的数组元素放在一个数组内最终组成一个二维数组
    参数:([数组],[数组][,[数组]]);
    案例：
    ```js
    _.zip(['小红', '小兰', '小刚'], ['女', '女', '男'], [18, 15, 16]);//[['小红', '女', 18], ['小兰', '女', 15], ['小刚', '男', 16]];
    ```
22. zipObject():
    作用：将两个数组组合起来形成数组，所对应key和value
    参数：([数组],[数组]);
    案例：
    ```js
    _.zipObject(['小红', '小兰', '小刚'], ['女', '女', '男']);//{小红:'女',小兰:'女',小刚:'男'}
    ```
23. unzip();
    作用：将zip转化后的类型转化成zip转化前的类型
    参数：(二维数组)

### Collection(集合)

1. _.countBy():
   作用；统计这个集合内的元素的你想要统计的东西次数
   参数：(数组,"你想统计的东西")
   案例：
   ```js
   console.log(_.countBy(['one', 'tow', 'three'], 'length'));// {3:2, 5:1}
   意思为：
   元素长度为3的有2个
   元素长度为5的有1个
   ```
2. _.groupBy():
   作用：统计这个集合内满足同一规则的元素组成的集合
   参数：([数组], '你想统计的规则')
   案例：
   ```js
   console.log(_.groupBy(['one', 'tow', 'three'], 'length'));// {3:['one', 'tow'], 5:['three']};
   ```
3. _.invokeMap():
   作用：给一个数组将这个数组设置成我们想要的样子
   参数：([数组], '你想设置的规则')
   案例：
   ```js
   //第一种案例
   console.log(_.invokeMap([[5,1,7],[4,1,6]], 'sort'));//[[1,5,7],[1,4,6]]
   //第二种案例
   console.log(_.invokeMap([123, 456], String.prototype.split, ''));//[['1','2','3'], ['4','5','6']]
   释译：
   将第三个参数传入你第二个规则中，然后通过第二个参数的规则对第一个参数的数组进行操作
   ```
4. _.keyBy():
   作用：将一个数组变成对象，将我们的第二个参数作为这个数组内元素的属性
   参数：([数组], '规则');
   案例：
   ```js
   var array = [
       {'dir' : 'left', 'code' : 97},
       {'dir' : 'right', 'code' : 100}
   ];
   //第一种
   console.log(_.keyBy([array], function (o){
       return String.fromCharCode(o.code);//将我们返回的东西作为数组元素的属性
   }))//{a:{'dir' : 'left', 'code' : 97},d:{'dir' : 'right', 'code' : 100}}
   //第二种
   console.log(_.keyBy([array], 'dir'));//{left:{'dir' : 'left', 'code' : 97},right:{'dir' : 'right', 'code' : 100}}
   ```
5. orderBy():
   作用：将一个数组内的元素按照第二个参数来进行排序，并且可选择升序还是降序
   参数：([数组], '按那个数据排', 'asc(升序)/desc(降序)');
   案例：
   ```js
   var user = [
       {'user' : 'fred', 'age' : 48},
       {'user' : 'barney', 'age' : 34},
       {'user' : 'fred', 'age' : 40},
       {'user' : 'barney', 'age' : 36},
   ]
   console.log(
       //升序
       _.orderBy(user, 'age', 'asc'),//通过元素中的属性age的值进行升序排序
       _.orderBy(user, 'age', 'desc');//降序
   )
   ```
6. _.partition():
   作用：将一个数组按照我们的规则拆分为一个二维数组
   参数：([数组], 规则);
   案例:
   ```js
   var users = [
       {'user' : 'fred', 'age' : 48, 'active' : false},
       {'user' : 'barney', 'age' : 34, 'active' : true},
       {'user' : 'pebbles', 'age' : 40, 'active' : false}
   ]
   console.log(
       _.partition(users, function (o){
           return o.active;//将这个作为规则，满足这个规则的放在同一个数组里，不满足的放另一个数组里
       })//[[{'user' : 'pebbles', 'age' : 40, 'active' : false}, {'user' : 'fred', 'age' : 48, 'active' : false}],[{'user' : 'barney', 'age' : 34, 'active' : true}]]
       _.partition(users, {age : 1, active : flase});//满足对象拥有这两个属性并且值一致的放在一起不满足则分开来
       //[[{'user' : 'pebbles', 'age' : 40, 'active' : false}],[{'user' : 'fred', 'age' : 48, 'active' : false},{'user' : 'barney', 'age' : 34, 'active' : true}]]
   )
   ```
7. _.reject():
   作用：将该数组中满足规则的元素过滤出去留下为匹配结果为false的
   参数：([数组], 规则)
   案例：
   ```js
   var users = [
       {active : false},
       {active : false, age : 18},
       {active : true, age : 20}
   ];
   console.log(
       _.reject(users, 'age')//[{active:false}];
   )
   ```
8. _.sample():
   作用：将我们传入的数组中的元素随机返回出来一个
   参数：([数组])
   案例：
   ```js
   console.log(_.sample([',','a','b']));
   //b
   //a
   //a
   //,
   ```
10. _.sampleSize():
    作用：将我们传入的数组中的元素随机返回出来一个，返回的个数我们可以规定
    参数：([数组], 返回多少个数)
    案例：
    ```js
    console.log(_.sampleSize(['a', 'v', 'e', ';'], 3));//['v', 'a', 'p']
    ```
11. _.shuffle():
    作用：将我们传入的数组进行乱序
    参数：([数组]);
    案例：
    ```js
    console.log(_.shuffle(['a', 'b', 'c']));//['c', 'a', 'b']
    ```
12. _.size():
    作用：统计这个对象中拥有多少个属性
    参数：({对象})
    案例：
    ```js
    console.log(_.size({a: 1, b:2}))//2
    ```

### Function:

1. _.defer():
   作用：延迟执行这个函数(当所有JS代码执行完后执行)
   参数:(function (形参){}, 实参)
   案例：
   ```js
   _.defer(function (a){
       console.log(a);
   }, '这是延迟了之后的输出')
   console.log('这是没有延迟执行的输出')
   //这是没有延迟执行的输出
   //这是延迟了之后的输出
   ```
2. flip():
   作用：将这个函数的内的形参值倒过来
   参数：(函数)
   案例：
   ```js
   var fn = _.flip(function a(){
       console.log(arguments);
   })
   fn(1,2,3);//[3,2,1]
   ```
4. once():
   作用：该函数只能执行一次，执行完一次这个函数就没了
   参数：(函数)
   案例：
   ```js
   function fn1(){
       console.log('fn1');
   }
   var newFn1 = _.once(fn1);
   newFn1();
   newFn1();
   > fn1
   ```

### Lang
1. castArray():
   作用：将参数强制转化成数组
   参数：(anything)
   案例：
   ```js
   console.log(castArray({a:1,b:2}));//[{a:1,b:2}]
   ```
2. cloneDeep():
   作用：深度克隆
   参数：(Object)
   案例：
   ```js
   var obj = {
       a:{b:1}
   }
   var obj1 = cloneDeep(obj);
   obj1.a.b = 2;
   ```
3. conformsTo():
   作用：判断这个元素是否满足我们所规定的规则，正确返回true,错误返回false
   参数：({},规则)
   案例：
   ```js
   var arr = [
       {a:1, b:2},
       {a:2, b:2}
   ]
   console.log(_.conformsTo(arr, {a:function(a){
       return a > 1;
   }}))
   //false
   console.log(_.conformsTo(arr, {a:function(a){
       return a > 0;
   }}))
   //true
   **他只会找到第一个匹配的结果**
   ```
4. toArray()：
   作用：将参数转化为数组
   参数：(anything)
   案例：
   ```js
   console.log(_.toArray({a:1,b:2}));//[1,2]
   console.log(_.toArray('abc'));//['a','b','c']
   ```
   注意：他并不会像castArray一样那么暴力，他获取的只是值

### Object
1. _.at():
   作用：以特殊的形式获取第一个参数中的数据，然后以数组的形式返回
   
   参数：(你要处理的对象，[返回的数组])
   
   案例：
   
   ```js
   var a = {a : [{ b : {c : 3}}, 4]};
           console.log(_.at(a, ['a[0].b.c', 'a[1]']));
           /*
           Array(2)
           0: 3
           1: 4
           length: 2
           __proto__: Array(0)
           */
   ```
   
2. _.defaults():

   作用：对象混杂(assign是后面的覆盖前面的，defaults是前面的覆盖后面的)

   参数：(多个对象)

   案例：

   ```js
   console.log(
               _.defaults({a:1},{b:2},{a:3}), //{a: 1, b: 2} 
               _.assign({a:1},{b:2},{a:3}) //{a: 3, b: 2}
           );
   ```

3. findKey():

   作用：在对象中查找值为第二个参数的key

   参数：(对象,需要判断对象的值)
   案例：

   ```js
   var obj = {
       a : {name:1,age:18},
       b : {name:2,age:11},
       c : {name:3,age:12}
   }
   console.log(_.findKey(obj,{name:2,age:11}));//b
   ```

   类似：findLastKey()按findKey的倒着来的顺序遍历

4. _.setWith():

   作用：设置这个对象的内容

   参数：(对象, 如何设置('key','value'),返回值类型)

   案例：

   ```js
   console.log(_.setWith({}, '[0][1]','a', Object));
           /*
           {0: {…}}
           {
               0: {
                   1: "a"
                   __proto__: Object
                   }
               __proto__: Object
           }
           */
   console.log(_.setWith({}, '[0][1]','a', Array));
   		/*
   		{0: […]}
   		{
               0: [
                   0:undefined,
                   1:"a"
                   ]
               __proto__: Object
           }
   		*/
   ```

5. invert():

   作用：将该对象的key和value调换位置(如果有同名属性则依据js的规则后面的覆盖前面的)

   参数：(对象)

   案例：

   ```js
   var obj = {a:1,b:2,c:1};
   console.log(_.invert(obj));//{1:c,2:b}
   ```

   