# 执行给定操作后更新数组的和

> 原文:[https://www . geeksforgeeks . org/执行给定操作后更新的阵列总和/](https://www.geeksforgeeks.org/sum-of-the-updated-array-after-performing-the-given-operation/)

给定一个由 **N** 元素组成的数组 **arr[]** ，任务是更新所有数组元素，这样一个元素 **arr[i]** 被更新为**arr[I]= arr[I]–X**，其中**X = arr[I+1]+arr[I+2]+…+arr[N–1]**并最终打印更新后数组的总和。
**举例:**

> **输入:** arr[] = {40，25，12，10}
> **输出:** 8
> 更新后的数组将为{-7，3，2，10}。
> -7 + 3 + 2 + 10 = 8
> **输入:** arr[] = {50，30，10，2，0}
> **输出:** 36

**方法:**一个简单的解决方案是对于 I 的每个可能值，更新 arr[I]= arr[I]–sum(arr[I+1…N-1])。

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Utility function to return
// the sum of the array
int sumArr(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    return sum;
}

// Function to return the sum
// of the modified array
int sumModArr(int arr[], int n)
{

    for (int i = 0; i < n - 1; i++) {

        // Find the sum of the subarray
        // arr[i+1...n-1]
        int subSum = 0;
        for (int j = i + 1; j < n; j++) {
            subSum += arr[j];
        }

        // Subtract the subarray sum
        arr[i] -= subSum;
    }

    // Return the sum of
    // the modified array
    return sumArr(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 40, 25, 12, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << sumModArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Utility function to return
// the sum of the array
static int sumArr(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    return sum;
}

// Function to return the sum
// of the modified array
static int sumModArr(int arr[], int n)
{
    for (int i = 0; i < n - 1; i++)
    {

        // Find the sum of the subarray
        // arr[i+1...n-1]
        int subSum = 0;
        for (int j = i + 1; j < n; j++)
        {
            subSum += arr[j];
        }

        // Subtract the subarray sum
        arr[i] -= subSum;
    }

    // Return the sum of
    // the modified array
    return sumArr(arr, n);
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 40, 25, 12, 10 };
    int n = arr.length;

    System.out.println(sumModArr(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to return
# the sum of the array
def sumArr(arr, n):
    sum = 0
    for i in range(n):
        sum += arr[i]
    return sum

# Function to return the sum
# of the modified array
def sumModArr(arr, n):

    for i in range(n - 1):

        # Find the sum of the subarray
        # arr[i+1...n-1]
        subSum = 0
        for j in range(i + 1, n):
            subSum += arr[j]

        # Subtract the subarray sum
        arr[i] -= subSum

    # Return the sum of
    # the modified array
    return sumArr(arr, n)

# Driver code
arr = [40, 25, 12, 10]
n = len(arr)

print(sumModArr(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Utility function to return
    // the sum of the array
    static int sumArr(int []arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        return sum;
    }

    // Function to return the sum
    // of the modified array
    static int sumModArr(int []arr, int n)
    {
        for (int i = 0; i < n - 1; i++)
        {

            // Find the sum of the subarray
            // arr[i+1...n-1]
            int subSum = 0;
            for (int j = i + 1; j < n; j++)
            {
                subSum += arr[j];
            }

            // Subtract the subarray sum
            arr[i] -= subSum;
        }

        // Return the sum of
        // the modified array
        return sumArr(arr, n);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 40, 25, 12, 10 };
        int n = arr.Length;

        Console.WriteLine(sumModArr(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Utility function to return
    // the sum of the array
    function sumArr(arr , n) {
        var sum = 0;
        for (i = 0; i < n; i++)
            sum += arr[i];
        return sum;
    }

    // Function to return the sum
    // of the modified array
    function sumModArr(arr , n) {
        for (i = 0; i < n - 1; i++) {

            // Find the sum of the subarray
            // arr[i+1...n-1]
            var subSum = 0;
            for (j = i + 1; j < n; j++) {
                subSum += arr[j];
            }

            // Subtract the subarray sum
            arr[i] -= subSum;
        }

        // Return the sum of
        // the modified array
        return sumArr(arr, n);
    }

    // Driver code

        var arr = [ 40, 25, 12, 10 ];
        var n = arr.length;

        document.write(sumModArr(arr, n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(N <sup>2</sup> )
**有效方法:**一种有效的解决方案是从末端遍历阵列，使得到目前为止子阵列的和(即**和(arr[i+1…n-1])** 可以用来计算当前子阵列的和 **arr[i…n-1]** 即**和(arr[I…N-1])= arr[arr
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Utility function to return
// the sum of the array
int sumArr(int arr[], int n)
{
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];
    return sum;
}

// Function to return the sum
// of the modified array
int sumModArr(int arr[], int n)
{

    int subSum = arr[n - 1];
    for (int i = n - 2; i >= 0; i--) {

        int curr = arr[i];

        // Subtract the subarray sum
        arr[i] -= subSum;

        // Sum of subarray arr[i...n-1]
        subSum += curr;
    }

    // Return the sum of
    // the modified array
    return sumArr(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 40, 25, 12, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << sumModArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Utility function to return
    // the sum of the array
    static int sumArr(int arr[], int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        return sum;
    }

    // Function to return the sum
    // of the modified array
    static int sumModArr(int arr[], int n)
    {
        int subSum = arr[n - 1];
        for (int i = n - 2; i >= 0; i--)
        {
            int curr = arr[i];

            // Subtract the subarray sum
            arr[i] -= subSum;

            // Sum of subarray arr[i...n-1]
            subSum += curr;
        }

        // Return the sum of
        // the modified array
        return sumArr(arr, n);
    }

    // Driver code
    public static void main (String[] args)
    {
        int []arr = { 40, 25, 12, 10 };
        int n = arr.length;

        System.out.println(sumModArr(arr, n));
    }
}

// This code is contributed by kanugargng
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to return
# the sum of the array
def sumArr(arr, n):

    sum = 0;
    for i in range(n):
        sum += arr[i];
    return sum;

# Function to return the sum
# of the modified array
def sumModArr(arr, n):

    subSum = arr[n - 1];
    for i in range(n - 2, -1, -1):

        curr = arr[i];

        # Subtract the subarray sum
        arr[i] -= subSum;

        # Sum of subarray arr[i...n-1]
        subSum += curr;

    # Return the sum of
    # the modified array
    return sumArr(arr, n);

# Driver code
arr = [40, 25, 12, 10 ];
n = len(arr);

print(sumModArr(arr, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Utility function to return
    // the sum of the array
    static int sumArr(int []arr, int n)
    {
        int sum = 0;
        for (int i = 0; i < n; i++)
            sum += arr[i];
        return sum;
    }

    // Function to return the sum
    // of the modified array
    static int sumModArr(int []arr, int n)
    {
        int subSum = arr[n - 1];
        for (int i = n - 2; i >= 0; i--)
        {
            int curr = arr[i];

            // Subtract the subarray sum
            arr[i] -= subSum;

            // Sum of subarray arr[i...n-1]
            subSum += curr;
        }

        // Return the sum of
        // the modified array
        return sumArr(arr, n);
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 40, 25, 12, 10 };
        int n = arr.Length;

        Console.WriteLine(sumModArr(arr, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Utility function to return
      // the sum of the array
      function sumArr(arr, n) {
        var sum = 0;
        for (var i = 0; i < n; i++) sum += arr[i];
        return sum;
      }

      // Function to return the sum
      // of the modified array

      function sumModArr(arr, n) {
        var subSum = arr[n - 1];
        for (var i = n - 2; i >= 0; i--) {
          var curr = arr[i];

          // Subtract the subarray sum
          arr[i] -= subSum;

          // Sum of subarray arr[i...n-1]
          subSum += curr;
        }

        // Return the sum of
        // the modified array
        return sumArr(arr, n);
      }

      // Driver code
      var arr = [40, 25, 12, 10];
      var n = arr.length;

      document.write(sumModArr(arr, n));

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
8
```

**时间复杂度:** O(N)