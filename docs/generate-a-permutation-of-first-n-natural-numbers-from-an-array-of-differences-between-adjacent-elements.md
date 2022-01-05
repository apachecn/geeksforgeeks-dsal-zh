# 从相邻元素之间的差异数组中生成前 N 个自然数的排列

> 原文:[https://www . geeksforgeeks . org/从相邻元素之间的差异数组中生成第一个 n 个自然数的排列/](https://www.geeksforgeeks.org/generate-a-permutation-of-first-n-natural-numbers-from-an-array-of-differences-between-adjacent-elements/)

给定一个由**(N–1)**组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是构造一个由第一个 **N** [**自然数**](https://www.geeksforgeeks.org/natural-numbers/) 组成的排列数组 **P[]** ，使得**arr[I]=(P[I+1]–P[I])**。如果不存在这样的排列，则打印**-1”**。

**示例:**

> **输入:** arr[] = {-1，2，-3，-1}
> **输出:** 4 3 5 2 1
> **解释:**
> 对于数组{4，3，5，2，1}，连续元素的相邻差数组为{ 4–3，5–3，2–5，1–2 } = {-1，2，-3，-1}，与数组 arr[]相同。
> 
> **输入:** arr[] = {1，1，1，1}
> **输出:** 1 2 3 4 5

**方法:**给定的问题可以通过考虑排列的第一个元素为 **0** 然后使用给定的数组 **arr[]构造一个新的[排列数组](https://www.geeksforgeeks.org/permute-the-elements-of-an-array-following-given-order/)来解决。**之后，在每个元素上加上新数组的[最小元素，使数组元素在**【1，N】**范围内。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

*   初始化一个数组，比如说大小为 **N** 的 **perm[]** 来存储结果排列。
*   将**perm【0】**初始化为 **0** ，同时初始化一个变量，比如说 **lastEle** 为 **0** 。
*   [使用变量 **i、**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**，并将**arr【I–1】**的值添加到元素 **lastEle** 中，并将**perm【I】**的值更新为 **lastEle** 。
*   初始化一个变量，对数组的最小元素**【彼尔姆】**说**最小元素**。
*   初始化一组整数 **st** 来存储排列的所有元素。另外，将变量 **mx** 初始化为 **0** ，以存储**perm【】**数组中的最大元素。
*   [遍历**perm【】**数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并将 **(-sm) + 1** 的值加到**perm【I】**的值上，将 **mx** 的值更新为 **max(mx，perm【I】)**并将**perm【I】**加到 **st** 上。
*   完成上述步骤后，如果 **mx** 的值和 HashSet **st** 的大小为 **N** ，则[打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/) **perm[]** 作为结果数组。否则，打印 **-1** 。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the permutation of
// N integers from the given difference
// array A[]
void findPermutation(int A[], int N)
{
    int lasEle = 0;

    // Stores the resultant permutation
    int perm[N];
    perm[0] = 0;

    for (int i = 1; i < N; i++) {

        // Update the value of lastEle
        lasEle += A[i - 1];

        // Initialize the value of
        // perm[i]
        perm[i] = lasEle;
    }

    // Stores the minimum element of
    // the array perm[]
    int sm = *min_element(perm, perm + N);

    // Stores the elements of the
    // permutation array perm[]
    unordered_set<int> st;
    int mx = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update the value of perm[i]
        perm[i] += (-sm) + 1;

        // Update the value of mx
        mx = max(mx, perm[i]);

        // Insert the current element
        // in the hashset
        st.insert(perm[i]);
    }

    // Check if the maximum element and
    // the size of hashset is N or not
    if (mx == N and st.size() == N) {

        // Print the permutation
        for (int i = 0; i < N; i++) {
            cout << perm[i] << " ";
        }
    }

    // Otherwise print -1
    else {
        cout << -1 << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { -1, 2, -3, -1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    findPermutation(arr, N + 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the permutation of
// N integers from the given difference
// array A[]
static void findPermutation(int []A, int N)
{
    int lasEle = 0;

    // Stores the resultant permutation
    int []perm = new int[N];
    perm[0] = 0;

    for (int i = 1; i < N; i++) {

        // Update the value of lastEle
        lasEle += A[i - 1];

        // Initialize the value of
        // perm[i]
        perm[i] = lasEle;
    }

    // Stores the minimum element of
    // the array perm[]
     int sm = perm[0]; 
        //Loop through the array 
        for (int i = 0; i < perm.length; i++) { 
            //Compare elements of array with min 
           if(perm[i] <sm) 
               sm = perm[i]; 
        }

    // Stores the elements of the
    // permutation array perm[]
    Set<Integer> st = new HashSet<Integer>();
    int mx = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update the value of perm[i]
        perm[i] += (-sm) + 1;

        // Update the value of mx
        mx = Math.max(mx, perm[i]);

        // Insert the current element
        // in the hashset
        st.add(perm[i]);
    }

    // Check if the maximum element and
    // the size of hashset is N or not
    if (mx == N && st.size() == N) {

        // Print the permutation
        for (int i = 0; i < N; i++) {
            System.out.print(perm[i]+" ");
        }
    }

    // Otherwise print -1
    else {
        System.out.print(-1);
    }
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { -1, 2, -3, -1 };
    int N = arr.length;
    findPermutation(arr, N + 1);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the permutation of
# N integers from the given difference
# array A[]
def findPermutation(A, N):
    lasEle = 0

    # Stores the resultant permutation
    perm = [0]*N
    perm[0] = 0

    for i in range(1,N):
        # Update the value of lastEle
        lasEle += A[i - 1]

        # Initialize the value of
        # perm[i]
        perm[i] = lasEle

    # Stores the minimum element of
    # the array perm[]
    sm = min(perm)

    # Stores the elements of the
    # permutation array perm[]
    st = {}
    mx = 0

    # Traverse the array
    for i in range(N):
        # Update the value of perm[i]
        perm[i] += (-sm) + 1

        # Update the value of mx
        mx = max(mx, perm[i])

        # Insert the current element
        # in the hashset
        st[perm[i]] = 1

    # Check if the maximum element and
    # the size of hashset is N or not
    if (mx == N and len(st) == N):

        # Prthe permutation
        for i in range(N):
            print(perm[i],end=" ")
    # Otherwise pr-1
    else:
        print(-1,end=" ")

# Driver Code
if __name__ == '__main__':
    arr = [-1, 2, -3, -1]
    N = len(arr)
    findPermutation(arr, N + 1)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;
using System.Collections.Generic;

class GFG {

// Function to find the permutation of
// N integers from the given difference
// array A[]
static void findPermutation(int[] A, int N)
{
    int lasEle = 0;

    // Stores the resultant permutation
    int[] perm = new int[N];
    perm[0] = 0;

    for (int i = 1; i < N; i++) {

        // Update the value of lastEle
        lasEle += A[i - 1];

        // Initialize the value of
        // perm[i]
        perm[i] = lasEle;
    }

    // Stores the minimum element of
    // the array perm[]
    int sm = perm.Min();

    // Stores the elements of the
    // permutation array perm[]
   List<int> st = new List<int>();
    int mx = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update the value of perm[i]
        perm[i] += (-sm) + 1;

        // Update the value of mx
        mx = Math.Max(mx, perm[i]);

        // Insert the current element
        // in the hashset
        st.Add(perm[i]);
    }

    // Check if the maximum element and
    // the size of hashset is N or not
    if (mx == N && st.Count == N) {

        // Print the permutation
        for (int i = 0; i < N; i++) {
           Console.Write(perm[i] + " ");
        }
    }

    // Otherwise print -1
    else {
        Console.Write(-1 + " ");
    }
}

    // Driver Code
    static void Main()
    {
        int[] arr= { -1, 2, -3, -1 };
    int N = arr.Length;
    findPermutation(arr, N + 1);
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the permutation of
// N integers from the given difference
// array A[]
function findPermutation(A, N) {
    let lasEle = 0;

    // Stores the resultant permutation
    let perm = new Array(N);
    perm[0] = 0;

    for (let i = 1; i < N; i++) {

        // Update the value of lastEle
        lasEle += A[i - 1];

        // Initialize the value of
        // perm[i]
        perm[i] = lasEle;
    }

    // Stores the minimum element of
    // the array perm[]

    let temp = [...perm];
    let sm = temp.sort((a, b) => a - b)[0]

    // Stores the elements of the
    // permutation array perm[]
    let st = new Set();
    let mx = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // Update the value of perm[i]
        perm[i] += (-sm) + 1;

        // Update the value of mx
        mx = Math.max(mx, perm[i]);

        // Insert the current element
        // in the hashset
        st.add(perm[i]);
    }

    // Check if the maximum element and
    // the size of hashset is N or not
    if (mx == N && st.size == N) {

        // Print the permutation
        for (let i of perm) {
            document.write(i + " ")
        }
    }

    // Otherwise print -1
    else {
        document.write(-1 + " ");
    }
}

// Driver Code

let arr = [-1, 2, -3, -1];
let N = arr.length
findPermutation(arr, N + 1);

</script>
```

**Output:** 

```
4 3 5 2 1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)