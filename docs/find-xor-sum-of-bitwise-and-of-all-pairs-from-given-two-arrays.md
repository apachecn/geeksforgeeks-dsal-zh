# 从给定的两个数组中找出所有对的按位“与”的异或和

> 原文:[https://www . geeksforgeeks . org/find-xor-对给定两个数组中的所有对按位求和/](https://www.geeksforgeeks.org/find-xor-sum-of-bitwise-and-of-all-pairs-from-given-two-arrays/)

给定两个大小分别为 **N** 和 **M** 的数组 **A** 和 **B** ，任务是计算所有对 **A** 和 **B** 的[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和[位运算](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

**示例:**

> **输入:** A={3，5}，B={2，3}，N=2，M=2
> **输出:**t5】0
> T7】解释:T9】答案是(3&2)^(3&3)^(5&2)^(5&3)=1^3^0^2=0.
> 
> **输入:** A={1，2，3}，B={5，6}，N=3，M=2
> **输出:**
> 0

**天真方法:**天真方法是使用[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples/)计算所有对的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，然后找到它们的[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和。按照以下步骤解决问题:

1.  将变量**和**初始化为 **-1** ，这将存储最终答案。
2.  遍历数组 **A** ，并执行以下操作:
    1.  对于每个当前元素，遍历数组 **B** ，并执行以下操作:
        1.  如果 **ans** 等于 **-1** ，则将 **ans 中元素的[位](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)存储起来。**
        2.  否则，将**和**的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和**和**中元素的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)存储起来。
3.  返回〔t0〕年。

下面是上述方法的实现:

## C++

```
// C++ algorithm for the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to calculate the XOR sum of all ANDS of all
// pairs on A[] and B[]
int XorSum(int A[], int B[], int N, int M)
{
    // variable to store anshu
    int ans = -1;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            // when there has been no
            // AND of pairs before this
            if (ans == -1)
                ans = (A[i] & B[j]);
            else
                ans ^= (A[i] & B[j]);
        }
    }
    return ans;
}

// Driver code
int main()
{
    // Input
    int A[] = { 3, 5 };
    int B[] = { 2, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    // Function call
    cout << XorSum(A, B, N, M) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to calculate the XOR sum of all ANDS of all
// pairs on A[] and B[]
public static int XorSum(int A[], int B[], int N, int M)
{

    // variable to store anshu
    int ans = -1;
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {

            // when there has been no
            // AND of pairs before this
            if (ans == -1)
                ans = (A[i] & B[j]);
            else
                ans ^= (A[i] & B[j]);
        }
    }
    return ans;
}

// Driver code
    public static void main (String[] args)
    {

         // Input
    int A[] = { 3, 5 };
    int B[] = { 2, 3 };
    int N = A.length;
    int M =B.length;

    // Function call
    System.out.println(XorSum(A, B, N, M));

    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 algorithm for the above approach

# Function to calculate the XOR sum of all ANDS of all
# pairs on A and B
def XorSum(A, B, N, M):

    # variable to store anshu
    ans = -1
    for i in range(N):
        for j in range(M):

            # when there has been no
            # AND of pairs before this
            if (ans == -1):
                ans = (A[i] & B[j])
            else:
                ans ^= (A[i] & B[j])

    return ans

# Driver code
if __name__ == '__main__':

    # Input
    A = [3, 5]
    B = [2, 3]

    N = len(A)
    M = len(B)

    # Function call
    print (XorSum(A, B, N, M))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# algorithm for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate the XOR sum of all ANDS of all
// pairs on A[] and B[]
static int XorSum(int []A, int []B, int N, int M)
{

    // variable to store anshu
    int ans = -1;
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {

            // when there has been no
            // AND of pairs before this
            if (ans == -1)
                ans = (A[i] & B[j]);
            else
                ans ^= (A[i] & B[j]);
        }
    }
    return ans;
}

// Driver code
public static void Main()
{
    // Input]
    int []A = {3, 5};
    int []B = {2, 3};
    int N = A.Length;
    int M = B.Length;

    // Function call
    Console.Write(XorSum(A, B, N, M));
}
}

// This code is contributed by SURENDER_GANGWAR.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

        // Function to calculate the XOR sum of all ANDS of all
        // pairs on A[] and B[]
        function XorSum(A, B, N, M)
        {

            // variable to store anshu
            let ans = -1;
            for (let i = 0; i < N; i++)
            {
                for (let j = 0; j < M; j++)
                {

                    // when there has been no
                    // AND of pairs before this
                    if (ans == -1)
                        ans = (A[i] & B[j]);
                    else
                        ans ^= (A[i] & B[j]);
                }
            }
            return ans;
        }

        // Driver code

        // Input
        let A = [3, 5];
        let B = [2, 3];
        let N = A.length;
        let M = B.length;

        // Function call
        document.write(XorSum(A, B, N, M));

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
0
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*

**有效方法:**

**观察:**利用与上异或的分配性质可以解决这个问题。

> 让 A[] = [a，b，c]
> 让 B[] = [d，e]
> 结果:
> (a&d)^(a&e)^(b&d)^(b&e)^(c&d)^(c&e)
> 通过应用分配性质，
> [(a ^ b ^ c)&d]^[(a b e)&e]
> (a

按照以下步骤解决问题:

*   将两个变量 **ans1** 和 **ans2** 初始化为 **0** ，分别存储第一数组和第二数组的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和。
*   遍历 **A** ，对于每个当前元素:
    *   将 **ans1** 的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和当前元素存储在 **ans1** 中。
*   遍历 **B** ，对于每个当前元素:
    *   将 **ans2** 的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和当前元素存储在 **ans2** 中。
*   返回**年 1 &年 2。**

下面是上述方法的实现:

## C++14

```
// C++ algorithm for the above approach
#include <bits/stdc++.h>
using namespace std;
// Function to calculate the XOR sum of all ANDS of all
// pairs on A[] and B[]
int XorSum(int A[], int B[], int N, int M)
{
    // variable to store xor sums
    // of first array and second
    // array respectively.
    int ans1 = 0, ans2 = 0;
    // Xor sum of first array
    for (int i = 0; i < N; i++)
        ans1 = ans1 ^ A[i];
    // Xor sum of second array
    for (int i = 0; i < M; i++)
        ans2 = ans2 ^ B[i];
    // required answer
    return (ans1 & ans2);
}
// Driver code
int main()
{
    // Input
    int A[] = { 3, 5 };
    int B[] = { 2, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    // Function call
    cout << XorSum(A, B, N, M) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java algorithm for the above approach
import java.io.*;

class GFG{

// Function to calculate the XOR sum of
// all ANDS of all pairs on A[] and B[]
static int XorSum(int A[], int B[], int N, int M)
{

    // Variable to store xor sums
    // of first array and second
    // array respectively.
    int ans1 = 0, ans2 = 0;

    // Xor sum of first array
    for(int i = 0; i < N; i++)
        ans1 = ans1 ^ A[i];

    // Xor sum of second array
    for(int i = 0; i < M; i++)
        ans2 = ans2 ^ B[i];

    // Required answer
    return (ans1 & ans2);
}

// Driver code
public static void main(String[] args)
{

    // Input
    int A[] = { 3, 5 };
    int B[] = { 2, 3 };
    int N = A.length;
    int M = B.length;

    // Function call
    System.out.print(XorSum(A, B, N, M));
}
}

// This code is contributed by subham348
```

## 蟒蛇 3

```
# python 3 algorithm for the above approach

# Function to calculate the XOR sum of all ANDS of all
# pairs on A[] and B[]
def XorSum(A, B, N, M):

    # variable to store xor sums
    # of first array and second
    # array respectively.
    ans1 = 0
    ans2 = 0

    # Xor sum of first array
    for i in range(N):
        ans1 = ans1 ^ A[i]

    # Xor sum of second array
    for i in range(M):
        ans2 = ans2 ^ B[i]

    # required answer
    return (ans1 & ans2)

# Driver code
if __name__ == '__main__':

    # Input
    A = [3, 5]
    B = [2, 3]
    N = len(A)
    M = len(B)

    # Function call
    print(XorSum(A, B, N, M))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach

using System;

class GFG {

// Function to calculate the XOR sum of
// all ANDS of all pairs on A[] and B[]
static int XorSum(int[] A, int[] B, int N, int M)
{

    // Variable to store xor sums
    // of first array and second
    // array respectively.
    int ans1 = 0, ans2 = 0;

    // Xor sum of first array
    for(int i = 0; i < N; i++)
        ans1 = ans1 ^ A[i];

    // Xor sum of second array
    for(int i = 0; i < M; i++)
        ans2 = ans2 ^ B[i];

    // Required answer
    return (ans1 & ans2);
}

  // Driver code
  public static void Main (String[] args)
  {

    // Input
    int[] A = { 3, 5 };
    int[] B = { 2, 3 };
    int N = A.Length;
    int M = B.Length;

    // Function call
    Console.Write(XorSum(A, B, N, M));
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// JavaScript algorithm for the above approach

// Function to calculate the XOR sum of all ANDS of all
// pairs on A[] and B[]
function XorSum(A, B, N, M)
{
    // variable to store xor sums
    // of first array and second
    // array respectively.
    let ans1 = 0, ans2 = 0;
    // Xor sum of first array
    for (let i = 0; i < N; i++)
        ans1 = ans1 ^ A[i];
    // Xor sum of second array
    for (let i = 0; i < M; i++)
        ans2 = ans2 ^ B[i];
    // required answer
    return (ans1 & ans2);
}
// Driver code
    // Input
    let A = [ 3, 5 ];
    let B = [ 2, 3 ];
    let N = A.length;
    let M = B.length;

    // Function call
    document.write(XorSum(A, B, N, M));

</script>
```

**Output**

```
0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)