# 递归冒泡排序

> 原文:[https://www.geeksforgeeks.org/recursive-bubble-sort/](https://www.geeksforgeeks.org/recursive-bubble-sort/)

**背景:**
[【冒泡排序】](https://www.geeksforgeeks.org/bubble-sort/)是最简单的排序算法，如果相邻元素的顺序不对，就重复交换相邻元素。
**示例:**
**第一遍:**
(**5****1**4 2 8)–>(**1****5**4 2 8)，这里，算法比较前两个元素，并交换自 5 > 1。
(1**5****4**2 8)–>(1**4****5**2 8)、互换自 5>4
(1 4**5**T32】28)–>(1 4**2**T36】58)、 交换自 5>2
(1 4 2**5****8**)–>(1 4 2**5****8**)现在，由于这些元素已经按顺序排列(8 > 5)，算法不会交换它们。
**第二遍:**
(**1**T53】42 5 8)–>(**1**T57】42 5 8)
(1**4**T62】25 8)–>(1**2**T66】4 互换自 4>2
(1 2**4**T71】58)–>(1 2**4**T75】58)
(1 2 4**5**T80】8)–>(1 2 4**5**T84】8【t88 算法需要一个**整体**通过，没有任何**的**交换才知道排序。
**第三关:**
(**1****2**4 5 8)–>(**1**T101】24 5 8)
(1**2**T106】45 8)–>(1**2**T110】4【t11
(1 2 4**5****8**)–>(1 2 4**5****8**)
以下是迭代冒泡排序算法:

```
// Iterative Bubble Sort
bubbleSort(arr[], n)
{
  for (i = 0; i < n-1; i++)      

     // Last i elements are already in place   
     for (j = 0; j < n-i-1; j++)
     {
         if(arr[j] > arr[j+1])
             swap(arr[j], arr[j+1]);
     }
} 
```

详见[气泡排序](https://www.geeksforgeeks.org/bubble-sort/)。
**如何递归实现？**
递归冒泡排序没有性能/实现上的优势，但是可以作为一个很好的问题来检验自己对冒泡排序和递归的理解。
如果我们仔细看看 Bubble Sort 算法，我们可以注意到在第一遍中，我们将最大的元素移动到末尾(假设按递增顺序排序)。在第二遍中，我们将第二大元素移到倒数第二的位置，以此类推。
**递归思想。**

1.  基本情况:如果数组大小为 1，则返回。
2.  做一遍正常的冒泡排序。此过程修复了当前子阵列的最后一个元素。
3.  除了当前子阵列的最后一个元素之外的所有元素重复出现。

下面是上述想法的实现。

## C++

```
// C/C++ program for recursive implementation
// of Bubble sort
#include <bits/stdc++.h>
using namespace std;

// A function to implement bubble sort
void bubbleSort(int arr[], int n)
{
    // Base case
    if (n == 1)
        return;

    // One pass of bubble sort. After
    // this pass, the largest element
    // is moved (or bubbled) to end.
    for (int i=0; i<n-1; i++)
        if (arr[i] > arr[i+1])
            swap(arr[i], arr[i+1]);

    // Largest element is fixed,
    // recur for remaining array
    bubbleSort(arr, n-1);
}

/* Function to print an array */
void printArray(int arr[], int n)
{
    for (int i=0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

// Driver program to test above functions
int main()
{
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);
    bubbleSort(arr, n);
    printf("Sorted array : \n");
    printArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for recursive implementation
// of Bubble sort

import java.util.Arrays;

public class GFG
{
    // A function to implement bubble sort
    static void bubbleSort(int arr[], int n)
    {
        // Base case
        if (n == 1)
            return;

        // One pass of bubble sort. After
        // this pass, the largest element
        // is moved (or bubbled) to end.
        for (int i=0; i<n-1; i++)
            if (arr[i] > arr[i+1])
            {
                // swap arr[i], arr[i+1]
                int temp = arr[i];
                arr[i] = arr[i+1];
                arr[i+1] = temp;
            }

        // Largest element is fixed,
        // recur for remaining array
        bubbleSort(arr, n-1);
    }

    // Driver Method
    public static void main(String[] args)
    {
        int arr[] = {64, 34, 25, 12, 22, 11, 90};

        bubbleSort(arr, arr.length);

        System.out.println("Sorted array : ");
        System.out.println(Arrays.toString(arr));
    }
}
```

## 蟒蛇 3

```
# Python Program for implementation of
# Recursive Bubble sort
class bubbleSort:
    """
     bubbleSort:
          function:
              bubbleSortRecursive : recursive
                  function to sort array
              __str__ : format print of array
              __init__ : constructor
                  function in python
          variables:
              self.array = contains array
              self.length = length of array
    """

    def __init__(self, array):
        self.array = array
        self.length = len(array)

    def __str__(self):
        return " ".join([str(x)
                        for x in self.array])

    def bubbleSortRecursive(self, n=None):
        if n is None:
            n = self.length

        # Base case
        if n == 1:
            return

        # One pass of bubble sort. After
        # this pass, the largest element
        # is moved (or bubbled) to end.
        for i in range(n - 1):
            if self.array[i] > self.array[i + 1]:
                self.array[i], self.array[i +
                1] = self.array[i + 1], self.array[i]

        # Largest element is fixed,
        #  recur for remaining array
        self.bubbleSortRecursive(n - 1)

# Driver Code
def main():
    array = [64, 34, 25, 12, 22, 11, 90]

    # Creating object for class
    sort = bubbleSort(array)

    # Sorting array
    sort.bubbleSortRecursive()
    print("Sorted array :\n", sort)

if __name__ == "__main__":
    main()

# Code contributed by Mohit Gupta_OMG,
# improved by itsvinayak
```

## C#

```
// C# program for recursive
// implementation of Bubble sort
using System;

class GFG
{

// A function to implement
// bubble sort
static void bubbleSort(int []arr,  
                       int n)
{
    // Base case
    if (n == 1)
        return;

    // One pass of bubble
    // sort. After this pass,
    // the largest element
    // is moved (or bubbled)
    // to end.
    for (int i = 0; i < n - 1; i++)
        if (arr[i] > arr[i + 1])
        {
            // swap arr[i], arr[i+1]
            int temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }

    // Largest element is fixed,
    // recur for remaining array
    bubbleSort(arr, n - 1);
}

// Driver code
static void Main()
{
    int []arr = {64, 34, 25,
                 12, 22, 11, 90};

    bubbleSort(arr, arr.Length);

    Console.WriteLine("Sorted array : ");
    for(int i = 0; i < arr.Length; i++)
    Console.Write(arr[i] + " ");
}
}

// This code is contributed
// by Sam007
```

## java 描述语言

```
<script>
// javascript program for recursive
// implementation of Bubble sort

// A function to implement
// bubble sort
  function bubbleSort(arr, n)
{

    // Base case
    if (n == 1)
        return;

    // One pass of bubble
    // sort. After this pass,
    // the largest element
    // is moved (or bubbled)
    // to end.

    for (var i = 0; i < n - 1; i++)
        if (arr[i] > arr[i + 1])
        {

            // swap arr[i], arr[i+1]
            var temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }

    // Largest element is fixed,
    // recur for remaining array
    bubbleSort(arr, n - 1);
}

// Driver code

    var arr = [64, 34, 25, 12, 22, 11, 90 ]
    bubbleSort(arr, arr.length);
    document.write("Sorted array : " + "<br>");
    for(var i = 0; i < arr.length; i++) {
    document.write(arr[i] + " ");
    }

    // This code is contributed by bunnyram19.
    </script>
```

**输出:**

```
Sorted array :
11 12 22 25 34 64 90
```

本文由**掌门人 Dey** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。