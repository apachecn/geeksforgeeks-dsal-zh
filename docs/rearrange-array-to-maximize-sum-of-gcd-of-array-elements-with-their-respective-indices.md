# 重新排列数组，以最大化数组元素与其各自索引的 GCD 之和

> 原文:[https://www . geeksforgeeks . org/重排数组以最大化数组元素及其各自索引的 gcd 总和/](https://www.geeksforgeeks.org/rearrange-array-to-maximize-sum-of-gcd-of-array-elements-with-their-respective-indices/)

给定一个由第一个 **N** 个自然数的排列组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过重新排列给定的数组元素来找到**σGCD(arr[I]，i)** ( *1 基索引*)的最大可能值。

**示例:**

> **输入:** arr[] = { 2，1}
> **输出:** 6
> **解释:**
> 将给定数组重新排列为{ 2，1}。
> σGCD(arr[I]，i) = GCD(arr[1]，1) + GCD(arr[2]，2) = GCD(2，1) + GCD(1，2)= 2
> 将给定数组重新排列为{ 1，2 }。
> σGCD(arr[I]，i) = GCD(arr[1]，1) + GCD(arr[2]，2) = GCD(1，1) + GCD(2，2) = 3
> 因此，要求的输出为 3
> 
> **输入:** arr[] = { 4，5，3，2，1 }
> T3】输出: 15

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)的所有可能排列，对于每个排列，求**σGCD(arr[I]，i)** 的值。最后打印每个排列的**σGCD(arr[I]，i)** 的最大值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// GCD(arr[i], i) by rearranging the array
int findMaxValByRearrArr(int arr[], int N)
{

    // Sort the array in
    // ascending order
    sort(arr, arr + N);

    // Stores maximum sum of GCD(arr[i], i)
    // by rearranging the array elements
    int res = 0;

    // Generate all possible
    // permutations of the array
    do {

        // Stores sum of GCD(arr[i], i)
        int sum = 0;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update sum
            sum += __gcd(i + 1, arr[i]);
        }

        // Update res
        res = max(res, sum);

    } while (next_permutation(arr, arr + N));

    return res;
}

