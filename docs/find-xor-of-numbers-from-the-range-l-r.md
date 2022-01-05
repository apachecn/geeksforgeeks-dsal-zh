# 从范围【L，R】

中找出数字的异或运算

> 原文:[https://www . geeksforgeeks . org/find-xor-of-numbers-from-l-r/](https://www.geeksforgeeks.org/find-xor-of-numbers-from-the-range-l-r/)

给定两个整数 **L** 和 **R** ，任务是求范围**【L，R】**元素的异或。
**示例:** '

> **输入:** L = 4，R = 8
> **输出:** 8
> 4 ^ 5 ^ 6 ^ 7 ^ 8 = 8
> **输入:** L = 3，R = 7
> **输出:** 3

**天真法:**将答案初始化为零，遍历从 **L** 到 **R** 的所有数字，将数字与答案逐一进行异或运算。这需要 **O(N)** 时间。
**高效方法:**按照这里讨论的方法，我们可以在 **O(1)** 时间内从范围**【1，N】**中找到元素的异或。
使用这种方法，我们必须从范围**【1，L–1】**和范围**【1，R】**中找到元素的异或，然后再次对各自的答案进行异或，以获得范围**【L，R】**中元素的异或。这是因为范围**【1，L–1】**中的每个元素都将在结果中被异或两次，从而产生一个 **0** ，当与范围**【L，R】**中的元素异或时，将给出结果。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the XOR of elements
// from the range [1, n]
int findXOR(int n)
{
    int mod = n % 4;

    // If n is a multiple of 4
    if (mod == 0)
        return n;

    // If n % 4 gives remainder 1
    else if (mod == 1)
        return 1;

    // If n % 4 gives remainder 2
    else if (mod == 2)
        return n + 1;

    // If n % 4 gives remainder 3
    else if (mod == 3)
        return 0;
}

// Function to return the XOR of elements
// from the range [l, r]
int findXOR(int l, int r)
{
    return (findXOR(l - 1) ^ findXOR(r));
}

// Driver code
int main()
{
    int l = 4, r = 8;

    cout << findXOR(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to return the XOR of elements
    // from the range [1, n]
    static int findXOR(int n)
    {
        int mod = n % 4;

        // If n is a multiple of 4
        if (mod == 0)
            return n;

        // If n % 4 gives remainder 1
        else if (mod == 1)
            return 1;

        // If n % 4 gives remainder 2
        else if (mod == 2)
            return n + 1;

        // If n % 4 gives remainder 3
        else if (mod == 3)
            return 0;
        return 0;
    }

    // Function to return the XOR of elements
    // from the range [l, r]
    static int findXOR(int l, int r)
    {
        return (findXOR(l - 1) ^ findXOR(r));
    }

    // Driver code
    public static void main(String[] args)
    {

        int l = 4, r = 8;

            System.out.println(findXOR(l, r));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from operator import xor

# Function to return the XOR of elements
# from the range [1, n]
def findXOR(n):
    mod = n % 4;

    # If n is a multiple of 4
    if (mod == 0):
        return n;

    # If n % 4 gives remainder 1
    elif (mod == 1):
        return 1;

    # If n % 4 gives remainder 2
    elif (mod == 2):
        return n + 1;

    # If n % 4 gives remainder 3
    elif (mod == 3):
        return 0;

# Function to return the XOR of elements
# from the range [l, r]
def findXORFun(l, r):
    return (xor(findXOR(l - 1) , findXOR(r)));

# Driver code
l = 4; r = 8;

print(findXORFun(l, r));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the XOR of elements
    // from the range [1, n]
    static int findXOR(int n)
    {
        int mod = n % 4;

        // If n is a multiple of 4
        if (mod == 0)
            return n;

        // If n % 4 gives remainder 1
        else if (mod == 1)
            return 1;

        // If n % 4 gives remainder 2
        else if (mod == 2)
            return n + 1;

        // If n % 4 gives remainder 3
        else if (mod == 3)
            return 0;
        return 0;
    }

    // Function to return the XOR of elements
    // from the range [l, r]
    static int findXOR(int l, int r)
    {
        return (findXOR(l - 1) ^ findXOR(r));
    }

    // Driver code
    public static void Main()
    {

        int l = 4, r = 8;

            Console.WriteLine(findXOR(l, r));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the XOR of elements
    // from the range [1, n]
    function findxOR(n)
    {
        let mod = n % 4;

        // If n is a multiple of 4
        if (mod == 0)
            return n;

        // If n % 4 gives remainder 1
        else if (mod == 1)
            return 1;

        // If n % 4 gives remainder 2
        else if (mod == 2)
            return n + 1;

        // If n % 4 gives remainder 3
        else if (mod == 3)
            return 0;
    }

    // Function to return the XOR of elements
    // from the range [l, r]
    function findXOR(l, r)
    {
        return (findxOR(l - 1) ^ findxOR(r));
    }

    let l = 4, r = 8;
    document.write(findXOR(l, r));

</script>
```

**Output:** 

```
8
```