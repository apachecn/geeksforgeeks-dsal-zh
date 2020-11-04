# 给定数组 A []和数字 x，请检查 A []中的对，且总和为 x

> 原文：[https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/)

编写一个程序，给定 n 个数字的数组 A []和另一个 x 的数组，确定 S 中是否存在两个元素的总和恰好是 x。

**示例**：

```
Input: arr[] = {0, -1, 2, -3, 1}
        sum = -2
Output: -3, 1
If we calculate the sum of the output,
1 + (-3) = -2

Input: arr[] = {1, -2, 1, 0, 5}
       sum = 0
Output: -1
No valid pair exists.

```

**方法 1 **：排序和两指针技术。

**方法**：解决此问题的棘手方法可以是使用两指针技术。 但是对于使用两个指针技术，必须对数组进行排序。 一旦对数组排序，就可以采用两个指针分别标记数​​组的开始和结束。 如果**的总和比这两个元素的总和大**，请向左移动指针以增加所需总和的值；如果**的总和比所需值小**，则向右移动 减小值的指针。 让我们通过一个例子来理解这一点。

> 令一个数组为{1、4、45、6、10，-8}并求和为 16
> 对数组进行排序后
> A = {-8、1、4、6、10、45}
> 现在，当对的总和小于所需的总和时，将'l'递增，而当对的总和大于所需的总和时，将'r'递减。
> 这是因为，当总和小于所需总和时，为了获得可以增加配对总和的数字，请从左向右移动（也对数组进行排序），从而“ l ++”，反之亦然。
> 初始化 l = 0，r = 5
> A [l] + A [r]（-8 + 45）> 16 = >递减 r。 现在 r = 4
> A [l] + A [r]（-8 + 10）增量 l。 现在 l = 1
> A [l] + A [r]（1 + 10）增量 l。 现在 l = 2
> A [l] + A [r]（4 + 10）递增 l。 现在 l = 3
> A [l] + A [r]（6 + 10）== 16 = >找到候选对象（返回 1）

**注意**：如果具有给定总和的一对以上，则此算法仅报告一个。 可以很容易地对此进行扩展。

**算法**：

1.  hasArrayTwoCandidates（A []​​，ar_size，sum）

2.  以非降序对数组进行排序。

3.  初始化两个索引变量以在排序数组中找到候选

    元素。

    1.  首先初始化到最左边的索引：l = 0

    2.  第二个初始化最右边的索引：r = ar_size-1

4.  当 l <r>1.  如果（A [l] + A [r] ==和），则返回 1

    2.  否则 if（A [l] + A [r]

    3.  其他 r–</r> 

5.  整个数组中没有候选者-返回 0

## C++

```cpp

// C++ program to check if given array
// has 2 elements whose sum is equal
// to the given value

#include <bits/stdc++.h>
using namespace std;

// Function to check if array has 2 elements
// whose sum is equal to the given value
bool hasArrayTwoCandidates(int A[], int arr_size,
                           int sum)
{
    int l, r;

    /* Sort the elements */
    sort(A, A + arr_size);

    /* Now look for the two candidates in 
       the sorted array*/
    l = 0;
    r = arr_size - 1;
    while (l < r) {
        if (A[l] + A[r] == sum)
            return 1;
        else if (A[l] + A[r] < sum)
            l++;
        else // A[i] + A[j] > sum
            r--;
    }
    return 0;
}

/* Driver program to test above function */
int main()
{
    int A[] = { 1, 4, 45, 6, 10, -8 };
    int n = 16;
    int arr_size = sizeof(A) / sizeof(A[0]);

    // Function calling
    if (hasArrayTwoCandidates(A, arr_size, n))
        cout << "Array has two elements"
                " with given sum";
    else
        cout << "Array doesn't have two"
                " elements with given sum";

    return 0;
}

```

## C

