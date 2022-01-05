# 寻找数组中最小的连续和对

> 原文:[https://www . geeksforgeeks . org/find-最小邻接数组中的和对/](https://www.geeksforgeeks.org/find-the-smallest-contiguous-sum-pair-in-an-array/)

给定一个包含 **N** 个不同整数的**数组 arr[]** ，任务是找到一个连续的对，使得该对中两个元素的和最小。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** (1，2)
> **解释:**
> 这里，与其和相连的对是(1，2) = 3，(2，3) = 5，(3，4) = 7，最小值是 3。
> **输入:** arr[] = {4，9，-3，2，0}
> **输出:** (-3，2)
> **解释:**
> 这里，与其和相连的对是(4，9) = 13，(9，-3) = 6，(-3，2) = -1，(2，0) = 2

**方法:**
为了解决上面提到的问题，我们必须考虑所有连续的对，并找到它们的和。具有最小(最小)和的一对是必需的答案。
以下是上述方法的实施:

## C++

```
//C++ program to find the smallest
// sum contiguous pair
#include<bits/stdc++.h>
using namespace std;

// Function to find the smallest sum
// contiguous pair
vector<int> smallestSumpair(int arr[], int n)
{

    // Contiguous pair
    vector<int>pair;

    // Initialize minimum sum
    // with maximum value
    int min_sum = INT_MAX;

    for(int i = 1; i < n; i++)
    {

        // Checking for minimum value
        if( min_sum > (arr[i] + arr[i - 1]))
        {
            min_sum = arr[i] + arr[i - 1];
            if (pair.empty())
            {

                // Add to pair
                pair.push_back(arr[i - 1]);
                pair.push_back(arr[i]);
            }
            else
            {

                // Updating pair
                pair[0] = arr[i - 1];
                pair[1] = arr[i];
            }
        }
    }
    return pair;
}

// Driver code
int main()
{
   int arr[] = {4, 9, -3, 2, 0};
   int n = sizeof(arr) / sizeof(arr[0]);

   vector<int>pair = smallestSumpair(arr, n);
   cout << pair[0] << " " << pair[1];
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest
// sum contiguous pair
import java.util.*;

class GFG{

// Function to find the smallest sum
// contiguous pair
public static Vector<Integer> smallestSumpair(int[] arr,
                                              int n)
{

    // Stores the contiguous pair
    Vector<Integer> pair = new Vector<Integer>();

    // Initialize minimum sum
    int min_sum = Integer.MAX_VALUE, i;

    for(i = 1; i < n; i++)
    {

        // Checking for minimum value
        if (min_sum > (arr[i] + arr[i - 1]))
        {
            min_sum = arr[i] + arr[i - 1];

            if (pair.isEmpty())
            {

                // Add to pair
                pair.add(arr[i - 1]);
                pair.add(arr[i]);
            }
            else
            {

                // Updating pair
                pair.set(0, arr[i - 1]);
                pair.set(1, arr[i]);
            }
        }
    }
    return pair;
}

// Driver Code        
public static void main(String[] args)
{
    int arr[] = { 4, 9, -3, 2, 0 };
    int N = arr.length;

    Vector<Integer> pair = new Vector<Integer>();
    pair = smallestSumpair(arr, N);

    System.out.println(pair.get(0) + " " +
                       pair.get(1));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find the smallest
# sum contiguous pair

# importing sys
import sys

# Function to find the smallest sum
# contiguous pair

def smallestSumpair(arr, n):

    # Contiguous pair
    pair = []

    # isntialize minimum sum
    # with maximum value
    min_sum = sys.maxsize

    for i in range(1, n):

        # checking for minimum value
        if min_sum > (arr[i] + arr[i-1]):
            min_sum = arr[i] + arr[i-1]

            if pair == []:

                # Add to pair
                pair.append(arr[i-1])
                pair.append(arr[i])
            else:

                # Updating pair
                pair[0] = arr[i-1]
                pair[1] = arr[i]

    return pair

# Driver code
arr = [4, 9, -3, 2, 0]
n = len(arr)
pair = smallestSumpair(arr, n)
print(pair[0], pair[1])
```

## C#

```
// C# program to find the smallest
// sum contiguous pair
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to find the smallest sum
// contiguous pair
public static ArrayList smallestSumpair(int[] arr,
                                        int n)
{

    // Stores the contiguous pair
    ArrayList pair = new ArrayList();

    // Initialize minimum sum
    int min_sum = int.MaxValue, i;

    for(i = 1; i < n; i++)
    {

        // Checking for minimum value
        if (min_sum > (arr[i] + arr[i - 1]))
        {
            min_sum = arr[i] + arr[i - 1];

            if (pair.Count == 0)
            {

                // Add to pair
                pair.Add(arr[i - 1]);
                pair.Add(arr[i]);
            }
            else
            {

                // Updating pair
                pair[0] = arr[i - 1];
                pair[1] = arr[i];
            }
        }
    }
    return pair;
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 4, 9, -3, 2, 0 };
    int N = arr.Length;

    ArrayList pair = new ArrayList();
    pair = smallestSumpair(arr, N);

    Console.Write(pair[0] + " " + pair[1]);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program to find the smallest
// sum contiguous pair

// Function to find the smallest sum
// contiguous pair
function smallestSumpair(arr,n)
{
    // Stores the contiguous pair
    let pair = [];

    // Initialize minimum sum
    let min_sum = Number.MAX_VALUE, i;

    for(i = 1; i < n; i++)
    {

        // Checking for minimum value
        if (min_sum > (arr[i] + arr[i - 1]))
        {
            min_sum = arr[i] + arr[i - 1];

            if (pair.length==0)
            {

                // Add to pair
                pair.push(arr[i - 1]);
                pair.push(arr[i]);
            }
            else
            {

                // Updating pair
                pair[0] = arr[i - 1];
                pair[1] = arr[i];
            }
        }
    }
    return pair;
}

// Driver Code  
let arr=[4, 9, -3, 2, 0 ];
let  N = arr.length;
let pair = smallestSumpair(arr, N);

document.write(pair[0] + " " +
                   pair[1]);

// This code is contributed by rag2127
</script>
```

**Output**

```
-3 2
```

***时间复杂度:**O(n)*T4】