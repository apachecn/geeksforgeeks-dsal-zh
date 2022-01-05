# 从 K 开始生成 N 位格雷码

> 原文:[https://www . geesforgeks . org/generating-n-bit-grey-code-from-k/](https://www.geeksforgeeks.org/generating-n-bit-grey-code-starting-from-k/)

给定一个值 **N** 和 **K** ，任务是从值 K 开始生成 N 位格雷码
**示例:**

> **输入:** N = 2，K = 3
> **输出:** 3 2 0 1
> **解释:**
> 3->11
> 2->10
> 0->00
> 1->01
> 每个值与其二进制表示中的下一个值仅相差一位。
> **输入:** N = 3，K = 2
> **输出:** 2 3 1 0 4 5 7 6

**进场:**

*   [格雷码](https://www.geeksforgeeks.org/generate-n-bit-gray-codes/)是两个连续数字之间有[汉明距离](https://www.geeksforgeeks.org/hamming-distance-between-two-integers/) 1 的数字。

*   与 N 位格雷码的每个元素的异或生成汉明距离为 1 的序列。

*   由于 n 位格雷码的第一个元素是 k，所以可以通过与 0 进行 is XOR 运算得到，即(k ^ 0)= k。

*   因此，序列将以 0 开始，每个连续的元素在其二进制表示中仅相差一位。

以下是上述方法的实现:

## C++

```
// C++ program Generating N-bit
// Gray Code starting from K

#include <bits/stdc++.h>
using namespace std;

// Function to Generating N-bit
// Gray Code starting from K
void genSequence(int n, int val)
{

    for (int i = 0; i < (1 << n); i++) {

        // Generate gray code of corresponding
        // binary number of integer i.
        int x = i ^ (i >> 1) ^ val;
        cout << x << " ";
    }
}

// Driver code
int main()
{
    int n = 3, k = 2;
    genSequence(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program Generating N-bit
// Gray Code starting from K

class GFG {

    // Function to Generating N-bit
    // Gray Code starting from K
    static void genSequence(int n, int val)
    {

        for (int i = 0; i < (1 << n); i++) {

            // Generate gray code of corresponding
            // binary number of integer i.
            int x = i ^ (i >> 1) ^ val;
            System.out.print(x + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 3, k = 2;
        genSequence(n, k);

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program Generating N-bit
# Gray Code starting from K

# Function to Generating N-bit
# Gray Code starting from K
def genSequence(n, val) :

    for i in range(1 << n) :

        # Generate gray code of corresponding
        # binary number of integer i.
        x = i ^ (i >> 1) ^ val;
        print(x, end= " ");

# Driver code
if __name__ == "__main__" :

    n = 3; k = 2;
    genSequence(n, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program Generating N-bit
// Gray Code starting from K
using System;

class GFG
{

    // Function to Generating N-bit
    // Gray Code starting from K
    static void genSequence(int n, int val)
    {

        for (int i = 0; i < (1 << n); i++)
        {

            // Generate gray code of corresponding
            // binary number of integer i.
            int x = i ^ (i >> 1) ^ val;
            Console.Write(x + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 3, k = 2;
        genSequence(n, k);

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript program Generating N-bit
// Gray Code starting from K

// Function to Generating N-bit
// Gray Code starting from K
function genSequence(n, val)
{

    for (let i = 0; i < (1 << n); i++) {

        // Generate gray code of corresponding
        // binary number of integer i.
        let x = i ^ (i >> 1) ^ val;
        document.write(x + " ");
    }
}

// Driver code
    let n = 3, k = 2;
    genSequence(n, k);

</script>
```

**Output:** 

```
2 3 1 0 4 5 7 6
```