```c

// C program to check if given array
// has 2 elements whose sum is equal
// to the given value

#include <stdio.h>
#define bool int

void quickSort(int*, int, int);

bool hasArrayTwoCandidates(
    int A[], int arr_size, int sum)
{
    int l, r;

    /* Sort the elements */
    quickSort(A, 0, arr_size - 1);

    /* Now look for the two candidates in the sorted 
       array*/
    l = 0;
    r = arr_size - 1;
    while (l < r) {
        if (A[l] + A[r] == sum)
            return 1;
        else if (A[l] + A[r] < sum)
            l++;
        else // A[i] + A[j] > sum
            r--;
    }
    return 0;
}

/* FOLLOWING FUNCTIONS ARE ONLY FOR SORTING 
    PURPOSE */
void exchange(int* a, int* b)
{
    int temp;
    temp = *a;
    *a = *b;
    *b = temp;
}

int partition(int A[], int si, int ei)
{
    int x = A[ei];
    int i = (si - 1);
    int j;

    for (j = si; j <= ei - 1; j++) {
        if (A[j] <= x) {
            i++;
            exchange(&A[i], &A[j]);
        }
    }
    exchange(&A[i + 1], &A[ei]);
    return (i + 1);
}

/* Implementation of Quick Sort
A[] --> Array to be sorted
si  --> Starting index
ei  --> Ending index
*/
void quickSort(int A[], int si, int ei)
{
    int pi; /* Partitioning index */
    if (si < ei) {
        pi = partition(A, si, ei);
        quickSort(A, si, pi - 1);
        quickSort(A, pi + 1, ei);
    }
}

/* Driver program to test above function */
int main()
{
    int A[] = { 1, 4, 45, 6, 10, -8 };
    int n = 16;
    int arr_size = 6;

    if (hasArrayTwoCandidates(A, arr_size, n))
        printf("Array has two elements with given sum");
    else
        printf("Array doesn't have two elements with given sum");

    getchar();
    return 0;
}

```

## Java

```java

// Java program to check if given array
// has 2 elements whose sum is equal
// to the given value
import java.util.*;

class GFG {
    // Function to check if array has 2 elements
    // whose sum is equal to the given value
    static boolean hasArrayTwoCandidates(
        int A[],
        int arr_size, int sum)
    {
        int l, r;

        /* Sort the elements */
        Arrays.sort(A);

        /* Now look for the two candidates 
        in the sorted array*/
        l = 0;
        r = arr_size - 1;
        while (l < r) {
            if (A[l] + A[r] == sum)
                return true;
            else if (A[l] + A[r] < sum)
                l++;
            else // A[i] + A[j] > sum
                r--;
        }
        return false;
    }

    // Driver code
    public static void main(String args[])
    {
        int A[] = { 1, 4, 45, 6, 10, -8 };
        int n = 16;
        int arr_size = A.length;

        // Function calling
        if (hasArrayTwoCandidates(A, arr_size, n))
            System.out.println("Array has two "
                               + "elements with given sum");
        else
            System.out.println("Array doesn't have "
                               + "two elements with given sum");
    }
}

```

## 蟒蛇

```

# Python program to check for the sum 
# condition to be satisified

def hasArrayTwoCandidates(A, arr_size, sum):

    # sort the array
    quickSort(A, 0, arr_size-1)
    l = 0
    r = arr_size-1

    # traverse the array for the two elements
    while l<r:
        if (A[l] + A[r] == sum):
            return 1
        elif (A[l] + A[r] < sum):
            l += 1
        else:
            r -= 1
    return 0

# Implementation of Quick Sort
# A[] --> Array to be sorted
# si  --> Starting index
# ei  --> Ending index
def quickSort(A, si, ei):
    if si < ei:
        pi = partition(A, si, ei)
        quickSort(A, si, pi-1)
        quickSort(A, pi + 1, ei)

# Utility function for partitioning 
# the array(used in quick sort)
def partition(A, si, ei):
    x = A[ei]
    i = (si-1)
    for j in range(si, ei):
        if A[j] <= x:
            i += 1

            # This operation is used to swap 
            # two variables is python
            A[i], A[j] = A[j], A[i]

        A[i + 1], A[ei] = A[ei], A[i + 1]

    return i + 1

# Driver program to test the functions
A = [1, 4, 45, 6, 10, -8]
n = 16
if (hasArrayTwoCandidates(A, len(A), n)):
    print("Array has two elements with the given sum")
else:
    print("Array doesn't have two elements 
                                  with the given sum")

## This code is contributed by __Devesh Agrawal__

```

## C#

