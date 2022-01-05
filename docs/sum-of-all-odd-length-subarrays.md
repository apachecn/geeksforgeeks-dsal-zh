# 所有奇数长度子阵列的和

> 原文:[https://www . geeksforgeeks . org/全奇数长度子阵之和/](https://www.geeksforgeeks.org/sum-of-all-odd-length-subarrays/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出奇数长度的所有可能子数组的所有元素的和。

**示例:**

> **输入:** arr[] = {3，2，4}
> **输出:** 18
> **解释:**
> 奇数长度子阵及其和如下:
> 1) {3} =和为 3。
> 2) {2} =总和为 2。
> 3) {4} =总和为 4。
> 4) {3，2，4} =和为 3 + 2 + 4 = 9。
> 因此，所有子阵之和= 3 + 2 + 4 + 9 = 18。
> 
> **输入:** arr[] = {1，2，1，2}
> **输出:** 15
> **解释:**
> 奇数长度子阵及其和如下:
> 1) {1} =和为 1。
> 2) {2} =总和为 2。
> 3) {1} =总和为 1。
> 4) {2} =总和为 2。
> 5) {1，2，1} =和为 1 + 2 + 1 = 4。
> 6) {2，1，2} =和为 2 + 1 + 2 = 5。
> 因此，所有子阵列之和= 1 + 2 + 1 + 2 + 4 + 5 = 15。

