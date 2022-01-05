# 给定二进制串中可被 2 整除的子序列数

> 原文:[https://www . geesforgeks . org/给定二进制字符串中可被 2 整除的子序列数/](https://www.geeksforgeeks.org/number-of-subsequences-in-a-given-binary-string-divisible-by-2/)

给定长度为 **N** 的二进制字符串 **str** ，任务是找出可被 **2** 整除的 **str** 的子序列数。子序列中的前导零是允许的。

**示例:**

> **输入:** str = "101"
> **输出:**2
> “0”和“10”是唯一可被 2 整除的子序列
> 。
> **输入:** str = "10010"
> **输出:** 22

**天真的方法:**天真的方法是生成所有可能的子序列，并检查它们是否能被 2 整除。时间复杂度为 0(2<sup>N</sup>* N)。

**有效方法:**可以观察到，任何二进制数只有在以一个 **0** 结尾时才能被 **2** 整除。现在的任务是计算以 **0** 结束的子序列的数量。因此，对于每个索引 **i** ，使得 **str[i] = '0'** ，找到以 **i** 结束的子序列的数量。该值等于 **2 <sup>i</sup>** (基于 0 的索引)。因此，最终答案将等于所有 **i** 的**2<sup>I</sup>T21 的总和，使得 **str[i] = '0'** 。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of the required subsequences
int countSubSeq(string str, int len)
{
    // To store the final answer
    int ans = 0;

    // Multiplier
    int mul = 1;

    // Loop to find the answer
    for (int i = 0; i < len; i++) {

        // Condition to update the answer
        if (str[i] == '0')
            ans += mul;
        // updating multiplier
        mul *= 2;
    }

    return ans;
}

// Driver code
int main()
{
    string str = "10010";
    int len = str.length();

    cout << countSubSeq(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of the required subsequences
static int countSubSeq(String str, int len)
{
    // To store the final answer
    int ans = 0;

    // Multiplier
    int mul = 1;

    // Loop to find the answer
    for (int i = 0; i < len; i++)
    {

        // Condition to update the answer
        if (str.charAt(i) == '0')
            ans += mul;

        // updating multiplier
        mul *= 2;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    String str = "10010";
    int len = str.length();

    System.out.print(countSubSeq(str, len));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of the required subsequences
def countSubSeq(strr, lenn):

    # To store the final answer
    ans = 0

    # Multiplier
    mul = 1

    # Loop to find the answer
    for i in range(lenn):

        # Condition to update the answer
        if (strr[i] == '0'):
            ans += mul

        # updating multiplier
        mul *= 2

    return ans

# Driver code
strr = "10010"
lenn = len(strr)

print(countSubSeq(strr, lenn))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of the required subsequences
    static int countSubSeq(string str, int len)
    {
        // To store the final answer
        int ans = 0;

        // Multiplier
        int mul = 1;

        // Loop to find the answer
        for (int i = 0; i < len; i++)
        {

            // Condition to update the answer
            if (str[i] == '0')
                ans += mul;

            // updating multiplier
            mul *= 2;
        }
        return ans;
    }

    // Driver code
    static public void Main ()
    {
        string str = "10010";
        int len = str.Length;

        Console.WriteLine(countSubSeq(str, len));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of the required subsequences
function countSubSeq(str, len)
{
    // To store the final answer
    var ans = 0;

    // Multiplier
    var mul = 1;

    // Loop to find the answer
    for (var i = 0; i < len; i++) {

        // Condition to update the answer
        if (str[i] == '0')
            ans += mul;
        // updating multiplier
        mul *= 2;
    }

    return ans;
}

// Driver code
var str = "10010";
var len = str.length;
document.write( countSubSeq(str, len));

</script>
```

**输出:**

```
22
```