```cs

// C# program to check for pair
// in A[] with sum as x

using System;

class GFG {
    static bool hasArrayTwoCandidates(int[] A,
                       int arr_size, int sum)
    {
        int l, r;

        /* Sort the elements */
        sort(A, 0, arr_size - 1);

        /* Now look for the two candidates 
        in the sorted array*/
        l = 0;
        r = arr_size - 1;
        while (l < r) {
            if (A[l] + A[r] == sum)
                return true;
            else if (A[l] + A[r] < sum)
                l++;
            else // A[i] + A[j] > sum
                r--;
        }
        return false;
    }

    /* Below functions are only to sort the 
    array using QuickSort */

    /* This function takes last element as pivot,
    places the pivot element at its correct
    position in sorted array, and places all
    smaller (smaller than pivot) to left of
    pivot and all greater elements to right
    of pivot */
    static int partition(int[] arr, int low, int high)
    {
        int pivot = arr[high];

        // index of smaller element
        int i = (low - 1);
        for (int j = low; j <= high - 1; j++) {
            // If current element is smaller
            // than or equal to pivot
            if (arr[j] <= pivot) {
                i++;

                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and arr[high] (or pivot)
        int temp1 = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp1;

        return i + 1;
    }

    /* The main function that 
    implements QuickSort()
    arr[] --> Array to be sorted,
    low --> Starting index,
    high --> Ending index */
    static void sort(int[] arr, int low, int high)
    {
        if (low < high) {
            /* pi is partitioning index, arr[pi] 
            is now at right place */
            int pi = partition(arr, low, high);

            // Recursively sort elements before
            // partition and after partition
            sort(arr, low, pi - 1);
            sort(arr, pi + 1, high);
        }
    }

    // Driver code
    public static void Main()
    {
        int[] A = { 1, 4, 45, 6, 10, -8 };
        int n = 16;
        int arr_size = 6;

        if (hasArrayTwoCandidates(A, arr_size, n))
            Console.Write("Array has two elements"
                          + " with given sum");
        else
            Console.Write("Array doesn't have "
                          + "two elements with given sum");
    }
}

// This code is contributed by Sam007

```

## PHP

```php

<?php
// PHP program to check if given 
// array has 2 elements whose sum 
// is equal to the given value

// Function to check if array has 
// 2 elements whose sum is equal
// to the given value
function hasArrayTwoCandidates($A, $arr_size,
                                        $sum)
{
    $l; $r;

    /* Sort the elements */
    //sort($A, A + arr_size);
    sort($A);

    /* Now look for the two candidates 
    in the sorted array*/
    $l = 0;
    $r = $arr_size - 1; 
    while ($l < $r)
    {
        if($A[$l] + $A[$r] == $sum)
            return 1; 
        else if($A[$l] + $A[$r] < $sum)
            $l++;
        else // A[i] + A[j] > sum
            $r--;
    } 
    return 0;
}

// Driver Code
$A = array (1, 4, 45, 6, 10, -8);
$n = 16;
$arr_size = sizeof($A);

// Function calling
if(hasArrayTwoCandidates($A, $arr_size, $n))
    echo "Array has two elements " .
                   "with given sum";
else
    echo "Array doesn't have two " . 
          "elements with given sum";

// This code is contributed by m_kit
?>

```

**输出**：

```
Array has two elements with the given sum

```

**复杂度分析**：

*   **时间复杂度**：取决于我们使用哪种排序算法。

    *   如果使用合并排序或堆排序，则在最坏的情况下使用（-）（nlogn）。

    *   如果使用快速排序，则在最坏的情况下为`O(N ^ 2)`。

*   **辅助空间**：这也取决于排序算法。 辅助空间是用于合并排序的`O(n)`和用于堆排序的`O(1)`。

**方法 2 **：[散列](http://www.geeksforgeeks.org/hashing-data-structure/)。

**方法**：通过使用哈希技术可以有效解决此问题。 使用 **hash_map** 检查当前数组值 **x（let）**，如果存在值 **target_sum-x** ，则将其添加到前者后得出 **] target_sum** 。 这可以在恒定时间内完成。 让我们看下面的例子。

> arr [] = {0，-1，2，-3，1}
> sum = -2
> 现在开始遍历：
> 步骤 1：对于'0'，没有有效的数字'-2' 因此将“ 0”存储在 hash_map 中。
> 步骤 2：对于“ -1”，没有有效的数字“ -1”，因此请将“ -1”存储在 hash_map 中。
> 步骤 3：对于“ 2”，没有有效的数字“ -4”，因此将“ 2”存储在 hash_map 中。
> 步骤 4：对于“ -3”，没有有效的数字“ 1”，因此请将“ -3”存储在 hash_map 中。
> 步骤 5：对于“ 1”，有效数字为“ -3”，因此答案为 1，-3。

**算法**：

1.  初始化一个空的哈希表 s。

2.  对 A []中的每个元素 A [i]执行以下操作

    1.  如果设置了 s [x – A [i]]，则打印该对（A [i]，x – A [i]）

    2.  将 A [i]插入 s。

**伪代码**：

```
unordered_set s
for(i=0 to end)
  if(s.find(target_sum - arr[i]) == s.end)
    insert(arr[i] into s)
  else 
    print arr[i], target-arr[i]

```

