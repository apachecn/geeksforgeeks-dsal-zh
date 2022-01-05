# 检查两个范围中的一对整数是否存在，使得它们的按位异或超过两个范围

> 原文:[https://www . geeksforgeeks . org/check-if-two-ranges-exists-with-bitwise-xor-over-two-ranges/](https://www.geeksforgeeks.org/check-if-a-pair-of-integers-from-two-ranges-exists-such-that-their-bitwise-xor-exceeds-both-the-ranges/)

给定两个整数 **A** 和 **B** ，任务是检查在范围**【1，A】**和**【1，B】**内是否分别存在两个整数**P**和 **Q** 大于 **A** 和 **B** 。如果发现是真的，那么打印**“是”**。否则，打印**“否”**。

**示例:**

> **输入:** X = 2，Y = 2
> **输出:**是
> **解释:**
> 通过分别选择 p 和 q 的值为 1 和 2，给出 p 和 q 的按位异或为 1^2 = 3，大于 a 和 b 的按位异或 A ^ B = 0。
> 因此，打印“是”。
> 
> **输入:** X = 2，Y = 4
> T3】输出:否

**天真方法:**解决给定问题的最简单方法是[通过遍历从 **1** 到 **X** 和 **1** 到 **Y** 的所有整数来生成( **P，Q)** 的所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，并检查是否存在这样的对:它们的[按位异或](https://www.geeksforgeeks.org/tag/xor/)大于 **X** 的[按位异或](https://www.geeksforgeeks.org/tag/xor/)否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if there exists
// any pair (P, Q) whose Bitwise XOR
// is greater than the Bitwise XOR
// of X and Y
void findWinner(int X, int Y)
{
    // Stores the Bitwise XOR of X & Y
    int playerA = (X ^ Y);

    bool flag = false;

    // Traverse all possible pairs
    for (int i = 1; i <= X; i++) {

        for (int j = 1; j <= Y; j++) {

            int val = (i ^ j);

            // If a pair exists
            if (val > playerA) {
                flag = true;
                break;
            }
        }

        if (flag) {
            break;
        }
    }

    // If a pair is found
    if (flag) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driver Code
int main()
{
    int A = 2, B = 4;
    findWinner(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if there exists
// any pair (P, Q) whose Bitwise XOR
// is greater than the Bitwise XOR
// of X and Y
static void findWinner(int X, int Y)
{

    // Stores the Bitwise XOR of X & Y
    int playerA = (X ^ Y);

    boolean flag = false;

    // Traverse all possible pairs
    for(int i = 1; i <= X; i++)
    {
        for(int j = 1; j <= Y; j++)
        {
            int val = (i ^ j);

            // If a pair exists
            if (val > playerA)
            {
                flag = true;
                break;
            }
        }

        if (flag)
        {
            break;
        }
    }

    // If a pair is found
    if (flag)
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}

// Driver code
public static void main(String[] args)
{
    int A = 2, B = 4;

    findWinner(A, B);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there exists
# any pair (P, Q) whose Bitwise XOR
# is greater than the Bitwise XOR
# of X and Y
def findWinner(X, Y):

    # Stores the Bitwise XOR of X & Y
    playerA = (X ^ Y)

    flag = False

    # Traverse all possible pairs
    for i in range(1, X + 1, 1):
        for j in range(1, Y + 1, 1):
            val = (i ^ j)

            # If a pair exists
            if (val > playerA):
                flag = True
                break

        if (flag):
            break

    # If a pair is found
    if (flag):
        print("Yes")
    else:
        print("No")

# Driver Code
if __name__ == '__main__':

    A = 2
    B = 4

    findWinner(A, B)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to check if there exists
// any pair (P, Q) whose Bitwise XOR
// is greater than the Bitwise XOR
// of X and Y
static void findWinner(int X, int Y)
{

    // Stores the Bitwise XOR of X & Y
    int playerA = (X ^ Y);

    bool flag = false;

    // Traverse all possible pairs
    for(int i = 1; i <= X; i++)
    {
        for(int j = 1; j <= Y; j++)
        {
            int val = (i ^ j);

            // If a pair exists
            if (val > playerA)
            {
                flag = true;
                break;
            }
        }

        if (flag)
        {
            break;
        }
    }

    // If a pair is found
    if (flag)
    {
        Console.WriteLine("Yes");
    }
    else
    {
        Console.WriteLine("No");
    }
}

// Driver code
public static void Main(String[] args)
{
    int A = 2, B = 4;

    findWinner(A, B);
}
}

// This code is contributed by amreshkumar3
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if there exists
// any pair (P, Q) whose Bitwise XOR
// is greater than the Bitwise XOR
// of X and Y
function findWinner(X,Y)
{
    // Stores the Bitwise XOR of X & Y
    let playerA = (X ^ Y);

    let flag = false;

    // Traverse all possible pairs
    for(let i = 1; i <= X; i++)
    {
        for(let j = 1; j <= Y; j++)
        {
            let val = (i ^ j);

            // If a pair exists
            if (val > playerA)
            {
                flag = true;
                break;
            }
        }

        if (flag)
        {
            break;
        }
    }

    // If a pair is found
    if (flag)
    {
        document.write("Yes<br>");
    }
    else
    {
        document.write("No<br>");
    }
}

// Driver code
let A = 2, B = 4;

findWinner(A, B);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
No
```

***时间复杂度:** O(X * Y)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以基于以下观察进行优化:

*   对于任意两个整数 **P** 和 **Q** ，最大**按位异或**值为 **(P + Q)** ，只有当 **P** 和 **Q** 在其[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)中没有公共位时才能找到。
*   有两种情况:
    *   **情况 1:** 如果玩家 A 有两个产生最大按位异或值的整数，则打印**“否”**。
    *   **情况 2:** 在这种情况下， **A** 和 **B** 之间必须有一些公共位，这样总会存在两个整数 **P** 和 **Q** ，它们的按位异或总是大于 **A** 和 **B** 的按位异或，其中 **(P ^ Q) = (X | Y)** 。

因此，从上面的观察来看，想法是检查给定的 **A^B** 的值是否等于 **A + B** 。如果发现属实，则打印**“否”**。否则，打印**“是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if there exists
// any pair (P, Q) whose Bitwise XOR
// is greater than the Bitwise XOR
// of X and Y
void findWinner(int X, int Y)
{
    int first = (X ^ Y);
    int second = (X + Y);

    // Check for the invalid condition
    if (first == second) {
        cout << "No";
    }

    // Otherwise,
    else {
        cout << "Yes";
    }
}

// Driver Code
int main()
{
    int A = 2, B = 4;
    findWinner(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if there exists
// any pair (P, Q) whose Bitwise XOR
// is greater than the Bitwise XOR
// of X and Y
static void findWinner(int X, int Y)
{
    int first = (X ^ Y);
    int second = (X + Y);

    // Check for the invalid condition
    if (first == second)
    {
        System.out.println("No");
    }

    // Otherwise,
    else
    {
        System.out.println("Yes");
    }
}

// Driver code
public static void main(String[] args)
{
    int A = 2, B = 4;

    findWinner(A, B);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if there exists
# any pair (P, Q) whose Bitwise XOR
# is greater than the Bitwise XOR
# of X and Y
def findWinner(X, Y):

    first = (X ^ Y)
    second = (X + Y)

    # Check for the invalid condition
    if (first == second):
        print ("No")

    # Otherwise,
    else:
        print ("Yes")

# Driver Code
if __name__ == '__main__':

    A, B = 2, 4

    findWinner(A, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if there exists
// any pair (P, Q) whose Bitwise XOR
// is greater than the Bitwise XOR
// of X and Y
static void findWinner(int X, int Y)
{
    int first = (X ^ Y);
    int second = (X + Y);

    // Check for the invalid condition
    if (first == second)
    {
        Console.Write("No");
    }

    // Otherwise,
    else
    {
        Console.Write("Yes");
    }
}

// Driver code
public static void Main(String[] args)
{
    int A = 2, B = 4;

    findWinner(A, B);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to check if there exists
// any pair (P, Q) whose Bitwise XOR
// is greater than the Bitwise XOR
// of X and Y
function findWinner(X,Y)
{
    let first = (X ^ Y);
    let second = (X + Y);

    // Check for the invalid condition
    if (first == second) {
        document.write("No");
    }

    // Otherwise,
    else {
        document.write("Yes");
    }
}

// Driver Code
let A = 2, B = 4;
findWinner(A, B);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
No
```

***时间复杂度:** O(1)*
***辅助空间:*** *O(1)*