# 计算将甲转换为乙所需的最小移动次数

> 原文:[https://www . geesforgeks . org/count-最小移动-需要转换为 a-b/](https://www.geeksforgeeks.org/count-minimum-moves-required-to-convert-a-to-b/)

给定两个整数 **A** 和 **B** ，通过多次执行以下操作之一，将 **A** 转换为 **B** :

*   **A = A + K**
*   **A = A–K**，其中 **K** 属于**【1，10】**

任务是找到使用上述操作将 **A** 转换为 **B** 所需的最小操作数。

**示例:**

> **输入:** A = 13，B = 42
> **输出:** 3
> **说明:**
> 可以进行以下顺序的招式:13 → 23 → 32 → 42(加 10，加 9，加 10)。
> 
> **输入:** A = 18，B = 4
> **输出:** 2
> **说明:**
> 可以进行如下的招式顺序:18 → 10 → 4(减 8，减 6)。

**方法:**思路是将 **A** 和 **B** 的[绝对差](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)除以**【1…10】**范围内的所有数字，并将其加到合成变量中，简单计算出所需的移动次数。按照以下步骤解决问题:

*   初始化一个变量 **required_moves** 来存储所需的最小移动次数。
*   求 **A** 和 **B** 的绝对差。
*   迭代范围**【1，10】**并执行以下操作:
    *   将该数除以 **i** ，并将其加到结果变量中。
    *   通过 **i** 计算绝对差的[模](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/)。
*   最后，打印**所需 _ 移动**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number
// of moves to obtained B from A
void convertBfromA(int a, int b)
{
    // Stores the minimum
    // number of moves
    int moves = 0;

    // Absolute difference
    int x = abs(a - b);

    // K is in range [0, 10]
    for (int i = 10; i > 0; i--) {
        moves += x / i;
        x = x % i;
    }

    // Print the required moves
    cout << moves << " ";
}

// Driver Code
int main()
{
    int A = 188, B = 4;

    convertBfromA(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find minimum number
// of moves to obtained B from A
static void convertBfromA(int a, int b)
{

    // Stores the minimum
    // number of moves
    int moves = 0;

    // Absolute difference
    int x = Math.abs(a - b);

    // K is in range [0, 10]
    for(int i = 10; i > 0; i--)
    {
        moves += x / i;
        x = x % i;
    }

    // Print the required moves
    System.out.print(moves + " ");
}

// Driver Code
public static void main (String[] args)
{
    int A = 188, B = 4;

    convertBfromA(A, B);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum number
# of moves to obtained B from A
def convertBfromA(a, b):

    # Stores the minimum
    # number of moves
    moves = 0

    # Absolute difference
    x = abs(a - b)

    # K is in range [0, 10]
    for i in range(10, 0, -1):
        moves += x // i
        x = x % i

    # Print the required moves
    print(moves, end = " ")

# Driver Code
A = 188
B = 4

convertBfromA(A, B)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function to find minimum number
// of moves to obtained B from A
static void convertBfromA(int a, int b)
{

    // Stores the minimum
    // number of moves
    int moves = 0;

    // Absolute difference
    int x = Math.Abs(a - b);

    // K is in range [0, 10]
    for(int i = 10; i > 0; i--)
    {
        moves += x / i;
        x = x % i;
    }

    // Print the required moves
    Console.Write(moves + " ");
}

// Driver Code
public static void Main ()
{
    int A = 188, B = 4;

    convertBfromA(A, B);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find minimum number
// of moves to obtained B from A
function convertBfromA(a, b)
{

    // Stores the minimum
    // number of moves
    let moves = 0;

    // Absolute difference
    let x = Math.abs(a - b);

    // K is in range [0, 10]
    for(let i = 10; i > 0; i--)
    {
        moves += Math.floor(x / i);
        x = x % i;
    }

    // Print the required moves
    document.write(moves + " ");
}

// Driver Code

    let A = 188, B = 4;

    convertBfromA(A, B);

</script>
```

**Output:** 

```
19
```

***时间复杂度:** O(K)，其中 K 在范围【0，10】*
***辅助空间:** O(1)*