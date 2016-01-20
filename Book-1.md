#第一章 PHP基础知识

##1. PHP入门指引

* PHP是什么?
PHP（“PHP: Hypertext Preprocessor”，超文本预处理器的字母缩写）是一种被广泛应用的开放源代码的多用途脚本语言，它可嵌入到 HTML中，尤其适合 web 开发。

Example #1 一个介绍性的范例

```
<html>
<head>
<title>Example</title>
</head>
<body>

<?php
echo "Hi, I'm a PHP script!";
?>

</body>
</html>

```

* PHP能做什么?


##2. PHP 安装及配置

###2.1 Linux 安装

###2.2 Mac 安装

###2.3 php.ini解读及使用说明

;官方推荐配置 之前叫Zend Optimizer+ （ php 5.5.3改名opcache）
[opcache] 
zend_extension=opcache.so
;OPcache 的共享内存大小，以兆字节为单位
opcache.memory_consumption=128

;用来存储临时字符串的内存大小，以兆字节为单位。 PHP 5.3.0 之前的版本会忽略此配置指令。
opcache.interned_strings_buffer=8


;OPcache 哈希表中可存储的脚本文件数量上限。 真实的取值是在质数集合 { 223, 463, 983, 1979, 3907, 7963, 16229, 32531, 65407, 130987 } 中找到的第一个比设置值大的质数。 设置值取值范围最小值是 200，最大值在 PHP 5.5.6 之前是 100000，PHP 5.5.6 及之后是 1000000。
opcache.max_accelerated_files=4000

;检查脚本时间戳是否有更新的周期，以秒为单位。 设置为 0 会导致针对每个请求， OPcache 都会检查脚本更新。如果 opcache.validate_timestamps 配置指令设置为禁用，那么此设置项将会被忽略。
opcache.revalidate_freq=60

;如果启用，则会使用快速停止续发事件。 所谓快速停止续发事件是指依赖 Zend 引擎的内存管理模块 一次释放全部请求变量的内存，而不是依次释放每一个已分配的内存块。
opcache.fast_shutdown=1

;仅针对 CLI 版本的 PHP 启用操作码缓存。 通常被用来测试和调试
opcache.enable_cli= On

;启用操作码缓存
opcache.enable= On


;更多配置项见
http://php.net/manual/zh/opcache.configuration.php

###2.4 Docker安装
