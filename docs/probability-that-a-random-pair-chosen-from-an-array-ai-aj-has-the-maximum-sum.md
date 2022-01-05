# 从数组(a[i]，a[j])中选择的随机对具有最大和的概率

> 原文:[https://www . geesforgeks . org/从数组中随机选择一对的概率 ai-aj-有最大和/](https://www.geeksforgeeks.org/probability-that-a-random-pair-chosen-from-an-array-ai-aj-has-the-maximum-sum/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是在选择一个随机对时，找出从数组中获得最大和对 **(arr[i]，arr[j])** 的概率。
**举例:**

> **输入:** arr[] = {3，3，3，3}
> **输出:** 1
> 所有对将给出最大和，即 6。
> **输入:** arr[] = {1，1，1，2，2，2}
> **输出:** 0.2
> 只有对(2，2)、(2，2)和(2，2)会给出
> 15 对中的最大和。
> 3 / 15 = 0.2

**方法:**运行两个嵌套循环以获得每一对的总和，保留任何对的最大总和及其计数(即给出该总和的对的数量)。现在，得到这个总数的概率将是**(计数/总计对)**，其中**总计对=(n *(n–1))/2**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the probability
// of getting the maximum pair sum
// when a random pair is chosen
// from the given array
float findProb(int arr[], int n)
{

    // Initialize the maximum sum, its count
    // and the count of total pairs
    long maxSum = INT_MIN, maxCount = 0, totalPairs = 0;

    // For every single pair
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Get the sum of the current pair
            int sum = arr[i] + arr[j];

            // If the sum is equal to the current
            // maximum sum so far
            if (sum == maxSum) {

                // Increment its count
                maxCount++;
            }

            // If the sum is greater than
            // the current maximum
            else if (sum > maxSum) {

                // Update the current maximum and
                // re-initialize the count to 1
                maxSum = sum;
                maxCount = 1;
            }

            totalPairs++;
        }
    }

    // Find the required probability
    float prob = (float)maxCount / (float)totalPairs;
    return prob;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 1, 2, 2, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << findProb(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the probability
// of getting the maximum pair sum
// when a random pair is chosen
// from the given array
static float findProb(int arr[], int n)
{

    // Initialize the maximum sum, its count
    // and the count of total pairs
    long maxSum = Integer.MIN_VALUE,
         maxCount = 0, totalPairs = 0;

    // For every single pair
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // Get the sum of the current pair
            int sum = arr[i] + arr[j];

            // If the sum is equal to the current
            // maximum sum so far
            if (sum == maxSum)
            {

                // Increment its count
                maxCount++;
            }

            // If the sum is greater than
            // the current maximum
            else if (sum > maxSum)
            {

                // Update the current maximum and
                // re-initialize the count to 1
                maxSum = sum;
                maxCount = 1;
            }

            totalPairs++;
        }
    }

    // Find the required probability
    float prob = (float)maxCount /
                 (float)totalPairs;
    return prob;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 1, 1, 1, 2, 2, 2 };
    int n = arr.length;

    System.out.println(findProb(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to return the probability
# of getting the maximum pair sum
# when a random pair is chosen
# from the given array
def findProb(arr, n) :

    # Initialize the maximum sum, its count
    # and the count of total pairs
    maxSum = -(sys.maxsize - 1);
    maxCount = 0;
    totalPairs = 0;

    # For every single pair
    for i in range(n - 1) :
        for j in range(i + 1, n) :

            # Get the sum of the current pair
            sum = arr[i] + arr[j];

            # If the sum is equal to the current
            # maximum sum so far
            if (sum == maxSum) :

                # Increment its count
                maxCount += 1;

            # If the sum is greater than
            # the current maximum
            elif (sum > maxSum) :

                # Update the current maximum and
                # re-initialize the count to 1
                maxSum = sum;
                maxCount = 1;

            totalPairs += 1;

    # Find the required probability
    prob = maxCount / totalPairs;

    return prob;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1, 1, 2, 2, 2 ];
    n = len(arr);

    print(findProb(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to return the probability
// of getting the maximum pair sum
// when a random pair is chosen
// from the given array
static float findProb(int []arr, int n)
{

    // Initialize the maximum sum, its count
    // and the count of total pairs
    long maxSum = int.MinValue,
        maxCount = 0, totalPairs = 0;

    // For every single pair
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {

            // Get the sum of the current pair
            int sum = arr[i] + arr[j];

            // If the sum is equal to the current
            // maximum sum so far
            if (sum == maxSum)
            {

                // Increment its count
                maxCount++;
            }

            // If the sum is greater than
            // the current maximum
            else if (sum > maxSum)
            {

                // Update the current maximum and
                // re-initialize the count to 1
                maxSum = sum;
                maxCount = 1;
            }

            totalPairs++;
        }
    }

    // Find the required probability
    float prob = (float)maxCount /
                 (float)totalPairs;
    return prob;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 1, 1, 2, 2, 2 };
    int n = arr.Length;

    Console.WriteLine(findProb(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the probability
// of getting the maximum pair sum
// when a random pair is chosen
// from the given array
function findProb(arr, n)
{

    // Initialize the maximum sum, its count
    // and the count of total pairs
    var maxSum = -100000000, maxCount = 0, totalPairs = 0;

    // For every single pair
    for (var i = 0; i < n - 1; i++) {
        for (var j = i + 1; j < n; j++) {

            // Get the sum of the current pair
            var sum = arr[i] + arr[j];

            // If the sum is equal to the current
            // maximum sum so far
            if (sum == maxSum) {

                // Increment its count
                maxCount++;
            }

            // If the sum is greater than
            // the current maximum
            else if (sum > maxSum) {

                // Update the current maximum and
                // re-initialize the count to 1
                maxSum = sum;
                maxCount = 1;
            }

            totalPairs++;
        }
    }

    // Find the required probability
    var prob = maxCount / totalPairs;
    return prob;
}

// Driver code
var arr = [ 1, 1, 1, 2, 2, 2 ]
var n = arr.length;
document.write(findProb(arr, n));

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
0.2
```

**时间复杂度:** O(n <sup>2</sup> )