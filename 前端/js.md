# **javascript学习**
## 1. 数据类型
* 基本数据类型
** Number,Boolean,String,Undefined,Null,Symbol*
        1. 基本类型不可以改变，任何方法都无法改变基本类型的值。
        2. 不可以给基本类型添加属性或方法。
        3. 基本类型存放于栈内存。包括变量标识符合变量的值。
* 引用数据类型
        * Object，Array*
        1. 可以添加属性和方法，也可以删除属性和方法。
        2. 引用类型存储需要栈区和堆区，栈区内存保存变量标识符和指向堆内存中该对象的指针，堆区保存变量的值。
* 两者比较
        1. 基本类型的==和===有区别，引用类型无区别。
        2. 基本类型赋值互不影响，而引用类型会影响，引用类型是复制地址的。
## 2. 深浅拷贝
    * 复制后跟着改变的是浅拷贝，不随着复制改变为浅拷贝。
    * 实现深拷贝的方法：
        1. 用JSON对象的parse和stringify。
            
            ```
            function deepClone(obj){
                let _obj = JSON.stringify(obj),
                    objClone = JSON.parse(_obj);
                return objClone
            }    
            ```
## 3. this的学习
    **在Javascript中this总是指向调用它所在方法的对象。因为this是在函数运行时，自动生成的一个内部对象，只能在函数内部使用。**
    1. 全局函数调用
        **全局函数调用中的this是window**
        
        ```
        var name = "global this";

        function globalTest() {
            this.name = "rename global this"
            console.log(this.name);
        }
        globalTest(); //rename global this
        ```
    2. 对象方法调用
        **函数作为对象方法调用，this指向调用他的对象**
        
        ```
        function showName() {
            console.log(this.name);
        }
        var obj = {};
        obj.name = "ooo";
        obj.show = showName;
        obj.show(); //ooo
        ```
    3. 构造函数调用
        **构造函数调用指向的是函数本身，因为new了个对象**
        
        ```
        var name = "global name";
    
        function showName() {
            this.name = "showName function";
        }
        var obj = new showName();
    
        console.log(obj.name); //showName function
        console.log(name); //global name
        ```
    4. apply/call调用
        **apply和call都可以改变函数体内部的this**
        
        ```
        var value = "Global value";
    
        function FunA() {
            this.value = "AAA";
        }
    
        function FunB() {
            console.log(this.value);
        }
        FunB(); //Global value 因为是在全局中调用的FunB(),this.value指向全局的value
        FunB.call(window); //Global value,this指向window对象，因此this.value指向全局的value
        FunB.call(new FunA()); //AAA, this指向参数new FunA()，即FunA对象
    
        FunB.apply(window); //Global value
        FunB.apply(new FunA()); //AAA
        ```
    5. setTimeout & setInterval
        **延时函数的this是window**
        ```
        //默认情况下代码
        function Person() {  
            this.age = 0;  
            setTimeout(function() {
                console.log(this);
            }, 3000);
        }
        var p = new Person();//3秒后返回 window 对象
        ==============================================
        //通过bind绑定
        function Person() {  
            this.age = 0;  
            setTimeout((function() {
                console.log(this);
            }).bind(this), 3000);
        }
        var p = new Person();//3秒后返回构造函数新生成的对象 Person{...}
        ```
    6. 普通对象中的this
        **普通对象中的this指向window**
        ```
        var obj={
           that:this,
           i:10,
           b:function y() {
               console.log(this)
               console.log(this.that);
           }
       }
       obj.b();
       // obj{that: Window, i: 10, b: ƒ}
       // Window{}
        ```
    7. ES6箭头函数的this
        **箭头函数不绑定this， 它会捕获其所在（即定义的位置）上下文的this值， 作为自己的this值**
        * call() / apply() / bind() 方法对于箭头函数来说只是传入参数，对它的 this 毫无影响。
        * 考虑到 this 是词法层面上的，严格模式中与 this 相关的规则都将被忽略。（可以忽略是否在严格模式下的影响）
        
        ```
        var obj = {
          i: 10,
          b: () => console.log(this.i, this),
          c: function() {
            console.log( this.i, this)
          }
        }
        obj.b();  // undefined window{...}
        obj.c();  // 10 Object {...}
        ```
    参考：https://www.cnblogs.com/dongcanliang/p/7054176.html ， https://www.cnblogs.com/Nancy-wang/p/6928395.html
## 4. 原型链
### 1.构造函数
**instanceof用于判断引用类型属于哪个构造函数的方法**
    var a={}其实是var a=new Object()的语法糖
    var a=[]其实是var a=new Array()的语法糖
    function Foo(){}其实是var Foo=new Function()
## 5. 异步与单线程
## 6. call,apply,bind的区别
**1.三者都可以改变this的属性。**
    **2.传参方式**
        call(this,参数1，参数2,...)
        apply(this,[参数1，参数2，...)
        bind(this,参数1，参数2,...)
**3.返回值**
        bind返回的是一个函数。
