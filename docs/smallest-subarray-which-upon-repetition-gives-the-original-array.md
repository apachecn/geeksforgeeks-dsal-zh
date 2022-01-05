# 重复时给出原始阵列的最小子阵列

> 原文:[https://www . geeksforgeeks . org/minist-subarray-它在重复时给出原始数组/](https://www.geeksforgeeks.org/smallest-subarray-which-upon-repetition-gives-the-original-array/)

给定一个由 **N 个**整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到大小至少为 2 的最小[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/) **brr[]** ，从而通过对数组 **brr[]** 执行重复运算，得到原始数组 **arr[]** 。如果找不到这样的子阵列，打印**-1”**。

> 一个数组上的**重复操作**就是将该数组的所有当前元素再次追加到同一个数组中。
> **例如**，如果一个数组 **arr[] = {1，2}** 那么在重复操作时数组变成 **{1，2，1，2}** 。

**示例:**

> **输入:** arr[] = {1，2，3，3，1，2，3，3}
> **输出:** {1，2，3，3}
> **解释:**
> {1，2，3，3，3}是最小的子阵列，重复 2 次就得到原始阵列{1，2，3，3，1，2，3，3}
> 
> **输入:** arr[] = {1，1，6，1，1，7}
> **输出:** -1
> **说明:**
> 不存在任何子阵。

**天真方法:**想法是[生成所有可能的长度至少为 2 的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并检查重复这些子阵列是否给出原始阵列。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法可以通过观察结果子阵列 **brr[]** 必须从原始阵列的第一个索引开始，以在重复时生成 **arr[]** 来优化。因此，只生成那些从第一个索引开始且长度至少为 2 的子阵列，并检查重复这些子阵列是否给出原始阵列。以下是步骤:

1.  创建一个辅助数组 **brr[]** ，并将原始数组的前两个元素插入其中，因为结果数组的大小必须至少为两个。
2.  遍历子阵列**【2，N/2+1】**的可能长度，并检查重复时长度为 **i** 的阵列 **brr[]** 是否给出原始阵列 **arr[]** 。
3.  如果是，那么打印这个子阵列，并打破循环。
4.  否则，将当前元素插入子阵列并再次检查。
5.  重复上述步骤，直到检查完所有子阵列。
6.  如果没有找到数组 **brr[]** ，则打印“-1”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <vector>
using namespace std;

// Function to print the array
void printArray(vector<int>& brr)
{
    for (auto& it : brr) {
        cout << it << ' ';
    }
}

// Function to find the smallest subarray
void RepeatingSubarray(int arr[], int N)
{
    // Corner Case
    if (N < 2) {
        cout << "-1";
    }

    // Initialize the auxiliary subarray
    vector<int> brr;

    // Push the first 2 elements into
    // the subarray brr[]
    brr.push_back(arr[0]);
    brr.push_back(arr[1]);

    // Iterate over the length of
    // subarray
    for (int i = 2; i < N / 2 + 1; i++) {

        // If array can be divided into
        // subarray of i equal length
        if (N % i == 0) {

            bool a = false;
            int n = brr.size();
            int j = i;

            // Check if on repeating the
            // current subarray gives the
            // original array or not
            while (j < N) {
                int K = j % i;
                if (arr[j] == brr[K]) {
                    j++;
                }
                else {
                    a = true;
                    break;
                }
            }

            // Subarray found
            if (!a && j == N) {
                printArray(brr);
                return;
            }
        }

        // Add current element into
        // subarray
        brr.push_back(arr[i]);
    }

    // No subarray found
    cout << "-1";
    return;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 2, 1, 2,
                  2, 1, 2, 2 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    RepeatingSubarray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print the array
static void printArray(Vector<Integer> brr)
{
    for(int it : brr)
    {
        System.out.print(it + " ");
    }
}

// Function to find the smallest subarray
static void RepeatingSubarray(int arr[], int N)
{

    // Corner Case
    if (N < 2)
    {
        System.out.print("-1");
    }

    // Initialize the auxiliary subarray
    Vector<Integer> brr = new Vector<Integer>();

    // Push the first 2 elements into
    // the subarray brr[]
    brr.add(arr[0]);
    brr.add(arr[1]);

    // Iterate over the length of
    // subarray
    for(int i = 2; i < N / 2 + 1; i++)
    {

        // If array can be divided into
        // subarray of i equal length
        if (N % i == 0)
        {
            boolean a = false;
            int n = brr.size();
            int j = i;

            // Check if on repeating the
            // current subarray gives the
            // original array or not
            while (j < N)
            {
                int K = j % i;
                if (arr[j] == brr.get(K))
                {
                    j++;
                }
                else
                {
                    a = true;
                    break;
                }
            }

            // Subarray found
            if (!a && j == N)
            {
                printArray(brr);
                return;
            }
        }

        // Add current element into
        // subarray
        brr.add(arr[i]);
    }

    // No subarray found
    System.out.print("-1");
    return;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 1, 2,
                  2, 1, 2, 2 };

    int N = arr.length;

    // Function call
    RepeatingSubarray(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the array
def printArray(brr):

    for it in brr:
        print(it, end = ' ')

# Function to find the smallest subarray
def RepeatingSubarray(arr, N):

    # Corner Case
    if (N < 2):
        print("-1")

    # Initialize the auxiliary subarray
    brr = []

    # Push the first 2 elements into
    # the subarray brr[]
    brr.append(arr[0])
    brr.append(arr[1])

    # Iterate over the length of
    # subarray
    for i in range(2, N // 2 + 1):

        # If array can be divided into
        # subarray of i equal length
        if (N % i == 0):
            a = False
            n = len(brr)
            j = i

            # Check if on repeating the
            # current subarray gives the
            # original array or not
            while (j < N):
                K = j % i

                if (arr[j] == brr[K]):
                    j += 1
                else:
                    a = True
                    break

            # Subarray found
            if (not a and j == N):
                printArray(brr)
                return

        # Add current element into
        # subarray
        brr.append(arr[i])

    # No subarray found
    print("-1")
    return

# Driver Code
if __name__ =="__main__":

    arr = [ 1, 2, 2, 1, 2,
            2, 1, 2, 2 ]

    N = len(arr)

    # Function call
    RepeatingSubarray(arr, N)

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to print the array
static void printArray(List<int> brr)
{
    foreach(int it in brr)
    {
        Console.Write(it + " ");
    }
}

// Function to find the smallest subarray
static void RepeatingSubarray(int []arr, int N)
{   
    // Corner Case
    if (N < 2)
    {
        Console.Write("-1");
    }

    // Initialize the auxiliary subarray
    List<int> brr = new List<int>();

    // Push the first 2 elements into
    // the subarray brr[]
    brr.Add(arr[0]);
    brr.Add(arr[1]);

    // Iterate over the length of
    // subarray
    for(int i = 2; i < N / 2 + 1; i++)
    {       
        // If array can be divided into
        // subarray of i equal length
        if (N % i == 0)
        {
            bool a = false;
            int n = brr.Count;
            int j = i;

            // Check if on repeating the
            // current subarray gives the
            // original array or not
            while (j < N)
            {
                int K = j % i;
                if (arr[j] == brr[K])
                {
                    j++;
                }
                else
                {
                    a = true;
                    break;
                }
            }

            // Subarray found
            if (!a && j == N)
            {
                printArray(brr);
                return;
            }
        }

        // Add current element into
        // subarray
        brr.Add(arr[i]);
    }

    // No subarray found
    Console.Write("-1");
    return;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {1, 2, 2, 1,
                 2, 2, 1, 2, 2};

    int N = arr.Length;

    // Function call
    RepeatingSubarray(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to print the array
function printArray(brr)
{
    for (let it of brr) {
        document.write(it + ' ');
    }
}

// Function to find the smallest subarray
function RepeatingSubarray(arr, N)
{
    // Corner Case
    if (N < 2) {
        document.write("-1");
    }

    // Initialize the auxiliary subarray
    let brr = [];

    // Push the first 2 elements into
    // the subarray brr[]
    brr.push(arr[0]);
    brr.push(arr[1]);

    // Iterate over the length of
    // subarray
    for (let i = 2; i < Math.floor(N / 2) + 1; i++) {

        // If array can be divided into
        // subarray of i equal length
        if (N % i == 0) {

            let a = false;
            let n = brr.length;
            let j = i;

            // Check if on repeating the
            // current subarray gives the
            // original array or not
            while (j < N) {
                let K = j % i;
                if (arr[j] == brr[K]) {
                    j++;
                }
                else {
                    a = true;
                    break;
                }
            }

            // Subarray found
            if (!a && j == N) {
                printArray(brr);
                return;
            }
        }

        // Add current element into
        // subarray
        brr.push(arr[i]);
    }

    // No subarray found
    document.write("-1");
    return;
}

// Driver Code
    let arr = [ 1, 2, 2, 1, 2,
                2, 1, 2, 2 ];

    let N = arr.length;

    // Function call
    RepeatingSubarray(arr, N);

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
1 2 2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*