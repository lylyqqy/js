# js
### js编写位置
- 可以将js代码编写到外部js文件中，然后通过script标签引入，写到外部文件中可以在不同页面中同时引用，也可以利用浏览器的缓存机制，推荐方式。
- script标签一旦用于引入外部文件了，就不能再编写代码了，如果需要则可以再创建一个新的script标签。
### 注释
- 单行注释 //
- 多行注释 /**/
### 基本语法
- 严格区分大小写
- 每一条语句以分号;结尾
- js中忽略多个空格和换行，所以可以对代码格式化，便于阅读
### 字面量和变量
字面量=常量
-变量
声明变量：用var关键字声明
-赋值
### 标识符
- 可以包含字母、数字、_、$
- 不能以数字开头
- 不能是es中的关键字和保留字
- 一般采用驼峰命名法，首字母小写，每个单词开头字母大写，其余字母小写
- js底层保存标识符时实际上采用的时unicode编码，因此也能识别中文，但极不推荐使用中文作为标识符
## 数据类型
六种数据类型：String、Number、Boolean、Null、Undefined、Object  
除Object都是基本数据类型，Object为引用数据类型
### 字符串
-在js中字符串需要使用引号引起来，单引号双引号都可
-字符串使用\n转义字符表示换行，在字符串中不能使用enter换行
### Number
-包括整数和浮点数
-使用typeof可以检查数据类型
-JS可以表示的数字的最大值Number.MAX_VALUE，如果使用Number表示的数字超过了最大值，则会返回Infinity（正无穷），使用typeof返回number，Number.MIN_VALUE表示最小的整数
-NaN：not a number,使用typeof返回number
-js中整数基本保证精确，浮点数（小数）可能得到一个不精确的结果
### Null
null这个值专门用来表示一个为空的对象
```
    var a=null;
    console.log(typeof a) // 返回Object !important
```
### Undefined
undefined,声明一个变量未赋值时，就是undefined
## 类型转换
主要指的是，将其他数据类型转换为String、Number、Boolean
### 转换为String
1. toString(); 
   - 该方法不会影响原变量，会将转换的结果返回
   - null、undefined没有该方法
2. String();
   - 该函数会将转换的数据作为参数传递给函数
   - null、undefined有该函数
   - 使用String()函数做强制类型转换时，对于Number和Boolean实际上就是调用的toString()方法，但是对于null和undefined,它会直接转换为“null”、“undefined”
3. +“”;
   - 本质上调用了String()函数
### 转换为Number
1. Number();
   - 字符串-->数字
        i. 如果是纯数字的字符串，直接转换为数字
        ii. 如果字符串中有非数字的内容，则转换为NaN
        iii. 如果字符串是空串，转换为0
   - 布尔-->数字
        i.true-->1
        ii.false-->0
   - Null-->数字
        0
   - Undefined-->数字 
        NaN
2. **这种方式专门用来对付字符串的**
- parseInt();把一个字符串转换为一个整数
    从左向右读到第一个非数字/.为止
- parseFloat();把一个字符串转换为一个浮点数
   从左向右读到第一个非数字/第二个.为止
3. -0，*1，/1
   任何值- * /运算时都会自动转换为Number,原理和Number()函数原理一致
4. +; 
   - 一元运算符
### 转换为Boolean
1. Boolean();
   - 数字-->布尔
    除了0和NaN,其余都是true
   - 字符串-->布尔
    除了空串，其余都是true
   - null、undefined都是false
   - 对象也会转换为true
2. !! 
   - 原理与Boolean()一样
## 其他进制的数字
在js中，如果需要表示16进制的数字，则需要以0x开头;8进制数字，以0开头。（2进制数字，以0b开头，但是不是所有的浏览器都支持。）
```
    a=0x10;
    console.log(a) //16
```
## 逻辑运算符

!:先转换为布尔类型，再取反
&&：对符号两侧的值进行与运算并返回结果
 - 都为布尔值时，两个值都为true时才返回true
||:
 - 都为布尔值时，一个值都为true时就返回true
**对于非布尔值进行与或运算时，会先将其转换为布尔值，再运算，并且返回原值**
&&：第一个值为true,返回第二个值，第一个值为false，返回第一个值
||:第一个值为true,返回第一个，第一个为false，返回第二个值
## 相等运算符
1. ==
- 如果比较的两个值类型不同，会转换为相同类型比较，大部分情况转换为数字比较 (但null==0 false)
==undefined衍生自null 因此undefined等于null==
- 可以通过isNaN()函数来判断一个值是否为NaN
2. !=
- 也会进行自动类型转换然后比较
3. ===
- 不进行类型转换 null===undefined false
4. !==
- 不进行类型转换
## 条件运算符（三元运算符）
 条件表达式?语句1:语句2;
