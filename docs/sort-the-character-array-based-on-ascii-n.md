# 根据 ASCII % N 对字符数组进行排序

> 原文:[https://www . geesforgeks . org/基于字符数组的 ascii-n 排序/](https://www.geeksforgeeks.org/sort-the-character-array-based-on-ascii-n/)

给定一个字符数组 **arr[]** 和一个整数 **M** ，任务是根据 **ASCII % M** 对数组进行排序，即 ASCII 值% M 最小的字符应该首先出现。

**示例:**

> **输入:** arr[] = {'a '，' b '，' c '，' e'}，M = 2
> **输出:** b a c e
> 数组的 ASCII % M 为
> {97 % 2，98 % 2，99 % 2，101 % 2}即{1，0，1，1}
> 
> **输入:** arr[] = {'g '，' e '，' e '，' k '，' s'}，M = 8
> T3】输出: k s e e g

**方法 1:** 编写一个函数对数组进行排序，不用比较字符的值，而是比较它们的 ASCII 值% M 来对数组进行排序。最后打印排序后的数组。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// A utility function to swap two elements
void swap(char* a, char* b)
{
    char t = *a;
    *a = *b;
    *b = t;
}

/* This function takes last element as pivot, places
the pivot element at its correct position in sorted
    array, and places all smaller (smaller than pivot)
to left of pivot and all greater elements to right
of pivot */
int partition(char arr[], int low, int high, int mod)
{

    // pivot
    char pivot = arr[high];

    // Index of smaller element
    int i = (low - 1);

    int piv = pivot % mod;
    for (int j = low; j <= high - 1; j++) {

        int a = arr[j] % mod;
        // If current element is smaller than or
        // equal to pivot
        // Instead of values, ASCII % m values
        // are compared
        if (a <= piv) {

            // Increment index of smaller element
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

/* The main function that implements QuickSort
arr[] --> Array to be sorted,
low --> Starting index,
high --> Ending index */
void quickSort(char arr[], int low, int high, int mod)
{
    if (low < high) {
        /* pi is partitioning index, arr[p] is now
        at right place */
        int pi = partition(arr, low, high, mod);

        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1, mod);
        quickSort(arr, pi + 1, high, mod);
    }
}

// Function to print the given array
void printArray(char arr[], int size)
{
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    char arr[] = { 'g', 'e', 'e', 'k', 's' };
    int n = sizeof(arr) / sizeof(arr[0]);
    int mod = 8;

    // Sort the given array
    quickSort(arr, 0, n - 1, mod);

    // Print the sorted array
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    /* This function takes last element as pivot, places
    the pivot element at its correct position in sorted
        array, and places all smaller (smaller than pivot)
    to left of pivot and all greater elements to right
    of pivot */
    static int partition(char arr[], int low, int high, int mod)
    {

        // pivot
        char pivot = arr[high];

        // Index of smaller element
        int i = (low - 1);

        int piv = pivot % mod;
        for (int j = low; j <= high - 1; j++)
        {

            int a = arr[j] % mod;

            // If current element is smaller than or
            // equal to pivot
            // Instead of values, ASCII % m values
            // are compared
            if (a <= piv)
            {

                // Increment index of smaller element
                i++;

                // swap
                char t = arr[i];
                arr[i] = arr[j];
                arr[j] = t;

            }
        }

        char t = arr[i+1];
        arr[i+1] = arr[high];
        arr[high] = t;

        return (i + 1);
    }

    /* The main function that implements QuickSort
    arr[] --> Array to be sorted,
    low --> Starting index,
    high --> Ending index */
    static void quickSort(char arr[], int low, int high, int mod)
    {
        if (low < high)
        {
            /* pi is partitioning index, arr[p] is now
            at right place */
            int pi = partition(arr, low, high, mod);

            // Separately sort elements before
            // partition and after partition
            quickSort(arr, low, pi - 1, mod);
            quickSort(arr, pi + 1, high, mod);
        }
    }

    // Function to print the given array
    static void printArray(char arr[], int size)
    {
        for (int i = 0; i < size; i++)
            System.out.print(arr[i] + " ");
    }

    // Driver code
    public static void main(String [] args)
    {
        char arr[] = { 'g', 'e', 'e', 'k', 's' };
        int n = arr.length;
        int mod = 8;

        // Sort the given array
        quickSort(arr, 0, n - 1, mod);

        // Print the sorted array
        printArray(arr, n);

    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

""" This function takes last element as pivot,
places the pivot element at its correct position
in sorted array, and places all smaller 
(smaller than pivot) to left of pivot and
all greater elements to right of pivot """
def partition(arr, low, high, mod) :

    # pivot
    pivot = ord(arr[high]);

    # Index of smaller element
    i = (low - 1);

    piv = pivot % mod;
    for j in range(low, high) :

        a = ord(arr[j]) % mod;

        # If current element is smaller than or
        # equal to pivot
        # Instead of values, ASCII % m values
        # are compared
        if (a <= piv) :

            # Increment index of smaller element
            i += 1;
            arr[i], arr[j] = arr[j], arr[i]

    arr[i + 1], arr[high] = arr[high], arr[i + 1]

    return (i + 1);

""" The main function that implements QuickSort
arr[] --> Array to be sorted,
low --> Starting index,
high --> Ending index """

def quickSort(arr, low, high, mod) :

    if (low < high) :

        ''' pi is partitioning index,
        arr[p] is now at right place '''
        pi = partition(arr, low, high, mod);

        # Separately sort elements before
        # partition and after partition
        quickSort(arr, low, pi - 1, mod);
        quickSort(arr, pi + 1, high, mod);

        return arr

# Function to print the given array
def printArray(arr, size) :

    for i in range(0, size) :
        print(arr[i], end = " ");

# Driver code
if __name__ == "__main__" :

    arr = [ 'g', 'e', 'e', 'k', 's' ];
    n = len(arr);
    mod = 8;

    # Sort the given array
    arr = quickSort(arr, 0, n - 1, mod);

    # Print the sorted array
    printArray(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    /* This function takes last element as pivot, places
    the pivot element at its correct position in sorted
        array, and places all smaller (smaller than pivot)
    to left of pivot and all greater elements to right
    of pivot */
    static int partition(char []arr, int low, int high, int mod)
    {

        // pivot
        char pivot = arr[high];

        // Index of smaller element
        int i = (low - 1);
        char t;
        int piv = pivot % mod;
        for (int j = low; j <= high - 1; j++)
        {

            int a = arr[j] % mod;
            // If current element is smaller than o
            // equal to pivot
            // Instead of values, ASCII % m values
            // are compared
            if (a <= piv)
            {

                // Increment index of smaller element
                i++;

                // swap
                t = arr[i];
                arr[i] = arr[j];
                arr[j] = t;

            }
        }

        t = arr[i+1];
        arr[i+1] = arr[high];
        arr[high] = t;

        return (i + 1);
    }

    /* The main function that implements QuickSort
    arr[] --> Array to be sorted,
    low --> Starting index,
    high --> Ending index */
    static void quickSort(char []arr, int low, int high, int mod)
    {
        if (low < high)
        {
            /* pi is partitioning index, arr[p] is now
            at right place */
            int pi = partition(arr, low, high, mod);

            // Separately sort elements before
            // partition and after partition
            quickSort(arr, low, pi - 1, mod);
            quickSort(arr, pi + 1, high, mod);
        }
    }

    // Function to print the given array
    static void printArray(char []arr, int size)
    {
        for (int i = 0; i < size; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        char []arr = { 'g', 'e', 'e', 'k', 's' };
        int n = arr.Length;
        int mod = 8;

        // Sort the given array
        quickSort(arr, 0, n - 1, mod);

        // Print the sorted array
        printArray(arr, n);

    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
// JavaScript implementation of the approach

    /* This function takes last element as pivot, places
    the pivot element at its correct position in sorted
        array, and places all smaller (smaller than pivot)
    to left of pivot and all greater elements to right
    of pivot */
    function partition( arr, low, high, mod)
    {

        // pivot
        var pivot = arr[high];

        // Index of smaller element
        var i = (low - 1);

        var piv = pivot % mod;
        for (var j = low; j <= high - 1; j++)
        {

            var a = arr[j] % mod;

            // If current element is smaller than or
            // equal to pivot
            // Instead of values, ASCII % m values
            // are compared
            if (a <= piv)
            {

                // Increment index of smaller element
                i++;

                // swap
                var t = arr[i];
                arr[i] = arr[j];
                arr[j] = t;

            }
        }

        var t = arr[i+1];
        arr[i+1] = arr[high];
        arr[high] = t;

        return (i + 1);
    }

    /* The main function that implements QuickSort
    arr[] --> Array to be sorted,
    low --> Starting index,
    high --> Ending index */
    function quickSort(arr, low, high, mod)
    {
        if (low < high)
        {
            /* pi is partitioning index, arr[p] is now
            at right place */
            var pi = partition(arr, low, high, mod);

            // Separately sort elements before
            // partition and after partition
            quickSort(arr, low, pi - 1, mod);
            quickSort(arr, pi + 1, high, mod);
        }
    }

    // Function to print the given array
    function printArray( arr, size)
    {
        for (var i = 0; i < size; i++)
            document.write(arr[i] + " ");
    }

    // Driver code
        var arr = ['g', 'e', 'e', 'k', 's' ];
        var n = arr.length;
        var mod = 8;

        // Sort the given array
        quickSort(arr, 0, n - 1, mod);

        // Print the sorted array
        printArray(arr, n);

// This code is contributed by shivanisinghss2110
```

**Output:** 

```
k s e e g
```

***时间复杂度:** O(n * log n)*

***辅助空间:** O(1)*

**方法 2:** 排序也可以使用 [std::sort()](https://www.geeksforgeeks.org/sort-c-stl/) 并修改比较器来完成。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int M;

// Comparator used to sort the array
// according to ASCII % M
bool comparator(char ch1, char ch2)
{
    int i = ch1 % M;
    int j = ch2 % M;
    return (i < j);
}

// Function to print the given array
void printArray(char arr[], int size)
{
    for (int i = 0; i < size; i++)
        cout << arr[i] << " ";
}

// Driver code
int main()
{
    char arr[] = { 'g', 'e', 'e', 'k', 's' };
    int n = sizeof(arr) / sizeof(arr[0]);
    M = 8;

    // Sort the given array
    sort(arr, arr + n, comparator);

    // Print the sorted array
    printArray(arr, n);

    return 0;
}
```

**Output:** 

```
k s e e g
```

***时间复杂度:** O(n * log n)*

***辅助空间:** O(1)*