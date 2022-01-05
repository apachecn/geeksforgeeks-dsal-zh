# 给定数组按降序-最低-升序排序

> 原文:[https://www . geesforgeks . org/sort-given-array-to-降序-最低-升序-form/](https://www.geeksforgeeks.org/sort-given-array-to-descending-lowest-ascending-form/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是[对数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，使得数组的第一个 **K** 元素按降序排列，数组的最后一个**N–K**元素按升序排列。

**示例:**

> **输入:** arr[]= {7，6，8，9，0，1，2，2，1，8，9，6，7}，K = 6
> **输出:**9 8 8 7 7 0 1 2 2 6
> **解释:**
> 排序数组的前 K (= 6)个元素为{9，9，8，8，7，7}，按降序排列。
> 排序数组的最后 N–K(= 6)个元素为{0，1，1，2，2，6，6}，按升序排列。
> 因此，需要的输出是 9 9 8 8 7 0 1 2 2 6 6
> 
> **输入:** arr[]= {65，34，54，56，75，34，54，65，56，75，15}，K = 5
> **输出:** 75 75 65 65 56 56 15 34 34 54 54

**方法:**按照以下步骤解决问题:

*   [按降序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   [按升序排列数组的最后**(N–K)**元素](https://www.geeksforgeeks.org/sort-c-stl/)。
*   [打印数组](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to sort first K array elements in
// descending and last N - K in ascending order
void sortArrayInDescAsc(int arr[], int N, int K)
{
    // Sort the array in descending order
    sort(arr, arr + N, greater<int>());

    // Sort last (N - K) array
    // elements in ascending order
    sort(arr + K, arr + N);

    // Print array elements
    for (int i = 0; i < N; i++) {
        cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 7, 6, 8, 9, 0, 1, 2,
                  2, 1, 8, 9, 6, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 6;
    sortArrayInDescAsc(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to sort first K array elements in
// descending and last N - K in ascending order
static void sortArrayInDescAsc(int arr[], int N,
                               int K)
{

    // Sort the array in descending order
    Arrays.sort(arr);

    for(int i = 0, j = N - 1; i < N / 2; i++)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        j--;
    }

    // Sort last (N - K) array
    // elements in ascending order
    Arrays.sort(arr, K, N);

    // Print array elements
    for(int i = 0; i < N; i++)
    {
        System.out.print(arr[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 7, 6, 8, 9, 0, 1, 2,
                  2, 1, 8, 9, 6, 7 };
    int N = arr.length;
    int K = 6;

    sortArrayInDescAsc(arr, N, K);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to sort first K array
# elements in descending and last
# N - K in ascending order
def sortArrayInDescAsc(arr, N, K):

    # Sort the array in descending order
    arr = sorted(arr)
    arr = arr[::-1]

    # Sort last (N - K) array
    # elements in ascending order
    for i in arr[:K]:
        print(i, end = " ")
    for i in reversed(arr[K:]):
        print(i, end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 7, 6, 8, 9, 0, 1,
            2, 2, 1, 8, 9, 6, 7 ]
    N = len(arr)
    K = 6

    sortArrayInDescAsc(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to sort first K array elements in
// descending and last N - K in ascending order
static void sortArrayInDescAsc(int[] arr, int N,
                               int K)
{

    // Sort the array in descending order
    Array.Sort(arr);
    Array.Reverse(arr);

    // Sort last (N - K) array
    // elements in ascending order
    int temp = 0;

    for(int i = K; i < N; i++)
    {
        for(int j = i + 1; j < N; j++)
        {    
            if (arr[i] > arr[j])
            {
                temp = arr[i];   
                arr[i] = arr[j];   
                arr[j] = temp;   
            }    
        }    
    }

    // Print array elements
    for(int i = 0; i < N; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver code
public static void Main()
{
    int[] arr = { 7, 6, 8, 9, 0, 1, 2,
                  2, 1, 8, 9, 6, 7 };
    int N = arr.Length;
    int K = 6;

    sortArrayInDescAsc(arr, N, K);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to sort first K array elements in
// descending and last N - K in ascending order
function sortArrayInDescAsc(arr, N, K)
{
    // Sort the array in descending order
    arr.sort((b,a)=> a-b)

    var temp = 0;

    for(var i = K; i < N; i++)
    {
        for(var j = i + 1; j < N; j++)
        {    
            if (arr[i] > arr[j])
            {
                temp = arr[i];   
                arr[i] = arr[j];   
                arr[j] = temp;   
            }    
        }    
    }

    // Print array elements
    arr.forEach(element => {
        document.write(element+" ");
    });
}

// Driver Code
var arr = [7, 6, 8, 9, 0, 1, 2,
              2, 1, 8, 9, 6, 7 ];
var N = arr.length;
var K = 6;
sortArrayInDescAsc(arr, N, K);

//This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
9 9 8 8 7 7 0 1 1 2 2 6 6
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*