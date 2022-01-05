# 计算给定数字 N 中除以 N 的数字

> 原文:[https://www . geesforgeks . org/count-digits-给定-number-n-divide-n/](https://www.geeksforgeeks.org/count-digits-given-number-n-divide-n/)

给定一个可能是 10^5 位数的数字 n，任务是计算 n 中除以 n 的所有位数。不允许除以 0。如果 N 中任何重复的数字除以 N，那么该数字的所有重复都应该被计数，即 N = 122324，这里 2 除以 N，它出现 3 次。所以数字 2 的计数是 3。
**例:**

```
Input  : N = "35"
Output : 1
There are two digits in N and 1 of them
(5)divides it.

Input  : N = "122324"
Output : 5
N is divisible by 1, 2 and 4
```

**对于存储为字符串的大 N，如何检查一个数字的可除性？**
思想是利用 mod 运算的分配性质。
(x+y)%a = ((x%a) + (y%a)) % a.

```
// This function returns true if digit divides N, 
// else false
bool divisible(string N, int digit)
{
    int ans = 0;
    for (int i = 0; i < N.length(); i++)
    {     
        // (N[i]-'0') gives the digit value and
        // form the number       
        ans  = (ans*10 + (N[i]-'0'));

        // We use distributive property of mod here. 
        ans %= digit;
    }
    return (ans == 0);
}
```

这个问题的一个**简单解决方案**是读取字符串形式的数字，并逐个检查 N 中出现的每个数字的可除性。这种方法的时间复杂度为 O(N <sup>2</sup> )。
这个问题的有效解决方案**是使用一个额外的大小为 10 的数组 divide【】。因为我们只有 10 个数字，所以运行一个从 1 到 9 的循环，并检查从 1 到 9 的每个数字的可除性。如果任一数字除 N，则在数字处的**除[]** 数组中标记**为真**作为索引。如果当前数字 I 的除数[i]为真，现在遍历数字串并增加结果**

## C++

```
// C++ program to find number of digits in N that
// divide N.
#include<bits/stdc++.h>
using namespace std;

// Utility function to check divisibility by digit
bool divisible(string N, int digit)
{
    int ans = 0;
    for (int i = 0; i < N.length(); i++)
    {
        // (N[i]-'0') gives the digit value and
        // form the number
        ans  = (ans*10 + (N[i]-'0'));
        ans %= digit;
    }
    return (ans == 0);
}

// Function to count digits which appears in N and
// divide N
// divide[10]  --> array which tells that particular
//                 digit divides N or not
// count[10]   --> counts frequency of digits which
//                 divide N
int allDigits(string N)
{
    // We initialize all digits of N as not divisible
    // by N.
    bool divide[10] = {false};
    divide[1] = true;  // 1 divides all numbers

    // start checking divisibility of N by digits 2 to 9
    for (int digit=2; digit<=9; digit++)
    {
        // if digit divides N then mark it as true
        if (divisible(N, digit))
            divide[digit] = true;
    }

    // Now traverse the number string to find and increment
    // result whenever a digit divides N.
    int result = 0;
    for (int i=0; i<N.length(); i++)
    {
        if (divide[N[i]-'0'] == true)
            result++;
    }

    return result;
}

// Driver program to run the case
int main()
{
    string N = "122324";
    cout << allDigits(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of digits in N that
// divide N.
import java.util.*;

class solution
{

// Utility function to check divisibility by digit
static boolean divisible(String N, int digit)
{
    int ans = 0;
    for (int i = 0; i < N.length(); i++)
    {
        // (N[i]-'0') gives the digit value and
        // form the number
        ans = (ans*10 + (N.charAt(i)-'0'));
        ans %= digit;
    }
    return (ans == 0);
}

// Function to count digits which appears in N and
// divide N
// divide[10] --> array which tells that particular
//                 digit divides N or not
// count[10] --> counts frequency of digits which
//                 divide N
static int allDigits(String N)
{
    // We initialize all digits of N as not divisible
    // by N.
    Boolean[] divide = new Boolean[10];
    Arrays.fill(divide, Boolean.FALSE);
    divide[1] = true; // 1 divides all numbers

    // start checking divisibility of N by digits 2 to 9
    for (int digit=2; digit<=9; digit++)
    {
        // if digit divides N then mark it as true
        if (divisible(N, digit))
            divide[digit] = true;
    }

    // Now traverse the number string to find and increment
    // result whenever a digit divides N.
    int result = 0;
    for (int i=0; i<N.length(); i++)
    {
        if (divide[N.charAt(i)-'0'] == true)
            result++;
    }

    return result;
}

// Driver program to run the case
public static void main(String args[])
{
    String N = "122324";
    System.out.println(allDigits(N));
}

}
// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to find number of
# digits in N that divide N.

# Utility function to check
# divisibility by digit
def divisible(N, digit):

    ans = 0;
    for i in range(len(N)):
        # (N[i]-'0') gives the digit
        # value and form the number
        ans = (ans * 10 + (ord(N[i]) - ord('0')));
        ans %= digit;
    return (ans == 0);

# Function to count digits which
# appears in N and divide N
# divide[10] --> array which tells
# that particular digit divides N or not
# count[10] --> counts frequency of
#                 digits which divide N
def allDigits(N):

    # We initialize all digits of N
    # as not divisible by N.
    divide =[False]*10;
    divide[1] = True; # 1 divides all numbers

    # start checking divisibility of
    # N by digits 2 to 9
    for digit in range(2,10):
        # if digit divides N then
        # mark it as true
        if (divisible(N, digit)):
            divide[digit] = True;

    # Now traverse the number string to
    # find and increment result whenever
    # a digit divides N.
    result = 0;
    for i in range(len(N)):

        if (divide[(ord(N[i]) - ord('0'))] == True):
            result+=1;

    return result;

# Driver Code
N = "122324";
print(allDigits(N));

# This code is contributed by mits
```

## C#

```
// C# program to find number of digits
// in N that divide N.
using System;

class GFG {

// Utility function to
// check divisibility by digit
static bool divisible(string N, int digit)
{
    int ans = 0;
    for (int i = 0; i < N.Length; i++)
    {

        // (N[i]-'0') gives the digit value and
        // form the number
        ans = (ans * 10 + (N[i] - '0'));
        ans %= digit;
    }
    return (ans == 0);
}

// Function to count digits which
// appears in N and divide N
// divide[10] --> array which
// tells that particular
// digit divides N or not
// count[10] --> counts
// frequency of digits which
// divide N
static int allDigits(string N)
{

    // We initialize all digits
    // of N as not divisible by N
    bool[] divide = new bool[10];

    for (int i = 0; i < divide.Length; i++)
    {
        divide[i] = false;
    }

    // 1 divides all numbers
    divide[1] = true;

    // start checking divisibility
    // of N by digits 2 to 9
    for (int digit = 2; digit <= 9; digit++)
    {

        // if digit divides N
        // then mark it as true
        if (divisible(N, digit))
            divide[digit] = true;
    }

    // Now traverse the number
    // string to find and increment
    // result whenever a digit divides N.
    int result = 0;

    for (int i = 0; i < N.Length; i++)
    {
        if (divide[N[i] - '0'] == true)
            result++;
    }

    return result;
}

// Driver Code
public static void Main()
{
    string N = "122324";
    Console.Write(allDigits(N));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// digits in N that divide N.

// Utility function to check
// divisibility by digit
function divisible($N, $digit)
{
    $ans = 0;
    for ($i = 0; $i < strlen($N); $i++)
    {
        // (N[i]-'0') gives the digit
        // value and form the number
        $ans = ($ans * 10 + (int)($N[$i] - '0'));
        $ans %= $digit;
    }
    return ($ans == 0);
}

// Function to count digits which
// appears in N and divide N
// divide[10] --> array which tells
// that particular digit divides N or not
// count[10] --> counts frequency of
//                 digits which divide N
function allDigits($N)
{
    // We initialize all digits of N
    // as not divisible by N.
    $divide = array_fill(0, 10, false);
    $divide[1] = true; // 1 divides all numbers

    // start checking divisibility of
    // N by digits 2 to 9
    for ($digit = 2; $digit <= 9; $digit++)
    {
        // if digit divides N then
        // mark it as true
        if (divisible($N, $digit))
            $divide[$digit] = true;
    }

    // Now traverse the number string to
    // find and increment result whenever
    // a digit divides N.
    $result = 0;
    for ($i = 0; $i < strlen($N); $i++)
    {
        if ($divide[(int)($N[$i] - '0')] == true)
            $result++;
    }

    return $result;
}

// Driver Code
$N = "122324";
echo allDigits($N);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program to find number of digits
// in N that divide N.

// Utility function to
// check divisibility by digit
function divisible(N, digit)
{
    let ans = 0;
    for (let i = 0; i < N.length; i++)
    {

        // (N[i]-'0') gives the digit value and
        // form the number
        ans = (ans * 10 + (N[i] - '0'));
        ans %= digit;
    }
    return (ans == 0);
}

// Function to count digits which
// appears in N and divide N
// divide[10] --> array which
// tells that particular
// digit divides N or not
// count[10] --> counts
// frequency of digits which
// divide N
function allDigits(N)
{

    // We initialize all digits
    // of N as not divisible by N
    let divide = [];

    for (let i = 0; i < divide.length; i++)
    {
        divide[i] = false;
    }

    // 1 divides all numbers
    divide[1] = true;

    // start checking divisibility
    // of N by digits 2 to 9
    for (let digit = 2; digit <= 9; digit++)
    {

        // if digit divides N
        // then mark it as true
        if (divisible(N, digit))
            divide[digit] = true;
    }

    // Now traverse the number
    // string to find and increment
    // result whenever a digit divides N.
    let result = 0;

    for (let i = 0; i < N.length; i++)
    {
        if (divide[N[i] - '0'] == true)
            result++;
    }

    return result;
}

// Driver Code
    let N = "122324";
    document.write(allDigits(N));

// This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
5
```

**时间复杂度:** O(n)
**辅助空间:** O(1)
本文由 [**沙莎克·米什拉(古鲁)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。