## break continue
-break关键字可以用来推出switch或循环语句，不能在if语句中使用continue和break
-break只对离它最近的循环起作用
可以为循环语句创建一个Label,来结束当前循环
label:循环语句
使用break语句时，可以在break后跟着一个label，这样break将会结束指定的循环，而不是最近的
break结束当前循环，continue跳过当次循环
## 对象
### 对象的分类：
1. 内建对象
   - 由es标准中定义的对象，在任何的es的实现中都可以使用
   -如Math String Number Boolean...
2. 宿主对象
   - 由js的运行环境提供的对象，目前来讲主要是指由浏览器提供的对象
   -如BOM、DOM
3. 自定义对象
### 自定义对象
对象的属性名不强制要求遵守标识符的规范。
如果要使用特殊的属性名，不能采用.的凡是来操作，语法:对象["属性名"]=属性值
in 运算符
 -通过该运算符可以检查一个对象中是否含有指定的属性
 ```
    console.log("test" in obj); //true or false
 ```
#### 自定义对象方式：
1.new
   ```
    var obj=new Object();
   ```
2. 对象字面量
  ```
   var obj={};
   ```
   对象字面量的属性名可以加引号也可以不加，建议不加，如果想使用特殊的名字，必须加引号
   名值对之间用,隔开
   ```
   var obj2={
       name:"孙悟空",
       age:10,
       gender:"男"
   }
   ```
3. 使用工厂方法创建对象
   ```
   function createPersn(name,age,gender){
       //创建一个新的对象
       var obj=new Object();
        obj.name=name;
        obj.age=age;
        obj.gender=gender;
        obj.sayname=function(){
            console.log(this.name);
        }

       //将新对象返回
       return obj;
   }
   
   var obj2=createPerson("孙悟空",10,"男");
   var obj3=createPerson("白骨精",10,"女");
   obj3.sayname(); //白骨精
   ```
   使用工厂方法创建的对象，使用的构造函数都是Object,所以创建的对象都是Object这个函数，就导致我们无法区分出多种不同类型的对象
4. ###### 使用构造函数创建对象
   构造函数：本质上就是一个普通的函数，创建方式和普通函数没有区别，不同的是构造函数习惯上首字母大写
   构造函数和普通函数的区别：
   普通函数直接调用，构造函数使用new关键字调用
    构造函数的执行流程：
    1. 立即创建一个新的对象
    2. ==将新建的对象设置为函数中的this，在构造函数中可以使用this来引用新建的对象==
    3. 逐行执行函数中的代码
    4. 将新建的对象作为返回值返回
   ```
   function Person(name,age,gender){
       this.name=name;
       this.age=age;
       this.gender=gender;
       this.sayName=function(){
           console.log(this.name);
       }
   }
   var per= new Person("孙悟空",10,"男"); //this就是新建的对象per
   console.log(per); //object
   
   ```
   使用同一个构造函数创建的对象，我们称为一类对象，也将一个构造函数称为一个类，我们将通过一个构造函数创建的对象，称为该类的实例
   ==使用instanceof可以检查一个对象是否时一个类的实例==
   ```
    console.log(per instanceof Person);  //true
    console.log(per instanceof Object);  //true 所有的对象都是Object的后代，所以任何对象和Object做instanceof检查时都会返回true
   ```
   ###### 构造函数修改
   创建一个Person构造函数
   -在Person构造函数中，为每一个对象都添加了一个sayName方法，目前我们的方法是在构造函数内部创建的，也就是构造函数执行一次就会创建一个新的sayName方法，这是完全没有必要的，完全可以使所以的对象共享同一个方法
     ```
   function Person(name,age,gender){
       this.name=name;
       this.age=age;
       this.gender=gender;
       this.sayName=fun;
   }
   function fun(){
           console.log(this.name);
       }
   var per= new Person("孙悟空",10,"男"); //this就是新建的对象per
   var per2= new Person("白骨精",10,"女");
   console.log(per.sayName==per2.sayName); //true
   console.log(per); //object
   
   ```
   **但**将函数定义在全局作用域，污染了全局作用域的命名空间
   ###### 解决方案：向原型中添加方法
    ```
   function Person(name,age,gender){
       this.name=name;
       this.age=age;
       this.gender=gender;
      
   }
   Person.prototype.sayname=function (){
           console.log(this.name);
       }
   var per= new Person("孙悟空",10,"男"); //this就是新建的对象per
   var per2= new Person("白骨精",10,"女");
   console.log(per.sayName==per2.sayName); //true
   
   ```
   以后我们创建构造函数时，可以将这些对象共有的属性和方法，同意添加到构造函数的原型对象中，这样不会影响全局作用域
   
