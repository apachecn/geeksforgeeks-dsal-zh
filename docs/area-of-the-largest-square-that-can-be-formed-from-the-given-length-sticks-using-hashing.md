# 使用散列法由给定长度的木棒形成的最大正方形的面积

> 原文:[https://www . geeksforgeeks . org/由给定长度的棒使用散列法形成的最大正方形面积/](https://www.geeksforgeeks.org/area-of-the-largest-square-that-can-be-formed-from-the-given-length-sticks-using-hashing/)

给定一个表示木棒高度的整数数组**arr[]****N**。任务是找到用这些木棒可以形成的最大正方形的面积，以及这些正方形的数量。**注意**正方形的单面只能用一根棍子。
**示例:**

> **输入:** arr[] = {5，3，2，3，6，3，3}
> **输出:**
> 面积= 9
> 计数= 1
> 正方形的边将为 3，
> 只有一个这样的正方形是可能的。
> **输入:** arr[] = {2，2，2，9，2，2，2，2，2}
> **输出:**
> 面积= 4
> 计数= 2

**方法:**统计数组所有元素的频率。现在，从最大值开始(为了最大化面积)，找到第一个频率，它至少是 4，这样就可以形成一个正方形，然后面积可以计算为 freq[i] * freq[i]，这样的正方形的计数将是 freq[i] / 4。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the area of the largest
// square that can be formed
// and the count of such squares
void findMaxSquare(int arr[], int n)
{

    // Maximum value from the array
    int maxVal = *max_element(arr, arr + n);

    // Update the frequencies of
    // the array elements
    int freq[maxVal + 1] = { 0 };
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Starting from the maximum length sticks
    // in order to maximize the area
    for (int i = maxVal; i > 0; i--) {

        // The count of sticks with the current
        // length has to be at least 4
        // in order to form a square
        if (freq[i] >= 4) {
            cout << "Area = " << (pow(i, 2));
            cout << "\nCount = " << (freq[i] / 4);
            return;
        }
    }

    // Impossible to form a square
    cout << "-1";
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 2, 9, 2, 2, 2, 2, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findMaxSquare(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the area of the largest
// square that can be formed
// and the count of such squares
static void findMaxSquare(int arr[], int n)
{

    // Maximum value from the array
    int maxVal = Arrays.stream(arr).max().getAsInt();

    // Update the frequencies of
    // the array elements
    int []freq = new int[maxVal + 1];
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Starting from the maximum length sticks
    // in order to maximize the area
    for (int i = maxVal; i > 0; i--)
    {

        // The count of sticks with the current
        // length has to be at least 4
        // in order to form a square
        if (freq[i] >= 4)
        {
            System.out.print("Area = " +
                            (Math.pow(i, 2)));
            System.out.print("\nCount = " +
                            (freq[i] / 4));
            return;
        }
    }

    // Impossible to form a square
    System.out.print("-1");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 2, 2, 9, 2, 2, 2, 2, 2 };
    int n = arr.length;

    findMaxSquare(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the area of the largest
# square that can be formed
# and the count of such squares
def findMaxSquare(arr, n) :

    # Maximum value from the array
    maxVal = max(arr);

    # Update the frequencies of
    # the array elements
    freq = [0] * (maxVal + 1) ;
    for i in range(n) :
        freq[arr[i]] += 1;

    # Starting from the maximum length sticks
    # in order to maximize the area
    for i in range(maxVal, 0, -1) :

        # The count of sticks with the current
        # length has to be at least 4
        # in order to form a square
        if (freq[i] >= 4) :
            print("Area = ", pow(i, 2));
            print("Count =", freq[i] // 4);
            return;

    # Impossible to form a square
    print("-1");

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 2, 2, 9, 2, 2, 2, 2, 2 ];
    n = len(arr);

    findMaxSquare(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

// Function to find the area of the largest
// square that can be formed
// and the count of such squares
static void findMaxSquare(int []arr, int n)
{

    // Maximum value from the array
    int maxVal = arr.Max();

    // Update the frequencies of
    // the array elements
    int []freq = new int[maxVal + 1];
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Starting from the maximum length sticks
    // in order to maximize the area
    for (int i = maxVal; i > 0; i--)
    {

        // The count of sticks with the current
        // length has to be at least 4
        // in order to form a square
        if (freq[i] >= 4)
        {
            Console.Write("Area = " +
                         (Math.Pow(i, 2)));
            Console.Write("\nCount = " +
                         (freq[i] / 4));
            return;
        }
    }

    // Impossible to form a square
    Console.Write("-1");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 2, 2, 9, 2, 2, 2, 2, 2 };
    int n = arr.Length;

    findMaxSquare(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the area of the largest
// square that can be formed
// and the count of such squares
function findMaxSquare(arr, n)
{

    // Maximum value from the array
    var maxVal = Math.max(...arr);

    // Update the frequencies of
    // the array elements
    var freq = Array(maxVal + 1).fill(0);
    for (var i = 0; i < n; i++)
        freq[arr[i]]++;

    // Starting from the maximum length sticks
    // in order to maximize the area
    for (var i = maxVal; i > 0; i--) {

        // The count of sticks with the current
        // length has to be at least 4
        // in order to form a square
        if (freq[i] >= 4) {
            document.write("Area = " + (Math.pow(i, 2)));
            document.write("<br>Count = " + (freq[i] / 4));
            return;
        }
    }

    // Impossible to form a square
    document.write("-1");
}

// Driver code
var arr = [ 2, 2, 2, 9, 2, 2, 2, 2, 2 ];
var n = arr.length;
findMaxSquare(arr, n);

</script>
```

**Output:** 

```
Area = 4
Count = 2
```

***时间复杂度:** O(n)*

***辅助空间:** O(n)*