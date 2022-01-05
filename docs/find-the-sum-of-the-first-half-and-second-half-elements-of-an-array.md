# 求数组前半部分和后半部分元素的和

> 原文:[https://www . geesforgeks . org/find-数组的前半部分和后半部分元素之和/](https://www.geeksforgeeks.org/find-the-sum-of-the-first-half-and-second-half-elements-of-an-array/)

给定一个大小为 **N** 的数组 **arr** 。任务是求一个数组的前半部分( **N/2** )元素和后半部分元素(**N–N/2**)的和。
**示例:**

> **输入:** arr[] = {20，30，60，10，25，15，40}
> **输出:** 110，90
> 前 N/2 元素 20 + 30 + 60 之和为 110
> **输入:** arr[] = {50，35，20，15}
> **输出:** 85，35

**方法:**
将 SumFirst 和 SumSecond 初始化为 0。遍历给定数组，如果当前索引小于 N/2，则在 SumFirst 中添加元素，否则在 SumSecond 中添加元素。
以下是上述方法的实施:

## C++

```
// C++ program to find the sum of the first half
// elements and second half elements of an array
#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of the first half
// elements and second half elements of an array
void sum_of_elements(int arr[], int n)
{
    int sumfirst = 0, sumsecond = 0;

    for (int i = 0; i < n; i++) {
        // Add elements in first half sum
        if (i < n / 2)
            sumfirst += arr[i];

        // Add elements in the second half sum
        else
            sumsecond += arr[i];
    }

    cout << "Sum of first half elements is " <<
                                   sumfirst << endl;

    cout << "Sum of second half elements is " <<
                                   sumsecond << endl;
}

// Driver Code
int main()
{
    int arr[] = { 20, 30, 60, 10, 25, 15, 40 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    sum_of_elements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs
// whose sum divisible by 'K'
import java.util.*;

class GFG
{

public static void sum_of_elements(int []arr,
                                   int n)
{
    int sumfirst = 0, sumsecond = 0;

    for (int i = 0; i < n; i++)
    {

        // Add elements in first half sum
        if (i < n / 2)
        {
            sumfirst += arr[i];
        }

        // Add elements in the second half sum
        else
        {
            sumsecond += arr[i];
        }
    }

    System.out.println("Sum of first half elements is " +
                                             sumfirst);

    System.out.println("Sum of second half elements is " +
                                            sumsecond);
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 20, 30, 60, 10, 25, 15, 40 };
    int n = arr.length;

    // Function call
    sum_of_elements(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# the first half elements and
# second half elements of an array

# Function to find the sum of 
# the first half elements and
# second half elements of an array
def sum_of_elements(arr, n):

    sumfirst = 0;
    sumsecond = 0;

    for i in range(n):

        # Add elements in first half sum
        if (i < n // 2):
            sumfirst += arr[i];

        # Add elements in the second half sum
        else:
            sumsecond += arr[i];

    print("Sum of first half elements is",
                    sumfirst, end = "\n");
    print("Sum of second half elements is",
                    sumsecond, end = "\n");

# Driver Code
arr = [20, 30, 60, 10, 25, 15, 40];

n = len(arr);

# Function call
sum_of_elements(arr, n);

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to count pairs
// whose sum divisible by 'K'
using System;

class GFG
{
    public static void sum_of_elements(int []arr,
                                       int n)
    {

    int sumfirst = 0, sumsecond = 0;

    for (int i = 0; i < n; i++)
    {

        // Add elements in first half sum
        if (i < n / 2)
        {
            sumfirst += arr[i];
        }

        // Add elements in the second half sum
        else
        {
            sumsecond += arr[i];
        }
    }

    Console.WriteLine("Sum of first half elements is " +
                                              sumfirst);

    Console.WriteLine("Sum of second half elements is " +
                                              sumsecond);
}

// Driver code
static public void Main ()
{
    int []arr = { 20, 30, 60, 10, 25, 15, 40 };
    int n = arr.Length;

    // Function call
    sum_of_elements(arr, n);
}
}

// This code is contributed by nidhiva
```

## java 描述语言

```
<script>

// Javascript program to count pairs
// whose sum divisible by 'K'

    function sum_of_elements(arr , n)
    {
        var sumfirst = 0, sumsecond = 0;

        for (i = 0; i < n; i++) {

            // Add elements in first half sum
            if (i < parseInt(n / 2))
            {
                sumfirst += arr[i];
            }

            // Add elements in the second half sum
            else {
                sumsecond += arr[i];
            }
        }

        document.write(
     "Sum of first half elements is " + sumfirst+"<br/>"
        );

        document.write(
    "Sum of second half elements is " + sumsecond+"<br/>"
        );
    }

    // Driver code

        var arr = [ 20, 30, 60, 10, 25, 15, 40 ];
        var n = arr.length;

        // Function call
        sum_of_elements(arr, n);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
Sum of first half elements is 110
Sum of second half elements is 90
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)