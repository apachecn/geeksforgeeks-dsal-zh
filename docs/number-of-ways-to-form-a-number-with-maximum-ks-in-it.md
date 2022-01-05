# 形成最大 Ks 数的方式数

> 原文:[https://www . geeksforgeeks . org/形成最大 ks 数的途径数/](https://www.geeksforgeeks.org/number-of-ways-to-form-a-number-with-maximum-ks-in-it/)

给定一个数字 **N** 和一个数字 **K** ，任务是计算形成其中最大数量 **Ks** 的数字的方法数，其中在一个操作中，总计为 **K** 的 **N** 的两个相邻数字都被 **K** 替换。

**示例**:

> **输入** :N=1454781，K=9
> **输出** : 2
> **说明** :9 在应用给定操作后最多可以出现两次，有两种方式。形成的两个数字是:19479 和 14979。194781 不能形成，因为它只包含一次 9，这不是最大值。
> 
> **输入** : N=1007，K=8
> **输出** : 1
> **说明**:1007 上不能进行任何操作。因此，可以存在的 8 的最大数量是 0，并且只有一个可能的这样的数量，即 1007。

**方法:**以下观察有助于解决问题:

1.  将数字视为字符串，形式为**“阿巴…”的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)**，其中 **A+B=K** 是数字中唯一有助于回答的部分。
2.  如果贡献子串的长度是偶数，那么只有一种方法可以对它们应用操作，因此，它们不会对答案做出贡献。例如，如果子串是**“ABAB”**，只能改成**“KK”**才能得到最终数中 **K 的**的最大个数
3.  否则，将会有 **⌈L/2⌉** 方法来获得 **Ks** 的最大数量，其中 **L** 是子串的长度。例如，如果子字符串是**“ABBAB”**，这可以转化为以下内容:
    1.  **【kka】**
    2.  **【kak】**
    3.  **"AKK"**

按照以下步骤解决问题:

1.  把 **N** 转换成[弦](https://www.geeksforgeeks.org/string-data-structure/)，说 **S** 。
2.  将变量**和**初始化为 **1** ，以存储最终答案。
3.  [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，对于每个当前索引 **i** ，执行以下操作:
    1.  初始化一个变量**计数**到 **1** ，存储当前答案的长度。
    2.  当 **i** 小于 **S** 的长度，并且**S【I】**和**S【I-1】**的位数之和等于 **K** 时循环，并执行以下操作:
        1.  增量 **i** 。
        2.  递增**计数**。
    3.  如果**计数**为奇数，则将 **ans** 更新为 **ans*(计数+1)/2。**
4.  返回〔t0〕年〔t1〕年。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to calculate number
// of ways a number can be
// formed that has the maximum number of Ks
int noOfWays(int N, int K)
{
    // convert to string
    string S = to_string(N);
    int ans = 1;
    // calculate length of subarrays
    // that can contribute to
    // the answer
    for (int i = 1; i < S.length(); i++) {
        int count = 1;
        // count length of subarray
        // where adjacent digits
        // add up to K
        while (i < S.length()
               && S[i] - '0' + S[i - 1] - '0' == K) {
            count++;
            i++;
        }
        // Current subarray can
        // contribute to the answer
        // only if it is odd
        if (count % 2)
            ans *= (count + 1) / 2;
    }
    // return the answer
    return ans;
}
// Driver code
int main()
{
    // Input
    int N = 1454781;
    int K = 9;

    // Function call
    cout << noOfWays(N, K) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate number
// of ways a number can be formed
// that has the maximum number of Ks
static int noOfWays(int N, int K)
{

    // Convert to string
    String S = String.valueOf(N);
    int ans = 1;

    // Calculate length of subarrays
    // that can contribute to
    // the answer
    for(int i = 1; i < S.length(); i++)
    {
        int count = 1;

        // Count length of subarray
        // where adjacent digits
        // add up to K
        while (i < S.length() && (int)S.charAt(i) - 48 +
              (int)S.charAt(i - 1) - 48 == K)
        {
            count++;
            i++;
        }

        // Current subarray can
        // contribute to the answer
        // only if it is odd
        if (count % 2 == 1)
            ans *= (count + 1) / 2;
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int N = 1454781;
    int K = 9;

    // Function call
    System.out.print(noOfWays(N, K));
}   
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate number of ways a
# number can be formed that has the
# maximum number of Ks
def noOfWays(N, K):

    # Convert to string
    S = str(N)
    ans = 1

    # Calculate length of subarrays
    # that can contribute to
    # the answer
    for i in range(1, len(S)):
        count = 1

        # Count length of subarray
        # where adjacent digits
        # add up to K
        while (i < len(S) and ord(S[i]) +
         ord(S[i - 1]) - 2 * ord('0') == K):
            count += 1
            i += 1

        # Current subarray can
        # contribute to the answer
        # only if it is odd
        if (count % 2):
            ans *= (count + 1) // 2

    # Return the answer
    return ans

# Driver code
if __name__ == '__main__':

    # Input
    N = 1454781
    K = 9

    # Function call
    print(noOfWays(N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate number
// of ways a number can be
// formed that has the maximum number of Ks
static int noOfWays(int N, int K)
{

    // Convert to string
    string S = N.ToString();
    int ans = 1;

    // Calculate length of subarrays
    // that can contribute to
    // the answer
    for(int i = 1; i < S.Length; i++)
    {
        int count = 1;

        // Count length of subarray
        // where adjacent digits
        // add up to K
        while (i < S.Length && (int)S[i] - 48 +
              (int)S[i - 1] - 48 == K)
        {
            count++;
            i++;
        }

        // Current subarray can
        // contribute to the answer
        // only if it is odd
        if (count % 2 == 1)
            ans *= (count + 1) / 2;
    }

    // Return the answer
    return ans;
}

// Driver code
public static void Main()
{

    // Input
    int N = 1454781;
    int K = 9;

    // Function call
    Console.Write(noOfWays(N, K));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate number
// of ways a number can be formed
// that has the maximum number of Ks
function noOfWays(N, K)
{

    // Convert to string
    let S = N.toString();
    let ans = 1;

    // Calculate length of subarrays
    // that can contribute to
    // the answer
    for(let i = 1; i < S.length; i++)
    {
        let count = 1;

        // Count length of subarray
        // where adjacent digits
        // add up to K
        while (i < S.length && S[i].charCodeAt() - 48 +
              S[i - 1].charCodeAt() - 48 == K)
        {
            count++;
            i++;
        }

        // Current subarray can
        // contribute to the answer
        // only if it is odd
        if (count % 2 == 1)
            ans *= Math.floor((count + 1) / 2);
    }

    // Return the answer
    return ans;
}

// Driver Code

// Input
let N = 1454781;
let K = 9;

// Function call
document.write(noOfWays(N, K));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(Log <sub>10</sub> N)，因为，N 中的位数是 Log <sub>10</sub> N*
***辅助空间:** O(1)*