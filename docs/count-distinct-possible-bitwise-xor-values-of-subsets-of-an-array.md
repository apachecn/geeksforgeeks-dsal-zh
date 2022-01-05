# 计算数组子集的不同的可能位异或值

> 原文:[https://www . geeksforgeeks . org/count-distinct-可能-按位异或-数组子集的值/](https://www.geeksforgeeks.org/count-distinct-possible-bitwise-xor-values-of-subsets-of-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到集合 **S** 的[大小，使得数组 **arr[]** 的任意](https://www.geeksforgeeks.org/setsize-c-stl/)[子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)存在于集合 **S** 中。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 8
> **解释:**
> 数组子集所有可能的按位异或值 **arr[]** 均为{0，1，2，3，4，5，6，7}。
> 因此，所需集合的大小为 8。
> 
> **输入:**arr[]= { 6 }
> T3】输出: 1

**天真方法:**最简单的方法是[生成给定数组**arr【】**的所有可能的非空子集](https://www.geeksforgeeks.org/find-distinct-subset-subsequence-sums-array/)，并将所有子集的[按位异或存储在](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。生成所有子集后，打印作为结果获得的集合的大小。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Stores the Bitwise XOR
// of every possible subset
unordered_set<int> s;

// Function to generate all
// combinations of subsets and
// store their Bitwise XOR in set S
void countXOR(int arr[], int comb[],
              int start, int end,
              int index, int r)
{
    // If the end of the
    // subset is reached
    if (index == r) {

        // Stores the Bitwise XOR
        // of the current subset
        int new_xor = 0;

        // Iterate comb[] to find XOR
        for (int j = 0; j < r; j++) {
            new_xor ^= comb[j];
        }

        // Insert the Bitwise
        // XOR of R elements
        s.insert(new_xor);
        return;
    }

    // Otherwise, iterate to
    // generate all possible subsets
    for (int i = start;
         i <= end && end - i + 1 >= r - index; i++) {
        comb[index] = arr[i];

        // Recursive call for next index
        countXOR(arr, comb, i + 1, end,
                 index + 1, r);
    }
}

// Function to find the size of the
// set having Bitwise XOR of all the
// subsets of the given array
void maxSizeSet(int arr[], int N)
{
    // Iterate over the given array
    for (int r = 2; r <= N; r++) {
        int comb[r + 1];

        // Generate all possible subsets
        countXOR(arr, comb, 0, N - 1,
                 0, r);
    }

    // Print the size of the set
    cout << s.size() << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxSizeSet(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Stores the Bitwise XOR
// of every possible subset
static HashSet<Integer> s;

// Function to generate all
// combinations of subsets and
// store their Bitwise XOR in set S
static void countXOR(int arr[], int comb[],
                     int start, int end,
                     int index, int r)
{

    // If the end of the
    // subset is reached
    if (index == r)
    {

        // Stores the Bitwise XOR
        // of the current subset
        int new_xor = 0;

        // Iterate comb[] to find XOR
        for(int j = 0; j < r; j++)
        {
            new_xor ^= comb[j];
        }

        // Insert the Bitwise
        // XOR of R elements
        s.add(new_xor);
        return;
    }

    // Otherwise, iterate to
    // generate all possible subsets
    for(int i = start;
            i <= end && end - i + 1 >= r - index;
            i++)
    {
        comb[index] = arr[i];

        // Recursive call for next index
        countXOR(arr, comb, i + 1, end, index + 1, r);
    }
}

// Function to find the size of the
// set having Bitwise XOR of all the
// subsets of the given array
static void maxSizeSet(int arr[], int N)
{

    // Iterate over the given array
    for(int r = 1; r <= N; r++)
    {
        int comb[] = new int[r + 1];

        // Generate all possible subsets
        countXOR(arr, comb, 0, N - 1, 0, r);
    }

    // Print the size of the set
    System.out.println(s.size());
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    // Initialize set
    s = new HashSet<>();

    // Function Call
    maxSizeSet(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the Bitwise XOR
# of every possible subset
s = set([])

# Function to generate all
# combinations of subsets and
# store their Bitwise XOR in set S
def countXOR(arr, comb, start, end, index, r):

    # If the end of the
    # subset is reached
    if (index == r) :

        # Stores the Bitwise XOR
        # of the current subset
        new_xor = 0

        # Iterate comb[] to find XOR
        for j in range(r):
            new_xor ^= comb[j]

        # Insert the Bitwise
        # XOR of R elements
        s.add(new_xor)
        return

    # Otherwise, iterate to
    # generate all possible subsets
    i = start
    while i <= end and (end - i + 1) >= (r - index):
        comb[index] = arr[i]

        # Recursive call for next index
        countXOR(arr, comb, i + 1, end, index + 1, r)
        i += 1

# Function to find the size of the
# set having Bitwise XOR of all the
# subsets of the given array
def maxSizeSet(arr, N):

    # Iterate over the given array
    for r in range(2, N + 1):
        comb = [0]*(r + 1)

        # Generate all possible subsets
        countXOR(arr, comb, 0, N - 1, 0, r)

    # Print the size of the set
    print(len(s))

arr = [ 1, 2, 3, 4, 5 ]
N = len(arr)

# Function Call
maxSizeSet(arr, N)

# This code is contributed by decode2207.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

// Stores the Bitwise XOR
// of every possible subset
static HashSet<int> s;

// Function to generate all
// combinations of subsets and
// store their Bitwise XOR in set S
static void countXOR(int []arr, int []comb,
                     int start, int end,
                     int index, int r)
{

    // If the end of the
    // subset is reached
    if (index == r)
    {

        // Stores the Bitwise XOR
        // of the current subset
        int new_xor = 0;

        // Iterate comb[] to find XOR
        for(int j = 0; j < r; j++)
        {
            new_xor ^= comb[j];
        }

        // Insert the Bitwise
        // XOR of R elements
        s.Add(new_xor);
        return;
    }

    // Otherwise, iterate to
    // generate all possible subsets
    for(int i = start;
            i <= end && end - i + 1 >= r - index;
            i++)
    {
        comb[index] = arr[i];

        // Recursive call for next index
        countXOR(arr, comb, i + 1, end, index + 1, r);
    }
}

// Function to find the size of the
// set having Bitwise XOR of all the
// subsets of the given array
static void maxSizeSet(int []arr, int N)
{

    // Iterate over the given array
    for(int r = 1; r <= N; r++)
    {
        int []comb = new int[r + 1];

        // Generate all possible subsets
        countXOR(arr, comb, 0, N - 1, 0, r);
    }

    // Print the size of the set
    Console.WriteLine(s.Count);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    // Initialize set
    s = new HashSet<int>();

    // Function Call
    maxSizeSet(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Stores the Bitwise XOR
// of every possible subset
let s;

// Function to generate all
// combinations of subsets and
// store their Bitwise XOR in set S
function countXOR(arr,comb,start,end,index,r)
{
    // If the end of the
    // subset is reached
    if (index == r)
    {

        // Stores the Bitwise XOR
        // of the current subset
        let new_xor = 0;

        // Iterate comb[] to find XOR
        for(let j = 0; j < r; j++)
        {
            new_xor ^= comb[j];
        }

        // Insert the Bitwise
        // XOR of R elements
        s.add(new_xor);
        return;
    }

    // Otherwise, iterate to
    // generate all possible subsets
    for(let i = start;
            i <= end && end - i + 1 >= r - index;
            i++)
    {
        comb[index] = arr[i];

        // Recursive call for next index
        countXOR(arr, comb, i + 1, end, index + 1, r);
    }
}

// Function to find the size of the
// set having Bitwise XOR of all the
// subsets of the given array
function maxSizeSet(arr,N)
{
    // Iterate over the given array
    for(let r = 1; r <= N; r++)
    {
        let comb = new Array(r + 1);

        // Generate all possible subsets
        countXOR(arr, comb, 0, N - 1, 0, r);
    }

    // Print the size of the set
    document.write(s.size);
}

// Driver Code
let arr=[1, 2, 3, 4, 5 ];
let N = arr.length;

// Initialize set
s = new Set();

// Function Call
maxSizeSet(arr, N);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)和[高斯消去法](https://www.geeksforgeeks.org/gaussian-elimination/)进行优化。按照以下步骤解决问题:

*   初始化一个辅助数组，比如大小为 **20、**的 **dp[]** ，存储每个数组元素的[掩码，并用 **0** 初始化。](https://www.geeksforgeeks.org/bit-tricks-competitive-programming/)
*   初始化一个变量，说 **ans** 为 **0** ，存储数组 **dp[]** 的大小。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个数组元素 **arr[]，**执行以下步骤:
    *   初始化一个变量，说**将**屏蔽为**arr【I】**，以检查最高有效设置位的位置。
    *   如果从**arr【I】**右侧起的 **i <sup>第</sup>位**被设置为且**DP【I】**为 **0** ，则更新数组**DP【I】**为**2<sup>I</sup>T17】，并将 **ans** 的值增加 **1** 和 [break](https://www.geeksforgeeks.org/break-statement-cc/)**
    *   否则，将**掩码**的值更新为**掩码**和**DP【I】**的按位异或。
*   完成上述步骤后，打印 **2 <sup>和</sup>T3 的值，作为所需元素集的合成大小。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int const size = 20;

// Stores the mask of the vector
int dp[size];

// Stores the current size of dp[]
int ans;

// Function to store the
// mask of given integer
void insertVector(int mask)
{
    // Iterate over the range [0, 20]
    for (int i = 0; i < 20; i++) {

        // If i-th bit 0
        if ((mask & 1 << i) == 0)
            continue;

        // If dp[i] is zero
        if (!dp[i]) {

            // Store the position in dp
            dp[i] = mask;

            // Increment the answer
            ++ans;

            // Return from the loop
            return;
        }

        // mask = mask XOR dp[i]
        mask ^= dp[i];
    }
}

// Function to find the size of the
// set having Bitwise XOR of all the
// subset of the given array
void maxSizeSet(int arr[], int N)
{
    // Traverse the array
    for (int i = 0; i < N; i++) {
        insertVector(arr[i]);
    }

    // Print the answer
    cout << (1 << ans) << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxSizeSet(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{
  final static int size = 20;

  // Stores the mask of the vector
  static int[] dp = new int[size];

  // Stores the current size of dp[]
  static int ans;

  // Function to store the
  // mask of given integer
  static void insertVector(int mask)
  {
    // Iterate over the range [0, 20]
    for (int i = 0; i < 20; i++) {

      // If i-th bit 0
      if ((mask & 1 << i) == 0)
        continue;

      // If dp[i] is zero
      if (dp[i]==0) {

        // Store the position in dp
        dp[i] = mask;

        // Increment the answer
        ++ans;

        // Return from the loop
        return;
      }

      // mask = mask XOR dp[i]
      mask ^= dp[i];
    }
  }

  // Function to find the size of the
  // set having Bitwise XOR of all the
  // subset of the given array
  static void maxSizeSet(int[] arr, int N)
  {

    // Traverse the array
    for (int i = 0; i < N; i++) {
      insertVector(arr[i]);
    }

    // Print the answer
    System.out.println(1<<ans);
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] arr = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    // Function Call
    maxSizeSet(arr, N);
  }
}

//This code is contributed by Hritik Dwivedi
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Stores the mask of the vector
dp = [0]*20

# Stores the current 20 of dp[]
ans = 0

# Function to store the
# mask of given integer
def insertVector(mask):
    global dp, ans

    # Iterate over the range [0, 20]
    for i in range(20):

        # If i-th bit 0
        if ((mask & 1 << i) == 0):
            continue

        # If dp[i] is zero
        if (not dp[i]):

            # Store the position in dp
            dp[i] = mask

            # Increment the answer
            ans += 1

            # Return from the loop
            return

        # mask = mask XOR dp[i]
        mask ^= dp[i]

# Function to find the 20 of the
# set having Bitwise XOR of all the
# subset of the given array
def maxSizeSet(arr, N):

    # Traverse the array
    for i in range(N):
        insertVector(arr[i])

    # Prthe answer
    print ((1 << ans))

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 3, 4, 5]
    N = len(arr)

    # Function Call
    maxSizeSet(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int size = 20;

// Stores the mask of the vector
static int[] dp = new int[size];

// Stores the current size of dp[]
static int ans;

// Function to store the
// mask of given integer
static void insertVector(int mask)
{

    // Iterate over the range [0, 20]
    for(int i = 0; i < 20; i++)
    {

        // If i-th bit 0
        if ((mask & 1 << i) == 0)
            continue;

        // If dp[i] is zero
        if (dp[i] == 0)
        {

            // Store the position in dp
            dp[i] = mask;

            // Increment the answer
            ++ans;

            // Return from the loop
            return;
        }

        // mask = mask XOR dp[i]
        mask ^= dp[i];
    }
}

// Function to find the size of the
// set having Bitwise XOR of all the
// subset of the given array
static void maxSizeSet(int[] arr, int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        insertVector(arr[i]);
    }

    // Print the answer
    Console.WriteLine(1 << ans);
}

// Driver code
public static void Main(string[] args)
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    // Function Call
    maxSizeSet(arr, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach
let size = 20;

// Stores the mask of the vector
var dp = new Array(size).fill(0);

// Stores the current size of dp[]
let ans = 0;

// Function to store the
// mask of given integer
function insertVector(mask)
{

    // Iterate over the range [0, 20]
    for(let i = 0; i < 20; i++)
    {

        // If i-th bit 0
        if ((mask & 1 << i) == 0)
            continue;

        // If dp[i] is zero
        if (dp[i] == 0)
        {

            // Store the position in dp
            dp[i] = mask;

            // Increment the answer
            ++ans;

            // Return from the loop
            return;
        }

        // mask = mask XOR dp[i]
        mask ^= dp[i];
    }
}

// Function to find the size of the
// set having Bitwise XOR of all the
// subset of the given array
function maxSizeSet(arr, N)
{

    // Traverse the array
    for(let i = 0; i < N; i++)
    {
        insertVector(arr[i]);
    }

    // Print the answer
    document.write(1<<ans);
}

// Driver Code
let arr = [ 1, 2, 3, 4, 5 ];
let N = arr.length;

// Function Call
maxSizeSet(arr, N);

// This code is contributed by nitin_sharma   

</script>
```

**Output:** 

```
8
```

***时间复杂度:** O(M * N)*
***辅助空间:** O(M * N)*