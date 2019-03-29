# CSS学习
## 1.三栏布局
    高固定，左右宽度300px中间自适应
    ```
    <section>
        <article>
            <div class="left></div>
            <div class="center></div>
            <div class="right></div>
        </article>
    </section>
    ```
* float
    ```
    <style>
        article{
            
        }
        .left{
            float:left;
            width:300px;
        }
        .right{
            float:right;
            width:300px;
        }
        .center{
            
        }
    </style>
    ```
    缺点：脱离了文档流，清楚浮动困难。
    优点：兼容性好。
    当高度不确定时：
* display:absolute
    ```
    <style>
        article{
            position:absolute;
        }
        .left{
            left:0;
            width:300px;
        }
        .right{
            right:0;
            width:300px;
        }
        .center{
            left:300px;
            right:300px;
        }
    </style>
    ```
    缺点：需要子元素也脱离文档流，导致有效性，可shiy使用性低。
    优点：快捷（配合js）
* display:flex
    ```
    <style>
        article{
            display:flex;
        }
        .left{
            width:300px;
        }
        .right{
            width:300px;
        }
        .center{
            flex:1; //原理 重！！
        }
    </style>
    ```
    相对比较完美，css3新出现的。
* display:table
    ```
    <style>
        article{
            display:table;
            width:100%;
            height:100px;
        }
         article>div{
            display:table-cell; 
        }
        .left{
            width:300px;
        }
        .right{
            
        }
        .center{
            width:300px;
        }
    </style>
    ```
    缺点：当其中一个单元格高度超出时，另外两个高度也会增高。
    优点：兼容性好。
* display:grid
    ```
    <style>
        article{
            display:grid;
            width:100%;
            grid-template-rows:100px; // 设置网格高度。
            grid-template-columns:300px auto 300px; // 设置网格列。
        }
         article>div{
        }
        .left{
        }
        .right{
            
        }
        .center{
        }
    </style>
    ```
    新出的技术，说明自己学习能力强。
    
*   去掉高度已知，float，absolute，grid不能用。flex和table可以用。
## 2.盒模型
*   基本概念：
    *   标准模型
        **宽高为content。**
    ![20140124141001609.jpg](http://kod.ksust.com/index.php?user/publicLink&fid=d7c7H7s5YRYNwwteKHE4-D2FGQXZVMYtrJSoghvlcSa--9le6xb1XP2IMHsWL7oh4E56yIKRnud3NDO6TjCRgjtRMlSlXt-BEEiJlojJUn8gbs_DocTh1XaDvRYzAqv6jmgR6Nw&file_name=/20140124141001609.jpg)
    *   ie模型
        **宽高为content+padding+border。**
        ![20140124141131218.jpg](http://kod.ksust.com/index.php?user/publicLink&fid=ada8RW97wRPMm-zKCLlfD3ZxD2NF3S5gX1naKnEa0xE_ibZt4QyFoNTTkUQ02CArEPOQBvw1cZImfVbHzTx3kAI8Y4pi3ypuQVEaEC_nWZjtc956SkIpbmYEE56RJF9LDdSiQKI&file_name=/20140124141131218.jpg)
*   如何设置：
    设置标准模型：  box-sizing:content-box;
    设置ie模型：    box-sizing:border-box;
*   js如何获取盒模型对应的宽和高
    * dom.style.width/height //只能获取行内定义style的标签
*   边距重叠问题
**两个或多个块级盒子的垂直相邻边界会重合。**
    结果的边界宽度是相邻边界宽度中最大的值。如果出现负边界，则在最大的正边界中减去绝对值最大的负边界。如果没有正边界，则从零中减去绝对值最大的负边界。
*   边距重叠问题解决
**利用bfc（块级格式化上下文）**
    在div外层包裹一个div，把该div设置为bfc，设置方法是：满足下列的任意一个或多个条件即可：
1、float的值不是none。
2、position的值不是static或者relative。
3、display的值是inline-block、table-cell、flex、table-caption或者inline-flex
4、overflow的值不是visible
## 3.单行溢出
    overflow: hidden;//超出部分设置为隐藏
    text-overflow:ellipsis;//文本超出部分显示为省略
    white-space: nowrap;//不换行 
## 4. CSS权重优先级顺序
**!important > 行内样式 > ID > 类、伪类、属性 > 标签名 > 继承 > 通配符**
