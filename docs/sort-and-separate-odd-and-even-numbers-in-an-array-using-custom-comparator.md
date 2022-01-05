# 使用自定义比较器对数组中的奇数和偶数进行排序和分离

> 原文:[https://www . geeksforgeeks . org/使用自定义比较器对数组中的奇数和偶数进行排序和分离/](https://www.geeksforgeeks.org/sort-and-separate-odd-and-even-numbers-in-an-array-using-custom-comparator/)

给定一个包含 **N** 元素的数组 **arr[]** ，任务是使用自定义比较器对数组中的奇数和偶数进行排序和分离。

**示例:**

> **输入:** arr[] = { 5，3，2，8，7，4，6，9，1 }
> **输出:** 2 4 6 8 1 3 5 7 9
> 
> **输入:** arr[] = { 12，15，6，2，7，13，9，4 }
> **输出:** 2 4 6 12 7 9 13 15

**方法:**正如我们所知 [std::sort()](https://www.geeksforgeeks.org/sort-c-stl/) 用于按升序排序，但是我们可以使用[自定义比较器](https://www.geeksforgeeks.org/comparator-class-in-c-with-examples/)来操纵 sort()。
现在，为了将它们分开，可以使用的属性是偶数的最后一位是 0，奇数的最后一位是 1。因此，让自定义比较器根据该数字的最后一位对元素进行排序。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Creating custom comparator
bool compare(int a, int b)
{

    // If both are odd or even
    // then sorting in increasing order
    if ((a & 1) == (b & 1)) {
        return a < b;
    }

    // Sorting on the basis of last bit if
    // if one is odd and the other one is even
    return (a & 1) < (b & 1);
}

// Function to
void seperateOddEven(int* arr, int N)
{
    // Seperating them using sort comparator
    sort(arr, arr + N, compare);

    for (int i = 0; i < N; ++i) {
        cout << arr[i] << ' ';
    }
}

// Driver Code
int main()
{
    int arr[] = { 12, 15, 6, 2, 7, 13, 9, 4 };
    int N = sizeof(arr) / sizeof(int);
    seperateOddEven(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Creating custom comparator
static boolean comparecust(Integer a, Integer b)
{

    // If both are odd or even
    // then sorting in increasing order
    if ((a & 1) == (b & 1)) {
        return a < b;
    }

    // Sorting on the basis of last bit if
    // if one is odd and the other one is even
    return (a & 1) < (b & 1);
}

// Function to
static void seperateOddEven(Integer []arr, int N)
{
    // Seperating them using sort comparator
    Arrays.sort(arr, new Comparator<Integer>() {

        @Override
        public int compare(Integer a, Integer b) {
            // If both are odd or even
            // then sorting in increasing order
            if ((a & 1) == (b & 1)) {
                return a < b?-1:1;
            }

            // Sorting on the basis of last bit if
            // if one is odd and the other one is even
            return ((a & 1) < (b & 1))?-1:1;
        }

    });

    for (int i = 0; i < N; ++i) {
        System.out.print(arr[i] +" ");
    }
}

// Driver Code
public static void main(String[] args)
{
    Integer arr[] = { 12, 15, 6, 2, 7, 13, 9, 4 };
    int N = arr.length;
    seperateOddEven(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class compare : IComparer
{

    // Call CaseInsensitiveComparer.Compare
    public int Compare(Object x, Object y)
    {
        int a = (int)x;
        int b = (int)y;

        // If both are odd or even
        // then sorting in increasing order
        if ((a & 1) == (b & 1))
        {
            return a < b ? -1 : 1;
        }

        // Sorting on the basis of last bit if
        // if one is odd and the other one is even
        return ((a & 1) < (b & 1)) ? -1 : 1;
    }
}

class GFG{

// Function to
static void seperateOddEven(int []arr, int N)
{

    // Seperating them using sort comparator
    // Instantiate the IComparer object
    IComparer cmp = new compare();
    Array.Sort(arr, cmp);

    for(int i = 0; i < N; ++i)
    {
        Console.Write(arr[i] + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 12, 15, 6, 2, 7, 13, 9, 4 };
    int N = arr.Length;

    seperateOddEven(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Creating custom comparator
function compare(a, b)
{

    // If both are odd or even
    // then sorting in increasing order
    if ((a & 1) == (b & 1)) {
        return a > b;
    }

    // Sorting on the basis of last bit if
    // if one is odd and the other one is even
    return (a & 1) > (b & 1);
}

// Function to
function seperateOddEven(arr, N)
{
    // Seperating them using sort comparator
    arr.sort(compare);

    for (let i = 0; i < N; ++i) {
        document.write(arr[i] + " ");
    }
}

// Driver Code
let arr = [ 12, 15, 6, 2, 7, 13, 9, 4 ];
let N = arr.length;
seperateOddEven(arr, N);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
2 4 6 12 7 9 13 15 
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(1)