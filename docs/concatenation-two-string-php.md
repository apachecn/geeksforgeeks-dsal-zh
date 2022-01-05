# PHP 中两个字符串的串联

> 原文:[https://www.geeksforgeeks.org/concatenation-two-string-php/](https://www.geeksforgeeks.org/concatenation-two-string-php/)

有两个字符串运算符。第一个是串联运算符('**)。**')，返回其左右参数的串联。第二个是串联赋值运算符(' T2 ')。= ')，它将右侧的参数追加到左侧的参数中。

示例:

```
Input : string1:  Hello
        string2 : World! 
Output : HelloWorld!

Input : string1: geeksfor
        string2: geeks
Output : geeksforgeeks

```

**代码#1:**

```
<?php

// First String
$a = 'Hello';

// Second String
$b = 'World!';

// Concatenation Of String
$c = $a.$b;

// print Concatenate String
echo " $c \n";
?>
```

输出:

```
 HelloWorld!

```

**代码#2 :**

```
<?php

// First String
$fname = 'John';

// Second String
$lname = 'Carter!';

// Concatenation Of String
$c = $fname." ".$lname;

// print Concatenate String
echo " $c \n";
?>
```

输出:

```
John Carter!
```

**代码#3 :**

```
<?php

// First String
$a = 'Hello';

// now $a contains "HelloWorld!"
$a. = "World!";

// Print The String $a
echo " $a \n";
?>
```

输出:

```
 HelloWorld!

```

PHP 是一种专门为 web 开发设计的服务器端脚本语言。您可以通过以下 [PHP 教程](https://www.geeksforgeeks.org/php-tutorials/)和 [PHP 示例](https://www.geeksforgeeks.org/php-examples/)从头开始学习 PHP。