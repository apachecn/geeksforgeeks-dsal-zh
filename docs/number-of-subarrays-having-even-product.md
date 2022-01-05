# 具有偶数积的子阵列数量

> 原文:[https://www . geeksforgeeks . org/拥有偶数产品的子阵列数量/](https://www.geeksforgeeks.org/number-of-subarrays-having-even-product/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/arrays-binarysearch-java-examples-set-1/) arr【】，任务是计算出具有偶数积的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的总数。

**示例:**

> **输入:** arr[] = { 7，5，4，9 }
> **输出:** 6
> **说明:**共有 6 个子阵
> 
> 1.  { 4 }
> 2.  { 5, 4 }
> 3.  { 7, 5, 4 }
> 4.  { 7, 5, 4, 9 }
> 5.  { 5, 4, 9 }
> 6.  { 4, 9 }
> 
> **输入:** arr[] = { 1，3，5 }
> T3】输出: 0

**天真的方法:**解决这个问题最简单的方法是[从给定的阵列中生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵列，检查其乘积是否为偶数。如果发现任何子阵列为真，则增加计数。最后，打印获得的计数。

以下是上述方法的实现:

## C++

```
// CPP implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to count subarrays with even product
void evenproduct(int arr[], int length)
{

  // Stores count of subarrays
  // with even product
  int count = 0;

  // Traverse the array
  for (int i = 0; i < length+1; i++) {

    // Initialize product
    int product = 1;

    for (int j = i; j < length+1; j++) {

      // Update product of the subarray
      product *= arr[j];

      if (product % 2 == 0)
        ++count;
    }
  }

  // Print total count of subarrays
  cout<<count;
}

// Driver Code
int main()
{

  // Input
  int arr[] = { 7, 5, 4, 9 };

  // Length of an array
  int length = (sizeof(arr)/sizeof(arr[0]))- 1;

  // Function call to count
  // subarrays with even product
  evenproduct(arr, length);
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG {

    // Function to count subarrays with even product
    static void evenproduct(int arr[], int length)
    {
        // Stores count of subarrays
        // with even product
        int count = 0;

        // Traverse the array
        for (int i = 0; i < arr.length; i++) {

            // Initialize product
            int product = 1;

            for (int j = i; j < arr.length; j++) {

                // Update product of the subarray
                product *= arr[j];

                if (product % 2 == 0)
                    ++count;
            }
        }

        // Print total count of subarrays
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int arr[] = { 7, 5, 4, 9 };

        // Length of an array
        int length = arr.length - 1;

        // Function call to count
        // subarrays with even product
        evenproduct(arr, length);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to count subarrays with even product
def evenproduct(arr, length) :

  # Stores count of subarrays
  # with even product
  count = 0;

  # Traverse the array
  for i in range(length + 1) :

    # Initialize product
    product = 1;
    for j in range(i, length + 1) :

      # Update product of the subarray
      product *= arr[j];

      if (product % 2 == 0) :
          count += 1;

  # Print total count of subarrays
  print(count);

# Driver Code
if __name__ == "__main__" :

    # Input
    arr = [ 7, 5, 4, 9 ];

    # Length of an array
    length = len(arr) - 1;

    # Function call to count
    # subarrays with even product
    evenproduct(arr, length);

    # This code is contributed by AnkThon
```

## C#

```
// C# implementation of the above approach
using System;
public class GFG
{

  // Function to count subarrays with even product
  static void evenproduct(int []arr, int length)
  {

    // Stores count of subarrays
    // with even product
    int count = 0;

    // Traverse the array
    for (int i = 0; i < arr.Length; i++) {

      // Initialize product
      int product = 1;

      for (int j = i; j < arr.Length; j++) {

        // Update product of the subarray
        product *= arr[j];

        if (product % 2 == 0)
          ++count;
      }
    }

    // Print total count of subarrays
    Console.WriteLine(count);
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Input
    int []arr = { 7, 5, 4, 9 };

    // Length of an array
    int length = arr.Length - 1;

    // Function call to count
    // subarrays with even product
    evenproduct(arr, length);
  }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to count subarrays with even product
function evenproduct(arr, length)
{

  // Stores count of subarrays
  // with even product
  var count = 0;
  var i,j;
  // Traverse the array
  for (i = 0; i < length+1; i++) {

    // Initialize product
    var product = 1;

    for (j = i; j < length+1; j++) {

      // Update product of the subarray
      product *= arr[j];

      if (product % 2 == 0)
        ++count;
    }
  }

  // Print total count of subarrays
  document.write(count);
}

// Driver Code

  // Input
  var arr = [7, 5, 4, 9];

  // Length of an array
  var length = arr.length;

  // Function call to count
  // subarrays with even product
  evenproduct(arr, length);

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤优化上述方法:

1.  大小为 **N** 的阵列中的子阵列总数为 **N * (N + 1) / 2** 。
2.  具有奇数乘积的子阵列的计数等于阵列中存在的连续奇数元素的总数。
3.  因此，偶数积的子阵列数= **(子阵列总数-奇数积的子阵列数)**。
4.  打印获得的子阵列计数值。

下面是上述方法的实现:

## C++

```
#include <iostream>
using namespace std;

// Function to count subarrays
// with even product
void evenproduct(int arr[],
                 int length)
{

  // Total number of subarrays
  int total_subarray
    = length * (length + 1) / 2;

  // Counter variables
  int total_odd = 0;
  int count_odd = 0;

  // Traverse the array
  for (int i = 0; i < length; ++i) {

    // If current element is odd
    if (arr[i] % 2 == 0) {
      count_odd = 0;
    }
    else {

      ++count_odd;

      // Update count of subarrays
      // with odd product up to index i
      total_odd += count_odd;
    }
  }

  // Print count of subarrays
  // with even product
  cout << (total_subarray
           - total_odd) << endl;
}

// Driver code
int main()
{

  // Input
  int arr[] = { 7, 5, 4, 9 };

  // Length of an array
  int length = sizeof(arr) / sizeof(arr[0]);

  // Function call to count
  // even product subarrays
  evenproduct(arr, length);

  return 0;
}

// This code is contributed by splevel62.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG {

    // Function to count subarrays
    // with even product
    static void evenproduct(int arr[],
                            int length)
    {
        // Total number of subarrays
        int total_subarray
            = length * (length + 1) / 2;

        // Counter variables
        int total_odd = 0;
        int count_odd = 0;

        // Traverse the array
        for (int i = 0; i < arr.length; ++i) {

            // If current element is odd
            if (arr[i] % 2 == 0) {
                count_odd = 0;
            }
            else {

                ++count_odd;

                // Update count of subarrays
                // with odd product up to index i
                total_odd += count_odd;
            }
        }

        // Print count of subarrays
        // with even product
        System.out.println(total_subarray
                           - total_odd);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Input
        int arr[] = { 7, 5, 4, 9 };

        // Length of an array
        int length = arr.length;

        // Function call to count
        // even product subarrays
        evenproduct(arr, length);
    }
}
```

## 蟒蛇 3

```
# Function to count subarrays
# with even product
def evenproduct(arr, length):

    # Total number of subarrays
    total_subarray = length * (length + 1) // 2

    # Counter variables
    total_odd = 0
    count_odd = 0

    # Traverse the array
    for i in range(length):

        # If current element is odd
        if (arr[i] % 2 == 0):
            count_odd = 0

        else:
            count_odd += 1

            # Update count of subarrays
            # with odd product up to index i
            total_odd += count_odd

    # Print count of subarrays
    # with even product
    print(total_subarray
          - total_odd)

# Driver code
if __name__ == "__main__":

    # Input
    arr = [7, 5, 4, 9]

    # Length of an array
    length = len(arr)

    # Function call to count
    # even product subarrays
    evenproduct(arr, length)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to count subarrays
  // with even product
  static void evenproduct(int[] arr,
                          int length)
  {

    // Total number of subarrays
    int total_subarray
      = length * (length + 1) / 2;

    // Counter variables
    int total_odd = 0;
    int count_odd = 0;

    // Traverse the array
    for (int i = 0; i < arr.Length; ++i) {

      // If current element is odd
      if (arr[i] % 2 == 0) {
        count_odd = 0;
      }
      else {

        ++count_odd;

        // Update count of subarrays
        // with odd product up to index i
        total_odd += count_odd;
      }
    }

    // Print count of subarrays
    // with even product
    Console.WriteLine(total_subarray
                      - total_odd);
  }

  // Driver Code
  public static void Main(string[] args)
  {

    // Input
    int[] arr = { 7, 5, 4, 9 };

    // Length of an array
    int length = arr.Length;

    // Function call to count
    // even product subarrays
    evenproduct(arr, length);
  }
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// javascript implementation of the above approach

   // Function to count subarrays
    // with even product
    function evenproduct(arr, length)
    {
        // Total number of subarrays
        var total_subarray
            = length * (length + 1) / 2;

        // Counter variables
        var total_odd = 0;
        var count_odd = 0;

        // Traverse the array
        for (i = 0; i < arr.length; ++i) {

            // If current element is odd
            if (arr[i] % 2 == 0) {
                count_odd = 0;
            }
            else {

                ++count_odd;

                // Update count of subarrays
                // with odd product up to index i
                total_odd += count_odd;
            }
        }

        // Print count of subarrays
        // with even product
        document.write(total_subarray
                           - total_odd);
    }

    // Driver Code
 // Input
    var arr = [ 7, 5, 4, 9 ];

    // Length of an array
    var length = arr.length;

    // Function call to count
    // even product subarrays
    evenproduct(arr, length);
// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间** : O(1)