# 通过增加或减少 1、2 或 5 任意次数将 A 转换为 B

> 原文:[https://www . geesforgeks . org/convert-a-to-b-by-递增-或递减-1-2-或-5-任意次数/](https://www.geeksforgeeks.org/convert-a-into-b-by-incrementing-or-decrementing-1-2-or-5-any-number-of-times/)

给定两个整数 **A** 和 **B** ，任务是通过将 **A** 递增或递减 **1** 、 **2** 或 **5** 任意次数，找到使 **A** 等于 **B** 所需的最小移动次数。

**示例:**

> **输入:** A = 4，B = 0
> **输出:** 2
> **说明:**
> 执行如下操作:
> 
> 1.  将 A 的值减 2 会将 A 的值修改为(4–2)= 2。
> 2.  将 A 的值减 2 会将 A 的值修改为(2–2)= 0。等于 b。
> 
> 因此，所需的移动次数是 2。
> 
> **输入:** A = 3，B = 9
> T3】输出: 2

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。思路是先找到 **5** 的增量或减量，然后 **2** ，再需要 **1** 将 **A** 转换为 **B** 。按照以下步骤解决问题:

*   将 **A** 的值更新为 **A** 和 **B** 的绝对差值。
*   现在，将 **(A/5) + (A%5)/2 + (A%5)%2** 的值打印为 **1** 、 **2** 或 **5** 的最小增量或减量数，将 **A** 转换为 **B** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of
// moves required to convert A into B
int minimumSteps(int a, int b)
{
    // Stores the minimum number of
    // moves required
    int cnt = 0;

    // Stores the absolute
    // difference
    a = abs(a - b);

    // FInd the number of moves
    cnt = (a / 5) + (a % 5) / 2 + (a % 5) % 2;

    // Return cnt
    return cnt;
}

// Driver Code
int main()
{
    // Input
    int A = 3, B = 9;
    // Function call
    cout << minimumSteps(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find minimum number of
    // moves required to convert A into B
    static int minimumSteps(int a, int b)
    {

        // Stores the minimum number of
        // moves required
        int cnt = 0;

        // Stores the absolute
        // difference
        a = Math.abs(a - b);

        // FInd the number of moves
        cnt = (a / 5) + (a % 5) / 2 + (a % 5) % 2;

        // Return cnt
        return cnt;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int A = 3, B = 9;
        // Function call
        System.out.println(minimumSteps(A, B));
    }
}

 // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find minimum number of
# moves required to convert A into B
def minimumSteps(a, b):

    # Stores the minimum number of
    # moves required
    cnt = 0

    # Stores the absolute
    # difference
    a = abs(a - b)

    # FInd the number of moves
    cnt = (a//5) + (a % 5)//2 + (a % 5) % 2

    # Return cnt
    return cnt

# Driver Code
# Input
A = 3
B = 9

# Function call
print(minimumSteps(A, B))

# This code is contributed by amreshkumar3.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum number of
// moves required to convert A into B
static int minimumSteps(int a, int b)
{

    // Stores the minimum number of
    // moves required
    int cnt = 0;

    // Stores the absolute
    // difference
    a = Math.Abs(a - b);

    // FInd the number of moves
    cnt = (a / 5) + (a % 5) / 2 + (a % 5) % 2;

    // Return cnt
    return cnt;
}

// Driver Code
public static void Main()
{

    // Input
    int A = 3, B = 9;

    // Function call
    Console.Write(minimumSteps(A, B));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to find minimum number of
        // moves required to convert A into B
        function minimumSteps(a, b)
        {

            // Stores the minimum number of
            // moves required
            let cnt = 0;

            // Stores the absolute
            // difference
            a = Math.abs(a - b);

            // FInd the number of moves
            cnt = Math.floor(a / 5) + Math.floor((a % 5) / 2) + (a % 5) % 2;

            // Return cnt
            return cnt;
        }

        // Driver Code

        // Input
        let A = 3, B = 9;
        // Function call
        document.write(minimumSteps(A, B));

    // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)