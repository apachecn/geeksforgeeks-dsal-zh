# 字符串字符的字母值之和

> 原文:[https://www . geesforgeks . org/字符串字符的字母值总和/](https://www.geeksforgeeks.org/sum-of-the-alphabetical-values-of-the-characters-of-a-string/)

给你一个字符串数组 *str* ，任务是从数组中找到给定字符串 *s* 的分数。字符串的分数被定义为其字符的字母值之和与字符串在数组中的位置的乘积。
**例:**

> **输入:**str[]= {“sahil”、“shashanak”、“sanjit”、“abhinav”、“mohit”}，s = "abhinav"
> **输出:**228
> abhinav " = 1+2+8+9+14+1+22 = 57
> str 中“abhinav”的位置为 4，57 x 4 = 228
> **输入:**str[]= {“geeksfs”

**进场:**

*   在数组中找到给定的字符串并存储该字符串的位置。
*   然后计算给定字符串的字母值之和。
*   将字符串在给定数组中的位置乘以上一步计算的值，并打印结果。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find string score
int strScore(string str[], string s, int n)
{
    int score = 0, index;
    for (int i = 0; i < n; i++) {
        if (str[i] == s) {
            for (int j = 0; j < s.length(); j++)
                score += s[j] - 'a' + 1;
            index = i + 1;
            break;
        }
    }

    score = score * index;
    return score;
}

// Driver code
int main()
{
    string str[] = { "sahil", "shashanak"
                      , "sanjit", "abhinav", "mohit" };
    string s = "abhinav";
    int n = sizeof(str) / sizeof(str[0]);
    int score = strScore(str, s, n);
    cout << score << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  Java implementation of the approach
import java.io.*;

class GFG {

// Function to find string score
static int strScore(String str[], String s, int n)
{
    int score = 0, index=0;
    for (int i = 0; i < n; i++) {
        if (str[i] == s) {
            for (int j = 0; j < s.length(); j++)
                score += s.charAt(j) - 'a' + 1;
            index = i + 1;
            break;
        }
    }

    score = score * index;
    return score;
}

// Driver code

    public static void main (String[] args) {
            String str[] = { "sahil", "shashanak"
                    , "sanjit", "abhinav", "mohit" };
    String s = "abhinav";
    int n = str.length;
    int score = strScore(str, s, n);
    System.out.println( score);
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach
# Function to find string score
def strScore(str, s, n):
    score = 0
    index = 0
    for i in range(n):
        if (str[i] == s):
            for j in range(len(s)):
                score += (ord(s[j]) -
                          ord('a') + 1)
            index = i + 1
            break
    score = score * index
    return score

# Driver code
str = ["sahil", "shashanak", "sanjit",
                  "abhinav", "mohit" ]
s = "abhinav"
n = len(str)
score = strScore(str, s, n);
print(score)

# This code is contributed
# by sahishelangia
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find string score
static int strScore(String []str,
                    String s, int n)
{
    int score = 0, index = 0;
    for (int i = 0; i < n; i++)
    {
        if (str[i] == s)
        {
            for (int j = 0; j < s.Length; j++)
                score += s[j] - 'a' + 1;
            index = i + 1;
            break;
        }
    }

    score = score * index;
    return score;
}

// Driver code
public static void Main (String[] args)
{
    String []str = { "sahil", "shashanak", "sanjit",
                     "abhinav", "mohit" };
    String s = "abhinav";
    int n = str.Length;
    int score = strScore(str, s, n);
    Console.Write( score);
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Function to find string score
function strScore($str, $s, $n)
{
    $score = 0;
    $index;
    for ($i = 0; $i < $n; $i++)
    {
        if ($str[$i] == $s)
        {
            for ($j = 0; $j < strlen($s); $j++)
                $score += (ord($s[$j]) - ord('a')) + 1;
            $index = ($i + 1);
            break;
        }
    }

    $score = $score * $index;
    return $score;
}

// Driver code
$str = array( "sahil", "shashanak",
              "sanjit", "abhinav", "mohit" );
$s = "abhinav";
$n = sizeof($str);
$score = strScore($str, $s, $n);
echo $score, "\n";

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

 //  javascript implementation of the approach

// Function to find string score
function strScore(str, s , n)
{
    var score = 0, index=0;
    for (i = 0; i < n; i++) {
        if (str[i] == s) {
            for (j = 0; j < s.length; j++){

                score += s.charAt(j).charCodeAt(0) - ('a').charCodeAt(0) + 1;
                }
            index = i + 1;
            break;
        }
    }

    score = score * index;
    return score;
}

// Driver code
str = [ "sahil", "shashanak"
                    , "sanjit", "abhinav", "mohit" ];
    s = "abhinav";
    var n = str.length;
    var score = strScore(str, s, n);
    document.write( score);

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
228
```