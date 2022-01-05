# 将数组压缩到范围内

> 原文:[https://www . geeksforgeeks . org/将数组压缩为范围/](https://www.geeksforgeeks.org/compress-the-array-into-ranges/)

给定一个大小为 N 的整数数组，任务是将连续的整数打印为一个范围。
**例:**

> **输入:** N = 7，arr=[7，8，9，15，16，20，25]
> **输出:** 7-9 15-16 20 25
> 出现的连续元素为[ {7，8，9}，{15，16}，{20}，{25} ]
> 因此输出结果为 7-9 15-16 20 25
> **输入:** N = 6，arr

**方法:**
这个问题可以很容易地想象成[游程编码问题](https://www.geeksforgeeks.org/run-length-encoding/)的变体。

*   首先对数组进行排序。
*   然后，开始 while 循环遍历数组以检查连续的元素。在任何特定情况下，连续数字的结束将由 ***j-1*** 表示，开始由 ***i*** 表示。
*   如果 I 不在 while 循环中，则增加 1，否则增加***【j+1】***，以便它跳到当前范围之外的下一个 ith 元素。

以下是上述方法的实现:

## C++

```
// C++ program to compress the array ranges
#include <bits/stdc++.h>
using namespace std;

// Function to compress the array ranges
void compressArr(int arr[], int n)
{
    int i = 0, j = 0;
    sort(arr, arr + n);
    while (i < n) {

        // start iteration from the
        // ith array element
        j = i;

        // loop until arr[i+1] == arr[i]
        // and increment j
        while ((j + 1 < n) &&
                 (arr[j + 1] == arr[j] + 1)) {
            j++;
        }

        // if the program do not enter into
        // the above while loop this means that
        // (i+1)th element is not consecutive
        // to i th element
        if (i == j) {
            cout << arr[i] << " ";

            // increment i for next iteration
            i++;
        }
        else {
            // print the consecutive range found
            cout << arr[i] << "-" << arr[j] << " ";

            // move i jump directly to j+1
            i = j + 1;
        }
    }
}

// Driver code
int main()
{

    int n = 7;
    int arr[n] = { 1, 3, 4, 5, 6, 9, 10 };

    compressArr(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to compress the array ranges
import java.util.Arrays;

class GFG
{

// Function to compress the array ranges
static void compressArr(int arr[], int n)
{
    int i = 0, j = 0;
    Arrays.sort(arr);
    while (i < n)
    {

        // start iteration from the
        // ith array element
        j = i;

        // loop until arr[i+1] == arr[i]
        // and increment j
        while ((j + 1 < n) &&
                (arr[j + 1] == arr[j] + 1))
        {
            j++;
        }

        // if the program do not enter into
        // the above while loop this means that
        // (i+1)th element is not consecutive
        // to i th element
        if (i == j)
        {
            System.out.print( arr[i] + " ");

            // increment i for next iteration
            i++;
        }
        else
        {
            // print the consecutive range found
            System.out.print( arr[i] + "-" + arr[j] + " ");

            // move i jump directly to j+1
            i = j + 1;
        }
    }
}

    // Driver code
    public static void main (String[] args)
    {
        int n = 7;
        int arr[] = { 1, 3, 4, 5, 6, 9, 10 };

        compressArr(arr, n);
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python program to compress the array ranges

# Function to compress the array ranges
def compressArr(arr, n):
    i = 0;
    j = 0;
    arr.sort();
    while (i < n):

        # start iteration from the
        # ith array element
        j = i;

        # loop until arr[i+1] == arr[i]
        # and increment j
        while ((j + 1 < n) and
                (arr[j + 1] == arr[j] + 1)):
            j += 1;

        # if the program do not enter into
        # the above while loop this means that
        # (i+1)th element is not consecutive
        # to i th element
        if (i == j):
            print(arr[i], end=" ");

            # increment i for next iteration
            i+=1;
        else:
            # print the consecutive range found
            print(arr[i], "-", arr[j], end=" ");

            # move i jump directly to j+1
            i = j + 1;

# Driver code
n = 7;
arr = [ 1, 3, 4, 5, 6, 9, 10 ];
compressArr(arr, n);

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to compress the array ranges
using System;

class GFG
{

// Function to compress the array ranges
static void compressArr(int []arr, int n)
{
    int i = 0, j = 0;
    Array.Sort(arr);
    while (i < n)
    {

        // start iteration from the
        // ith array element
        j = i;

        // loop until arr[i+1] == arr[i]
        // and increment j
        while ((j + 1 < n) &&
                (arr[j + 1] == arr[j] + 1))
        {
            j++;
        }

        // if the program do not enter into
        // the above while loop this means that
        // (i+1)th element is not consecutive
        // to i th element
        if (i == j)
        {
            Console.Write( arr[i] + " ");

            // increment i for next iteration
            i++;
        }
        else
        {
            // print the consecutive range found
            Console.Write( arr[i] + "-" + arr[j] + " ");

            // move i jump directly to j+1
            i = j + 1;
        }
    }
}

// Driver code
public static void Main ()
{
    int n = 7;
    int []arr = { 1, 3, 4, 5, 6, 9, 10 };

    compressArr(arr, n);
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript program to compress the array ranges

    // Function to compress the array ranges
    function compressArr(arr, n)
    {
        let i = 0, j = 0;
        arr.sort(function(a, b){return a - b});
        while (i < n)
        {

            // start iteration from the
            // ith array element
            j = i;

            // loop until arr[i+1] == arr[i]
            // and increment j
            while ((j + 1 < n) && (arr[j + 1] == arr[j] + 1))
            {
                j++;
            }

            // if the program do not enter into
            // the above while loop this means that
            // (i+1)th element is not consecutive
            // to i th element
            if (i == j)
            {
                document.write( arr[i] + " ");

                // increment i for next iteration
                i++;
            }
            else
            {
                // print the consecutive range found
                document.write( arr[i] + "-" + arr[j] + " ");

                // move i jump directly to j+1
                i = j + 1;
            }
        }
    }

    let n = 7;
    let arr = [ 1, 3, 4, 5, 6, 9, 10 ];

    compressArr(arr, n);

</script>
```

**Output:** 

```
1 3-6 9-10
```

**时间复杂度:** O(nlogn)