# 生成没有任何连续 0 且最多 K 个连续 1 的二进制字符串

> 原文:[https://www . geesforgeks . org/generate-a-binary-string-不带任何连续 0 和最多 k 个连续 1/](https://www.geeksforgeeks.org/generate-a-binary-string-without-any-consecutive-0s-and-at-most-k-consecutive-1s/)

给定两个整数 **N** 和 **M** ，任务是用以下条件构造一个二进制字符串:

*   二进制字符串由 **N** 0 和 **M** 1 组成
*   二进制字符串最多有 **K** 个连续的 1
*   二进制字符串不包含任何相邻的 0

如果无法构造这样的二进制字符串，则打印 **-1** 。

**例:**

> **输入:** N = 5，M = 9，K = 2
> **输出:** 01101101101101
> **说明:**
> 字符串“01101101101101”满足以下条件:
> 
> *   不存在连续的 0。
> *   出现的连续 1 不超过 K(= 2)。
> 
> **输入:** N = 4，M = 18，K = 4
> **输出:**110111101111101110111

**进场:**

要构造满足给定属性的二进制字符串，请观察以下内容:

*   如果没有两个“ **0** 连续的*，它们之间应该至少有一个“ **1** ”。*
*   *因此，对于“ **0** 的 **N** 号，至少应有**N-1**“**1**存在，以生成所需类型的字符串。*
*   *由于不超过 **K** 个连续的‘**1**可以放在一起，对于 **N** 0，最多可以有 **(N+1) * K '1** 个可能。*
*   *因此，‘**1**的数量应该在范围内:* 

> ***N–1？m？(N + 1) * K***

*   *如果给定值 **N** 和 **M** 不满足上述条件，则打印 **-1** 。*
*   *否则，请按照以下步骤解决问题:

    *   将' **0** 附加到最终字符串中。
    *   在每对****0′**之间插入“ **1** ，从 **M** 中减去**N–1**，因为**N–1****1**已经放置。**
    *   **对于剩余的“ **1** ，将***min(K–1，M)*****1**放置在每个已放置的“ **1** 旁边，以确保不超过**K**1 放置在一起。**
    *   **对于任何剩余的“ **1** ，将它们追加到最终字符串的开始和结束。*** 
*   ***最后，打印生成的字符串。***

***下面是上述方法的实现:***

## ***C++***

```
***// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct the binary string
string ConstructBinaryString(int N, int M,
                             int K)
{
    // Conditions when string construction
    // is not possible
    if (M < (N - 1) || M > K * (N + 1))
        return "-1";

    string ans = "";

    // Stores maximum 1's that
    // can be placed in between
    int l = min(K, M / (N - 1));
    int temp = N;
    while (temp--) {
        // Place 0's
        ans += '0';

        if (temp == 0)
            break;

        // Place 1's in between
        for (int i = 0; i < l; i++) {
            ans += '1';
        }
    }

    // Count remaining M's
    M -= (N - 1) * l;

    if (M == 0)
        return ans;

    l = min(M, K);
    // Place 1's at the end
    for (int i = 0; i < l; i++)
        ans += '1';

    M -= l;
    // Place 1's at the beginning
    while (M > 0) {
        ans = '1' + ans;
        M--;
    }

    // Return the final string
    return ans;
}

// Driver Code
int main()
{
    int N = 5, M = 9, K = 2;

    cout << ConstructBinaryString(N, M, K);
}***
```

## ***Java 语言(一种计算机语言，尤用于创建网站)***

```
***// Java implementation of
// the above approach
class GFG{

// Function to construct the binary string
static String ConstructBinaryString(int N, int M,
                                    int K)
{

    // Conditions when string construction
    // is not possible
    if (M < (N - 1) || M > K * (N + 1))
        return "-1";

    String ans = "";

    // Stores maximum 1's that
    // can be placed in between
    int l = Math.min(K, M / (N - 1));
    int temp = N;

    while (temp != 0)
    {
        temp--;

        // Place 0's
        ans += '0';

        if (temp == 0)
            break;

        // Place 1's in between
        for(int i = 0; i < l; i++)
        {
            ans += '1';
        }
    }

    // Count remaining M's
    M -= (N - 1) * l;

    if (M == 0)
        return ans;

    l = Math.min(M, K);

    // Place 1's at the end
    for(int i = 0; i < l; i++)
        ans += '1';

    M -= l;

    // Place 1's at the beginning
    while (M > 0)
    {
        ans = '1' + ans;
        M--;
    }

    // Return the final string
    return ans;
}

// Driver code   
public static void main(String[] args)
{
    int N = 5, M = 9, K = 2;

    System.out.println(ConstructBinaryString(N, M, K));
}
}

// This code is contributed by rutvik_56***
```

## ***蟒蛇 3***

```
***# Python3 implementation of
# the above approach

# Function to construct the binary string
def ConstructBinaryString(N, M, K):

    # Conditions when string construction
    # is not possible
    if(M < (N - 1) or M > K * (N + 1)):
        return '-1'

    ans = ""

    # Stores maximum 1's that
    # can be placed in between
    l = min(K, M // (N - 1))
    temp = N

    while(temp):
        temp -= 1

        # Place 0's
        ans += '0'

        if(temp == 0):
            break

        # Place 1's in between
        for i in range(l):
            ans += '1'

    # Count remaining M's
    M -= (N - 1) * l

    if(M == 0):
        return ans

    l = min(M, K)

    # Place 1's at the end
    for i in range(l):
        ans += '1'

    M -= l

    # Place 1's at the beginning
    while(M > 0):
        ans = '1' + ans
        M -= 1

    # Return the final string
    return ans

# Driver Code
if __name__ == '__main__':

    N = 5
    M = 9
    K = 2

    print(ConstructBinaryString(N, M , K))

# This code is contributed by Shivam Singh***
```

## ***C#***

```
***// C# implementation of
// the above approach
using System;
class GFG{

// Function to construct the binary string
static String ConstructBinaryString(int N, int M,
                                    int K)
{

    // Conditions when string construction
    // is not possible
    if (M < (N - 1) || M > K * (N + 1))
        return "-1";

    string ans = "";

    // Stores maximum 1's that
    // can be placed in between
    int l = Math.Min(K, M / (N - 1));
    int temp = N;

    while (temp != 0)
    {
        temp--;

        // Place 0's
        ans += '0';

        if (temp == 0)
            break;

        // Place 1's in between
        for(int i = 0; i < l; i++)
        {
            ans += '1';
        }
    }

    // Count remaining M's
    M -= (N - 1) * l;

    if (M == 0)
        return ans;

    l = Math.Min(M, K);

    // Place 1's at the end
    for(int i = 0; i < l; i++)
        ans += '1';

    M -= l;

    // Place 1's at the beginning
    while (M > 0)
    {
        ans = '1' + ans;
        M--;
    }

    // Return the final string
    return ans;
}

// Driver code   
public static void Main(string[] args)
{
    int N = 5, M = 9, K = 2;

    Console.Write(ConstructBinaryString(N, M, K));
}
}

// This code is contributed by Ritik Bansal***
```

## ***java 描述语言***

```
***<script>
// JavaScript program for the above approach

// Function to construct the binary string
function ConstructBinaryString(N, M, K)
{

    // Conditions when string construction
    // is not possible
    if (M < (N - 1) || M > K * (N + 1))
        return "-1";

    let ans = "";

    // Stores maximum 1's that
    // can be placed in between
    let l = Math.min(K, M / (N - 1));
    let temp = N;

    while (temp != 0)
    {
        temp--;

        // Place 0's
        ans += '0';

        if (temp == 0)
            break;

        // Place 1's in between
        for(let i = 0; i < l; i++)
        {
            ans += '1';
        }
    }

    // Count remaining M's
    M -= (N - 1) * l;

    if (M == 0)
        return ans;

    l = Math.min(M, K);

    // Place 1's at the end
    for(let i = 0; i < l; i++)
        ans += '1';

    M -= l;

    // Place 1's at the beginning
    while (M > 0)
    {
        ans = '1' + ans;
        M--;
    }

    // Return the final string
    return ans;
}

// Driver Code   

        let N = 5, M = 9, K = 2;

    document.write(ConstructBinaryString(N, M, K));

</script>***
```

*****Output:** 

```
01101101101101
```*** 

******时间复杂度:** O(N+M)*
***辅助空间:** O(N+M)****