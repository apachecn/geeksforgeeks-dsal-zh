# 查找数组中每个元素的剩余计数

> 原文:[https://www . geesforgeks . org/find-super Asser-数组中每个元素的计数/](https://www.geeksforgeeks.org/find-surpasser-count-of-each-element-in-array/)

数组中一个元素的余数是它右边的一个更大的元素，因此 x[j]是 x[i]的余数，如果 i < j and x[i] < x[j]. The surpasser count of an element is the number of surpassers. Given an array of distinct integers, for each element of the array find its surpasser count i.e. count the number of elements to the right that are greater than that element.
**例:**

```
Input:  [2, 7, 5, 3, 0, 8, 1]
Output: [4, 1, 1, 1, 2, 0, 0]
```

**方法 1(天真)**
天真的解决方案是运行两个循环。对于数组中的每一个元素，我们计算其右边所有大于它的元素。这个解决方案的复杂度是 O(n <sup>2</sup> )

## C++

```
// Naive C++ program to find surpasser count of
// each element in array
#include <bits/stdc++.h>
using namespace std;

// Function to find surpasser count of each element
// in array
void findSurpasser(int arr[], int n)
{
    for (int i = 0; i < n; i++)
    {
        // stores surpasser count for element arr[i]
        int count = 0;
        for (int j = i + 1; j < n; j++)
            if (arr[j] > arr[i])
                count++;

        cout << count << " ";
    }
}

/* Function to print an array */
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

/* Driver program to test above functions */
int main()
{
    int arr[] = { 2, 7, 5, 3, 0, 8, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Given array is \n");
    printArray(arr, n);

    printf("Surpasser Count of array is \n");
    findSurpasser(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Naive Java program to find surpasser count
// of each element in array
import java.io.*;

class GFG {

    // Function to find surpasser count of
    // each element in array
    static void findSurpasser(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
        {

            // stores surpasser count for
            // element arr[i]
            int count = 0;
            for (int j = i + 1; j < n; j++)
                if (arr[j] > arr[i])
                    count++;

            System.out.print(count +" ");
        }
    }

    /* Function to print an array */
    static void printArray(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print( arr[i] + " ");

        System.out.println();
    }

    // Driver program to test above functions
    public static void main (String[] args)
    {
        int arr[] = { 2, 7, 5, 3, 0, 8, 1 };
        int n = arr.length;

        System.out.println("Given array is ");
        printArray(arr, n);

        System.out.println("Surpasser Count of"
                               + " array is ");
        findSurpasser(arr, n);
    }
}

// This code is contributed by Anuj_67.
```

## 蟒蛇 3

```
# Naive Python3 program to find
# surpasser count of each element in array

# Function to find surpasser count of
# each element in array
def findSurpasser(arr, n):

    for i in range(0, n):

        # stores surpasser count for element
        # arr[i]
        count = 0;

        for j in range (i + 1, n):
            if (arr[j] > arr[i]):
                count += 1

        print(count, end = " ")

# Function to print an array
def printArray(arr, n):

    for i in range(0, n):
        print(arr[i], end = " ")

# Driver program to test above functions
arr = [2, 7, 5, 3, 0, 8, 1 ]
n = len(arr)

print("Given array is")
printArray(arr , n)

print("\nSurpasser Count of array is");
findSurpasser(arr , n)

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// Naive C# program to find surpasser count
// of each element in array
using System;

class GFG {

    // Function to find surpasser count of
    // each element in array
    static void findSurpasser(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
        {

            // stores surpasser count for
            // element arr[i]
            int count = 0;
            for (int j = i + 1; j < n; j++)
                if (arr[j] > arr[i])
                    count++;

            Console.Write(count + " ");
        }
    }

    /* Function to print an array */
    static void printArray(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write( arr[i] + " ");

        Console.WriteLine();
    }

    // Driver program to test above functions
    public static void Main ()
    {
        int []arr = { 2, 7, 5, 3, 0, 8, 1 };
        int n = arr.Length;

        Console.WriteLine("Given array is ");
        printArray(arr, n);

        Console.WriteLine("Surpasser Count of"
                            + " array is ");
        findSurpasser(arr, n);
    }
}

// This code is contributed by Anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Naive PHP program to find
// surpasser count of each
// element in array

// Function to find surpasser
// count of each element in array
function findSurpasser($arr, $n)
{
    for ( $i = 0; $i < $n; $i++)
    {
        // stores surpasser count
        // for element arr[i]
        $count = 0;
        for ( $j = $i + 1; $j < $n; $j++)
            if ($arr[$j] > $arr[$i])
                $count++;

        echo $count , " ";
    }
}

/* Function to print an array */
function printArray( $arr, $n)
{
    for ( $i = 0; $i < $n; $i++)
        echo $arr[$i]," ";
        echo "\n";
}

// Driver Code
$arr = array( 2, 7, 5, 3, 0, 8, 1 );
$n = count($arr);

echo "Given array is \n";
printArray($arr, $n);

echo "Surpasser Count of array is \n";
findSurpasser($arr, $n);

// This code is contributed by Anuj_67.
?>
```

## java 描述语言

```
<script>

// Naive Javascript program to find surpasser count
// of each element in array

    // Function to find surpasser count of
    // each element in array
    function findSurpasser(arr, n)
    {
        for (let i = 0; i < n; i++)
        {

            // stores surpasser count for
            // element arr[i]
            let count = 0;
            for (let j = i + 1; j < n; j++)
                if (arr[j] > arr[i])
                    count++;

            document.write(count +" ");
        }
    }

    /* Function to print an array */
    function printArray(arr, n)
    {
        for (let i = 0; i < n; i++)
            document.write( arr[i] + " ");

        document.write();
    }

// Driver Code

        let arr = [ 2, 7, 5, 3, 0, 8, 1 ];
        let n = arr.length;

        document.write("Given array is " + "<br />");
        printArray(arr, n);

        document.write("<br />");

        document.write("Surpasser Count of"
                               + " array is " + "<br />");
        findSurpasser(arr, n);

</script>
```

**输出:**

```
Given array is 
2 7 5 3 0 8 1 
Surpasser Count of array is 
4 1 1 1 2 0 0
```

**时间复杂度:** O(n <sup>2</sup> )
**方法 2(使用合并排序)**
对于数组的任何元素，如果我们知道它右边的元素数量少于那个元素，我们可以很容易地找出右边大于那个元素的元素数量。其思想是使用合并排序来计算数组中每个元素的反转次数。因此，位置 I 处元素的剩余计数将等于该位置的“n–I–反转计数”，其中 n 是数组的大小。
这里已经讨论了如何求全阵[的逆序计数。我们修改了所讨论的方法，以找到数组中每个元素的求逆次数，而不是返回整个数组的求逆次数。此外，由于数组的所有元素都是不同的，我们维护一个存储数组每个元素的反转计数的映射。
以下是上述思路的 C++实现–](https://www.geeksforgeeks.org/counting-inversions/) 

## C++

```
// C++ program to find surpasser count of each element
// in array
#include <bits/stdc++.h>
using namespace std;

/* Function to merge the two haves arr[l..m] and
   arr[m+1..r] of array arr[] */
int merge(int arr[], int l, int m, int r,
          unordered_map<int, int> &hm)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;

    /* create temp arrays */
    int L[n1], R[n2];

    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];

    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    /* Merge the temp arrays back into arr[l..r]*/
    i = 0, j = 0, k = l;
    int c = 0;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            // increment inversion count of L[i]
            hm[L[i]] += c;
            arr[k++] = L[i++];
        }
        else
        {
            arr[k++] = R[j++];

            // inversion found
            c++;
        }
    }

    /* Copy the remaining elements of L[], if
    there are any */
    while (i < n1)
    {
        hm[L[i]] += c;
        arr[k++] = L[i++];
    }

    /* Copy the remaining elements of R[], if
    there are any */
    while (j < n2)
        arr[k++] = R[j++];
}

/* l is for left index and r is right index of
the sub-array of arr to be sorted */
int mergeSort(int arr[], int l, int r,
              unordered_map<int, int> &hm)
{
    if (l < r)
    {
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m, hm);
        mergeSort(arr, m + 1, r, hm);
        merge(arr, l, m, r, hm);
    }
}

/* Function to print an array */
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

void findSurpasser(int arr[], int n)
{
    // To store inversion count for elements
    unordered_map<int, int> hm;

    // To store copy of array
    int dup[n];
    memcpy(dup, arr, n*sizeof(arr[0]));

    // Sort the copy and store inversion count
    // for each element.
    mergeSort(dup, 0, n - 1, hm);

    printf("Surpasser Count of array is \n");
    for (int i = 0; i < n; i++)
        printf("%d ", (n - 1) - i - hm[arr[i]]);
}

/* Driver program to test above functions */
int main()
{
    int arr[] = { 2, 7, 5, 3, 0, 8, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Given array is \n");
    printArray(arr, n);

    findSurpasser(arr, n);

    return 0;
}
```

**输出:**

```
Given array is 
2 7 5 3 0 8 1 
Surpasser Count of array is 
4 1 1 1 2 0 0
```

上述解的时间复杂度为 0(nlogn)。
本文由**阿迪亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。