## C++

```cpp

// C++ program to check if given array
// has 2 elements whose sum is equal
// to the given value
#include <bits/stdc++.h>

using namespace std;

void printPairs(int arr[], int arr_size, int sum)
{
    unordered_set<int> s;
    for (int i = 0; i < arr_size; i++) 
    {
        int temp = sum - arr[i];

        if (s.find(temp) != s.end())
            cout << "Pair with given sum "
                 << sum << " is (
                           " << arr[i] << ",
                " 
                    << temp << ")" << endl;

        s.insert(arr[i]);
    }
}

/* Driver Code */
int main()
{
    int A[] = { 1, 4, 45, 6, 10, 8 };
    int n = 16;
    int arr_size = sizeof(A) / sizeof(A[0]);

    // Function calling
    printPairs(A, arr_size, n);

    return 0;
}

```

## C

```c

// C++ program to check if given array
// has 2 elements whose sum is equal
// to the given value

// Works only if range elements is limited
#include <stdio.h>
#define MAX 100000

void printPairs(int arr[], int arr_size, int sum)
{
    int i, temp;

    /*initialize hash set as 0*/
    bool s[MAX] = { 0 };

    for (i = 0; i < arr_size; i++) 
    {
        temp = sum - arr[i];
        if (s[temp] == 1)
            printf(
                "Pair with given sum %d is (%d, %d) n",
                sum, arr[i], temp);
        s[arr[i]] = 1;
    }
}

/* Driver Code */
int main()
{
    int A[] = { 1, 4, 45, 6, 10, 8 };
    int n = 16;
    int arr_size = sizeof(A) / sizeof(A[0]);

    printPairs(A, arr_size, n);

    getchar();
    return 0;
}

```

## Java

```java

// Java implementation using Hashing
import java.io.*;
import java.util.HashSet;

class PairSum {
    static void printpairs(int arr[], int sum)
    {
        HashSet<Integer> s = new HashSet<Integer>();
        for (int i = 0; i < arr.length; ++i) 
        {
            int temp = sum - arr[i];

            // checking for condition
            if (s.contains(temp)) {
                System.out.println(
                    "Pair with given sum "
                    + sum + " is (" + arr[i]
                    + ", " + temp + ")");
            }
            s.add(arr[i]);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int A[] = { 1, 4, 45, 6, 10, 8 };
        int n = 16;
        printpairs(A, n);
    }
}

// This article is contributed by Aakash Hasija

```

## 蟒蛇

```

# Python program to find if there are
# two elements wtih given sum

# function to check for the given sum
# in the array
def printPairs(arr, arr_size, sum):

    # Create an empty hash set
    s = set()

    for i in range(0, arr_size):
        temp = sum-arr[i]
        if (temp in s):
            print "Pair with given sum "+ str(sum) +
       " is (" + str(arr[i]) + ", " + str(temp) + ")"
        s.add(arr[i])

# driver code
A = [1, 4, 45, 6, 10, 8]
n = 16
printPairs(A, len(A), n)

# This code is contributed by __Devesh Agrawal__

```

## C#

```cs

// C# implementation using Hashing
using System;
using System.Collections.Generic;

class GFG {
    static void printpairs(int[] arr,
                           int sum)
    {
        HashSet<int> s = new HashSet<int>();
        for (int i = 0; i < arr.Length; ++i) 
        {
            int temp = sum - arr[i];

            // checking for condition
            if (s.Contains(temp)) {
                Console.Write("Pair with given sum " + 
           sum + " is (" + arr[i] + ", " + temp + ")");
            }
            s.Add(arr[i]);
        }
    }

    // Driver Code
    static void Main()
    {
        int[] A = new int[] { 1, 4, 45,
                              6, 10, 8 };
        int n = 16;
        printpairs(A, n);
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)

```

**输出**：

```
Pair with given sum 16 is (10, 6)

```

**复杂度分析**：

*   **时间复杂度**：`O(n)`。

    由于整个数组仅需要遍历一次。

*   **辅助空间**：`O(n)`。

    由于哈希映射已用于存储数组元素。

**注意**：如果数字范围包含负数，则也可以正常工作。

https://www.youtube.com/watch?v=I7Nz1XzzPYc

**方法 3 **：使用小于 x 的元素的余数。

**方法**：