### 函数
函数也是一个对象
- 创建一个函数对象
```
var func=new Function();
```
使用typeof 返回function
可以将要封装的代码以字符串的形式传递给构造函数
```
var func=new Function("console.log("等你调用我哦")");
func(); //封装到函数的代码不会立即执行，调用时才执行
```
- 使用函数声明来创建一个函数
  语法： function 函数名([参数1，参数2，...]){
        语句...
  }
- 使用函数表达式来创建一个函数
  var 函数名=function([形参1，形参2,...]]){
      语句...
  };
###### 函数的参数
```
    function sum(a,b){
        console.log(a+b); //声明形参就相当于在函数内部声明了对应的变量
    }

```
###### return
return后面的值会作为函数的执行结果返回，如果return语句不跟任何值/不写return，则返回undefined
###### 实参可以是任意的数据类型
当函数参数过多时，可以将实参封装到一个对象中，通过对象传值
###### 返回值可以是任意的数据类型
可以是一个对象，也可以是一个函数
#### 立即执行函数
函数定义完立即被调用，只会执行一次
```
(function(a,b){
    console.log(a);
    console.log(b);
})(123,456);

```
#### 方法
对象的属性值可以是任何数据类型，也可以是个函数
obj.sayName=function(){
  console.log(123);
};
如果一个函数作为一个对象的属性保存，那么我们称这个函数为这个对象的方法
##### 枚举对象中的属性
- 使用for...in语句
  对象中有几个属性，循环体就会执行几次
  每次执行时，会将对象中的一个属性的名字赋值给变量
  语法：
    for(var 变量名 in 对象){

    }
```
    for(var n in obj){

    }


```
### 全局作用域
全局作用域的变量是全局变量，在页面的任意部分都可以访问到
- 变量的声明提前
    -使用var关键字声明的变量，会在所有的代码执行之前被声明
    -如果不使用var 关键字声明，则不会提前
- 函数声明提前
    -使用函数声明形式创建的函数（function 函数名(){}）,会在所有代码执行之前就被创建
    -使用函数表达式创建的函数不会被声明提前，不能在声明前调用
### 函数作用域
1. 调用函数时创建函数作用域，函数执行完毕后，函数作用域销毁
2. 每调用一次函数就会创建一个新的函数作用域，它们之间时相互独立的
3. 在函数作用域中可以访问到全局作用域的变量，在全局作用域中无法访问到函数作用域的变量
4. 当在函数作用域中操作一个变量时，它会先在自身作用域中寻找，如果没有再向上一级作用域寻找，直到找到全局作用域，如果全局作用域也没找到就报错
5. 在函数中要访问全局变量可以使用window对象
6. 在函数作用域中也有声明提前的特性（变量、函数声明提前）
7. 在函数中，不适用var声明的变量都会变为全局变量
### 函数的方法
- call(),apply()
  函数对象的方法，通过函数对象调用
```
    function fun(){
        alert("xixi);
    }
    fun.call(); //xixi
    fun.apply(); //xixi
```
  当对函数对象调用call()和apply()时都会调用函数执行
  在调用call()和apply()时可以指定第一个参数,此时这个对象将会称为函数执行时的this
```
var obj={
    name:"孙悟空",
    sayname:function(){
        alert(this.name);
    }

};
var obj2={
    name:"白骨精",
    

};
 function fun(){
        alert(this);
    }
    fun.call(obj); //Object object
    fun.apply(obj); //Object object
    obj.sayname.apply(obj2); //白骨精
```
- call(),apply()区别
  ==call()方法可以将实参在对象之后依次传递==
```
  function fun(a,b){
        alert("xixi",(a+b));
    }
  var obj2={
    name:"白骨精",
};
    fun.call(obj2,2,3); //xixi,5

```
  ==apply()方法需要将实参封装到一个数组中统一传递==
```
   function fun(a,b){
        alert("xixi",(a+b));
    }
  var obj2={
    name:"白骨精",
};
    fun.call(obj2,[2,3]); //xixi,5
```
## 61.this
解析器在调用函数时每次都会向函数内部传递一个隐含的参数。  

这个隐含的参数就是this,this指向的是一个对象，这个对象我们称为函数执行的上下文对象。
- 根据函数的调用方式不同，this会指向不同的对象
    1. 以函数的形式调用时，this永远都是window
    2. 以方法的形式调用时，this就是调用方法的那个对象
    3. 以构造函数的形式调用时，this就是新创建的那个对象
    4. 使用call和apply调用时，this是指定的那个对象
