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
##### 数组
js提供了一种拥有一些类数组特性的对象，它的属性的检索和更新的方式与对象一模一样，只不过多一个可以用整数作为属性名的特性
length属性的值是这个数组的最大整数属性名加1，它不一定等于数组里的属性的个数  

你可以直接设置length的值，设置更大的length不会给数组分配更多的空间
##### 正则表达式
用正则表达式字面量创建RegExp对象共享同一个实例
```
    function make_a_matcher(){
        return /a/gi;
    }
    var x = make_a_matcher();
    var y = make_a_matcher();
    // x和y是相同的对象
    x.lastIndex = 10;
    document.write(y.lastIndex);  //10
```
一个正则表达式因子可以是一个字符，一个由圆括号包围的组，一个字符类，或者是一个转义序列，除了控制字符和特殊字符以外，所有的字符都会按照字面处理：
```
     \ / [ ] ( ) { } ? + * | . ^ $
```
如果你希望上面列出的字符按字面去匹配，那么必须要用一个\前缀来进行转义，你如果拿不准的话，可以给任何特殊字符都添加一个\前缀来使其字面化。
一个未被转义的.会匹配出行结束以外的任何字符
##### 方法
- array.push()
把一个或多个参数添加到数组的尾部，和concat方法不同的是，它会修改array，如果参数是一个数组，它会把参数数组作为单个元素整个添加到数组中，并返回这个array的新长度值
- array.reverse()
  修改数组自身
- array.sort()
```
    var n = [4,8,15,16,23,42];
    n.sort(function (a,b) ){
        return a-b;
    });
    // n是[4，8，15，16，23，42]
```
上面这个函数可以使数字正确排序，但它不能使字符串排序，如果我们想要给任何包含简单值得数组排序，可以这样：
```
    var m = ["aa","bb","a",4,8,15,16];
    m.sort(function (a,b){
        if(a===b){
            return 0;
        }
        if(typeof a === typeof b){
            return a<b? -1:1;
        }
        return typeof a< typeof b? -1:1;
    });
    // m:[4,8,15,16,"a","aa","bb"]
```
- number.toFixed()
  将number转换称为一个十进制形式得字符串
- regexp.exec(string)
  如果regexp带有一个g标识，查找得不是从这个字符串的其实位置来世，而是从regexp.lastIndex(初始值为0)位置开始，如果匹配成功，那么regexp.lastIndex将被设置为该匹配后第一个字符的位置，不成功的匹配会重置regexp.lastIndex为0.
  这就允许你通过循环调用exec去查询一个匹配模式在一个字符串中发生了几次，有两件事情需要注意，如果你提前退出了这个循环，再次进入这个循环前必须把regexp.lastIndex重置为0，而且，^因子仅匹配regexp.lastIndex为0的情况。  
      
- string.replace(searchValue,replaceValue)
  repalce方法对string进行查找和替换操作，并返回一个新的字符串，参数searchValue可以使一个字符串或一个正则表达式对象。如果searchValue使一个正则表达式并且带有g标识，它会替换所有的匹配，如果没有带g标识，它仅会替换第一个匹配
  replaceValue可以使一个字符床或一个函数，如果replaceValue是一个函数，那么每遇到一次匹配函数就会配调用一次，而该函数返回的字符串会被用作替换文本