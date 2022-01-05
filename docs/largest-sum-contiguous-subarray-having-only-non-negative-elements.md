# 只有非负元素的最大和连续子阵列

> 原文:[https://www . geesforgeks . org/maximum-sum-continuous-subarray-with-non-negative-elements/](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray-having-only-non-negative-elements/)

给定一个整数数组 **arr[]** ，任务是找到非负元素的最大和邻接子数组并返回其和。

**示例:**

> **输入:** arr[] = {1，4，-3，9，5，-6}
> **输出:** 14
> **说明:**
> 子阵【9，5】是所有非负元素之和最大的子阵。
> 
> **输入:** arr[] = {12，0，10，3，11 }
> T3】输出: 36

**天真方法:**
最简单的方法是在遍历子阵列并计算每个有效子阵列的和并更新最大和的同时，生成所有只有非负元素的子阵列。

***时间复杂度:** O(N^2)*

**高效方法:**
为了优化上述方法，遍历数组，对于遇到的每个非负元素，继续计算总和。对于遇到的每个负元素，在与当前总和进行比较后更新最大总和。将总和重置为 0，并继续下一个元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return Largest Sum Contiguous
// Subarray having non-negative number
int maxNonNegativeSubArray(int A[], int N)
{

    // Length of given array
    int l = N;

    int sum = 0, i = 0;
    int Max = -1;

    // Traversing array
    while (i < l)
    {

        // Increment i counter to avoid
        // negative elements
        while (i < l && A[i] < 0)
        {
            i++;
            continue;
        }

        // Calculating sum of contiguous
        // subarray of non-negative
        // elements
        while (i < l && 0 <= A[i])
        {
            sum += A[i++];

            // Update the maximum sum
            Max = max(Max, sum);
        }

        // Reset sum
        sum = 0;
    }

    // Return the maximum sum
    return Max;
}

// Driver code
int main()
{
    int arr[] = { 1, 4, -3, 9, 5, -6 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxNonNegativeSubArray(arr, N);
    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG {

    // Function to return Largest Sum Contiguous
    // Subarray having non-negative number
    static int maxNonNegativeSubArray(int[] A)
    {
        // Length of given array
        int l = A.length;

        int sum = 0, i = 0;

        int max = -1;

        // Traversing array
        while (i < l) {

            // Increment i counter to avoid
            // negative elements
            while (i < l && A[i] < 0) {
                i++;
                continue;
            }

            // Calculating sum of contiguous
            // subarray of non-negative
            // elements
            while (i < l && 0 <= A[i]) {

                sum += A[i++];

                // Update the maximum sum
                max = Math.max(max, sum);
            }

            // Reset sum
            sum = 0;
        }

        // Return the maximum sum
        return max;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] arr = { 1, 4, -3, 9, 5, -6 };

        System.out.println(maxNonNegativeSubArray(
            arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to return Largest Sum Contiguous
# Subarray having non-negative number
def maxNonNegativeSubArray(A, N):

    # Length of given array
    l = N

    sum = 0
    i = 0
    Max = -1

    # Traversing array
    while (i < l):

        # Increment i counter to avoid
        # negative elements
        while (i < l and A[i] < 0):
            i += 1
            continue

        # Calculating sum of contiguous
        # subarray of non-negative
        # elements
        while (i < l and 0 <= A[i]):
            sum += A[i]
            i += 1

            # Update the maximum sum
            Max = max(Max, sum)

        # Reset sum
        sum = 0;

    # Return the maximum sum
    return Max

# Driver code
arr = [ 1, 4, -3, 9, 5, -6 ]

# Length of array
N = len(arr)

print(maxNonNegativeSubArray(arr, N))

# This code is contributed by sanjoy_62   
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to return Largest Sum Contiguous
// Subarray having non-negative number
static int maxNonNegativeSubArray(int[] A)
{

    // Length of given array
    int l = A.Length;

    int sum = 0, i = 0;
    int max = -1;

    // Traversing array
    while (i < l)
    {

        // Increment i counter to avoid
        // negative elements
        while (i < l && A[i] < 0)
        {
            i++;
            continue;
        }

        // Calculating sum of contiguous
        // subarray of non-negative
        // elements
        while (i < l && 0 <= A[i])
        {
            sum += A[i++];

            // Update the maximum sum
            max = Math.Max(max, sum);
        }

        // Reset sum
        sum = 0;
    }

    // Return the maximum sum
    return max;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 4, -3, 9, 5, -6 };

    Console.Write(maxNonNegativeSubArray(arr));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to return Largest Sum Contiguous
// Subarray having non-negative number
function maxNonNegativeSubArray(A, N)
{

    // Length of given array
    var l = N;

    var sum = 0, i = 0;
    var Max = -1;

    // Traversing array
    while (i < l)
    {

        // Increment i counter to avoid
        // negative elements
        while (i < l && A[i] < 0)
        {
            i++;
            continue;
        }

        // Calculating sum of contiguous
        // subarray of non-negative
        // elements
        while (i < l && 0 <= A[i])
        {
            sum += A[i++];

            // Update the maximum sum
            Max = Math.max(Max, sum);
        }

        // Reset sum
        sum = 0;
    }

    // Return the maximum sum
    return Max;
}

// Driver code
var arr = [1, 4, -3, 9, 5, -6];
var N = arr.length;
document.write( maxNonNegativeSubArray(arr, N));

// This code is contributed by famously.
</script>
```

**Output**

```
14
```

***时间复杂度:O(N)***

***辅助空间:O(1)***

#### 更简单的方法:这种方法的思想是，当我们每次添加元素时，总和应该增加。如果没有，那么我们遇到了一个负值，总和会更小。

## C++

```
#include <iostream>

using namespace std;

int main()
{
    int arr[] = { 1, 4, -3, 9, 5, -6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int max_so_far = 0, max_right_here = 0;
    int start = 0, end = 0, s = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] < 0) {
            s = i + 1;
            max_right_here = 0;
        }
        else {
            max_right_here += arr[i];
        }

        if (max_right_here > max_so_far) {
            max_so_far = max_right_here;
            start = s;
            end = i;
        }
    }

    cout << ("Sub Array : ");
    for (int i = start; i <= end; i++) {
        cout << arr[i] << " ";
    }

    cout << endl;
    cout << "Largest Sum : " << max_so_far;
}

// This code is contributed by SoumikMondal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG
{

public static void main(String[] args)
{
    int arr[] = { 1, 4, -3, 9, 5, -6 };
    int n = arr.length;
    int max_so_far = 0, max_right_here = 0;
    int start = 0, end = 0, s = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] < 0) {
            s = i + 1;
            max_right_here = 0;
        }
        else {
            max_right_here += arr[i];
        }

        if (max_right_here > max_so_far) {
            max_so_far = max_right_here;
            start = s;
            end = i;
        }
    }

    System.out.print("Sub Array : ");
    for (int i = start; i <= end; i++) {
        System.out.print( arr[i]);
        System.out.print(" ");
    }
    System.out.println();
    System.out.print("Largest Sum : ");
    System.out.print( max_so_far);
}

}

// This code is contributed by amreshkumar3.
```

## java 描述语言

```
<script>

let arr = [ 1, 4, -3, 9, 5, -6 ];
let n = arr.length;
let max_so_far = 0, max_right_here = 0;
let start = 0, end = 0, s = 0;
for(let i = 0; i < n; i++)
{
    if (arr[i] < 0)
    {
        s = i + 1;
        max_right_here = 0;
    }
    else
    {
        max_right_here += arr[i];
    }

    if (max_right_here > max_so_far)
    {
        max_so_far = max_right_here;
        start = s;
        end = i;
    }
}

// Driver code
document.write("Sub Array : ");
for(let i = start; i <= end; i++)
{
    document.write(arr[i] + " ");
}

document.write("<br>");
document.write("Largest Sum : " + max_so_far);

// This code is contributed by Potta Lokesh

</script>
```

## 蟒蛇 3

```
arr = [1, 4, -3, 9, 5, -6]
n = len(arr)
max_so_far = 0
max_right_here = 0
start = 0
end = 0
s = 0
for i in range(0, n):
    if arr[i] < 0:
        s = i + 1
        max_right_here = 0
    else:
        max_right_here += arr[i]

    if max_right_here > max_so_far:
        max_so_far = max_right_here
        start = s
        end = i

print("Sub Array : ")
for i in range(start, end + 1):
    print(arr[i], end=" ")
print()
print("largest sum=", max_so_far)

# This code is contributed by amreshkumar3.
```

**Output**

```
Sub Array : 9 5 
Largest Sum : 14
```

**时间复杂度:O(n)**

**空间复杂度:O(1)**