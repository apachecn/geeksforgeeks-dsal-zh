# 一个煎饼分类问题

> 原文:[https://www.geeksforgeeks.org/a-pancake-sorting-question/](https://www.geeksforgeeks.org/a-pancake-sorting-question/)

我们在之前的帖子中已经讨论过[煎饼分类](https://www.geeksforgeeks.org/pancake-sorting/)。下面是一个基于煎饼排序的问题。
给定一个未排序的数组，给定数组排序。您只能对数组执行以下操作。

```
flip(arr, i): Reverse array from 0 to i 
```

**想象一台假想的机器，翻转(I)总是需要 O(1)时间**。**编写一个高效的程序，在给定的机器上按照 O(nLogn)时间对给定的数组进行排序**。如果我们在这里应用[相同的算法](https://www.geeksforgeeks.org/pancake-sorting/),所花费的时间将是 O(n^2)，因为该算法在循环中调用 findMax()，即使在这个假设的机器上，findMax()也花费 O(n)个时间。
我们可以使用使用二分搜索法的插入排序。其思想是运行从第二个元素到最后一个元素(从 i = 1 到 n-1)的循环，并在 arr[0]中逐个插入 arr[i]..i-1](如[标准插入排序算法](http://en.wikipedia.org/wiki/Insertion_sort#Algorithm))。当我们插入一个元素 arr[i]时，我们可以用二分搜索法来求 arr[i]在 O(Logi)时间中的位置。一旦我们有了位置，我们可以使用一些翻转操作将 arr[i]放到它的新位置。以下是一些抽象的步骤。

```
// Standard Insertion Sort Loop that starts from second element
for (i=1; i  O(n)
{
  int key = arr[i];

  // Find index of ceiling of arr[i] in arr[0..i-1] using binary search
  j = celiSearch(arr, key, 0, i-1); ----> O(logn) (See this)

  // Apply some flip operations to put arr[i] at correct place
} 
```

由于翻转操作在给定的假设机器上需要 O(1)，因此上述算法的总运行时间为 O(nlogn)。感谢[库马尔](https://www.geeksforgeeks.org/pancake-sorting/#comment-15835)提出上述问题和算法。
让我们看看上面的算法是如何工作的。[ceilisearch()](https://www.geeksforgeeks.org/search-floor-and-ceil-in-a-sorted-array/)实际上返回 arr[0]中大于 arr[i]的最小元素的索引..i-1]。如果没有这样的元素，它将返回-1。假设返回值是 j，如果 j 是-1，那么我们不需要做任何事情，因为 arr[i]已经是 arr[0]中最大的元素..我】。否则我们需要在逮捕[j]之前逮捕[i]。
那么如何使用 I 和 j 的值应用翻转操作将 arr[i]放在 arr[j]之前呢，让我们举个例子来理解这一点。设 I 为 6，当前数组为{12，15，18，30，35，40， **20** ，6，90，80}。要将 20 放在新位置，数组应改为{12，15，18， **20** ，30，35，40，6，90，80}。我们应用以下步骤将 20 放在其新位置。
1)使用 ceilSearch 查找 j(在上面的示例中，j 是 3)。
2)翻转(arr，j-1)(数组变成{18，15，12，30，35，40， **20** ，6，90，80})
3)翻转(arr，I-1)；(数组变成{40，35，30，12，15，18， **20** ，6，90，80})
4)翻转(arr，I)；(数组变成{ **20** 、18、15、12、30、35、40、6、90、80})
5)翻转(arr，j)；(数组变成{12，15，18， **20** ，30，35，40，6，90，80})
下面是上面算法的实现。

## C++

```
// C++ program of Pancake Sorting Problem
#include<bits/stdc++.h>
using namespace std;

/* A Binary Search based function to
get index of ceiling of x in
arr[low..high] */
int ceilSearch(int arr[], int low, int high, int x)
{
    int mid;

    /* If x is smaller than or equal
    to the first element,
    then return the first element */
    if(x <= arr[low])
        return low;

    /* If x is greater than the
    last element, then return -1 */
    if(x > arr[high])
        return -1;

    /* get the index of middle
    element of arr[low..high]*/
    mid = (low + high)/2; /* low + (high – low)/2 */

    /* If x is same as middle
    element, then return mid */
    if(arr[mid] == x)
        return mid;

    /* If x is greater than arr[mid],
    then either arr[mid + 1]
    is ceiling of x, or ceiling
    lies in arr[mid+1...high] */
    if(arr[mid] < x)
    {
        if(mid + 1 <= high && x <= arr[mid+1])
            return mid + 1;
        else
            return ceilSearch(arr, mid+1, high, x);
    }

    /* If x is smaller than arr[mid], then either arr[mid]
    is ceiling of x or ceiling lies in arr[mid-1...high] */
    if (mid - 1 >= low && x > arr[mid-1])
        return mid;
    else
        return ceilSearch(arr, low, mid - 1, x);
}

/* Reverses arr[0..i] */
void flip(int arr[], int i)
{
    int temp, start = 0;
    while (start < i)
    {
        temp = arr[start];
        arr[start] = arr[i];
        arr[i] = temp;
        start++;
        i--;
    }
}

/* Function to sort an array using
insertion sort, binary search and flip */
void insertionSort(int arr[], int size)
{
    int i, j;

    // Start from the second element
    // and one by one insert arr[i]
    // in already sorted arr[0..i-1]
    for(i = 1; i < size; i++)
    {
        // Find the smallest element in arr[0..i-1]
        // which is also greater than
        // or equal to arr[i]
        int j = ceilSearch(arr, 0, i-1, arr[i]);

        // Check if there was no element
        // greater than arr[i]
        if (j != -1)
        {
            // Put arr[i] before arr[j] using
            // following four flip operations
            flip(arr, j-1);
            flip(arr, i-1);
            flip(arr, i);
            flip(arr, j);
        }
    }
}

/* A utility function to print an array of size n */
void printArray(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        cout<<arr[i]<<" ";
}

/* Driver code */
int main()
{
    int arr[] = {18, 40, 35, 12, 30, 35, 20, 6, 90, 80};
    int n = sizeof(arr)/sizeof(arr[0]);
    insertionSort(arr, n);
    printArray(arr, n);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C program of Pancake Sorting Problem
#include <stdlib.h>
#include <stdio.h>

/* A Binary Search based function to get index of ceiling of x in
   arr[low..high] */
int ceilSearch(int arr[], int low, int high, int x)
{
    int mid;

    /* If x is smaller than or equal to the first element,
      then return the first element */
    if(x <= arr[low])
        return low;

    /* If x is greater than the last element, then return -1 */
    if(x > arr[high])
        return -1;

    /* get the index of middle element of arr[low..high]*/
    mid = (low + high)/2;  /* low + (high – low)/2 */

    /* If x is same as middle element, then return mid */
    if(arr[mid] == x)
        return mid;

    /* If x is greater than arr[mid], then either arr[mid + 1]
      is ceiling of x, or ceiling lies in arr[mid+1...high] */
    if(arr[mid] < x)
    {
        if(mid + 1 <= high && x <= arr[mid+1])
            return mid + 1;
        else
            return ceilSearch(arr, mid+1, high, x);
    }

    /* If x is smaller than arr[mid], then either arr[mid]
       is ceiling of x or ceiling lies in arr[mid-1...high] */
    if (mid - 1 >= low && x > arr[mid-1])
        return mid;
    else
        return ceilSearch(arr, low, mid - 1, x);
}

/* Reverses arr[0..i] */
void flip(int arr[], int i)
{
    int temp, start = 0;
    while (start < i)
    {
        temp = arr[start];
        arr[start] = arr[i];
        arr[i] = temp;
        start++;
        i--;
    }
}

/* Function to sort an array using insertion sort, binary search and flip */
void insertionSort(int arr[], int size)
{
    int i, j;

    // Start from the second element and one by one insert arr[i]
    // in already sorted arr[0..i-1]
    for(i = 1; i < size; i++)
    {
        // Find the smallest element in arr[0..i-1] which is also greater than
        // or equal to arr[i]
        int j = ceilSearch(arr, 0, i-1, arr[i]);

        // Check if there was no element greater than arr[i]
        if (j != -1)
        {
            // Put arr[i] before arr[j] using following four flip operations
            flip(arr, j-1);
            flip(arr, i-1);
            flip(arr, i);
            flip(arr, j);
        }
    }
}

/* A utility function to print an array of size n */
void printArray(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        printf("%d ", arr[i]);
}

/* Driver program to test insertion sort */
int main()
{
    int arr[] = {18, 40, 35, 12, 30, 35, 20, 6, 90, 80};
    int n = sizeof(arr)/sizeof(arr[0]);
    insertionSort(arr, n);
    printArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of Pancake Sorting Problem
class GfG {

/* A Binary Search based function to get index of ceiling of x in
arr[low..high] */
static int ceilSearch(int arr[], int low, int high, int x)
{
    int mid;

    /* If x is smaller than or equal to the first element,
    then return the first element */
    if(x <= arr[low])
        return low;

    /* If x is greater than the last element, then return -1 */
    if(x > arr[high])
        return -1;

    /* get the index of middle element of arr[low..high]*/
//     low + (high - low)/2
    mid = (low + high)/2;

    /* If x is same as middle element, then return mid */
    if(arr[mid] == x)
        return mid;

    /* If x is greater than arr[mid], then either arr[mid + 1]
    is ceiling of x, or ceiling lies in arr[mid+1...high] */
    if(arr[mid] < x)
    {
        if(mid + 1 <= high && x <= arr[mid+1])
            return mid + 1;
        else
            return ceilSearch(arr, mid+1, high, x);
    }

    /* If x is smaller than arr[mid], then either arr[mid]
    is ceiling of x or ceiling lies in arr[mid-1...high] */
    if (mid - 1 >= low && x > arr[mid-1])
        return mid;
    else
        return ceilSearch(arr, low, mid - 1, x);
}

/* Reverses arr[0..i] */
static void flip(int arr[], int i)
{
    int temp, start = 0;
    while (start < i)
    {
        temp = arr[start];
        arr[start] = arr[i];
        arr[i] = temp;
        start++;
        i--;
    }
}

/* Function to sort an array using insertion sort, binary search and flip */
static void insertionSort(int arr[], int size)
{
    int i;

    // Start from the second element and one by one insert arr[i]
    // in already sorted arr[0..i-1]
    for(i = 1; i < size; i++)
    {
        // Find the smallest element in arr[0..i-1] which is also greater than
        // or equal to arr[i]
        int j = ceilSearch(arr, 0, i-1, arr[i]);

        // Check if there was no element greater than arr[i]
        if (j != -1)
        {
            // Put arr[i] before arr[j] using following four flip operations
            flip(arr, j-1);
            flip(arr, i-1);
            flip(arr, i);
            flip(arr, j);
        }
    }
}

/* A utility function to print an array of size n */
static void printArray(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        System.out.print(arr[i] + " ");
}

/* Driver program to test insertion sort */
public static void main(String[] args)
{
    int arr[] = {18, 40, 35, 12, 30, 35, 20, 6, 90, 80};
    int n = arr.length;
    insertionSort(arr, n);
    printArray(arr, n);
}
}
```

## 计算机编程语言

```
# Python program of Pancake Sorting Problem
#A Binary Search based function to get index of ceiling of x in arr[low..high]

def ceilSearch(arr,low,high,x):

    #If x is smaller than or equal to the first element,
    #then return the first element
    if x <= arr[low]:
        return low

    #If x is greater than the last element, then return -1
    if x > arr[high]:
        return -1

    #get the index of middle element of arr[low..high]
    mid = (low + high)/2  #low + (high-low)/2

    #If x is same as middle element, then return mid
    if(arr[mid] == x):
        return mid

    #If x is greater than arr[mid], then either arr[mid + 1]
    #is ceiling of x, or ceiling lies in arr[mid+1...high]
    if(arr[mid] < x):
        if(mid + 1 <= high and x <= arr[mid+1]):
            return mid + 1
        else:
            return ceilSearch(arr, mid+1, high, x)

    #If x is smaller than arr[mid], then either arr[mid]
    #is ceiling of x or ceiling lies in arr[mid-1...high]
    if (mid - 1 >= low and x > arr[mid-1]):
        return mid
    else:
        return ceilSearch(arr, low, mid - 1, x)

#Reverses arr[0..i] */
def flip(arr,i):

    start = 0;
    while (start < i):
        temp = arr[start]
        arr[start] = arr[i]
        arr[i] = temp
        start+=1
        i-=1

#Function to sort an array using insertion sort, binary search and flip
def insertionSort(arr):

    #Start from the second element and one by one insert arr[i]
    #in already sorted arr[0..i-1]
    for i in range(1,len(arr)):
        #Find the smallest element in arr[0..i-1] which is also greater than
        #or equal to arr[i]
        j = ceilSearch(arr, 0, i-1, arr[i])

        #Check if there was no element greater than arr[i]
        if (j != -1):
            #Put arr[i] before arr[j] using following four flip operations
            flip(arr, j-1)
            flip(arr, i-1)
            flip(arr, i)
            flip(arr, j)

# A utility function to print an array of size n
def printArray(arr):
    for i in range(0,len(arr)):
        print arr[i],

#Driver function to test above function
arr=[18, 40, 35, 12, 30, 35, 20, 6, 90, 80]
insertionSort(arr)
printArray(arr)

#This code is contributed by Devesh Agrawal
```

## C#

```
// C# program of Pancake Sorting Problem
using System;

class GFG
{

// A Binary Search based function to get
// index of ceiling of x in arr[low..high]
static int ceilSearch(int []arr, int low,
                      int high, int x)
{
    int mid;

    // If x is smaller than or equal to
    // the first element,
    // then return the first element
    if(x <= arr[low])
        return low;

    // If x is greater than the last element,
    // then return -1
    if(x > arr[high])
        return -1;

    // get the index of middle element
    // of arr[low..high]
    // low + (high - low)/2
    mid = (low + high) / 2;

    // If x is same as middle element,
    // then return mid
    if(arr[mid] == x)
        return mid;

    // If x is greater than arr[mid],
    // then either arr[mid + 1] is ceiling of x,
    // or ceiling lies in arr[mid+1...high]
    if(arr[mid] < x)
    {
        if(mid + 1 <= high && x <= arr[mid + 1])
            return mid + 1;
        else
            return ceilSearch(arr, mid + 1, high, x);
    }

    // If x is smaller than arr[mid],
    // then either arr[mid] is ceiling of x
    // or ceiling lies in arr[mid-1...high]
    if (mid - 1 >= low && x > arr[mid - 1])
        return mid;
    else
        return ceilSearch(arr, low, mid - 1, x);
}

// Reverses arr[0..i]
static void flip(int []arr, int i)
{
    int temp, start = 0;
    while (start < i)
    {
        temp = arr[start];
        arr[start] = arr[i];
        arr[i] = temp;
        start++;
        i--;
    }
}

// Function to sort an array using insertion sort,
// binary search and flip
static void insertionSort(int []arr, int size)
{
    int i;

    // Start from the second element and
    // one by one insert arr[i] in
    // already sorted arr[0..i-1]
    for(i = 1; i < size; i++)
    {
        // Find the smallest element in arr[0..i-1]
        // which is also greater than or equal to arr[i]
        int j = ceilSearch(arr, 0, i - 1, arr[i]);

        // Check if there was no element greater than arr[i]
        if (j != -1)
        {
            // Put arr[i] before arr[j] using
            // following four flip operations
            flip(arr, j - 1);
            flip(arr, i - 1);
            flip(arr, i);
            flip(arr, j);
        }
    }
}

// A utility function to print an array of size n
static void printArray(int []arr, int n)
{
    int i;
    for (i = 0; i < n; ++i)
        Console.Write(arr[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {18, 40, 35, 12, 30,
                 35, 20, 6, 90, 80};
    int n = arr.Length;
    insertionSort(arr, n);
    printArray(arr, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program of Pancake Sorting Problem

/* A Binary Search based function to
get index of ceiling of x in
arr[low..high] */
function ceilSearch(arr, low, high, x)
{
    var mid;

    /* If x is smaller than or equal
    to the first element,
    then return the first element */
    if(x <= arr[low])
        return low;

    /* If x is greater than the
    last element, then return -1 */
    if(x > arr[high])
        return -1;

    /* get the index of middle
    element of arr[low..high]*/
    mid = parseInt((low + high)/2); /* low + (high – low)/2 */

    /* If x is same as middle
    element, then return mid */
    if(arr[mid] == x)
        return mid;

    /* If x is greater than arr[mid],
    then either arr[mid + 1]
    is ceiling of x, or ceiling
    lies in arr[mid+1...high] */
    if(arr[mid] < x)
    {
        if(mid + 1 <= high && x <= arr[mid+1])
            return mid + 1;
        else
            return ceilSearch(arr, mid+1, high, x);
    }

    /* If x is smaller than arr[mid], then either arr[mid]
    is ceiling of x or ceiling lies in arr[mid-1...high] */
    if (mid - 1 >= low && x > arr[mid-1])
        return mid;
    else
        return ceilSearch(arr, low, mid - 1, x);
}

/* Reverses arr[0..i] */
function flip( arr, i)
{
    var temp, start = 0;
    while (start < i)
    {
        temp = arr[start];
        arr[start] = arr[i];
        arr[i] = temp;
        start++;
        i--;
    }
}

/* Function to sort an array using
insertion sort, binary search and flip */
function insertionSort( arr,  size)
{
    var i, j;

    // Start from the second element
    // and one by one insert arr[i]
    // in already sorted arr[0..i-1]
    for(i = 1; i < size; i++)
    {
        // Find the smallest element in arr[0..i-1]
        // which is also greater than
        // or equal to arr[i]
        var j = ceilSearch(arr, 0, i-1, arr[i]);

        // Check if there was no element
        // greater than arr[i]
        if (j != -1)
        {
            // Put arr[i] before arr[j] using
            // following four flip operations
            flip(arr, j-1);
            flip(arr, i-1);
            flip(arr, i);
            flip(arr, j);
        }
    }
}

/* A utility function to print an array of size n */
function printArray(arr, n)
{
    var i;
    for (i = 0; i < n; ++i)
        document.write(arr[i]+" ");
}

    var arr = [18, 40, 35, 12, 30, 35, 20, 6, 90, 80];
    var n = arr.length;
    insertionSort(arr, n);
    printArray(arr, n);

// This code is contributed by SoumikMondal
</script>
```

**输出:**

```
6 12 18 20 30 35 35 40 80 90
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。