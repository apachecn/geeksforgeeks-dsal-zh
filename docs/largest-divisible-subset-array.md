# 数组中最大的可分子集

> 原文:[https://www . geesforgeks . org/最大可分子集数组/](https://www.geeksforgeeks.org/largest-divisible-subset-array/)

给定一个数组，任务是找出数组中最大的可分子集。如果对于子集中的每一对(x，y)，x 除 y 或 y 除 x，则子集称为可分的。
示例:

```
Input  : arr[] = {1, 16, 7, 8, 4}
Output : 16 8 4 1
In the output subset, for every pair,
either the first element divides second
or second divides first.

Input  : arr[] = {2, 4, 3, 8}
Output : 8 4 2
```

一个简单的解决方案是[生成给定集合](https://www.geeksforgeeks.org/power-set/)的所有子集。对于每个生成的子集，检查它是否可分。最后打印最大的可分子集。
高效解决方案**包括以下步骤。** 

1.  按升序对所有数组元素进行排序。排序的目的是确保一个元素的所有除数都出现在它的前面。
2.  创建一个与输入数组大小相同的数组 divCount[]。divCount[i]存储以 arr[i]结尾的可分子集的大小(在排序数组中)。divCount[i]的最小值应为 1。
3.  遍历所有数组元素。对于每个元素，找到 divCount[j]值最大的除数 arr[j]，并将 divCount[i]的值存储为 divCount[j] + 1。

## C++

```
// C++ program to find largest divisible
// subset in a given array
#include<bits/stdc++.h>
using namespace std;

// Prints largest divisible subset
void findLargest(int arr[], int n)
{
    // We first sort the array so that all divisors
    // of a number are before it.
    sort(arr, arr+n);

    // To store count of divisors of all elements
    vector <int> divCount(n, 1);

    // To store previous divisor in result
    vector <int> prev(n, -1);

    // To store index of largest element in maximum
    // size subset
    int max_ind = 0;

    // In i'th iteration, we find length of chain
    // ending with arr[i]
    for (int i=1; i<n; i++)
    {
        // Consider every smaller element as previous
        // element.
        for (int j=0; j<i; j++)
        {
            if (arr[i]%arr[j] == 0)
            {
                if (divCount[i] < divCount[j] + 1)
                {
                    divCount[i] = divCount[j]+1;
                    prev[i] = j;
                }
            }
        }

        // Update last index of largest subset if size
        // of current subset is more.
        if (divCount[max_ind] < divCount[i])
            max_ind = i;
    }

    // Print result
    int k = max_ind;
    while (k >= 0)
    {
        cout << arr[k] << " ";
        k = prev[k];
    }
}

// Driven code
int main()
{
    int arr[] = {1, 2, 17, 4};
    int n = sizeof(arr)/sizeof(int);
    findLargest(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find largest divisible
// subset in a given arrayimport java.io.*;
import java.util.*;

class DivSubset {

    public static int[][] dp;

    // Prints largest divisible subset
    static void findLargest(int[] arr) {

        // array that maintains the maximum index
        // till which the condition is satisfied
        int divCount[] = new int[arr.length];

        // we will always have atleast one
        // element divisible by itself
        Arrays.fill(divCount, 1);

        // maintain the index of the last increment
        int prev[] = new int[arr.length];
        Arrays.fill(prev, -1);

        // index at which last increment happened
        int max_ind = 0;

        for (int i = 1; i < arr.length; i++) {
            for (int j = 0; j < i; j++) {

                // only increment the maximum index if
                // this iteration will increase it
                if (arr[i] % arr[j] == 0 &&
                    divCount[i] < divCount[j] + 1) {
                    prev[i] = j;
                    divCount[i] = divCount[j] + 1;

                }

            }
        // Update last index of largest subset if size
        // of current subset is more.
            if (divCount[i] > divCount[max_ind])
                max_ind = i;
        }

        // Print result
        int k = max_ind;
        while (k >= 0) {
            System.out.print(arr[k] + " ");
            k = prev[k];
        }

    }

    public static void main(String[] args) {

        int[] x = { 1, 2, 17, 4};

        // sort the array
        Arrays.sort(x);

        findLargest(x);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find largest divisible
# subset in a given array

# Prints largest divisible subset
def findLargest(arr, n):

    # We first sort the array so that all divisors
    # of a number are before it.
    arr.sort(reverse = False)

    # To store count of divisors of all elements
    divCount = [1 for i in range(n)]

    # To store previous divisor in result
    prev = [-1 for i in range(n)]

    # To store index of largest element in maximum
    # size subset
    max_ind = 0

    # In i'th iteration, we find length of chain
    # ending with arr[i]
    for i in range(1,n):
        # Consider every smaller element as previous
        # element.
        for j in range(i):
            if (arr[i] % arr[j] == 0):
                if (divCount[i] < divCount[j] + 1):
                    divCount[i] = divCount[j]+1
                    prev[i] = j

        # Update last index of largest subset if size
        # of current subset is more.
        if (divCount[max_ind] < divCount[i]):
            max_ind = i

    # Print result
    k = max_ind
    while (k >= 0):
        print(arr[k],end = " ")
        k = prev[k]

# Driven code
if __name__ == '__main__':
    arr = [1, 2, 17, 4]
    n = len(arr)
    findLargest(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find largest divisible
// subset in a given array
using System;

public class DivSubset
{
    public static int[,] dp;

    // Prints largest divisible subset
    static void findLargest(int[] arr)
    {

        // array that maintains the maximum index
        // till which the condition is satisfied
        int []divCount = new int[arr.Length];

        // we will always have atleast one
        // element divisible by itself
        for(int i = 0; i < arr.Length; i++)
            divCount[i] = 1;

        // maintain the index of the last increment
        int []prev = new int[arr.Length];
        for(int i = 0; i < arr.Length; i++)
            prev[i] = -1;

        // index at which last increment happened
        int max_ind = 0;

        for (int i = 1; i < arr.Length; i++)
        {
            for (int j = 0; j < i; j++)
            {

                // only increment the maximum index if
                // this iteration will increase it
                if (arr[i] % arr[j] == 0 &&
                    divCount[i] < divCount[j] + 1)
                {
                    prev[i] = j;
                    divCount[i] = divCount[j] + 1;

                }

            }

        // Update last index of largest subset if size
        // of current subset is more.
            if (divCount[i] > divCount[max_ind])
                max_ind = i;
        }

        // Print result
        int k = max_ind;
        while (k >= 0)
        {
            Console.Write(arr[k] + " ");
            k = prev[k];
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] x = { 1, 2, 17, 4};

        // sort the array
        Array.Sort(x);

        findLargest(x);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find largest divisible
// subset in a given arrayimport java.io.*;

let dp;

// Prints largest divisible subset
function findLargest(arr)
{
    // array that maintains the maximum index
        // till which the condition is satisfied
        let divCount = new Array(arr.length);

        // we will always have atleast one
        // element divisible by itself
        for(let i=0;i<arr.length;i++)
        {
            divCount[i]=1;
        }

        // maintain the index of the last increment
        let prev = new Array(arr.length);
        for(let i=0;i<arr.length;i++)
        {
            prev[i]=-1;
        }

        // index at which last increment happened
        let max_ind = 0;

        for (let i = 1; i < arr.length; i++) {
            for (let j = 0; j < i; j++) {

                // only increment the maximum index if
                // this iteration will increase it
                if (arr[i] % arr[j] == 0 &&
                    divCount[i] < divCount[j] + 1) {
                    prev[i] = j;
                    divCount[i] = divCount[j] + 1;

                }

            }
        // Update last index of largest subset if size
        // of current subset is more.
            if (divCount[i] > divCount[max_ind])
                max_ind = i;
        }

        // Print result
        let k = max_ind;
        while (k >= 0) {
            document.write(arr[k] + " ");
            k = prev[k];
        }
}

let x=[1, 2, 17, 4];
// sort the array
x.sort(function(a,b){return a-b;});

findLargest(x);

// This code is contributed by rag2127

</script>
```

**输出:**

```
4 2 1
```

**时间复杂度:**O(n)<sup>2</sup>)
**辅助空间:** O(n)
本文由 [**丹麦语 _RAZA**](https://www.facebook.com/danish.raza.98096721) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。