# 改进线性搜索技术

> 原文:[https://www . geesforgeks . org/improving-linear-search-technology/](https://www.geeksforgeeks.org/improving-linear-search-technique/)

[线性搜索或顺序搜索](https://www.geeksforgeeks.org/linear-search/)是一种在列表中查找元素的方法。它依次检查列表中的每个元素，直到找到匹配项或搜索了整个列表。观察到当搜索一个**关键元素**时，有可能一次又一次地搜索相同的关键元素。

目标是如果相同的元素被再次搜索，那么操作必须花费更少的时间。因此，在这种情况下，可以通过使用以下两种方法来改进线性搜索:

1.  调换
2.  移到前面

### <u>换位</u>:

在转置中，如果找到了关键字元素，它会被交换到元素之前的索引中，以增加特定关键字的搜索计数，搜索操作还会优化并保持将元素移动到数组的开始处，在该处搜索时间复杂度为常数时间。

**例如:**如果数组**arr【】**是{2，5，7，1，6，4，5，8，3，7}并且让要搜索的键是 4，那么下面是步骤:

*   搜索关键字 **4** 后，经过 6 次比较，在给定数组的**索引 5** 处找到该元素。现在换位后，数组变成{2，5，7，1，4，6，5，8，3，7}，即值为 4 的键位于索引 4 处。
*   再次搜索关键字 **4** 后，经过 6 次比较，在给定数组的**索引 4** 处找到该元素。现在换位后，数组变成{2，5，7，4，1，6，5，8，3，7}，即值为 4 的键位于索引 3 处。
*   如果要查找的元素不在第一个索引处，上述过程将继续，直到任何键到达数组的前面。

下面是上面讨论的算法的实现:

## C++

```
// C++ program for transposition to
// improve the Linear Search Algorithm
#include <iostream>
using namespace std;

// Structure of the array
struct Array {

    int A[10];
    int size;
    int length;
};

// Function to print the array element
void Display(struct Array arr)
{
    int i;

    // Traverse the array arr[]
    for (i = 0; i < arr.length; i++) {
        cout <<" "<< arr.A[i];
    }
    cout <<"\n";
}

// Function that swaps two elements
// at different addresses
void swap(int* x, int* y)
{
    // Store the value store at
    // x in a variable temp
    int temp = *x;

    // Swapping of value
    *x = *y;
    *y = temp;
}

// Function that performs the Linear
// Search Transposition
int LinearSearchTransposition(
    struct Array* arr, int key)
{
    int i;

    // Traverse the array
    for (i = 0; i < arr->length; i++) {

        // If key is found, then swap
        // the element with it's
        // previous index
        if (key == arr->A[i]) {

            // If key is first element
            if (i == 0)
                return i;

            swap(&arr->A[i],
                 &arr->A[i - 1]);

            return i;
        }
    }
    return -1;
}

// Driver Code
int main()
{
    // Given array arr[]
    struct Array arr
        = { { 2, 23, 14, 5, 6, 9, 8, 12 },
            10,
            8 };

    cout <<"Elements before Linear"
           " Search Transposition: ";

    // Function Call for displaying
    // the array arr[]
    Display(arr);

    // Function Call for transposition
    LinearSearchTransposition(&arr, 14);

    cout <<"Elements after Linear"
           " Search Transposition: ";

    // Function Call for displaying
    // the array arr[]
    Display(arr);
    return 0;
}

// this code is contributed by shivanisinghss2110
```

## C

```
// C program for transposition to
// improve the Linear Search Algorithm
#include <stdio.h>

// Structure of the array
struct Array {

    int A[10];
    int size;
    int length;
};

// Function to print the array element
void Display(struct Array arr)
{
    int i;

    // Traverse the array arr[]
    for (i = 0; i < arr.length; i++) {
        printf("%d ", arr.A[i]);
    }
    printf("\n");
}

// Function that swaps two elements
// at different addresses
void swap(int* x, int* y)
{
    // Store the value store at
    // x in a variable temp
    int temp = *x;

    // Swapping of value
    *x = *y;
    *y = temp;
}

// Function that performs the Linear
// Search Transposition
int LinearSearchTransposition(
    struct Array* arr, int key)
{
    int i;

    // Traverse the array
    for (i = 0; i < arr->length; i++) {

        // If key is found, then swap
        // the element with it's
        // previous index
        if (key == arr->A[i]) {

            // If key is first element
            if (i == 0)
                return i;

            swap(&arr->A[i],
                 &arr->A[i - 1]);

            return i;
        }
    }
    return -1;
}

// Driver Code
int main()
{
    // Given array arr[]
    struct Array arr
        = { { 2, 23, 14, 5, 6, 9, 8, 12 },
            10,
            8 };

    printf("Elements before Linear"
           " Search Transposition: ");

    // Function Call for displaying
    // the array arr[]
    Display(arr);

    // Function Call for transposition
    LinearSearchTransposition(&arr, 14);

    printf("Elements after Linear"
           " Search Transposition: ");

    // Function Call for displaying
    // the array arr[]
    Display(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for transposition
// to improve the Linear Search
// Algorithm
class GFG{

// Structure of the
// array
static class Array
{
  int []A = new int[10];
  int size;
  int length;
  Array(int []A, int size,
        int length)
  {
    this.A = A;
    this.size = size;
    this.length = length;
  }
};

// Function to print the
// array element
static void Display(Array arr)
{
  int i;

  // Traverse the array arr[]
  for (i = 0; i < arr.length; i++)
  {
    System.out.printf("%d ",
                      arr.A[i]);
  }
  System.out.printf("\n");
}

// Function that performs the Linear
// Search Transposition
static int LinearSearchTransposition(Array arr,
                                     int key)
{
  int i;

  // Traverse the array
  for (i = 0; i < arr.length; i++)
  {
    // If key is found, then swap
    // the element with it's
    // previous index
    if (key == arr.A[i])
    {
      // If key is first element
      if (i == 0)
        return i;
      int temp = arr.A[i];
      arr.A[i] = arr.A[i - 1];
      arr.A[i - 1] = temp;
      return i;
    }
  }
  return -1;
}

// Driver Code
public static void main(String[] args)
{
  // Given array arr[]
  int tempArr[] = {2, 23, 14, 5,
                   6, 9, 8, 12};
  Array arr = new Array(tempArr,
                        10, 8);

  System.out.printf("Elements before Linear" +
                    " Search Transposition: ");

  // Function Call for displaying
  // the array arr[]
  Display(arr);

  // Function Call for transposition
  LinearSearchTransposition(arr, 14);

  System.out.printf("Elements after Linear" +
                    " Search Transposition: ");

  // Function Call for displaying
  // the array arr[]
  Display(arr);
}
}

// This code is contributed by Princi Singh
```

## C#

```
// C# program for transposition
// to improve the Linear Search
// Algorithm
using System;

class GFG{

// Structure of the
// array
public class Array
{
    public int []A = new int[10];
    public int size;
    public int length;

    public Array(int []A, int size,
                 int length)
    {
        this.A = A;
        this.size = size;
        this.length = length;
    }
};

// Function to print the
// array element
static void Display(Array arr)
{
    int i;

    // Traverse the array []arr
    for(i = 0; i < arr.length; i++)
    {
        Console.Write(arr.A[i] + " ");
    }
    Console.Write("\n");
}

// Function that performs the Linear
// Search Transposition
static int LinearSearchTransposition(Array arr,
                                     int key)
{
    int i;

    // Traverse the array
    for(i = 0; i < arr.length; i++)
    {

        // If key is found, then swap
        // the element with it's
        // previous index
        if (key == arr.A[i])
        {

            // If key is first element
            if (i == 0)
                return i;

            int temp = arr.A[i];
            arr.A[i] = arr.A[i - 1];
            arr.A[i - 1] = temp;
            return i;
        }
    }
    return -1;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []tempArr = { 2, 23, 14, 5,
                      6, 9, 8, 12 };
    Array arr = new Array(tempArr, 10, 8);

    Console.Write("Elements before Linear " +
                  "Search Transposition: ");

    // Function Call for displaying
    // the array []arr
    Display(arr);

    // Function Call for transposition
    LinearSearchTransposition(arr, 14);

    Console.Write("Elements after Linear " +
                  "Search Transposition: ");

    // Function Call for displaying
    // the array []arr
    Display(arr);
}
}

// This code is contributed by Amit Katiyar
```

**Output:** Elements before Linear Search Transposition: 2 23 14 5 6 9 8 12 Elements after Linear Search Transposition: 2 14 23 5 6 9 8 12  

### <u>移至前端/头部</u>:

在这种方法中，如果找到了关键元素，则直接与索引 **0** 交换，以便下一个连续的时间，对同一关键元素的搜索操作是 **O(1)** ，即恒定时间。

**例如:**如果数组**arr【】**是{2，5，7，1，6，4，5，8，3，7}并且让要搜索的键是 4，那么下面是步骤:

*   搜索关键字 **4** 后，经过 6 次比较，在给定数组的**索引 5** 处找到该元素。现在移到前面操作后，数组变成{4，2，5，7，1，6，5，8，3，7}，即值为 4 的键出现在**索引 0** 处。
*   再次搜索关键字 **4** 后，在给定数组的**索引 0** 处找到该元素，这减少了整个的搜索空间。

## C++

```
// C program to implement the move to
// front to optimized Linear Search
#include <iostream>
using namespace std;

// Structure of the array
struct Array {

    int A[10];
    int size;
    int length;
};

// Function to print the array element
void Display(struct Array arr)
{
    int i;

    // Traverse the array arr[]
    for (i = 0; i < arr.length; i++) {
        cout <<" "<< arr.A[i];
    }
    cout <<"\n";
}

// Function that swaps two elements
// at different addresses
void swap(int* x, int* y)
{
    // Store the value store at
    // x in a variable temp
    int temp = *x;

    // Swapping of value
    *x = *y;
    *y = temp;
}

// Function that performs the move to
// front operation for Linear Search
int LinearSearchMoveToFront(
    struct Array* arr, int key)
{
    int i;

    // Traverse the array
    for (i = 0; i < arr->length; i++) {

        // If key is found, then swap
        // the element with 0-th index
        if (key == arr->A[i]) {
            swap(&arr->A[i], &arr->A[0]);
            return i;
        }
    }
    return -1;
}

// Driver code
int main()
{
    // Given array arr[]
    struct Array arr
        = { { 2, 23, 14, 5, 6, 9, 8, 12 },
            10,
            8 };

    cout <<"Elements before Linear"
           " Search Move To Front: ";

    // Function Call for displaying
    // the array arr[]
    Display(arr);

    // Function Call for Move to
    // front operation
    LinearSearchMoveToFront(&arr, 14);

    cout <<"Elements after Linear"
           " Search Move To Front: ";

    // Function Call for displaying
    // the array arr[]
    Display(arr);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program to implement the move to
// front to optimized Linear Search
#include <stdio.h>

// Structure of the array
struct Array {

    int A[10];
    int size;
    int length;
};

// Function to print the array element
void Display(struct Array arr)
{
    int i;

    // Traverse the array arr[]
    for (i = 0; i < arr.length; i++) {
        printf("%d ", arr.A[i]);
    }
    printf("\n");
}

// Function that swaps two elements
// at different addresses
void swap(int* x, int* y)
{
    // Store the value store at
    // x in a variable temp
    int temp = *x;

    // Swapping of value
    *x = *y;
    *y = temp;
}

// Function that performs the move to
// front operation for Linear Search
int LinearSearchMoveToFront(
    struct Array* arr, int key)
{
    int i;

    // Traverse the array
    for (i = 0; i < arr->length; i++) {

        // If key is found, then swap
        // the element with 0-th index
        if (key == arr->A[i]) {
            swap(&arr->A[i], &arr->A[0]);
            return i;
        }
    }
    return -1;
}

// Driver code
int main()
{
    // Given array arr[]
    struct Array arr
        = { { 2, 23, 14, 5, 6, 9, 8, 12 },
            10,
            8 };

    printf("Elements before Linear"
           " Search Move To Front: ");

    // Function Call for displaying
    // the array arr[]
    Display(arr);

    // Function Call for Move to
    // front operation
    LinearSearchMoveToFront(&arr, 14);

    printf("Elements after Linear"
           " Search Move To Front: ");

    // Function Call for displaying
    // the array arr[]
    Display(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the move to front to optimized
// Linear Search
class GFG{

// Structure of the array
static class Array
{
  int []A = new int[10];
  int size;
  int length;
  Array(int []A, int size,
        int length)
  {
    this.A = A;
    this.size = size;
    this.length = length;
  }
};

// Function to print the
// array element
static void Display(Array arr)
{
  int i;

  // Traverse the array arr[]
  for (i = 0;
       i < arr.length; i++)
  {
    System.out.printf("%d ", arr.A[i]);
  }
  System.out.printf("\n");
}

// Function that performs the
// move to front operation for
// Linear Search
static int LinearSearchMoveToFront(Array arr,
                                   int key)
{
  int i;

  // Traverse the array
  for (i = 0; i < arr.length; i++)
  {
    // If key is found, then swap
    // the element with 0-th index
    if (key == arr.A[i])
    {
      int temp = arr.A[i];
      arr.A[i] = arr.A[0];
      arr.A[0] = temp;
      return i;
    }
  }
  return -1;
}

// Driver code
public static void main(String[] args)
{
  // Given array arr[]
  int a[] = {2, 23, 14, 5,
             6, 9, 8, 12 };
  Array arr = new Array(a, 10, 8);

  System.out.printf("Elements before Linear" +
                    " Search Move To Front: ");

  // Function Call for
  // displaying the array
  // arr[]
  Display(arr);

  // Function Call for Move
  // to front operation
  LinearSearchMoveToFront(arr, 14);

  System.out.printf("Elements after Linear" +
                    " Search Move To Front: ");

  // Function Call for displaying
  // the array arr[]
  Display(arr);
}
}

// This code is contributed by gauravrajput1
```

## C#

```
// C# program to implement
// the move to front to optimized
// Linear Search
using System;
class GFG{

// Structure of the array
public class Array
{
  public int []A = new int[10];
  public int size;
  public int length;
  public Array(int []A,
               int size,
               int length)
  {
    this.A = A;
    this.size = size;
    this.length = length;
  }
};

// Function to print the
// array element
static void Display(Array arr)
{
  int i;

  // Traverse the array []arr
  for (i = 0;
       i < arr.length; i++)
  {
    Console.Write(" " + arr.A[i]);
  }
  Console.Write("\n");
}

// Function that performs the
// move to front operation for
// Linear Search
static int LinearSearchMoveToFront(Array arr,
                                   int key)
{
  int i;

  // Traverse the array
  for (i = 0; i < arr.length; i++)
  {
    // If key is found, then swap
    // the element with 0-th index
    if (key == arr.A[i])
    {
      int temp = arr.A[i];
      arr.A[i] = arr.A[0];
      arr.A[0] = temp;
      return i;
    }
  }
  return -1;
}

// Driver code
public static void Main(String[] args)
{
  // Given array []arr
  int []a = {2, 23, 14, 5,
             6, 9, 8, 12 };

  Array arr = new Array(a, 10, 8);
  Console.Write("Elements before Linear" +
                " Search Move To Front: ");

  // Function Call for
  // displaying the array
  // []arr
  Display(arr);

  // Function Call for Move
  // to front operation
  LinearSearchMoveToFront(arr, 14);

  Console.Write("Elements after Linear" +
                " Search Move To Front: ");

  // Function Call for displaying
  // the array []arr
  Display(arr);
}
}

// This code is contributed by gauravrajput1
```

**Output:** Elements before Linear Search Move To Front: 2 23 14 5 6 9 8 12 Elements after Linear Search Move To Front: 14 23 2 5 6 9 8 12 

**时间复杂度:**O(N)
T3】辅助空间 : O(1)