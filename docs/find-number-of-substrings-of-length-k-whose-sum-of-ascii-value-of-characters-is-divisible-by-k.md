# 找出字符 ASCII 值之和可被 k 整除的长度为 k 的子串个数

> 原文:[https://www . geeksforgeeks . org/find-长度为 k 的子串数-其 ascii 字符值之和可被 k 整除/](https://www.geeksforgeeks.org/find-number-of-substrings-of-length-k-whose-sum-of-ascii-value-of-characters-is-divisible-by-k/)

给定一个字符串和一个数字 *k* ，任务是找到长度为 k 的子字符串的数量，其字符的 ASCII 值之和可被 k 整除。

**示例:**

> **输入:** str = "bcgabc "，k = 3
> **输出:** 2
> 子串“bcg”的 ASCII 值之和为 300，“abc”的 ASCII 值之和为 294，可被 3 整除。
> 
> **输入:** str = "adkf "，k = 3
> **输出:** 1

**方法:**首先求出长度为 k 的第一个子串的字符的 ASCII 值之和，然后利用滑动窗口技术减去前一个子串的第一个字符的 ASCII 值，再加上当前字符的 ASCII 值。如果和能被 k 整除，我们将在每一步增加计数器。

下面是上述方法的实现:

## C++

```
// C++ program to find number of substrings
// of length k whose sum of ASCII value of
// characters is divisible by k
#include<bits/stdc++.h>
using namespace std;

int count(string s, int k)
{

    // Finding length of string
    int n = s.length();
    int d = 0 ,i;
    int count = 0 ;

    for (i = 0; i <n; i++)
        // finding sum of ASCII value of first
        // substring
        d += s[i] ;

    if (d % k == 0)
        count += 1 ;

    for (i = k; i < n; i++)
    {

        // Using sliding window technique to
        // find sum of ASCII value of rest of
        // the substring
        int prev = s[i-k];
        d -= prev;
        d += s[i];

        // checking if sum is divisible by k
        if (d % k == 0)
        count += 1;
    }

    return count ;
    }

    // Driver code
    int main()
    {

        string s = "bcgabc" ;
        int k = 3 ;
        int ans = count(s, k);
        cout<<(ans);
    }
    // This code is contributed by
    // Sahil_Shelangia
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of substrings
// of length k whose sum of ASCII value of
// characters is divisible by k

public class GFG{

    static int count(String s, int k){

    // Finding length of string
    int n = s.length() ;
    int d = 0 ,i;
    int count = 0 ;

    for (i = 0; i <n; i++)
        // finding sum of ASCII value of first
        // substring
        d += s.charAt(i) ;

    if (d % k == 0)
        count += 1 ;

    for (i = k; i < n; i++)
    {

        // Using sliding window technique to
        // find sum of ASCII value of rest of
        // the substring
        int prev = s.charAt(i-k) ;
        d -= prev ;
        d += s.charAt(i) ;

        // checking if sum is divisible by k
        if (d % k == 0)
        count += 1 ;
    }

    return count ;
    }

    // Driver code
    public static void main(String[]args) {

        String s = "bcgabc" ;
        int k = 3 ;
        int ans = count(s, k);
        System.out.println(ans);
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 program to find number of substrings
# of length k whose sum of ASCII value of
# characters is divisible by k

def count(s, k):

    # Finding length of string
    n = len(s)
    d, count = 0, 0
    for i in range(k):

        # finding sum of ASCII value of first
        # substring
        d += ord(s[i])
        if (d % k == 0):
            count += 1
            for i in range(k, n):

                # Using sliding window technique to
                # find sum of ASCII value of rest of
                # the substring
                prev = ord(s[i-k])
                d -= prev
                d += ord(s[i])

                # checking if sum is divisible by k
                if (d % k == 0):
                    count += 1
                    return count
# Driver code
s = "bcgabc"
k = 3
ans = count(s, k)
print(ans)
```

## C#

```
// C# program to find number of substrings
// of length k whose sum of ASCII value of
// characters is divisible by k

using System;
public class GFG{

    static int count(string s, int k){

    // Finding length of string
    int n = s.Length ;
    int d = 0 ,i;
    int count = 0 ;

    for (i = 0; i <n; i++)
        // finding sum of ASCII value of first
        // substring
        d += s[i] ;

    if (d % k == 0)
        count += 1 ;

    for (i = k; i < n; i++)
    {

        // Using sliding window technique to
        // find sum of ASCII value of rest of
        // the substring
        int prev = s[i-k] ;
        d -= prev ;
        d += s[i] ;

        // checking if sum is divisible by k
        if (d % k == 0)
        count += 1 ;
    }

    return count ;
    }

    // Driver code
    public static void Main() {

        string s = "bcgabc" ;
        int k = 3 ;
        int ans = count(s, k);
        Console.Write(ans);
    }

}
```

## java 描述语言

```
<script>

// JavaScript program to find number of
// substrings of length k whose sum of
// ASCII value of characters is divisible by k
function count(s, k)
{

    // Finding length of string
    var n = s.length;
    var d = 0, i;
    var count = 0;

    for(i = 0; i < n; i++)

        // Finding sum of ASCII value of first
        // substring
        d += s[i].charCodeAt(0);

        if (d % k === 0)
        {
            count += 1;
        }

        for(i = k; i < n; i++)
        {

            // Using sliding window technique to
            // find sum of ASCII value of rest of
            // the substring
            var prev = s[i - k];
            d -= prev.charCodeAt(0);
            d += s[i].charCodeAt(0);

            // checking if sum is divisible by k
            if (d % k === 0)
                count += 1;
        }

    return count;
}

// Driver code
var s = "bcgabc";
var k = 3;
var ans = count(s, k);

document.write(ans);

// This code is contributed by rdtank

</script>
```

**Output:** 

```
2
```