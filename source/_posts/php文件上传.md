---
title: php文件上传
date: 2019-04-19 14:53:58
tags: 代码  
categories: PHP
---

#### PHP实现文件上传
<!--more-->
1. _FILES

    $_FILES是PHP的全局数组，可以上传文件。第一个参数是文件名，第二个参数可以使如下所示的几个：
    ```
    $_FILES["file"]["name"] - 上传文件的名称
    $_FILES["file"]["type"] - 上传文件的类型
    $_FILES["file"]["size"] - 上传文件的大小，以字节计
    $_FILES["file"]["tmp_name"] - 存储在服务器的文件的临时副本的名称
    $_FILES["file"]["error"] - 由文件上传导致的错误代码
    ```
    错误代码各值所代表的意思：
    ```
    UPLOAD_ERR_OK           //其值为 0，没有错误发生，文件上传成功。 
    UPLOAD_ERR_INI_SIZE     //其值为 1，上传的文件超过了 php.ini 中 upload_max_filesize 选项限制的值。 
    UPLOAD_ERR_FORM_SIZE    //其值为 2，上传文件的大小超过了 HTML 表单中 MAX_FILE_SIZE 选项指定的值。 
    UPLOAD_ERR_PARTIAL      //其值为 3，文件只有部分被上传。 
    UPLOAD_ERR_NO_FILE      //其值为 4，没有文件被上传。 
    UPLOAD_ERR_NO_TMP_DIR   //其值为 6，找不到临时文件夹。PHP 4.3.10 和 PHP 5.0.3 引进。 
    UPLOAD_ERR_CANT_WRITE   //其值为 7，文件写入失败。PHP 5.1.0 引进。 
    ```
2. move_uploaded_file

    * move_uploaded_file函数，将上传的文件移动到新的位置。
    * 说明：`move_uploaded_file( string $filename, string $destination) : bool`,本函数检查并确保由 filename 指定的文件是合法的上传文件（即通过 PHP 的 HTTP POST 上传机制所上传的）。如果文件合法，则将其移动为由 destination 指定的文件。 这种检查显得格外重要，如果上传的文件有可能会造成对用户或本系统的其他用户显示其内容的话。 
    * 参数：`filename` 上传的文件名      `destination` 要移动到的位置
3. 文件上传表单
    ```
    <html>
    <head>
    <meta charset="utf-8">
    <title>lpower</title>
    </head>
    <body>

    <form action="upload_file.php" method="post" enctype="multipart/form-data">
        <label for="file">文件名：</label>
        <input type="file" name="file" id="file"><br>
        <input type="submit" name="submit" value="提交">
    </form>

    </body>
    </html>
    ```
    注意：<form> 标签的 enctype 属性规定了在提交表单时要使用哪种内容类型。在表单需要二进制数据时，比如文件内容，请使用 "multipart/form-data"。
4. 上传脚本
    ```
    <?php
    // 允许上传的图片后缀
    $allowedExts = array("gif", "jpeg", "jpg", "png");
    $temp = explode(".", $_FILES["file"]["name"]);
    echo $_FILES["file"]["size"];
    $extension = end($temp);     // 获取文件后缀名
    if ((($_FILES["file"]["type"] == "image/gif")
    || ($_FILES["file"]["type"] == "image/jpeg")
    || ($_FILES["file"]["type"] == "image/jpg")
    || ($_FILES["file"]["type"] == "image/pjpeg")
    || ($_FILES["file"]["type"] == "image/x-png")
    || ($_FILES["file"]["type"] == "image/png"))
    && ($_FILES["file"]["size"] < 204800)   // 小于 200 kb
    && in_array($extension, $allowedExts))
    {
        if ($_FILES["file"]["error"] > 0)
        {
            echo "错误：: " . $_FILES["file"]["error"] . "<br>";
        }
        else
        {
            echo "上传文件名: " . $_FILES["file"]["name"] . "<br>";
            echo "文件类型: " . $_FILES["file"]["type"] . "<br>";
            echo "文件大小: " . ($_FILES["file"]["size"] / 1024) . " kB<br>";
            echo "文件临时存储的位置: " . $_FILES["file"]["tmp_name"] . "<br>";
            
            // 判断当期目录下的 upload 目录是否存在该文件
            // 如果没有 upload 目录，你需要创建它，upload 目录权限为 777
            if (file_exists("upload/" . $_FILES["file"]["name"]))
            {
                echo $_FILES["file"]["name"] . " 文件已经存在。 ";
            }
            else
            {
                // 如果 upload 目录不存在该文件则将文件上传到 upload 目录下
                move_uploaded_file($_FILES["file"]["tmp_name"], "upload/" . $_FILES["file"]["name"]);
                echo "文件存储在: " . "upload/" . $_FILES["file"]["name"];
            }
        }
    }
    else
    {
        echo "非法的文件格式";
    }
    ?>
    ```
    服务器的 PHP 临时文件夹中创建了一个被上传文件的临时副本,要保存上传的文件，要拷贝到upload文件下。
