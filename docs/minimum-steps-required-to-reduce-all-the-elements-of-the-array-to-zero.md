# 将数组的所有元素减少到零所需的最小步骤

> 原文:[https://www . geesforgeks . org/将数组的所有元素减少到零所需的最少步骤/](https://www.geeksforgeeks.org/minimum-steps-required-to-reduce-all-the-elements-of-the-array-to-zero/)

给定一个正整数数组 **arr[]** ，任务是找到将所有元素减少到 **0** 的最小步骤。在单个步骤中， **-1** 可以同时添加到数组的所有非零元素中。
**举例:**

> **输入:** arr[] = {1，5，6}
> **输出:** 6
> 操作 1: arr[] = {0，4，5}
> 操作 2: arr[] = {0，3，4}
> 操作 3: arr[] = {0，2，3}
> 操作 4: arr[] = {0，1，2}
> 操作 5: arr[] = {0，0，1}
> 操作 6: arr[] = {0，0，1}

**天真的方法:**一个简单的方法是首先对数组进行排序，然后从最小元素开始，计算将其减少到 0 所需的步骤数。这个计数将从下一个数组元素开始减少，因为所有元素将同时更新。
**高效方法:**可以观察到，最小步数总是等于数组中的最大元素。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum steps
// required to reduce all the elements to 0
int minSteps(int arr[], int n)
{

    // Maximum element from the array
    int maxVal = *max_element(arr, arr + n);
    return maxVal;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4 };
    int n = sizeof(arr) / sizeof(int);

    cout << minSteps(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // method to get maximum number from array elements
    static int getMax(int inputArray [])
    {
        int maxValue = inputArray[0];

        for(int i = 1; i < inputArray.length; i++)
        {
            if(inputArray[i] > maxValue)
            {
                maxValue = inputArray[i];
            }
        }
        return maxValue;
    }

    // Function to return the minimum steps
    // required to reduce all the elements to 0
    static int minSteps(int arr[], int n)
    {

        // Maximum element from the array
        int maxVal = getMax(arr);
        return maxVal;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 4 };
        int n = arr.length;

        System.out.println(minSteps(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum steps
# required to reduce all the elements to 0
def minSteps(arr, n):

    # Maximum element from the array
    maxVal = max(arr)
    return maxVal

# Driver code
arr = [1, 2, 4]
n = len(arr)

print(minSteps(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // method to get maximum number from array elements
    static int getMax(int []inputArray)
    {
        int maxValue = inputArray[0];

        for(int i = 1; i < inputArray.Length; i++)
        {
            if(inputArray[i] > maxValue)
            {
                maxValue = inputArray[i];
            }
        }
        return maxValue;
    }

    // Function to return the minimum steps
    // required to reduce all the elements to 0
    static int minSteps(int []arr, int n)
    {

        // Maximum element from the array
        int maxVal = getMax(arr);
        return maxVal;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []arr = { 1, 2, 4 };
        int n = arr.Length;

        Console.WriteLine(minSteps(arr, n));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimum steps
// required to reduce all the elements to 0
function minSteps(arr, n)
{

    // Maximum element from the array
    let maxVal = Math.max(...arr);
    return maxVal;
}

// Driver code
    let arr = [ 1, 2, 4 ];
    let n = arr.length;

    document.write(minSteps(arr, n));

</script>
```

**Output:** 

```
4
```