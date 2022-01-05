# 改变给定数组中的一个元素，使其成为算术级数

> 原文:[https://www . geesforgeks . org/change-给定数组中的一个元素使其成为算术级数/](https://www.geeksforgeeks.org/change-one-element-in-the-given-array-to-make-it-an-arithmetic-progression/)

给定一个数组，它是一个改变了一个元素的原始算术级数。任务是让它再次成为算术级数。如果有许多这样的可能序列，返回其中任何一个。数组的长度总是大于 2。
**例:**

> **输入:** arr = [1，3，4，7]
> **输出:** arr = [1，3，5，7]
> 等差数列的公差是 2，因此得到的
> 等差数列是[1，3，5，7]。
> 
> **输入:** arr = [1，3，7]
> **输出:** arr = [-1，3，7]
> 共同的区别可以是 2 或 3 或 4。
> 因此得到的数组可以是[1，3，5]，[-1，3，7]或[1，4，7]。
> 由于可以选择任意一个，[-1，3，7]作为输出返回。

**进场:**

算术级数的关键组成部分是初始项和公共差。所以我们的任务是找到这两个值来知道实际的算术级数。

*   如果数组的长度为 3，则取公差作为任意两个元素的差。
*   否则，尝试使用前四个元素来找到共同的区别。
    *   使用公式 a[1]–a[0]= a[2]–a[1]检查前三个元素是否是算术级数。如果它们是等差数列，则公共差 d = a[1]–a[0]和初始项将是 a[0]
    *   使用公式 a[2]–a[1]= a[3]–a[2]检查第二、第三和第四个元素是否在算术级数中。如果它们是等差数列，则公共差 d = a[2]–a[1]，这意味着第一个元素已被更改，因此初始项是 a[0]= a[1]–d
    *   在上述两种情况下，我们已经检查了第一个元素或第四个元素是否已被更改。如果这两种情况都为假，则意味着第一个或第四个元素没有改变。所以公差带可以取为 d =(a[3]–a[0])/3，初始项= a[0]
*   使用初始术语和常见差异打印所有元素。

以下是上述方法的实现:

## C/C++

```
// C++ program to change one element of an array such
// that the resulting array is in arithmetic progression.
#include <bits/stdc++.h>
using namespace std;

// Finds the initial term and common difference and
// prints the resulting sequence.
void makeAP(int arr[], int n)
{
    int initial_term, common_difference;

    if (n == 3) {
        common_difference = arr[2] - arr[1];
        initial_term = arr[1] - common_difference;
    }

    else if ((arr[1] - arr[0]) == arr[2] - arr[1]) {

        // Check if the first three elements are in
        // arithmetic progression
        initial_term = arr[0];
        common_difference = arr[1] - arr[0];
    }
    else if ((arr[2] - arr[1]) == (arr[3] - arr[2])) {

        // Check if the first element is not
        // in arithmetic progression
        common_difference = arr[2] - arr[1];
        initial_term = arr[1] - common_difference;
    }
    else {

        // The first and fourth element are
        // in arithmetic progression
        common_difference = (arr[3] - arr[0]) / 3;
        initial_term = arr[0];
    }

    // Print the arithmetic progression
    for (int i = 0; i < n; i++)
        cout << initial_term + (i * common_difference) << " ";
    cout << endl;
}

// Driver Program
int main()
{
    int arr[] = { 1, 3, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    makeAP(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to change one element of an array such
// that the resulting array is in arithmetic progression.
import java.util.Arrays;

class AP {
    static void makeAP(int arr[], int n)
    {
        int initial_term, common_difference;

        // Finds the initial term and common difference and
        // prints the resulting array.
        if (n == 3) {
            common_difference = arr[2] - arr[1];
            initial_term = arr[1] - common_difference;
        }
        else if ((arr[1] - arr[0]) == arr[2] - arr[1]) {

            // Check if the first three elements are in
            // arithmetic progression
            initial_term = arr[0];
            common_difference = arr[1] - arr[0];
        }
        else if ((arr[2] - arr[1]) == (arr[3] - arr[2])) {
            // Check if the first element is not
            // in arithmetic progression
            common_difference = arr[2] - arr[1];
            initial_term = arr[1] - common_difference;
        }
        else {
            // The first and fourth element are
            // in arithmetic progression
            common_difference = (arr[3] - arr[0]) / 3;
            initial_term = arr[0];
        }

        // Print the arithmetic progression
        for (int i = 0; i < n; i++)
            System.out.print(initial_term +
                            (i * common_difference) + " ");
        System.out.println();
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 3, 7 };
        int n = arr.length;
        makeAP(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python program to change one element of an array such
# that the resulting array is in arithmetic progression.
def makeAP(arr, n): 
    initial_term, common_difference = 0, 0
    if (n == 3):
        common_difference = arr[2] - arr[1]
        initial_term = arr[1] - common_difference
    elif((arr[1] - arr[0]) == arr[2] - arr[1]):

        # Check if the first three elements are in 
        # arithmetic progression
        initial_term = arr[0]
        common_difference = arr[1] - arr[0]

    elif((arr[2] - arr[1]) == (arr[3] - arr[2])):

        # Check if the first element is not 
        # in arithmetic progression
        common_difference = arr[2] - arr[1]
        initial_term = arr[1] - common_difference

    else:
        # The first and fourth element are 
        # in arithmetic progression
        common_difference = (arr[3] - arr[0]) / 3
        initial_term = arr[0]

    # Print the arithmetic progression
    for i in range(n):
        print(int(initial_term+
                 (i * common_difference)), end = " ")
    print()

# Driver code 
arr = [1, 3, 7] 
n = len(arr) 
makeAP(arr, n)
```

## C#

```
// C# program to change one element of an array such
// that the resulting array is in arithmetic progression.
using System;

public class AP 
{
    static void makeAP(int []arr, int n)
    {
        int initial_term, common_difference;

        // Finds the initial term and common difference and
        // prints the resulting array.
        if (n == 3) 
        {
            common_difference = arr[2] - arr[1];
            initial_term = arr[1] - common_difference;
        }
        else if ((arr[1] - arr[0]) == arr[2] - arr[1]) 
        {

            // Check if the first three elements are in
            // arithmetic progression
            initial_term = arr[0];
            common_difference = arr[1] - arr[0];
        }
        else if ((arr[2] - arr[1]) == (arr[3] - arr[2]))
        {
            // Check if the first element is not
            // in arithmetic progression
            common_difference = arr[2] - arr[1];
            initial_term = arr[1] - common_difference;
        }
        else
        {
            // The first and fourth element are
            // in arithmetic progression
            common_difference = (arr[3] - arr[0]) / 3;
            initial_term = arr[0];
        }

        // Print the arithmetic progression
        for (int i = 0; i < n; i++)
            Console.Write(initial_term +
                            (i * common_difference) + " ");
        Console.WriteLine();
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 1, 3, 7 };
        int n = arr.Length;
        makeAP(arr, n);
    }
}

// This code contributed by Rajput-Ji
```

**Output:**

```
-1 3 7

```

**时间复杂度** : O(N)，其中 N 为数组中的元素个数。