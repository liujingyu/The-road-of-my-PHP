#[第一章 PHP基础知识](https://github.com/liujingyu/The-road-of-my-PHP/blob/master/Book-1.md)

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
PHP 能做任何事。PHP 主要是用于服务端的脚本程序，因此可以用 PHP 来完成任何其它的 CGI 程序能够完成的工作，例如收集表单数据，生成动态网页，或者发送／接收 Cookies。但 PHP 的功能远不局限于此。

PHP 脚本主要用于以下三个领域：

* 服务端脚本。这是 PHP 最传统，也是最主要的目标领域。开展这项工作需要具备以下三点：PHP 解析器（CGI 或者服务器模块）、web 服务器和 web 浏览器。需要在运行 web 服务器时，安装并配置 PHP，然后，可以用 web 浏览器来访问 PHP 程序的输出，即浏览服务端的 PHP 页面。如果只是实验 PHP 编程，所有的这些都可以运行在自己家里的电脑中。请查阅安装一章以获取更多信息。
* 命令行脚本。可以编写一段 PHP 脚本，并且不需要任何服务器或者浏览器来运行它。通过这种方式，仅仅只需要 PHP 解析器来执行。这种用法对于依赖 cron（Unix 或者 Linux 环境）或者 Task Scheduler（Windows 环境）的日常运行的脚本来说是理想的选择。这些脚本也可以用来处理简单的文本。请参阅 PHP 的命令行模式以获取更多信息。
* 编写桌面应用程序。对于有着图形界面的桌面应用程序来说，PHP 或许不是一种最好的语言，但是如果用户非常精通 PHP，并且希望在客户端应用程序中使用 PHP 的一些高级特性，可以利用 PHP-GTK 来编写这些程序。用这种方法，还可以编写跨平台的应用程序。PHP-GTK 是 PHP 的一个扩展，在通常发布的 PHP 包中并不包含它。如果对 PHP-GTK 感兴趣，请访问其» 网站以获取更多信息。


##2. PHP 安装及配置

###2.1 Linux 安装

首先，php安装主要分为源码编译安装和包安装。
下面是包安装的命令：

```
rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm

yum --enablerepo=remi,remi-php56 -y install php php-common php-cli php-gd php-pear php-mysqlnd php-pdo php-pgsql php-pecl-mongo php-sqlite php-pecl-memcached php-pecl-memcache php-xml php-soap php-mcrypt php-fpm php-redis php-opcache php-mbstring php-xhprof
```

php选取的web服务器主要有两种Apache和Nginx。目前，大部分高并发的应用一般选取Nginx,nginx支持长连接200w。select，poll，epoll都是IO多路复用的机制。Apache选用的是select,Nginx选用的是epoll。nginx出来比较晚，而且遇到了当今的大并发问题，并将其考虑到nginx设计中，可谓后来居上。与此同时，Apache也不敢是示弱，增加了多线程模式worker，但是php的第三方扩展可能有线程安全问题，所以目前用perfork模式的居多。
除此之外，还有命令行运行模式。

再次，源码编译安装:

在本示例中，我们仅进行包含 PHP-FPM 和 MySQL 支持的简单配置。

```
tar zxf php-x.x.x

./configure --prefix=/usr/local/php --enable-fpm --with-mysql

make && make install


```

###2.2 Mac 安装

###2.3 php.ini解读及常见问题解答

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



[session]

;session.save_handler 定义了来存储和获取与会话关联的数据的处理器的名字。默认为 files。

session.save_handler = files

;session.save_path 定义了传递给存储处理器的参数。如果选择了默认的 files 文件处理器，则此值是创建文件的路径。默认为 /tmp。

session.save_path = /tmp

;session.name 指定会话名以用做 cookie 的名字。只能由字母数字组成，默认为 PHPSESSID。

session.name = PHPSESSID

;session.auto_start 指定会话模块是否在请求开始时自动启动一个会话。默认为 0（不启动）。无论是通过调用函数 session_start() 手动开启会话， 还是使用配置项 session.auto_start 自动开启会话， 对于基于文件的会话数据保存（PHP 的默认行为）而言， 在会话开始的时候都会给会话数据文件加锁， 直到 PHP 脚本执行完毕或者显式调用 session_write_close() 来保存会话数据。
在此期间，其他脚本不可以访问同一个会话数据文件。出处：http://php.net/manual/zh/function.session-write-close.php

session.auto_start 0

