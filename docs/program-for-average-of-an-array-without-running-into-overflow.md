# 对数组求平均值而不溢出的程序

> 原文:[https://www . geeksforgeeks . org/无溢出运行的阵列平均程序/](https://www.geeksforgeeks.org/program-for-average-of-an-array-without-running-into-overflow/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是在不溢出的情况下找到数组元素的[平均值。](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)

**示例:**

> **输入:** arr[] = { INT_MAX，INT_MAX }
> **输出:**
> 标准法平均值:-1.0000000000
> 高效法平均值:2147483647.000000000
> **说明:**
> 两个数标准法平均值为(和/ 2)。
> 由于两个数之和超过 INT_MAX，标准方法得到的输出不正确。
> 
> **输入:** arr[] = { INT_MAX，1，2 }
> **输出:**
> 用标准方法求平均值:-715827882.000000000000
> 用高效方法求平均值:715827882.03333333305

**方法:**给定的问题可以基于以下观察来解决:

*   **N** 数组元素的平均值可以通过将数组元素的[和除以 **N.** 得到，但是，如果数组包含大整数，计算数组**arr【】**](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的[和可能会导致整数溢出。](https://www.geeksforgeeks.org/python-program-to-find-sum-of-array/)
*   因此，可以通过以下步骤有效地计算阵列的平均值:
    *   [使用变量 **i** 在指数**【0，N-1】**的范围内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
    *   更新**avg =(avg+(arr[I]–avg)/(I+1))**

按照以下步骤解决问题:

*   初始化两个变量，将**求和**表示为 **0** ，将**平均**表示为 **0** ，分别存储数组元素的和与平均。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]，**更新**avg = avg+(arr[I]–avg)/(I+1)**并更新 **sum = sum + arr[i]。**
*   完成上述步骤后，用标准方法打印平均值，即 **sum / N** ，用高效方法打印平均值，即 **avg**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate average of
// an array using standard method
double average(int arr[], int N)
{
    // Stores the sum of array
    int sum = 0;

    // Find the sum of the array
    for (int i = 0; i < N; i++)
        sum += arr[i];

    // Return the average
    return (double)sum / N;
}

// Function to calculate average of
// an array using efficient method
double mean(int arr[], int N)
{
    // Store the average of the array
    double avg = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Update avg
        avg += (arr[i] - avg) / (i + 1);
    }

    // Return avg
    return avg;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { INT_MAX, 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << "Average by Standard method: " << fixed
         << setprecision(10) << average(arr, N) << endl;

    cout << "Average by Efficient method: " << fixed
         << setprecision(10) << mean(arr, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to calculate average of
// an array using standard method
static Double average(int arr[], int N)
{

    // Stores the sum of array
    int sum = 0;

    // Find the sum of the array
    for (int i = 0; i < N; i++)
        sum += arr[i];

    // Return the average
    return Double.valueOf(sum / N);
}

// Function to calculate average of
// an array using efficient method
static Double mean(int arr[], int N)
{

    // Store the average of the array
    Double avg = 0.0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Update avg
        avg += Double.valueOf((arr[i] - avg) / (i + 1));
    }

    // Return avg
    return avg;
}

// Driver Code
public static void main(String args[])
{

    // Input
    int arr[] = {Integer.MAX_VALUE, 1, 2 };
    int N = arr.length;

    // Function call
    System.out.println("Average by Standard method: "+ String.format("%.10f", average(arr, N)));
    System.out.println("Average by Efficient method: "+ String.format("%.10f", mean(arr, N)));
}
}

// This code is contributed by ipg2016107.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to calculate average of
# an array using standard method
def average(arr, N):

    # Stores the sum of array
    sum = 0

    # Find the sum of the array
    for i in range(N):
        sum += arr[i]

    # Return the average
    return sum // N * 1.0 - 1

# Function to calculate average of
# an array using efficient method
def mean(arr, N):

    # Store the average of the array
    avg = 0

    # Traverse the array arr[]
    for i in range(N):

        # Update avg
        avg += (arr[i] - avg) / (i + 1)

    # Return avg
    return round(avg, 7)

# Driver Code
if __name__ == '__main__':

    # Input
    arr = [2147483647, 1, 2]
    N = len(arr)

    # Function call
    print("Average by Standard method: ","{:.10f}".format(
        -1.0 * average(arr, N)))

    print("Average by Efficient method: ","{:.10f}".format(
        mean(arr, N)))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate average of
// an array using standard method
static double average(int[] arr, int N)
{

    // Stores the sum of array
    int sum = 0;

    // Find the sum of the array
    for(int i = 0; i < N; i++)
        sum += arr[i];

    // Return the average
    return (double)(sum / N);
}

// Function to calculate average of
// an array using efficient method
static double mean(int[] arr, int N)
{

    // Store the average of the array
    double avg = 0.0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update avg
        avg += ((double)((arr[i] - avg) / (i + 1)));
    }

    // Return avg
    return avg;
}

// Driver Code
static public void Main()
{

    // Input
    int[] arr = { Int32.MaxValue, 1, 2 };
    int N = arr.Length;

    // Function call
    Console.WriteLine("Average by Standard method: " +
         (average(arr, N)).ToString("F10"));
    Console.WriteLine("Average by Efficient method: " +
         (mean(arr, N)).ToString("F10"));
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate average of
// an array using standard method
function average(arr, N)
{
    // Stores the sum of array
    var sum = 0;

    // Find the sum of the array
    for(var i = 0; i < N; i++)
        sum += arr[i];

    if(sum>2147483647)
    {
        sum = -2147483647 + (sum - 2147483649)
    }

    // Return the average
    return parseInt(sum / N);
}

// Function to calculate average of
// an array using efficient method
function mean(arr, N)
{
    // Store the average of the array
    var avg = 0;

    // Traverse the array arr[]
    for(var i = 0; i < N; i++) {

        // Update avg
        avg += parseFloat((arr[i] - avg) / (i + 1));
    }

    // Return avg
    return avg;
}

// Driver Code
// Input
var arr = [2147483647, 1, 2 ];
var N = arr.length
// Function call
document.write( "Average by Standard method: " + average(arr, N).toFixed(10) + "<br>");
document.write( "Average by Efficient method: " + mean(arr, N).toFixed(10)+ "<br>");

</script>
```

**Output:** 

```
Average by Standard method: -715827882.0000000000
Average by Efficient method: 715827883.3333332539
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)