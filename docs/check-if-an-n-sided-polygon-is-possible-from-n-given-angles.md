# 从 N 个给定角度检查 N 边多边形是否可能

> 原文:[https://www . geesforgeks . org/check-an-n-side-polygon-从 n 个给定角度来看是否可能/](https://www.geeksforgeeks.org/check-if-an-n-sided-polygon-is-possible-from-n-given-angles/)

给定一个由 **N 个**元素组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中每个元素代表一个多边形的一个角度(以度为单位)，任务是检查是否可以用所有给定的角度制作一个 **N 边**多边形。如果可能，则打印**是**否则打印**否**。

**示例:**

> **输入:** N = 3，arr[] = {60，60，60}
> **输出:**是
> **说明:**存在满足上述角度的三角形(即多边形)。因此输出是“是”。
> 
> **输入:** N = 4，arr[] = {90，90，90，100}
> **输出:**否
> **说明:**不存在满足上述角度的多边形。因此输出为否

**方法:**只有当所有给定角度之和等于 **180*(N-2)** 时，才可能出现 **N 边**多边形。因此 ides 是求数组中所有给定角度的和**arr【】**，如果和等于 **180*(N-2)** 则打印 ***是*** ，否则打印 ***否*** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if the polygon
// exists or not
void checkValidPolygon(int arr[], int N)
{
    // Initialize a variable to
    // store the sum of angles
    int sum = 0;

    // Loop through the array and
    // calculate the sum of angles
    for (int i = 0; i < N; i++) {
        sum += arr[i];
    }

    // Check the condition for
    // an N-side polygon
    if (sum == 180 * (N - 2))
        cout << "Yes";
    else
        cout << "No";
}

// Driver Code
int main()
{
    int N = 3;

    // Given array arr[]
    int arr[] = { 60, 60, 60 };

    // Function Call
    checkValidPolygon(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if the polygon
// exists or not
static void checkValidPolygon(int arr[], int N)
{

    // Initialize a variable to
    // store the sum of angles
    int sum = 0;

    // Loop through the array and
    // calculate the sum of angles
    for(int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // Check the condition for
    // an N-side polygon
    if (sum == 180 * (N - 2))
        System.out.println("Yes");
    else
        System.out.println("No");
}

// Driver code
public static void main(String[] args)
{
    int N = 3;

    // Given array arr[]
    int arr[] = { 60, 60, 60 };

    // Function call
    checkValidPolygon(arr, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if the polygon
# exists or not
def checkValidPolygon(arr, N):

    # Initialize a variable to
    # store the sum of angles
    Sum = 0

    # Loop through the array and
    # calculate the sum of angles
    for i in range(N):
        Sum += arr[i]

    # Check the condition for
    # an N-side polygon
    if Sum == 180 * (N - 2):
        print("Yes")
    else:
        print("No")

# Driver Code
N = 3

# Given array arr[]
arr = [ 60, 60, 60 ]

# Function Call
checkValidPolygon(arr, N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the polygon
// exists or not
static void checkValidPolygon(int []arr, int N)
{

    // Initialize a variable to
    // store the sum of angles
    int sum = 0;

    // Loop through the array and
    // calculate the sum of angles
    for(int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // Check the condition for
    // an N-side polygon
    if (sum == 180 * (N - 2))
        Console.Write("Yes");
    else
        Console.Write("No");
}

// Driver code
public static void Main(string[] args)
{
    int N = 3;

    // Given array arr[]
    int []arr = { 60, 60, 60 };

    // Function call
    checkValidPolygon(arr, N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to check if the polygon
// exists or not
function checkValidPolygon(arr, N)
{

    // Initialize a variable to
    // store the sum of angles
    var sum = 0;

    // Loop through the array and
    // calculate the sum of angles
    for(var i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // Check the condition for
    // an N-side polygon
    if (sum == 180 * (N - 2))
        document.write("Yes");
    else
        document.write("No");
}

// Driver code
var N = 3;

// Given array arr[]
var arr = [ 60, 60, 60 ];

// Function call
checkValidPolygon(arr, N);

// This code is contributed by Kirti

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** *O(N)，其中 N 为数组长度。*
**辅助空间:** *O(1)*