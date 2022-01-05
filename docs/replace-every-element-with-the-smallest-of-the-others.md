# 用其他元素中最小的元素替换每个元素

> 原文:[https://www . geesforgeks . org/用最小的元素替换每个元素/](https://www.geeksforgeeks.org/replace-every-element-with-the-smallest-of-the-others/)

给定一个由 **N** 个不同整数组成的数组 **arr[]** ，任务是用数组中所有其他剩余元素中的最小值替换每个元素。
**例:**

> **输入:** arr[] = { 4，2，1，3 }
> **输出:** arr[]= { 1，1，2，1 }
> **解释:**
> 对于 arr[0]，剩余元素中最小的是 1。所以 arr[0]被 1 代替。
> 对于 arr[1]，剩余元素中最小的是 1。所以 arr[1]被 1 代替。
> 对于 arr[2]，剩余元素中最小的是 2。所以 arr[2]被 2 代替。
> 对于 arr[3]，剩余元素中最小的是 1。所以 arr[3]被 1 代替。
> **输入:** arr[] = { 1，5，2，4 }
> **输出:** arr[] = { 2，1，1，1 }

**天真方法:**
运行一个嵌套循环，为每个元素找到所有其他元素中最小的一个并存储它们。
***时间复杂度:** O(N <sup>2</sup> )*
**高效途径:**

1.  遍历数组，找到数组中最小的两个元素。
2.  再次遍历数组，现在用第二小元素替换最小元素，用最小元素替换数组中的所有其他元素。
3.  打印修改后的数组。

以下是上述方法的实现:

## C++

```
// C# implementation to find the
// maximum array sum by concatenating
// corresponding elements of given two arrays
using System;
class GFG{

// Function to join the two numbers
static int joinNumbers(int numA, int numB)
{
    int revB = 0;

    // Loop to reverse the digits
    // of the one number
    while (numB > 0)
    {
        revB = revB * 10 + (numB % 10);
        numB = numB / 10;
    }

    // Loop to join two numbers
    while (revB > 0)
    {
        numA = numA * 10 + (revB % 10);
        revB = revB / 10;
    }

    return numA;
}

// Function to find the maximum array sum
static int findMaxSum(int []A, int []B, int n)
{
    int []maxArr = new int[n];

    // Loop to iterate over the two
    // elements of the array
    for(int i = 0; i < n; ++i)
    {
        int X = joinNumbers(A[i], B[i]);
        int Y = joinNumbers(B[i], A[i]);
        int mx = Math.Max(X, Y);

        maxArr[i] = mx;
    }

    // Find the array sum
    int maxAns = 0;
    for(int i = 0; i < n; i++)
    {
        maxAns += maxArr[i];
    }

    // Return the array sum
    return maxAns;
}

// Driver Code
public static void Main(String []args)
{
    int N = 5;
    int []A = { 11, 23, 38, 43, 59 };
    int []B = { 36, 24, 17, 40, 56 };

    Console.WriteLine(findMaxSum(A, B, N));
}
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach.
import java.util.*;

class GFG {

    static void ReplaceElements(
        int[] arr, int n)
    {

        // There should be atleast
        // two elements
        if (n < 2) {

            System.out.println(
                "Invalid Input");

            return;
        }

        int firstSmallest
            = Integer.MAX_VALUE;
        int secondSmallest
            = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++) {

            // If current element is smaller
            // than firstSmallest then update
            // both firstSmallest
            // and secondSmallest
            if (arr[i] < firstSmallest) {

                secondSmallest = firstSmallest;
                firstSmallest = arr[i];
            }

            // If arr[i] is in between
            // firstSmallest and secondSmallest
            // then update secondSmallest
            else if (arr[i] < secondSmallest
                     && arr[i] != firstSmallest)
                secondSmallest = arr[i];
        }

        // Replace every element by
        // smallest of all other elements
        for (int i = 0; i < n; i++) {

            if (arr[i] != firstSmallest)
                arr[i] = firstSmallest;

            else
                arr[i] = secondSmallest;
        }

        // Print the modified array.
        for (int i = 0; i < n; ++i) {
            System.out.print(arr[i]
                             + ", ");
        }
    }

    // Driver code
    public static void main(
        String[] args)
    {
        int arr[] = { 4, 2, 1, 3 };
        int n = arr.length;

        ReplaceElements(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 code for the above approach.
def ReplaceElements(arr, n):

    # There should be atleast
    # two elements
    if (n < 2):
        print("Invalid Input")
        return

    firstSmallest = 10 ** 18
    secondSmallest = 10 ** 18

    for i in range(n):

        # If current element is smaller
        # than firstSmallest then update
        # both firstSmallest
        # and secondSmallest
        if (arr[i] < firstSmallest):
            secondSmallest = firstSmallest
            firstSmallest = arr[i]

        # If arr[i] is in between
        # firstSmallest and secondSmallest
        # then update secondSmallest
        elif (arr[i] < secondSmallest and
              arr[i] != firstSmallest):
            secondSmallest = arr[i]

    # Replace every element by
    # smallest of all other elements
    for i in range(n):

        if (arr[i] != firstSmallest):
            arr[i] = firstSmallest

        else:
            arr[i] = secondSmallest

    # Print the modified array.
    for i in arr:
        print(i, end = ", ")

# Driver code
if __name__ == '__main__':

    arr= [ 4, 2, 1, 3 ]
    n = len(arr)

    ReplaceElements(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# code for the above approach.
using System;

class GFG{

static void ReplaceElements(int[] arr, int n)
{

    // There should be atleast
    // two elements
    if (n < 2)
    {
        Console.Write("Invalid Input");

        return;
    }

    int firstSmallest = Int32.MaxValue;
    int secondSmallest = Int32.MaxValue;

    for(int i = 0; i < n; i++)
    {

       // If current element is smaller
       // than firstSmallest then update
       // both firstSmallest
       // and secondSmallest
       if (arr[i] < firstSmallest)
       {
           secondSmallest = firstSmallest;
           firstSmallest = arr[i];
       }

       // If arr[i] is in between
       // firstSmallest and secondSmallest
       // then update secondSmallest
       else if (arr[i] < secondSmallest &&
                arr[i] != firstSmallest)
           secondSmallest = arr[i];
    }

    // Replace every element by
    // smallest of all other elements
    for(int i = 0; i < n; i++)
    {
       if (arr[i] != firstSmallest)
           arr[i] = firstSmallest;
       else
           arr[i] = secondSmallest;
    }

    // Print the modified array.
    for(int i = 0; i < n; ++i)
    {
       Console.Write(arr[i] + ", ");
    }
}

// Driver code
public static void Main()
{
    int []arr = { 4, 2, 1, 3 };
    int n = arr.Length;

    ReplaceElements(arr, n);
}
}

// This code is contributed by Nidhi_Biet
```

## java 描述语言

```
<script>
// Javascript code for the above approach.
function ReplaceElements(arr, n)
{

    // There should be atleast
        // two elements
        if (n < 2)
        {

            document.write(
                "Invalid Input<br>");

            return;
        }

        let firstSmallest
            = Number.MAX_VALUE;
        let secondSmallest
            = Number.MAX_VALUE;

        for (let i = 0; i < n; i++)
        {

            // If current element is smaller
            // than firstSmallest then update
            // both firstSmallest
            // and secondSmallest
            if (arr[i] < firstSmallest)
            {

                secondSmallest = firstSmallest;
                firstSmallest = arr[i];
            }

            // If arr[i] is in between
            // firstSmallest and secondSmallest
            // then update secondSmallest
            else if (arr[i] < secondSmallest
                     && arr[i] != firstSmallest)
                secondSmallest = arr[i];
        }

        // Replace every element by
        // smallest of all other elements
        for (let i = 0; i < n; i++) {

            if (arr[i] != firstSmallest)
                arr[i] = firstSmallest;

            else
                arr[i] = secondSmallest;
        }

        // Print the modified array.
        for (let i = 0; i < n; ++i) {
            document.write(arr[i]
                             + ", ");
        }
}

 // Driver code
let arr=[ 4, 2, 1, 3 ];
let n = arr.length;
ReplaceElements(arr, n);

// This code is contributed by unknown2108.
</script>
```

**Output:** 

```
1, 1, 2, 1,
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*