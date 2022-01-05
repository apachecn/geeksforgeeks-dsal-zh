# 数组中重复‘k’次的所有元素的总和

> 原文:[https://www . geeksforgeeks . org/所有元素的总和-重复-k 次数组/](https://www.geeksforgeeks.org/sum-of-all-elements-repeating-k-times-in-an-array/)

给定一个数组，我们必须找到数组中重复 k 次的所有元素的和。我们只需要在总和中考虑一次每个重复元素。
**例:**

```
Input : arr[] = {2, 3, 9, 9}
            k = 1
Output : 5
2 + 3 = 5

Input : arr[] = {9, 8, 8, 8, 10, 4}
          k = 3
Output : 8
```

一个**简单的解决方案**是使用两个嵌套循环来计算每个元素的出现次数。在计数时，我们只需要考虑尚未考虑的元素。

## C++

```
// C++ program find sum of elements that
// appear k times.
#include <bits/stdc++.h>
using namespace std;

// Function to count the sum
int sumKRepeating(int arr[], int n, int k)
{
    int sum = 0;

    // To keep track of processed elements
    vector<bool> visited(n, false);

    // initializing count equal to zero
    for (int i = 0; i < n; i++) {

        // If arr[i] already processed
        if (visited[i] == true)
            continue;

        // counting occurrences of arr[i]
        int count = 1;
        for (int j = i + 1; j < n; j++) {           
            if (arr[i] == arr[j]) {
                count++;
                visited[j] = true;
            }
        }

        if (count == k)
           sum += arr[i];
    }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 9, 9, 10, 11, 8, 8, 9, 8 };
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 3;
    cout << sumKRepeating(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program find sum of
// elements that appear k times.
import java.util.*;

class GFG
{
// Function to count the sum
static int sumKRepeating(int arr[],
                         int n, int k)
{
    int sum = 0;

    // To keep track of
    // processed elements
    Vector<Boolean> visited = new Vector<Boolean>();

    for (int i = 0; i < n; i++)
    visited.add(false);

    // initializing count
    // equal to zero
    for (int i = 0; i < n; i++)
    {

        // If arr[i] already processed
        if (visited.get(i) == true)
            continue;

        // counting occurrences of arr[i]
        int count = 1;
        for (int j = i + 1; j < n; j++)
        {        
            if (arr[i] == arr[j])
            {
                count++;
                visited.add(j, true);
            }
        }

        if (count == k)
        sum += arr[i];
    }

    return sum;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 9, 9, 10, 11,
                  8, 8, 9, 8 };
    int n = arr.length;
    int k = 3;
    System.out.println(sumKRepeating(arr, n, k));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program find sum of elements
# that appear k times.

# Function to count the sum
def sumKRepeating(arr, n, k):
    sum = 0

    # To keep track of processed elements
    visited = [False for i in range(n)]

    # initializing count equal to zero
    for i in range(0, n, 1):

        # If arr[i] already processed
        if (visited[i] == True):
            continue

        # counting occurrences of arr[i]
        count = 1
        for j in range(i + 1, n, 1):
            if (arr[i] == arr[j]):
                count += 1
                visited[j] = True

        if (count == k):
            sum += arr[i]

    return sum

# Driver code
if __name__ == '__main__':
    arr = [9, 9, 10, 11, 8, 8, 9, 8]
    n = len(arr)
    k = 3
    print(sumKRepeating(arr, n, k))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// c# program find sum of
// elements that appear k times.
using System;
using System.Collections.Generic;

class GFG
{
// Function to count the sum
public static int sumKRepeating(int[] arr,
                                int n, int k)
{
    int sum = 0;

    // To keep track of
    // processed elements
    List<bool> visited = new List<bool>();

    for (int i = 0; i < n; i++)
    {
        visited.Add(false);
    }

    // initializing count
    // equal to zero
    for (int i = 0; i < n; i++)
    {

        // If arr[i] already processed
        if (visited[i] == true)
        {
            continue;
        }

        // counting occurrences of arr[i]
        int count = 1;
        for (int j = i + 1; j < n; j++)
        {
            if (arr[i] == arr[j])
            {
                count++;
                visited.Insert(j, true);
            }
        }

        if (count == k)
        {
            sum += arr[i];
        }
    }

    return sum;
}

// Driver code
public static void Main(string[] args)
{
    int[] arr = new int[] {9, 9, 10, 11,
                           8, 8, 9, 8};
    int n = arr.Length;
    int k = 3;
    Console.WriteLine(sumKRepeating(arr, n, k));
}
}

// This code is contributed
// by Shrikant13
```

## java 描述语言

```
<script>
// Javascript program find sum of
// elements that appear k times.

// Function to count the sum
function sumKRepeating(arr,n,k)
{
    let sum = 0;

    // To keep track of
    // processed elements
    let visited = [];

    for (let i = 0; i < n; i++)
        visited.push(false);

    // initializing count
    // equal to zero
    for (let i = 0; i < n; i++)
    {

        // If arr[i] already processed
        if (visited[i] == true)
            continue;

        // counting occurrences of arr[i]
        let count = 1;
        for (let j = i + 1; j < n; j++)
        {        
            if (arr[i] == arr[j])
            {
                count++;
                visited[j]= true;
            }
        }

        if (count == k)
            sum += arr[i];
    }

    return sum;
}

// Driver code
let arr=[9, 9, 10, 11,
                  8, 8, 9, 8 ];

let n = arr.length;
let k = 3;
document.write(sumKRepeating(arr, n, k));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
17
```