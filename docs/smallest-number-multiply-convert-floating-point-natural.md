# 将浮点转换为自然数的最小乘法数

> 原文:[https://www . geesforgeks . org/minist-number-multiple-convert-floating-point-natural/](https://www.geeksforgeeks.org/smallest-number-multiply-convert-floating-point-natural/)

给定一个正浮点数 **n** ，任务是找到最小的整数 k，这样当我们用 n 乘 k 时，就得到一个自然数。
示例:

```
Input : 30.25
Output : 4
30.25 * 4 = 321, there is no number less than 4
which can convert 30.25 into natural number.

Input : 5.5
Output : 2
5.5 * 2 = 11, there is no number less than 2
which can convert 5.5 into natural number.

Input : 5.33
Output : 100
```

想法是把给定的浮点数转换成分数(不一定是简化形式)[求分子和分母的 GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。例如，如果输入的浮点数是 30.25，我们转换成分数为 3025/100。这可以很容易地通过找到点的位置来完成。
最后为了得到答案，我们把转换分数的分母除以分母和分子的 GCD。比如 3025 和 100 的 GCD 是 25。我们用 100 除以 25，得到的答案是 4。
以下是本办法的实施情况:

## C++

```
// C++ program to find the smallest number to multiply
// to convert a floating point number into natural number.
#include<bits/stdc++.h>
using namespace std;

// Finding GCD of two number
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a%b);
}

// Returns smallest integer k such that k * str becomes
// natural. str is an input floating point number
int findnum(string &str)
{
    // Find size of string representing a
    // floating point number.
    int n = str.length();

    // Below is used to find denominator in
    // fraction form.
    int count_after_dot = 0;

    // Used to find value of count_after_dot
    bool dot_seen = false;

    // To find numerator in fraction form of
    // given number. For example, for 30.25,
    // numerator would be 3025.
    int num = 0;
    for (int i = 0; i < n; i++)
    {
        if (str[i] != '.')
        {
            num = num*10 + (str[i] - '0');
            if (dot_seen == true)
                count_after_dot++;
        }
        else
            dot_seen = true;
    }

    // If there was no dot, then number
    // is already a natural.
    if (dot_seen == false)
    return 1;

    // Find denominator in fraction form. For example,
    // for 30.25, denominator is 100
    int dem = (int)pow(10, count_after_dot);

    // Result is denominator divided by
    // GCD-of-numerator-and-denominator. For example, for
    // 30.25, result is 100 / GCD(3025,100) = 100/25 = 4
    return (dem / gcd(num, dem));
}

// Driven Program
int main()
{
    string str = "5.125";
    cout << findnum(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest number to multiply
// to convert a floating point number into natural number.
class GFG {
  // Finding GCD of two number
  static int gcd(int a, int b) {
    if (b == 0)
      return a;
    return gcd(b, a % b);
  }

  // Returns smallest integer k such that k * str becomes
  // natural. str is an input floating point number
  static int findnum(String str) {
    // Find size of string representing a
    // floating point number.
    int n = str.length();

    // Below is used to find denominator in
    // fraction form.
    int count_after_dot = 0;

    // Used to find value of count_after_dot
    boolean dot_seen = false;

    // To find numerator in fraction form of
    // given number. For example, for 30.25,
    // numerator would be 3025.
    int num = 0;
    for (int i = 0; i < n; i++) {
      if (str.charAt(i) != '.') {
        num = num * 10 + (str.charAt(i) - '0');
        if (dot_seen == true)
          count_after_dot++;
      } else
        dot_seen = true;
    }

    // If there was no dot, then number
    // is already a natural.
    if (dot_seen == false)
      return 1;

    // Find denominator in fraction form. For example,
    // for 30.25, denominator is 100
    int dem = (int)Math.pow(10, count_after_dot);

    // Result is denominator divided by
    // GCD-of-numerator-and-denominator. For example, for
    // 30.25, result is 100 / GCD(3025, 100) = 100/25 = 4
    return (dem / gcd(num, dem));
  }

  // Driver code
  public static void main(String[] args) {
    String str = "5.125";
    System.out.print(findnum(str));
  }
}
// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to find the smallest number to multiply
# to convert a floating point number into natural number.
# Finding GCD of two number
import math
def gcd(a, b):

    if (b == 0):
        return a
    return gcd(b, a%b)

# Returns smallest integer k such that k * str becomes
# natural. str is an input floating point number
def findnum(str):

    # Find size of string representing a
    # floating point number.
    n = len(str)
    # Below is used to find denominator in
    # fraction form.
    count_after_dot = 0

    # Used to find value of count_after_dot
    dot_seen = 0

    # To find numerator in fraction form of
    # given number. For example, for 30.25,
    # numerator would be 3025.
    num = 0
    for i in range(n):
        if (str[i] != '.'):
            num = num*10 + int(str[i])
            if (dot_seen == 1):
                count_after_dot += 1
        else:
            dot_seen = 1

    # If there was no dot, then number
    # is already a natural.
    if (dot_seen == 0):
       return 1

    # Find denominator in fraction form. For example,
    # for 30.25, denominator is 100
    dem = int(math.pow(10, count_after_dot))

    # Result is denominator divided by
    # GCD-of-numerator-and-denominator. For example, for
    # 30.25, result is 100 / GCD(3025,100) = 100/25 = 4
    return (dem / gcd(num, dem))

# Driver Program

str = "5.125"
print findnum(str)

# Contributed by: Afzal Ansari
```

## C#

```
// C# program to find the smallest
// number to multiply to convert a
// floating point number into
// natural number.
using System;

class GFG {

// Finding GCD of two number
static int gcd(int a, int b)
{
    if (b == 0)
    return a;
    return gcd(b, a % b);
}

// Returns smallest integer k
// such that k * str becomes
// natural. str is an input
// floating point number
static int findnum(String str)
{

    // Find size of string representing
    // a floating point number.
    int n = str.Length;

    // Below is used to find denominator
    // in fraction form.
    int count_after_dot = 0;

    // Used to find value of count_after_dot
    bool dot_seen = false;

    // To find numerator in fraction form of
    // given number. For example, for 30.25,
    // numerator would be 3025.
    int num = 0;
    for (int i = 0; i < n; i++)
    {
        if (str[i] != '.')
        {
            num = num * 10 + (str[i] - '0');
            if (dot_seen == true)
            count_after_dot++;
        }
        else
            dot_seen = true;
    }

    // If there was no dot, then
    // number is already a natural.
    if (dot_seen == false)
    return 1;

    // Find denominator in fraction form.
    // For example, for 30.25,
    // denominator is 100
    int dem = (int)Math.Pow(10, count_after_dot);

    // Result is denominator divided by
    // GCD-of-numerator-and-denominator.
    // For example, for 30.25, result is
    // 100 / GCD(3025, 100) = 100/25 = 4
    return (dem / gcd(num, dem));
}

// Driver code
public static void Main()
{
    String str = "5.125";
    Console.Write(findnum(str));
}
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the smallest
// number to multiply to convert a
// floating point number into
// natural number.

// Finding GCD of two number
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return gcd($b, $a % $b);
}

// Returns smallest integer k
// such that k * str becomes
// natural. str is an input
// floating point number
function findnum( $str)
{

    // Find size of string
    // representing a floating
    // point number.
    $n = strlen($str);

    // Below is used to
    // find denominator in
    // fraction form.
    $count_after_dot = 0;

    // Used to find value
    // of count_after_dot
    $dot_seen = false;

    // To find numerator in
    // fraction form of
    // given number. For
    // example, for 30.25,
    // numerator would be 3025.
    $num = 0;
    for($i = 0; $i < $n; $i++)
    {
        if ($str[$i] != '.')
        {
            $num = $num*10 + ($str[$i] - '0');
            if ($dot_seen == true)
                $count_after_dot++;
        }
        else
            $dot_seen = true;
    }

    // If there was no dot,
    // then number is
    // already a natural.
    if ($dot_seen == false)
    return 1;

    // Find denominator in
    // fraction form. For
    // example, for 30.25,
    // denominator is 100
    $dem = pow(10, $count_after_dot);

    // Result is denominator
    // divided by GCD-of-
    // numerator-and-denominator.
    // For example, for 30.25,
    // result is 100 / GCD(3025,100)
    // = 100/25 = 4
    return ($dem / gcd($num, $dem));
}

// Driver Code
{
    $str = "5.125";
    echo findnum($str) ;
    return 0;
}

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
// javascript program to find the smallest number to multiply
// to convert a floating point number into natural number.

    // Finding GCD of two number
    function gcd(a , b) {
        if (b == 0)
            return a;
        return gcd(b, a % b);
    }

    // Returns smallest integer k such that k * str becomes
    // natural. str is an input floating point number
    function findnum( str)
    {

        // Find size of string representing a
        // floating point number.
        var n = str.length;

        // Below is used to find denominator in
        // fraction form.
        var count_after_dot = 0;

        // Used to find value of count_after_dot
        let dot_seen = false;

        // To find numerator in fraction form of
        // given number. For example, for 30.25,
        // numerator would be 3025.
        var num = 0;
        for (i = 0; i < n; i++) {
            if (str.charAt(i) != '.') {
                num = num * 10 + (str.charAt(i) - '0');
                if (dot_seen == true)
                    count_after_dot++;
            } else
                dot_seen = true;
        }

        // If there was no dot, then number
        // is already a natural.
        if (dot_seen == false)
            return 1;

        // Find denominator in fraction form. For example,
        // for 30.25, denominator is 100
        var dem = parseInt( Math.pow(10, count_after_dot));

        // Result is denominator divided by
        // GCD-of-numerator-and-denominator. For example, for
        // 30.25, result is 100 / GCD(3025, 100) = 100/25 = 4
        return (dem / gcd(num, dem));
    }

    // Driver code   
    let str = "5.125";
    document.write(findnum(str));

// This code is contributed by todaysgaurav
</script>
```

输出:

```
8
```

本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。