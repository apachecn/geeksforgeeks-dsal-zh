# 检查字符串是否相互旋转的 Php 程序

> 原文:[https://www . geesforgeks . org/PHP-程序检查字符串是否相互旋转/](https://www.geeksforgeeks.org/php-program-to-check-if-strings-are-rotations-of-each-other-or-not/)

给定一个字符串 s1 和一个字符串 s2，写一个片段来说明 s2 是否是 s1 的旋转？
(如给定 s1 = ABCD，s2 = CDAB，返回真，给定 s1 = ABCD，s2 = ACBD，返回假)

 **算法:**旋转(str1，str2)

```
    1\. Create a temp string and store concatenation of str1 to
       str1 in temp.
                          temp = str1.str1
    2\. If str2 is a substring of temp then str1 and str2 are 
       rotations of each other.

    Example:                 
                     str1 = "ABACD"
                     str2 = "CDABA"

     temp = str1.str1 = "ABACDABACD"
     Since str2 is a substring of temp, str1 and str2 are 
     rotations of each other.

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to check if 
// two given strings are 
// rotations of each other

/* Function checks if passed 
strings (str1 and str2) are 
rotations of each other */
function areRotations($str1, $str2)
{
/* Check if sizes of two
   strings are same */
if (strlen($str1) != strlen($str2))
{
        return false;
}

$temp = $str1 + $str1; 
if ($temp.count($str2)> 0)
{
        return true;
}
else
{
    return false;
}
}

// Driver code
$str1 = "AACD";
$str2 = "ACDA";
if (areRotations($str1, $str2))
{
    echo "Strings are rotations ". 
                  "of each other";
}
else
{
    echo "Strings are not " . 
         "rotations of each other" ;
}

// This code is contributed
// by Shivi_Aggarwal.
?>
```

**Output:**

```
Strings are rotations of each other
```

**使用的库函数:**
strtr:
strtr 在字符串中查找子字符串。
原型:char * strtr(const char * S1，const char * S2)；
见[http://www.lix.polytechnique.fr/Labo/Leo.liberti/public/computing/Prog/C/C/MAN/strtr . htm](http://www.lix.polytechnique.fr/Labo/Leo.Liberti/public/computing/prog/c/C/MAN/strstr.htm)了解更多详情

strcat:
strcat 串联两个字符串
原型:char *strcat(char *dest，const char * src)；
见[http://www.lix.polytechnique.fr/Labo/Leo.更多详情请访问](http://www.lix.polytechnique.fr/Labo/Leo.Liberti/public/computing/prog/c/C/MAN/strcat.htm)

**时间复杂度:**这个问题的时间复杂度取决于 strstr 函数的实现。
如果使用 KMP 匹配器实现 strstr，那么上述程序的复杂度为(-)(n1 + n2)，其中 n1 和 n2 是字符串的长度。KMP 匹配器花费(-)(n)时间在长度为 n 的字符串中找到子字符串，其中假设子字符串的长度小于该字符串。
详情请参考 [A 程序查看琴弦是否相互旋转](https://www.geeksforgeeks.org/a-program-to-check-if-strings-are-rotations-of-each-other/)的完整文章！