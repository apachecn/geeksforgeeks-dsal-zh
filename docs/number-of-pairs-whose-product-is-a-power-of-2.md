# 乘积为 2 的幂的对数

> 原文:[https://www . geesforgeks . org/对数-谁的产品是 2 的幂/](https://www.geeksforgeeks.org/number-of-pairs-whose-product-is-a-power-of-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算给定数组中数组元素对的总数，使得 **arr[i] * arr[j]** 是 2 的[次方](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)。

**示例:**

> **输入:** arr[] = {2，4，7，2}
> **输出:** 3
> **解释:**T8】arr[0]* arr[1]= 8
> arr[0]* arr[3]= 4
> arr[1]* arr[3]= 8
> 
> **输入:** arr[] = {8，1，12，4，2 }
> T3】输出: 6

**方法:**这个想法是基于这样一个事实:如果一个数只包含 **2** 作为其[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)，那么它就是 2 的[次方。所以它的所有除数也是 2 的**次方**。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)

1.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
2.  对于每个数组元素，[检查是否是 2 的幂](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)。增加此类元素的**计数**
3.  最后，打印**(计数*(计数–1))/2**作为所需计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count pairs having
// product equal to a power of 2
int countPairs(int arr[], int N)
{
    // Stores count of array elements
    // which are power of 2
    int countPowerof2 = 0;

    for (int i = 0; i < N; i++) {

        // If array element contains
        // only one set bit
        if (__builtin_popcount(arr[i]) == 1)

            // Increase count of
            // powers of 2
            countPowerof2++;
    }

    // Count required number of pairs
    int desiredPairs
        = (countPowerof2
           * (countPowerof2 - 1))
          / 2;

    // Print the required number of pairs
    cout << desiredPairs << ' ';
}

// Driver Code
int main()
{
    // Given array
    int arr[4] = { 2, 4, 7, 2 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

// Function to count pairs having
// product equal to a power of 2
static void countPairs(int arr[],
                       int N)
{
  // Stores count of array elements
  // which are power of 2
  int countPowerof2 = 0;

  for (int i = 0; i < N; i++)
  {
    // If array element contains
    // only one set bit
    if (Integer.bitCount(arr[i]) == 1)

      // Increase count of
      // powers of 2
      countPowerof2++;
  }

  // Count required number of pairs
  int desiredPairs = (countPowerof2 *
                     (countPowerof2 - 1)) / 2;

  // Print the required number of pairs
  System.out.print(desiredPairs + " ");
}

// Driver Code
public static void main(String[] args)
{
  // Given array
  int arr[] = {2, 4, 7, 2};

  // Size of the array
  int N = arr.length;

  // Function Call
  countPairs(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count pairs having
# product equal to a power of 2
def countPairs(arr, N):

    # Stores count of array elements
    # which are power of 2
    countPowerof2 = 0

    for i in range(N):

        # If array element contains
        # only one set bit
        if (bin(arr[i]).count('1') == 1):

            # Increase count of
            # powers of 2
            countPowerof2 += 1

    # Count required number of pairs
    desiredPairs = (countPowerof2 *
                   (countPowerof2 - 1)) // 2

    # Print the required number of pairs
    print(desiredPairs)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 2, 4, 7, 2 ]

    # Size of the array
    N = len(arr)

    # Function call
    countPairs(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Linq;

class GFG{

// Function to count pairs having
// product equal to a power of 2
static void countPairs(int []arr,
                       int N)
{

    // Stores count of array elements
    // which are power of 2
    int countPowerof2 = 0;

    for(int i = 0; i < N; i++)
    {

        // If array element contains
        // only one set bit
        if ((Convert.ToString(
             arr[i], 2)).Count(
             f => (f == '1')) == 1)

            // Increase count of
            // powers of 2
            countPowerof2++;
    }

    // Count required number of pairs
    int desiredPairs = (countPowerof2 *
                       (countPowerof2 - 1)) / 2;

    // Print the required number of pairs
    Console.WriteLine(desiredPairs + " ");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 2, 4, 7, 2 };

    // Size of the array
    int N = arr.Length;

    // Function call
    countPairs(arr, N);
}
}

// This code is contributed by math_lover
```

## java 描述语言

```
<script>
// Javascript program for the
// above approach

// Function to count pairs having
// product equal to a power of 2
function countPairs(arr,N)
{
    // Stores count of array elements
  // which are power of 2
  let countPowerof2 = 0;

  for (let i = 0; i < N; i++)
  {
    // If array element contains
    // only one set bit
    if (Number(arr[i].toString(2).split("").sort().join("")).toString().length == 1)

      // Increase count of
      // powers of 2
      countPowerof2++;
  }

  // Count required number of pairs
  let desiredPairs = (countPowerof2 *
                     (countPowerof2 - 1)) / 2;

  // Print the required number of pairs
  document.write(desiredPairs + " ");
}

// Driver Code
// Given array
let arr=[2, 4, 7, 2];
// Size of the array
let N = arr.length;

// Function Call
countPairs(arr, N);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)