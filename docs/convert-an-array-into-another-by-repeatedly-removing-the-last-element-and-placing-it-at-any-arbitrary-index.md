# 通过重复移除最后一个元素并将其放在任意索引处，将一个数组转换为另一个数组

> 原文:[https://www . geeksforgeeks . org/通过重复移除最后一个元素并将其放置在任意索引处将数组转换为另一个数组/](https://www.geeksforgeeks.org/convert-an-array-into-another-by-repeatedly-removing-the-last-element-and-placing-it-at-any-arbitrary-index/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，这两个数组都由第一个 **N 个**自然数的[排列组成，任务是计算](https://www.geeksforgeeks.org/find-permutation-of-first-n-natural-numbers-that-satisfies-the-given-condition/)[最后一个数组元素](https://www.geeksforgeeks.org/get-first-and-last-elements-from-array-and-vector-in-cpp/)需要移动到数组中任意位置的最小次数 **A[]** ，以使两个数组 **A[]** 和**B[**相等。

***例:***

> **输入:** A[] = {1，2，3，4，5}，B[] = {1，5，2，3，4}
> **输出:** 1
> **解释:**
> 最初，数组 A[]为{1，2，3，4，5}。移动最后一个数组元素，即 5，并将其放在 arr[0] (= 1)和 arr[1](= 2)之间后，会将数组修改为{1，5，2，3，4}，这与数组 B[]相同。
> 因此，将数组 A[]转换为 B[]所需的最小操作数为 1。
> 
> **输入:** A[] = {3，2，1}，B[] = {1，2，3}
> **输出:** 2
> **说明:**
> 最初，数组 A[]为{3，2，1}。
> **操作 1:** 将最后一个数组元素即 1 移动到数组的开头后，将数组修改为{1，3，2}。
> **操作 2:** 移动数组的最后一个元素，即 2，并将其放在元素 arr[0] (= 1)和 arr[1] (= 3)之间后，将数组修改为{1，2，3}，与数组 B[]相同。
> 因此，将数组 A[]转换为 B[]所需的最小操作数为 2。

**方法:**给定的问题可以通过找到第一个置换的第一个 **i** 连续元素来解决，第一个置换与第二个置换的 [**子序列**](https://www.geeksforgeeks.org/given-two-strings-find-first-string-subsequence-second/) 相同，那么运算次数必须至少少于**(N–**I**)**，因为最后一个**(N–I)**元素可以被最佳选择并插入到所需的索引处。因此，**(N–I)**是将数组 **A[]** 转换为 **B[]** 所需的最小步数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to count the minimum number
// of operations required to convert
// the array A[] into array B[]
int minCount(int A[], int B[], int N)
{
    // Stores the index in the first
    // permutation A[] which is same
    // as the subsequence in B[]
    int i = 0;

    // Find the first i elements in A[]
    // which is a subsequence in B[]
    for (int j = 0; j < N; j++) {

        // If element A[i]
        // is same as B[j]
        if (A[i] == B[j]) {
            i++;
        }
    }

    // Return the count of
    // operations required
    return N - i;
}

// Driver Code
int main()
{
    int A[] = { 1, 2, 3, 4, 5 };
    int B[] = { 1, 5, 2, 3, 4 };

    int N = sizeof(A) / sizeof(A[0]);

    cout << minCount(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count the minimum number
// of operations required to convert
// the array A[] into array B[]
static int minCount(int A[], int B[], int N)
{

    // Stores the index in the first
    // permutation A[] which is same
    // as the subsequence in B[]
    int i = 0;

    // Find the first i elements in A[]
    // which is a subsequence in B[]
    for(int j = 0; j < N; j++)
    {

        // If element A[i]
        // is same as B[j]
        if (A[i] == B[j])
        {
            i++;
        }
    }

    // Return the count of
    // operations required
    return N - i;
}

// Driver Code
public static void main (String[] args)
{
    int A[] = { 1, 2, 3, 4, 5 };
    int B[] = { 1, 5, 2, 3, 4 };
    int N = A.length;

    System.out.println(minCount(A, B, N));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum number
# of operations required to convert
# the array A[] into array B[]
def minCount(A, B, N):

    # Stores the index in the first
    # permutation A[] which is same
    # as the subsequence in B[]
    i = 0

    # Find the first i elements in A[]
    # which is a subsequence in B[]
    for j in range(N):

        # If element A[i]
        # is same as B[j]
        if (A[i] == B[j]):
            i += 1

    # Return the count of
    # operations required
    return N - i

# Driver Code
if __name__ == '__main__':

    A = [ 1, 2, 3, 4, 5 ]
    B = [ 1, 5, 2, 3, 4 ]

    N = len(A)

    print(minCount(A, B, N))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the minimum number
// of operations required to convert
// the array A[] into array B[]
static int minCount(int[] A, int[] B, int N)
{

    // Stores the index in the first
    // permutation A[] which is same
    // as the subsequence in B[]
    int i = 0;

    // Find the first i elements in A[]
    // which is a subsequence in B[]
    for(int j = 0; j < N; j++)
    {

        // If element A[i]
        // is same as B[j]
        if (A[i] == B[j])
        {
            i++;
        }
    }

    // Return the count of
    // operations required
    return N - i;
}

// Driver Code
public static void Main(string[] args)
{
    int[] A = { 1, 2, 3, 4, 5 };
    int[] B = { 1, 5, 2, 3, 4 };
    int N = A.Length;

    Console.WriteLine(minCount(A, B, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the minimum number
// of operations required to convert
// the array A[] into array B[]
function minCount(A, B, N){

    // Stores the index in the first
    // permutation A[] which is same
    // as the subsequence in B[]
    var i = 0

    // Find the first i elements in A[]
    // which is a subsequence in B[]
    for(let j = 0; j < N; j++){

        // If element A[i]
        // is same as B[j]
        if (A[i] == B[j])
            i += 1
      }
    // Return the count of
    // operations required
    return N - i

}

// Driver Code

var A = [ 1, 2, 3, 4, 5 ]
var B = [ 1, 5, 2, 3, 4 ]

N = A.length

document.write(minCount(A, B, N))

// This code is contributed by AnkThon

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)