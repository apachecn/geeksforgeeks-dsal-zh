# 前缀和数组的前缀阶乘

> 原文:[https://www . geesforgeks . org/prefix-factories-of-a-prefix-sum-array/](https://www.geeksforgeeks.org/prefix-factorials-of-a-prefix-sum-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到给定数组的[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的前缀阶乘，即![prefix[i] = (\sum_{0}^{i}arr[i])!                 ](img/0653c2eb1c04110e054071d2c193f75d.png "Rendered by QuickLaTeX.com")。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 1 6 720 3628800
> **解释:**
> 给定数组的前缀和为{1，3，6，10}。因此，获得的前缀和数组的前缀阶乘为{1！, (1+2)!, (1+2+3)!, (1+2+3+4)!} = {1!, 3!, 6!, 10!} = {1 6 720 3628800}.
> 
> **输入:** arr[] = {2，4，3，1}
> **输出:** 2 720 362880 3628800

**天真法:**解决给定问题最简单的方法是先求给定数组的[前缀和，然后](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)[求前缀和数组中每个数组元素](https://www.geeksforgeeks.org/factorial-of-an-array-of-integers/)的阶乘。计算前缀和后，打印阶乘数组。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the factorial of
// a number N
int fact(int N)
{
    // Base Case
    if (N == 1 || N == 0)
        return 1;

    // Find the factorial recursively
    return N * fact(N - 1);
}

// Function to find the prefix
// factorial array
void prefixFactorialArray(int arr,
                          int N)
{
    // Find the prefix sum array
    for (int i = 1; i < N; i++) {
        arr[i] += arr[i - 1];
    }

    // Find the factorials of each
    // array element
    for (int i = 0; i < N; i++) {
        arr[i] = fact(arr[i]);
    }

    // Print the resultant array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    prefixFactorialArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the factorial of
// a number N
static int fact(int N)
{

    // Base Case
    if (N == 1 || N == 0)
        return 1;

    // Find the factorial recursively
    return N * fact(N - 1);
}

// Function to find the prefix
// factorial array
static void prefixFactorialArray(int[] arr, int N)
{

    // Find the prefix sum array
    for(int i = 1; i < N; i++)
    {
        arr[i] += arr[i - 1];
    }

    // Find the factorials of each
    // array element
    for(int i = 0; i < N; i++)
    {
        arr[i] = fact(arr[i]);
    }

    // Print the resultant array
    for(int i = 0; i < N; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4 };
    int N = arr.length;

    prefixFactorialArray(arr, N);
}
}

// This code is contributed by ukasp
```

## 蟒蛇 3

```
# Python implementation of the approach
def fact(N):

    # Base Case
    if (N == 1 or N == 0):
        return 1

    # Find the factorial recursively
    return N * fact(N - 1)

# Function to find the prefix
# factorial array
def prefixFactorialArray(arr, N):

    # Find the prefix sum array
    for i in range(1, N):
        arr[i] += arr[i - 1]

    # Find the factorials of each
    # array element
    for i in range(N):
        arr[i] = fact(arr[i])

        # Print the resultant array
    for i in range(N):
        print(arr[i], end=" ")

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 4]
    N = len(arr)
    prefixFactorialArray(arr, N)

# This code is contributed by kirtishsurangalikar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the factorial of
// a number N
static int fact(int N)
{

    // Base Case
    if (N == 1 || N == 0)
        return 1;

    // Find the factorial recursively
    return N * fact(N - 1);
}

// Function to find the prefix
// factorial array
static void prefixFactorialArray(int[] arr,
                                 int N)
{

    // Find the prefix sum array
    for(int i = 1; i < N; i++)
    {
        arr[i] += arr[i - 1];
    }

    // Find the factorials of each
    // array element
    for(int i = 0; i < N; i++)
    {
        arr[i] = fact(arr[i]);
    }

    // Print the resultant array
    for(int i = 0; i < N; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    prefixFactorialArray(arr, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the factorial of
// a number N
function fact(N) {
    // Base Case
    if (N == 1 || N == 0)
        return 1;

    // Find the factorial recursively
    return N * fact(N - 1);
}

// Function to find the prefix
// factorial array
function prefixFactorialArray(arr, N) {
    // Find the prefix sum array
    for (let i = 1; i < N; i++) {
        arr[i] += arr[i - 1];
    }

    // Find the factorials of each
    // array element
    for (let i = 0; i < N; i++) {
        arr[i] = fact(arr[i]);
    }

    // Print the resultant array
    for (let i = 0; i < N; i++) {
        document.write(arr[i] + " ");
    }
}

// Driver Code

let arr = [1, 2, 3, 4];
let N = arr.length;
prefixFactorialArray(arr, N);

</script>
```

**输出:**

```
1 6 720 3628800 
```

***时间复杂度:** O(N*M)，其中 M 为* [*阵元之和*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) *。*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过预先计算数组元素之和[的](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)[阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)进行优化，使得每个指标 is 的阶乘计算可以在 ***O(1)时间*** 进行。

下面是上述方法的一个实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the factorial of
// prefix sum at every possible index
void prefixFactorialArray(int A[], int N)
{
    // Find the prefix sum array
    for (int i = 1; i < N; i++) {
        A[i] += A[i - 1];
    }

    // Stores the factorial of all the
    // element till the sum of array
    int fact[A[N - 1] + 1];
    fact[0] = 1;

    // Find the factorial array
    for (int i = 1; i <= A[N - 1]; i++) {
        fact[i] = i * fact[i - 1];
    }

    // Find the factorials of
    // each array element
    for (int i = 0; i < N; i++) {
        A[i] = fact[A[i]];
    }

    // Print the resultant array
    for (int i = 0; i < N; i++) {
        cout << A[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    prefixFactorialArray(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the factorial of
// prefix sum at every possible index
static void prefixFactorialArray(int A[], int N)
{

    // Find the prefix sum array
    for(int i = 1; i < N; i++)
    {
        A[i] += A[i - 1];
    }

    // Stores the factorial of all the
    // element till the sum of array
    int fact[] = new int[A[N - 1] + 1];
    fact[0] = 1;

    // Find the factorial array
    for(int i = 1; i <= A[N - 1]; i++)
    {
        fact[i] = i * fact[i - 1];
    }

    // Find the factorials of
    // each array element
    for(int i = 0; i < N; i++)
    {
        A[i] = fact[A[i]];
    }

    // Print the resultant array
    for(int i = 0; i < N; i++)
    {
        System.out.print(A[i] + " ");
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int N = arr.length;

    prefixFactorialArray(arr, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# // python program for the above approach

# // Function to find the factorial of
# // prefix sum at every possible index
def prefixFactorialArray(A, N):

    # // Find the prefix sum array
    for i in range(1, N):
        A[i] += A[i - 1]

    # // Stores the factorial of all the
    # // element till the sum of array
    fact = [0 for x in range(A[N - 1] + 1)]
    fact[0] = 1

    # // Find the factorial array
    for i in range(1, A[N-1]+1):
        fact[i] = i * fact[i - 1]

    # // Find the factorials of
    # // each array element
    for i in range(0, N):
        A[i] = fact[A[i]]

    # // Print the resultant array
    for i in range(0, N):
        print(A[i], end=" ")

# Driver code
arr = [1, 2, 3, 4]
N = len(arr)
prefixFactorialArray(arr, N)

# This code is contributed by amreshkumar3.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the factorial of
    // prefix sum at every possible index
    static void prefixFactorialArray(int[] A, int N)
    {

        // Find the prefix sum array
        for(int i = 1; i < N; i++)
        {
            A[i] += A[i - 1];
        }

        // Stores the factorial of all the
        // element till the sum of array
        int[] fact = new int[A[N - 1] + 1];
        fact[0] = 1;

        // Find the factorial array
        for(int i = 1; i <= A[N - 1]; i++)
        {
            fact[i] = i * fact[i - 1];
        }

        // Find the factorials of
        // each array element
        for(int i = 0; i < N; i++)
        {
            A[i] = fact[A[i]];
        }

        // Print the resultant array
        for(int i = 0; i < N; i++)
        {
            Console.Write(A[i] + " ");
        }
    }

  // Driver code
  static void Main() {
    int[] arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    prefixFactorialArray(arr, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the factorial of
// prefix sum at every possible index
function prefixFactorialArray(A, N) {
    // Find the prefix sum array
    for (let i = 1; i < N; i++) {
        A[i] += A[i - 1];
    }

    // Stores the factorial of all the
    // element till the sum of array
    let fact = new Array(A[N - 1] + 1);
    fact[0] = 1;

    // Find the factorial array
    for (let i = 1; i <= A[N - 1]; i++) {
        fact[i] = i * fact[i - 1];
    }

    // Find the factorials of
    // each array element
    for (let i = 0; i < N; i++) {
        A[i] = fact[A[i]];
    }

    // Print the resultant array
    for (let i = 0; i < N; i++) {
        document.write(A[i] + " ");
    }
}

// Driver Code

let arr = [1, 2, 3, 4];
let N = arr.length
prefixFactorialArray(arr, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
1 6 720 3628800
```

***时间复杂度:** O(N + M)，其中 M 为* [*阵元之和*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) *。*
***辅助空间:** O(M)，其中 M 为* [*数组元素之和*](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) *。*