**天真方法:**最简单的方法是[从给定的数组中生成所有可能的奇数长度的子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并求出所有这些子数组的和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the sum
// of all odd length subarrays
int OddLengthSum(vector<int>& arr)
{
    // Stores the sum
    int sum = 0;

    // Size of array
    int l = arr.size();

    // Traverse the array
    for (int i = 0; i < l; i++) {

        // Generate all subarray of
        // odd length
        for (int j = i; j < l; j += 2) {

            for (int k = i; k <= j; k++) {

                // Add the element to sum
                sum += arr[k];
            }
        }
    }

    // Return the final sum
    return sum;
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { 1, 5, 3, 1, 2 };

    // Function Call
    cout << OddLengthSum(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG{

// Function to calculate the sum
// of all odd length subarrays
static int OddLengthSum(int[] arr)
{

    // Stores the sum
    int sum = 0;

    // Size of array
    int l = arr.length;

    // Traverse the array
    for(int i = 0; i < l; i++)
    {

        // Generate all subarray of
        // odd length
        for(int j = i; j < l; j += 2)
        {
            for(int k = i; k <= j; k++)
            {

                // Add the element to sum
                sum += arr[k];
            }
        }
    }

    // Return the final sum
    return sum;
}

// Driver Code
public static void main (String[] args)
{

    // Given array arr[]
    int[] arr = { 1, 5, 3, 1, 2 };

    // Function call
    System.out.print(OddLengthSum(arr));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the sum
# of all odd length subarrays
def OddLengthSum(arr):

    # Stores the sum
    sum = 0

    # Size of array
    l = len(arr)

    # Traverse the array
    for i in range(l):

        # Generate all subarray of
        # odd length
        for j in range(i, l, 2):
            for k in range(i, j + 1, 1):

                # Add the element to sum
                sum += arr[k]

    # Return the final sum
    return sum

# Driver Code

# Given array arr[]
arr = [ 1, 5, 3, 1, 2 ]

# Function call
print(OddLengthSum(arr))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate the sum
// of all odd length subarrays
static int OddLengthSum(int[] arr)
{

    // Stores the sum
    int sum = 0;

    // Size of array
    int l = arr.Length;

    // Traverse the array
    for(int i = 0; i < l; i++)
    {

        // Generate all subarray of
        // odd length
        for(int j = i; j < l; j += 2)
        {
            for(int k = i; k <= j; k++)
            {

                // Add the element to sum
                sum += arr[k];
            }
        }
    }

    // Return the final sum
    return sum;
}

// Driver Code
public static void Main ()
{

    // Given array arr[]
    int[] arr = { 1, 5, 3, 1, 2 };

    // Function call
    Console.Write(OddLengthSum(arr));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to calculate the sum
// of all odd length subarrays
function OddLengthSum(arr)
{

    // Stores the sum
    var sum = 0;

    // Size of array
    var l = arr.length;

    // Traverse the array
    for(var i = 0; i < l; i++)
    {

        // Generate all subarray of
        // odd length
        for(var j = i; j < l; j += 2)
        {
            for(var k = i; k <= j; k++)
            {

                // Add the element to sum
                sum += arr[k];
            }
        }
    }

    // Return the final sum
    return sum;
}

// Driver Code

    // Given array arr[]
    var arr = [ 1, 5, 3, 1, 2 ]

    // Function call
    document.write(OddLengthSum(arr));

// This code is contributed by bunnyram19.
</script>
```

**Output**

```
48
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，其思想是在生成所有奇数长度的子阵列后观察以下模式:

*   对于索引 **idx** 处的任何元素，其左侧有 **(idx + 1)** 选项，右侧有**(N–idx)**选项。
*   因此，对于任何元素 **arr[i]** ，arr[i]在所有子阵列中的计数为**(I+1)*(N–I)**。
*   因此，对于一个元素**arr【I】**，存在奇数长度的**((I+1)*(N–I)+1)/2**子阵列。
*   最后，**arr【I】**总共有**((I+1)*(n–I)+1)/2**个频率之和。

因此，为了找到奇数长度的所有子阵列的所有元素的和，想法是[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个 i <sup>第</sup>个数组元素，将[**((I+1)*(n–I)+1)/2]* arr[I]**添加到和中。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the sum of all
// the element of subarrays of odd length
int OddLengthSum(vector<int>& arr)
{
    // Stores the sum
    int sum = 0;

    // Size of array
    int l = arr.size();

    // Traverse the given array arr[]
    for (int i = 0; i < l; i++) {

        // Add to the sum for each
        // contribution of the arr[i]
        sum += (((i + 1)
                     * (l - i)
                 + 1)
                / 2)
               * arr[i];
    }

    // Return the final sum
    return sum;
}

// Driver Code
int main()
{
    // Given array arr[]
    vector<int> arr = { 1, 5, 3, 1, 2 };

    // Function Call
    cout << OddLengthSum(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function that finds the sum of all
// the element of subarrays of odd length
static int OddLengthSum(int []arr)
{

    // Stores the sum
    int sum = 0;

    // Size of array
    int l = arr.length;

    // Traverse the given array arr[]
    for(int i = 0; i < l; i++)
    {

        // Add to the sum for each
        // contribution of the arr[i]
        sum += (((i + 1) * (l - i) +
                 1) / 2) * arr[i];
    }

    // Return the final sum
    return sum;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int []arr = { 1, 5, 3, 1, 2 };

    // Function call
    System.out.print(OddLengthSum(arr));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the sum of all
# the element of subarrays of odd length
def OddLengthSum(arr):

    # Stores the sum
    Sum = 0

    # Size of array
    l = len(arr)

    # Traverse the given array arr[]
    for i in range(l):

        # Add to the sum for each
        # contribution of the arr[i]
        Sum += ((((i + 1) *
                  (l - i) +
                 1) // 2) * arr[i])

    # Return the final sum
    return Sum

# Driver code

# Given array arr[]
arr = [ 1, 5, 3, 1, 2 ]

# Function call
print(OddLengthSum(arr))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for
// the above approach
using System;
class GFG{

// Function that finds the
// sum of all the element of
// subarrays of odd length
static int OddLengthSum(int []arr)
{
  // Stores the sum
  int sum = 0;

  // Size of array
  int l = arr.Length;

  // Traverse the given array []arr
  for(int i = 0; i < l; i++)
  {
    // Add to the sum for each
    // contribution of the arr[i]
    sum += (((i + 1) *
             (l - i) + 1) / 2) * arr[i];
  }

  // Return the readonly sum
  return sum;
}

// Driver Code
public static void Main(String[] args)
{
  // Given array []arr
  int []arr = {1, 5, 3, 1, 2};

  // Function call
  Console.Write(OddLengthSum(arr));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function that finds the sum of all
// the element of subarrays of odd length
function OddLengthSum(arr)
{

    // Stores the sum
    let sum = 0;

    // Size of array
    let l = arr.length;

    // Traverse the given array arr[]
    for(let i = 0; i < l; i++)
    {

        // Add to the sum for each
        // contribution of the arr[i]
        sum += Math.floor(((i + 1) * (l - i) +
                 1) / 2) * arr[i];
    }

    // Return the final sum
    return sum;
}

// Driver Code

    // Given array arr[]
    let arr = [ 1, 5, 3, 1, 2 ];

    // Function call
    document.write(OddLengthSum(arr));

// This code is contributed by target_2.
</script>
```

**Output**

```
48
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)