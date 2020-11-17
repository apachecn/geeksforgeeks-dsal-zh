# 使用 PHP 生成随机字符串

> 原文：[https://www.geeksforgeeks.org/generating-random-string-using-php/](https://www.geeksforgeeks.org/generating-random-string-using-php/)

使用 PHP 生成一个随机的，唯一的字母数字字符串。

例子：

```
EA070
aBX32gTf

```

**方法 1：暴力**

第一种方法是最容易理解的方法，因此也是暴力。

可以通过以下方式实现：

*   将所有可能的字母存储到字符串中。

*   生成从 0 到字符串`length-1`的随机索引。

*   在打印该索引处的字母。

*   执行此步骤`n`次（其中`n`是所需字符串的长度）。

**程序**：

```
<?php
$n =10;
function getName( $n ) {
$characters = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ' ;
$randomString = '' ;
for ( $i = 0; $i < $n ; $i ++) {
$index = rand(0, strlen ( $characters ) - 1);
$randomString .= $characters [ $index ];
}
return $randomString ;
}
echo [ getName( $n );
?>
```

输出 1：

```
3HDrSOvRIs

```

输出 2：

```
lipHh

```

**方法 2：使用哈希函数**

PHP 具有一些函数，如`md5()`，`sha1()`和`hash()`，可用于基于某些算法（例如`sha1`，`sha256`，`md5`等）对字符串进行哈希处理。所有这些函数都将字符串作为参数并输出字母数字哈希字符串。

要了解有关这些功能更多信息，[请单击此处](https://www.geeksforgeeks.org/php-md5-sha1-hash-functions/)。

一旦我们了解了如何利用这些功能，我们的任务就会变得非常简单。

*   使用`rand()`函数生成一个随机数。

*   使用以上函数之一对其进行哈希处理。

**程序 1**：

```
<?php
$str =rand();
$result = md5( $str );
echo $result ;
?>
```

输出 1：

```
2e437510c181dd2ae100fc1661a445d4

```

输出 2：

```
256394010059991a71ea05e5d859d2be

```

**程序 2**：

```
<?php
$str =rand();
$result = sha1( $str );
echo $result ;
?>
```

输出 1：

```
6eadd9b2c4389d9b109b3b869f66aab5d8f9420a

```

输出 2：

```
ca2d3c0993ab87e842d0a7a01f319aca6c587a87

```

**程序 3**：

```
<?php
$str = rand();
$result = hash( "sha256" , $str );
echo $result ;
?>
```

输出 1：

```
2a41cbc8cc11f8c8d0eb54210fe524748b4def1c5b04fcf18c2d5972e24d11c2

```

输出 2：

```
291144c1cbba4de0bf199d37ee265ac95cc2e44e80fd2642b22a6e8ef2f42a39

```

**注意**：上述所有函数都是哈希函数，因此生成的字符串的长度将始终取决于所使用的算法，但对于算法，它将始终保持恒定。 因此，如果要生成固定长度的字符串，则可以根据需要截断生成的字符串或与另一个字符串连接。

**方法 3**：使用`uniqid()`函数。

PHP 中的[`uniqid()`](https://www.geeksforgeeks.org/php-uniqid-function/)函数是一个内置函数，用于基于微秒（微秒）的当前时间生成唯一 ID。 默认情况下，它返回一个 13 个字符长的唯一字符串。

**程序**：

```
<?php
$result = uniqid();
echo $result ;
?>
```

输出 1：

```
5bdd0b74e9a6c 

```

输出 2：

```
5bdd0bbc200c4   

```

**注意**：所有上述方法都是基于`rand()`和`uniqid()`函数构建的。 这些函数不是加密安全的随机生成器。 因此建议，如果随机性程度影响应用程序的安全性，则应避免使用这些方法。

**方法 4**：使用`random_bytes()`函数。 （加密安全）

[`random_bytes()`](https://www.geeksforgeeks.org/php-random_bytes-function/)函数生成加密安全的伪随机字节，稍后可使用[`bin2hex()`](https://www.geeksforgeeks.org/php-bin2hex-function/)函数将其转换为十六进制格式。

**程序**：

```
<?php
$n = 20;
$result = bin2hex(random_bytes( $n ));
echo $result ;
?>
```

输出 1：

```
235aed08a01468f90fa726bd56319fb893967da8 

```

输出 2：

```
508b84494cdf31bec01566d12a924c75d4baed39 

```



* * *

* * *



