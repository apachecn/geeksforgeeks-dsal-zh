# 使用给定操作的最小次数将一个字符串转换为另一个字符串

> 原文:[https://www . geesforgeks . org/transform-一个字符串到另一个字符串-使用最小给定操作数/](https://www.geeksforgeeks.org/transform-one-string-to-another-using-minimum-number-of-given-operation/)

给定两个字符串 A 和 B，任务是在可能的情况下将 A 转换为 B。唯一允许的操作是将 A 中的任何字符放在前面并插入。查找是否可以转换字符串。如果是，则输出转换所需的最小操作数。

**示例:**

```
Input:  A = "ABD", B = "BAD"
Output: 1
Explanation: Pick B and insert it at front.

Input:  A = "EACBD", B = "EABCD"
Output: 3
Explanation: Pick B and insert at front, EACBD => BEACD
             Pick A and insert at front, BEACD => ABECD
             Pick E and insert at front, ABECD => EABCD
```

检查一个字符串是否可以转换成另一个字符串很简单。我们需要检查两个字符串是否具有相同的字符数和相同的字符集。这可以通过为第一个字符串创建计数数组并检查第二个字符串是否每个字符的计数相同来轻松完成。
当我们确定能把 A 变换成 B 时，如何求最小运算次数？想法是从两个字符串的最后一个字符开始匹配。如果最后一个字符匹配，那么我们的任务减少到 n-1 个字符。如果最后几个字符不匹配，那么找到 B 的不匹配字符在 A 中的位置，两个位置的差异表明 A 的这许多字符必须移动到 A 的当前字符之前。

下面是完整的算法。
1)首先为 A 的所有字符创建一个计数数组，然后与 B 一起检查 B 是否对每个字符都有相同的计数，从而找出 A 是否可以转换为 B。
2)将结果初始化为 0。
3)从两根弦的末端开始穿越。
…… a)如果 A 和 B 的当前字符匹配，即 A[I]= = B[j]
……则 i = i-1 和 j = j-1
b)如果当前字符不匹配，则在剩余的
中搜索 B[j]……A .搜索时，保持递增结果，因为这些字符
……必须向前移动以进行 A 到 B 的转换

下面是基于这个想法的实现。

## C++

```
// C++ program to find minimum number of
// operations required to transform one string to other
#include<bits/stdc++.h>
using namespace std;

// Function to find minimum number of operations required to transform
// A to B.
int minOps(string& A, string& B)
{
    int m = A.length(), n = B.length();

     // This parts checks whether conversion is
     // possible or not
    if (n != m)
       return -1;
    int count[256];
    memset(count, 0, sizeof(count));
    for (int i=0; i<n; i++)   // count characters in A
       count[B[i]]++;
    for (int i=0; i<n; i++)   // subtract count for
       count[A[i]]--;         // every character in B
    for (int i=0; i<256; i++)   // Check if all counts become 0
      if (count[i])
         return -1;

    // This part calculates the number of operations required
    int res = 0;
    for (int i=n-1, j=n-1; i>=0; )
    {
        // If there is a mismatch, then keep incrementing
        // result 'res' until B[j] is not found in A[0..i]
        while (i>=0 && A[i] != B[j])
        {
            i--;
            res++;
        }

        // If A[i] and B[j] match
        if (i >= 0)
        {
            i--;
            j--;
        }
    }
    return res;
}

// Driver program
int main()
{
    string A = "EACBD";
    string B = "EABCD";
    cout << "Minimum number of operations "
            "required is " << minOps(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of
// operations required to transform one
// string to other
import java.io.*;
import java.util.*;

public class GFG {

    // Function to find minimum number of
    // operations required to transform
    // A to B.
    public static int minOps(String A, String B)
    {

        // This parts checks whether conversion is
        // possible or not
        if(A.length() != B.length())
            return -1;

        int i, j, res = 0;
        int count [] = new int [256];

        // count characters in A

        // subtract count for every character in B
        for(i = 0; i < A.length(); i++)
        {
            count[A.charAt(i)]++;
            count[B.charAt(i)]--;
        }

        // Check if all counts become 0
        for(i = 0; i < 256; i++)
            if(count[i] != 0)
                return -1;

        i = A.length() - 1;
        j = B.length() - 1;

        while(i >= 0)
        {
            // If there is a mismatch, then
            // keep incrementing result 'res'
            // until B[j] is not found in A[0..i]
            if(A.charAt(i) != B.charAt(j))
                res++;
            else
                j--;
            i--;        
        }
        return res;    
    }

    // Driver code
    public static void main(String[] args)
    {
        String A = "EACBD";
        String B = "EABCD";

        System.out.println("Minimum number of "
                    + "operations required is "
                                 + minOps(A, B));
    }
}

// This code is contributed by Dipesh Jain
// (dipesh_jain)
```

## 计算机编程语言

