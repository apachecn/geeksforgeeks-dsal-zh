# 将由“11”组成的 N 长度二进制串计为子串

> 原文:[https://www . geesforgeks . org/count-n-length-binary-strings-由-11 组成-as-substring/](https://www.geeksforgeeks.org/count-n-length-binary-strings-consisting-of-11-as-substring/)

给定一个正整数 **N** ，任务是找到长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)的数量，其中包含**“11”**作为子字符串。

**示例:**

> **输入:** N = 2
> **输出:** 1
> **解释:**长度为 2 的字符串中唯一以“11”作为子串的是“11”。
> 
> **输入:**N = 12
> T3】输出: 3719

**方法:**想法是基于以下观察，导出将**“11”**作为以 **0** 或 **1** 开始的二进制表示的子串的可能性数量:

*   如果第一个位是 **0** ，那么起始位对具有**“11”**作为[子串](https://www.geeksforgeeks.org/substring-in-cpp/)的串没有贡献。因此，剩余的**(N–1)位**必须形成一个以**“11**”为子串的字符串。
*   如果第一个位是 **1** ，后面的位也是 **1** ，那么就存在**2<sup>(N–2)</sup>**个以**“11”**为子串的字符串。
*   如果第一个位是 **1** 但是后面的位是 **0** ，那么可以用剩余的**(N–2)位**形成一个以**“11”**为子串的字符串。
*   因此，生成所有长度为 **N** 的二进制字符串的递归关系为:

> DP[I]= DP[I–1]+DP[I–2]+2<sup>(I–2)</sup>
> 其中，
> dp[i]是长度为 I 的字符串，以“11”作为子字符串。
> 和 dp[0] = dp[1] = 0。

按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，称之为 **dp[]** ，大小为 **(N + 1)** ，将 **dp[0]** 指定为 **0** ，将 **dp[1]** 指定为 **0** 。
*   预计算**2**T5 的第一**N**T2【乘方】并将其存储在数组中，比如**乘方[]** 。
*   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【2，N】**并将 **dp[i]** 更新为**(DP[I–1]+DP[I–2]+功率[I–2])**。
*   完成上述步骤后，打印**DP【N】**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count binary strings
// of length N having substring "11"
void binaryStrings(int N)
{
    // Initialize dp[] of size N + 1
    int dp[N + 1];

    // Base Cases
    dp[0] = 0;
    dp[1] = 0;

    // Iterate over the range [2, N]
    for (int i = 2; i <= N; i++) {
        dp[i] = dp[i - 1]
                + dp[i - 2]       
                + (1<<(i-2));   // 1<<(i-2) means power of 2^(i-2)
    }

    // Print total count of substrings
    cout << dp[N];
}

// Driver Code
int main()
{
    int N = 12;
    binaryStrings(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count binary strings
// of length N having substring "11"
static void binaryStrings(int N)
{

    // Initialize dp[] of size N + 1
    int[] dp = new int[N + 1];

    // Base Cases
    dp[0] = 0;
    dp[1] = 0;

    // Stores the first N powers of 2
    int[] power = new int[N + 1];
    power[0] = 1;

    // Generate
    for(int i = 1; i <= N; i++)
    {
        power[i] = 2 * power[i - 1];
    }

    // Iterate over the range [2, N]
    for(int i = 2; i <= N; i++)
    {
        dp[i] = dp[i - 1] + dp[i - 2] + power[i - 2];
    }

    // Print total count of substrings
    System.out.println(dp[N]);
}

// Driver Code
public static void main(String[] args)
{
    int N = 12;

    binaryStrings(N);
}
}

// This code is contributed by ukasp
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count binary strings
# of length N having substring "11"
def binaryStrings(N):

    # Initialize dp[] of size N + 1
    dp = [0]*(N + 1)

    # Base Cases
    dp[0] = 0
    dp[1] = 0

    # Stores the first N powers of 2
    power = [0]*(N + 1)
    power[0] = 1

    # Generate
    for i in range(1, N + 1):
        power[i] = 2 * power[i - 1]

    # Iterate over the range [2, N]
    for i in range(2, N + 1):
        dp[i] = dp[i - 1] + dp[i - 2] + power[i - 2]

    # Prtotal count of substrings
    print (dp[N])

# Driver Code
if __name__ == '__main__':
    N = 12
    binaryStrings(N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to count binary strings
  // of length N having substring "11"
  static void binaryStrings(int N)
  {

    // Initialize dp[] of size N + 1
    int []dp = new int[N + 1];

    // Base Cases
    dp[0] = 0;
    dp[1] = 0;

    // Stores the first N powers of 2
    int []power = new int[N + 1];
    power[0] = 1;

    // Generate
    for (int i = 1; i <= N; i++) {
      power[i] = 2 * power[i - 1];
    }

    // Iterate over the range [2, N]
    for (int i = 2; i <= N; i++) {
      dp[i] = dp[i - 1]
        + dp[i - 2]
        + power[i - 2];
    }

    // Print total count of substrings
    Console.WriteLine(dp[N]);
  }

  // Driver Code
  public static void Main()
  {
    int N = 12;
    binaryStrings(N);
  }
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

    // Function to count binary strings
    // of length N having substring "11"
    function binaryStrings(N) {

        // Initialize dp of size N + 1
        var dp = Array(N + 1).fill(0);

        // Base Cases
        dp[0] = 0;
        dp[1] = 0;

        // Stores the first N powers of 2
        var power = Array(N+1).fill(0);
        power[0] = 1;

        // Generate
        for (i = 1; i <= N; i++) {
            power[i] = 2 * power[i - 1];
        }

        // Iterate over the range [2, N]
        for (i = 2; i <= N; i++) {
            dp[i] = dp[i - 1] + dp[i - 2] + power[i - 2];
        }

        // Print total count of substrings
        document.write(dp[N]);
    }

    // Driver Code

        var N = 12;

        binaryStrings(N);

// This code contributed by aashish1995

</script>
```

**Output**

```
3719
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)