的想法是计算除以 x 的元素的余数，即 **0 到 x-1** ，每个余数分别计算。 假设我们将 **x 设为 6** ，则小于 6 且余数总计为 6 的数字相加后得出的总和为 6。 例如，我们在数组中有 2,4 个元素，2％6 = 2 和 4％6 = 4，这些余数加起来得到 6。这样，我们必须检查是否有余数对（1,5） ，（2,4），（3,3）。 如果我们有一个或多个元素的余数为 1 且一个或多个元素的余数为 5，则肯定得到的总和为 6。在这里，我们不考虑（0,6），因为结果对的元素应小于 6 。关于（3,3），我们必须检查是否有两个元素的余数为 3，那么我们可以说“存在一个对，其对为 x”。

**算法**：

```
1.create an array with size x. //rem[x]
2.initialize all rem elements to zero.
3\. traverse the given array
   3.1 do the following if arr[i] is less than x:
       3.1.1 r=arr[i]%x //get the remainder.
       3.1.2 rem[r]=rem[r]+1 // increasing the count of elements which have remainder r when divided with x.
4.Now, traverse the rem array form 1 to x/2.
   4.1 if(rem[i]> 0 and rem[x-i]>0) then print "YES" and come out of the loop. //This means that we have a pair which results in x upon dding.
5.Now when we reach at x/2 in above loop
   5.1 if x is even, // for getting a pair we should have two elements with remainder x/2\. 
       5.1.1 if rem[x/2]>1 then print "YES" else print "NO" 
   5.2 if 5.1 is not satisfied //that is x is odd, it will have a separate pair with x-x/2.
       5.2.1 if rem[x/2]>1 and rem[x-x/2]>1 , then print "Yes" else, print"No";

```

**上面的** **算法的实现**：

## CPP

```

// Code in cpp to tell if there 
// exists a pair in array whose
// sum results in x.
#include <iostream>
using namespace std;

// Funtion to print pairs
void printPairs(int a[], int n, int x)
{
      int i;
    int rem[x];
    for (i = 0; i < x; i++) 
    {

        // initializing the rem 
        // values with 0's.
        rem[i] = 0;
    }
    for (i = 0; i < n; i++) 
    {
        if (a[i] < x) 
        {

            // Perform the remainder 
            // operation only if the
            // element is x, as numbers 
            // greater than x can't
            // be used to get a sum x.
            // Updating the count of remainders.
            rem[a[i] % x]++;
        }
    }

    // Traversing the remainder list 
    // from start to middle to
    // find pairs
    for (i = 1; i < x / 2; i++) 
    {
        if (rem[i] > 0 && rem[x - i] > 0) 
        {

            // The elements with remainders 
            // i and x-i will
            // result to a sum of x. 
            // Once we get two
            // elements which add up to x , 
            // we print x and
            // break.
            cout << "Yes"
                 << "\n";
            break;
        }
    }

    // Once we reach middle of 
    // remainder array, we have to
    // do operations based on x.
    if (i >= x / 2) 
    {
        if (x % 2 == 0) 
        {
            if (rem[x / 2] > 1) 
            {

                // if x is even and 
                // we have more than 1
                // elements with remainder 
                // x/2, then we will
                // have two distinct elements 
                // which add up
                // to x. if we dont have 
                //more than 1
                // element, print "No".
                cout << "Yes"
                     << "\n";
            }
            else
            {
                cout << "No"
                     << "\n";
            }
        }
        else
        {

            // When x is odd we continue 
            // the same process
            // which we did in previous loop.
            if (rem[x / 2] > 0 && 
                  rem[x - x / 2] > 0)
            {
                cout << "Yes"
                     << "\n";
            }
            else
            {
                cout << "No"
                     << "\n";
            }
        }
    }
}

/* Driver Code */
int main()
{
    int A[] = { 1, 4, 45, 6, 10, 8 };
    int n = 16;
    int arr_size = sizeof(A) / sizeof(A[0]);

    // Function calling
    printPairs(A, arr_size, n);

    return 0;
}
// This article is contributed by Sai Sanjana Gudla

```

**Output**

```
Yes

```

**时间复杂度**：O（n + x）

**辅助空间**：O（x）

**相关问题**：

*   [给定两个未排序的数组，找到总和为 x 的所有对。](https://www.geeksforgeeks.org/given-two-unsorted-arrays-find-pairs-whose-sum-x/)

*   [具有给定总和的计数对](https://www.geeksforgeeks.org/count-pairs-with-given-sum/)

*   [计算所有差值等于 k 的不重复对](https://www.geeksforgeeks.org/count-pairs-difference-equal-k/)

如果您发现以上任何代码/算法不正确，或者找到其他解决相同问题的方法，请发表评论。

