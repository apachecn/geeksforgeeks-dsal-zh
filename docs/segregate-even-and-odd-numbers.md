# 隔离偶数和奇数

> 原文:[https://www . geeksforgeeks . org/隔离偶数和奇数/](https://www.geeksforgeeks.org/segregate-even-and-odd-numbers/)

给定一个数组 A[]，编写一个分离偶数和奇数的函数。函数应该把所有偶数放在第一位，然后是奇数。

**示例:**

```
Input  = {12, 34, 45, 9, 8, 90, 3}
Output = {12, 34, 8, 90, 45, 9, 3}
```

在输出中，数字的顺序可以改变，即在上面的例子中，34 可以在 12 之前，3 可以在 9 之前。

这个问题和我们以前的帖子[很像，把 0 和 1 分隔成一个数组](https://www.geeksforgeeks.org/segregate-0s-and-1s-in-an-array-by-traversing-array-once/)，这两个问题都是著名的[荷兰国旗问题](http://www.csse.monash.edu.au/~lloyd/tildeAlgDS/Sort/Flag/)的变种。

```
Algorithm: segregateEvenOdd()
1) Initialize two index variables left and right:  
            left = 0,  right = size -1 
2) Keep incrementing left index until we see an even number.
3) Keep decrementing right index until we see an odd number.
4) If left < right then swap arr[left] and arr[right]
```

**实施:**

## C++

```
// C++ program to segregate even and odd elements of array
#include <iostream>
using namespace std;

/* Function to swap *a and *b */
void swap(int *a, int *b);

void segregateEvenOdd(int arr[], int size)
{
    /* Initialize left and right indexes */
    int left = 0, right = size-1;
    while (left < right)
    {
        /* Increment left index while we see 0 at left */
        while (arr[left] % 2 == 0 && left < right)
            left++;

        /* Decrement right index while we see 1 at right */
        while (arr[right] % 2 == 1 && left < right)
            right--;

        if (left < right)
        {
            /* Swap arr[left] and arr[right]*/
            swap(&arr[left], &arr[right]);
            left++;
            right--;
        }
    }
}

/* UTILITY FUNCTIONS */
void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

/* Driver code */
int main()
{
    int arr[] = {12, 34, 45, 9, 8, 90, 3};
    int arr_size = sizeof(arr)/sizeof(arr[0]);
    int i = 0;

    segregateEvenOdd(arr, arr_size);

    cout <<"Array after segregation ";
    for (i = 0; i < arr_size; i++)
        cout << arr[i] << " ";

    return 0;
}

// This code is contributed by shubhamsingh10
```

## C

```
// C program to segregate even and odd elements of array
#include<stdio.h>

/* Function to swap *a and *b */
void swap(int *a, int *b);

void segregateEvenOdd(int arr[], int size)
{
    /* Initialize left and right indexes */
    int left = 0, right = size-1;
    while (left < right)
    {
        /* Increment left index while we see 0 at left */
        while (arr[left]%2 == 0 && left < right)
            left++;

        /* Decrement right index while we see 1 at right */
        while (arr[right]%2 == 1 && left < right)
            right--;

        if (left < right)
        {
            /* Swap arr[left] and arr[right]*/
            swap(&arr[left], &arr[right]);
            left++;
            right--;
        }
    }
}

/* UTILITY FUNCTIONS */
void swap(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

/* driver program to test */
int main()
{
    int arr[] = {12, 34, 45, 9, 8, 90, 3};
    int arr_size = sizeof(arr)/sizeof(arr[0]);
    int i = 0;

    segregateEvenOdd(arr, arr_size);

    printf("Array after segregation ");
    for (i = 0; i < arr_size; i++)
        printf("%d ", arr[i]);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to segregate even and odd elements of array
import java.io.*;

class SegregateOddEven
{
    static void segregateEvenOdd(int arr[])
    {
        /* Initialize left and right indexes */
        int left = 0, right = arr.length - 1;
        while (left < right)
        {
            /* Increment left index while we see 0 at left */
            while (arr[left]%2 == 0 && left < right)
                left++;

            /* Decrement right index while we see 1 at right */
            while (arr[right]%2 == 1 && left < right)
                right--;

            if (left < right)
            {
                /* Swap arr[left] and arr[right]*/
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;
                left++;
                right--;
            }
        }
    }

    /* Driver program to test above functions */
    public static void main (String[] args)
    {
        int arr[] = {12, 34, 45, 9, 8, 90, 3};

        segregateEvenOdd(arr);

        System.out.print("Array after segregation ");
        for (int i = 0; i < arr.length; i++)
            System.out.print(arr[i]+" ");
    }
}
/*This code is contributed by Devesh Agrawal*/
```

## 计算机编程语言

```
# Python program to segregate even and odd elements of array

def segregateEvenOdd(arr):

    # Initialize left and right indexes
    left,right = 0,len(arr)-1

    while left < right:

        # Increment left index while we see 0 at left
        while (arr[left]%2==0 and left < right):
            left += 1

        # Decrement right index while we see 1 at right
        while (arr[right]%2 == 1 and left < right):
            right -= 1

        if (left < right):
              # Swap arr[left] and arr[right]*/
              arr[left],arr[right] = arr[right],arr[left]
              left += 1
              right = right-1

# Driver function to test above function
arr = [12, 34, 45, 9, 8, 90, 3]
segregateEvenOdd(arr)
print ("Array after segregation "),
for i in range(0,len(arr)):
    print arr[i],
# This code is contributed by Devesh Agrawal
```

## C#

```
// C# program to segregate even
// and odd elements of array
using System;

class GFG
{
    static void segregateEvenOdd(int []arr)
    {
        /* Initialize left and right indexes */
        int left = 0, right = arr.Length - 1;
        while (left < right)
        {
            /* Increment left index while we see 0 at left */
            while (arr[left]%2 == 0 && left < right)
                left++;

            /* Decrement right index while we see 1 at right */
            while (arr[right]%2 == 1 && left < right)
                right--;

            if (left < right)
            {
                /* Swap arr[left] and arr[right]*/
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;
                left++;
                right--;
            }
        }
    }

    /* Driver program to test above functions */
    public static void Main ()
    {
        int []arr = {12, 34, 45, 9, 8, 90, 3};

        segregateEvenOdd(arr);

        Console.Write("Array after segregation ");
        for (int i = 0; i < arr.Length; i++)
            Console.Write(arr[i]+" ");
    }
}

//This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to segregate even and
// odd elements of array

function segregateEvenOdd(&$arr, $size)
{
    // Initialize left and right indexes
    $left = 0;
    $right = $size-1;
    while ($left < $right)
    {
        // Increment left index while we
        // see 0 at left
        while ($arr[$left] % 2 == 0 &&
                    $left < $right)
            $left++;

        // Decrement right index while we
        // see 1 at right
        while ($arr[$right] % 2 == 1 &&
                    $left < $right)
            $right--;

        if ($left < $right)
        {
            // Swap $arr[$left] and $arr[$right]
            swap($arr[$left], $arr[$right]);
            $left++;
            $right--;
        }
    }
}

// UTILITY FUNCTIONS
function swap(&$a, &$b)
{
    $temp = $a;
    $a = $b;
    $b = $temp;
}

// Driver Code
$arr = array(12, 34, 45, 9, 8, 90, 3);
$arr_size = count($arr);

segregateEvenOdd($arr, $arr_size);

echo "Array after segregation ";
for ($i = 0; $i < $arr_size; $i++)
    echo $arr[$i]." ";

// This code is contributed
// by rathbhupendra
?>
```

## java 描述语言

```
<script>

// javascript program to segregate even
// and odd elements of array

function segregateEvenOdd(arr)
{
    /* Initialize left and right indexes */
       var left = 0, right = arr.length - 1;
    while (left < right)
    {
        /* Increment left index while
           we see 0 at left */
        while (arr[left]%2 == 0 && left < right)
            left++;

        /* Decrement right index while we see
           1 at right */
        while (arr[right]%2 == 1 && left < right)
            right--;

        if (left < right)
        {
            /* Swap arr[left] and arr[right]*/
            var temp = arr[left];
            arr[left] = arr[right];
            arr[right] = temp;
            left++;
            right--;
        }
    }
}

/* Driver program to test above functions */
   var arr = [12, 34, 45, 9, 8, 90, 3];

   segregateEvenOdd(arr);

   document.write("Array after segregation ");
   for (i = 0; i < arr.length; i++)
       document.write(arr[i]+" ");

// This code is contributed by 29AjayKumar

</script>
```

**Output**

```
Array after segregation 12 34 90 8 9 45 3 
```

**时间复杂度:** O(n)

**交替实现(** [**洛木托分区**](https://www.geeksforgeeks.org/hoares-vs-lomuto-partition-scheme-quicksort/) **):**

## C++

```
// A Lomuto partition based scheme to segregate
// even and odd numbers.
#include <iostream>
using namespace std;

// Function to rearrange the array in given way.
void rearrangeEvenAndOdd(int arr[], int n)
{
    // Variables
    int j = -1;

    // Quick sort method
    for (int i = 0; i < n; i++) {

        // If array of element
        // is odd then swap
        if (arr[i] % 2 == 0) {

            // increment j by one
            j++;

            // swap the element
            swap(arr[i], arr[j]);
        }
    }
}

int main()
{
    int arr[] = { 12, 10, 9, 45, 2, 10, 10, 45 };
    int n = sizeof(arr) / sizeof(arr[0]);

    rearrangeEvenAndOdd(arr, n);

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}
// This code is contributed by devagarwalmnnit
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Lomuto partition based scheme to segregate
// even and odd numbers.
import java.io.*;

class GFG
{
    // function to rearrange the array in given way.
    static void rearrangeEvenAndOdd(int arr[], int n)
    {
        // variables
        int j = -1,temp;

        // quick sort method
        for (int i = 0; i < n; i++) {

            // if array of element
            // is odd then swap
            if (arr[i] % 2 == 0) {

                // increment j by one
                j++;

                // swap the element
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 12, 10, 9, 45, 2, 10, 10, 45 };
        int n = arr.length;

        rearrangeEvenAndOdd(arr, n);

        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }
}

// This code is contributed by Nikita Tiwari.
```

## 蟒蛇 3

```
# A Lomuto partition based scheme to
# segregate even and odd numbers.

# function to rearrange the
# array in given way.
def rearrangeEvenAndOdd(arr, n) :
    # variables
    j = -1

    # quick sort method
    for i in range(0, n) :

        # if array of element
        # is odd then swap
        if (arr[i] % 2 == 0) :
            # increment j by one
            j = j + 1

            # swap the element
            temp = arr[i]
            arr[i] = arr[j]
            arr[j] = temp

# Driver code       
arr = [ 12, 10, 9, 45, 2, 10, 10, 45 ]
n = len(arr)

rearrangeEvenAndOdd(arr, n)

for i in range(0,n) :
    print( arr[i] ,end= " ")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// A Lomuto partition based scheme
// to segregate even and odd numbers.
using System;

class GFG
{
    // function to rearrange
    // the array in given way.
    static void rearrangeEvenAndOdd(int []arr,
                                        int n)
    {
        // variables
        int j = -1, temp;

        // quick sort method
        for (int i = 0; i < n; i++) {

            // if array of element
            // is odd then swap
            if (arr[i] % 2 == 0) {

                // increment j by one
                j++;

                // swap the element
                temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 12, 10, 9, 45, 2,
                            10, 10, 45 };
        int n = arr.Length;

        rearrangeEvenAndOdd(arr, n);

        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A Lomuto partition based scheme to
// segregate even and odd numbers.

// function to rearrange the array
// in given way.
function rearrangeEvenAndOdd(&$arr, $n)
{
    // variables
    $j = -1; $temp;

    // quick sort method
    for ($i = 0; $i < $n; $i++)
    {

        // if array of element
        // is odd then swap
        if ($arr[$i] % 2 == 0)
        {

            // increment j by one
            $j++;

            // swap the element
            $temp = $arr[$i];
            $arr[$i] = $arr[$j];
            $arr[$j] = $temp;
        }
    }
}

// Driver code
$arr = array( 12, 10, 9, 45, 2, 10, 10, 45 );
$n = sizeof($arr);

rearrangeEvenAndOdd($arr, $n);

for ($i = 0; $i < $n; $i++)
    echo($arr[$i] . " ");

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// A Lomuto partition based scheme to segregate
// even and odd numbers.

// Function to rearrange the array in given way.
function rearrangeEvenAndOdd(arr, n)
{

    // Variables
    var j = -1, temp;

    // Quick sort method
    for(i = 0; i < n; i++)
    {

        // If array of element
        // is odd then swap
        if (arr[i] % 2 == 0)
        {

            // Increment j by one
            j++;

            // Swap the element
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
}

// Driver code
var arr = [ 12, 10, 9, 45, 2, 10, 10, 45 ];
var n = arr.length;

rearrangeEvenAndOdd(arr, n);

for(i = 0; i < n; i++)
    document.write(arr[i] + " ");

// This code is contributed by gauravrajput1

</script>
```

**Output**

```
12 10 2 10 10 45 9 45 
```

**时间复杂度:** O(n)

**交替实现(使用** [**稳定分区**](https://www.geeksforgeeks.org/stdstable_partition-in-c/) **):**

为了实现上述问题，我们将在 C++中使用 stable_partition。stable_partition()算法排列由 start 和 end 定义的序列，使得 pfn 指定的谓词返回 true 的所有元素都在谓词返回 false 的元素之前。分区是稳定的。这意味着序列的相对顺序被保留。

**语法:**

```
template 
BiIter stable_partition(BiIter start, BiIter end, UnPred pfn);
```

**参数:**

```
start: the range of elements to reorder
end: the range of elements to reorder
pfn: User-defined predicate function object that defines 
the condition to be satisfied if an element
is to be classified. A predicate takes single argument 
and returns true or false.
Return Value:
Returns an iterator to the beginning of the elements 
for which the predicate is false.
```

*该函数试图分配一个临时缓冲区。如果分配失败，则选择效率较低的算法。*

下面是上述逻辑的实现。

**代码:**

## C++14

```
// CPP program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to rearrange the array in given way.
void rearrangeEvenAndOdd(vector<int>v)
{

    // Using stable partition with lambda expression
    stable_partition(v.begin(), v.end(),
                     [](auto a) { return a % 2 == 0; });

    for (int num : v)
        cout << num << " ";
}

// Driver Code
int main()
{
    vector<int> v = { 12, 10, 9, 45, 2, 10, 10, 45 };

    // Function Call
    rearrangeEvenAndOdd(v);
    return 0;
}
// This code is contributed by Chirag Shilwant
```

**Output**

```
12 10 2 10 10 9 45 45 
```

**时间复杂度:**

如果有足够的额外内存可用，则在第一个和最后一个之间的[距离](https://www.geeksforgeeks.org/stddistance-in-c/)内呈线性(即 **O(N)** ，其中 N 是第一个和最后一个之间的距离)。它对每个元素只应用一次谓词(即上述代码的第三个参数)，并且最多执行这么多元素移动。

否则，最多执行 **N*log(N)** 元素交换(其中 N 是上面的距离)。它还对每个元素只应用一次谓词。

**替代实施:**

1.  使用两个指针 I 和 j，我将指向索引 0，j 将指向最后一个索引。
2.  运行一个 while 循环；如果 a[i]是奇数，a[j]是偶数，那么我们将交换它们，否则我们将减少 j。

**代码:**

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to segregate
void segregate(int a[], int n)
{
    int i = 0, j = (n - 1);

    // Iterate while j >= i
    while (j >= i) {

        // Check is a[i] is even
        // or odd
        if (a[i] % 2 != 0)
        {
            if (a[j] % 2 == 0)
            {

                // Swap a[i] and a[j]
                swap(a[i], a[j]);
                i++;
                j--;
            }
            else
                j--;
        }
        else
            i++;
    }

    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
}

// Driver Code
int main()
{
    int a[] = { 1,2,3,4,5,6 };
    int n = sizeof(a) / sizeof(a[0]);

    // Function Call
    segregate(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to segregate
static void segregate(int a[], int n)
{
    int i = 0, j = (n - 1);

    // Iterate while j >= i
    while (j >= i)
    {

        // Check is a[i] is even
        // or odd
        if (a[i] % 2 != 0)
        {
            if (a[j] % 2 == 0)
            {

                // Swap a[i] and a[j]
                a = swap(a, i, j);
                i++;
                j--;
            }
            else
                j--;
        }
        else
            i++;
    }

    for(i = 0; i < n; i++)
        System.out.print(a[i] + " ");
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3, 4, 5, 6 };
    int n = a.length;

    // Function Call
    segregate(a, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to segregate
def segregate(a, n):

    i = 0
    j = (n - 1)

    # Iterate while j >= i
    while (j >= i):

        # Check is a[i] is even
        # or odd
        if (a[i] % 2 != 0):
            if (a[j] % 2 == 0):

                # Swap a[i] and a[j]
                a[i], a[j] = a[j], a[i]
                i += 1
                j -= 1

            else:
                j -= 1
        else:
            i += 1;

    for i in range(n):
        print(a[i], end = " ")

# Driver Code
a = [ 1, 2, 3, 4, 5, 6 ]
n = len(a)

segregate(a, n)

#  This code is contributed by rag2127
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to segregate
    static void segregate(int[] a, int n)
    {
        int i = 0, j = (n - 1);

        // Iterate while j >= i
        while (j >= i)
        {

            // Check is a[i] is even
            // or odd
            if (a[i] % 2 != 0) {
                if (a[j] % 2 == 0) {

                    // Swap a[i] and a[j]
                    int temp = a[i];
                    a[i] = a[j];
                    a[j] = temp;
                    i++;
                    j--;
                }
                else
                    j--;
            }
            else
                i++;
        }

        for (i = 0; i < n; i++)
            Console.Write(a[i] + " ");
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] a = { 1, 2, 3, 4, 5, 6 };
        int n = a.Length;

        // Function Call
        segregate(a, n);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
// JAVASCRIPT program for the above approach

import java.util.*;
class GFG{

// Function to segregate
static void segregate(int a[], int n)
{
    int i = 0, j = (n - 1);

    // Iterate while j >= i
    while (j >= i) {

        // Check is a[i] is even
        // or odd
        if (a[i] % 2 != 0)
        {
            if (a[j] % 2 == 0)
            {

                // Swap a[i] and a[j]
                a = swap(a,i,j);
                i++;
                j--;
            }
            else
                j--;
        }
        else
            i++;
    }

    for (i = 0; i < n; i++)
        System.out.print(a[i]+ " ");
}
static int[] swap(int []arr, int i, int j){
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}
// Driver Code
public static void main(String[] args)
{
    int a[] = { 1,2,3,4,5,6 };
    int n = a.length;

    // Function Call
    segregate(a, n);
}
}

// This code contributed by Princi Singh
```

**Output**

```
6 2 4 3 5 1 
```

**时间复杂度:**O(N)**T3】**

**空间复杂度:** O(1)

参考文献:
[【http://www.csse.monash.edu.au/~lloyd/tildeAlgDS/Sort/Flag/】](http://www.csse.monash.edu.au/~lloyd/tildeAlgDS/Sort/Flag/)
如果发现以上代码/算法不正确，请写评论，或者找到更好的方法解决同样的问题。