# 给定二进制串中可被 2 整除的子串数

> 原文:[https://www . geesforgeks . org/给定二进制字符串中可被 2 整除的子字符串数/](https://www.geeksforgeeks.org/number-of-sub-strings-in-a-given-binary-string-divisible-by-2/)

给定长度为 **N** 的二进制字符串 **str** ，任务是找出可被 **2** 整除的 **str** 的子字符串数。子串中的前导零是允许的。

**示例:**

> **输入:** str = "101"
> **输出:**2
> “0”和“10”是唯一可被 2 整除的子串
> 。
> 
> **输入:**str = " 10010 "
> T3】输出: 10

**天真的方法:**天真的方法是生成所有可能的子串，并检查它们是否能被 2 整除。时间复杂度为 0(N<sup>3</sup>)。

**有效方法:**可以观察到，任何二进制数只有在以一个 **0** 结尾时才能被 **2** 整除。现在，任务是计算以 **0** 结束的子串数量。因此，对于每个索引 **i** ，使得 **str[i] = '0'** ，找到以 **i** 结束的子串的数量。该值等于 **(i + 1)** (基于 0 的索引)。因此，最终答案将等于所有 **i** 的 **(i + 1)** 的总和，使得 **str[i] = '0'** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of the required substrings
int countSubStr(string str, int len)
{
    // To store the final answer
    int ans = 0;

    // Loop to find the answer
    for (int i = 0; i < len; i++) {

        // Condition to update the answer
        if (str[i] == '0')
            ans += (i + 1);
    }

    return ans;
}

// Driver code
int main()
{
    string str = "10010";
    int len = str.length();

    cout << countSubStr(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the count
    // of the required substrings
    static int countSubStr(String str, int len)
    {
        // To store the final answer
        int ans = 0;

        // Loop to find the answer
        for (int i = 0; i < len; i++)
        {

            // Condition to update the answer
            if (str.charAt(i) == '0')
                ans += (i + 1);
        }
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "10010";
        int len = str.length();

        System.out.println(countSubStr(str, len));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of the required substrings
def countSubStr(strr, lenn):

    # To store the final answer
    ans = 0

    # Loop to find the answer
    for i in range(lenn):

        # Condition to update the answer
        if (strr[i] == '0'):
            ans += (i + 1)

    return ans

# Driver code
strr = "10010"
lenn = len(strr)

print(countSubStr(strr, lenn))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of the required substrings
    static int countSubStr(string str, int len)
    {
        // To store the final answer
        int ans = 0;

        // Loop to find the answer
        for (int i = 0; i < len; i++)
        {

            // Condition to update the answer
            if (str[i] == '0')
                ans += (i + 1);
        }
        return ans;
    }

    // Driver code
    public static void Main ()
    {
        string str = "10010";
        int len = str.Length;

        Console.WriteLine(countSubStr(str, len));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of the required substrings
function countSubStr(str, len)
{
    // To store the final answer
    var ans = 0;

    // Loop to find the answer
    for (var i = 0; i < len; i++) {

        // Condition to update the answer
        if (str[i] == '0')
            ans += (i + 1);
    }

    return ans;
}

// Driver code
var str = "10010";
var len = str.length;
document.write( countSubStr(str, len));

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(N)，N =字符串长度

**辅助空间:** O(1)