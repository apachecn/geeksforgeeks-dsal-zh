# 使用循环排序

对包含 0(N)中 1 到 N 个值的数组进行排序

> 原文:[https://www . geeksforgeeks . org/sort-a-array-其中包含 1 到 n 个值-on-on-use-cycle-sort/](https://www.geeksforgeeks.org/sort-an-array-which-contain-1-to-n-values-in-on-using-cycle-sort/)

**先决条件:** [循环排序](https://www.geeksforgeeks.org/cycle-sort/)
给定一个从 **1 到 N** 的元素的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[**，任务是在 **O(N)** 时间内对给定数组进行排序。
**示例:**

> **输入:** arr[] = { 2，1，5，4，3}
> **输出:** 1 2 3 4 5
> **解释:**
> 既然 arr[0] = 2 不在正确位置，那么用 arr[arr[0]–1]
> 交换 arr[0]，现在数组变成:arr[] = {1，2，5，4，3}
> 现在 arr[2] = 5 不在正确位置，那么用 arr 交换 arr[2]
> **输入:** arr[] = {1，2，3，4，5，6}
> **输出:** 1 2 3 4 5 6
> **解释:**
> 数组已经排序。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 。
*   如果当前元素不在正确的位置，即 **arr[i]不等于 i+1** ，则[用具有正确位置的元素替换](https://www.geeksforgeeks.org/swap-two-variables-in-one-line-in-c-c-python-php-and-java/)当前元素。
    **例如:**

> 让 arr[] = {2，1，4，5，3}
> 因为，arr[0] = 2，它不在正确的位置 1。
> 然后用它的正确位置交换这个元素，即交换(arr[0]，arr[2-1])
> 然后数组变成:arr[] = {1，2，4，5，3}

*   如果当前元素在正确的位置，那么检查下一个元素。
*   重复以上步骤，直到我们到达数组的末尾。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to swap two a & b value
void swap(int* a, int* b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Function to print array element
void printArray(int arr[], int N)
{

    // Traverse the array
    for (int i = 0; i < N; i++) {
        cout << arr[i] << ' ';
    }
}

// Function to sort the array in O(N)
void sortArray(int arr[], int N)
{

    // Traverse the array
    for (int i = 0; i < N;) {

        // If the current element is
        // at correct position
        if (arr[i] == i + 1) {
            i++;
        }

        // Else swap the current element
        // with it's correct position
        else {
            swap(&arr[i], &arr[arr[i] - 1]);
        }
    }
}

// Driver Code
int main()
{

    int arr[] = { 2, 1, 5, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to sort the array
    sortArray(arr, N);

    // Function call to print the array
    printArray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class Main{

// Function to print array element
public static void printArray(int arr[], int N)
{

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
       System.out.print(arr[i] + " ");
    }
}

// Function to sort the array in O(N)
public static void sortArray(int arr[], int N)
{

    // Traverse the array
    for(int i = 0; i < N;)
    {

       // If the current element is
       // at correct position
       if (arr[i] == i + 1)
       {
           i++;
       }

       // Else swap the current element
       // with it's correct position
       else
       {
           // Swap the value of
           // arr[i] and arr[arr[i]-1]
           int temp1 = arr[i];
           int temp2 = arr[arr[i] - 1];
           arr[i] = temp2;
           arr[temp1 - 1] = temp1;
       }
    }
}

// Driver Code   
public static void main(String[] args)
{
    int arr[] = { 2, 1, 5, 3, 4 };
    int N = arr.length;

    // Function call to sort the array
    sortArray(arr, N);

    // Function call to print the array
    printArray(arr, N);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print array element
def printArray(arr, N):

    # Traverse the array
    for i in range(N):
        print(arr[i], end = ' ')

# Function to sort the array in O(N)
def sortArray(arr, N):

    i = 0

    # Traverse the array
    while i < N:

        # If the current element is
        # at correct position
        if arr[i] == i + 1:
            i += 1

        # Else swap the current element
        # with it's correct position
        else:

            # Swap the value of
            # arr[i] and arr[arr[i]-1]
            temp1 = arr[i]
            temp2 = arr[arr[i] - 1]
            arr[i] = temp2
            arr[temp1 - 1] = temp1

# Driver code
if __name__=='__main__':

    arr = [ 2, 1, 5, 3, 4 ]
    N = len(arr)

    # Function call to sort the array
    sortArray(arr, N)

    # Function call to print the array
    printArray(arr, N)

# This code is contributed by rutvik_56   
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to print array element
public static void printArray(int []arr, int N)
{   
    // Traverse the array
    for(int i = 0; i < N; i++)
    {
       Console.Write(arr[i] + " ");
    }
}

// Function to sort the array in O(N)
public static void sortArray(int []arr, int N)
{
    // Traverse the array
    for(int i = 0; i < N; )
    {
       // If the current element is
       // at correct position
       if (arr[i] == i + 1)
       {
           i++;
       }

       // Else swap the current element
       // with it's correct position
       else
       {
           // Swap the value of
           // arr[i] and arr[arr[i]-1]
           int temp1 = arr[i];
           int temp2 = arr[arr[i] - 1];
           arr[i] = temp2;
           arr[temp1 - 1] = temp1;
       }
    }
}

// Driver Code   
public static void Main(String[] args)
{
    int []arr = {2, 1, 5, 3, 4};
    int N = arr.Length;

    // Function call to sort the array
    sortArray(arr, N);

    // Function call to print the array
    printArray(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print array element
function printArray(arr, N)
{

    // Traverse the array
    for (var i = 0; i < N; i++) {
        document.write( arr[i] + ' ');
    }
}

// Function to sort the array in O(N)
function sortArray(arr, N)
{

    // Traverse the array
    for (var i = 0; i < N;) {

        // If the current element is
        // at correct position
        if (arr[i] == i + 1) {
            i++;
        }

        // Else swap the current element
        // with it's correct position
        else {
            var temp1 = arr[i];
           var temp2 = arr[arr[i] - 1];
           arr[i] = temp2;
           arr[temp1 - 1] = temp1;
        }
    }
}

// Driver Code
var arr =  [ 2, 1, 5, 3, 4 ];
var N = arr.length;

// Function call to sort the array
sortArray(arr, N);

// Function call to print the array
printArray(arr, N);

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
1 2 3 4 5
```

***时间复杂度:** O(N)* ，其中 N 为数组长度。
***辅助空间:** O(1)*