# 按位“或”等于 n 的最大集合

> 原文:[https://www.geeksforgeeks.org/largest-set-bitwise-equal-n/](https://www.geeksforgeeks.org/largest-set-bitwise-equal-n/)

给定一个整数 n，求按位 OR 等于 n 的最大可能非负整数集合。
**示例:**

```
Input : n = 5
Output : arr[] = [0, 1, 4, 5]
The bitwise OR of 0, 1, 4 and 5 equals 5\. 
It is not possible to obtain a set larger than this.

Input : n = 8
Output : arr[] = [0, 8]
```

**先决条件:** [按位 OR 等于 k 的最大子集](https://www.geeksforgeeks.org/maximum-subset-bitwise-equal-k/)
上面引用的文章和这篇文章的区别在于要检查的元素数量。在上面提到的文章中，我们有一个 n 个数字的数组，在这篇文章中，我们有整个非负数的集合。
遍历一个数组很简单，时间复杂度为 O(N)，但是遍历无限的非负数集合是不可能的。那么，我们如何将自己限制在一组更小的数字上呢？
答案在于使用的概念。对于任何大于 n 的数，x 和 n 的按位“或”永远不会等于 n。
因此我们只需要从 0 遍历到 n 就可以得到答案。
第二个区别就是这个问题总会有答案。另一方面，在上面提到的文章中没有确定答案的存在。这是因为我们总是可以在结果集中包含 n。
**算法:**
遍历从 0 到 n 的数字，用 n 检查其按位或。如果按位或等于 n，则在结果集中包括该数字。

## C++

```
// CPP Program to find the largest set
// with bitwise OR equal to n
#include <bits/stdc++.h>
using namespace std;

// function to find the largest set with
// bitwise OR equal to n
void setBitwiseORk(int n)
{
    vector<int> v;

    for (int i = 0; i <= n; i++) {

        // If the bitwise OR of n and i
        // is equal to n, then include i
        // in the set
        if ((i | n) == n)
            v.push_back(i);
    }

    for (int i = 0; i < v.size(); i++)
        cout << v[i] << ' ';
}

// Driver Code
int main()
{
    int n = 5;

    setBitwiseORk(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the largest set
// with bitwise OR equal to n
import java.util.*;

class GFG
{

    // function to find the largest set with
    // bitwise OR equal to n
    static void setBitwiseORk(int n)
    {
        Vector<Integer> v = new Vector<Integer>();

        for (int i = 0; i <= n; i++)
        {

            // If the bitwise OR of n and i
            // is equal to n, then include i
            // in the set
            if ((i | n) == n)
            {
                v.add(i);
            }
        }

        for (int i = 0; i < v.size(); i++)
        {
            System.out.print(v.get(i) + " ");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;

        setBitwiseORk(n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python 3 Program to find the largest
# set with bitwise OR equal to n

# function to find the largest set
# with bitwise OR equal to n
def setBitwiseORk(n):
    v = []

    for i in range(0, n + 1, 1):

        # If the bitwise OR of n and i
        # is equal to n, then include i
        # in the set
        if ((i | n) == n):
            v.append(i)

    for i in range(0, len(v), 1):
        print(v[i], end = ' ')

# Driver Code
if __name__ == '__main__':
    n = 5

    setBitwiseORk(n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# Program to find the largest set
// with bitwise OR equal to n
using System;
using System.Collections.Generic;

class GFG
{

    // function to find the largest set with
    // bitwise OR equal to n
    static void setBitwiseORk(int n)
    {
        List<int> v = new List<int>();

        for (int i = 0; i <= n; i++)
        {

            // If the bitwise OR of n and i
            // is equal to n, then include i
            // in the set
            if ((i | n) == n)
            {
                v.Add(i);
            }
        }

        for (int i = 0; i < v.Count; i++)
        {
            Console.Write(v[i] + " ");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 5;

        setBitwiseORk(n);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Program to find the largest set
// with bitwise OR equal to n

// function to find the largest set with
// bitwise OR equal to n
function setBitwiseORk(n)
{
    var v = [];

    for (var i = 0; i <= n; i++) {

        // If the bitwise OR of n and i
        // is equal to n, then include i
        // in the set
        if ((i | n) == n)
            v.push(i);
    }

    for (var i = 0; i < v.length; i++)
        document.write( v[i] + ' ');
}

// Driver Code
var n = 5;
setBitwiseORk(n);

</script>
```

**输出:**

```
0 1 4 5
```

**时间复杂度:** O(N)