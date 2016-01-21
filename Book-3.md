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
