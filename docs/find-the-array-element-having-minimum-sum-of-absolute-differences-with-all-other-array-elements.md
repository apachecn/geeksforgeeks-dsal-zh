# 找出与所有其他数组元素绝对差之和最小的数组元素

> 原文:[https://www . geeksforgeeks . org/find-the-array-element-with-all-other-array-elements-differences/](https://www.geeksforgeeks.org/find-the-array-element-having-minimum-sum-of-absolute-differences-with-all-other-array-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是找出一个数组元素与另一个数组的所有元素的绝对差的最小和。

> **输入:** arr[ ] = {1，2，3，4，5}，N = 5
> **输出:** 3
> **解释:**
> 对于 arr[0](= 1):Sum = ABS(2–1)+ABS(3–1)+ABS(4–1)+ABS(5–1)= 10。
> 对于 arr[1](= 2):Sum = ABS(2–1)+ABS(3–2)+ABS(4–2)+ABS(5–2)= 7。
> 对于 arr[2](= 3):总和= ABS(3–1)+ABS(3–2)+ABS(4–3)+ABS(5–3)= 6**(最小值)**。
> 对于 arr[3](= 4):Sum = ABS(4–1)+ABS(4–2)+ABS(4–3)+ABS(5–4)= 7。
> 对于 arr[0](= 1): Sum = 10。
> 
> **输入:** arr[ ] = {1，2，3，4}，N = 4
> T3】输出: 2

**方法:**基于观察到对于数组的中值，所有数组元素的绝对差之和最小，可以解决这个问题。按照以下步骤解决问题:

*   [排序数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 。
*   打印排序数组的中间元素作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the array element
// having minimum sum of absolute
// differences with other array elements
void minAbsDiff(int arr[], int n)
{

    // Sort the array
    sort(arr, arr + n);

    // Print the middle element
    cout << arr[n / 2] << endl;
}

// Driver Code
int main()
{

    int n = 5;
    int arr[] = { 1, 2, 3, 4, 5 };

    minAbsDiff(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;
public class GFG
{

  // Function to return the array element
  // having minimum sum of absolute
  // differences with other array elements
  static void minAbsDiff(int arr[], int n)
  {

    // Sort the array
    Arrays.sort(arr);

    // Print the middle element
    System.out.println(arr[n / 2]);
  }

  // Driver code
  public static void main(String[] args)
  {
    int n = 5;
    int arr[] = { 1, 2, 3, 4, 5 };
    minAbsDiff(arr, n);
  }
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the array element
# having minimum sum of absolute
# differences with other array elements
def minAbsDiff(arr, n):

    # Sort the array
    arr.sort()

    # Print the middle element
    print(arr[n // 2])

# Driver Code
if __name__ == '__main__':

    n = 5
    arr = [ 1, 2, 3, 4, 5 ]

    minAbsDiff(arr, n)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the array element
// having minimum sum of absolute
// differences with other array elements
static void minAbsDiff(int []arr, int n)
{

    // Sort the array
    Array.Sort(arr);

    // Print the middle element
    Console.WriteLine(arr[n / 2]);
}

// Driver code
public static void Main(string[] args)
{
    int n = 5;
    int []arr = { 1, 2, 3, 4, 5 };

    minAbsDiff(arr, n);
}
}

// This code is contributed by ankThon
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to return the array element
// having minimum sum of absolute
// differences with other array elements
function minAbsDiff(arr, n){

    // Sort the array
    arr.sort(function(a, b){return a-b})

    // Print the middle element
    document.write(arr[Math.floor(n / 2)])
    }

// main code
let n = 5
let arr = [ 1, 2, 3, 4, 5 ]

minAbsDiff(arr, n)

// This code is contributed by AnkThon

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*