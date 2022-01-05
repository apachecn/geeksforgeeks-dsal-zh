# 找出两个不同的数字，使它们的 LCM 在给定的范围内

> 原文:[https://www . geeksforgeeks . org/find-两个不同的数字-它们的 lcm 位于给定的范围内/](https://www.geeksforgeeks.org/find-two-distinct-numbers-such-that-their-lcm-lies-in-given-range/)

给定两个数字 **L** 和 **R** ，任务是找到两个不同的最小正整数 **X** 和 **Y** ，使得其 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 位于范围**【L，R】**内。如果不存在任何 X 和 Y 值，则打印**-1”**。

**示例:**

> **输入:** L = 3，R = 8
> **输出:** x = 3，y=6
> **说明:**
> 3 和 6 的 LCM 为 6，在 3，8 范围内
> 
> **输入:** L = 88，R = 90
> **输出:** -1
> **说明:**
> 最小可能的 x 和 y 分别为 88 和 176，但 176 大于 90。

**方法:**思路是选择 X 和 Y 的值，使得它们的 LCM 在给定的范围内**【L，R】**。以下是步骤:

1.  对于 **X** 的最小值，选择 **L** 作为最小值，因为这是给定范围内的最小值。
2.  现在对于 **Y** 的值选择 **2*L** ，因为这是 LCM 为 **L** 的 Y 的最小值。
3.  现在，如果 X 和 Y 的上述两个值在范围**【L，R】**内，那么这是具有 X 和 Y 的最小可能值的必需整数对
4.  否则，打印**-1”**，因为不存在任何其他对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find two distinct numbers
// X and Y s.t. their LCM lies between
// L and R  and X, Y are minimum possible
void answer(int L, int R)
{

    // Check if 2*L lies in range L, R
    if (2 * L <= R)

        // Print the answer
        cout << L << ", "
             << 2 * L << "\n";
    else
        cout << -1;
}

// Driver Code
int main()
{
    // Given value of ranges
    int L = 3, R = 8;

    // Function call
    answer(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find two distinct numbers
// X and Y s.t. their LCM lies between
// L and R and X, Y are minimum possible
static void answer(int L, int R)
{

    // Check if 2*L lies in range L, R
    if (2 * L <= R)

        // Print the answer
        System.out.println(L + ", " + (2 * L));

    else
        System.out.println("-1");
}

// Driver Code
public static void main(String[] args)
{

    // Given value of ranges
    int L = 3, R = 8;

    // Function call
    answer(L, R);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find two distinct numbers
# X and Y s.t. their LCM lies between
# L and R and X, Y are minimum possible
def answer(L, R):

    # Check if 2*L lies in range L, R
    if (2 * L <= R):

        # Print the answer
        print(L, ",", 2 * L)

    else:
        print(-1)

# Driver Code

# Given value of ranges
L = 3
R = 8

# Function call
answer(L, R)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find two distinct numbers
// X and Y s.t. their LCM lies between
// L and R and X, Y are minimum possible
static void answer(int L, int R)
{

    // Check if 2*L lies in range L, R
    if (2 * L <= R)

        // Print the answer
        Console.WriteLine(L + ", " + (2 * L));

    else
        Console.WriteLine("-1");
}

// Driver Code
public static void Main()
{

    // Given value of ranges
    int L = 3, R = 8;

    // Function call
    answer(L, R);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// JavaScript program for the above approac

// Function to find two distinct numbers
// X and Y s.t. their LCM lies between
// L and R and X, Y are minimum possible
function answer(L, R)
{

    // Check if 2*L lies in range L, R
    if (2 * L <= R)

        // Print the answer
        document.write(L + ", "
            + 2 * L + "<br>");
    else
        document.write(-1);
}

// Driver Code

    // Given value of ranges
    let L = 3, R = 8;

    // Function call
    answer(L, R);

// This code is contributed by Manoj.
</script>
```

**Output:** 

```
3, 6
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)