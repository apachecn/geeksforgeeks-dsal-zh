# 计算 N 位数字，使每个位置都能被该位置的数字整除

> 原文:[https://www . geesforgeks . org/count-n-digits-numbers-这样每个位置都可以被该位置的数字整除/](https://www.geeksforgeeks.org/count-n-digit-numbers-such-that-every-position-is-divisible-by-the-digit-at-that-position/)

给定一个正整数 **N** ，任务是计算 **N** 位数字的个数，使得数字中的每个索引*(基于 1 的索引)*都可以被该索引处出现的数字整除。既然球场可以很大，那就打印出来[模 **10 <sup>9</sup> + 7**](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** N = 2
> **输出:** 2
> **说明:**数字 11 和 12 是唯一满足条件的两位数。
> 
> **输入:**N = 5
> T3】输出: 24

**天真方法:**解决问题最简单的方法是生成所有可能的 **N** 位数字，对于每个这样的数字，检查其所有数字是否满足要求的条件。

***时间复杂度:**O(10<sup>N</sup>* N)*
***辅助空间:** O(1)*

**高效进场:**优化上述进场，思路是观察每个位置，从 1 到 9 有 9 个可能的选择。检查每一个可能的选项，并找到结果。
按照以下步骤解决这个问题:

*   将变量**和**初始化为 **1** 来存储答案。
*   [使用变量**索引**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并执行以下任务:
    *   初始化变量，将**选项**设为 **0，**以存储特定索引的选项数量。
    *   [使用变量**数字**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，9】**，并执行以下任务:
        *   如果**指数百分比数字**等于 **0，**则将**选项**的值增加 **1。**
    *   将 **ans** 的值设置为**(ans * 1LL *选项)%mod** 。
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;

// Function to count N-digit numbers
// such that each position is divisible
// by the digit occurring at that position
void countOfNumbers(int N)
{
    // Stores the answer.
    int ans = 1;

    // Iterate from indices 1 to N
    for (int index = 1; index <= N; ++index) {

        // Stores count of digits that can
        // be placed at the current index
        int choices = 0;

        // Iterate from digit 1 to 9
        for (int digit = 1; digit <= 9; ++digit) {

            // If index is divisible by digit
            if (index % digit == 0) {
                ++choices;
            }
        }

        // Multiply answer with possible choices
        ans = (ans * 1LL * choices) % mod;
    }

    cout << ans << endl;
}

// Driver Code
int main()
{
    // Given Input
    int N = 5;

    // Function call
    countOfNumbers(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

static int mod = 1000000007;

// Function to count N-digit numbers
// such that each position is divisible
// by the digit occurring at that position
static void countOfNumbers(int N)
{

    // Stores the answer.
    int ans = 1;

    // Iterate from indices 1 to N
    for(int index = 1; index <= N; ++index)
    {

        // Stores count of digits that can
        // be placed at the current index
        int choices = 0;

        // Iterate from digit 1 to 9
        for(int digit = 1; digit <= 9; ++digit)
        {

            // If index is divisible by digit
            if (index % digit == 0)
            {
                ++choices;
            }
        }

        // Multiply answer with possible choices
        ans = (ans * choices) % mod;
    }
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int N = 5;

    // Function call
    countOfNumbers(N);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# python program for the above approach
mod = 1000000000 + 7

# Function to count N-digit numbers
# such that each position is divisible
# by the digit occurring at that position
def countOfNumbers(N):

    # Stores the answer.
    ans = 1

    # Iterate from indices 1 to N
    for index in range(1, N + 1):

        # Stores count of digits that can
        # be placed at the current index
        choices = 0

        # Iterate from digit 1 to 9
        for digit in range(1, 10):

            # If index is divisible by digit
            if (index % digit == 0):
                choices += 1

        # Multiply answer with possible choices
        ans = (ans * choices) % mod
    print(ans)

# Driver Code

# Given Input
N = 5

# Function call
countOfNumbers(N)

# This code is contributed by amreshkumar3.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  static int mod = 1000000007;

// Function to count N-digit numbers
// such that each position is divisible
// by the digit occurring at that position
static void countOfNumbers(int N)
{
    // Stores the answer.
    int ans = 1;

    // Iterate from indices 1 to N
    for (int index = 1; index <= N; ++index) {

        // Stores count of digits that can
        // be placed at the current index
        int choices = 0;

        // Iterate from digit 1 to 9
        for (int digit = 1; digit <= 9; ++digit) {

            // If index is divisible by digit
            if (index % digit == 0) {
                ++choices;
            }
        }

        // Multiply answer with possible choices
        ans = (ans * choices) % mod;
    }

    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    // Given Input
    int N = 5;

    // Function call
    countOfNumbers(N);
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach
        const mod = 1e9 + 7;

        // Function to count N-digit numbers
        // such that each position is divisible
        // by the digit occurring at that position
        function countOfNumbers(N)
        {

            // Stores the answer.
            let ans = 1;

            // Iterate from indices 1 to N
            for (let index = 1; index <= N; ++index) {

                // Stores count of digits that can
                // be placed at the current index
                let choices = 0;

                // Iterate from digit 1 to 9
                for (let digit = 1; digit <= 9; ++digit) {

                    // If index is divisible by digit
                    if (index % digit == 0) {
                        ++choices;
                    }
                }

                // Multiply answer with possible choices
                ans = (ans * 1 * choices) % mod;
            }

            document.write(ans);
        }

        // Driver Code

        // Given Input
        let N = 5;

        // Function call
        countOfNumbers(N);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
24
```

***时间复杂度:** O(10 * N)*
***辅助空间:** O(1)*