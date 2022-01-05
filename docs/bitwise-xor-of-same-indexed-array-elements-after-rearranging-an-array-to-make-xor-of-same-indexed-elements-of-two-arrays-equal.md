# 在重新排列一个数组后，对相同的索引数组元素进行逐位异或运算，使两个数组的相同索引元素的异或相等

> 原文:[https://www . geeksforgeeks . org/同索引数组元素按位异或-重新排列数组后对同索引数组元素进行异或-相等/](https://www.geeksforgeeks.org/bitwise-xor-of-same-indexed-array-elements-after-rearranging-an-array-to-make-xor-of-same-indexed-elements-of-two-arrays-equal/)

给定由 **N** 个正整数组成的两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，任务是在重新排列数组**B【】**之后对相同索引数组元素进行[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，使得数组**A【】**的相同索引元素的[位异或](https://www.geeksforgeeks.org/tag/xor/)变得相等。

**示例:**

> **输入:** A[] = {1，2，3}，B[] = {4，6，7}
> **输出:** 5
> **解释:**
> 以下是可能的安排:
> 
> *   将数组 B[]重新排列为{4，7，6}。现在，相同索引元素的按位异或相等，即 1 ^ 4 = 5，2 ^ 7 = 5，3 ^ 6 = 5。
> 
> 重新排列后，所需的按位异或是 5。
> 
> **输入:** A[] = { 7，8，14 }，B[] = { 5，12，3 }
> **输出:** 11
> **解释:**
> 以下是可能的安排:
> 
> *   将数组 B[]重新排列为{12，3，5}。现在，相同索引元素的按位异或相等，即 7 ^ 12 = 11，8 ^ 3 = 11，14 ^ 5 = 11。
> 
> 重新排列后，所需的按位异或是 11。

**天真的做法:**给定的问题可以基于重新排列的计数最多可以是 **N** 的观察来解决，因为**A【】**中的任何元素只能与**B【**中的 **N** 其他整数配对。所以 **N** 候选值为 **X** 。现在，只需[将 **A[]** 中每个元素的所有候选进行](https://www.geeksforgeeks.org/calculate-xor-1-n/)异或，检查 **B[]** 是否可以按此顺序排列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible values
// of Bitwise XOR such after rearranging
// the array elements the Bitwise XOR
// value at corresponding indexes is same
void findPossibleValues(int A[], int B[],
                        int n)
{

    // Sort the array B
    sort(B, B + n);
    int C[n];

    // Stores all the possible values
    // of the Bitwise XOR
    set<int> numbers;

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // Possible value of K
        int candidate = A[0] ^ B[i];

        // Array B for the considered
        // value of K
        for (int j = 0; j < n; j++) {
            C[j] = A[j] ^ candidate;
        }

        sort(C, C + n);
        bool flag = false;

        // Verify if the consodered value
        // satisfies the condition or not
        for (int j = 0; j < n; j++)
            if (C[j] != B[j])
                flag = true;

        // Insert the possible Bitwise
        // XOR value
        if (!flag)
            numbers.insert(candidate);
    }

    // Print all the values obtained
    for (auto x : numbers) {
        cout << x << " ";
    }
}

// Driver Code
int main()
{
    int A[] = { 7, 8, 14 };
    int B[] = { 5, 12, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    findPossibleValues(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find all possible values
// of Bitwise XOR such after rearranging
// the array elements the Bitwise XOR
// value at corresponding indexes is same
static void findPossibleValues(int A[], int B[],
                        int n)
{

    // Sort the array B
    Arrays.sort(B);
    int []C = new int[n];

    // Stores all the possible values
    // of the Bitwise XOR
    HashSet<Integer> numbers = new HashSet<Integer>();

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // Possible value of K
        int candidate = A[0] ^ B[i];

        // Array B for the considered
        // value of K
        for (int j = 0; j < n; j++) {
            C[j] = A[j] ^ candidate;
        }

        Arrays.sort(C);
        boolean flag = false;

        // Verify if the consodered value
        // satisfies the condition or not
        for (int j = 0; j < n; j++)
            if (C[j] != B[j])
                flag = true;

        // Insert the possible Bitwise
        // XOR value
        if (!flag)
            numbers.add(candidate);
    }

    // Print all the values obtained
    for (int x : numbers) {
        System.out.print(x+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 7, 8, 14 };
    int B[] = { 5, 12, 3 };
    int N = A.length;
    findPossibleValues(A, B, N);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find all possible values
# of Bitwise XOR such after rearranging
# the array elements the Bitwise XOR
# value at corresponding indexes is same
def findPossibleValues(A, B, n):

  # Sort the array B
  B.sort();
  C = [0] * n;

  # Stores all the possible values
  # of the Bitwise XOR
  numbers = set();

  # Iterate over the range
  for i in range(n):

    # Possible value of K
    candidate = A[0] ^ B[i];

    # Array B for the considered
    # value of K
    for j in range(n):
      C[j] = A[j] ^ candidate;

    C.sort();
    flag = False;

    # Verify if the consodered value
    # satisfies the condition or not
    for j in range(n):
        if (C[j] != B[j]):
             flag = True;

    # Insert the possible Bitwise
    # XOR value
    if (not flag):
        numbers.add(candidate);

  # Print all the values obtained
  for x in numbers:
    print(x, end = " ");

# Driver Code
A = [7, 8, 14];
B = [5, 12, 3];
N = len(A);
findPossibleValues(A, B, N);

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find all possible values
// of Bitwise XOR such after rearranging
// the array elements the Bitwise XOR
// value at corresponding indexes is same
static void findPossibleValues(int []A, int []B,
                        int n)
{

    // Sort the array B
    Array.Sort(B);
    int []C = new int[n];

    // Stores all the possible values
    // of the Bitwise XOR
    HashSet<int> numbers = new HashSet<int>();

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // Possible value of K
        int candidate = A[0] ^ B[i];

        // Array B for the considered
        // value of K
        for (int j = 0; j < n; j++) {
            C[j] = A[j] ^ candidate;
        }

        Array.Sort(C);
        bool flag = false;

        // Verify if the consodered value
        // satisfies the condition or not
        for (int j = 0; j < n; j++)
            if (C[j] != B[j])
                flag = true;

        // Insert the possible Bitwise
        // XOR value
        if (!flag)
            numbers.Add(candidate);
    }

    // Print all the values obtained
    foreach (int x in numbers) {
        Console.Write(x+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 7, 8, 14 };
    int []B = { 5, 12, 3 };
    int N = A.Length;
    findPossibleValues(A, B, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find all possible values
// of Bitwise XOR such after rearranging
// the array elements the Bitwise XOR
// value at corresponding indexes is same
function findPossibleValues(A, B, n) {
  // Sort the array B
  B.sort((a, b) => a - b);
  let C = new Array(n);

  // Stores all the possible values
  // of the Bitwise XOR
  let numbers = new Set();

  // Iterate over the range
  for (let i = 0; i < n; i++) {
    // Possible value of K
    let candidate = A[0] ^ B[i];

    // Array B for the considered
    // value of K
    for (let j = 0; j < n; j++) {
      C[j] = A[j] ^ candidate;
    }

    C.sort((a, b) => a - b);
    let flag = false;

    // Verify if the consodered value
    // satisfies the condition or not
    for (let j = 0; j < n; j++) if (C[j] != B[j]) flag = true;

    // Insert the possible Bitwise
    // XOR value
    if (!flag) numbers.add(candidate);
  }

  // Print all the values obtained
  for (let x of numbers) {
    document.write(x + " ");
  }
}

// Driver Code
let A = [7, 8, 14];
let B = [5, 12, 3];
let N = A.length;
findPossibleValues(A, B, N);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
11
```

***时间复杂度:**O(N<sup>2</sup>* log(N))*
***辅助空间:** O(N)*

**高效方法:**上述方法也可以通过不排序数组并存储 **B[]** 的所有元素的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，然后与 **C[]** 中的所有元素进行**位异或**来优化。如果结果是 **0** ，那么这意味着两个数组具有相同的元素。按照以下步骤解决问题:

*   初始化变量，比如说 **x** 存储数组 **B[]所有元素的**异或**。**
*   [初始化一组](https://www.geeksforgeeks.org/set-in-cpp-stl/)，说**数字[]** 只存储唯一的数字..
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下步骤:
    *   将变量**候选项**初始化为**A【0】**和**B【I】**的异或，将 **curr_xor** 初始化为 **x** ，执行所需操作后，查看是否为 **0** 。
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下步骤:
        *   将变量 **y** 初始化为**A【j】**和**候选**的异或，用 **curr_xor 进行异或 **y** 。**
    *   如果 **curr_xor** 等于 **0，**则[将值**候选项**插入到设置的](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/) **数字中[]。**
*   执行上述步骤后，打印设置的**数字[]** 作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find all possible values
// of Bitwise XOR such after rearranging
// the array elements the Bitwise XOR
// value at corresponding indexes is same
void findPossibleValues(int A[], int B[],
                        int n)
{
    // Stores the XOR of the array B[]
    int x = 0;

    for (int i = 0; i < n; i++) {
        x = x ^ B[i];
    }

    // Stores all possible value of
    // Bitwise XOR
    set<int> numbers;

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // Possible value of K
        int candidate = A[0] ^ B[i];
        int curr_xor = x;

        // Array B for the considered
        // value of K
        for (int j = 0; j < n; j++) {
            int y = A[j] ^ candidate;
            curr_xor = curr_xor ^ y;
        }

        // This means all the elements
        // are equal
        if (curr_xor == 0)
            numbers.insert(candidate);
    }

    // Print all the possible value
    for (auto x : numbers) {
        cout << x << " ";
    }
}

// Driver Code
int main()
{
    int A[] = { 7, 8, 14 };
    int B[] = { 5, 12, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    findPossibleValues(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for above approach
import java.util.*;

class GFG{

// Function to find all possible values
// of Bitwise XOR such after rearranging
// the array elements the Bitwise XOR
// value at corresponding indexes is same
static void findPossibleValues(int A[], int B[],
                        int n)
{
    // Stores the XOR of the array B[]
    int x = 0;

    for (int i = 0; i < n; i++) {
        x = x ^ B[i];
    }

    // Stores all possible value of
    // Bitwise XOR
    HashSet<Integer> numbers = new HashSet<Integer>();

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // Possible value of K
        int candidate = A[0] ^ B[i];
        int curr_xor = x;

        // Array B for the considered
        // value of K
        for (int j = 0; j < n; j++) {
            int y = A[j] ^ candidate;
            curr_xor = curr_xor ^ y;
        }

        // This means all the elements
        // are equal
        if (curr_xor == 0)
            numbers.add(candidate);
    }

    // Print all the possible value
    for (int i : numbers) {
        System.out.print(i + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 7, 8, 14 };
    int B[] = { 5, 12, 3 };
    int N = A.length;
    findPossibleValues(A, B, N);
}
}

// This code is contributed by avijitmondal1998.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find all possible values
# of Bitwise XOR such after rearranging
# the array elements the Bitwise XOR
# value at corresponding indexes is same
def findPossibleValues(A, B, n):

    # Stores the XOR of the array B[]
    x = 0

    for i in range(n):
        x = x ^ B[i]

    # Stores all possible value of
    # Bitwise XOR
    numbers = set()

    # Iterate over the range
    for i in range(n):
        # Possible value of K
        candidate = A[0] ^ B[i]
        curr_xor = x

        # Array B for the considered
        # value of K
        for j in range(n):
            y = A[j] ^ candidate
            curr_xor = curr_xor ^ y

        # This means all the elements
        # are equal
        if (curr_xor == 0):
            numbers.add(candidate)

    # Print all the possible value
    for x in numbers:
        print(x, end = " ")

# Driver Code
if __name__ == '__main__':
    A = [7, 8, 14]
    B = [5, 12, 3]
    N = len(A)
    findPossibleValues(A, B, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# code for above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to find all possible values
// of Bitwise XOR such after rearranging
// the array elements the Bitwise XOR
// value at corresponding indexes is same
static void findPossibleValues(int []A, int []B,
                        int n)
{

    // Stores the XOR of the array []B
    int x = 0;

    for (int i = 0; i < n; i++) {
        x = x ^ B[i];
    }

    // Stores all possible value of
    // Bitwise XOR
    HashSet<int> numbers = new HashSet<int>();

    // Iterate over the range
    for (int i = 0; i < n; i++) {

        // Possible value of K
        int candidate = A[0] ^ B[i];
        int curr_xor = x;

        // Array B for the considered
        // value of K
        for (int j = 0; j < n; j++) {
            int y = A[j] ^ candidate;
            curr_xor = curr_xor ^ y;
        }

        // This means all the elements
        // are equal
        if (curr_xor == 0)
            numbers.Add(candidate);
    }

    // Print all the possible value
    foreach (int i in numbers) {
        Console.Write(i + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 7, 8, 14 };
    int []B = { 5, 12, 3 };
    int N = A.Length;
    findPossibleValues(A, B, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript code for above approach

// Function to find all possible values
// of Bitwise XOR such after rearranging
// the array elements the Bitwise XOR
// value at corresponding indexes is same
function findPossibleValues(A, B, n)
{

    // Stores the XOR of the array B
    var x = 0;

    for (var i = 0; i < n; i++) {
        x = x ^ B[i];
    }

    // Stores all possible value of
    // Bitwise XOR
    var numbers = new Set();

    // Iterate over the range
    for (var i = 0; i < n; i++) {

        // Possible value of K
        var candidate = A[0] ^ B[i];
        var curr_xor = x;

        // Array B for the considered
        // value of K
        for (var j = 0; j < n; j++) {
            var y = A[j] ^ candidate;
            curr_xor = curr_xor ^ y;
        }

        // This means all the elements
        // are equal
        if (curr_xor == 0)
            numbers.add(candidate);
    }

    // Prvar all the possible value
    for (var i of numbers) {
        document.write(i + " ");
    }
}

// Driver Code
var A = [ 7, 8, 14 ];
var B = [ 5, 12, 3 ];
var N = A.length;
findPossibleValues(A, B, N);

// This code is contributed by shikhasingrajput
</script>
```

**Output:** 

```
11
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*