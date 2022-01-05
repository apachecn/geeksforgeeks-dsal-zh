# 给定数量 K 的数组中每个元素的异或运算

> 原文:[https://www . geeksforgeeks . org/给定数字的数组的每个元素的 xor-k/](https://www.geeksforgeeks.org/xor-of-every-element-of-an-array-with-a-given-number-k/)

给定一个数组 **arr** 和一个数字 **K** ，从给定数组中找出相应元素与给定数字 K 进行异或运算形成的新数组。
T5】示例:

> **输入:** arr[] = { 2，4，1，3，5 }，K = 5
> **输出:** 7 1 4 6 0
> **解释:**
> 2 XOR 5 = 7
> 4 XOR 5 = 1
> 1 XOR 5 = 4
> 3 XOR 5 = 6
> 5 XOR 5 = 0
> **输入:** arr[] = { 4，75，45，42 }，K = 0

**进场:**

1.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
2.  然后计算每个元素与 k 的异或。
3.  然后将其存储为输出数组中该索引处的元素。
4.  打印更新后的数组。

下面是上述方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find XOR of every element
// of an array with a given number K

#include <bits/stdc++.h>
using namespace std;

// Function to construct new array
void constructXORArray(int A[], int n, int K)
{
    int B[n];

    // Traverse the array and
    // compute XOR with K
    for (int i = 0; i < n; i++)
        B[i] = A[i] ^ K;

    // Print new array
    for (int i = 0; i < n; i++)
        cout << B[i] << " ";
    cout << endl;
}

// Driver code
int main()
{
    int A[] = { 2, 4, 1, 3, 5 };
    int K = 5;
    int n = sizeof(A) / sizeof(A[0]);
    constructXORArray(A, n, K);

    int B[] = { 4, 75, 45, 42 };
    K = 2;
    n = sizeof(B) / sizeof(B[0]);
    constructXORArray(B, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find XOR of every element
// of an array with a given number K
import java.util.*;
class GFG
{

// Function to construct new array
static void constructXORArray(int A[], int n, int K)
{

     int[] B = new int[n];

    // Traverse the array and
    // compute XOR with K
    for (int i = 0; i < n; i++)
        B[i] = A[i] ^ K;

    // Print new array
    for (int i = 0; i < n; i++)
        System.out.print( B[i] +" ");
    System.out.println();
}

// Driver code
public static void main(String args[])
{
    int A[] = { 2, 4, 1, 3, 5 };
    int K = 5;
    int n = A.length;
    constructXORArray(A, n, K);

    int B[] = { 4, 75, 45, 42 };
    K = 2;
    n = B.length;
    constructXORArray(B, n, K);

}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python program to find XOR of every element
# of an array with a given number K

# Function to construct new array
def constructXORArray(A, n, K):

    B = [0]*n;

    # Traverse the array and
    # compute XOR with K
    for i in range(n):
        B[i] = A[i] ^ K;

    # Print new array
    for i in range(n):
        print(B[i], end=" ");
    print();

# Driver code
if __name__ == '__main__':
    A = [ 2, 4, 1, 3, 5 ];
    K = 5;
    n = len(A);
    constructXORArray(A, n, K);

    B = [ 4, 75, 45, 42 ];
    K = 2;
    n = len(B);
    constructXORArray(B, n, K);
# This code contributed by sapnasingh4991
```

## C#

```
// C# program to find XOR of every element
// of an array with a given number K
using System;

class GFG
{

// Function to construct new array
static void constructXORArray(int []A, int n, int K)
{

     int[] B = new int[n];

    // Traverse the array and
    // compute XOR with K
    for (int i = 0; i < n; i++)
        B[i] = A[i] ^ K;

    // Print new array
    for (int i = 0; i < n; i++)
        Console.Write( B[i] +" ");
    Console.WriteLine();
}

// Driver code
public static void Main(String []args)
{
    int []A = { 2, 4, 1, 3, 5 };
    int K = 5;
    int n = A.Length;
    constructXORArray(A, n, K);

    int []B = { 4, 75, 45, 42 };
    K = 2;
    n = B.Length;
    constructXORArray(B, n, K);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to find XOR of every element
    // of an array with a given number K

    // Function to construct new array
    function constructXORArray(A, n, K)
    {
        let B = new Array(n);

        // Traverse the array and
        // compute XOR with K
        for (let i = 0; i < n; i++)
            B[i] = A[i] ^ K;

        // Print new array
        for (let i = 0; i < n; i++)
            document.write(B[i] + " ");
        document.write("</br>")
    }

    let A = [ 2, 4, 1, 3, 5 ];
    let K = 5;
    let n = A.length;
    constructXORArray(A, n, K);

    let B = [ 4, 75, 45, 42 ];
    K = 2;
    n = B.length;
    constructXORArray(B, n, K);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
7 1 4 6 0 
6 73 47 40
```