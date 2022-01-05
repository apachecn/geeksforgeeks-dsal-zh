# 生成包含给定数量 A 和 B 的相邻元素差值相等的 N 大小数组

> 原文:[https://www . geesforgeks . org/generate-n-size-array-with-equal-different-of-elements-contained-numbers-a-and-b/](https://www.geeksforgeeks.org/generate-n-size-array-with-equal-difference-of-adjacent-elements-containing-given-numbers-a-and-b/)

给定两个自然数 **A** 和 **B** (B > = A)和一个整数 **N** ，你的任务是以非递减的顺序生成一个**自然数**的数组，这样 A 和 B 都必须是数组的一部分，并且每对相邻元素之间的差异是相同的，同时保持数组的最大元素尽可能最小。

**示例:**

> **输入:** A = 10，B=20，N = 4
> **输出:** 5 10 15 20
> **说明:**数组{5，10，15，20}只包含自然数，A = 10 和 B = 20 都包含在数组中。每个相邻对之间的差值为 5，最大元素为 20，不能再减少了。
> 
> **输入:** A = 12，B = 33，N = 2
> T3】输出: 12 33
> 
> **输入:** A = 7，B = 17，N = 5
> T3】输出: 2 7 12 17 22

**方法:**所需阵列形成 [AP 系列](https://www.geeksforgeeks.org/progressions-ap-gp-hp/)。由于 A 和 B 必须包含在 AP 中，相邻项之间的共同差异 **d** 必须是(B–A)的除数。为了最小化最大项，最佳方法是生成满足给定条件的具有最小可能公共差的数组。该问题可以通过以下步骤解决:

*   迭代 **d** 从 **1** 到 **B-A** 的所有值。
*   如果 **d** 是 **B-A** 的一个因子，并且从 **A** 到 **B** 之间具有共同差异 **d** 的元素数量不超过 **N** ，则继续进行。否则，转到 **d** 的下一个值。
*   有两种可能的情况
    *   *情况 1*–具有相同差异的小于或等于 **B** 的元素数量 **d** 大于 **N** 。在这种情况下，数组的第一个元素将是**B –( d *(N-1))**。
    *   *情况 2*–具有相同差异的小于或等于 **B** 的元素数量 **d** 小于 **N** 。在这种情况下，数组的第一个元素将是**B–d *(B- 1)/d**(即 1)。
*   使用第一个元素和公共差打印数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the array of N
// natural numbers in increasing order
// with equal difference of adjacent
// elements and containing A and B
void generateAP(int A, int B, int N)
{
    // maximum possible difference
    int d = B - A;
    int cd, f;

    // Iterating over all values of d
    for (int i = 1; i <= d; i++) {

        // Check if i is a factor of d
        // and number of elements from
        // a to b with common difference
        // d are not more than N
        if (d % i == 0 && (d / i) + 1 <= N) {

            // Number off natural numbers
            // less than B and having
            // difference as i
            int cnt = min((B - 1) / i, N - 1);

            // Calculate the 1st element of
            // the required array
            f = B - (cnt * i);
            cd = i;
            break;
        }
    }

    // Print the resulting array
    for (int i = 0; i < N; i++) {
        cout << (f + i * cd) << " ";
    }
}

// Driver code
int main()
{
    int A = 10, B = 20, N = 4;

    // Function call
    generateAP(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
  public static int min(int a ,int b){
    if(a < b){
      return a;
    }
    return b;
  }
   public static void generateAP(int A, int B, int N)
    {
        // maximum possible difference
        int d = B - A;
        int cd = 0, f= 0;

        // Iterating over all values of d
        for (int i = 1; i <= d; i++) {

            // Check if i is a factor of d
            // and number of elements from
            // a to b with common difference
            // d are not more than N
            if (d % i == 0 && (d / i) + 1 <= N) {

                // Number off natural numbers
                // less than B and having
                // difference as i
                int cnt = min((B - 1) / i, N - 1);

                // Calculate the 1st element of
                // the required array
                f = B - (cnt * i);
                cd = i;
                break;
            }
        }

        // Print the resulting array
        for (int i = 0; i < N; i++) {
            System.out.print((f + i * cd) + " ");
        }
    }

    // Driver code

    public static void main(String[] args)
    {

        int A = 10, B = 20, N = 4;

        // Function call
        generateAP(A, B, N);
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to print array of N
# natural numbers in increasing order
# with equal difference of adjacent
# elements and containing A and B
def generateAP(A, B, N):

    # maximum possible difference
    d = B - A

    # Iterating over all values of d
    for i in range(1,d+1):

        # Check if i is a factor of d
        # and number of elements from
        # a to b with common difference
        # d are not more than N
        if (d % i == 0 and (d // i) + 1 <= N):

            # Number off natural numbers
            # less than B and having
            # difference as i
            cnt = min((B - 1) // i, N - 1)

            # Calculate the 1st element of
            # the required array
            f = B - (cnt * i)
            cd = i
            break

    # Print resulting array
    for i in range(N):
        print(f + i * cd , end=" ")

# Driver code
A = 10
B = 20
N = 4

# Function call
generateAP(A, B, N)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  public static int min(int a ,int b){
    if(a < b){
      return a;
    }
    return b;
  }
   public static void generateAP(int A, int B, int N)
    {
        // maximum possible difference
        int d = B - A;
        int cd = 0, f= 0;

        // Iterating over all values of d
        for (int i = 1; i <= d; i++) {

            // Check if i is a factor of d
            // and number of elements from
            // a to b with common difference
            // d are not more than N
            if (d % i == 0 && (d / i) + 1 <= N) {

                // Number off natural numbers
                // less than B and having
                // difference as i
                int cnt = min((B - 1) / i, N - 1);

                // Calculate the 1st element of
                // the required array
                f = B - (cnt * i);
                cd = i;
                break;
            }
        }

        // Print the resulting array
        for (int i = 0; i < N; i++) {
            Console.Write((f + i * cd) + " ");
        }
    }

// Driver Code
public static void Main()
{
    int A = 10, B = 20, N = 4;

        // Function call
        generateAP(A, B, N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

function min(a, b)
{
    if (a < b)
    {
        return a;
    }
    return b;
}

// Function to print the array of N
// natural numbers in increasing order
// with equal difference of adjacent
// elements and containing A and B
function generateAP(A, B, N)
{

    // Maximum possible difference
    var d = B - A;
    var cd = 0, f = 0;

    // Iterating over all values of d
    for(var i = 1; i <= d; i++)
    {

        // Check if i is a factor of d
        // and number of elements from
        // a to b with common difference
        // d are not more than N
        if (d % i == 0 && (d / i) + 1 <= N)
        {

            // Number off natural numbers
            // less than B and having
            // difference as i
            var cnt = min((B - 1) / i, N - 1);

            // Calculate the 1st element of
            // the required array
            f = B - (cnt * i);
            cd = i;
            break;
        }
    }

    // Print the resulting array
    for(var i = 0; i < N; i++)
    {
        document.write((f + i * cd) + " ");
    }
}

// Driver code
var A = 10, B = 20, N = 4;

// Function call
generateAP(A, B, N);

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
5 10 15 20 
```

**时间复杂度:***O(N+√B)*
T5】辅助空间: O(1)