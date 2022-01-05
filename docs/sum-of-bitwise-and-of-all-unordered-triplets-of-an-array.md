# 数组中所有无序三元组的按位“与”的和

> 原文:[https://www . geeksforgeeks . org/全无序数组三元组按位求和/](https://www.geeksforgeeks.org/sum-of-bitwise-and-of-all-unordered-triplets-of-an-array/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是求所有可能三元组 **(arr[i]、arr[j]、arr[k])的**的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)之和，使得 **i < j < k** 。

**示例:**

> **输入:** arr[] = {3，5，4，7}
> **输出:** 5
> **解释:**所有可能三元组的位与之和=(3&5&4)+(3&5&7)+(3&4&7)+(5&4&7)= 0+1+0+4 = 5。
> 
> **输入:** arr[] = {4，4，4 }
> T3】输出: 4

**天真方法:**解决给定问题的最简单方法是[生成给定数组](https://www.geeksforgeeks.org/print-all-triplets-with-given-sum/)的所有可能三元组 **(i，j，k)** ，使得 **i < j < k** 并打印所有可能三元组的[位与](https://www.geeksforgeeks.org/calculate-sum-of-bitwise-and-of-all-pairs/)之和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of Bitwise
// AND of all unordered triplets from
// a given array such that (i < j < k)
void tripletAndSum(int arr[], int n)
{
    // Stores the resultant sum of
    // Bitwise AND of all triplets
    int ans = 0;

    // Generate all triplets of
    // (arr[i], arr[j], arr[k])
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = j + 1; k < n; k++) {

                // Add Bitwise AND to ans
                ans += arr[i] & arr[j] & arr[k];
            }
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 4, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    tripletAndSum(arr, N);
//This code is contributed by Potta Lokesh
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to calculate sum of Bitwise
    // AND of all unordered triplets from
    // a given array such that (i < j < k)
    public static void tripletAndSum(int arr[], int n)
    {

        // Stores the resultant sum of
        // Bitwise AND of all triplets
        int ans = 0;

        // Generate all triplets of
        // (arr[i], arr[j], arr[k])
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {

                    // Add Bitwise AND to ans
                    ans += arr[i] & arr[j] & arr[k];
                }
            }
        }

        // Print the result
        System.out.println(ans);
    }

    public static void main(String[] args)
    {
        int arr[] = { 3, 5, 4, 7 };
        int N = arr.length;
        tripletAndSum(arr, N);
    }
}

 //This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum of Bitwise
# AND of all unordered triplets from
# a given array such that (i < j < k)
def tripletAndSum(arr, n):

    # Stores the resultant sum of
    # Bitwise AND of all triplets
    ans = 0

    # Generate all triplets of
    # (arr[i], arr[j], arr[k])
    for i in range(n):
        for j in range(i + 1, n, 1):
            for k in range(j + 1, n, 1):

                # Add Bitwise AND to ans
                ans += arr[i] & arr[j] & arr[k]

    # Print the result
    print(ans)

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 5, 4, 7 ]
    N = len(arr)

    tripletAndSum(arr, N)

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to calculate sum of Bitwise
    // AND of all unordered triplets from
    // a given array such that (i < j < k)
    public static void tripletAndSum(int[] arr, int n)
    {

        // Stores the resultant sum of
        // Bitwise AND of all triplets
        int ans = 0;

        // Generate all triplets of
        // (arr[i], arr[j], arr[k])
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {

                    // Add Bitwise AND to ans
                    ans += arr[i] & arr[j] & arr[k];
                }
            }
        }

        // Print the result
        Console.WriteLine(ans);
    }

