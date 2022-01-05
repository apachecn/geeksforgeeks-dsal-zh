# 将二进制字符串拆分为 0 和 1 数量相等的子字符串

> 原文:[https://www . geesforgeks . org/将二进制字符串拆分为 0 和 1 等份的子字符串/](https://www.geeksforgeeks.org/split-the-binary-string-into-substrings-with-equal-number-of-0s-and-1s/)

给定长度为 **N** 的二进制字符串 **str** ，任务是找到连续子字符串 **str** 的最大计数，该最大计数可以被划分为使得所有子字符串都是平衡的，即它们具有相等数量的 **0s** 和 **1s** 。如果无法拆分满足条件的**字符串**，则打印 **-1** 。
**例:**

> **输入:** str = "0100110101"
> **输出:** 4
> 所需子串为“01”“0011”“01”“01”。
> **输入:** str = "0111100010"
> **输出:** 3
> 
> **输入:** str = "0000000000 "
> 
> **输出:** -1

**方式:**初始化**计数= 0** 逐字符遍历字符串并记录 **0s** 和 **1s** 的数量到目前为止，每当 **0s** 和 **1s** 的计数相等时，递增计数。如在给定的问题中，如果不可能分割字符串，那么在该时间，计数 0 必须不等于计数 1**，然后返回 **-1** ，否则在遍历完整的字符串后打印计数值。
以下是上述方法的实施:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of maximum substrings str
// can be divided into
int maxSubStr(string str, int n)
{

    // To store the count of 0s and 1s
    int count0 = 0, count1 = 0;

    // To store the count of maximum
    // substrings str can be divided into
    int cnt = 0;
    for (int i = 0; i < n; i++) {
        if (str[i] == '0') {
            count0++;
        }
        else {
            count1++;
        }
        if (count0 == count1) {
            cnt++;
        }
    }

    // It is not possible to
    // split the string
    if (count0!=count1) {
        return -1;
    }

    return cnt;
}

// Driver code
int main()
{
    string str = "0100110101";
    int n = str.length();

    cout << maxSubStr(str, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
class GFG
{

// Function to return the count
// of maximum substrings str
// can be divided into
static int maxSubStr(String str, int n)
{

    // To store the count of 0s and 1s
    int count0 = 0, count1 = 0;

    // To store the count of maximum
    // substrings str can be divided into
    int cnt = 0;
    for (int i = 0; i < n; i++)
    {
        if (str.charAt(i) == '0')
        {
            count0++;
        }
        else
        {
            count1++;
        }
        if (count0 == count1)
        {
            cnt++;
        }
    }

    // It is not possible to
    // split the string
    if (count0 != count1)
    {
        return -1;
    }
    return cnt;
}

// Driver code
public static void main(String []args)
{
    String str = "0100110101";
    int n = str.length();

    System.out.println(maxSubStr(str, n));
}
}

// This code is contributed by PrinciRaj1992
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Function to return the count
# of maximum substrings str
# can be divided into
def maxSubStr(str, n):

    # To store the count of 0s and 1s
    count0 = 0
    count1 = 0

    # To store the count of maximum
    # substrings str can be divided into
    cnt = 0

    for i in range(n):
        if str[i] == '0':
            count0 += 1
        else:
            count1 += 1

        if count0 == count1:
            cnt += 1

# It is not possible to
    # split the string
    if count0 != count1:
        return -1

    return cnt

# Driver code
str = "0100110101"
n = len(str)
print(maxSubStr(str, n))
```

## **C#**

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the count
// of maximum substrings str
// can be divided into
static int maxSubStr(String str, int n)
{

    // To store the count of 0s and 1s
    int count0 = 0, count1 = 0;

    // To store the count of maximum
    // substrings str can be divided into
    int cnt = 0;
    for (int i = 0; i < n; i++)
    {
        if (str[i] == '0')
        {
            count0++;
        }
        else
        {
            count1++;
        }
        if (count0 == count1)
        {
            cnt++;
        }
    }

    // It is not possible to
    // split the string
    if (count0 != count1)
    {
        return -1;
    }
    return cnt;
}

// Driver code
public static void Main(String []args)
{
    String str = "0100110101";
    int n = str.Length;

    Console.WriteLine(maxSubStr(str, n));
}
}

// This code is contributed by PrinciRaj1992
```

## **java 描述语言**

```
<script>

// JavaScript implementation of the approach

// Function to return the count
// of maximum substrings str
// can be divided into
function maxSubStr(str, n)
{

    // To store the count of 0s and 1s
    var count0 = 0, count1 = 0;

    // To store the count of maximum
    // substrings str can be divided into
    var cnt = 0;
    for (var i = 0; i < n; i++) {
        if (str[i] == '0') {
            count0++;
        }
        else {
            count1++;
        }
        if (count0 == count1) {
            cnt++;
        }
    }

    // It is not possible to
    // split the string
    if (count0 != count1) {
        return -1;
    }

    return cnt;
}

// Driver code
var str = "0100110101";
var n = str.length;
document.write( maxSubStr(str, n));

</script>
```

****Output:** 

```
4
```** 

****时间复杂度:** O(N)其中 N 为弦的长度
T3】空间复杂度: O(1)**