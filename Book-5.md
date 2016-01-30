#[第五章 PHP包管理器](https://github.com/liujingyu/The-road-of-my-PHP/blob/master/Book-5.md)

##1. Composer
Composer是 PHP 用来管理依赖（dependency）关系的工具。你可以在自己的项目中声明所依赖的外部工具库（libraries），Composer 会帮你安装这些依赖的库文件。

Composer install 背后到底是怎么运作的？
![运行图](http://image.phpcomposer.com/3/06/71554febd8a45c1aed1ba3b0aaf0d.png)

Composer 就是我们安装在自己系统上的 composer 工具。所有 package 元数据和 zip 文件的下载、安装工作都是它帮我们完成的。

从图上我们可以看到，不管是 Packagist.org 还是 Github.com 出现故障或者被墙，我们都无法正常安装 package，即便能安装的时候，也是龟速。

说到这里，我们看到如果要做镜像的话，单是为 Packagist.org 做镜像显然是不够的，因为它存放的是所有 package 的元数据，真正安装包还在 Github.com 上面呢。所以“全量镜像”就必须将 Packagist.org 和 Github.com 全部镜像才可以。具体到我们的实现来说，就是将 Packagist.org 上的元数据和 Github.com 上面的 zip 包镜像到国内。

由于墙的原因：需要使用Composer镜像.又拍云提供.
![运行图](http://image.phpcomposer.com/a/9e/913f6809905d56039602d7fb34e27.png)


##2. Pear

