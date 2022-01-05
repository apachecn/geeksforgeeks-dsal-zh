# 在线性时间内对从 0 到 n^2-1 范围内的 n 个数字进行排序

> 原文:[https://www . geesforgeks . org/sort-n-numbers-range-0-N2-1-linear-time/](https://www.geeksforgeeks.org/sort-n-numbers-range-0-n2-1-linear-time/)

给定一个大小为 n 的数字数组。还给定数组元素的范围为 0 到 n<sup>2</sup>–1。以线性时间对给定数组进行排序。

**示例:**

```
Since there are 5 elements, the elements can be from 0 to 24.
Input: arr[] = {0, 23, 14, 12, 9}
Output: arr[] = {0, 9, 12, 14, 23}

Since there are 3 elements, the elements can be from 0 to 8.
Input: arr[] = {7, 0, 2}
Output: arr[] = {0, 2, 7}
```

**解决方案:**如果我们使用[计数排序](https://www.geeksforgeeks.org/counting-sort/)，将花费 O(n^2 时间，因为给定的范围是 n^2.大小使用任何基于比较的排序，如[合并排序](http://geeksquiz.com/merge-sort/)、[堆排序](http://geeksquiz.com/heap-sort/)，..等需要 0(nLogn)时间。
现在问题来了，如何在 0(n)中做到这一点？首先，可能吗？我们可以使用问题中给出的数据吗？n 个数字，范围从 0 到 n<sup>2</sup>–1？

想法是使用[基数排序](https://www.geeksforgeeks.org/radix-sort/)。以下是标准基数排序算法。

```
1) Do following for each digit i where i varies from least 
   significant digit to the most significant digit.
…………..a) Sort input array using counting sort (or any stable 
         sort) according to the i’th digit
```

假设输入整数中有 d 个数字。基数排序需要 O(d*(n+b))时间，其中 b 是表示数字的基数，例如，对于十进制系统，b 是 10。由于 n <sup>2</sup> -1 是最大可能值，d 的值将是 O(log <sub>b</sub> (n))。所以整体时间复杂度是 O((n+b)*O(log <sub>b</sub> (n))。这看起来比基于比较的排序算法对于一个大 k 的时间复杂度更高，想法是改变基数 b，如果我们将 b 设置为 n，O(log <sub>b</sub> (n))的值变成 O(1)，整体时间复杂度变成 O(n)。

```
arr[] = {0, 10, 13, 12, 7}

Let us consider the elements in base 5\. For example 13 in
base 5 is 23, and 7 in base 5 is 12.
arr[] = {00(0), 20(10), 23(13), 22(12), 12(7)}

After first iteration (Sorting according to the last digit in 
base 5),  we get.
arr[] = {00(0), 20(10), 12(7), 22(12), 23(13)}

After second iteration, we get
arr[] = {00(0), 12(7), 20(10), 22(12), 23(13)}
```

下面是对大小为 n 的数组进行排序的实现，其中元素的范围从 0 到 n<sup>2</sup>–1。

## C++

```
#include<iostream>
using namespace std;

// A function to do counting sort of arr[] according to
// the digit represented by exp.
int countSort(int arr[], int n, int exp)
{

    int output[n]; // output array
    int i, count[n] ;
    for (int i=0; i < n; i++)
       count[i] = 0;

    // Store count of occurrences in count[]
    for (i = 0; i < n; i++)
        count[ (arr[i]/exp)%n ]++;

    // Change count[i] so that count[i] now contains actual
    // position of this digit in output[]
    for (i = 1; i < n; i++)
        count[i] += count[i - 1];

    // Build the output array
    for (i = n - 1; i >= 0; i--)
    {
        output[count[ (arr[i]/exp)%n] - 1] = arr[i];
        count[(arr[i]/exp)%n]--;
    }

    // Copy the output array to arr[], so that arr[] now
    // contains sorted numbers according to current digit
    for (i = 0; i < n; i++)
        arr[i] = output[i];
}

// The main function to that sorts arr[] of size n using Radix Sort
void sort(int arr[], int n)
{
    // Do counting sort for first digit in base n. Note that
    // instead of passing digit number, exp (n^0 = 1) is passed.
    countSort(arr, n, 1);

    // Do counting sort for second digit in base n. Note that
    // instead of passing digit number, exp (n^1 = n) is passed.
    countSort(arr, n, n);
}

// A utility function to print an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver program to test above functions
int main()
{
    // Since array size is 7, elements should be from 0 to 48
    int arr[] = {40, 12, 45, 32, 33, 1, 22};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Given array is n";
    printArr(arr, n);

    sort(arr, n);

    cout << "nSorted array is n";
    printArr(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to sort an array of size n where elements are
// in range from 0 to n^2 – 1.
class Sort1ToN2
{
    // A function to do counting sort of arr[] according to
    // the digit represented by exp.
    void countSort(int arr[], int n, int exp)
    {
        int output[] = new int[n]; // output array
        int i, count[] = new int[n] ;
        for (i=0; i < n; i++)
           count[i] = 0;

        // Store count of occurrences in count[]
        for (i = 0; i < n; i++)
            count[ (arr[i]/exp)%n ]++;

        // Change count[i] so that count[i] now contains actual
        // position of this digit in output[]
        for (i = 1; i < n; i++)
            count[i] += count[i - 1];

        // Build the output array
        for (i = n - 1; i >= 0; i--)
        {
            output[count[ (arr[i]/exp)%n] - 1] = arr[i];
            count[(arr[i]/exp)%n]--;
        }

        // Copy the output array to arr[], so that arr[] now
        // contains sorted numbers according to current digit
        for (i = 0; i < n; i++)
            arr[i] = output[i];
    }

    // The main function to that sorts arr[] of size n using Radix Sort
    void sort(int arr[], int n)
    {
        // Do counting sort for first digit in base n. Note that
        // instead of passing digit number, exp (n^0 = 1) is passed.
        countSort(arr, n, 1);

        // Do counting sort for second digit in base n. Note that
        // instead of passing digit number, exp (n^1 = n) is passed.
        countSort(arr, n, n);
    }

    // A utility function to print an array
    void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i]+" ");
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        Sort1ToN2 ob = new Sort1ToN2();

        // Since array size is 7, elements should be from 0 to 48
        int arr[] = {40, 12, 45, 32, 33, 1, 22};
        int n = arr.length;
        System.out.println("Given array");
        ob.printArr(arr, n);

        ob.sort(arr, n);

        System.out.println("Sorted array");
        ob.printArr(arr, n);
    }
}
/*This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# Python3 the implementation to sort an
# array of size n

# A function to do counting sort of arr[]
# according to the digit represented by exp.
def countSort(arr, n, exp):
    output = [0] * n # output array
    count = [0] * n
    for i in range(n):
        count[i] = 0

    # Store count of occurrences in count[]
    for i in range(n):
        count[ (arr[i] // exp) % n ] += 1

    # Change count[i] so that count[i] now contains
    # actual position of this digit in output[]
    for i in range(1, n):
        count[i] += count[i - 1]

    # Build the output array
    for i in range(n - 1, -1, -1):

        output[count[ (arr[i] // exp) % n] - 1] = arr[i]
        count[(arr[i] // exp) % n] -= 1

    # Copy the output array to arr[], so that
    # arr[] now contains sorted numbers according
    # to current digit
    for i in range(n):
        arr[i] = output[i]

# The main function to that sorts arr[] of
# size n using Radix Sort
def sort(arr, n) :

    # Do counting sort for first digit in base n.
    # Note that instead of passing digit number,
    # exp (n^0 = 1) is passed.
    countSort(arr, n, 1)

    # Do counting sort for second digit in base n.
    # Note that instead of passing digit number,
    # exp (n^1 = n) is passed.
    countSort(arr, n, n)

# Driver Code
if __name__ =="__main__":

    # Since array size is 7, elements should
    # be from 0 to 48
    arr = [40, 12, 45, 32, 33, 1, 22]
    n = len(arr)
    print("Given array is")
    print(*arr)

    sort(arr, n)

    print("Sorted array is")
    print(*arr)

# This code is contribute by
# Shubham Singh(SHUBHAMSINGH10)
```

## C#

```
// C# program to sort an array of
// size n where elements are
// in range from 0 to n^2 – 1.
using System;

class GFG {

    // A function to do counting
    // sort of arr[] according to
    // the digit represented by exp.
    static void countSort(int[] arr,
                          int n,
                          int exp)
    {

        // output array
        int[] output = new int[n];
        int[] count = new int[n] ;
        int i;
        for (i = 0; i < n; i++)
        count[i] = 0;

        // Store count of
        // occurrences in count[]
        for (i = 0; i < n; i++)
            count[(arr[i] / exp) % n ]++;

        // Change count[i] so that
        // count[i] now contains actual
        // position of this digit in output[]
        for (i = 1; i < n; i++)
            count[i] += count[i - 1];

        // Build the output array
        for (i = n - 1; i >= 0; i--)
        {
            output[count[(arr[i] /
                   exp) % n] - 1] = arr[i];
            count[(arr[i] / exp) % n]--;
        }

        // Copy the output array to
        // arr[], so that arr[] now
        // contains sorted numbers
        // according to current digit
        for (i = 0; i < n; i++)
            arr[i] = output[i];
    }

    // The main function to that
    // sorts arr[] of size n
    // using Radix Sort
    static void sort(int[] arr, int n)
    {

        // Do counting sort for first
        // digit in base n. Note that
        // instead of passing digit number,
        // exp (n^0 = 1) is passed.
        countSort(arr, n, 1);

        // Do counting sort for second
        // digit in base n. Note that
        // instead of passing digit number,
        // exp (n^1 = n) is passed.
        countSort(arr, n, n);
    }

    // A utility function
    // to print an array
    static void printArr(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver Code
    static public void Main ()
    {

        // Since array size is 7,
        // elements should be
        // from 0 to 48
        int[] arr = {40, 12, 45, 32, 33, 1, 22};
        int n = arr.Length;
        Console.WriteLine("Given array");
        printArr(arr, n);

        sort(arr, n);

        Console.WriteLine("\nSorted array");
        printArr(arr, n);
    }
}

// This code is contributed by Ajit.
```

## java 描述语言

```
<script>

// Javascript program to sort an array of
// size n where elements are
// in range from 0 to n^2 – 1.

// A function to do counting
// sort of arr[] according to
// the digit represented by exp.
function countSort(arr, n, exp)
{

    // Output array
    let output = new Array(n);
    let count = new Array(n);

    count.fill(0);
    output.fill(0);
    let i;

    for(i = 0; i < n; i++)
        count[i] = 0;

    // Store count of
    // occurrences in count[]
    for(i = 0; i < n; i++)
        count[parseInt(arr[i] / exp, 10) % n ]++;

    // Change count[i] so that
    // count[i] now contains actual
    // position of this digit in output[]
    for(i = 1; i < n; i++)
        count[i] += count[i - 1];

    // Build the output array
    for (i = n - 1; i >= 0; i--)
    {
        output[count[parseInt(
            arr[i] / exp, 10) % n] - 1] = arr[i];
        count[parseInt(arr[i] / exp, 10) % n]--;
    }

    // Copy the output array to
    // arr[], so that arr[] now
    // contains sorted numbers
    // according to current digit
    for(i = 0; i < n; i++)
        arr[i] = output[i];
}

// The main function to that
// sorts arr[] of size n
// using Radix Sort
function sort(arr, n)
{

    // Do counting sort for first
    // digit in base n. Note that
    // instead of passing digit number,
    // exp (n^0 = 1) is passed.
    countSort(arr, n, 1);

    // Do counting sort for second
    // digit in base n. Note that
    // instead of passing digit number,
    // exp (n^1 = n) is passed.
    countSort(arr, n, n);
}

// A utility function
// to print an array
function printArr(arr, n)
{
    for(let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Driver code

// Since array size is 7,
// elements should be
// from 0 to 48
let arr = [ 40, 12, 45, 32, 33, 1, 22 ];
let n = arr.length;

document.write("Given array" + "</br>");
printArr(arr, n);

sort(arr, n);

document.write("</br>Sorted array" + "</br>");
printArr(arr, n);

// This code is contributed by divyesh072019

</script>
```

**输出:**

```
Given array is
40 12 45 32 33 1 22
Sorted array is
1 12 22 32 33 40 45
```

**范围从 1 到 n <sup>2</sup> 如何排序？**
如果范围从 1 到 n n <sup>2</sup> ，则不能直接应用上述过程，必须进行更改。考虑 n = 100，范围从 1 到 10000。因为基数是 100，所以一个数字必须从 0 到 99，并且数字中应该有 2 个数字。但是数字 10000 有超过 2 位数。所以要在 1 到 n <sup>2</sup> 的范围内对数字进行排序，我们可以使用以下过程。
1)将所有数字减 1。
2)由于现在的范围是 0 到 n <sup>2</sup> ，按照上面的实现做两次计数排序。
3)元素排序后，将所有数字加 1，得到原始数字。

**如果范围从 0 到 n^3 -1，如何排序？**
由于基数 n 可以有 3 位数字，我们需要调用计数排序 3 次。
本文由**巴特斯**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息