# 每个员工的最低加薪幅度，这样就不会有员工觉得不公平

> 原文:[https://www . geeksforgeeks . org/每位员工最低加薪-没有员工觉得不公平/](https://www.geeksforgeeks.org/minimum-salary-hike-for-each-employee-such-that-no-employee-feels-unfair/)

一个公司有 **N** 个员工，每个员工都有一些评分。员工会根据他们的评分获得加薪，即评分较高的员工将获得更高的加薪。员工只知道其邻居的提价和评级，即员工的左侧和右侧。
给定一个表示 **N** 员工评分的正整数[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)T5【arr】，任务是找到每个员工应该提高的最低加薪幅度，这样就不会有员工觉得不公平。

**注:**提价仅为正整数，评级始终大于零。

**示例:**

> **输入:** arr[] = {1，3，5，4}
> **输出:** 1 2 3 1
> **说明:**
> 每个员工最低加薪的分配必须是:
> 1 + 2 + 3 + 1 = 6
> 
> **输入:** arr[] = {5，3，4，2，1，6}
> **输出:**2 1 3 2 1 2 2 2
> T6】说明:T8】每个员工最低加薪的分配必须是:
> 2 + 1 + 3 + 2 + 1 + 2 = 11

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。由于员工只知道他们邻居的 hike 和 rating，因此以下条件之一将适用于给定的 rating:

1.  **类型 1:**H<sub>I–1</sub>T8】H<sub>I</sub>T9】H<sub>I+1</sub>
2.  **类型 2:**H<sub>I–1</sub>T8】H<sub>I</sub>T9】H<sub>I+1</sub>
3.  **类型 3:**H<sub>I–1</sub>T8】H<sub>I</sub>T9】H<sub>I+1</sub>
4.  **类型 4:**H<sub>I–1</sub>T8】H<sub>I</sub>T9】H<sub>I+1</sub>

对于每个员工，基于上述条件，将每个员工的加薪设置为:

*   **类型 1:** 设置徒步至 **1** 。
*   **第二种:**通过 **H <sub>i-1</sub> + 1** 提高他的步幅。
*   **第三种:**通过 **H <sub>i+1</sub> + 1** 提高他的步幅。
*   **第四种:**提高**最大值(H <sub>i-1</sub> ，H <sub>i+1</sub> ) + 1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define INF 1e9

// Function that print minimum hike
void findMinHike(vector<int> arr,
                 int n)
{

    // Insert INF at begin and
    // end of array
    arr.insert(arr.begin(), INF);
    arr.push_back(INF);

    // To store hike of each employee
    vector<int> hike(n + 2, 0);

    // for Type 1 employee
    for (int i = 1; i <= n; i++) {

        if (arr[i - 1] >= arr[i]
            && arr[i] <= arr[i + 1]) {
            hike[i] = 1;
        }
    }

    // for Type 2 employee
    for (int i = 1; i <= n; i++) {
        if (arr[i - 1] < arr[i]
            && arr[i] <= arr[i + 1]) {
            hike[i] = hike[i - 1] + 1;
        }
    }

    // for Type 3 employee
    for (int i = 1; i <= n; i++) {
        if (arr[i - 1] >= arr[i]
            && arr[i] > arr[i + 1]) {
            hike[i] = hike[i + 1] + 1;
        }
    }

    // for Type 4 employee
    for (int i = 1; i <= n; i++) {
        if (arr[i - 1] < arr[i]
            && arr[i] > arr[i + 1]) {
            hike[i] = max(hike[i - 1],
                          hike[i + 1])
                      + 1;
        }
    }

    // Print the min hike for each employee
    for (int i = 1; i <= n; i++) {
        cout << hike[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given array of rating of employees
    vector<int> arr = { 5, 3, 4, 2, 1, 6 };

    // Function Call
    findMinHike(arr, arr.size());

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static final int INF = 10000009;

// Function that print minimum hike
static void findMinHike(Vector<Integer> arr,
                        int n)
{
  // Insert INF at begin and
  // end of array
  arr.add(0, INF);
  arr.add(INF);

  // To store hike of
  // each employee
  int []hike = new int[n + 2];

  // for Type 1 employee
  for (int i = 1; i <= n; i++)
  {
    if (arr.get(i - 1) >= arr.get(i) &&
        arr.get(i) <= arr.get(i + 1))
    {
      hike[i] = 1;
    }
  }

  // For Type 2 employee
  for (int i = 1; i <= n; i++)
  {
    if (arr.get(i - 1) < arr.get(i) &&
        arr.get(i) <= arr.get(i + 1))
    {
      hike[i] = hike[i - 1] + 1;
    }
  }

  // For Type 3 employee
  for (int i = 1; i <= n; i++)
  {
    if (arr.get(i - 1) >= arr.get(i) &&
        arr.get(i) > arr.get(i + 1))
    {
      hike[i] = hike[i + 1] + 1;
    }
  }

  // For Type 4 employee
  for (int i = 1; i <= n; i++)
  {
    if (arr.get(i - 1) < arr.get(i) &&
        arr.get(i) > arr.get(i + 1))
    {
      hike[i] = Math.max(hike[i - 1],
                         hike[i + 1]) + 1;
    }
  }

  // Print the min hike for each employee
  for (int i = 1; i <= n; i++)
  {
    System.out.print(hike[i] + " ");
  }
}

// Driver Code
public static void main(String[] args)
{
  // Given array of rating of employees
  Vector<Integer> arr = new Vector<>();

  arr.add(5);
  arr.add(3);
  arr.add(4);
  arr.add(2);
  arr.add(1);
  arr.add(6);

  // Function Call
  findMinHike(arr, arr.size());
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program for the above approach
INF = 1e9

# Function that print minimum hike
def findMinHike(arr,n):

    # Insert INF at begin and
    # end of array
    arr.insert(0, INF)
    arr.append(INF)

    # To store hike of each employee
    hike = [0] * (n + 2)

    # For Type 1 employee
    for i in range(1, n + 1):
        if (arr[i - 1] >= arr[i] and
            arr[i] <= arr[i + 1]):
            hike[i] = 1

    # For Type 2 employee
    for i in range(1, n + 1):
        if (arr[i - 1] < arr[i] and
            arr[i] <= arr[i + 1]):
            hike[i] = hike[i - 1] + 1

    # For Type 3 employee
    for i in range(1, n + 1):
        if (arr[i - 1] >= arr[i] and
            arr[i] > arr[i + 1]):
            hike[i] = hike[i + 1] + 1

    # For Type 4 employee
    for i in range(1, n + 1):
        if (arr[i - 1] < arr[i] and
            arr[i] > arr[i + 1]):
            hike[i] = max(hike[i - 1],
                          hike[i + 1]) + 1

    # Print the min hike for each employee
    for i in range(1, n + 1):
        print(hike[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given array of rating of employees
    arr = [ 5, 3, 4, 2, 1, 6 ]

    # Function Call
    findMinHike(arr, len(arr))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

static readonly int INF = 10000009;

// Function that print minimum hike
static void findMinHike(List<int> arr,
                        int n)
{
  // Insert INF at begin and
  // end of array
  arr.Insert(0, INF);
  arr.Add(INF);

  // To store hike of
  // each employee
  int []hike = new int[n + 2];

  // for Type 1 employee
  for (int i = 1; i <= n; i++)
  {
    if (arr[i - 1] >= arr[i] &&
        arr[i] <= arr[i + 1])
    {
      hike[i] = 1;
    }
  }

  // For Type 2 employee
  for (int i = 1; i <= n; i++)
  {
    if (arr[i - 1] < arr[i] &&
        arr[i] <= arr[i + 1])
    {
      hike[i] = hike[i - 1] + 1;
    }
  }

  // For Type 3 employee
  for (int i = 1; i <= n; i++)
  {
    if (arr[i - 1] >= arr[i] &&
        arr[i] > arr[i + 1])
    {
      hike[i] = hike[i + 1] + 1;
    }
  }

  // For Type 4 employee
  for (int i = 1; i <= n; i++)
  {
    if (arr[i - 1] < arr[i] &&
        arr[i] > arr[i + 1])
    {
      hike[i] = Math.Max(hike[i - 1],
                         hike[i + 1]) + 1;
    }
  }

  // Print the min hike for
  // each employee
  for (int i = 1; i <= n; i++)
  {
    Console.Write(hike[i] + " ");
  }
}

// Driver Code
public static void Main(String[] args)
{
  // Given array of rating of employees
  List<int> arr = new List<int>();

  arr.Add(5);
  arr.Add(3);
  arr.Add(4);
  arr.Add(2);
  arr.Add(1);
  arr.Add(6);

  // Function Call
  findMinHike(arr, arr.Count);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the
// above approach
let INF = 10000009;

// Function that print minimum hike
function findMinHike(arr, n)
{

    // Insert INF at begin and
  // end of array
  arr.unshift(INF);
  arr.push(INF);

  // To store hike of
  // each employee
  let hike = new Array(n + 2);

  // for Type 1 employee
  for (let i = 1; i <= n; i++)
  {
    if (arr[i-1] >= arr[i] &&
        arr[i] <= arr[i+1])
    {
      hike[i] = 1;
    }
  }

  // For Type 2 employee
  for (let i = 1; i <= n; i++)
  {
    if (arr[i - 1] < arr[i] &&
        arr[i] <= arr[i + 1])
    {
      hike[i] = hike[i - 1] + 1;
    }
  }

  // For Type 3 employee
  for (let i = 1; i <= n; i++)
  {
    if (arr[i-1] >= arr[i] &&
        arr[i] > arr[i+1])
    {
      hike[i] = hike[i + 1] + 1;
    }
  }

  // For Type 4 employee
  for (let i = 1; i <= n; i++)
  {
    if (arr[i-1] < arr[i] &&
        arr[i] > arr[i+1])
    {
      hike[i] = Math.max(hike[i - 1],
                         hike[i + 1]) + 1;
    }
  }

  // Print the min hike for each employee
  for (let i = 1; i <= n; i++)
  {
    document.write(hike[i] + " ");
  }
}

// Driver Code

// Given array of rating of employees
let arr = [5,3,4,2,1,6];

// Function Call
findMinHike(arr, arr.length);

// This code is contributed by unknown2108
</script>
```

**Output**

```
2 1 3 2 1 2 
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)

**接近 2:** (使用 2 个通道)

1.  首先给每个员工分配尽可能小的加薪，即 1
2.  现在我们不能根据相邻员工的加薪来减少当前的员工加薪，总是寻找增加的案例。
3.  Pass1(从左->右)与以前的员工加薪进行比较，如果需要，增加当前的员工加薪。
4.  Pass2(从右->左)与下一次员工加薪进行比较，如果需要，增加当前员工加薪。

下面是上述方法的实现:

## C++

```
// C++ program to find the minimum hike of each
// employee such that no adjacent employee feels
// unfair
#include <iostream>
using namespace std;

void findMinimumHike(int ratings[],int employees)
{
    int hikes[employees];

    // As hikes are positive integers, keeping
    // minimum value
    for(int i = 0; i < employees; i++)
    {
        hikes[i] = 1;
    }

    // Pass-1: compare with previous employee
    for(int i = 1; i < employees; i++)
    {
        if (ratings[i - 1] < ratings[i] &&
              hikes[i - 1] >= hikes[i])
        {
            hikes[i] = hikes[i - 1] + 1;
        }
    }

    // Pass-2: compare with Next employee
    for(int i = employees - 2; i >= 0; i--)
    {
        if (ratings[i] > ratings[i + 1] &&
              hikes[i + 1] >= hikes[i])
        {
            hikes[i] = hikes[i + 1] + 1;
        }
    }

    // Result
    cout << "[";
    int i;
    for(i = 0; i < employees - 1; i++)
    {
        cout << hikes[i] << ", ";
    }
    cout << hikes[i] << "]" << endl;
}

// Driver Code
int main()
{
    int data[] = { 5, 3, 4, 2, 1, 6 };

    // Function Call
    findMinimumHike(data, sizeof(data)/sizeof(data[0]));

    int data1[] = { 1, 3, 5, 4 };

    // Function Call
    findMinimumHike(data1, sizeof(data1)/sizeof(data1[0]));

    int data2[] = { 1, 4 };

    // Function Call
    findMinimumHike(data2, sizeof(data2)/sizeof(data2[0]));
    return 0;
}

// This code is contributed by rag2127
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum hike of each employee
// such that no adjacent employee feels unfair

import java.io.*;
import java.util.*;

class GFG {

    public static int[] findMinimumHike(int[] ratings,
                                        int employees)
    {
        int[] hikes = new int[employees];

        // As hikes are positive integers, keeping minimum
        // value
        for (int i = 0; i < employees; i++)
            hikes[i] = 1;

        // Pass-1: compare with previous employee
        for (int i = 1; i < employees; i++) {
            if (ratings[i - 1] < ratings[i]
                && hikes[i - 1] >= hikes[i])
                hikes[i] = hikes[i - 1] + 1;
        }

        // Pass-2: compare with Next employee
        for (int i = employees - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]
                && hikes[i + 1] >= hikes[i])
                hikes[i] = hikes[i + 1] + 1;
        }

        return hikes;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] data = new int[] { 5, 3, 4, 2, 1, 6 };

        // Function Call
        int[] result = findMinimumHike(data, data.length);
        // result -> [2, 1, 3, 2, 1, 2]
        System.out.println(Arrays.toString(result));

        data = new int[] { 1, 3, 5, 4 };

        // Function Call
        result = findMinimumHike(data, data.length);
        // result -> [1, 2, 3, 1]
        System.out.println(Arrays.toString(result));

        data = new int[] { 1, 4 };

        // Function Call
        result = findMinimumHike(data, data.length);
        // result -> [1, 2]
        System.out.println(Arrays.toString(result));
    }
}
```

## 蟒蛇 3

```
# Python Program to find the minimum hike of each employee
# such that no adjacent employee feels unfair
def findMinimumHike(ratings, employees):

    # As hikes are positive integers, keeping minimum
    # value
    hikes = [1 for i in range(employees)]

    # Pass-1: compare with previous employee
    for i in range(1,employees):
        if(ratings[i - 1] < ratings[i] and hikes[i - 1] >= hikes[i]):
            hikes[i] = hikes[i - 1] + 1;

    # Pass-2: compare with Next employee
    for i in range(employees - 2, -1, -1):
        if(ratings[i] > ratings[i + 1] and hikes[i + 1] >= hikes[i]):
            hikes[i] = hikes[i + 1] + 1;
    return hikes

# Driver Code
data = [ 5, 3, 4, 2, 1, 6 ]

# Function Call
result=findMinimumHike(data, len(data))

# result -> [2, 1, 3, 2, 1, 2]
print(result)
data = [1, 3, 5, 4 ]

# Function Call
result=findMinimumHike(data, len(data))

# result -> [1, 2, 3, 1]
print(result)
data = [1, 4]

# Function Call
result=findMinimumHike(data, len(data))

# result -> [1, 2]
print(result)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find the minimum hike
// of each employee such that no
// adjacent employee feels unfair
using System;

class GFG{

public static int[] findMinimumHike(int[] ratings,
                                    int employees)
{
    int[] hikes = new int[employees];

    // As hikes are positive integers, keeping
    // minimum value
    for(int i = 0; i < employees; i++)
        hikes[i] = 1;

    // Pass-1: compare with previous employee
    for(int i = 1; i < employees; i++)
    {
        if (ratings[i - 1] < ratings[i] &&
              hikes[i - 1] >= hikes[i])
            hikes[i] = hikes[i - 1] + 1;
    }

    // Pass-2: compare with Next employee
    for(int i = employees - 2; i >= 0; i--)
    {
        if (ratings[i] > ratings[i + 1] &&
              hikes[i + 1] >= hikes[i])
            hikes[i] = hikes[i + 1] + 1;
    }
    return hikes;
}

// Driver Code
public static void Main(String[] args)
{
    int[] data = new int[]{ 5, 3, 4, 2, 1, 6 };

    // Function Call
    int[] result = findMinimumHike(data, data.Length);

    // result -> [2, 1, 3, 2, 1, 2]
    Console.WriteLine("[" + String.Join(",", result) + "]");

    data = new int[]{ 1, 3, 5, 4 };

    // Function Call
    result = findMinimumHike(data, data.Length);

    // result -> [1, 2, 3, 1]
    Console.WriteLine("[" + String.Join(",", result) + "]");

    data = new int[]{ 1, 4 };

    // Function Call
    result = findMinimumHike(data, data.Length);
    // result -> [1, 2]
    Console.WriteLine("[" + String.Join(",", result) + "]");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript Program to find the minimum hike of each employee
// such that no adjacent employee feels unfair
function findMinimumHike(ratings, employees)
{
    let hikes = new Array(employees);

        // As hikes are positive integers, keeping minimum
        // value
        for (let i = 0; i < employees; i++)
            hikes[i] = 1;

        // Pass-1: compare with previous employee
        for (let i = 1; i < employees; i++)
        {
            if (ratings[i - 1] < ratings[i]
                && hikes[i - 1] >= hikes[i])
                hikes[i] = hikes[i - 1] + 1;
        }

        // Pass-2: compare with Next employee
        for (let i = employees - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]
                && hikes[i + 1] >= hikes[i])
                hikes[i] = hikes[i + 1] + 1;
        }

        return hikes;
}

 // Driver Code
let data = [5, 3, 4, 2, 1, 6];

// Function Call
let result = findMinimumHike(data, data.length);

 // result -> [2, 1, 3, 2, 1, 2]
document.write("["+(result).join(", ")+"]<br>");

data = [1, 3, 5, 4 ];

// Function Call
result = findMinimumHike(data, data.length);

// result -> [1, 2, 3, 1]
document.write("["+(result).join(", ")+"]<br>");
data = [1, 4 ];

// Function Call
result = findMinimumHike(data, data.length);

// result -> [1, 2]
document.write("["+(result).join(", ")+"]<br>");

// This code is contributed by patel2127
</script>
```

**Output**

```
[2, 1, 3, 2, 1, 2]
[1, 2, 3, 1]
[1, 2]
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)