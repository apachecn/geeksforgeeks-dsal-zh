# 重新排列数组，最大化局部最小值的个数

> 原文:[https://www . geeksforgeeks . org/rearray-array-to-maximum-count-local-minim/](https://www.geeksforgeeks.org/rearrange-array-to-maximize-count-of-local-minima/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是重新排列数组元素，使得数组中局部最小值的[计数最大。](https://www.geeksforgeeks.org/find-local-minima-array/)

**注意:**一个元素**arr【x】**如果小于或等于其相邻的两个元素，则称其为**局部最小值**。第一个和最后一个数组元素不能被认为是局部最小值。

**示例:**

> **输入:** arr[]= {1，2，3，4，5}
> **输出:** 3 1 4 2 5
> **解释:**
> 将数组元素重新排列为{3，1，4，2，5}。数组中局部极小值的个数为 2，即{arr[1]，arr[3]}，这是可以从数组中得到的局部极小值的最大可能个数。因此，所需的输出是 3 1 4 2 5。
> 
> **输入:** arr[]= {1，2，3，4，5，6 }
> T3】输出: 4 1 5 2 6 3

**方法:**思路是使用[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)和[两个指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)来解决这个问题。按照以下步骤解决此问题:

*   [按升序排列数组](https://www.geeksforgeeks.org/sort-c-stl/)。
*   初始化两个变量，说**左= 0** 和**右= N / 2** 分别存储左右指针的索引。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，每次遍历先打印 **arr【右】**的值，再打印 **arr【左】**的值，将**左**和**右**的值增加 **1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange array elements to
// maximize count of local minima in the array
void rearrangeArrMaxcntMinima(int arr[], int N)
{
    // Sort the array in
    // ascending order
    sort(arr, arr + N);

    // Stores index of
    // left pointer
    int left = 0;

    // Stores index of
    // right pointer
    int right = N / 2;

    // Traverse the array elements
    while (left < N / 2 || right < N) {

        // if right is less than N
        if (right < N) {

            // Print array element
            cout << arr[right] << " ";

            // Update right
            right++;
        }

        if (left < N / 2) {

            // Print array element
            cout << arr[left] << " ";

            // Update left
            left++;
        }
    }
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    rearrangeArrMaxcntMinima(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to rearrange array elements to
// maximize count of local minima in the array
static void rearrangeArrMaxcntMinima(int arr[],
                                     int N)
{

    // Sort the array in
    // ascending order
    Arrays.sort(arr);

    // Stores index of
    // left pointer
    int left = 0;

    // Stores index of
    // right pointer
    int right = N / 2;

    // Traverse the array elements
    while (left < N / 2 || right < N)
    {

        // If right is less than N
        if (right < N)
        {

            // Print array element
            System.out.print(arr[right] + " ");

            // Update right
            right++;
        }

        if (left < N / 2)
        {

            // Print array element
            System.out.print(arr[left] + " ");

            // Update left
            left++;
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };

    int N = arr.length;

    rearrangeArrMaxcntMinima(arr, N);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to rearrange array
# elements to maximize count of
# local minima in the array
def rearrangeArrMaxcntMinima(arr, N):

    # Sort the array in
    # ascending order
    arr.sort()

    # Stores index of
    # left pointer
    left = 0

    # Stores index of
    # right pointer
    right = N // 2

    # Traverse the array elements
    while (left < N // 2 or
           right < N):

        # if right is less
        # than N
        if (right < N):

            # Print array element
            print(arr[right],
                  end = " ")

            # Update right
            right += 1

        if (left < N // 2):

            # Print array element
            print(arr[left],
                  end = " ")

            # Update left
            left += 1

# Driver Code
if __name__ == "__main__":

    arr = [1, 2, 3, 4, 5]
    N = len(arr)
    rearrangeArrMaxcntMinima(arr, N)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to rearrange array elements to
// maximize count of local minima in the array
static void rearrangeArrMaxcntMinima(int []arr,
                                     int N)
{

    // Sort the array in
    // ascending order
    Array.Sort(arr);

    // Stores index of
    // left pointer
    int left = 0;

    // Stores index of
    // right pointer
    int right = N / 2;

    // Traverse the array elements
    while (left < N / 2 || right < N)
    {

        // If right is less than N
        if (right < N)
        {

            // Print array element
            Console.Write(arr[right] + " ");

            // Update right
            right++;
        }
        if (left < N / 2)
        {

            // Print array element
            Console.Write(arr[left] + " ");

            // Update left
            left++;
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int N = arr.Length;

    rearrangeArrMaxcntMinima(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to rearrange array elements to
// maximize count of local minima in the array
function rearrangeArrMaxcntMinima(arr, N)
{

    // Sort the array in
    // ascending order
    arr.sort(function(a, b){return a - b;});

    // Stores index of
    // left pointer
    let left = 0;

    // Stores index of
    // right pointer
    let right = Math.floor(N / 2);

    // Traverse the array elements
    while (left < Math.floor(N / 2) || right < N)
    {

        // If right is less than N
        if (right < N)
        {

            // Print array element
            document.write(arr[right] + " ");

            // Update right
            right++;
        }

        if (left < Math.floor(N / 2))
        {

            // Print array element
            document.write(arr[left] + " ");

            // Update left
            left++;
        }
    }
}

// Driver Code
let arr = [ 1, 2, 3, 4, 5 ];
let N = arr.length;

rearrangeArrMaxcntMinima(arr, N);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3 1 4 2 5
```

***时间复杂度:** O(N log(N))*
***辅助空间:** O(1)*