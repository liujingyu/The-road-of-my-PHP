#[第三章 PHP编写中的技巧](https://github.com/liujingyu/The-road-of-my-PHP/blob/master/Book-3.md)

##1. 字符串技巧

##2. 数组技巧

- array_column 返回数组中指定的一列

array array_column(array $input , mixed $column_key [, mixed $index_key ])

array_column() 返回input数组中键值为column_key的列， 如果指定了可选参数index_key，那么input数组中的这一列的值将作为返回数组中对应值的键。

Example #1 从结果集中取出first names列:

```
<?php
// Array representing a possible record set returned from a database
$records = array(
    array(
        'id' => 2135,
        'first_name' => 'John',
        'last_name' => 'Doe',
    ),
    array(
        'id' => 3245,
        'first_name' => 'Sally',
        'last_name' => 'Smith',
    ),
    array(
        'id' => 5342,
        'first_name' => 'Jane',
        'last_name' => 'Jones',
    ),
    array(
        'id' => 5623,
        'first_name' => 'Peter',
        'last_name' => 'Doe',
    )
);

$first_names = array_column($records, 'first_name');
print_r($first_names);
?>

```
以上例程会输出：

```
Array
(
    [0] => John
    [1] => Sally
    [2] => Jane
    [3] => Peter
)
```

Example #2 从结果集中总取出last names列，用相应的id作为键值

```
<?php
// Using the $records array from Example #1
$last_names = array_column($records, 'last_name', 'id');
print_r($last_names);
?>
```
以上例程会输出：

```
Array
(
    [2135] => Doe
    [3245] => Smith
    [5342] => Jones
    [5623] => Doe
)
```

more: http://php.net/manual/zh/function.array-column.php

- array_unique vs array_flip vs array_keys

```
<?php

$test = array();
for ($run = 0; $run < 1000; ++$run) {
    $test[] = rand(0, 100);
}

$time = microtime(true);

for ($run = 0; $run < 100; ++$run) {
    $out = array_unique($test);
}

$time = microtime(true) - $time;
echo 'Array Unique: '.$time."\n";

$time = microtime(true);

for ($run = 0; $run < 100; ++$run) {
    $out = array_keys(array_flip($test));
}

$time = microtime(true) - $time;
echo 'Keys Flip: '.$time."\n";

$time = microtime(true);

for ($run = 0; $run < 100; ++$run) {
    $out = array_flip(array_flip($test));
}

$time = microtime(true) - $time;
echo 'Flip Flip: '.$time."\n";

```
运行结果:

```
Array Unique: 0.20008397102356
Keys Flip: 0.0058798789978027
Flip Flip: 0.0052719116210938
```


##3. 编写技巧

- 去掉else

```
if (isset($shopIds[$goods_id]) {
    $open = true;
} else {
    $open = false;
}
```

可改为：
```
$open = false;
if (isset($shopIds[$goods_id]) {
    $open = true;
}

```

复杂的else例子

```
public function addThreeInts($first, $second, $third) {
    if (is_int($first)) {
        if (is_int($second)) {
            if (is_int($third)) {
                $sum = $first + $second + $third;
            } else {
                return null;
            }
        } else {
            return null;
        }
    } else {
        return null;
    }

    return $sum;
}
```
改为

```
public function addThreeInts($first, $second, $third) {
    if (!is_int($first)) {
        return null;
    }

    if (!is_int($second)) {
        return null;
    }

    if (!is_int($third)) {
        return null;
    }

    return $first + $second + $third;
}
```


- 表驱动法(一种编程模式)

获取日期的对应中文星期吧

```
<?php
date_default_timezone_set('PRC');

#当前日期索引
$index = (int)date('w');

#日期查询表
$week = ['周日', '周一', '周二', '周三', '周四', '周五', '周六'];

#表驱动法
echo $week[$index].PHP_EOL;

#if
if ($index === 0) {
    echo '周日';
} elseif ($index === 1) {
    echo '周一';
} elseif ($index === 2) {
    echo '周二';
} elseif ($index === 3) {
    echo '周三';
} elseif ($index === 4) {
    echo '周四';
} elseif ($index === 5) {
    echo '周五';
} elseif ($index === 6) {
    echo '周六';
}
```
1、使用表驱动法的两个问题

怎样从表中查询信息
直接访问
索引访问
阶梯访问
应该在表里面存些什么
数据
描述动作的代码
对实现动作的子程序的引用
2、直接访问表

直接访问表代替了更为复杂的逻辑控制结构。无需绕圈子就能直接在表里面找到想要的信息。

构造查询键值的方法：

复制信息从而能够直接使用键值
转换键值以使其能够直接使用
把键值转换提取成独立子程序
3、索引访问表

有点时候，只用一个简单的数学运算还无法把数据转换成表键值，这类情况的一部分可以通过使用索引访问的方法。索引表不是直接访问，而是经过居间的索引去访问。

索引访问技术的优点：

如果主查询表中的每一条记录都很大，那么创建一个浪费了很多空间的索引数组所用的空间，要比创建一个浪费了很多空间的主查询所有的空间要小得多
即使用了索引后没有节省内存空间，操作位于索引中的记录也要比操作位于主表中的记录更方便廉价
表查询技术在可维护性上具有的普遍优点，编写到表里面的数据比嵌入代码中的数据更容易维护
4、阶梯访问表

阶梯结构的基本想法是表中的记录对于不同的数据范围有效，而不是对不同的数据点有效。这种方法不像索引结构直接，但是要比索引访问节省空间。

使用阶梯技术时要注意的细节：

留心断点
确认循环能在找出最高一级的区间之后恰当的终止，同时确保正确地处理了两边的边界
考虑使用二分法查找取代顺序查找
阶梯访问大列表时顺序查找可能会比较耗时，可以采用二分的方法来提高效率
考虑用索引访问来取代阶梯技术
阶梯方法中的查找操作可能会比较耗时，如果执行速度更重要，可以考虑使用索引访问取代阶梯访问。


