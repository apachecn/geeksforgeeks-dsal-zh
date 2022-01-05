# PHP | ereg_replace()函数

> 原文:[https://www.geeksforgeeks.org/php-ereg_replace-function/](https://www.geeksforgeeks.org/php-ereg_replace-function/)

*ereg_replace()* 是 PHP 中的一个内置函数，用于搜索其他字符串中的字符串模式。如果在原始字符串中找到模式，那么它将用替换字符串替换匹配的文本。关于使用正则表达式进行模式匹配的基本理解，可以参考[正则表达式](https://www.geeksforgeeks.org/write-regular-expressions/)一文。

**语法:**

```
*string* ereg_replace ( $string_pattern, $replace_string,  $original_string )

```

**使用的参数:**该功能接受三个强制参数，所有这些参数描述如下。

*   ***$ string _ pattern* :** This parameter specifies the pattern to be searched in $original_string. It can be used for both array types and string types with parentheses.
*   ***$ replace _ string* :** This parameter specifies the string whose matching text will be replaced. It can be used for array and string types. Replace the substring in the form of \ number, which replaces the text with parenthesis substring that matches the number, \0 generates the whole content string.
*   ***$ origin _ string* :** This parameter specifies the input string, which can be of array type or string type.

**返回值:**如果找到匹配项，该函数返回修改后的字符串或数组。如果与原始字符串中的 fount 不匹配，则它将返回未更改的原始字符串或数组。

**注意:**的 *ereg_replace()* 功能在 PHP 中是*区分大小写的*。这个功能在 PHP 5.3.0 中被*弃用*，在 PHP 7.0.0 中*去掉了*。

示例:

```
Input: $original_string = "Geeksforgeeks PHP article."; 
       $string_pattern = "(.*)PHP(.*)"; 
       $replace_string = " You should read \\1all\\2"; 
Output: You should read Geeksforgeeks all article.
Explanation: Within the parenthesis "\1" and "\2" to access
             the part of string and replace with 'PHP' to 'all'.

Input: $original_string = "Geeksforgeeks is no:one computer 
                                             science portal.";
       $replace_string = '1'; 
       $original_string = ereg_replace('one', $replace_string,
                                             $original_string);
Output: Geeksforgeeks is no:1 computer science portal. 

```

以下程序说明了 *ereg_replace()* 功能。

**节目 1:**

```
<?php 

// Original input string 
$original_string = "Write any topic .";

// Pattern to be searched
$string_pattern = "(.*)any(.*)"; 

// Replace string
$replace_string = " own yours own \\1biography\\2"; 

echo ereg_replace($patternstrVal, $replacesstrVal, $stringVal); 

?>
```

输出:

```
Write own yours own biography topic.

```

**注意:**当使用整数值作为替换参数时，我们没有得到预期的结果，因为函数将数字解释为字符的序数。

**节目 2:**

```
<?php 

// Original input string 
$original_string = "India To Become World's Fifth
                        Largest Economy In 2018.";

// Replace string
$replace_string = 5; 

// This function call will not show the expected output as the
// function interpret the number to ordinal value of character.
echo ereg_replace('Fifth',$replace_string, $original_string);

$original_string = "India To Become World's Fifth
                         Largest Economy In 2018.";

// Replace String
$replace_string = '5'; 

// This function call will show 
// the correct expected output
echo ereg_replace('Fifth',$replace_string, $original_string);

?> 
```

输出:

```
India To Become World's  Largest Economy In 2018.
India To Become World's 5 Largest Economy In 2018.

```

**参考**:[http://php.net/manual/en/function.ereg-replace.php](http://php.net/manual/en/function.ereg-replace.php)