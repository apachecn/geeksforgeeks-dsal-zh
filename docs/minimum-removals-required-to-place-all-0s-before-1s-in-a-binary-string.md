# 将二进制字符串中所有 0 放在 1 之前所需的最小删除量

> 原文:[https://www . geesforgeks . org/minimum-removes-required-to-place-all-0s-before-1s in-a-binary-string/](https://www.geeksforgeeks.org/minimum-removals-required-to-place-all-0s-before-1s-in-a-binary-string/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到需要从 **S** 中删除的最小字符数，这样所有的 **0** s 都被放在 **1** s 之前

**示例:**

> **输入:**S =“001101”
> **输出:** 1
> **解释:**
> 移除 S[4] (= '0 ')将字符串 S 修改为“00111”。
> 因此，所需的最小删除数为 1。
> 
> **输入:** S = 01001
> **输出:** 1
> **解释:**
> 移除 S[1] (= '1 ')将字符串 S 修改为“0001”。
> 因此，所需的最小删除数为 1。

**方法:**解决问题的方法是:从右边找出最少需要删除的**‘0’**s 个字符，说 **right_0，**和最少需要删除的**‘1’**s 个字符，说 **left_1** ，得到需要的字符串。任一指标得到的 **right_0** 和 **left_0** 的最小和即为最终结果。

按照以下步骤解决给定的问题:

1.  初始化两个计数器变量，比如说**右 _0** 和**左 _1** 。
2.  将字符串 **S** 中**0’**的计数存储在**右 _0** 中，并将**左 _1** 设置为等于 **0** 。
3.  初始化一个变量，说 **res，**来存储需要的答案。
4.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，对于每个字符:
    *   检查**s[I]是否等于‘0’。**
        *   如果发现为真，则用 **1** 减少**右 _0** 。
        *   否则，用 **1** 增加**左 _1** 。
    *   检查 **right_0，left_1** 之和是否小于 **res** 。如果发现为真，则更新 **res** 至最小 **res** 和 **right_0 + left_1。**
5.  完成数组遍历后，打印 **res** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum removals
// required to arrange all 0s before 1s
int minimumDeletions(string s)
{
    // Count the occurences of 0 in s
    int right_0 = count(s.begin(), s.end(), '0');

    int left_1 = 0;

    // Size of the string
    int n = s.size();

    // Stores the minimum
    // number of removals required
    int res = INT_MAX;

    // Iterate over each of the
    // characters in the string s
    for (int i = 0; i < n; i++)
    {
        // If the i-th character
        // is found to be '0'
        if (s[i] == '0')
        {
            right_0 -= 1;
        }
        else
        {
            left_1 += 1;
        }

        // Store the minimum of res
        // and right_0 + left_1 in res
        res = min(res, right_0 + left_1);
    }

    // Return the final result
    return res;
}

// Driver Code
int main()
{
    string s = "001101";
    int count = minimumDeletions(s);

    cout << count;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to count minimum removals
// required to arrange all 0s before 1s
static int minimumDeletions(String s)
{

    // Count the occurences of 0 in s
    int right_0 = (int)(s.chars().filter(ch -> ch == '0').count());
    int left_1 = 0;

    // Size of the string
    int n = s.length();

    // Stores the minimum
    // number of removals required
    int res = Integer.MAX_VALUE;

    // Iterate over each of the
    // characters in the string s
    for (int i = 0; i < n; i++)
    {
        // If the i-th character
        // is found to be '0'
        if (s.charAt(i) == '0')
        {
            right_0 -= 1;
        }
        else
        {
            left_1 += 1;
        }

        // Store the minimum of res
        // and right_0 + left_1 in res
        res = Math.min(res, right_0 + left_1);
    }

    // Return the final result
    return res;
}

// Driver Code
public static void main(String[] args)
{
    String s = "001101";
    int count = minimumDeletions(s);

    System.out.print(count);
}
}

// This code is contributed by  sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to count minimum removals
# required to arrange all 0s before 1s
def minimumDeletions(s) :

    # Count the occurences of 0 in s
    right_0 = s.count('0')

    left_1 = 0

    # Size of the string
    n = len(s)

    # Stores the minimum
    # number of removals required
    res = sys.maxsize

    # Iterate over each of the
    # characters in the string s
    for i in range(n):

        # If the i-th character
        # is found to be '0'
        if (s[i] == '0') :
            right_0 -= 1

        else :
            left_1 += 1

        # Store the minimum of res
        # and right_0 + left_1 in res
        res = min(res, right_0 + left_1)

    # Return the final result
    return res

# Driver Code
s = "001101"
count = minimumDeletions(s)

print( count)

# This code is contributed by splevel62.
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to count minimum removals
// required to arrange all 0s before 1s
static int minimumDeletions(string s)
{

    // Count the occurences of 0 in s
    int right_0 = (int)s.Split('0').Length - 1;
    int left_1 = 0;

    // Size of the string
    int n = s.Length;

    // Stores the minimum
    // number of removals required
    int res = Int32.MaxValue;

    // Iterate over each of the
    // characters in the string s
    for (int i = 0; i < n; i++)
    {
        // If the i-th character
        // is found to be '0'
        if (s[i] == '0')
        {
            right_0 -= 1;
        }
        else
        {
            left_1 += 1;
        }

        // Store the minimum of res
        // and right_0 + left_1 in res
        res = Math.Min(res, right_0 + left_1);
    }

    // Return the final result
    return res;
}

// Driver code
public static void Main(String[] args)
{
    string s = "001101";
    int count = minimumDeletions(s);

    Console.WriteLine(count);
}
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count minimum removals
// required to arrange all 0s before 1s
function minimumDeletions(s)
{
    // Count the occurences of 0 in s
    var right_0 = 0;
    var i;
    for (i=0;i<s.length;i++){
        if(s[i]=='0')
            right_0++;
    }
    var left_1 = 0;

    // Size of the string
    var n = s.length;

    // Stores the minimum
    // number of removals required
    var res = 2147483647;

    // Iterate over each of the
    // characters in the string s
    for (i = 0; i < n; i++)
    {
        // If the i-th character
        // is found to be '0'
        if (s[i] == '0')
        {
            right_0 -= 1;
        }
        else
        {
            left_1 += 1;
        }

        // Store the minimum of res
        // and right_0 + left_1 in res
        res = Math.min(res, right_0 + left_1);
    }

    // Return the final result
    return res;
}

// Driver Code
    var s = "001101";
    var count = minimumDeletions(s);
    document.write(count);

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(|S|)*
***辅助空间:** O(1)*