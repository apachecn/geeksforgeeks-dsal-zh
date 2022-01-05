# 等于所有后续元素之和的元素索引

> 原文:[https://www . geeksforgeeks . org/等于所有后续元素总和的元素索引/](https://www.geeksforgeeks.org/index-of-the-elements-which-are-equal-to-the-sum-of-all-succeeding-elements/)

给定一个正整数数组**arr[]****N**。任务是找到等于所有后续元素之和的元素索引。如果不存在这样的元素，则打印 **-1** 。
**举例:**

> **输入:** arr[] = { 36，2，17，6，6，5 }
> **输出:**0 2
> arr[0]= arr[1]+arr[2]+arr[3]+arr[4]+arr[5]
> arr[2]= arr[3]+arr[4]+arr[5]
> **输入:**arr[= { 7，25，17，7}
> **输出**

**方法:**从最后一个索引开始遍历给定数组**arr【】**时，保持一个 **sum** 变量，该变量存储到目前为止遍历的元素的总和。将总和与当前元素**arr【I】**进行比较。如果相等，将该元素的索引推入答案[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)。如果最终答案向量的大小为 0，则打印 **-1** 否则打印其内容。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the valid indices
void find_idx(int arr[], int n)
{

    // Vector to store the indices
    vector<int> answer;

    // Initialise sum with 0
    int sum = 0;

    // Starting from the last element
    for (int i = n - 1; i >= 0; i--) {

        // If sum till now is equal to
        // the current element
        if (sum == arr[i]) {
            answer.push_back(i);
        }

        // Add current element to the sum
        sum += arr[i];
    }

    if (answer.size() == 0) {
        cout << "-1";
        return;
    }

    for (int i = answer.size() - 1; i >= 0; i--)
        cout << answer[i] << " ";
}

// Driver code
int main()
{
    int arr[] = { 36, 2, 17, 6, 6, 5 };
    int n = sizeof(arr) / sizeof(int);

    find_idx(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to find the valid indices
    static void find_idx(int arr[], int n)
    {

        // Vector to store the indices
        Vector answer = new Vector();

        // Initialise sum with 0
        int sum = 0;

        // Starting from the last element
        for (int i = n - 1; i >= 0; i--)
        {

            // If sum till now is equal to
            // the current element
            if (sum == arr[i])
            {
                answer.add(i);
            }

            // Add current element to the sum
            sum += arr[i];
        }

        if (answer.size() == 0)
        {
            System.out.println("-1");
            return;
        }

        for (int i = answer.size() - 1; i >= 0; i--)
            System.out.print(answer.get(i) + " ");
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 36, 2, 17, 6, 6, 5 };
        int n = arr.length;

        find_idx(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the valid indices
def find_idx(arr, n):

    # List to store the indices
    answer=[]

    # Initialise sum with 0
    _sum = 0

    # Starting from the last element
    for i in range(n - 1, -1, -1):

        # If sum till now is equal to
        # the current element
        if (_sum == arr[i]) :
            answer.append(i)

        # Add current element to the sum
        _sum += arr[i]

    if (len(answer) == 0) :
        print(-1)
        return

    for i in range(len(answer) - 1, -1, -1):
        print(answer[i], end = " ")

# Driver code
arr = [ 36, 2, 17, 6, 6, 5 ]
n = len(arr)

find_idx(arr, n)

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the valid indices
    static void find_idx(int[] arr, int n)
    {

        // List to store the indices
        List<int> answer = new List<int>();

        // Initialise sum with 0
        int sum = 0;

        // Starting from the last element
        for (int i = n - 1; i >= 0; i--)
        {

            // If sum till now is equal to
            // the current element
            if (sum == arr[i])
            {
                answer.Add(i);
            }

            // Add current element to the sum
            sum += arr[i];
        }

        if (answer.Count == 0)
        {
            Console.WriteLine("-1");
            return;
        }

        for (int i = answer.Count - 1; i >= 0; i--)
            Console.Write(answer[i] + " ");
    }

    // Driver code
    public static void Main (String[] args)
    {
        int[] arr = { 36, 2, 17, 6, 6, 5 };
        int n = arr.Length;

        find_idx(arr, n);
    }
}

// This code is contributed by Ashutosh450
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to find the valid indices
function find_idx(arr, n) {

    // Vector to store the indices
    let answer = [];

    // Initialise sum with 0
    let sum = 0;

    // Starting from the last element
    for (let i = n - 1; i >= 0; i--) {

        // If sum till now is equal to
        // the current element
        if (sum == arr[i]) {
            answer.push(i);
        }

        // Add current element to the sum
        sum += arr[i];
    }

    if (answer.length == 0) {
        document.write("-1");
        return;
    }

    for (let i = answer.length - 1; i >= 0; i--)
        document.write(answer[i] + " ");
}

// Driver code
let arr = [36, 2, 17, 6, 6, 5];
let n = arr.length;

find_idx(arr, n);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
0 2
```