# 根据给定的按位“与”和按位“异或”值计算两个整数的按位“或”

> 原文:[https://www . geeksforgeeks . org/从给定的按位和按位异或值计算两个整数的按位或/](https://www.geeksforgeeks.org/calculate-bitwise-or-of-two-integers-from-their-given-bitwise-and-and-bitwise-xor-values/)

给定两个整数 **X** 和 **Y** ，表示两个正整数的**按位异或**和**按位与**，任务是计算这两个正整数的**按位或**值。

**示例:**

> **输入:** X = 5，Y = 2
> **输出:** 7
> **解释:**
> 如果 a 和 b 是两个正整数，使得 A ^ B = 5，A & B = 2，那么 a 和 b 的可能值分别为 3 和 6。
> 因此，(A | B) = (3 | 6) = 7。
> 
> **输入:** X = 14，Y = 1
> **输出:** 15
> **解释:**
> 如果 a 和 b 是两个正整数，使得 A ^ B = 14，A & B = 1，那么 a 和 b 的可能值分别为 7 和 9。
> 因此，(A | B) = (7 | 9) = 15。

**天真法:**解决这个问题最简单的方法就是迭代到[的最大值 **X** 和**Y**T7】，说 **N** ，生成所有可能的第一个 **N** 自然数对。对于每一对，检查**按位异或**和该对的按位与是否分别为 **X** 和 **Y** 。如果发现为真，则打印该对的**位或**。](https://www.geeksforgeeks.org/maximum-of-two-numbers-in-python/)

***时间复杂度:** O(N <sup>2</sup> ，其中 N = max(X，Y)*
*T8】辅助空间: O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

> (a ^ b)=(a | b)–(a & b)
> =>(a | b)=(a ^ b)+(a&b)= x+y

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate Bitwise OR from given
// bitwise XOR and bitwise AND values
int findBitwiseORGivenXORAND(int X, int Y)
{
    return X + Y;
}

// Driver Code
int main()
{
    int X = 5, Y = 2;
    cout << findBitwiseORGivenXORAND(X, Y);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG {

    // Function to calculate Bitwise OR from given
    // bitwise XOR and bitwise AND values
    static int findBitwiseORGivenXORAND(int X, int Y)
    {
        return X + Y;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int X = 5, Y = 2;
        System.out.print(findBitwiseORGivenXORAND(X, Y));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate Bitwise OR from
# given bitwise XOR and bitwise AND values
def findBitwiseORGivenXORAND(X, Y):

    return X + Y

# Driver Code
if __name__ == "__main__" :

    X = 5
    Y = 2

    print(findBitwiseORGivenXORAND(X, Y))

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate Bitwise OR from given
// bitwise XOR and bitwise AND values
static int findBitwiseORGivenXORAND(int X, int Y)
{
    return X + Y;
}

// Driver Code
public static void Main(string []args)
{
    int X = 5, Y = 2;

    Console.Write(findBitwiseORGivenXORAND(X, Y));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to calculate Bitwise OR from given
// bitwise XOR and bitwise AND values
function findBitwiseORGivenXORAND(X, Y)
{
    return X + Y;
}

// Driver Code

    let X = 5, Y = 2;
    document.write(findBitwiseORGivenXORAND(X, Y));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
7
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)