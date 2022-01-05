# 求数组中最大除数子集

> 原文:[https://www . geesforgeks . org/find-数组中最大除数子集/](https://www.geeksforgeeks.org/find-the-largest-divisor-subset-in-the-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到 **arr[]** 的最大子集，使得在该子集的每对数字中，一个数字是另一个数字的除数。
**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 4 2 1
> 所有可能的子序列对为:
> (4，2) - > 4 % 2 = 0
> (4，1) - > 4 % 1 = 0
> 和(2，1) - > 2 % 1 = 0
> **输入:** arr[] = {1，3，4，9 }

****方法:**这里的任务是找到最大的子集，其中在每对数字中，一个可被另一个整除，即对于序列 **a <sub>1</sub> ，a <sub>2</sub> ，a<sub>3</sub>…a<sub>k</sub>T11】其中**a<sub>1</sub>üa<sub>2</sub>≤a<sub>k</sub>T19】和这个序列可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)找到(类似于[最长递增子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/))。
以下是上述方法的实施:******

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required subsequence
void findSubSeq(int arr[], int n)
{

    // Sort the array
    sort(arr, arr + n);

    // Keep a count of the length of the
    // subsequence and the previous element
    int count[n] = { 1 };
    int prev[n] = { -1 };

    // Set the initial values
    memset(count, 1, sizeof(count));
    memset(prev, -1, sizeof(prev));

    // Maximum length of the subsequence and
    // the last element
    int max = 0;
    int maxprev = -1;

    // Run a loop for every element
    for (int i = 0; i < n; i++) {

        // Check for all the divisors
        for (int j = i - 1; j >= 0; j--) {

            // If the element is a divisor and the length
            // of subsequence will increase by adding
            // j as previous element of i
            if (arr[i] % arr[j] == 0
                && count[j] + 1 > count[i]) {

                // Increase the count
                count[i] = count[j] + 1;
                prev[i] = j;
            }
        }

        // Update the max count
        if (max < count[i]) {
            max = count[i];
            maxprev = i;
        }
    }

    // Get the last index of the subsequence
    int i = maxprev;
    while (i >= 0) {

        // Print the element
        if (arr[i] != -1)
            cout << arr[i] << " ";

        // Move the index to the previous element
        i = prev[i];
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(int);

    findSubSeq(arr, n);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.*;
class GFG
{

    // Function to find the required subsequence
    static void findSubSeq(int arr[], int n)
    {

        // Sort the array
        Arrays.sort(arr);

        // Keep a count of the length of the
        // subsequence and the previous element
        int count[] = new int[n];
        int prev[] = new int[n];

        int i, j;

        // Set the initial values
        for(i = 0 ; i < n; i++)
        count[i] = 1;

        for(j = 0; j < n; j++)
            prev[j] = -1;

        // Maximum length of the subsequence and
        // the last element
        int max = 0;
        int maxprev = -1;

        // Run a loop for every element
        for ( i = 0; i < n; i++)
        {

            // Check for all the divisors
            for ( j = i - 1; j >= 0; j--)
            {

                // If the element is a divisor and
                // the length of subsequence will
                // increase by adding j as
                // previous element of i
                if (arr[i] % arr[j] == 0 &&
                    count[j] + 1 > count[i])
                {

                    // Increase the count
                    count[i] = count[j] + 1;
                    prev[i] = j;
                }
            }

            // Update the max count
            if (max < count[i])
            {
                max = count[i];
                maxprev = i;
            }
        }

        // Get the last index of the subsequence
        i = maxprev;
        while (i >= 0)
        {

            // Print the element
            if (arr[i] != -1)
                System.out.print(arr[i] + " ");

            // Move the index to the previous element
            i = prev[i];
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int n = arr.length;

        findSubSeq(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Function to find the required subsequence
def findSubSeq(arr, n) :

    # Sort the array
    arr.sort();

    # Keep a count of the length of the
    # subsequence and the previous element
    # Set the initial values
    count = [1] * n;
    prev = [-1] * n;

    # Maximum length of the subsequence and
    # the last element
    max = 0;
    maxprev = -1;

    # Run a loop for every element
    for i in range(n) :

        # Check for all the divisors
        for j in range(i - 1, -1, -1) :

            # If the element is a divisor and the length
            # of subsequence will increase by adding
            # j as previous element of i
            if (arr[i] % arr[j] == 0 and
                count[j] + 1 > count[i]) :

                # Increase the count
                count[i] = count[j] + 1;
                prev[i] = j;

        # Update the max count
        if (max < count[i]) :
            max = count[i];
            maxprev = i;

    # Get the last index of the subsequence
    i = maxprev;
    while (i >= 0) :

        # Print the element
        if (arr[i] != -1) :
            print(arr[i], end = " ");

        # Move the index to the previous element
        i = prev[i];

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5 ];
    n = len(arr);

    findSubSeq(arr, n);

# This code is contributed by AnkitRai01
```

## **C#**

```
// C# implementation of the approach
using System;
using System.Collections;

class GFG
{

    // Function to find the required subsequence
    static void findSubSeq(int []arr, int n)
    {

        // Sort the array
        Array.Sort(arr);

        // Keep a count of the length of the
        // subsequence and the previous element
        int []count = new int[n];
        int []prev = new int[n];

        int i, j;

        // Set the initial values
        for(i = 0; i < n; i++)
        count[i] = 1;

        for(j = 0; j < n; j++)
            prev[j] = -1;

        // Maximum length of the subsequence 
        // and the last element
        int max = 0;
        int maxprev = -1;

        // Run a loop for every element
        for ( i = 0; i < n; i++)
        {

            // Check for all the divisors
            for ( j = i - 1; j >= 0; j--)
            {

                // If the element is a divisor and
                // the length of subsequence will
                // increase by adding j as
                // previous element of i
                if (arr[i] % arr[j] == 0 &&
                    count[j] + 1 > count[i])
                {

                    // Increase the count
                    count[i] = count[j] + 1;
                    prev[i] = j;
                }
            }

            // Update the max count
            if (max < count[i])
            {
                max = count[i];
                maxprev = i;
            }
        }

        // Get the last index of the subsequence
        i = maxprev;
        while (i >= 0)
        {

            // Print the element
            if (arr[i] != -1)
                Console.Write(arr[i] + " ");

            // Move the index to the previous element
            i = prev[i];
        }
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;

        findSubSeq(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## **java 描述语言**

```
<script>
// Javascript implementation of above approach

// Function to find the required subsequence
function findSubSeq(arr, n)
{

    // Sort the array
    arr.sort();

    // Keep a count of the length of the
    // subsequence and the previous element
    var count = new Array(n);
    var prev = new Array(n);

    // Set the initial values
    count.fill(1);
    prev.fill(-1);

    // Maximum length of the subsequence and
    // the last element
    var max = 0;
    var maxprev = -1;

    // Run a loop for every element
    for (var i = 0; i < n; i++) {

        // Check for all the divisors
        for (var j = i - 1; j >= 0; j--) {

            // If the element is a divisor and the length
            // of subsequence will increase by adding
            // j as previous element of i
            if (arr[i] % arr[j] == 0
                && count[j] + 1 > count[i]) {

                // Increase the count
                count[i] = count[j] + 1;
                prev[i] = j;
            }
        }

        // Update the max count
        if (max < count[i]) {
            max = count[i];
            maxprev = i;
        }
    }

    // Get the last index of the subsequence
    var i = maxprev;
    while (i >= 0) {

        // Print the element
        if (arr[i] != -1)
            document.write( arr[i] + " ");

        // Move the index to the previous element
        i = prev[i];
    }
}

var arr = [ 1, 2, 3, 4, 5 ];
var n = arr.length;
findSubSeq(arr, n);

//This code is contributed by SoumikMondal
</script>
```

****Output:** 

```
4 2 1
```** 

****时间复杂度:** O(N <sup>2</sup> )**

****辅助空间:** O(1)**