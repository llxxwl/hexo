---
title: php验证码
tags: 代码
categories: PHP
abbrlink: 13584
date: 2019-03-25 16:05:08
---

### 刚刚看了验证码的实现过程，觉得有必要记一下
<!--more-->
1. 实现函数
    1) imagecreatefromjpeg() 载入图片
    2) imageTTFText() 设置字体颜色
    3) imagefill() 填充背景
    4) imagejpeg() 创建jpg图片
    5) imagedestory() 销毁图片，释放内存空间
2. 代码实现
    ```
    <?php
    //制作验证码
    //创建画布
    $img = imagecreatetruecolor(170, 40);
    //填充背景色
    $backcolor = imagecolorallocate($img, 255, 255, 255);//默认红、绿、蓝三色。
    imagefill($img, 0, 0, $backcolor);
    //产生随机验证码字符串
    $arr = array_merge(range(0,9),range('a','z'),range('A','Z'));//array_merge() 将一个或多个数组的单元合并起来，一个数组中的值附加在前一个数组的后面。返回作为结果的数组。
    shuffle($arr);//打乱数组，伪随机
    $rand_keys = array_rand($arr,4);
    $str = '';
    foreach ($rand_keys as  $value) {
        $str .= $arr[$value]; 
    }
    //保存到session
    session_start();
    $_SESSION['captcha'] = $str;//将获取的随机数验证码写入到session变量中
    //添加文字
    $span = floor(170/(4+1));
    for($i=1;$i<=4;$i++) {
        $stringcolor = imagecolorallocate($img, mt_rand(0,255), mt_rand(0,100), mt_rand(0,80));
        imagestring($img, 5, $i*$span, 12, $str[$i-1], $stringcolor);//水平输出字符
    }
    //添加干扰线
    for ($i=1; $i<=6 ; $i++) {
        $linecolor = imagecolorallocate($img,mt_rand(0,255),mt_rand(0,100),mt_rand(0,80));
        imageline($img,mt_rand(0,169),mt_rand(0,39),mt_rand(0,169),mt_rand(0,39),$linecolor);//设置随机字体和x,y坐标
    }
    //添加干扰点
    for($i=0;$i<strlen($_SESSION['captcha']);$i++){
        $pixel = imagecolorallocate($img,mt_rand(100,150),mt_rand(0,120),mt_rand(0,255));//设置背景色
        imagesetpixel($img, mt_rand(0,169), mt_rand(0,39), $pixel);//设置随机字体和x,y坐标
    }
    //输出图片
    header("Content-type:image/png");
    ob_clean();//清理缓冲区
    imagepng($img);//输出图片
    imagedestroy($img);//销毁图片
    ```
    mt_rand()返回随机整数