;session.serialize_handler 定义用来序列化／解序列化的处理器名字。 当前支持 PHP 序列化格式 (名为 php_serialize)、 PHP PHP 内部格式 (名为 php 及 php_binary) 和 WDDX (名为 wddx)。 如果 PHP 编译时加入了 WDDX 支持，则只能用 WDDX。 自 PHP 5.5.4 起可以使用 php_serialize。 php_serialize 在内部简单地直接使用 serialize/unserialize 函数，并且不会有 php 和 php_binary 所具有的限制。 使用较旧的序列化处理器导致 $_SESSION 的索引既不能是数字也不能包含特殊字符(| and !) 。 使用
php_serialize 避免脚本退出时，数字及特殊字符索引导致出错。 默认使用 php。

session.serialize_handler = php

;session.gc_probability 与 session.gc_divisor 合起来用来管理 gc（garbage collection 垃圾回收）进程启动的概率。默认为 1。
; Default Value: 1
; Development Value: 1
; Production Value: 1

session.gc_probability 1

;session.gc_divisor 与 session.gc_probability 合起来定义了在每个会话初始化时启动 gc（garbage collection 垃圾回收）进程的概率。此概率用 gc_probability/gc_divisor 计算得来。例如 1/100 意味着在每个请求中有 1% 的概率启动 gc 进程。session.gc_divisor 默认为 100。

session.gc_divisor = 1000

;session.gc_maxlifetime 指定过了多少秒之后数据就会被视为“垃圾”并被清除。 垃圾搜集可能会在 session 启动的时候开始（ 取决于session.gc_probability 和 session.gc_divisor）。

session.gc_maxlifetime = 1440

;php5.4 Session提供了上传进度支持，通过$_SESSION["upload_progress_name"]就可以获得当前文件上传的进度信息，结合Ajax就能很容易实现上传进度条了。使用详情见http://www.laruence.com/2011/10/10/2217.html

session.upload_progress.enabled = 1

;session.use_cookies 指定是否在客户端用 cookie 来存放会话 ID。默认为 1（启用）。

session.use_cookies = 1

;session.use_only_cookies 指定是否在客户端仅仅使用 cookie 来存放会话 ID。。启用此设定可以防止有关通过 URL 传递会话 ID 的攻击。此设定是 PHP 4.3.0 添加的。自PHP 5.3.0开始，默认值改为1（启用）

session.use_only_cookies = 1

;session.cookie_lifetime 以秒数指定了发送到浏览器的 cookie 的生命周期。值为 0 表示“直到关闭浏览器”。默认为 0

session.cookie_lifetime = 0

;session.cookie_path 指定了要设定会话 cookie 的路径。默认为 /。

session.cookie_path = /

;session.cookie_domain 指定了要设定会话 cookie 的域名。默认为无，表示根据 cookie 规范产生 cookie 的主机名。

session.cookie_domain = 


;如果开启则表明你的cookie只有通过HTTPS协议传输时才起作用。

session.cookie_secure = 1

;Marks the cookie as accessible only through the HTTP protocol. This means that the cookie won't be accessible by scripting languages, such as JavaScript. This setting can effectively help to reduce identity theft through XSS attacks (although it is not supported by all browsers).

session.cookie_httponly =

;深入阅读

http://www.laruence.com/2012/01/10/2469.html

常见问题解答:

* 浏览器打开一个网站很慢，打开新的tab，输入了该网站的另一个网页还是慢？
* 答：对于大量使用 Ajax 或者并发请求的网站而言，这可能是一个严重的问题。 解决这个问题最简单的做法是如果修改了会话中的变量， 那么应该尽快调用 session_write_close() 来保存会话数据并释放文件锁。 还有一种选择就是使用支持并发操作的会话保存管理器来替代文件会话保存管理器。

* session 文件存储file lock问题？
* 答：无论是通过调用函数 session_start() 手动开启会话， 还是使用配置项 session.auto_start 自动开启会话， 对于基于文件的会话数据保存（PHP 的默认行为）而言， 在会话开始的时候都会给会话数据文件加锁， 直到 PHP 脚本执行完毕或者显式调用 session_write_close() 来保存会话数据。 在此期间，其他脚本不可以访问同一个会话数据文件。

* 为什么重启浏览器后 Session 数据就取不到了？
* 答：session.cookie_lifetime = 0

* 为什么有时首次访问一个网站，用xhprof检测到session创建占了整个请求的80%的时间？

* Session 和 Cookie 有什么关系？

* 为什么不能用memcached存储Session？
* 答：如果用memcached存储Session，那么当memcached集群发生故障（比如内存溢出）或者维护（比如升级、增加或减少服务器）时，用户会无法登录，或者被踢掉线；memcached的回收机制可能会导致用户无缘无故地掉线。详见 http://www.infoq.com/cn/news/2015/01/memcached-store-session




###2.4 Docker安装
