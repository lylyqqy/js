强语言允许编译器再编译时检测错误，我们能越早检测和修复错误，付出的代价就越小
在js中，那些字符对也可能出现在正则表达式字面量里，所以块注释对于被注释的代码块来说是不安全的
```
    /*
        var rm=/a*/.match(s);
    */
```
转义字符用来把那些正常情况下不被允许的字符插入到字符串中
  
switch、while、for和do语句允许有一个可选的前置标签（label）,它配合break语句来使用
if语句中，下面列出的值被当作假
- false
- null
- undefined
- 空字符串""
- 数字 0
- 数字 NAN
  
switch()内数字或字符串
for in语句会枚举一个对象的所有属性名  

object.hasOwnProperty(variable)来确定这个属性名是该对象的成员，还是来自于原型链
  
try语句执行一个代码块，并捕获该代码块抛出的任何异常，catch从句定义一个新的变量variable来接收抛出的异常对象，throw语句抛出一个异常，如果throw语句在一个try代码块中，那么控制流会跳转到catch从句中，如果throw语句在函数中，则该函数调用被放弃，控制流跳转到调用该函数的try语句的catch从句中。
throw语句中的表达式通常是一个对象字面量，它包含一个name属性和一个message属性。异常捕获器可以使用这些信息区决定该做什么。  
typeof运算符产生的值有number、string、boolean、undefined、function、object，如果运算数是一个数组或null，那么结果是object
/运算符可能会产生一个非整数结果，即使两个运算数都是整数
在对象字面量中，如果属性名是一个合法的js标识符且不是保留字，则并不强制要求用引号括住属性名
要检索对象里包含的值，可以采用在[]后缀中括住一个字符串表达式的方式  
##### 枚举  
for in 语句可用来遍历一个对象中的所有属性名，该枚举过程将会列出所有的属性，包括函数和原型中的属性，所以有必要过滤掉那些你不想要的值，最为常用的过滤器是hasOwnProperty方法，以及使用typeof来排除函数。
属性名出现的顺序是不确定的，因此要对任何可能出现的顺序有所准备，如果你想要确保属性以特定的顺序出现，最好的办法就是完全避免使用for in语句，而是创建一个数组，在其中以正确的顺序包含属性名
##### 删除
delete运算符可以用来删除对象的属性，如果对象包含该属性，那么该属性就会被移除，它不会初级原型链中的任何对象
##### 减少全局变量污染
1. 把全局性的资源都纳入一个名称空间之下，你的程序与其他应用程序，组件或类库之间发生冲突的可能性就会显著降低。
2. 用闭包来进行信息隐藏的方式。
##### 函数调用模式
以此模式调用函数时，this被绑定到全局对象，这是语言设计上的一个错误，倘若语言设计正确，那么当内部函数被调用时，this应该仍然到外部函数的this变量，这个设计错误的后果就是方法不能利用内部函数来帮助它工作，因为内部函数的this被绑定了错误的值，所以不能共享该方法对对象的访问权，幸运的是，有一个很容易的解决方案：如果该方法定义一个变量并给它赋值为this，那么内部函数就可以通过那个变量访问到this，按照约定，把那个变量命名为that
```
    //给myObejct增加一个double方法
    myObject.double = function(){
        var that =this;
        var helper = function(){
                that.value=add(that.value,that.value);
        }
        helper();  //以函数的形式调用helper
    }
    //以方法的形式调用double
    myObject.double();
    document.writeln(myObject.value);  //6
``` 
##### 返回
一个函数总会返回一个值，如果没有指定返回值，则返回undefined
##### 柯里化
把多参数函数转换为一系列但参数函数并进行调用的技术
##### arguments
aeguments数组并非一个真正的数组，所以它并没有concat方法，要避开这个问题，我们必须在arguments数组上应用数组的slice方法，这样产生出拥有concat方法的常规数组
***
基本类型的原型是公用结构，所以在类库混用时无比小心，一个保险的做法就是只在确认没有该方法时才添加它
```
    Function.prototype.method=function (name,func){
        if(!this.prototype[name]){
            this.prototype[name]=func;
        }
        return this;
    };

```