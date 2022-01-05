# 找到占据给定球的盒子的位置

> 原文:[https://www . geeksforgeeks . org/find-占据指定球的盒子位置/](https://www.geeksforgeeks.org/find-the-position-of-box-which-occupies-the-given-ball/)

给定两个阵 **A[]** 和 **B[]** 。其中 **A[]** 的大小代表行数， **A[i]** 代表第**I**行中的箱数。数组 **B[]** 代表球的数组，其中 **B[i]** 代表球上的一个数字。假设球 **i** (具有值 B[i])将被放置在一个盒子中，该盒子从开始的位置是 B[i](行-主)。任务是找到每个 **B[i]** 对应的框的行列。
**例:**

> **输入:** A[] = {2，3，4，5}，B[] = {1，4，6，3}
> **输出:**
> 1，1
> 2，2
> 3，1
> 2，1
> B[0] = 1，因此箱位置为第 1 行，第 1 列
> B[1] = 4，因此箱位置为第 2 行，第 2 列
> B[2] = 6，因此箱位置为第 3 行 第一列
> **输入:** A[] = {2，2，2，2}，B[] = {1，2，3，4}
> **输出:**
> 1，1
> 1，2
> 2，1
> 2，2

**进场:**根据问题陈述，第一排**A【0】**号箱同样放置在第二排**A【1】**号箱。所以，如果一个球要放在第二排的任何一个盒子里，它的值必须大于**A【0】**。所以，要找到一个球 **B[i]** 将要放置的盒子的实际位置，首先要找到数组 **A[]** 的累积和，然后找到累积和数组中刚好大于 **B[i]** 的元素的位置，这将是行号，要找到特定行中的盒子号，要找到累积数组中刚好小于 **B[i]的值**B[I]–值**
以下是上述方法的实施:** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the position of each boxes
// where a ball has to be placed
void printPosition(int A[], int B[], int sizeOfA, int sizeOfB)
{

    // Find the cumulative sum of array A[]
    for (int i = 1; i < sizeOfA; i++)
        A[i] += A[i - 1];

    // Find the position of box for each ball
    for (int i = 0; i < sizeOfB; i++) {

        // Row number
        int row = lower_bound(A, A + sizeOfA, B[i]) - A;

        // Column (position of box in particular row)
        int boxNumber = (row >= 1) ? B[i] - A[row - 1] : B[i];

        // Row + 1 denotes row if indexing of array start from 1
        cout << row + 1 << ", " << boxNumber << "\n";
    }
}

// Driver code
int main()
{

    int A[] = { 2, 2, 2, 2 };
    int B[] = { 1, 2, 3, 4 };
    int sizeOfA = sizeof(A) / sizeof(A[0]);
    int sizeOfB = sizeof(B) / sizeof(B[0]);
    printPosition(A, B, sizeOfA, sizeOfB);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{

    // Function to print the position of each boxes
    // where a ball has to be placed
    static void printPosition(int A[], int B[],
                        int sizeOfA, int sizeOfB)
    {

        // Find the cumulative sum of array A[]
        for (int i = 1; i < sizeOfA; i++)
        {
            A[i] += A[i - 1];
        }

        // Find the position of box for each ball
        for (int i = 0; i < sizeOfB; i++)
        {

            // Row number
            int row = lower_bound(A, 0, A.length, B[i]);

            // Column (position of box in particular row)
            int boxNumber = (row >= 1) ? B[i] - A[row - 1] : B[i];

            // Row + 1 denotes row if indexing of array start from 1
            System.out.print(row + 1 + ", " + boxNumber + "\n");
        }
    }

    private static int lower_bound(int[] a, int low, int high, int element)
    {
        while (low < high)
        {
            int middle = low + (high - low) / 2;
            if (element > a[middle])
            {
                low = middle + 1;
            }
            else
            {
                high = middle;
            }
        }
        return low;
    }
    // Driver code
    public static void main(String[] args)
    {
        int A[] = {2, 2, 2, 2};
        int B[] = {1, 2, 3, 4};
        int sizeOfA = A.length;
        int sizeOfB = B.length;
        printPosition(A, B, sizeOfA, sizeOfB);

    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import bisect

# Function to print the position of each boxes
# where a ball has to be placed
def printPosition(A, B, sizeOfA, sizeOfB):

    # Find the cumulative sum of array A[]
    for i in range(1, sizeOfA):
        A[i] += A[i - 1]

    # Find the position of box for each ball
    for i in range(sizeOfB):

        # Row number
        row = bisect.bisect_left(A, B[i])

        # Column (position of box in particular row)
        if row >= 1:
            boxNumber = B[i] - A[row - 1]
        else:
            boxNumber = B[i]

        # Row + 1 denotes row
        # if indexing of array start from 1
        print(row + 1, ",", boxNumber)

# Driver code
A = [2, 2, 2, 2]
B = [1, 2, 3, 4]
sizeOfA = len(A)
sizeOfB = len(B)
printPosition(A, B, sizeOfA, sizeOfB)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to print the position of each boxes
    // where a ball has to be placed
    static void printPosition(int []A, int []B,
                        int sizeOfA, int sizeOfB)
    {

        // Find the cumulative sum of array A[]
        for (int i = 1; i < sizeOfA; i++)
        {
            A[i] += A[i - 1];
        }

        // Find the position of box for each ball
        for (int i = 0; i < sizeOfB; i++)
        {

            // Row number
            int row = lower_bound(A, 0, A.Length, B[i]);

            // Column (position of box in particular row)
            int boxNumber = (row >= 1) ? B[i] - A[row - 1] : B[i];

            // Row + 1 denotes row if indexing of array start from 1
            Console.WriteLine(row + 1 + ", " + boxNumber + "\n");
        }
    }

    private static int lower_bound(int[] a, int low,
                                    int high, int element)
    {
        while (low < high)
        {
            int middle = low + (high - low) / 2;
            if (element > a[middle])
            {
                low = middle + 1;
            }
            else
            {
                high = middle;
            }
        }
        return low;
    }

    // Driver code
    static public void Main ()
    {
        int []A = {2, 2, 2, 2};
        int []B = {1, 2, 3, 4};
        int sizeOfA = A.Length;
        int sizeOfB = B.Length;
        printPosition(A, B, sizeOfA, sizeOfB);

    }
}

// This code has been contributed by Tushil.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// function to find the lower bound
function lower_bound($A, $valueTosearch)
{
    $row = 0;
    foreach ($A as $key=>$value)
    {
        if($valueTosearch <= $value)
            return $row;
        $row++;
    }
    return $row+1;
}

// Function to print the position of each boxes
// where a ball has to be placed
function printPosition($A, $B, $sizeOfA, $sizeOfB)
{

    // Find the cumulative sum of array A[]
    for ($i = 1; $i <$sizeOfA; $i++)
        $A[$i] += $A[$i - 1];

    // Find the position of box for each ball
    for ($i = 0; $i < $sizeOfB; $i++)
    {

        // Row number
        $row = lower_bound($A, $B[$i]) ;

        // Column (position of box in particular row)
        $boxNumber = ($row >= 1) ? $B[$i] - $A[$row - 1] : $B[$i];

        // Row + 1 denotes row if indexing of array start from 1
        print_r($row+1 .", ".$boxNumber);
        echo "\n";
    }
}

    // Driver code
    $A = array(2, 2, 2, 2 );
    $B = array( 1, 2, 3, 4 );
    $sizeOfA =count($A);
    $sizeOfB = count($B);
    printPosition($A, $B, $sizeOfA, $sizeOfB);

    // This code is contributed by Shivam.Pradhan
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach
    // Function to print the position of each boxes
    // where a ball has to be placed
    function printPosition(A , B , sizeOfA , sizeOfB) {

        // Find the cumulative sum of array A
        for (i = 1; i < sizeOfA; i++) {
            A[i] += A[i - 1];
        }

        // Find the position of box for each ball
        for (i = 0; i < sizeOfB; i++) {

            // Row number
            var row = lower_bound(A, 0, A.length, B[i]);

            // Column (position of box in particular row)
            var boxNumber = (row >= 1) ? B[i] - A[row - 1] : B[i];

            // Row + 1 denotes row if indexing of array start from 1
            document.write(row + 1 + ", " + boxNumber + "<br/>");
        }
    }

     function lower_bound(a , low , high , element) {
        while (low < high) {
            var middle = low + (high - low) / 2;
            if (element > a[middle]) {
                low = middle + 1;
            } else {
                high = middle;
            }
        }
        return low;
    }

    // Driver code

        var A = [ 2, 2, 2, 2 ];
        var B = [ 1, 2, 3, 4 ];
        var sizeOfA = A.length;
        var sizeOfB = B.length;
        printPosition(A, B, sizeOfA, sizeOfB);

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
1, 1
1, 2
2, 1
2, 2
```