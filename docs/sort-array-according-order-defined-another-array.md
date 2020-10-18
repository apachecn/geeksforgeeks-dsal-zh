# 根据另一个数组定义的顺序对数组进行排序

> 原文： [https://www.geeksforgeeks.org/sort-array-according-order-defined-another-array/](https://www.geeksforgeeks.org/sort-array-according-order-defined-another-array/)

给定两个数组`A1[]`和`A2[]`，对`A1`进行排序，以使元素之间的相对顺序与`A2`中的相对顺序相同。 对于`A2`中不存在的元素，最后按排序顺序附加它们。

**例如**：

```
 Input: A1[] = {2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8}
       A2[] = {2, 1, 8, 3}
Output: A1[] = {2, 2, 1, 1, 8, 8, 3, 5, 6, 7, 9}

```

该代码应处理所有情况，例如与`A1[]`相比，`A2[]`中的元素数量可能更多或更少。 `A2[]`可能包含`A1[]`中可能不存在的某些元素，反之亦然。

**来源**： [Amazon 面试 | 系列 110（校园内）](https://www.geeksforgeeks.org/amazon-interview-set-110-campus/)

[](https://practice.geeksforgeeks.org/problem-page.php?pid=434)

## 强烈建议您在继续解决方案之前，单击这里进行练习。

**方法 1（使用排序和二分搜索）**：

假设`A1[]`的大小为`m`，而`A2[]`的大小为`n`。

*   创建一个大小为`m`的临时数组`temp`，并将`A1[]`的内容复制到其中。

*   创建另一个访问过的数组，并将其中的所有条目初始化为`false`。 `visit[]`用于标记`temp[]`中复制到`A1[]`的那些元素。

*   排序`temp[]`。

*   将输出索引`ind`初始化为 0。

*   对`A2[]`中的每个元素`A2[i]`进行跟踪。

    *   二分搜索`temp[]`中所有出现的`A2[i]`（如果存在），然后将所有出现的内容复制到`A1[ind]`并递增`ind`。 还标记复制的元素`visit[]`。

*   将所有未访问的元素从`temp[]`复制到`A1[]`。

.

下图是上述方法的模拟：

![](img/e0a9a40010483842ee91568c4e78b46a.png)

下面是上述方法的实现：

## C++ 

```cpp

// A C++ program to sort an array according to the order defined 
// by another array 
#include <bits/stdc++.h> 
using namespace std; 

// A Binary Search based function to find index of FIRST occurrence 
// of x in arr[].  If x is not present, then it returns -1 

// The same can be done using the lower_bound 
// function in C++ STL 
int first(int arr[], int low, int high, int x, int n) 
{ 

    // Checking condition 
    if (high >= low) { 

        // FInd the mid element 
        int mid = low + (high - low) / 2; 

        // Check if the element is the extreme left 
        // in the left half of the array 
        if ((mid == 0 || x > arr[mid - 1]) && arr[mid] == x) 
            return mid; 

        // If the element lies on the right half 
        if (x > arr[mid]) 
            return first(arr, (mid + 1), high, x, n); 

        // Check for element in the left half 
        return first(arr, low, (mid - 1), x, n); 
    } 

    // ELement not found 
    return -1; 
} 

// Sort A1[0..m-1] according to the order defined by A2[0..n-1]. 
void sortAccording(int A1[], int A2[], int m, int n) 
{ 
    // The temp array is used to store a copy of A1[] and visited[] 
    // is used mark the visited elements in temp[]. 
    int temp[m], visited[m]; 
    for (int i = 0; i < m; i++) { 
        temp[i] = A1[i]; 
        visited[i] = 0; 
    } 

    // Sort elements in temp 
    sort(temp, temp + m); 

    // for index of output which is sorted A1[] 
    int ind = 0; 

    // Consider all elements of A2[], find them in temp[] 
    // and copy to A1[] in order. 
    for (int i = 0; i < n; i++) { 
        // Find index of the first occurrence of A2[i] in temp 
        int f = first(temp, 0, m - 1, A2[i], m); 

        // If not present, no need to proceed 
        if (f == -1) 
            continue; 

        // Copy all occurrences of A2[i] to A1[] 
        for (int j = f; (j < m && temp[j] == A2[i]); j++) { 
            A1[ind++] = temp[j]; 
            visited[j] = 1; 
        } 
    } 

    // Now copy all items of temp[] 
    // which are not present in A2[] 
    for (int i = 0; i < m; i++) 
        if (visited[i] == 0) 
            A1[ind++] = temp[i]; 
} 

// Utility function to print an array 
void printArray(int arr[], int n) 
{ 

    // Iterate in the array 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
    cout << endl; 
} 

// Driver Code 
int main() 
{ 
    int A1[] = { 2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8 }; 
    int A2[] = { 2, 1, 8, 3 }; 
    int m = sizeof(A1) / sizeof(A1[0]); 
    int n = sizeof(A2) / sizeof(A2[0]); 

    // Prints the sorted array 
    cout << "Sorted array is \n"; 
    sortAccording(A1, A2, m, n); 
    printArray(A1, m); 
    return 0; 
} 

```

## Java

```java
// A JAVA program to sort an array according
// to the order defined by another array
import java.io.*;
import java.util.Arrays;
 
class GFG {
 
    /* A Binary Search based function to find
    index of FIRST occurrence of x in arr[].
    If x is not present, then it returns -1 */
    static int first(int arr[], int low, int high,
                     int x, int n)
    {
        if (high >= low) {
            /* (low + high)/2; */
            int mid = low + (high - low) / 2;
 
            if ((mid == 0 || x > arr[mid - 1]) && arr[mid] == x)
                return mid;
            if (x > arr[mid])
                return first(arr, (mid + 1), high,
                             x, n);
            return first(arr, low, (mid - 1), x, n);
        }
        return -1;
    }
 
    // Sort A1[0..m-1] according to the order
    // defined by A2[0..n-1].
    static void sortAccording(int A1[], int A2[], int m,
                              int n)
    {
        // The temp array is used to store a copy
        // of A1[] and visited[] is used to mark the
        // visited elements in temp[].
        int temp[] = new int[m], visited[] = new int[m];
        for (int i = 0; i < m; i++) {
            temp[i] = A1[i];
            visited[i] = 0;
        }
 
        // Sort elements in temp
        Arrays.sort(temp);
 
        // for index of output which is sorted A1[]
        int ind = 0;
 
        // Consider all elements of A2[], find them
        // in temp[] and copy to A1[] in order.
        for (int i = 0; i < n; i++) {
            // Find index of the first occurrence
            // of A2[i] in temp
            int f = first(temp, 0, m - 1, A2[i], m);
 
            // If not present, no need to proceed
            if (f == -1)
                continue;
 
            // Copy all occurrences of A2[i] to A1[]
            for (int j = f; (j < m && temp[j] == A2[i]);
                 j++) {
                A1[ind++] = temp[j];
                visited[j] = 1;
            }
        }
 
        // Now copy all items of temp[] which are
        // not present in A2[]
        for (int i = 0; i < m; i++)
            if (visited[i] == 0)
                A1[ind++] = temp[i];
    }
 
    // Utility function to print an array
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }
 
    // Driver program to test above function.
    public static void main(String args[])
    {
        int A1[] = { 2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8 };
        int A2[] = { 2, 1, 8, 3 };
        int m = A1.length;
        int n = A2.length;
        System.out.println("Sorted array is ");
        sortAccording(A1, A2, m, n);
        printArray(A1, m);
    }
}
 
/*This code is contributed by Nikita Tiwari.*/
```

## Python3

```py
"""A Python 3  program to sort an array 
according to the order defined by 
another array"""
 
"""A Binary Search based function to find 
index of FIRST occurrence of x in arr[].
If x is not present, then it returns -1 """
 
def first(arr, low, high, x, n) :
    if (high >= low) :
        mid = low + (high - low) // 2;  # (low + high)/2; 
        if ((mid == 0 or x > arr[mid-1]) and arr[mid] == x) :
            return mid
        if (x > arr[mid]) :
            return first(arr, (mid + 1), high, x, n)
        return first(arr, low, (mid -1), x, n)
         
    return -1
     
# Sort A1[0..m-1] according to the order
# defined by A2[0..n-1].
def sortAccording(A1, A2, m, n) :
   
    """The temp array is used to store a copy
    of A1[] and visited[] is used mark the 
    visited elements in temp[]."""
    temp = [0] * m
    visited = [0] * m
     
    for i in range(0, m) :
        temp[i] = A1[i]
        visited[i] = 0
  
    # Sort elements in temp
    temp.sort()
     
    # for index of output which is sorted A1[]
    ind = 0   
  
    """Consider all elements of A2[], find
    them in temp[] and copy to A1[] in order."""
    for i in range(0, n) :
         
        # Find index of the first occurrence
        # of A2[i] in temp
        f = first(temp, 0, m-1, A2[i], m)
  
        # If not present, no need to proceed
        if (f == -1) :
            continue
  
        # Copy all occurrences of A2[i] to A1[]
        j = f
        while (j<m and temp[j]== A2[i]) :
            A1[ind] = temp[j];
            ind = ind + 1
            visited[j] = 1
            j = j + 1
     
    # Now copy all items of temp[] which are
    # not present in A2[]
    for i in range(0, m) :
        if (visited[i] == 0) :
            A1[ind] = temp[i]
            ind = ind + 1
             
# Utility function to print an array
def printArray(arr, n) :
    for i in range(0, n) :
        print(arr[i], end = " ")
    print("")
     
  
# Driver program to test above function.
A1 = [2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8]
A2 = [2, 1, 8, 3]
m = len(A1)
n = len(A2)
print("Sorted array is ")
sortAccording(A1, A2, m, n)
printArray(A1, m)
 
 
# This code is contributed by Nikita Tiwari.
```

## C#

```cs
// A C# program to sort an array according
// to the order defined by another array
using System;
 
class GFG {
 
    /* A Binary Search based function to find
    index of FIRST occurrence of x in arr[].
    If x is not present, then it returns -1 */
    static int first(int[] arr, int low,
                     int high, int x, int n)
    {
        if (high >= low) {
            /* (low + high)/2; */
            int mid = low + (high - low) / 2;
 
            if ((mid == 0 || x > arr[mid - 1]) && arr[mid] == x)
                return mid;
            if (x > arr[mid])
                return first(arr, (mid + 1), high,
                             x, n);
            return first(arr, low, (mid - 1), x, n);
        }
        return -1;
    }
 
    // Sort A1[0..m-1] according to the order
    // defined by A2[0..n-1].
    static void sortAccording(int[] A1, int[] A2,
                              int m, int n)
    {
 
        // The temp array is used to store a copy
        // of A1[] and visited[] is used to mark
        // the visited elements in temp[].
        int[] temp = new int[m];
        int[] visited = new int[m];
 
        for (int i = 0; i < m; i++) {
            temp[i] = A1[i];
            visited[i] = 0;
        }
 
        // Sort elements in temp
        Array.Sort(temp);
 
        // for index of output which is
        // sorted A1[]
        int ind = 0;
 
        // Consider all elements of A2[], find
        // them in temp[] and copy to A1[] in
        // order.
        for (int i = 0; i < n; i++) {
 
            // Find index of the first occurrence
            // of A2[i] in temp
            int f = first(temp, 0, m - 1, A2[i], m);
 
            // If not present, no need to proceed
            if (f == -1)
                continue;
 
            // Copy all occurrences of A2[i] to A1[]
            for (int j = f; (j < m && temp[j] == A2[i]); j++) {
                A1[ind++] = temp[j];
                visited[j] = 1;
            }
        }
 
        // Now copy all items of temp[] which are
        // not present in A2[]
        for (int i = 0; i < m; i++)
            if (visited[i] == 0)
                A1[ind++] = temp[i];
    }
 
    // Utility function to print an array
    static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
        Console.WriteLine();
    }
 
    // Driver program to test above function.
    public static void Main()
    {
        int[] A1 = { 2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8 };
        int[] A2 = { 2, 1, 8, 3 };
        int m = A1.Length;
        int n = A2.Length;
        Console.WriteLine("Sorted array is ");
        sortAccording(A1, A2, m, n);
        printArray(A1, m);
    }
}
 
// This code is contributed by nitin mittal.
```

## PHP

```php
<?php 
// A PHP program to sort an array according 
// to the order defined by another array
 
/* A Binary Search based function to find index 
of FIRST occurrence of x in arr[]. If x is not 
present, then it returns -1 */
function first(&$arr, $low, $high, $x, $n)
{
    if ($high >= $low)
    {
        $mid = intval($low + ($high - $low) / 2); 
        if (($mid == 0 || $x > $arr[$mid - 1]) && 
                               $arr[$mid] == $x)
            return $mid;
        if ($x > $arr[$mid])
            return first($arr, ($mid + 1), $high, $x, $n);
        return first($arr, $low, ($mid - 1), $x, $n);
    }
    return -1;
}
 
// Sort A1[0..m-1] according to the order 
// defined by A2[0..n-1].
function sortAccording(&$A1, &$A2, $m, $n)
{
    // The temp array is used to store a copy 
    // of A1[] and visited[] is used mark the
    // visited elements in temp[].
    $temp = array_fill(0, $m, NULL);
    $visited = array_fill(0, $m, NULL);
    for ($i = 0; $i < $m; $i++)
    {
        $temp[$i] = $A1[$i];
        $visited[$i] = 0;
    }
 
    // Sort elements in temp
    sort($temp);
 
    $ind = 0; // for index of output which is sorted A1[]
 
    // Consider all elements of A2[], find 
    // them in temp[] and copy to A1[] in order.
    for ($i = 0; $i < $n; $i++)
    {
        // Find index of the first occurrence
        // of A2[i] in temp
        $f = first($temp, 0, $m - 1, $A2[$i], $m);
 
        // If not present, no need to proceed
        if ($f == -1) continue;
 
        // Copy all occurrences of A2[i] to A1[]
        for ($j = $f; ($j < $m && 
             $temp[$j] == $A2[$i]); $j++)
        {
            $A1[$ind++] = $temp[$j];
            $visited[$j] = 1;
        }
    }
 
    // Now copy all items of temp[] which
    // are not present in A2[]
    for ($i = 0; $i < $m; $i++)
        if ($visited[$i] == 0)
            $A1[$ind++] = $temp[$i];
}
 
// Utility function to print an array
function printArray(&$arr, $n)
{
    for ($i = 0; $i < $n; $i++)
        echo $arr[$i] . " ";
    echo "\n";
}
 
// Driver Code
$A1 = array(2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8);
$A2 = array(2, 1, 8, 3);
$m = sizeof($A1);
$n = sizeof($A2);
echo "Sorted array is \n";
sortAccording($A1, $A2, $m, $n);
printArray($A1, $m);
 
// This code is contributed by ita_c
?>
```

输出：

```
Sorted array is 
2 2 1 1 8 8 3 5 6 7 9 
```

时间复杂度：步骤 1 和 2 需要`O(m)`时间。 步骤 3 需要`O(M * Log M)`时间。 步骤 5 需要`O(N Log M)`时间。 因此，总体时间复杂度为`O(M Log M + N Log M)`。

感谢 vivek 提出了这种方法。

方法 2（使用自平衡二进制搜索树）：

我们还可以使用自平衡 BST，例如 AVL 树，红黑树等。以下是详细步骤。

+   为`A1[]`中的所有元素创建一个自平衡 BST。 在 BST 的每个节点中，还应跟踪密钥和访问的`bool`字段的出现次数，该字段对于所有节点均初始化为`false`。
+   将输出索引`ind`初始化为 0。
+   对`A2[]`中`A2[i]`的每个元素进行跟踪
+   在 BST 中搜索`A2[i]`（如果存在），然后将所有匹配项复制到`A1[ind]`，并递增`ind`。 还标记在 BST 节点中访问的复制元素。
+   进行 BST 的有序遍历，并将所有未访问的密钥复制到`A1[]`。

此方法的时间复杂度与以前的方法相同。 请注意，在自平衡二进制搜索树中，所有操作都需要`logm`时间。

方法 3（使用哈希）：

+   遍历`A1[]`，将每个数字的计数存储在`HashMap`中（键：数字，值：数字计数）
+   遍历`A2[]`，检查它是否存在于`HashMap`中，如果存在，则将其放置在输出数组中多次，并从`HashMap`中删除该数字。
+   对`HashMap`中存在的其余数字进行排序，并放入输出数组中。

感谢 Anurag Sigh 提出了这种方法。

下面是上述方法的实现：

## Python3

```py
from collections import Counter
 
# Function to sort arr1 
# according to arr2
def solve(arr1, arr2):
    # Our output array
    res = []
     
    # Counting Frequency of each
    # number in arr1
    f = Counter(arr1)
     
    # Iterate over arr2 and append all 
    # occurences of element of
    # arr2 from arr1
    for e in arr2:
       
        # Appending element 'e', 
        # f[e] number of times
        res.extend([e]*f[e])
         
        # Count of 'e' after appending is zero
        f[e] = 0
         
    # Remaining numbers in arr1 in sorted 
    # order (Numbers with non-zero frequency)
    rem = list(sorted(filter(
      lambda x: f[x] != 0, f.keys())))
     
    # Append them also
    for e in rem:
        res.extend([e]*f[e])
         
    return res
 
 
# Driver Code
if __name__ == "__main__":
    arr1 = [2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8]
    arr2 = [2, 1, 8, 3]
    print(*solve(arr1, arr2))
```

输出：

```
2 2 1 1 8 8 3 5 6 7 9
```

假设我们有一个良好的哈希函数，平均插入和搜索花费`O(1)`时间，则步骤 1 和 2 平均花费`O(m + n)`时间。第三步花费`O(p Log p)`时间，其中`p`是考虑`A2[]`的元素后剩余的元素数。

方法 4（通过编写自定义的比较方法）：

我们也可以定制排序算法的比较方法来解决上述问题。例如，C 语言中的`qsort()`允许我们传递自己的自定义比较方法。

+   如果`num1`和`num2`都在`A2`中，则`A2`中具有较低索引的数字将被视为比其他数字小。
+   如果`A2`中仅存在`num1`或`num2`中的一个，则该数字将被处理成小于`A2`中不存在的另一个数字。
+   如果两者都不在`A2`中，则采用自然排序。

如果我们使用`O(nLogn)`时间复杂度排序算法，则此方法的时间复杂度为`O(mnLogm)`。通过使用散列而不是进行线性搜索，我们可以将时间复杂度提高到`O(mLogm)`。

下面是上述方法的实现：

## C

```c
// A C++ program to sort an array according to the order defined
// by another array
#include <stdio.h>
#include <stdlib.h>
 
// A2 is made global here so that it can be accesed by compareByA2()
// The syntax of qsort() allows only two parameters to compareByA2()
int A2[5];
 
// size of A2[]
int size = 5;
 
int search(int key)
{
    int i = 0, idx = 0;
    for (i = 0; i < size; i++)
        if (A2[i] == key)
            return i;
    return -1;
}
 
// A custom comapre method to compare elements of A1[] according
// to the order defined by A2[].
int compareByA2(const void* a, const void* b)
{
    int idx1 = search(*(int*)a);
    int idx2 = search(*(int*)b);
    if (idx1 != -1 && idx2 != -1)
        return idx1 - idx2;
    else if (idx1 != -1)
        return -1;
    else if (idx2 != -1)
        return 1;
    else
        return (*(int*)a - *(int*)b);
}
 
// This method mainly uses qsort to sort A1[] according to A2[]
void sortA1ByA2(int A1[], int size1)
{
    qsort(A1, size1, sizeof(int), compareByA2);
}
 
// Driver program to test above function
int main(int argc, char* argv[])
{
    int A1[] = { 2, 1, 2, 5, 7, 1, 9, 3, 6, 8, 8, 7, 5, 6, 9, 7, 5 };
 
    // A2[] = {2, 1, 8, 3, 4};
    A2[0] = 2;
    A2[1] = 1;
    A2[2] = 8;
    A2[3] = 3;
    A2[4] = 4;
    int size1 = sizeof(A1) / sizeof(A1[0]);
 
    sortA1ByA2(A1, size1);
 
    printf("Sorted Array is ");
    int i;
    for (i = 0; i < size1; i++)
        printf("%d ", A1[i]);
    return 0;
}
```

输出：

```
Sorted Array is 2 2 1 1 8 8 3 5 5 5 6 6 7 7 7 9 9 
```

该方法基于读者的评论（Xinuo Chen，Pranay Doshi 和 javakurious），并由 Anurag Singh 编写。