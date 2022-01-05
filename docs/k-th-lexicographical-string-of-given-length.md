# 给定长度的第 K 个词典字符串

> 原文:[https://www . geesforgeks . org/k-th-给定长度的词典式字符串/](https://www.geeksforgeeks.org/k-th-lexicographical-string-of-given-length/)

给定两个整数 **N** 和 **K** ，任务是找到**字典上的** **K <sup>th</sup>** 长度的字符串 **N** 。如果长度 **N** 的可能串数小于 **K** ，打印 **-1** 。
**例:**

> **输入:** N = 3，K = 10
> **输出:**【aaj】
> **说明:**从“aaa”开始的字典顺序中的第 10 个字符串是“aaj”。
> **输入:** N = 2，K = 1000
> **输出:** -1
> ***说明:*** 总共 26*26 = 676 个长度为 2 的字符串都是可以的。所以输出会是-1。

**进场:**

*   让我们假设一串长度 **N** 为基数 26 的**整数**。

*   例如，如果 N = 3，第一个字符串将是 **s = "aaa"** ，其整数形式的基数 26 表示将是 **0 0 0** ，第二个字符串将是 **s = "aab"** ，基数 26 表示将是 **0 0 1** 以此类推。因此每个数字可以有一个在**【0，25】**内的值。

*   从最后一个数字开始，我们需要将其更改为所有可能的值，然后是倒数第二个数字，以此类推。

*   所以，简化的问题是把一个十进制数 **K** 的表示变成一个 26 的基数。您可以阅读[这篇文章](https://www.geeksforgeeks.org/convert-base-decimal-vice-versa/)来清楚地了解如何做到这一点。

*   在我们找到以 26 为基数的整数形式的答案后，我们将把每个数字转换成它的等价字符，其中 **0** 是**【a】**， **1** 是**【b】**，…。 **24** 为**‘y’**， **25** 为**‘z’**。

以下是上述方法的实现:

## C++

```
// C++ program to find the K-th
// lexicographical string of length N
#include <bits/stdc++.h>
using namespace std;

string find_kth_String_of_n(int n, int k)
{

    // Initialize the array to store
    // the base 26 representation of 
    // K with all zeroes, that is, 
    // the initial String consists
    // of N a's
    int d[n] = {0};

    // Start filling all the
    // N slots for the base 26
    // representation of K
    for(int i = n - 1; i > -1; i--)
    {

       // Store the remainder
       d[i] = k % 26;

       // Reduce K
       k /= 26;
    }

    // If K is greater than the
    // possible number of strings
    // that can be represented by
    // a string of length N
    if (k > 0)
        return "-1";

    string s = "";

    // Store the Kth lexicographical
    // string
    for(int i = 0; i < n; i++)
       s += (d[i] + ('a'));

    return s;
}

// Driver Code
int main()
{
    int n = 3;
    int k = 10;

    // Reducing k value by 1 because
    // our stored value starts from 0
    k -= 1;

    cout << find_kth_String_of_n(n, k);
    return 0;
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// K-th lexicographical String
// of length N
class GFG{

static String find_kth_String_of_n(int n, int k)
{
    // Initialize the array to
    // store the base 26
    // representation of K
    // with all zeroes, that is,
    // the initial String consists
    // of N a's
    int[] d = new int[n];

    // Start filling all the
    // N slots for the base 26
    // representation of K
    for (int i = n - 1; i > -1; i--)
    {

        // Store the remainder
        d[i] = k % 26;

        // Reduce K
        k /= 26;
    }

    // If K is greater than the
    // possible number of Strings
    // that can be represented by
    // a String of length N
    if (k > 0)
        return "-1";

    String s = "";
    // Store the Kth lexicographical
    // String
    for (int i = 0; i < n; i++)
        s += (char)(d[i] + ('a'));

    return s;
}

public static void main(String[] args)
{
    int n = 3;
    int k = 10;

    // Reducing k value by 1 because
    // our stored value starts from 0
    k -= 1;
    System.out.println(find_kth_String_of_n(n, k));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python program to find the
# K-th lexicographical string
# of length N
def find_kth_string_of_n(n, k):
    # Initialize the array to
    # store the base 26
    # representation of K
    # with all zeroes, that is,
    # the initial string consists
    # of N a's
    d =[0 for i in range(n)]

    # Start filling all the
    # N slots for the base 26
    # representation of K
    for i in range(n - 1, -1, -1):

        # Store the remainder
        d[i]= k % 26

        # Reduce K
        k//= 26

    # If K is greater than the
    # possible number of strings
    # that can be represented by
    # a string of length N
    if k>0:
        return -1

    s =""
    # Store the Kth lexicographical
    # string
    for i in range(n):
        s+= chr(d[i]+ord('a'))

    return s    
n = 3
k = 10
# Reducing k value by 1 because
# our stored value starts from 0
k-= 1
print(find_kth_string_of_n(n, k))
```

## C#

```
// C# program to find the
// K-th lexicographical String
// of length N
using System;
class GFG{

static String find_kth_String_of_n(int n, int k)
{
    // Initialize the array to
    // store the base 26
    // representation of K
    // with all zeroes, that is,
    // the initial String consists
    // of N a's
    int[] d = new int[n];

    // Start filling all the
    // N slots for the base 26
    // representation of K
    for (int i = n - 1; i > -1; i--)
    {

        // Store the remainder
        d[i] = k % 26;

        // Reduce K
        k /= 26;
    }

    // If K is greater than the
    // possible number of Strings
    // that can be represented by
    // a String of length N
    if (k > 0)
        return "-1";

    string s = "";

    // Store the Kth lexicographical
    // String
    for (int i = 0; i < n; i++)
        s += (char)(d[i] + ('a'));

    return s;
}

// Driver Code
public static void Main()
{
    int n = 3;
    int k = 10;

    // Reducing k value by 1 because
    // our stored value starts from 0
    k -= 1;
    Console.Write(find_kth_String_of_n(n, k));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
    // Javascript program to find the
    // K-th lexicographical String
    // of length N

    function find_kth_String_of_n(n, k)
    {
        // Initialize the array to
        // store the base 26
        // representation of K
        // with all zeroes, that is,
        // the initial String consists
        // of N a's
        let d = new Array(n);
        d.fill(0);

        // Start filling all the
        // N slots for the base 26
        // representation of K
        for (let i = n - 1; i > -1; i--)
        {

            // Store the remainder
            d[i] = k % 26;

            // Reduce K
            k = parseInt(k / 26, 10);
        }

        // If K is greater than the
        // possible number of Strings
        // that can be represented by
        // a String of length N
        if (k > 0)
            return "-1";

        let s = "";

        // Store the Kth lexicographical
        // String
        for (let i = 0; i < n; i++)
            s += String.fromCharCode(d[i] + ('a').charCodeAt());

        return s;
    }

    let n = 3;
    let k = 10;

    // Reducing k value by 1 because
    // our stored value starts from 0
    k -= 1;
    document.write(find_kth_String_of_n(n, k));

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
aaj
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)