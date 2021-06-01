---
title: 'js,jquery的一点小基础'
tags:
  - js
  - jQuery
categories: web前端
abbrlink: 56164
date: 2018-07-25 16:05:05
---

#### 一、javascript
1. 使用

    HTML 中的脚本必须位于 <script> 与 </script> 标签之间。脚本可被放置在 HTML 页面的 <body> 和 <head> 部分中
2. 输出
<!--more-->
        document.write()  大部分的输出方式，写到文档输出
        document.getElementById(id)  用id属性标识HTML元素，达到访问目的

        ```
        <!DOCTYPE HTML>
        <html>
        <body>
        <p id="demo">biaoqian</p>
        <script>
        document.getElementById().innerText;
        </script>
        </body>
        </html>
        ```
3. JavaScript严格区分大小写
4. 函数
    - toUpperCase()   小写转大写
    - getDay()  得到现在的日期
5. 错误
    用try，catch检测，try与catch不可分割，成对出现。try语句里是有错的代码块，catch语句输出错误信息。throw 抛出异常 。可用可不用
6. HTML事件
    ```
    onchange   HTML元素改变
    onclick       用户点击HTML元素
    onmouseover   用户在一个HTML元素上移动鼠标
    onmouseout    用户在一个HTML元素上移开鼠标i
    onkeydown     用户按下键盘按键
    onload            浏览器已完成页面的加载
    ```
    可用于处理表单验证，用户输入，用户行为及浏览器动作。
7. 判断对象的具体类型
    
    通过instanceof操作符来判断
    ```
    arr = [1,2,3];
    if(arr instanceof Array){
        document.write("arr 是一个数组");
    } else {
        document.write("arr 不是一个数组");
    }   
    ```
    如果是返回true，如果不是则返回false。
8. 严格模式（可用可不用）
* 不允许使用未声明的变量
* 不允许删除变量或对象
* 不允许删除函数
* 不允许变量重名
* 不允许使用八进制
* 不允许使用转义字符
* 不允许对只读属性赋值
* 不允许对一个使用getter方法读取的属性进行复制
* 变量名不能使用eval，arguments字符串
* 保留关键字
#### 二、jQuery
1. 语法
    
    通过选取HTML元素，并对选取的元素执行某些操作
    基础语法：`$(selector)action()`
    * '$'定义jQuery
    * 选择符selector 查询和查找HTML元素
    * action()执行对元素的操作
    
    为了防止文档在完全加载（就绪）之前运行 jQuery 代码，即在 DOM 加载完成后才可以对 DOM 进行操作，jQuery函数要在一个ready函数中
    ```
    $(function(){
        //jquery代码
    });
    ```
2. 选择器
    * 元素选择器：基于元素名选取元素
    ```
    //在页面中选取所有<p>元素
    $("p")
    ```
    * #id选择器，通过唯一id选取指定元素
    * .class选择器，通过指定的class选取元素
3. jQuery事件
    - click()当按钮点击事件被触发时会调用一个函数
    - mouseenter()当鼠标指针穿过元素时，会发生mouseenter事件
    - mouseleave()当鼠标指针离开元素时，会发生mouseleave事件
    - focus() 当元素获得焦点时，发生focus事件
4. jQuery Dom操作
    * 获取、设置内容
    text() - 设置或返回所选元素的文本内容

    html() - 设置或返回所选元素的内容（包括 HTML 标记）

    val() - 设置或返回表单字段的值
    * 获取、设置属性：attr()获取属性值
    * 添加元素
        - append() 在被选元素的结尾插入内容
        - preappend() 在被选元素的开头插入内容
        - before() 在被选元素之前插入内容
        - after() 在被选元素之后插入内容
5. 遍历
    * 向上遍历Dom
        - parent方法返回被选元素的直接父元素
        - parents方法返回被选元素的所有父元素，一路向上，一直到根元素
        - parentsUntil方法返回介于两元素之间的  所有祖先元素
    * 向下遍历
        - children方法返回被选元素的所有直接子元素
        - find方法返回被选元素的所有后代元素，一路向下到最后一个后代
    - 水平遍历
        - siblings返回被选元素的所有同胞元素
        - next返回被选元素的下一个同胞元素