// Driver Code
int main()
{

    int arr[] = { 3, 2, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findMaxValByRearrArr(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

  // Function to find the maximum sum of
  // GCD(arr[i], i) by rearranging the array
  static int findMaxValByRearrArr(int arr[], int N)
  {

    // Sort the array in
    // ascending order
    Arrays.sort(arr);

    // Stores maximum sum of GCD(arr[i], i)
    // by rearranging the array elements
    int res = 0;

    // Generate all possible
    // permutations of the array
    do {

      // Stores sum of GCD(arr[i], i)
      int sum = 0;

      // Traverse the array
      for (int i = 0; i < N; i++) {

        // Update sum
        sum += __gcd(i + 1, arr[i]);
      }

      // Update res
      res = Math.max(res, sum);

    } while (next_permutation(arr));

    return res;
  }
  static int __gcd(int a, int b) 
  { 
    return b == 0? a:__gcd(b, a % b);    
  }
  static boolean next_permutation(int[] p)
  {
    for (int a = p.length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (int b = p.length - 1;; --b)
          if (p[b] > p[a])
          {
            int t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.length - 1; a < b; ++a, --b)
            {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 3, 2, 1 };
    int N = arr.length;
    System.out.print(findMaxValByRearrArr(arr, N));
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum sum of
# GCD(arr[i], i) by rearranging the array
def findMaxValByRearrArr(arr, N):

    # Sort the array in
    # ascending order
    arr.sort()

    # Stores maximum sum of GCD(arr[i], i)
    # by rearranging the array elements
    res = 0

    # Generate all possible
    # permutations of the array
    while (True):

        # Stores sum of GCD(arr[i], i)
        Sum = 0

        # Traverse the array
        for i in range(N):

            # Update sum
            Sum += __gcd(i + 1, arr[i])

        # Update res
        res = max(res, Sum)

        if (not next_permutation(arr)):
            break

    return res

def __gcd(a, b): 

    if b == 0:
        return a
    else:
        return __gcd(b, a % b)

def next_permutation(p):

    for a in range(len(p) - 2, -1, -1):
        if (p[a] < p[a + 1]):
            b = len(p) - 1

            while True:
                if (p[b] > p[a]):
                    t = p[a]
                    p[a] = p[b]
                    p[b] = t
                    a += 1
                    b = len(p) - 1

                    while a < b:
                        t = p[a]
                        p[a] = p[b]
                        p[b] = t
                        a += 1
                        b -= 1

                    return True

                b -= 1

    return False

# Driver code   
arr = [ 3, 2, 1 ]
N = len(arr)

print(findMaxValByRearrArr(arr, N))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to find the maximum sum of
  // GCD(arr[i], i) by rearranging the array
  static int findMaxValByRearrArr(int []arr, int N)
  {

    // Sort the array in
    // ascending order
    Array.Sort(arr);

    // Stores maximum sum of GCD(arr[i], i)
    // by rearranging the array elements
    int res = 0;

    // Generate all possible
    // permutations of the array
    do
    {

      // Stores sum of GCD(arr[i], i)
      int sum = 0;

      // Traverse the array
      for (int i = 0; i < N; i++)
      {

        // Update sum
        sum += __gcd(i + 1, arr[i]);
      }

      // Update res
      res = Math.Max(res, sum);

    } while (next_permutation(arr));

    return res;
  }
  static int __gcd(int a, int b) 
  { 
    return b == 0? a:__gcd(b, a % b);    
  }
  static bool next_permutation(int[] p)
  {
    for (int a = p.Length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (int b = p.Length - 1;; --b)
          if (p[b] > p[a])
          {
            int t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.Length - 1; a < b; ++a, --b)
            {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 3, 2, 1 };
    int N = arr.Length;
    Console.Write(findMaxValByRearrArr(arr, N));
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

  // Function to find the maximum sum of
  // GCD(arr[i], i) by rearranging the array
  function findMaxValByRearrArr(arr, N)
  {

    // Sort the array in
    // ascending order
    arr.sort();

    // Stores maximum sum of GCD(arr[i], i)
    // by rearranging the array elements
    let res = 0;

    // Generate all possible
    // permutations of the array
    do {

      // Stores sum of GCD(arr[i], i)
      let sum = 0;

      // Traverse the array
      for (let i = 0; i < N; i++) {

        // Update sum
        sum += __gcd(i + 1, arr[i]);
      }

      // Update res
      res = Math.max(res, sum);

    } while (next_permutation(arr));

    return res;
  }
  function __gcd(a, b)
  {
    return b == 0? a:__gcd(b, a % b);   
  }
  function next_permutation(p)
  {
    for (let a = p.length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (let b = p.length - 1;; --b)
          if (p[b] > p[a])
          {
            let t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.length - 1; a < b; ++a, --b)
            {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

// Driver Code
    let arr = [ 3, 2, 1 ];
    let N = arr.length;
    document.write(findMaxValByRearrArr(arr, N));

   // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> GCD 的最大可能值(X，Y) = min(X，Y)
> 因此，GCD 的最大可能值(I，arr[i]) = min(i，arr[i])
> 如果数组被排序，那么 i = arr[i]和 GCD 的值(I，arr[I])= I
> σGCD(arr[I]，I)=σI = N *(N+1)/2

按照以下步骤解决问题:

*   初始化一个变量，比如 **res** ，以存储**σGCD(arr[I]，i)** 的最大可能和。
*   更新 **res = (N * (N + 1) / 2)** 。
*   最后，打印 **res** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// GCD(arr[i], i) by rearranging the array
int findMaxValByRearrArr(int arr[], int N)
{

    // Stores maximum sum of GCD(arr[i], i)
    // by rearranging the array elements
    int res = 0;

    // Update res
    res = (N * (N + 1)) / 2;

    return res;
}

// Driver Code
int main()
{

    int arr[] = { 3, 2, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findMaxValByRearrArr(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to find the maximum sum of
// GCD(arr[i], i) by rearranging the array
static int findMaxValByRearrArr(int arr[], int N)
{

    // Stores maximum sum of GCD(arr[i], i)
    // by rearranging the array elements
    int res = 0;

    // Update res
    res = (N * (N + 1)) / 2;
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 1 };
    int N = arr.length;
    System.out.print(findMaxValByRearrArr(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the maximum sum of
# GCD(arr[i], i) by rearranging the array
def findMaxValByRearrArr(arr, N):

    # Stores maximum sum of GCD(arr[i], i)
    # by rearranging the array elements
    res = 0;

    # Update res
    res = (N * (N + 1)) // 2;
    return res;

# Driver Code
if __name__ == '__main__':
    arr = [ 3, 2, 1 ];
    N = len(arr);
    print(findMaxValByRearrArr(arr, N));

# This code contributed by shikhasingrajput
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the maximum sum of
// GCD(arr[i], i) by rearranging the array
static int findMaxValByRearrArr(int []arr, int N)
{

    // Stores maximum sum of GCD(arr[i], i)
    // by rearranging the array elements
    int res = 0;

    // Update res
    res = (N * (N + 1)) / 2;
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 3, 2, 1 };
    int N = arr.Length;

    Console.Write(findMaxValByRearrArr(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to find the maximum sum of
    // GCD(arr[i], i) by rearranging the array
    function findMaxValByRearrArr(arr, N)
    {

        // Stores maximum sum of GCD(arr[i], i)
        // by rearranging the array elements
        let res = 0;

        // Update res
        res = parseInt((N * (N + 1)) / 2, 10);
        return res;
    }

    let arr = [ 3, 2, 1 ];
    let N = arr.length;

    document.write(findMaxValByRearrArr(arr, N));

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)