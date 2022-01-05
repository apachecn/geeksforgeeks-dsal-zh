# 形成不同元素的阵列，每个元素是来自每个阵列的元素的总和

> 原文:[https://www . geeksforgeeks . org/form-a-array-of-distinct-elements-from-from-array-from-element-from-array-from-element-from-element-from-array/](https://www.geeksforgeeks.org/form-an-array-of-distinct-elements-with-each-element-as-sum-of-an-element-from-each-array/)

给定两个包含不同元素的大小相等的数组 **arr1[]** 和 **arr2[]** ，任务是找到另一个包含不同元素的数组，这样第三个数组的元素由 arr1[]和 arr2[]的一对一元素相加而成。

**示例:**

> **输入:** arr[] = {1，7，8，3}，arr2[] = {6，5，10，2}
> **输出:** 3 8 13 18
> **解释:**
> **指数 0:** 1 + 2 = 3
> **指数 1:** 3 + 5 = 8
> **指数 2:** 7 + 6 = 13
> **指数**
> 
> **输入:** arr1[] = {15，20，3}，arr2[] = {5，4，3}
> **输出:** 6 19 25
> **解释:**
> **指数 0:** 3 + 3 = 6
> **指数 1:** 15 + 4 = 19
> **指数 2:** 20 + 5 = 25
> 的元素

**方法:**这个问题的关键观察是两个数组都包含不同的元素，如果我们对数组进行排序，那么数组对应元素的和也会形成不同的元素。
上述方法的分步算法描述如下-

*   按升序或降序对两个数组进行排序。
*   初始化另一个数组(比如 **arr3[]** )来存储由数组的两个元素之和形成的不同元素
*   迭代从 0 到数组长度的循环
*   第三个数组的元素将是前两个数组元素的总和-

```
 arr3[i] = arr1[i] + arr2[i]
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find distinct
// array such that the elements of the
// array is sum of two
// elements of other two arrays

#include <bits/stdc++.h>
using namespace std;

// Function to find a distinct array
// such that elements of the third
// array is sum of two elements
// of other two arrays
void thirdArray(int a[], int b[], int n)
{
    int c[n];
    sort(a, a + n);
    sort(b, b + n);

    // Loop to find the array
    // such that each element is
    // sum of other two elements
    for (int i = 0; i < n; i++) {
        c[i] = a[i] + b[i];
    }

    // Loop to print the array
    for (int i = 0; i < n; i++)
        cout << c[i] << " ";
}

// Driver code
int main()
{
    int a[] = { 1, 7, 8, 3 };
    int b[] = { 6, 5, 10, 2 };

    int size = sizeof(a) / sizeof(a[0]);

    thirdArray(a, b, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find distinct
// array such that the elements of the
// array is sum of two
// elements of other two arrays
import java.util.*;

class GFG
{
    // Function to find a distinct array
    // such that elements of the third
    // array is sum of two elements
    // of other two arrays
    static void thirdArray(int a[], int b[], int n)
    {
        int[] c = new int[20];;
        Arrays.sort(a);
        Arrays.sort(b);

        // Loop to find the array
        // such that each element is
        // sum of other two elements
        for (int i = 0; i < n; i++) {
            c[i] = a[i] + b[i];
        }

        // Loop to print the array
        for (int i = 0; i < n; i++)
            System.out.print(c[i] + " ");
    }

    // Driver code
    public static void main(String args[])
    {
        int a[] = { 1, 7, 8, 3 };
        int b[] = { 6, 5, 10, 2 };

        int size = a.length;

        thirdArray(a, b, size);
    }
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 implementation to find distinct
# array such that the elements of the
# array is sum of two
# elements of other two arrays

# Function to find a distinct array
# such that elements of the third
# array is sum of two elements
# of other two arrays
def thirdArray(a, b, n):

    c = [0]*n
    a = sorted(a)
    b = sorted(b)

    # Loop to find the array
    # such that each element is
    # sum of other two elements
    for i in range(n):
        c[i] = a[i] + b[i]

    # Loop to print the array
    for i in range(n):
        print(c[i], end=" ")

# Driver code
a = [1, 7, 8, 3]
b = [6, 5, 10, 2]

size = len(a)

thirdArray(a, b, size)

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# implementation to find distinct
// array such that the elements of the
// array is sum of two
// elements of other two arrays
using System;

class GFG
{
    // Function to find a distinct array
    // such that elements of the third
    // array is sum of two elements
    // of other two arrays
    static void thirdArray(int []a, int []b, int n)
    {
        int[] c = new int[20];;
        Array.Sort(a);
        Array.Sort(b);

        // Loop to find the array
        // such that each element is
        // sum of other two elements
        for (int i = 0; i < n; i++) {
            c[i] = a[i] + b[i];
        }

        // Loop to print the array
        for (int i = 0; i < n; i++)
            Console.Write(c[i] + " ");
    }

    // Driver code
    public static void Main(String []args)
    {
        int []a = { 1, 7, 8, 3 };
        int []b = { 6, 5, 10, 2 };

        int size = a.Length;

        thirdArray(a, b, size);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// javascript implementation to find distinct
// array such that the elements of the
// array is sum of two
// elements of other two arrays

// Function to find a distinct array
// such that elements of the third
// array is sum of two elements
// of other two arrays
function thirdArray(a, b, n)
{
    var c = new Array(n);
    a = a.sort(function(a, b) {
          return a - b;
    });
    b = b.sort(function(a, b) {
          return a - b;
    });

    var i,j;
    // Loop to find the array
    // such that each element is
    // sum of other two elements
    for (i = 0; i < n; i++) {
        c[i] = a[i] + b[i];
    }

    // Loop to print the array
    for (i = 0; i < n; i++)
        document.write(c[i] + " ");
}

// Driver code

    var a = [1, 7, 8, 3];
    var b = [6, 5, 10, 2];

    var size = a.length;
    thirdArray(a, b, size);

</script>
```

**Output:** 

```
3 8 13 18
```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，排序 N 大小的数组需要 O(N*logN)个时间，因此时间复杂度为 **O(N*logN)** 。
*   **空间复杂度:**和上面的方法一样，没有使用额外的空间，因此空间复杂度为 **O(1)** 。