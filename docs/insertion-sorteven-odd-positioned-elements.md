# 插入排序以不同顺序对偶数和奇数位置的元素进行排序

> 原文:[https://www . geeksforgeeks . org/insertion-sort 偶数-奇数-定位-elements/](https://www.geeksforgeeks.org/insertion-sorteven-odd-positioned-elements/)

给了我们一个数组。我们需要按照升序对偶数位置的元素进行排序，按照降序对奇数位置的元素进行排序。我们必须应用[插入排序](https://www.geeksforgeeks.org/insertion-sort/)来对它们进行排序。
例子:

```
Input : a[] = {7, 10, 11, 3, 6, 9, 2, 13, 0}
Output :      11  3   7  9  6  10  2  13  0
Even positioned elements after sorting int 
ascending order : 3 9 10 13
Odd positioned elements after sorting int 
descending order : 11 7 6 2 0
```

我们对偶数位置的元素和奇数位置的元素分别应用插入排序技术，但它们在同一个数组中。循环从第 0 个索引(第 1 个元素)的奇数位置开始，从第 1 个索引(第 2 个元素)的偶数位置开始，并继续增加 2，因为每个交替位置都是奇数/偶数位置。
我们现在简单地对奇数位置和偶数位置应用插入排序过程。奇数位置的元素是 A[0，2，4，…]，偶数位置的元素是 A[1，3，5，7..].因此，它们被视为独立的子阵列，但在同一阵列中。
**对奇数位置的解释:**
第 0 个元素已经排序。现在将第二个元素与第 0 个元素进行比较，然后插入第(i+2)个元素与前一个元素进行比较，直到数组结束。相同的方法适用于阵列中的均匀定位的元素。(这与插入排序技术相同)。

## C++

```
// C++ program to sort even positioned elements
// in ascending order and odd positioned
// elements in descending order.
#include<stdio.h>
#include<stdlib.h>

// Function to calculate the given problem.
void evenOddInsertionSort(int arr[], int n)
{
  for (int i = 2; i < n; i++)
  {
      int j = i-2;
      int temp = arr[i];

      /* checking whether the position is even
        or odd. And after checking applying the
        insertion sort to the given
        positioned elements.*/   

      // checking for odd positioned.
      if ((i+1) & 1 == 1)
      {
         // Inserting even positioned elements
         // in ascending order.
         while (temp >= arr[j] && j >= 0)
         {
            arr[j+2] = arr[j];
            j -= 2;
         }
         arr[j+2] = temp;           
      }

     // sorting the even positioned.
     else {

         // Inserting odd positioned elements
         // in descending order.
         while (temp <= arr[j] && j >= 0)
         {
            arr[j+2] = arr[j];
           j -= 2;
         }
         arr[j+2] = temp;  
      }
   }
}

// A utility function to print an array of size n
void printArray(int arr[], int n)
{
    for (int i=0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

/* Driver program to test insertion sort */
int main()
{
    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr)/sizeof(arr[0]);

    evenOddInsertionSort(arr, n);
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort even positioned elements
// in ascending order and odd positioned
// elements in descending order.

class GFG
{

    // Function to calculate the given problem.
    static void evenOddInsertionSort(int arr[], int n)
    {
        for (int i = 2; i < n; i++)
        {
            int j = i - 2;
            int temp = arr[i];

            /* checking whether the position is even
            or odd. And after checking applying the
            insertion sort to the given
            positioned elements.*/
            // checking for odd positioned.
            if (((i + 1) & 1) == 1)
            {
                // Inserting even positioned elements
                // in ascending order.
                while (j >= 0 && temp >= arr[j])
                {
                    arr[j + 2] = arr[j];
                    j -= 2;
                }
                arr[j + 2] = temp;
            }

            // sorting the even positioned.
            else
            {

                // Inserting odd positioned elements
                // in descending order.
                while (j >= 0 && temp <= arr[j])
                {
                    arr[j + 2] = arr[j];
                    j -= 2;
                }
                arr[j + 2] = temp;
            }
        }
    }

    // A utility function to print an array of size n
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
        {
            System.out.printf("%d ", arr[i]);
        }
        System.out.printf("\n");
    }

    /* Driver program to test insertion sort */
    public static void main(String[] args)
    {
        int arr[] = {12, 11, 13, 5, 6};
        int n = arr.length;

        evenOddInsertionSort(arr, n);
        printArray(arr, n);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to sort even
# positioned elements in ascending
# order and odd positionedelements
# in descending order.

# Function to calculate
# the given problem.
def evenOddInsertionSort(arr, n):

    for i in range(2, n):

        j = i - 2
        temp = arr[i]

        # checking whether the position
        #  is even or odd. And after
        # checking applying the insertion
        # sort to the given
        # positioned elements.

        # checking for odd positioned.
        if ((i + 1) & 1 == 1) :

            # Inserting even positioned elements
            # in ascending order.
            while (temp >= arr[j] and j >= 0):

                arr[j + 2] = arr[j]
                j -= 2

            arr[j + 2] = temp    

        # sorting the even positioned.
        else :

            # Inserting odd positioned elements
            # in descending order.
            while (temp <= arr[j] and j >= 0) :

                arr[j + 2] = arr[j]
                j -= 2

            arr[j + 2] = temp

# A utility function to print an array of size n
def printArray(arr, n):

    for i in range(0, n):
            print(arr[i], end=" ")

# Driver program
arr = [12, 11, 13, 5, 6]
n = len(arr)
evenOddInsertionSort(arr, n)
printArray(arr, n)

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to sort even positioned elements
// in ascending order and odd positioned
// elements in descending order.
using System;

class GFG
{

    // Function to calculate the given problem.
    static void evenOddInsertionSort(int []arr, int n)
    {
        for (int i = 2; i < n; i++)
        {
            int j = i - 2;
            int temp = arr[i];

            /* checking whether the position is even
            or odd. And after checking applying the
            insertion sort to the given
            positioned elements.*/
            // checking for odd positioned.
            if (((i + 1) & 1) == 1)
            {
                // Inserting even positioned elements
                // in ascending order.
                while (j >= 0 && temp >= arr[j])
                {
                    arr[j + 2] = arr[j];
                    j -= 2;
                }
                arr[j + 2] = temp;
            }

            // sorting the even positioned.
            else
            {

                // Inserting odd positioned elements
                // in descending order.
                while (j >= 0 && temp <= arr[j])
                {
                    arr[j + 2] = arr[j];
                    j -= 2;
                }
                arr[j + 2] = temp;
            }
        }
    }

    // A utility function to print an array of size n
    static void printArray(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
        {
            Console.Write("{0} ", arr[i]);
        }
        Console.Write("\n");
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        int []arr = {12, 11, 13, 5, 6};
        int n = arr.Length;

        evenOddInsertionSort(arr, n);
        printArray(arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to sort even positioned elements
// in ascending order and odd positioned
// elements in descending order.

    // Function to calculate the given problem.
    function evenOddInsertionSort(arr, n)
    {
        for (let i = 2; i < n; i++)
        {
            let j = i - 2;
            let temp = arr[i];

            /* checking whether the position is even
            or odd. And after checking applying the
            insertion sort to the given
            positioned elements.*/
            // checking for odd positioned.
            if (((i + 1) & 1) == 1)
            {
                // Inserting even positioned elements
                // in ascending order.
                while (j >= 0 && temp >= arr[j])
                {
                    arr[j + 2] = arr[j];
                    j -= 2;
                }
                arr[j + 2] = temp;
            }

            // sorting the even positioned.
            else
            {

                // Inserting odd positioned elements
                // in descending order.
                while (j >= 0 && temp <= arr[j])
                {
                    arr[j + 2] = arr[j];
                    j -= 2;
                }
                arr[j + 2] = temp;
            }
        }
    }

    // A utility function to print an array of size n
     function printArray(arr, n)
    {
        for (let i = 0; i < n; i++)
        {
            document.write(arr[i] + " ");
        }
        document.write();
    } 

// Driver code

        let arr = [12, 11, 13, 5, 6];
        let n = arr.length;

        evenOddInsertionSort(arr, n);
        printArray(arr, n);

</script>
```

**输出:**

```
13 5 12 11 6 
```

***时间复杂度:** O(n <sup>2</sup> )*

***辅助空间:** O(1)*
在没有插入排序的情况下，有更好的方法来解决这个问题。详见[按升序排列偶数元素，按降序排列奇数元素](https://www.geeksforgeeks.org/sort-even-placed-elements-increasing-odd-placed-decreasing-order/)。