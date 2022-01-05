# 求龙曲线序列的第 n 项

> 原文:[https://www . geesforgeks . org/find-n th-term-dragon-curve-sequence/](https://www.geeksforgeeks.org/find-nth-term-dragon-curve-sequence/)

[**龙曲线序列**](https://en.wikipedia.org/wiki/Regular_paperfolding_sequence) 是 0 和 1 的无限二进制序列。序列的第一项是 1。
从下一个术语开始，我们在前一个术语的每个元素之间交替插入 1 和 0。
为了更好地理解，请参考以下解释:

> *   1 (starting from 1)
>     
> *   "1" 1 "0"
>     1 and 0 are alternately inserted around the last term. The numbers in double quotes here represent the newly added elements.
>     So the second term becomes
>     1 1 0.
> *   "1" 1 "0" 1 "1" 0 "
>     So the third term becomes
>     1 101 01 00
>     
> *   "1" 101 "0" 01 "1" 0 "0" 1 "0"
>     The fourth term becomes
>     110101010101000 【T10】

这也就是俗称的**常规折纸顺序**。给定一个自然数 **n** 。任务是找到长度为![2^n - 1 ](img/cc29a41a0d3069cc8d06aabb3eadc302.png "Rendered by QuickLaTeX.com")的龙曲线序列形成的第 n 根弦。
**例:**

```
Input: n = 4
Output: 110110011100100
Explanation:
We get 1 as the first term, 
"110" as the second term,
"1101100" as the third term ,
And hence our fourth term will be
"110110011100100"

Input: n = 3
Output: 1101100
```

**方法:**从第一项 1 开始。然后在前一项的每个元素后交替添加 1 和 0。获得的新项成为当前项。在从 1 到 n 的循环中重复这个过程，生成每个项，最后生成第 n 个项。
以下是以上想法的实现:

## C++

```
// CPP code to find nth term
// of the Dragon Curve Sequence
#include <bits/stdc++.h>
using namespace std;

// function to generate the nth term
string Dragon_Curve_Sequence(int n) 
{
    // first term
    string s = "1"; 

    // generating each term of the sequence
    for (int i = 2; i <= n; i++) 
    {
        string temp = "1";
        char prev = '1', zero = '0', one = '1';

        // loop to generate the ith term
        for (int j = 0; j < s.length(); j++) 
        {
            // add character from the 
            // original string
            temp += s[j];

            // add alternate 0 and 1 in between
            if (prev == '0') 
            {
                // if previous added term
                // was '0' then add '1'
                temp += one;

                // now current term becomes
                // previous term
                prev = one;
            }
            else 
            {
                // if previous added term
                // was '1', then add '0'
                temp += zero;

                // now current term becomes
                // previous term
                prev = zero;
            }
        }

        // s becomes the ith term of the sequence
        s = temp;
    }
    return s;
}

// Driver program
int main()
{
    // Taking inputs
    int n = 4;

    // generate nth term of dragon curve sequence
    string s = Dragon_Curve_Sequence(n);

    // Printing output
    cout << s << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find nth term
// of the Dragon Curve Sequence
import java.util.*;

class solution
{

// function to generate the nth term
static String Dragon_Curve_Sequence(int n) 
{
    // first term
    String s = "1"; 

    // generating each term of the sequence
    for (int i = 2; i <= n; i++) 
    {
        String temp = "1";
        char prev = '1', zero = '0', one = '1';

        // loop to generate the ith term
        for (int j = 0; j < s.length(); j++) 
        {
            // add character from the 
            // original string
            temp += s.charAt(j);

            // add alternate 0 and 1 in between
            if (prev == '0') 
            {
                // if previous added term
                // was '0' then add '1'
                temp += one;

                // now current term becomes
                // previous term
                prev = one;
            }
            else 
            {
                // if previous added term
                // was '1', then add '0'
                temp += zero;

                // now current term becomes
                // previous term
                prev = zero;
            }
        }

        // s becomes the ith term of the sequence
        s = temp;
    }
    return s;
}

// Driver program
public static void main(String args[])
{
    // Taking inputs
    int n = 4;

    // generate nth term of dragon curve sequence
    String s = Dragon_Curve_Sequence(n);

    // Printing output
    System.out.println(s);
}

}

//This code is contributed by 
//Surendra_Gangwar
```

## 计算机编程语言

```
# Python code to find nth term
# of the Dragon Curve Sequence

# function to generate 
# the nth term
def Dragon_Curve_Sequence(n):

    # first term
    s = "1"

    # generating each term
    # of the sequence
    for i in range(2, n + 1):
        temp = "1"
        prev = '1'
        zero = '0'
        one = '1'

        # loop to generate the ith term
        for j in range(len(s)):

            # add character from the
            # original string
            temp += s[j]

            # add alternate 0 and 
            # 1 in between
            if (prev == '0'):

                # if previous added term
                # was '0' then add '1'
                temp += one

                # now current term becomes
                # previous term
                prev = one

            else:

                # if previous added term
                # was '1', then add '0'
                temp += zero

                # now current term becomes
                # previous term
                prev = zero

        # s becomes the ith term
        # of the sequence
        s = temp

    return s

# Driver Code
n = 4

# generate nth term of 
# dragon curve sequence
s = Dragon_Curve_Sequence(n)

# Printing output
print(s)

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# code to find nth term 
// of the Dragon Curve Sequence 
using System;

class GFG
{ 

// function to generate the nth term 
static String Dragon_Curve_Sequence(int n) 
{ 
    // first term 
    String s = "1"; 

    // generating each term of the sequence 
    for (int i = 2; i <= n; i++) 
    { 
        String temp = "1"; 
        char prev = '1', zero = '0', one = '1'; 

        // loop to generate the ith term 
        for (int j = 0; j < s.Length; j++) 
        { 
            // add character from the 
            // original string 
            temp += s[j]; 

            // add alternate 0 and 1 in between 
            if (prev == '0') 
            { 
                // if previous added term 
                // was '0' then add '1' 
                temp += one; 

                // now current term becomes 
                // previous term 
                prev = one; 
            } 
            else
            { 
                // if previous added term 
                // was '1', then add '0' 
                temp += zero; 

                // now current term becomes 
                // previous term 
                prev = zero; 
            } 
        } 

        // s becomes the ith term of the sequence 
        s = temp; 
    } 
    return s; 
} 

// Driver Code
public static void Main() 
{ 
    // Taking inputs 
    int n = 4; 

    // generate nth term of dragon
    // curve sequence 
    String s = Dragon_Curve_Sequence(n); 

    // Printing output 
    Console.WriteLine(s); 
} 
} 

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find nth term
// of the Dragon Curve Sequence

// function to generate the nth term
function Dragon_Curve_Sequence($n) 
{
    // first term
    $s = "1"; 

    // generating each term of the sequence
    for ($i = 2; $i <= $n; $i++) 
    {
        $temp = "1";
        $prev = '1';
        $zero = '0';
        $one = '1';

        // loop to generate the ith term
        for ($j = 0; $j < strlen($s); $j++) 
        {
            // add character from the 
            // original string
            $temp .= $s[$j];

            // add alternate 0 and 1 in between
            if ($prev == '0') 
            {
                // if previous added term
                // was '0' then add '1'
                $temp .= $one;

                // now current term becomes
                // previous term
                $prev = $one;
            }
            else
            {
                // if previous added term
                // was '1', then add '0'
                $temp .= $zero;

                // now current term becomes
                // previous term
                $prev = $zero;
            }
        }

        // s becomes the ith term of the sequence
        $s = $temp;
    }
    return $s;
}

// Driver code

    // Taking inputs
    $n = 4;

    // generate nth term of dragon curve sequence
    $s = Dragon_Curve_Sequence($n);

    // Printing output
    echo $s."\n";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// Javascript code to find nth term
// of the Dragon Curve Sequence

// function to generate the nth term
function Dragon_Curve_Sequence(n) 
{
    // first term
    let s = "1"; 

    // generating each term of the sequence
    for (let i = 2; i <= n; i++) 
    {
        let temp = "1";
        let prev = '1';
        let zero = '0';
        let one = '1';

        // loop to generate the ith term
        for (let j = 0; j < s.length; j++) 
        {
            // add character from the 
            // original string
            temp = temp + s[j];

            // add alternate 0 and 1 in between
            if (prev == '0') 
            {
                // if previous added term
                // was '0' then add '1'
                temp += one;

                // now current term becomes
                // previous term
                prev = one;
            }
            else
            {
                // if previous added term
                // was '1', then add '0'
                temp += zero;

                // now current term becomes
                // previous term
                prev = zero;
            }
        }

        // s becomes the ith term of the sequence
        s = temp;
    }
    return s;
}

// Driver code

    // Taking inputs
    let n = 4;

    // generate nth term of dragon curve sequence
    let s = Dragon_Curve_Sequence(n);

    // Printing output
    document.write(s + "<br>");

// This code is contributed by gfgking
</script>
```

**输出:**

```
110110011100100
```