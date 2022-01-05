# 生成一个 N 长度数组，该数组具有相等的计数和两个奇偶校验的元素之和

> 原文:[https://www . geesforgeks . org/generate-an-n-length-array-with-count-and-sum-of-elements-of-parities/](https://www.geeksforgeeks.org/generate-an-n-length-array-having-equal-count-and-sum-of-elements-of-both-parities/)

给定一个整数**N***(3≤N≤10<sup>5</sup>)*，任务是生成一个由 **N** 个不同的正元素组成的数组，这样双方元素的个数和和和即偶数和奇数是相同的。如果无法构建这样的阵列，请打印 **-1** 。

**示例:**

> **输入:** N = 8
> **输出:** 2、4、6、8、1、3、5、11
> 
> **输入:** 6
> **输出:** -1
> **说明:**为了奇偶数组元素的个数相等，数组中必须存在 3 个奇偶元素。但是，3 个 od 元素之和总是奇数。因此，不可能生成这样的数组。

**方法:**按照以下步骤解决问题:

1.  如果 **N** 为奇数或 **(N / 2)** 为奇数，则打印 **-1** 。
2.  否则:
    *   从 **2** 开始打印 **N/2** 偶数值，并将计数存储在某个变量中，比如**sumever**。
    *   打印**N/2–1**从 **1** 开始的奇数，并将总和存储在另一个变量中，比如 **SumOdd** 。
    *   最后打印**sum 偶数–sum 奇数**，也是**奇数**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Fun dtion to print the
// required sequence
void Print(int N)
{
    if ((N / 2) % 2 == 1
|| (N % 2 == 1)) {
        cout << -1 << endl;
        return;
    }

// Stores count of even
// and odd elements
    int CurEven = 2, CurOdd = 1;

// Stores sum of even
// and odd elements
    int SumOdd = 0, SumEven = 0;

// Print N / 2 even elements
    for (int i = 0; i < (N / 2); i++) {

        cout << CurEven << " ";
        SumEven += CurEven;
        CurEven += 2;
    }

// Print N / 2 - 1 odd elements
    for (int i = 0; i < N / 2 - 1; i++) {
        cout << CurOdd << " ";
        SumOdd += CurOdd;
        CurOdd += 2;
    }

    CurOdd = SumEven - SumOdd;

    // Print final odd element
    cout << CurOdd << '\n';
}

// Driver Code
int main()
{
    int N = 12;
    Print(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.io.*;
class GFG
{

  // Fun dtion to print the
  // required sequence
  static void Print(int N)
  {
    if ((N / 2) % 2 == 1 || (N % 2 == 1))
    {
      System.out.print(-1);
      return;
    }

    // Stores count of even
    // and odd elements
    int CurEven = 2, CurOdd = 1;

    // Stores sum of even
    // and odd elements
    int SumOdd = 0, SumEven = 0;

    // Print N / 2 even elements
    for (int i = 0; i < (N / 2); i++)
    {
      System.out.print(CurEven + " ");
      SumEven += CurEven;
      CurEven += 2;
    }

    // Print N / 2 - 1 odd elements
    for (int i = 0; i < N / 2 - 1; i++)
    {
      System.out.print(CurOdd + " ");
      SumOdd += CurOdd;
      CurOdd += 2;
    }
    CurOdd = SumEven - SumOdd;

    // Print final odd element
    System.out.println(CurOdd);
  }

  // Driver Code
  public static void main (String[] args)
  {
    int N = 12;
    Print(N);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Fun dtion to print the
# required sequence
def Print(N):
    if ((N / 2) % 2 or (N % 2)):
        print(-1)
        return

# Stores count of even
# and odd elements
    CurEven = 2
    CurOdd = 1

# Stores sum of even
# and odd elements
    SumOdd = 0
    SumEven = 0

# Print N / 2 even elements
    for i in range(N // 2):

        print(CurEven,end=" ")
        SumEven += CurEven
        CurEven += 2

# Print N / 2 - 1 odd elements
    for i in range( (N//2) - 1):
        print(CurOdd, end=" ")
        SumOdd += CurOdd
        CurOdd += 2

    CurOdd = SumEven - SumOdd

    # Print final odd element
    print(CurOdd)

# Driver Code
N = 12
Print(N)

# This code is contributed by rohitsingh07052
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{

  // Fun dtion to print the
  // required sequence
  static void Print(int N)
  {
    if ((N / 2) % 2 == 1 || (N % 2 == 1))
    {
      Console.WriteLine(-1);
      return;
    }

    // Stores count of even
    // and odd elements
    int CurEven = 2, CurOdd = 1;

    // Stores sum of even
    // and odd elements
    int SumOdd = 0, SumEven = 0;

    // Print N / 2 even elements
    for (int i = 0; i < (N / 2); i++)
    {
      Console.Write(CurEven + " ");
      SumEven += CurEven;
      CurEven += 2;
    }

    // Print N / 2 - 1 odd elements
    for (int i = 0; i < N / 2 - 1; i++)
    {
      Console.Write(CurOdd + " ");
      SumOdd += CurOdd;
      CurOdd += 2;
    }
    CurOdd = SumEven - SumOdd;

    // Print final odd element
    Console.WriteLine(CurOdd);
  }

  // Driver Code
  public static void Main()
  {
    int N = 12;
    Print(N);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Fun dtion to print the
// required sequence
function Print(N)
{
    if ((N / 2) % 2 == 1 || (N % 2 == 1))
    {
         document.write(-1);
        return;
    }

    // Stores count of even
    // and odd elements
    var CurEven = 2, CurOdd = 1;

    // Stores sum of even
    // and odd elements
    var SumOdd = 0, SumEven = 0;

    // Print N / 2 even elements
    for(var i = 0; i < (N / 2); i++)
    {
        document.write(CurEven + " ");
        SumEven += CurEven;
        CurEven += 2;
    }

    // Print N / 2 - 1 odd elements
    for(var i = 0; i < N / 2 - 1; i++)
    {
        document.write(CurOdd + " ");
        SumOdd += CurOdd;
        CurOdd += 2;
    }
    CurOdd = SumEven - SumOdd;

    // Print final odd element
    document.write(CurOdd);
}

// Driver Code
var N = 12;

Print(N);

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
2 4 6 8 10 12 1 3 5 7 9 17
```

**时间复杂度:**O(N)
T3】辅助空间 O(1)