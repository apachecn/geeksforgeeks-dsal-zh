# 构造一个从 X 开始的前缀异或数组为 N 长度递增序列的数组

> 原文:[https://www . geesforgeks . org/construct-a-array-what-prefix-xor-array-from-x-is-n-length-递增序列/](https://www.geeksforgeeks.org/construct-an-array-whose-prefix-xor-array-starting-from-x-is-an-n-length-increasing-sequence/)

给定两个整数 **N** 和 **X** ，任务是**生成一个大小为 N** 的 [**数组**](https://www.geeksforgeeks.org/array-data-structure/) **，这样 X 的 [**前缀**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **异或数组**与生成的数组将是前 N 个自然数的[**排列**](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/) **。****

**示例:**

> **输入:** N = 4，X = 3
> **输出:**【2，3，1，7】
> **说明:**数组{2，3，1，7}的前缀 XOR 数组如下:
> 
> 1.  X ⊕ 2 = 1。现在，X = 1
> 2.  X ⊕ 3 = 2。现在，X = 2
> 3.  X ⊕ 1 = 3。现在，X = 3
> 4.  X ⊕ 7 = 4。现在，X = 4
> 
> 数组[1，2，3，4]是前 4 个自然数的排列。
> 
> **输入:** N = 7，X = 52
> **输出:**【53，3，1，7，1，3，1】

**方法:**这个问题可以使用 XOR 的 [**属性来解决(*如果 **x ⊕ a = b** ，那么 **x ⊕ b = a*** )。假设生成数组中元素与 **X** 的异或运算直到 **i <sup>th</sup>** 索引为 **X** ，生成数组中 **(i + 1) <sup>th</sup>** 元素为 **B** ，则 **B** 可以通过以下步骤计算:**](https://www.geeksforgeeks.org/introduction-of-logic-gates/)

> **X ⊕ B = i + 1**
> 根据问题陈述，使用 XOR 的性质(如果 x⊕ a = b 那么，x⊕b = a)……
> **x⊕I+1 = b**
> 或
> **B = X ⊕ i + 1，这是 B** 的要求值。

按照以下步骤解决问题:

*   初始化一个变量，说 **prev_xor** 为 **X** 。
*   使用变量迭代一个循环，比如说 **i** ，从 **1** 到 **N** 并打印 **prev_xor ⊕ i** 。
*   更新 **prev_xor 为 i** 。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required array
void GenerateArray(int N, int X)
{
    int prev_xor = X;

    // Iterative from 1 to N
    for (int i = 1; i <= N; i++) {

        // Print the i-th element
        cout << (i ^ prev_xor);

        if (i != N) {
            cout << " ";
        }

        // Update prev_xor to i
        prev_xor = i;
    }
}

// Driver Code
int main()
{
    // Given Input
    int N = 4, X = 3;

    // Function Call
    cout << "The generated array is ";
    GenerateArray(N, X);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

  // Function to print the required array
  static void GenerateArray(int N, int X)
  {
    int prev_xor = X;

    // Iterative from 1 to N
    for (int i = 1; i <= N; i++) {

      // Print the i-th element
      System.out.print(i ^ prev_xor);

      if (i != N) {
        System.out.print(" ");
      }

      // Update prev_xor to i
      prev_xor = i;
    }
  }

  // Driver Code
  public static void main(String args[]) {

    // Given Input
    int N = 4, X = 3;

    // Function Call
    System.out.print("The generated array is ");
    GenerateArray(N, X);
  }
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to print the required array
def GenerateArray(N, X):
    prev_xor = X

    # Iterative from 1 to N
    for i in range(1,N+1,1):
        # Print the i-th element
        print(i ^ prev_xor,end="")

        if (i != N):
            print(" ",end="")

        # Update prev_xor to i
        prev_xor = i

# Driver Code
if __name__ == '__main__':
    # Given Input
    N = 4
    X = 3

    # Function Call
    print("The generated array is ",end="")
    GenerateArray(N, X)

    # This code is contributed by ipg2016107
```

## C#

```
// C# program for above approach
using System;
class GFG
{

// Function to print the required array
static void GenerateArray(int N, int X)
{
    int prev_xor = X;

    // Iterative from 1 to N
    for (int i = 1; i <= N; i++) {

        // Print the i-th element
        Console.Write(i ^ prev_xor);

        if (i != N) {
            Console.Write(" ");
        }

        // Update prev_xor to i
        prev_xor = i;
    }
}

// Driver Code
static void Main()
{

    // Given Input
    int N = 4, X = 3;

    // Function Call
    Console.Write("The generated array is ");
    GenerateArray(N, X);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach;

// Function to print the required array
function GenerateArray(N, X)
{
    let prev_xor = X;

    // Iterative from 1 to N
    for(let i = 1; i <= N; i++)
    {

        // Print the i-th element
        document.write((i ^ prev_xor));

        if (i != N)
        {
            document.write(" ");
        }

        // Update prev_xor to i
        prev_xor = i;
    }
}

// Driver Code

// Given Input
let N = 4, X = 3;

// Function Call
document.write("The generated array is ");
GenerateArray(N, X);

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
The generated array is 2 3 1 7
```

***时间复杂度:*** O(N)
***辅助空间*** : O(1)