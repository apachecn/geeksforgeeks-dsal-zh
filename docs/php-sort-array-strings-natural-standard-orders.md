# PHP |以自然和标准顺序对字符串数组进行排序

> 原文:[https://www . geesforgeks . org/PHP-sort-array-strings-natural-standard-orders/](https://www.geeksforgeeks.org/php-sort-array-strings-natural-standard-orders/)

给你一个字符串数组。您必须以标准方式(字母大小写很重要)和自然方式(字母大小写无关紧要)对给定的数组进行排序。

```
Input : arr[] = {"Geeks", "for", "geeks"}
Output : Standard sorting: Geeks for geeks 
         Natural sorting: for Geeks geeks 

Input : arr[] = {"Code", "at", "geeks", "Practice"}
Output : Standard sorting: Code Practice at geeks 
         Natural sorting: at Code geeks Practice 

```

如果您试图以简单的方式对字符串数组进行排序，您可以简单地创建一个用于字符比较的比较函数，并对给定的字符串数组进行排序。但这将区分小写字母和大写字母。要解决这个问题，如果你想在 c/java 中解决这个问题，你必须编写自己的比较函数，专门处理字母的情况。但是如果我们选择 PHP 作为我们的语言，那么我们可以在 natcasesort()的帮助下直接对它进行排序。
natcasesort():它对字符串进行排序，而不管它们的大小写。意思是“A”&“A”在这种排序方法中被视为小于“B”&“B”。

```
// declare array
$arr = array ("Hello", "to", "geeks", "for", "GEEks");

// Standard sort
$standard_result = sort($arr);
print_r($standart_result);

// natural sort
$natural_result = natcasesort($arr);
print_r($natural_result);

```

```
<?php
// PHP program to sort an array 
// in standard and natural ways.

// function to print array
function printArray ($arr)
{
    foreach ($arr as $value) {
        echo "$value ";
    }
}

// declare array
$arr = array ("Hello", "to", "geeks", "for", "GEEks");

// Standard sort
$standard_result = $arr;
sort($standard_result);
echo "Array after Standard sorting: ";
printArray($standard_result);

// natural sort
$natural_result = $arr;
natcasesort($natural_result);
echo "\nArray after Natural sorting: ";
printArray($natural_result);
?>
```

输出:

```
Array after Standard sorting: GEEks Hello for geeks to 
Array after Natural sorting: for geeks GEEks Hello to 

```