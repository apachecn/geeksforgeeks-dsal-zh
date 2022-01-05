# 二进制字符串中十进制值为奇数的子字符串数量

> 原文:[https://www . geeksforgeeks . org/二进制字符串中带有奇数十进制值的子字符串数量/](https://www.geeksforgeeks.org/number-of-substrings-with-odd-decimal-value-in-a-binary-string/)

给定一个只包含 0 和 1 的二进制字符串。编写一个程序来查找十进制表示为奇数的该字符串的子字符串的数量。

**示例:**

```
Input : 101
Output : 3
Explanation : Substrings with odd decimal 
              representation are:
              {1, 1, 101}

Input : 1101
Output : 6
Explanation : Substrings with odd decimal 
              representation are:
              {1, 1, 1, 11, 101, 1011}
```

**蛮力法**:解决上述问题最简单的方法是生成给定字符串的所有可能的子串，并将其转换为十进制，并检查十进制表示是否为奇数。二进制到十进制的转换可以参考[这篇](https://www.geeksforgeeks.org/program-binary-decimal-conversion/)文章。
时间复杂度:O(n*n)

**有效方法**:一个有效的方法是观察如果一个二进制数的最后一位是 1，那么它是奇数，否则它是偶数。所以我们现在的问题是检查最后一个索引值为 1 的所有子字符串。通过从头到尾遍历，我们可以很容易地在单次遍历中解决这个问题。如果字符串中第 I 个索引的值是 1，那么在这个索引之前有 I 个奇数子字符串。但这也包括前导零的字符串。为了处理这个问题，我们可以使用一个辅助数组来记录索引前 1 的个数。我们只数一对 1。

下面是该方法的实现:

## C++

```
// CPP program to count substrings
// with odd decimal value
#include<iostream>
using namespace std;

// function to count number of substrings
// with odd decimal representation
int countSubstr(string s)
{  
    int n = s.length();

    // auxiliary array to store count
    // of 1's before ith index
    int auxArr[n] = {0};

    if (s[0] == '1')
        auxArr[0] = 1;

    // store  count of 1's before
    // i-th  index
    for (int i=1; i<n; i++)
    {
        if (s[i] == '1')
            auxArr[i] = auxArr[i-1]+1;
        else
            auxArr[i] = auxArr[i-1];
    }

    // variable to store answer
    int count = 0;

    // traverse the string reversely to
    // calculate number of odd substrings
    // before i-th index
    for (int i=n-1; i>=0; i--)   
        if (s[i] == '1')
            count += auxArr[i];   

    return count;
}

// Driver code
int main()
{
    string s = "1101";   
    cout << countSubstr(s);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count substrings
// with odd decimal value
import java.io.*;
import java.util.*;

class GFG {

// function to count number of substrings
// with odd decimal representation
static int countSubstr(String s)
{
    int n = s.length();

    // auxiliary array to store count
    // of 1's before ith index
    int[] auxArr=new int[n];

    if (s.charAt(0) == '1')
        auxArr[0] = 1;

    // store count of 1's before
    // i-th index
    for (int i=1; i<n; i++)
    {
        if (s.charAt(i) == '1')
            auxArr[i] = auxArr[i-1]+1;
        else
            auxArr[i] = auxArr[i-1];
    }

    // variable to store answer
    int count = 0;

    // traverse the string reversely to
    // calculate number of odd substrings
    // before i-th index
    for (int i=n-1; i>=0; i--)
        if (s.charAt(i) == '1')
            count += auxArr[i];

    return count;
}

public static void main (String[] args) {
     String s = "1101";
    System.out.println(countSubstr(s));

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# python program to count substrings
# with odd decimal value
import math

# function to count number of substrings
# with odd decimal representation
def countSubstr( s):

    n = len(s)

    # auxiliary array to store count
    # of 1's before ith index
    auxArr= [0 for i in range(n)]

    if (s[0] == '1'):
        auxArr[0] = 1

    # store count of 1's before
    # i-th index
    for i in range(0,n):

      if (s[i] == '1'):
            auxArr[i] = auxArr[i-1]+1
      else:
            auxArr[i] = auxArr[i-1]

    # variable to store answer
    count = 0

    # traverse the string reversely to
    # calculate number of odd substrings
    # before i-th index
    for i in range(n-1,-1,-1):
        if (s[i] == '1'):
            count += auxArr[i]

    return count
# Driver method
s = "1101"
print (countSubstr(s))

# This code is contributed by Gitanjali.
```

## C#

```
// C# program to count substrings
// with odd decimal value
using System;

class GFG {

// Function to count number of substrings
// with odd decimal representation
static int countSubstr(string s)
{
    int n = s.Length;

    // auxiliary array to store count
    // of 1's before ith index
    int[] auxArr = new int[n];

    if (s[0] == '1')
        auxArr[0] = 1;

    // store count of 1's before
    // i-th index
    for (int i = 1; i < n; i++)
    {
        if (s[i] == '1')
            auxArr[i] = auxArr[i - 1] + 1;
        else
            auxArr[i] = auxArr[i - 1];
    }

    // variable to store answer
    int count = 0;

    // Traverse the string reversely to
    // calculate number of odd substrings
    // before i-th index
    for (int i = n - 1; i >= 0; i--)
        if (s[i] == '1')
            count += auxArr[i];

    return count;
}

// Driver Code
public static void Main () {
    string s = "1101";
    Console.WriteLine(countSubstr(s));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// substrings with odd
// decimal value

// function to count number
// of substrings with odd
// decimal representation
function countSubstr($s)
{
    $n = strlen($s);

    // auxiliary array to
    // store count of 1's
    // before ith index
    $auxArr = array();

    if ($s[0] == '1')
        $auxArr[0] = 1;

    // store count of 1's
    // before i-th index
    for ($i = 1; $i < $n; $i++)
    {
        if ($s[$i] == '1')
            $auxArr[$i] = $auxArr[$i - 1] + 1;
        else
            $auxArr[$i] = $auxArr[$i - 1];
    }

    // variable to
    // store answer
    $count = 0;

    // traverse the string
    // reversely to calculate
    // number of odd substrings
    // before i-th index
    for ($i = $n - 1; $i >= 0; $i--)
        if ($s[$i] == '1')
            $count += $auxArr[$i];

    return $count;
}

// Driver code
$s = "1101";
echo countSubstr($s);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

// Javascript program to count substrings
// with odd decimal value

// Function to count number of substrings
// with odd decimal representation
function countSubstr(s)
{
    let n = s.length;

    // auxiliary array to store count
    // of 1's before ith index
    let auxArr = new Array(n);

    if (s[0] == '1')
        auxArr[0] = 1;

    // Store count of 1's before
    // i-th index
    for(let i = 1; i < n; i++)
    {
        if (s[i] == '1')
            auxArr[i] = auxArr[i - 1] + 1;
        else
            auxArr[i] = auxArr[i - 1];
    }

    // Variable to store answer
    let count = 0;

    // Traverse the string reversely to
    // calculate number of odd substrings
    // before i-th index
    for(let i = n - 1; i >= 0; i--)
        if (s[i] == '1')
            count += auxArr[i];

    return count;
}

// Driver code
let s = "1101";

document.write(countSubstr(s));

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
6
```

**时间复杂度**:O(n)
T3】辅助空间 : O(n)