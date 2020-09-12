---
title: PHPmvc笔记
date: 2018-11-25 19:52:23
tags: 笔记
categories: PHP
---
## 因为是在学习的中途才写的笔记，所以有一些不全，以后有时间会补全，现在主要是关于samrty语法的多。
<!--more-->
### 含义：MVC是一种设计模式，它强制性的使应用程序的输入，处理和输出分开。使用MVC应用程序被分成三个核心部件：模型（Model），视图（View），控制器（Controller），他们各自处理自己的任务。
* 模型：处理数据和业务逻辑
* 视图：通过布局向用户展示数据
* 控制器：接收用户请求，并调用相应的模型处理
1. 单一入口机制：指在一个web应用程序中，所有的请求都是指向一个脚本文件，所有对实用程序的访问都必须通过这个入口。
2. eval()函数：把字符串转换为可执行的PHP语句。
3. addslashes()函数：对特殊符号进行转义。
4. in_array()函数：判断字符串是否在数组里面
5. smarty语法
 * 配置
```
    require("libs/Smarty.class.php");//引入模板
    $smarty = new Smarty();
    $smarty->left_delimiter = "{";  //左定界符
    $smarty->right_delimiter = "}";  //右定界符
    $smarty->template_dir = "tpl";  //html模板的地址
    $smarty->compile_dir = "template_c";  //模板编译生成的文件
    $smarty->cache_dir = "cache";  //缓存
    $smarty->caching = false;
``` 
* 函数
1. assign()函数：向模板里注册变量，变量名是第一个参数，变量值是第二个参数。
2. display()函数：展示函数，在网页里展示，参数为模板文件。
* 编写模板：test.tpl
```
{变量名}
```
* 基本语法
1. 注释 {* 这里是注释的语句 *}
2. 常用变量调节器
    1. 首字母大写capitalize 例：`{$test|capitalize}`
    2. 字符串连接cat 例：`{$test|cat:"yesterday"}`
    3. 日期格式化date_format 例： `{$yesterday|date_format}`
    4. 为未赋值或为空的变量指定默认值default 例：`{$title|default:"no title"}`
    5. 转换变量字符串大小写upper(转换为大写)  lower（转换为小写）： 例： `{$test|upper}    {$TEST|lower}`
3. 条件判断语句：
    ```
    {if 条件}
    ......
    {elseif 条件}
    ......
    {else}
    ......
    {/if}
    ```
    其中条件修饰符eq相当于==，neq相当于!=，gt相当于>，lt相当于<。
3. 循环语句
    ```
    {foreach item=被赋值的量 from=变量名}
        .......
        .......
    {foreachelse}
    {/foreach}
    ```
    在smarty3里，foreach与php源生语法一致，`{foreach $test as $tt}`
4. 插件
    1. 使用registerPlugin方法注册写好的自定义函数
    2. 将写好的插件放入Smarty解压目录下lib目录下的plugins目录里
    3. php的内置函数，可以自动以修饰插件的形式在模板里运用