### arguments
在调用函数时，浏览器每次都会传递两个隐含的参数
1.函数的上下文对象this
2.封装实参的对象arguments
 - arguments时一个类数组对象,可以通过索引来操作数组，获取长度
 - 调用函数时，我们所传递的实参都会在arguments中保存
    ```
        function fun(){
            console.log(arguments instanceof Array); //false
            console.log(Array.isArray(arguments)); //false
            console.log(arguments.callee==fun); //true
        }
    ```
 - arguments有一个callee属性，指向当前正在执行的函数的对象
##### 原型prototype
我们所创建每一个函数，解析器都会向函数中添加一个属性prototype
这个属性对应着一个对象，这个对象就是我们所谓的原型对象
如果函数作为普通函数调用prototype没有任何作用
当函数以构造函数的形式调用时，它所创建的对象中都会有一个隐含的属性（```__proto__```），指向该构造函数的原型对象
###### in运算符
  使用in检查对象中是否含有某个属性时，如果对象中没有但是原型中有，也会返回true，可以是那样对象的hasOwnProperty()来检查对象自身中是否含有该属性
#### tostring()
  当我们直接在页面打印一个对象时，实际上是输出对象的toString()方法的返回值
```
    var per=new Person("孙悟空",18,"男");
    console.log(per);// 等于console.log(per.toString())
```
### 垃圾回收（GC）
在js中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁，我们需要做的知识将不再使用的对象设置为null即可
```
var obj=new Object();
obj=null;

```
## 数组
数组中的元素可以是任意的数据类型
#### 创建数组
- new
```
    var arr= new Array();
    使用构造函数创建数组时，也可以同时添加元素，将要添加的元素作为构造函数的参数传递
    var arr1=new Array(10,20,30);
    
```
 数组也是一个对象 
- 字面量创建
```
    var arr=[];
    console.log(typeof arr)  //object
    使用字面量创建数组时，可以添加元素
    var arr1=[1,2,3,4];
```
==区别==
```
    var arr2=new Array(10); //创建了长度为10个的数组
    var arr2=[10]; //创建了长度为1值为10的数组

```
#### 数组的四个方法
- push()
  向数组的末尾添加一个或多个元素，并返回新的长度
```
    var arr=[10,20,30];
    var result=arr.push(40,50,60);
    console.log(result); //6 
```
- pop()
  删除数组末尾最后一个元素并返回数组被删除的元素
```
    var arr=[10,20,30];
    var result=arr.pop();
    console.log(result); //30
```
- unshift()
  向数组开头添加一个或多个元素，并返回新的数组长度
  向前面插入元素以后，其他的元素索引会依次调整
```
    var arr=[10,20,30];
    var result=arr.unshift(40,50,60);
    console.log(result); //6 
    console.log(arr);//40,50,60,10,20,30
```
- shift()
  删除数组开头的第一个元素并返回被删除的元素
```
     var arr=[10,20,30];
    var result=arr.shift();
    console.log(result); //10
```
#### forEach
-forEach()方法需要一个函数作为参数
```
    var arr=[10,20,30,40,50,60];
    arr.forEach(function(){
        console.log("hey"); //输出6个hey
    });

```
像这种函数，由我们创建但是不由我们调用的，我们称为回调函数  

数组中有几个元素函数就会执行几次，每次执行时，浏览器会将遍历到的元素以实参的形式传递进来，我们可以定义形参来读取这些内容  
浏览器会在回调函数中传递三个参数：
- 第一个参数，当前正在遍历的元素
- 第二个参数，当前正在遍历的元素的索引
- 第三个参数，正在遍历的数组
```
    var arr=[10,20,30,40,50,60];
    arr.forEach(function(value,index,arr){

    });
``` 
#### slice和splice
- slice()
  从已有的数组中返回指定的元素,返回截取到的元素，不会影响原数组
  arrayObject.slice(start,end); 
  第二个参数可不写，截取到最后
```
 var arr=[10,20,30,40,50,60];
 var result=arr.slice(0,2);  //[0,2)
 console.log(result);   //10,20
``` 
  索引可以传递一个负值,-1表示最后一个
- splice()
  删除元素，并向数组添加新元素
  会影响原数组，并将被删除的元素怒作为返回值返回
  arrayObject.splice(start,number,addarray);  
  1. 第二个参数：删除数量
  2. 第三个参数及以后：可以传递一些新的元素，这些元素将会自动插入到开始位置索引前面
