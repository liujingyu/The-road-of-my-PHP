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


中国镜像配置修改:

有两种方式启用本镜像服务：

系统全局配置： 即将配置信息添加到 Composer 的全局配置文件 config.json 中。见“例1”
单个项目配置： 将配置信息添加到某个项目的 composer.json 文件中。见“例2”

例1：修改 composer 的全局配置文件（推荐方式）

打开命令行窗口（windows用户）或控制台（Linux、Mac 用户）并执行如下命令：

```
composer config -g repo.packagist composer http://packagist.phpcomposer.com
```

例2：修改当前项目的 composer.json 配置文件：

打开命令行窗口（windows用户）或控制台（Linux、Mac 用户），进入你的项目的根目录（也就是 composer.json 文件所在目录），执行如下命令：

```
composer config repo.packagist composer http://packagist.phpcomposer.com
```
上述命令将会在当前项目中的 composer.json 文件的末尾自动添加镜像的配置信息（你也可以自己手工添加）：

```
"repositories": {
    "packagist": {
        "type": "composer",
        "url": "http://packagist.phpcomposer.com"
    }
}
```

以 laravel 项目的 composer.json 配置文件为例，执行上述命令后如下所示（注意最后几行）：

```
{
    "name": "laravel/laravel",
        "description": "The Laravel Framework.",
        "keywords": ["framework", "laravel"],
        "license": "MIT",
        "type": "project",
        "require": {
            "php": ">=5.5.9",
            "laravel/framework": "5.2.*"
        },
        "require-dev": {
            "fzaninotto/faker": "~1.4",
            "mockery/mockery": "0.9.*",
            "phpunit/phpunit": "~4.0",
            "symfony/css-selector": "2.8.*|3.0.*",
            "symfony/dom-crawler": "2.8.*|3.0.*"
        },
        "autoload": {
            "classmap": [
                "database"
            ],
            "psr-4": {
                "App\\": "app/"
            }
        },
        "autoload-dev": {
            "classmap": [
                "tests/TestCase.php"
            ]
        },
        "scripts": {
            "post-root-package-install": [
                "php -r \"copy('.env.example', '.env');\""
            ],
            "post-create-project-cmd": [
                "php artisan key:generate"
            ],
            "post-install-cmd": [
                "php artisan clear-compiled",
            "php artisan optimize"
            ],
            "pre-update-cmd": [
                "php artisan clear-compiled"
            ],
            "post-update-cmd": [
                "php artisan optimize"
            ]
        },
        "config": {
            "preferred-install": "dist"
        },
        "repositories": {
            "packagist": {
                "type": "composer",
                "url": "http://packagist.phpcomposer.com"
            }
        }
}
```
OK，一切搞定！试一下 composer install 来体验飞一般的速度吧！

依赖管理

Composer 不是一个包管理器。是的，它涉及 "packages" 和 "libraries"，但它在每个项目的基础上进行管理，在你项目的某个目录中（例如 vendor）进行安装。默认情况下它不会在全局安装任何东西。因此，这仅仅是一个依赖管理。

这种想法并不新鲜，Composer 受到了 node's npm 和 ruby's bundler 的强烈启发。而当时 PHP 下并没有类似的工具。

Composer 将这样为你解决问题：

a) 你有一个项目依赖于若干个库。

b) 其中一些库依赖于其他库。

c) 你声明你所依赖的东西。

d) Composer 会找出哪个版本的包需要安装，并安装它们（将它们下载到你的项目中）


##2. Pear

