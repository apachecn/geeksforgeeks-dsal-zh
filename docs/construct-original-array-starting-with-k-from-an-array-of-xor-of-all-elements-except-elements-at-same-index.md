# 从除相同索引的元素之外的所有元素的异或数组中构建以 K 开头的原始数组

> 原文:[https://www . geeksforgeeks . org/construct-original-array-从所有元素的异或数组开始-除了相同索引处的元素/](https://www.geeksforgeeks.org/construct-original-array-starting-with-k-from-an-array-of-xor-of-all-elements-except-elements-at-same-index/)

给定一个由 **N** 个整数和数组的第一个元素**B【】**组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**作为 **K** ，任务是从**A【】**构造数组**B【】**，使得对于任何索引 **i** ，**A【I】**是**所有数组元素的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)**

**示例:**

> **输入:** A[] = {13，14，10，6}，K = 2
> **输出:** 2 1 5 9
> **解释:**
> 对于任何一个索引 I，A[i]都是 B[]除 B[i]之外的所有元素的按位异或。
> 
> 1.  B[1] ^ B[2] ^ B[3] = 1 ^ 5 ^ 9 = 13 = A[0]
> 2.  B[0] ^ B[2] ^ B[3] = 2 ^ 5 ^ 9 = 14 = A[1]
> 3.  B[0] ^ B[1] ^ B[3] = 2 ^ 1 ^ 9 = 10 = A[2]
> 4.  B[0] ^ B[1] ^ B[2] = 2 ^ 1 ^ 5 = 6 = A[3]
> 
> **输入:** A[] = {3，5，0，2，4}，K = 2
> T3】输出: 2 4 1 3 5

**方法:**这个想法是基于这样的观察:计算偶数次的相同值的按位异或是 **0** 。

> 对于任何索引 I，
> a[I]= b[0]^ b[1]^…b[I-1]^ b[I+1]^…b[n-1]
> 因此，B[]，total XOR = b[0]^ b[1]^…b[I–1]^ b[I]^ b[I+1]…b[n–1]的所有元素的 xor。
> 因此，B[i] = totalXor ^ A[i]。(因为除了 B[i]，每个元素都出现两次)

按照以下步骤解决问题:

*   将数组中存在的所有元素**【b】**的[位异或存储在一个变量中，比如 **totalXOR** ，其中 **totalXOR = A[0] ^ K** 。](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **A[]** 对于每个数组元素 A[i]，将 **B[i]** 的值存储为 **totalXOR ^ A[i]** 。
*   完成以上步骤后，打印数组 **B[]** 中存储的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to construct an array
// with each element equal to XOR
// of all array elements except
// the element at the same index
void constructArray(int A[], int N,
                    int K)
{
    // Original array
    int B[N];

    // Stores Bitwise XOR of array
    int totalXOR = A[0] ^ K;

    // Calculate XOR of all array elements
    for (int i = 0; i < N; i++)
        B[i] = totalXOR ^ A[i];

    // Print the original array B[]
    for (int i = 0; i < N; i++) {
        cout << B[i] << " ";
    }
}

// Driver Code
int main()
{
    int A[] = { 13, 14, 10, 6 }, K = 2;
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    constructArray(A, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to construct an array
// with each element equal to XOR
// of all array elements except
// the element at the same index
static void constructArray(int A[], int N,
                           int K)
{

    // Original array
    int B[] = new int[N];

    // Stores Bitwise XOR of array
    int totalXOR = A[0] ^ K;

    // Calculate XOR of all array elements
    for(int i = 0; i < N; i++)
        B[i] = totalXOR ^ A[i];

    // Print the original array B[]
    for(int i = 0; i < N; i++)
    {
        System.out.print(B[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 13, 14, 10, 6 }, K = 2;
    int N = A.length;

    // Function Call
    constructArray(A, N, K);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to construct an array
# with each element equal to XOR
# of all array elements except
# the element at the same index
def constructArray(A, N, K):

    # Original array
    B = [0] * N;

    # Stores Bitwise XOR of array
    totalXOR = A[0] ^ K;

    # Calculate XOR of all array elements
    for i in range(N):
        B[i] = totalXOR ^ A[i];

    # Print the original array B
    for i in range(N):
        print(B[i], end = " ");

# Driver Code
if __name__ == '__main__':
    A = [13, 14, 10, 6];
    K = 2;
    N = len(A);

    # Function Call
    constructArray(A, N, K);

# This code is contributed by Princi Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG {

    // Function to construct an array
    // with each element equal to XOR
    // of all array elements except
    // the element at the same index
    static void constructArray(int[] A, int N,
                               int K)
    {

        // Original array
        int[] B = new int[N];

        // Stores Bitwise XOR of array
        int totalXOR = A[0] ^ K;

        // Calculate XOR of all array elements
        for(int i = 0; i < N; i++)
            B[i] = totalXOR ^ A[i];

        // Print the original array B[]
        for(int i = 0; i < N; i++)
        {
            Console.Write(B[i] + " ");
        }
    }

  static void Main() {
    int[] A = { 13, 14, 10, 6 };
    int K = 2;
    int N = A.Length;

    // Function Call
    constructArray(A, N, K);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to construct an array
// with each element equal to XOR
// of all array elements except
// the element at the same index
function constructArray(A, N, K)
{
    // Original array
    let B = new Array(N);

    // Stores Bitwise XOR of array
    let totalXOR = A[0] ^ K;

    // Calculate XOR of all array elements
    for (let i = 0; i < N; i++)
        B[i] = totalXOR ^ A[i];

    // Print the original array B[]
    for (let i = 0; i < N; i++) {
        document.write(B[i] + " ");
    }
}

// Driver Code
    let A = [ 13, 14, 10, 6 ], K = 2;
    let N = A.length;

    // Function Call
    constructArray(A, N, K);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
2 1 5 9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)