#### 数组的剩余方法
- concat()
  可以连接两个或多个数组，并将新的数组返回，不会对原数组产生影响
- join()
  可以将数组转换为一个字符串，将转换后的字符串返回，不会对原数组产生影响
  在join()中可以指定一个字符串作为参数，这个字符串将会称为数组中元素的连接符，如果不知道链接发，则使用默认,作为连接符
- reverse()
  反转数组，会修改原数组
- sort()
  排序数组，会修改原数组，默认按unicode编码排序
  所以对于纯数字的数组，可能得到错误的排序规则。
  **我们可以在sort()添加一个回调函数，来指定排序规则**
  浏览器会根据回调函数的返回值来决定元素的顺序
   1.>0 交换位置
   2.<=0 不交换位置
  ```
   arr=[10,30,20,41,34,24,42,65];
   arr.sort(function(a,b){
       return b-a; //降序排列

   });
  
  ```
## Date对象
函数
-在js中使用Date对象来表示一个时间
- 创建一个Date对象，如果直接使用构造函数船舰一个Date对象，则会封装为当前代码执行的时间
 ```
    var d=new Date();
    console.log(d);
 ```
- 创建一个指定的时间对象，需要在构造函数中传递一个宝石时间的字符串作为参数
```
    var d2=new Date("10/03/2019 11:00:00");
    console.log(d2);

```
##### getDate()
获取当前日期对象是几日
```
    var d2=new Date("10/03/2019 11:00:00");
    console.log(d2);
    d2.getDate(); //3
```
##### getDay()
获取当前日期对象是周几，返回0-6的值
##### getMonth()
获取当前日期对象的月份，返回0-11的值
##### getTime()
获取当前日期对象的时间戳，时间戳，指的是从格林威治标准时间开始到当前时间所花费的毫秒数(1s=1000ms)
###### 获取当前的时间戳
```
var time=Date.now();
```
## Math
-Math和其他的对象不同，它不是一个构造函数，它是一个工具类不用创建对象，直接用即可
- Math.PI
- Math.abs();
- Math.ceil(); //向上取整
- Math.floor(); //向下取整
- Math.round(); //四舍五入取整
- Math.random(); //生成(0,1)之间的随机数
- Math.max(); //  Math.max(10,20,30,40,23) 40
- Math.min(); 
- Math.pow(x,y) //返回x的y次幂
- Math.sqrt() //开方
## 包装类
在js中为我们提供了3个包装类，通过这三个包装类可以将基本数据类型的数据转换为对象
- String()
- Number()
- Boolean()
```
    var num=new Number(3);
    conloe.log(typeof num); //Object
```
**在实际开发中，不常用基本数据类型的对象，变为堆后会导致不相等**
方法和属性只能添加给对象，不能添加给基本数据类型，当我们对一些基本数据类型的值去调用属性和方法时，浏览器会临时使用包装类将其转换为对象，然后再调用对象的属性和方法
### 字符串的方法
 在底层字符串是以字符数组的形式保存的
 - length //获取字符串长度
 - charAt() //返回字符串中指定位置的字符
```
    var str="hello hdsakhsd";
    var result=str.charAt(6);
    console.log(result); //h
```
 - charCodeAt() //返回字符串中指定位置的Unicode编码
 - fromCharCode()  //Unicode-->字符串
 - concat() //连接两个或多个字符串,对原子符串没影响
```
var str="hello";
var result=str.concat("world");

```
 - indexOf() //检索一个字符串中是否有指定内容
   如果字符串中含有该内容，则会返回其第一次出现的索引位置，没有则返回-1
   可以指定一个第二个参数，指定开始查找的位置
```
    var str="hello hdsakhsd";
    var result=str.indexOf("h");
    console.log(result); // 0
```
- lastIndexOf()  //与indexOf()一样，不过从后向前找，也可以指定一个第二个参数，指定开始查找的位置
- slice() 
  与数组的slice()一致
- substring() 
  与slice()类似，但是不同的是不能接受负数作为参数，如果传递了一个负数则默认为0，而且还可以自动调整参数的位置，如果第二个参数小于第一个，则自动交换
- substr()
  用来截取字符串
  参数：1.截取开始位置的索引
        2.截取的长度
- split()
  可以将一个字符串拆分为一个数组
  参数：需要一个字符串作为参数，将会根据该字符串去拆分数组
```
    var str="abc,bcd,efg,hij";
    var result=str.split("d");
    console.log(result.length) //2
    var result1=str.split("") //将每个字符都拆分为数组的元素
```
- toLowerCase() 
  转换为小写，不影响原来字符串
