# 求数组中零、正数、负数的比例

> 原文:[https://www . geeksforgeeks . org/find-数组中零-正数和负数的比率/](https://www.geeksforgeeks.org/find-ratio-of-zeroes-positive-numbers-and-negative-numbers-in-the-array/)

给定一个由大小为 **N** 的整数组成的数组 **a** ，任务是找出数组中的正数、负数和零的比例，最多到小数点后四位。

**示例:**

> **输入:** a[] = {2，-1，5，6，0，-3}
> **输出:** 0.5000 0.3333 0.1667
> 有 3 个正，2 个负，1 个零。它们的比率将是正的:3/6 = 0.5000，负的:2/6 = 0.3333，零的:1/6 = 0.1667。
> 
> **输入:** a[] = {4，0，-2，-9，-7，1}
> 输出: 0.3333 0.5000 0.1667
> 有 2 正，3 负，1 零。它们的比率将是正的:2/6 = 0.3333，负的:3/6 = 0.5000，零的:1/6 = 0.1667。

**进场:**

1.  计算数组中正元素的总数。
2.  计算数组中负元素的总数。
3.  计算数组中零元素的总数。
4.  将正元素、负元素和零元素的总数除以数组的大小，得到比值。
5.  打印数组中的正、负、零元素的比率，最多四位小数。

下面是上述方法的实现。

## C++

```
// C++ program to find the ratio of positive,
// negative, and zero elements in the array.
#include<bits/stdc++.h>
using namespace std;

// Function to find the ratio of
// positive, negative, and zero elements
void positiveNegativeZero(int arr[], int len)
{
    // Initialize the postiveCount, negativeCount, and
    // zeroCountby 0 which will count the total number
    // of positive, negative and zero elements
    float positiveCount = 0;
    float negativeCount = 0;
    float zeroCount = 0;

    // Traverse the array and count the total number of
    // positive, negative, and zero elements.
    for (int i = 0; i < len; i++) {
        if (arr[i] > 0) {
            positiveCount++;
        }
        else if (arr[i] < 0) {
            negativeCount++;
        }
        else if (arr[i] == 0) {
            zeroCount++;
        }
    }

    // Print the ratio of positive,
    // negative, and zero elements
    // in the array up to four decimal places.
    cout << fixed << setprecision(4) << (positiveCount / len)<<" ";
    cout << fixed << setprecision(4) << (negativeCount / len)<<" ";
    cout << fixed << setprecision(4) << (zeroCount / len);
    cout << endl;
}

// Driver Code.
int main()
{
    // Test Case 1:
    int a1[] = { 2, -1, 5, 6, 0, -3 };
    int len=sizeof(a1)/sizeof(a1[0]);
    positiveNegativeZero(a1,len);

    // Test Case 2:
    int a2[] = { 4, 0, -2, -9, -7, 1 };
    len=sizeof(a2)/sizeof(a2[0]);
    positiveNegativeZero(a2,len);
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the ratio of positive,
// negative, and zero elements in the array.

class GFG {

    // Function to find the ratio of
    // positive, negative, and zero elements
    static void positiveNegativeZero(int[] arr)
    {

        // Store the array length into the variable len.
        int len = arr.length;

        // Initialize the postiveCount, negativeCount, and
        // zeroCountby 0 which will count the total number
        // of positive, negative and zero elements
        float positiveCount = 0;
        float negativeCount = 0;
        float zeroCount = 0;

        // Traverse the array and count the total number of
        // positive, negative, and zero elements.
        for (int i = 0; i < len; i++) {
            if (arr[i] > 0) {
                positiveCount++;
            }
            else if (arr[i] < 0) {
                negativeCount++;
            }
            else if (arr[i] == 0) {
                zeroCount++;
            }
        }

        // Print the ratio of positive,
        // negative, and zero elements
        // in the array up to four decimal places.
        System.out.printf("%1.4f ", positiveCount / len);
        System.out.printf("%1.4f ", negativeCount / len);
        System.out.printf("%1.4f ", zeroCount / len);
        System.out.println();
    }

    // Driver Code.
    public static void main(String args[])
    {

        // Test Case 1:
        int[] a1 = { 2, -1, 5, 6, 0, -3 };
        positiveNegativeZero(a1);

        // Test Case 2:
        int[] a2 = { 4, 0, -2, -9, -7, 1 };
        positiveNegativeZero(a2);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the ratio of positive,
# negative, and zero elements in the array.

# Function to find the ratio of
# positive, negative, and zero elements
def positiveNegativeZero(arr):

    # Store the array length into the variable len.
    length = len(arr);

    # Initialize the postiveCount, negativeCount, and
    # zeroCountby 0 which will count the total number
    # of positive, negative and zero elements
    positiveCount = 0;
    negativeCount = 0;
    zeroCount = 0;

    # Traverse the array and count the total number of
    # positive, negative, and zero elements.
    for i in range(length):
        if (arr[i] > 0):
            positiveCount += 1;
        elif(arr[i] < 0):
            negativeCount += 1;
        elif(arr[i] == 0):
            zeroCount += 1;

    # Print the ratio of positive,
    # negative, and zero elements
    # in the array up to four decimal places.
    print("{0:.4f}".format((positiveCount / length)), end=" ");
    print("%1.4f "%(negativeCount / length), end=" ");
    print("%1.4f "%(zeroCount / length), end=" ");
    print();

# Driver Code.
if __name__ == '__main__':

    # Test Case 1:
    a1 = [ 2, -1, 5, 6, 0, -3 ];
    positiveNegativeZero(a1);

    # Test Case 2:
    a2 = [ 4, 0, -2, -9, -7, 1 ];
    positiveNegativeZero(a2);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program to find the ratio of positive,
// negative, and zero elements in the array.
using System;

class GFG {

    // Function to find the ratio of
    // positive, negative, and zero elements
    static void positiveNegativeZero(int[] arr)
    {

        // Store the array length into the variable len.
        int len = arr.Length;

        // Initialize the postiveCount, negativeCount, and
        // zeroCountby 0 which will count the total number
        // of positive, negative and zero elements
        float positiveCount = 0;
        float negativeCount = 0;
        float zeroCount = 0;

        // Traverse the array and count the total number of
        // positive, negative, and zero elements.
        for (int i = 0; i < len; i++) {
            if (arr[i] > 0) {
                positiveCount++;
            }
            else if (arr[i] < 0) {
                negativeCount++;
            }
            else if (arr[i] == 0) {
                zeroCount++;
            }
        }

        // Print the ratio of positive,
        // negative, and zero elements
        // in the array up to four decimal places.
        Console.Write("{0:F4} ", positiveCount / len);
        Console.Write("{0:F4} ", negativeCount / len);
        Console.Write("{0:F4} ", zeroCount / len);
        Console.WriteLine();
    }

    // Driver Code.
    public static void Main(String []args)
    {

        // Test Case 1:
        int[] a1 = { 2, -1, 5, 6, 0, -3 };
        positiveNegativeZero(a1);

        // Test Case 2:
        int[] a2 = { 4, 0, -2, -9, -7, 1 };
        positiveNegativeZero(a2);
    }
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the
// ratio of positive, negative, and
// zero elements in the array.

// Function to find the ratio of
// positive, negative, and zero elements
function positiveNegativeZero(arr)
{

    // Store the array length into
    // the variable len.
    let len = arr.length;

    // Initialize the postiveCount,
    // negativeCount, and zeroCountby
    // 0 which will count the total number
    // of positive, negative and zero elements
    let positiveCount = 0;
    let negativeCount = 0;
    let zeroCount = 0;

    // Traverse the array and count the
    // total number of positive, negative,
    // and zero elements.
    for(let i = 0; i < len; i++)
    {
        if (arr[i] > 0)
        {
            positiveCount++;
        }
        else if (arr[i] < 0)
        {
            negativeCount++;
        }
        else if (arr[i] == 0)
        {
            zeroCount++;
        }
    }

    // Print the ratio of positive,
    // negative, and zero elements
    // in the array up to four decimal places.
    document.write((positiveCount / len).toFixed(4) + " ");
    document.write((negativeCount / len).toFixed(4) + " ");
    document.write((zeroCount / len).toFixed(4));
    document.write("<br>");
}

// Driver Code.

// Test Case 1:
let a1 = [ 2, -1, 5, 6, 0, -3 ];
positiveNegativeZero(a1);

// Test Case 2:
let a2 = [ 4, 0, -2, -9, -7, 1 ];
positiveNegativeZero(a2);

// This code is contributed by sravan kumar G

</script>
```

**Output:** 

```
0.5000 0.3333 0.1667 
0.3333 0.5000 0.1667
```

***时间复杂度:** O(len)*

***辅助空间:** O(1)*