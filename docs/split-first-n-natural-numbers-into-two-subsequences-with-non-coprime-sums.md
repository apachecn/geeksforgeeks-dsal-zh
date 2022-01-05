# 用非互质和将前 N 个自然数分成两个子序列

> 原文:[https://www . geesforgeks . org/split-first-n-自然数-分成两个子序列-具有非互素-和/](https://www.geeksforgeeks.org/split-first-n-natural-numbers-into-two-subsequences-with-non-coprime-sums/)

给定一个整数**N**(**N**T14】e； **3** ，任务是将从 **1** 到 **N** 的所有数字拆分为两个[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)，使得两个[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)的和互不互质。

***例:***

> **输入:** N = 5
> **输出:**
> {1，3，5}
> {2，4}
> **说明:**子序列 X[] = 1 + 3 + 5 = 9 的和。
> 子序列 Y[] = 2 + 4 = 6 的和。
> 由于 GCD(9，6)为 3，所以和之间不是同素的。
> 
> **输入:** N = 4
> **输出:**
> {1，4}
> {2，3}

**天真方法:**最简单的方法是首先以所有可能的方式将 **N** 个自然数拆分为两个子序列，对于每个组合，检查两个子序列的和是否为非互质。如果发现任何一对子序列为真，打印该子序列并[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   第一个**(N–1)**自然数的[和由**(N *(N–1))/2**给出。](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)
*   因此**((N *(N–1))/2)****N**的 GCD 为 **N** 。

根据以上观察，将范围**【1，N】**中的所有数字插入一个子序列中，并将 **N** 插入另一个子序列中。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to split 1 to N
// into two subsequences
// with non-coprime sums
void printSubsequence(int N)
{
    cout << "{ ";
    for (int i = 1; i < N - 1; i++) {
        cout << i << ", ";
    }

    cout << N - 1 << " }\n";

    cout << "{ " << N << " }";
}
// Driver Code
int main()
{
    int N = 8;

    printSubsequence(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

  // Function to split 1 to N
  // into two subsequences
  // with non-coprime sums
  public static void printSubsequence(int N)
  {
    System.out.print("{ ");
    for (int i = 1; i < N - 1; i++)
    {
      System.out.print(i + ", ");
    }

    System.out.println(N - 1 + " }");
    System.out.print("{ " + N + " }");
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 8;
    printSubsequence(N);
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to split 1 to N
# into two subsequences
# with non-coprime sums
def printSubsequence(N):

    print("{ ", end = "")
    for i in range(1, N - 1):
        print(i, end = ", ")

    print(N - 1, end = " }\n")

    print("{", N, "}")

# Driver Code
if __name__ == '__main__':

    N = 8

    printSubsequence(N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to split 1 to N
  // into two subsequences
  // with non-coprime sums
  public static void printSubsequence(int N)
  {
    Console.Write("{ ");
    for (int i = 1; i < N - 1; i++)
    {
        Console.Write(i + ", ");
    }

    Console.WriteLine(N - 1 + " }");
    Console.Write("{ " + N + " }");
  }

  // Driver code
  public static void Main(string[] args)
  {
    int N = 8;
    printSubsequence(N);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to split 1 to N
    // into two subsequences
    // with non-coprime sums
    function printSubsequence(N)
    {
      document.write("{ ");
      for (let i = 1; i < N - 1; i++)
      {
          document.write(i + ", ");
      }

      document.write(N - 1 + " }" + "</br>");
      document.write("{ " + N + " }" + "</br>");
    }

    let N = 8;
    printSubsequence(N);

</script>
```

**Output:** 

```
{ 1, 2, 3, 4, 5, 6, 7 }
{ 8 }
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)