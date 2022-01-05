# 将数组转换为简化形式|集合 3(二分搜索法)

> 原文:[https://www . geesforgeks . org/convert-a-array-to-reduced-form-set-3-binary-search/](https://www.geeksforgeeks.org/convert-an-array-to-reduced-form-set-3-binary-search/)

给定由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是将给定数组转换为前 N 个非负整数的序列，即**【0，N–1】**，使得元素的顺序相同，即 **0** 位于最小数组元素的索引处， **1** 位于第二小元素的索引处，依此类推。

**示例:**

> **输入:** arr[] = {10，40，20}
> **输出:** 0 2 1
> 
> **输入:** arr[] = {5，10，40，30，20 }
> T3】输出: 0 1 4 3 2

[**基于哈希的**](https://www.geeksforgeeks.org/hashing-data-structure/) **方法:**基于哈希的方法请参考本文的[集 1](https://www.geeksforgeeks.org/convert-an-array-to-reduced-form-set-1-simple-and-hashing/) 帖子。
***时间复杂度:**O(N * log N)*
***辅助空间:** O(N)*

[**对矢量**](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) **基进场:**使用[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)对[矢量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)进场，请参考本文[集 2](https://www.geeksforgeeks.org/convert-array-reduced-form-set-2-using-vector-pairs/) 帖。
***时间复杂度:**O(N * log N)*
***辅助空间:** O(N)*

[**【二分搜索法】**](https://www.geeksforgeeks.org/binary-search/)**——基于方法:**按照步骤解决问题:

*   初始化一个数组，说 **brr[]** 并将数组的所有元素 **arr[]** 存储到 **brr[]** 中。
*   [按升序排列数组**brr[]**](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)。
*   [遍历给定数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr[]** ，对于每个元素，即 **arr[i]** [，在数组 **brr[]** 中找到 **arr[i]** 的下界](https://www.geeksforgeeks.org/binary-search-functions-in-c-stl-binary_search-lower_bound-and-upper_bound/)，并打印 is 的索引作为当前元素的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the reduced form
// of the given array arr[]
void convert(int arr[], int n)
{
    // Stores the sorted form of the
    // the given array arr[]
    int brr[n];

    for (int i = 0; i < n; i++)
        brr[i] = arr[i];

    // Sort the array brr[]
    sort(brr, brr + n);

    // Traverse the given array arr[]
    for (int i = 0; i < n; i++) {

        int l = 0, r = n - 1, mid;

        // Perform the Binary Search
        while (l <= r) {

            // Calculate the value of
            // mid
            mid = (l + r) / 2;

            if (brr[mid] == arr[i]) {

                // Print the current
                // index and break
                cout << mid << ' ';
                break;
            }

            // Update the value of l
            else if (brr[mid] < arr[i]) {
                l = mid + 1;
            }

            // Update the value of r
            else {
                r = mid - 1;
            }
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 10, 20, 15, 12, 11, 50 };
    int N = sizeof(arr) / sizeof(arr[0]);
    convert(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG
{

    // Function to find the reduced form
    // of the given array arr[]
    static void convert(int arr[], int n)
    {

        // Stores the sorted form of the
        // the given array arr[]
        int brr[] = new int[n];

        for (int i = 0; i < n; i++)
            brr[i] = arr[i];

        // Sort the array brr[]
        Arrays.sort(brr);

        // Traverse the given array arr[]
        for (int i = 0; i < n; i++) {

            int l = 0, r = n - 1, mid;

            // Perform the Binary Search
            while (l <= r) {

                // Calculate the value of
                // mid
                mid = (l + r) / 2;

                if (brr[mid] == arr[i]) {

                    // Print the current
                    // index and break
                    System.out.print(mid + " ");
                    break;
                }

                // Update the value of l
                else if (brr[mid] < arr[i]) {
                    l = mid + 1;
                }

                // Update the value of r
                else {
                    r = mid - 1;
                }
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 10, 20, 15, 12, 11, 50 };
        int N = arr.length;
        convert(arr, N);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the reduced form
# of the given array arr[]
def convert(arr, n):

    # Stores the sorted form of the
    # the given array arr[]
    brr = [i for i in arr]

    # Sort the array brr[]
    brr = sorted(brr)

    # Traverse the given array arr[]
    for i in range(n):

        l, r, mid = 0, n - 1, 0

        # Perform the Binary Search
        while (l <= r):

            # Calculate the value of
            # mid
            mid = (l + r) // 2

            if (brr[mid] == arr[i]):

                # Print the current
                # index and break
                print(mid,end=" ")
                break
            # Update the value of l
            elif (brr[mid] < arr[i]):
                l = mid + 1
            # Update the value of r
            else:
                r = mid - 1

# Driver Code
if __name__ == '__main__':
    arr=[10, 20, 15, 12, 11, 50]
    N = len(arr)
    convert(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the reduced form
// of the given array arr[]
static void convert(int[] arr, int n)
{

    // Stores the sorted form of the
    // the given array arr[]
    int[] brr = new int[n];

    for(int i = 0; i < n; i++)
        brr[i] = arr[i];

    // Sort the array brr[]
    Array.Sort(brr);

    // Traverse the given array arr[]
    for(int i = 0; i < n; i++)
    {
        int l = 0, r = n - 1, mid;

        // Perform the Binary Search
        while (l <= r)
        {

            // Calculate the value of
            // mid
            mid = (l + r) / 2;

            if (brr[mid] == arr[i])
            {

                // Print the current
                // index and break
                Console.Write(mid + " ");
                break;
            }

            // Update the value of l
            else if (brr[mid] < arr[i])
            {
                l = mid + 1;
            }

            // Update the value of r
            else
            {
                r = mid - 1;
            }
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 10, 20, 15, 12, 11, 50 };
    int N = arr.Length;

    convert(arr, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to find the reduced form
// of the given array arr[]
function convert(arr, n)
{
    // Stores the sorted form of the
    // the given array arr[]
    var brr = Array(n).fill(0);
    var i;
    for (i = 0; i < n; i++)
        brr[i] = arr[i];

    // Sort the array brr[]
    brr.sort();

    // Traverse the given array arr[]
    for (i = 0; i < n; i++) {

        var l = 0, r = n - 1, mid;

        // Perform the Binary Search
        while (l <= r) {

            // Calculate the value of
            // mid
            mid = parseInt((l + r) / 2,10);

            if (brr[mid] == arr[i]) {

                // Print the current
                // index and break
                document.write(mid + ' ');
                break;
            }

            // Update the value of l
            else if (brr[mid] < arr[i]) {
                l = mid + 1;
            }

            // Update the value of r
            else {
                r = mid - 1;
            }
        }
    }
}

// Driver Code
    var arr = [10, 20, 15, 12, 11, 50];
    var N = arr.length;
    convert(arr, N);

// This code is contributed by SURENDRA_GANGWAR.
</script>
```

**Output:** 

```
0 4 3 2 1 5
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*