// Driver code
static public void Main()
{
    int[] arr = { 3, 5, 4, 7 };
        int N = arr.Length;
        tripletAndSum(arr, N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to calculate sum of Bitwise
        // AND of all unordered triplets from
        // a given array such that (i < j < k)
        function tripletAndSum(arr, n) {
            // Stores the resultant sum of
            // Bitwise AND of all triplets
            let ans = 0;

            // Generate all triplets of
            // (arr[i], arr[j], arr[k])
            for (let i = 0; i < n; i++) {
                for (let j = i + 1; j < n; j++) {
                    for (let k = j + 1; k < n; k++) {

                        // Add Bitwise AND to ans
                        ans += arr[i] & arr[j] & arr[k];
                    }
                }
            }

            // Print the result
            document.write(ans);
        }

        // Driver Code

        let arr = [3, 5, 4, 7];
        let N = arr.length
        tripletAndSum(arr, N);

        // This code is contributed by Potta Lokesh
  </script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法也可以通过考虑数字的[二进制表示](https://www.geeksforgeeks.org/binary-representations-in-digital-logic/)来优化。按照以下步骤解决问题:

*   初始化一个变量，比如说**和**为 **0** ，它存储所有可能三元组的[位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的合成和。
*   [在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，31】**内循环，并执行以下步骤:
    *   初始化一个变量，将 **cnt** 设为 **0** ，该变量存储数组元素的[计数，数组元素的 **i <sup>第</sup>位**被设置。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
    *   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[如果 **i <sup>第</sup>位**被设置](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/)，那么 **cnt** 的值增加 **1** 。
    *   在上述步骤之后，对于具有[的所有可能的三元组, **i <sup>第</sup>位**被设置为](https://www.geeksforgeeks.org/check-whether-k-th-bit-set-not/),则它将值**(<sup>CNT</sup>C<sub>3</sub>)* 2<sup>I</sup>)**贡献给合成总和。因此，将该值添加到变量 **cnt** 中。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum of Bitwise
// AND of all unordered triplets from
// a given array such that (i < j < k)
int tripletAndSum(int arr[], int n)
{
    // Stores the resultant sum of
    // Bitwise AND of all triplets
    int ans = 0;

    // Traverse over all the bits
    for (int bit = 0; bit < 32; bit++) {
        int cnt = 0;

        // Count number of elements
        // with the current bit set
        for (int i = 0; i < n; i++) {
            if (arr[i] & (1 << bit))
                cnt++;
        }

        // There are (cnt)C(3) numbers
        // with the current bit set and
        // each triplet contributes
        // 2^bit to the result
        ans += (1 << bit) * cnt
               * (cnt - 1) * (cnt - 2) / 6;
    }

    // Return the resultant sum
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 5, 4, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << tripletAndSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to calculate sum of Bitwise
// AND of all unordered triplets from
// a given array such that (i < j < k)
static int tripletAndSum(int[] arr, int n)
{

    // Stores the resultant sum of
    // Bitwise AND of all triplets
    int ans = 0;

    // Traverse over all the bits
    for(int bit = 0; bit < 32; bit++)
    {
        int cnt = 0;

        // Count number of elements
        // with the current bit set
        for(int i = 0; i < n; i++)
        {
            if ((arr[i] & (1 << bit)) != 0)
                cnt++;
        }

        // There are (cnt)C(3) numbers
        // with the current bit set and
        // each triplet contributes
        // 2^bit to the result
        ans += (1 << bit) * cnt *
               (cnt - 1) * (cnt - 2) / 6;
    }

    // Return the resultant sum
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 5, 4, 7 };
    int N = arr.length;

    System.out.print(tripletAndSum(arr, N));
}
}

// This code is contributed by subham348
```

## 蟒蛇 3

```
# Python program for the above approach
# Function to calculate sum of Bitwise
# AND of all unordered triplets from
# a given array such that (i < j < k)
def tripletAndSum(arr, n):

    # Stores the resultant sum of
    # Bitwise AND of all triplets
    ans = 0

    # Traverse over all the bits
    for bit in range(32):
        cnt = 0

        # Count number of elements
        # with the current bit set
        for i in range(n):
            if(arr[i] & (1 << bit)):
                cnt+=1

        # There are (cnt)C(3) numbers
        # with the current bit set and
        # each triplet contributes
        # 2^bit to the result
        ans += (1 << bit) * cnt * (cnt - 1) * (cnt - 2) // 6

    # Return the resultant sum
    return ans

# Driver Code
arr =  [3, 5, 4, 7]
N = len(arr)
print(tripletAndSum(arr, N))

# this code is contributed by shivanisinghss2110
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate sum of Bitwise
// AND of all unordered triplets from
// a given array such that (i < j < k)
static int tripletAndSum(int[] arr, int n)
{

    // Stores the resultant sum of
    // Bitwise AND of all triplets
    int ans = 0;

    // Traverse over all the bits
    for(int bit = 0; bit < 32; bit++)
    {
        int cnt = 0;

        // Count number of elements
        // with the current bit set
        for(int i = 0; i < n; i++)
        {
            if ((arr[i] & (1 << bit)) != 0)
                cnt++;
        }

        // There are (cnt)C(3) numbers
        // with the current bit set and
        // each triplet contributes
        // 2^bit to the result
        ans += (1 << bit) * cnt * (cnt - 1) *
                                  (cnt - 2) / 6;
    }

    // Return the resultant sum
    return ans;
}

// Driver Code
public static void Main()
{
    int[] arr = { 3, 5, 4, 7 };
    int N = arr.Length;

    Console.Write(tripletAndSum(arr, N));
}
}

// This code is contributed by rishavmahato348
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate sum of Bitwise
// AND of all unordered triplets from
// a given array such that (i < j < k)
function tripletAndSum(arr, n) {
    // Stores the resultant sum of
    // Bitwise AND of all triplets
    let ans = 0;

    // Traverse over all the bits
    for (let bit = 0; bit < 32; bit++) {
        let cnt = 0;

        // Count number of elements
        // with the current bit set
        for (let i = 0; i < n; i++) {
            if (arr[i] & (1 << bit))
                cnt++;
        }

        // There are (cnt)C(3) numbers
        // with the current bit set and
        // each triplet contributes
        // 2^bit to the result
        ans += (1 << bit) * cnt
            * (cnt - 1) * (cnt - 2) / 6;
    }

    // Return the resultant sum
    return ans;
}

// Driver Code

let arr = [3, 5, 4, 7];
let N = arr.length;
document.write(tripletAndSum(arr, N));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)