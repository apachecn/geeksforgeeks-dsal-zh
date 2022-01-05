# 打印前 N 个自然数的所有不同的偶数和奇数前缀按位异或

> 原文:[https://www . geeksforgeeks . org/print-all-distinct-偶数和奇数-前缀-n 个自然数的按位异或/](https://www.geeksforgeeks.org/print-all-distinct-even-and-odd-prefix-bitwise-xors-of-first-n-natural-numbers/)

给定一个正整数 **N** ，任务是打印第一个**N**T6】自然数的前缀[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的所有不同的奇偶值。

**示例:**

> **输入:** N = 6
> **输出:**
> 偶数:0 4
> 奇数:1 3 7
> **解释:**
> 前 6 个自然数 si {1，3，0，4，1，7}的前缀按位异或。
> 偶前缀按位异或为 0，4。
> 奇数前缀按位异或是 1、3、7。
> 
> **输入:** N = 9
> **输出:**
> 偶数:0 4 8
> 奇数:1 3 7

**方法:**给定的问题可以基于以下观察来解决:

*   如果 **N 模 4** 的值是 **0** ，那么第一个 **N** 自然数的按位异或的值是 **N** 。
*   如果 **N 模 4** 的值是 **1** ，那么第一个 **N** 自然数的按位异或的值是 **1** 。
*   如果 **N 模 4** 的值是 **2** ，那么第一个 **N** 自然数的按位异或的值是 **(N + 1)** 。
*   如果 **N 模 4** 的值是 **3** ，那么第一个 **N** 自然数的按位异或的值是 **0** 。

因此，从上述原理可以说，作为偶数的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)总是作为 **0** 或 **4** 的倍数出现，作为奇数的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)总是作为小于 **4** 倍数的 **1** 或 **1** 出现。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Print all distinct even & odd
// prefix Bitwise XORs from 1 to N
void evenOddBitwiseXOR(int N)
{

    cout << "Even: " << 0 << " ";

    // Print the even number
    for (int i = 4; i <= N; i = i + 4) {
        cout << i << " ";
    }

    cout << "\n";

    cout << "Odd: " << 1 << " ";

    // Print the odd number
    for (int i = 4; i <= N; i = i + 4) {
        cout << i - 1 << " ";
    }

    if (N % 4 == 2)
        cout << N + 1;
    else if (N % 4 == 3)
        cout << N;
}

// Driver Code
int main()
{
    int N = 6;
    evenOddBitwiseXOR(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java approach for the above approach
class GFG{

// Print all distinct even & odd
// prefix Bitwise XORs from 1 to N
static void evenOddBitwiseXOR(int N)
{
    System.out.print("Even: " + 0 + " ");

    // Print the even number
    for(int i = 4; i <= N; i = i + 4)
    {
        System.out.print(i + " ");
    }

    System.out.print("\n");

    System.out.print("Odd: " + 1 + " ");

    // Print the odd number
    for(int i = 4; i <= N; i = i + 4)
    {
        System.out.print(i - 1 + " ");
    }

    if (N % 4 == 2)
        System.out.print(N + 1);
    else if (N % 4 == 3)
        System.out.print(N);
}

// Driver Code
public static void main(String[] args)
{
    int N = 6;
    evenOddBitwiseXOR(N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Print all distinct even & odd
# prefix Bitwise XORs from 1 to N
def evenOddBitwiseXOR(N):

    print("Even: ", 0, end = " ")

    # Print the even number
    for i in range(4, N + 1, 4):
        print(i, end = " ")

    print()

    print("Odd: ", 1, end = " ")

    # Print the odd number
    for i in range(4, N + 1, 4):
        print(i - 1, end = " ")

    if (N % 4 == 2):
        print(N + 1)
    elif (N % 4 == 3):
        print(N)

# Driver Code
N = 6

evenOddBitwiseXOR(N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Print all distinct even & odd
// prefix Bitwise XORs from 1 to N
static void evenOddBitwiseXOR(int N)
{
    Console.Write("Even: " + 0 + " ");

    // Print the even number
    for(int i = 4; i <= N; i = i + 4)
    {
        Console.Write(i + " ");
    }

   Console.Write("\n");

    Console.Write("Odd: " + 1 + " ");

    // Print the odd number
    for(int i = 4; i <= N; i = i + 4)
    {
        Console.Write(i - 1 + " ");
    }

    if (N % 4 == 2)
        Console.Write(N + 1);
    else if (N % 4 == 3)
        Console.Write(N);
}

// Driver code
public static void Main()
{
    int N = 6;
    evenOddBitwiseXOR(N);
}
}

// This code is contributed by splevel62
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Print all distinct even & odd
// prefix Bitwise XORs from 1 to N
function evenOddBitwiseXOR(N)
{
    document.write("Even: " + 0 + " ");

    // Print the even number
    for(let i = 4; i <= N; i = i + 4)
    {
        document.write(i + " ");
    }

    document.write("<br/>");

    document.write("Odd: " + 1 + " ");

    // Print the odd number
    for(let i = 4; i <= N; i = i + 4)
    {
       document.write(i - 1 + " ");
    }

    if (N % 4 == 2)
        document.write(N + 1);
    else if (N % 4 == 3)
        document.write(N);
}

  // Driver Code

    let N = 6;
    evenOddBitwiseXOR(N);

</script>
```

**Output:** 

```
Even: 0 4 
Odd: 1 3 7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)