- toUpperCase()
  转换为大写，不影响原来字符串
  
## 正则表达式
    使用typeof检查正则对象，返回Object
- 创建正则表达式：
```
var reg=new RegExp("正则表达式","匹配模式");
var reg=new RegExp("a"，"i"); // "/a/"
var str="a";
var result=reg.test(str); //true
```

- 字面量创建
```
 var 变量=/正则表达式/匹配模式
 var reg=/a/i;
 reg=/a|b/; // |表或者
 console.log(reg.test("bcd")); //true
```
|表或者 []里的内容也是或的关系
[a-z] 任意小写字母
[A-Z]任意大写字母
[A-z]任意字母
[^]除了
[0-9]任意数字
[^0-9]除了数字
##### 正则表达式的方法：
- test();
  检查一个字符串是否符合正则表达式的规则
匹配模式：
    - i,忽略大小写
    - g,全局匹配模式 
- split();
  方法中可以传递一个正则表达式作为参数，这样方法就会根据正则表达式去拆分字符串
```
    var result=str.split(/[A-Z]/);
    //根据任意字母来将字符串拆分
```
- search()
  可以搜索字符串中是否含有指定内容，如果字符串中含有该内容，则会返回其第一次出现的索引位置，没有则返回-1
  可以接受一个正则表达式作为参数，然后根据正则表达式去检索字符串
```
    var str="hello abc hello aec afc";
    result=str.search(/a[bef]c/);
    //6
```
- match()
  根据正则表达式，从一个字符串中将符合条件的内容提取出来
  默认情况下match()只会找到第一个符合要求的内容，我们可以设置正则表达式为全局匹配模式，这样可以匹配到到所有的内容
  可以为一个正则表达式设置多个匹配模式，且顺序无所谓。
  match()会将匹配到的内容封装到一个数组中返回，即使只查询到一个结果
```
    var str="1a2b3c4d5e6f7";
    result=str.match(/A-z/g);
    //"a,b,c,d,e,f"
```
- replace()
  可以将字符串中指定内容替换为新的内容
  -参数：
  1.被替换的内容，可以接受一个正则表达式作为参数
  2.新的内容
  默认只会替换一个，可以设置正则表达式为全局匹配模式，这样可以替换到所有的内容
