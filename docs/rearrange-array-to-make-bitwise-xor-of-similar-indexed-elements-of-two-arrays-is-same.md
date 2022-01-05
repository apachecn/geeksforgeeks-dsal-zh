# 重新排列数组，使两个数组的相似索引元素按位异或相同

> 原文:[https://www . geeksforgeeks . org/array-to-make-bitwise-xor-of-indexed-elements-of-two-array-is-same/](https://www.geeksforgeeks.org/rearrange-array-to-make-bitwise-xor-of-similar-indexed-elements-of-two-arrays-is-same/)

给定由 **N** 个整数( **N** 为奇数)组成的两个[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[]** 和 **B[]** ，任务是重新排列数组 **B[]** ，使得对于每个 **1 ≤ i ≤ N** ，[按位异或](https://www.geeksforgeeks.org/tag/xor/)**A[I]**和 **B[i]** 相同。如果不可能重新排列，打印**-1”**。否则，打印重排。

**示例:**

> **输入:** A[] = {1，2，3，4，5}，B[] = {5，4，3，2，1}
> **输出:** {1，2，3，4，5}
> **解释:**
> 重新排列数组 B[]{ 1，2，3，4，5}，每对对应的数组元素之间的按位异或是相同的，即 0。
> 
> **输入:** A[] = {14，21，33，49，53}，B[] = {54，50，34，22，14}
> **输出:** -1

**天真方法:**最简单的方法是[生成数组 **B[]** 的所有可能排列](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)，并打印与相应元素按位异或相同的数组组合。

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**有效方法:**思路是利用[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的交换性质。以下是步骤:

*   求两个数组元素的按位异或，取值为 **xor_value** 。
*   [在](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 中存储阵 T2【B】的元素频率。
*   要重新排列 **B[]** [的数组元素，遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **B[]** ，并执行以下操作:
    *   将该数组的当前元素更新为 **A[i]^xor_value** 。
    *   如果更新的当前元素的频率大于 1，则递减它。
    *   否则没有这种可能的安排，跳出循环，打印**-1”**。
*   完成上述步骤后，打印数组 **B[]** ，因为它包含重新排列的数组。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array
// B[] such that A[i] ^ B[i] is same
// for each element
vector<int> rearrangeArray(
    vector<int>& A, vector<int>& B, int N)
{
    // Store frequency of elements
    map<int, int> m;

    // Stores xor value
    int xor_value = 0;

    for (int i = 0; i < N; i++) {

        // Taking xor of all the
        // values of both arrays
        xor_value ^= A[i];
        xor_value ^= B[i];

        // Store frequency of B[]
        m[B[i]]++;
    }

    for (int i = 0; i < N; i++) {

        // Find the array B[] after
        // rearrangement
        B[i] = A[i] ^ xor_value;

        // If the updated value is
        // present then decrement
        // its frequency
        if (m[B[i]]) {
            m[B[i]]--;
        }

        // Otherwise return empty vector
        else
            return vector<int>{};
    }

    return B;
}

// Utility function to rearrange the
// array B[] such that A[i] ^ B[i]
// is same for each element
void rearrangeArrayUtil(
    vector<int>& A, vector<int>& B, int N)
{
    // Store rearranged array B
    vector<int> ans
        = rearrangeArray(A, B, N);

    // If rearrangement possible
    if (ans.size()) {
        for (auto x : ans) {
            cout << x << " ";
        }
    }

    // Otherwise return -1
    else {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    // Given vector A
    vector<int> A = { 13, 21, 33, 49, 53 };

    // Given vector B
    vector<int> B = { 54, 50, 34, 22, 14 };

    // Size of the vector
    int N = (int)A.size();

    // Function Call
    rearrangeArrayUtil(A, B, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to rearrange the array
// B[] such that A[i] ^ B[i] is same
// for each element
static ArrayList<Integer> rearrangeArray(
       ArrayList<Integer> A,
       ArrayList<Integer> B, int N)
{

    // Store frequency of elements
    HashMap<Integer,
            Integer> m = new HashMap<Integer,
                                     Integer>();

    // Stores xor value
    int xor_value = 0;

    for(int i = 0; i < N; i++)
    {

        // Taking xor of all the
        // values of both arrays
        xor_value ^= A.get(i);
        xor_value ^= B.get(i);

        // Store frequency of B[]
        m.put(B.get(i),
              m.getOrDefault(B.get(i) + 1, 0));
    }

    for(int i = 0; i < N; i++)
    {

        // Find the array B[] after
        // rearrangement
        B.set(i, A.get(i) ^ xor_value);

        // If the updated value is
        // present then decrement
        // its frequency
        if (m.getOrDefault(B.get(i), -1) != -1)
        {
            m.put(B.get(i),
                  m.getOrDefault(B.get(i), 0) - 1);
        }

        // Otherwise return empty vector
        else
            return (new ArrayList<Integer>());
    }
    return B;
}

// Utility function to rearrange the
// array B[] such that A[i] ^ B[i]
// is same for each element
static void rearrangeArrayUtil(ArrayList<Integer> A,
                               ArrayList<Integer> B, int N)
{

    // Store rearranged array B
    ArrayList<Integer> ans = rearrangeArray(A, B, N);

    // If rearrangement possible
    if (ans.size() != 0)
    {
        for(int i = 0; i < ans.size(); i++)
        {
            System.out.print(ans.get(i) + " ");
        }
    }

    // Otherwise return -1
    else
    {
        System.out.println("-1");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given vector A
    ArrayList<Integer> A = new ArrayList<Integer>(
        Arrays.asList(13, 21, 33, 49, 53));

    // Given vector B
    ArrayList<Integer> B = new ArrayList<Integer>(
        Arrays.asList(54, 50, 34, 22, 14));

    // Size of the vector
    int N = (int)A.size();

    // Function Call
    rearrangeArrayUtil(A, B, N);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to rearrange the array
# B[] such that A[i] ^ B[i] is same
# for each element
def rearrangeArray(A, B, N):

  # Store frequency of elements
  m = {}

  # Stores xor value
  xor_value = 0

  for i in range(0, N):

    # Taking xor of all the
    # values of both arrays
    xor_value ^= A[i]
    xor_value ^= B[i]

    # Store frequency of B[]
    if B[i] in m:
      m[B[i]] = m[B[i]] + 1
    else:
      m[B[i]] = 1

  for i in range(0, N):

    # Find the array B[] after
    # rearrangement
    B[i] = A[i] ^ xor_value

    # If the updated value is
    # present then decrement
    # its frequency
    if B[i] in m:
      m[B[i]] = m[B[i]] - 1

    # Otherwise return empty vector
    else:
      X = []
      return X

  return B

# Utility function to rearrange the
# array B[] such that A[i] ^ B[i]
# is same for each element
def rearrangeArrayUtil(A, B, N):

  # Store rearranged array B
  ans = rearrangeArray(A, B, N)

  # If rearrangement possible
  if (len(ans) > 0):
     for x in ans:
        print(x, end = ' ')

  # Otherwise return -1
  else:
    print("-1")

# Driver Code
if __name__ == '__main__':

  # Given vector A
  A = [ 13, 21, 33, 49, 53 ]

  # Given vector B
  B = [ 54, 50, 34, 22, 14 ]

  # Size of the vector
  N = len(A)

  # Function Call
  rearrangeArrayUtil(A, B, N)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to rearrange the array
// B[] such that A[i] ^ B[i] is same
// for each element
static ArrayList rearrangeArray(ArrayList A,
                                ArrayList B, int N)
{

    // Store frequency of elements
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    // Stores xor value
    int xor_value = 0;

    for(int i = 0; i < N; i++)
    {

        // Taking xor of all the
        // values of both arrays
        xor_value ^= (int)A[i];
        xor_value ^= (int)B[i];

        // Store frequency of B[]
        if (!m.ContainsKey((int)B[i]))
            m.Add((int)B[i], 1);
        else
            m[(int)B[i]] = m[(int)B[i]] + 1;
    }

    for(int i = 0; i < N; i++)
    {

        // Find the array B[] after
        // rearrangement
        B[i] = (int)A[i] ^ xor_value;

        // If the updated value is
        // present then decrement
        // its frequency
        if (m.ContainsKey((int)B[i]))
        {
            m[(int)B[i]]--;
        }

        // Otherwise return empty vector
        else
            return (new ArrayList());
    }
    return B;
}

// Utility function to rearrange the
// array B[] such that A[i] ^ B[i]
// is same for each element
static void rearrangeArrayUtil(ArrayList A,
                               ArrayList B,
                               int N)
{

    // Store rearranged array B
    ArrayList ans = rearrangeArray(A, B, N);

    // If rearrangement possible
    if (ans.Count != 0)
    {
        for(int i = 0; i < ans.Count; i++)
        {
            Console.Write(ans[i] + " ");
        }
    }

    // Otherwise return -1
    else
    {
        Console.WriteLine("-1");
    }
}

// Driver Code
public static void Main()
{

    // Given vector A
    ArrayList A = new ArrayList{ 13, 21, 33, 49, 53 };

    // Given vector B
    ArrayList B = new ArrayList{ 54, 50, 34, 22, 14 };

    // Size of the vector
    int N = A.Count;

    // Function Call
    rearrangeArrayUtil(A, B, N);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to rearrange the array
// B[] such that A[i] ^ B[i] is same
// for each element
function rearrangeArray(A, B, N)
{

    // Store frequency of elements
    let m = new Map();

    // Stores xor value
    let xor_value = 0;

    for (let i = 0; i < N; i++) {

        // Taking xor of all the
        // values of both arrays
        xor_value ^= A[i];
        xor_value ^= B[i];

        // Store frequency of B[]
        if (m.has(B[i])) {
            m.set(B[i], m.get(B[i]) + 1)
        } else {
            m.set(B[i], 1)
        }
    }

    for (let i = 0; i < N; i++) {

        // Find the array B[] after
        // rearrangement
        B[i] = A[i] ^ xor_value;

        // If the updated value is
        // present then decrement
        // its frequency
        if (m.has(B[i])) {
            m.set(B[i], m.get(B[i]) - 1)
        }

        // Otherwise return empty vector
        else
            return [];
    }

    return B;
}

// Utility function to rearrange the
// array B[] such that A[i] ^ B[i]
// is same for each element
function rearrangeArrayUtil(A, B, N)
{

    // Store rearranged array B
    let ans = rearrangeArray(A, B, N);

    // If rearrangement possible
    if (ans.length > 0) {
        for (let x of ans) {
            document.write(x + " ");
        }
    }

    // Otherwise return -1
    else {
        document.write("-1");
    }
}

// Driver Code

// Given vector A
let A = [13, 21, 33, 49, 53];

// Given vector B
let B = [54, 50, 34, 22, 14];

// Size of the vector
let N = A.length;

// Function Call
rearrangeArrayUtil(A, B, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
14 22 34 50 54
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)