# 计数与 K 之和大于最大元素的元素

> 原文:[https://www . geesforgeks . org/count-elements-其与 k 的和大于-max-element/](https://www.geeksforgeeks.org/count-elements-whose-sum-with-k-is-greater-than-max-element/)

给定一个**数组 arr[]** 和**整数 K** ，我们的任务是确定数组中每个元素和 K 的和是否大于或等于数组中存在的最大元素，即 **arr[i] + k > =数组的最大元素**。打印所有此类元素的总数。
**举例:**

> **输入:** arr = [2，3，5，1，3]，k = 3
> **输出:** 4
> **解释:**
> 在给定的数组中，元素 2，3，5，3 满足条件，因为所有元素加起来等于 3(=K)，得到的值大于数组的最大元素 5。
> **输入:** arr = [4，2，1，1，2]，k = 1
> **输出:** 1
> **解释:**
> 在给定的数组中，元素 4 满足条件，因为在将 4 与 1 相加时(=K)，我们得到的值大于数组的最大元素，即 4 本身。

**方法:**
要解决上面提到的问题，我们必须首先**存储数组中的最大元素。**然后对于每个元素，检查元素和 K 的和是否给出大于最大元素的值，然后增加计数，否则转到下一个元素。
以下是上述方法的实施:

## C++

```
// C++ implementation to Count of all the elements
// in the array whose summation with integer K returns
// a value that is greater than or equal to the
// maximum value present in the array
#include <bits/stdc++.h>
using namespace std;

// Function to count all the elements
int countNum(int arr[], int K, int n)
{
    int maxi = INT_MIN;

    // Store the maximum array element
    for (int i = 0; i < n; i++) {
        if (arr[i] > maxi)
            maxi = arr[i];
    }

    int cnt = 0;

    // Iterate in array
    for (int i = 0; i < n; i++) {
        // Check if current element and k gives
        // a greater sum than max element
        if (arr[i] + K >= maxi)

            // Increment the count
            cnt++;
        else
            continue;
    }

    // Return the final result
    return cnt;
}

// Driver code
int main()
{
    int arr[] = { 4, 2, 1, 1, 2 };

    int k = 1;

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countNum(arr, k, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count of all the elements
// in the array whose summation with integer K returns
// a value that is greater than or equal to the
// maximum value present in the array
class GFG{

// Function to count all the elements
public static int countNum(int arr[], int K, int n)
{
    int maxi = 0;

    // Store the maximum array element
    for(int i = 0; i < n; i++)
    {
       if (arr[i] > maxi)
           maxi = arr[i];
    }

    int cnt = 0;

    // Iterate in array
    for(int i = 0; i < n; i++)
    {

       // Check if current element and k gives
       // a greater sum than max element
       if (arr[i] + K >= maxi)

           // Increment the count
           cnt++;
       else
           continue;
    }

    // Return the final result
    return cnt;
}

// Driver code   
public static void main(String[] args)
{
    int arr[] = { 4, 2, 1, 1, 2 };
    int k = 1;
    int n = arr.length;

    System.out.println(countNum(arr, k, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to Count of all the elements
# in the array whose summation with integer K returns
# a value that is greater than or equal to the
# maximum value present in the array

import sys

# Function to count all the elements
def countNum(arr, K, n):

    maxi = -sys.maxsize

    # Store the maximum array element
    for i in range(n) :
        if arr[i] > maxi:
            maxi = arr[i]

    cnt = 0

    # Iterate in array
    for i in range(n):

        # Check if current element and k gives
        # a greater sum than max element
        if (arr[i] + K) >= maxi:

            # Increment the count
            cnt += 1
        else :
            continue

    # Return the final result
    return cnt

# Driver code
if __name__=='__main__':

    arr = [ 4, 2, 1, 1, 2 ]
    k = 1
    n = len(arr)

    print(countNum(arr, k, n))

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation to count of all
// the elements in the array whose
// summation with integer K returns
// a value that is greater than or
// equal to the maximum value present
// in the array
using System;

class GFG{

// Function to count all the elements
public static int countNum(int[] arr, int K,
                                      int n)
{
    int maxi = 0;

    // Store the maximum array element
    for(int i = 0; i < n; i++)
    {
       if (arr[i] > maxi)
           maxi = arr[i];
    }

    int cnt = 0;

    // Iterate in array
    for(int i = 0; i < n; i++)
    {

       // Check if current element and k
       // gives a greater sum than max
       // element
       if (arr[i] + K >= maxi)

           // Increment the count
           cnt++;
       else
           continue;
    }

    // Return the final result
    return cnt;
}

// Driver code
public static void Main()
{
    int[] arr = { 4, 2, 1, 1, 2 };
    int k = 1;
    int n = arr.Length;

    Console.Write(countNum(arr, k, n));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation to Count of all the elements
// in the array whose summation with integer K returns
// a value that is greater than or equal to the
// maximum value present in the array

// Function to count all the elements
function countNum(arr, K, n)
{
    var maxi = -1000000000;

    // Store the maximum array element
    for (var i = 0; i < n; i++) {
        if (arr[i] > maxi)
            maxi = arr[i];
    }

    var cnt = 0;

    // Iterate in array
    for (var i = 0; i < n; i++) {
        // Check if current element and k gives
        // a greater sum than max element
        if (arr[i] + K >= maxi)

            // Increment the count
            cnt++;
        else
            continue;
    }

    // Return the final result
    return cnt;
}

// Driver code
var arr = [4, 2, 1, 1, 2];
var k = 1;
var n = arr.length;
document.write( countNum(arr, k, n));

</script>
```

**Output:** 

```
1
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)