```
# Python program to find the minimum number of
# operations required to transform one string to other

# Function to find minimum number of operations required
# to transform A to B
def minOps(A, B):
    m = len(A)
    n = len(B)

    # This part checks whether conversion is possible or not
    if n != m:
        return -1

    count = [0] * 256

    for i in xrange(n):        # count characters in A
        count[ord(B[i])] += 1
    for i in xrange(n):        # subtract count for every char in B
        count[ord(A[i])] -= 1
    for i in xrange(256):    # Check if all counts become 0
        if count[i]:
            return -1

    # This part calculates the number of operations required
    res = 0
    i = n-1
    j = n-1   
    while i >= 0:

        # if there is a mismatch, then keep incrementing
        # result 'res' until B[j] is not found in A[0..i]
        while i>= 0 and A[i] != B[j]:
            i -= 1
            res += 1

        # if A[i] and B[j] match
        if i >= 0:
            i -= 1
            j -= 1

    return res

# Driver program
A = "EACBD"
B = "EABCD"
print "Minimum number of operations required is " + str(minOps(A,B))
# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to find minimum number of
// operations required to transform one
// string to other
using System;

class GFG
{

// Function to find minimum number of
// operations required to transform
// A to B.
public static int minOps(string A, string B)
{

    // This parts checks whether
    // conversion is possible or not
    if (A.Length != B.Length)
    {
        return -1;
    }

    int i, j, res = 0;
    int[] count = new int [256];

    // count characters in A

    // subtract count for every
    // character in B
    for (i = 0; i < A.Length; i++)
    {
        count[A[i]]++;
        count[B[i]]--;
    }

    // Check if all counts become 0
    for (i = 0; i < 256; i++)
    {
        if (count[i] != 0)
        {
            return -1;
        }
    }

    i = A.Length - 1;
    j = B.Length - 1;

    while (i >= 0)
    {
        // If there is a mismatch, then
        // keep incrementing result 'res'
        // until B[j] is not found in A[0..i]
        if (A[i] != B[j])
        {
            res++;
        }
        else
        {
            j--;
        }
        i--;
    }
    return res;
}

// Driver code
public static void Main(string[] args)
{
    string A = "EACBD";
    string B = "EABCD";

    Console.WriteLine("Minimum number of " +
                      "operations required is " +
                       minOps(A, B));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number of
// operations required to transform one string to other

// Function to find minimum number of operations required to transform
// A to B.
function minOps($A, $B)
{
    $m = strlen($A);
    $n = strlen($B);

     // This parts checks whether conversion is
     // possible or not
    if ($n != $m)
       return -1;
    $count = array_fill(0,256,NULL);
    for ($i=0; $i<$n; $i++)   // count characters in A
       $count[ord($B[$i])]++;
    for ($i=0; $i<$n; $i++)   // subtract count for
       $count[ord($A[$i])]--;         // every character in B
    for ($i=0; $i<256; $i++)   // Check if all counts become 0
      if ($count[$i])
         return -1;

    // This part calculates the number of operations required
    $res = 0;
    for ($i=$n-1, $j=$n-1; $i>=0; )
    {
        // If there is a mismatch, then keep incrementing
        // result 'res' until B[j] is not found in A[0..i]
        while ($i>=0 && $A[$i] != $B[$j])
        {
            $i--;
            $res++;
        }

        // If A[i] and B[j] match
        if ($i >= 0)
        {
            $i--;
            $j--;
        }
    }
    return $res;
}

// Driver program

$A = "EACBD";
$B = "EABCD";
echo "Minimum number of operations ".
            "required is ". minOps($A, $B);
return 0;
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum number
// of operations required to transform one
// string to other

// Function to find minimum number of
// operations required to transform
// A to B.
function minOps(A, B)
{

    // This parts checks whether conversion
    // is possible or not
    if (A.length != B.length)
        return -1;

    let i, j, res = 0;
    let count = new Array(256);

    for(let i = 0; i < 256; i++)
    {
        count[i] = 0;
    }

    // count characters in A

    // Subtract count for every character in B
    for(i = 0; i < A.length; i++)
    {
        count[A[i].charCodeAt(0)]++;
        count[B[i].charCodeAt(0)]--;
    }

    // Check if all counts become 0
    for(i = 0; i < 256; i++)
        if (count[i] != 0)
            return -1;

    i = A.length - 1;
    j = B.length - 1;

    while(i >= 0)
    {

        // If there is a mismatch, then
        // keep incrementing result 'res'
        // until B[j] is not found in A[0..i]
        if (A[i] != B[j])
            res++;
        else
            j--;

        i--;        
    }
    return res;    
}

// Driver code
let A = "EACBD";
let B = "EABCD";

document.write("Minimum number of " +
               "operations required is " +
               minOps(A, B));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Minimum number of operations required is 3
```

**时间复杂度:** O(n)，请注意 I 总是递减(在 while 循环和 if 中)，for 循环从 n-1 开始，在 i > = 0 时运行。

感谢 Gaurav Ahirwar 的上述解决方案。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息