```
    var str="1a2b3c4d5e6f7";
    result=str.replace(/[a-z]/gi,"@_@");
    result=str.replace(/[a-z]/gi,""); //1234567
```
#### 正则表达式语法
- 量词
  {n} 正好出现n次
  {m,n} 出现[m,n]次
  {m,} 出现[m次以上
  +至少一次
  *0个或多个
  ?0个或一个
  ^表示开头
  $表示结尾
```
    var reg=/(ab){3}/;
    console.log(reg.test("ababab")); //true
```
- 检查一个字符串中是否含有.
  .表示任意字符
  在正则表达式中使用\作为转义字符
  \.来表示.
  \\表示\
  注意，使用构造函数时，由于它的参数时一个字符串，而\是字符串转义字符，如果要使用\则需要使用\\来表示
```
    var reg=/\./;
    console.log(reg.test(".")); //true
```
```
    var reg=/\\/;
    console.log(reg.test("b\\")); //true
```
 \W 任意字母、数字、_
 \w 除了字母、数字、_
 \d 任意的数字
 \D 除了数字
 \s 空格
 \S 除了空格
 \b 单词边界
 \B 除了单词边界
## DOM
文档对象模型：通过DOM对html文档进行操作
 - 节点：文档节点：整个Html文档 
 - 元素节点：html文档中的Html标签
 - 属性节点：元素的属性 
 - 文本节点：html标签中的文本内容

|  nodename | nodetype|  nodevalue|
| :-----| ----: | :----: |:----: |
|文档节点  |  #document  |    9   |     null  |
|元素节点  |   标签名     |   1   |     null   |
|属性节点  |  属性名      |  2    |      属性值 |
|文本节点  | #text       | 3     |       文本内容|

  
#### 页面的加载
 浏览器在加载一个页面时，时按照自上向下的顺序加载的，如果将script标签写在页面的上边，在代码执行时，页面还没加载，会报错
 onload时间会在整个页面加载完成之后才触发，为window绑定一个onload事件
childNodes属性会获取包含文本节点在内的所有节点
children属性会获取当前元素的所有子元素不包含文本节点
previousSibling前一个兄弟节点也可能获取到空白的文本
nextSlibing下一个
文本框的value只就是文本框中填写的位置
#### 110 其他样式相关的属性
- element.clientWudth:
  元素可见宽度，不带px，包括内容区和内边框，只读
- element.clientHeight:
  元素可见高度，不带 px，包括内容区和内边框，只读
- offsetWidth、offsetHeight
  获取元素的整个的宽度和高度，包括内容区、内边框、边框
- offsetParent
  用来获取当前元素的定位父元素
- offsetLeft、offsetRight
  当前元素相对于其定位元素的水平偏移量/垂直偏移量
- scrollWidth、scrollHeight
  获取元素整个滚动区域的宽度和高度
- scrollLeft、scrollTop
  获取水平/垂直滚动条滚动的距离
  当满足scrollHeight-scrollTop=clientHeight时垂直滚动条到底了
  当满足scrollWidth-scrollLeft=clientWidth时水平滚动条到底了
#### 事件对象(event)
- 事件给谁绑定的，this就是谁
- onmousemove 该事件在鼠标在元素中移动时触发
- 事件对象
  当事件的响应函数被触发时，浏览器每次都会将一个事件对象作为实参传递进响应函数
  在事件对象中封装了当前事件相关的一切信息，比如：鼠标的坐标，键盘的哪个键被按下...
-clientX、clientY
  获取鼠标指针在==当前窗口==的水平坐标和垂直坐标
- pageX、pageY 
  获取鼠标相对于当前页面的坐标
- chrome认为浏览器的滚动条时body的，可以通过body.scrollTop来获取
  火狐等浏览器认为浏览器的滚动条时html的
#### 事件冒泡
当后代元素上的事件被触发时，其祖先元素的相同事件也会被触发
取消冒泡：event.cancelBubble=true;
#### 事件的委派
我们希望，只绑定一次事件，即可应用到多个元素上，即使元素是后添加的，我们可以尝试将其绑定给元素的共同的祖先元素，这样当后代元素的事件触发时，会一直冒泡到祖先元素，从而通过祖先元素的响应函数来处理事件（事件冒泡的应用）
- target 返回触发事件的对象
#### 事件的绑定
使用对象.事件=函数的形式绑定响应函数不能绑定多个，否则后边会覆盖前边的
- addEventListener();
  通过这个方法也可以为元素绑定响应函数
  参数：
    1.事件的字符串，不要on
    2.回调函数，当事件触发时该函数会被调用
    3.是否在捕获阶段触发事件，需要一个布尔值,一般都传fasle
```
    btn.addEventListener("click",function(){ 
        alert("1");},fasle);
    btn.addEventListener("click",function(){
        alert("2);
    },fasle);
```
使用addEventListener()可以同时为一个元素的相同事件停驶绑定多个响应函数，当事件被触发时，响应函数会按照绑定顺序来执行
- attachEvent()
  在ie8中可以使用attachEvent()来绑定事件
  参数：
    1.事件的字符串，要写on
    2.回调函数
- 定义一个函数，用来指定元素绑定响应函数
  addEventListener();中的this时绑定事件的对象
  attachEvent();中的this是window
  需要统一两个方法的this
```
    function bind(obj,eventStr,callback){
        if(obj.addEventListener){
            obj.addEventListener(eventStr,callback,fasle);
        }else{
            //this是谁由调用方式决定的
            //callback.call(obj);
            obj.attachEvent("on"+eventStr,function(){
                //在匿名函数中调用回调函数
               callback.call(obj); //这样就将this变为绑定事件的对象了
            });
        }
    }
```
#### 事件的传播
1.捕获阶段
    在捕获阶段时从最外层的祖先元素，向目标元素进行事件的捕获，但是默认此时不会触发事件
2.目标阶段
    事件捕获到目标元素，捕获结束开始在目标元素上触发事件
3.冒泡阶段
    事件从目标元素向他的祖先元素传递，依次触发祖先元素上的事件
-如果希望在捕获阶段就触发事件，可以将addEventListener()的第三个参数设置为true，一般情况下我们不会希望在捕获阶段触发事件，所以这个参数一般都是false
-ie8及以下的浏览器没有捕获阶段
#### 滚轮的事件
- onmousewheel
  鼠标滚轮滚动的事件，会在滚轮滚动时触发，但是火狐不支持该属性
- DOMMouseScroll()
 在火狐浏览器中需要使用DOMMouseScroll来绑定滚动事件
 注意该事件需要通过addEventListener()函数来绑定
- event.wheelDelta 
  获取鼠标滚轮滚动的方向，这个值我们不看大小只看正负，向上滚>0，向下滚<0，但是火狐不支持
- event.detail
  火狐获取鼠标滚轮滚动的方向
使用addEventListener()方法绑定响应函数，取消默认行为时不能使用return false 需要使用vent.prevenrDefault()取消默认行为
#### 键盘事件
- onkeydown
  按键被按下
  对于onkeydown来说如果一致按着某个按键不松手，事件会一直触发
  当onkeydown连续触发时，第一次和第二次之间间隔会稍微长一点，其他的会非常快，这种设计是为了防止误操作
- onkeyup
  按键按键被松开
  键盘事件一般都会绑定给一些可以获取焦点的对象或者是document
- KeyCode
  获取按键的编码
```   
    if(event.keyCode==89){
        console.log("y被按下了);
    }

```
在文本框中输入内容属于onkeydown的默认行为，如果在onkeydown中取消了默认行为，则输入的内容不会出现在文本框中(return false;)
- altKey、shiftKey、ctrlkey
  分别用来判断alt,shift,crtl是否被按下，按下返回true,否则返回false
## BOM
    浏览器对象模型
    在BOM中为我们提供一组对象，用来完成对浏览器的操作
BOM对象
    - Window
        代表整个浏览器的窗口，同时Window也是网页中的全局对象
    - Navigator
        代表当前浏览器的信息，通过该对象可以来识别不同的浏览器
    - Location
        代表当前浏览器的地址栏信息，通过Location可以获取地址栏信息或者操作浏览器跳转页面
    - History
        代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录，但由于隐私原因，该对象不能获取到具体的历史纪录，只能操作浏览器向前或向后翻页，并且该操作只在当次访问时有效
    - Screen
        代表用户的屏幕信息，通过该对象可以获取到用户的显示器的相关信息
我们这些BOM对象在浏览器中都是作为Window对象的属性保存的，可以通过Window对象来使用，也可以直接使用
#### Navigator
```
    console.log(navigator.userAgent);
```
由于历史原是一Navigator中的大部分属性以及不能帮助我们识别浏览器了，一般我们只会使用userAgent来判断浏览器的新，userAgent是一个字符串，这个字符串包含有用来描述浏览器信息的内容，不同的浏览器会有不同的userAgent
- chrome:
  Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) ==Chrome==/77.0.3865.90 Safari/537.36
