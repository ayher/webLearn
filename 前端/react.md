# **React学习**
## 1. 优势
* **声明式开发**
        不像原生js那样需要一步步，程序员告诉网页怎么操作DOM，发出一步步命令实现功能。而react是程序员告诉网页要实现什么功能，具体的实现方法是react自己实现的。
* **组件化**
        react把网页分成一个个的模块，具体到项目就是组件，这样可以提高项目开发的效率和，提高代码的简洁性，可读性。
* **单项数据流**
        数据只能从父组件传递给子组件，子组件不能修改父组件上的信息，如果想修改只能通过调用父组件的方法，让父组件自己修改自己的信息。
* **视图层框架**
        react相隔较远的组件传值比较困难，所以不能单独作为一个大型框架，需要配合数据层框架，如redux。所以react是视图层框架。
* **能和别的框架并存**
        react操作的单位是组件，在组件上层其他DOM就和react无关，在这里就可以用别的js框架了。
##  2. react中的es6
* **块级作用域**
        let的作用域是在函数中的，在函数外面就没用了。
* **参数默认值**
        可以给函数的参数一个默认值，如：
        
        ```
        function test(value = 10){
            console.log(value);
        }
        test()  // 10
        test(1) // 1
        ```
* **箭头函数**
        箭头函数没用this,和普通函数不一样，其内部的this就是外部的this。
* **展开运算符**
        不需要apply来给数组添加值。如：
        ```
        var arr=[1,2,3];
        console.log(...arr) // 1 2 3
        console.log(...arr,5) // 1 2 3 5
                        
        var test= [...arr,4,5]
        console.log(test) // 1 2 3 4 5
        
        var function t(a,b,c){}
        t(...arr);
        ```
* **解构赋值**
    
    ```
    var p={a:1,b:2}
    var {a}=p;
    console.log(a);  // 1
    ```
    
* **class语法糖**
    类似于类一样，class有extends等的结构；

    ```
        class Dog{
            constructor(name){
               this.name = name;            
            }
            saySomething(){
               console.log('汪汪汪');      
            }
        }
        var dog = new Dog('LiLy'); //也是通过new实例化
        dog.name //LiLy
        dog.saySomething() //汪汪汪
    ```
        
##  3. 虚拟DOM
* 加载过程：
        1. 有state数据。
        2. 有JSX模板。
        3. 数据+模板 生成虚拟DOM。
        4. 根据虚拟DOM生成真实的DIM，显示。
        5. state发送变化。
        6. 数据+模板 生成新的虚拟DOM。
        7. 比较原始虚拟DOM和新的虚拟DOM。
        8. 找出不同，直接操作虚拟DOM改变。
* 实质
    虚拟DOM就是一个js对象，用它来描述真实DOM。
* 结构
    真实DOM：
    ```
    <div id="div1">
        <span>
            hello
        </span>
    </div>
    ```
    虚拟DOM：
    
    ```
    [
        'div',
        {'id':'div1'},
        [
            'span',
            {},
            'hello'
        ],
    ];
* 优点
    1. 提高浏览器的性能。
    2. 能跨应用实现。（如手机端：只需要把 虚拟DOM->真实DOM 变成 虚拟DOM->手机原生）
        
##  4. 生命周期
    