- 火狐
  Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:55.0) Gecko/20100101 ==Firefox==/55.0
- ie10
   Mozilla/5.0 (compatible; ==MSIE 10.0==; Windows NT 6.2; Trident/6.0)
- ie8
   Mozilla/4.0 (compatible; ==MSIE 8.0==; Windows NT 6.1; Trident/4.0)
- ie11
   Mozilla/5.0 (Windows NT 6.3; Trident/7.0; rv:11.0) like Gecko
```
    var ua=navigator.userAgent;
    console.log(ua);
    if(/firefox/i.test(ua)){
        alert("你是火狐);
    }
    else if(/chorme/i.test(ua)){
        alert("你是谷歌);
    }
    else if(/msie/i.test(ua)){
        alert("你是ie");
    }
    else if("ActiveObject" in window){
        alert("你是ie11");
    }

```
如果通过userAgent不能判断，Hailey通过一些浏览器中特有的对象来判断浏览器的信息，比如：ActiveObject
```
    if("ActiveObject" in window){
        alert("ie");
    }
    else{
        alert("你不是ie");
    }

```
#### history
- length
   属性，可以获取到当次访问的连接数量
- back();
  回退到上一个页面
- forward();
  跳转到下一个页面
- go();
  用来跳转到指定的页面，需要一个整数的参数
  1.表示向前跳转一个页面
  2.表示向前跳转两个页面
  -1.表示向后跳转一个页面
#### location
如果直接打印Location,可以获取地址栏的信息，直接修改location页面会自动跳转到该路径，并且生成历史纪录
```
    alert(location);
```
- assgin()
  用于跳转到其他页面，作用和直接修改location一样
- reload()
  用于重新加载当前页面，作用和刷新按钮一样
  如果在该方法中传递一个true作为参数，则会强制清空缓存刷新
- replace()
  可以使用一个新的页面替换当前页面，调用完毕也会跳转页面，不会生成历史纪录，即不能回退
### 定时器
##### 定时调用
- setInterval();
  参数：
  1.回调函数，该函数每隔一段时间被调用一次
  2.每次调用间隔的时间，单位是毫秒
  返回值
  放回一个number类型的值，这个数字用来作为定时器的唯一标识

- clearInterval();
  关闭定时器，需要一个唯一标识作为参数
##### 延时调用
- setTimeout();
  一个函数不马上执行，而是隔一段时间后再执行，且只执行一次
- clearTimeout();
  关闭延时调用

