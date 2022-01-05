# 将阵列分成三个等和子阵列

> 原文:[https://www . geesforgeks . org/split-array-三等和-subarray/](https://www.geeksforgeeks.org/split-array-three-equal-sum-subarrays/)

考虑一个由 n 个整数组成的数组 A。确定数组 A 是否可以分成三个连续的部分，使每个部分的总和相等。如果是，则打印任何索引对(I，j ),使得和(arr[0..i]) = sum(arr[i+1..j]) = sum(arr[j+1..n-1])，否则打印-1。
示例:

```
Input : arr[] = {1, 3, 4, 0, 4}
Output : (1, 2)
Sum of subarray arr[0..1] is equal to
sum of subarray arr[2..3] and also to
sum of subarray arr[4..4]. The sum is 4\. 

Input : arr[] = {2, 3, 4}
Output : -1
No three subarrays exist which have equal
sum.
```

一个**简单的**解法是先找到所有的子阵，将这些子阵的和与它们的起止点存储起来，然后找到三个和相等的不相交的连续子阵。这个解的时间复杂度将是二次的。
一个**高效的**解是先求所有数组元素的和 S。检查这个和是否能被 3 整除。这是因为如果和不能被整除，那么和就不能被分成三个相等的和集合。如果有三个和相等的邻接子阵，那么每个子阵的和就是 S/3。假设所需的索引对是(I，j ),使得和(arr[0..i]) = sum(arr[i+1..j]) = S/3。也求和(arr[0..i]) =假设[i]和总和(arr[i+1..j])= PleN[j]–PleN[I]。这给出了 PleN[I]= PleN[j]–PleN[I]= S/3。这给出了 PleN[j]= 2 * PleN[I]。因此，问题简化为找到两个指数 I 和 j，使得假定[i] = S/3 和假定[j] = 2*(S/3)。
要找到这两个索引，遍历数组，将当前元素的总和存储在变量“假定”中。检查假设是否等于 S/3 和 2*(S/3)。
**实施:**

## C++

```
// CPP program to determine if array arr[]
// can be split into three equal sum sets.
#include <iostream>
using namespace std;

// Function to determine if array arr[]
// can be split into three equal sum sets.
int findSplit(int arr[], int n)
{
    int i;

    // variable to store prefix sum
    int preSum = 0;

    // variables to store indices which
    // have prefix sum divisible by S/3.
    int ind1 = -1, ind2 = -1;

    // variable to store sum of
    // entire array.
    int S;

    // Find entire sum of the array.
    S = arr[0];
    for (i = 1; i < n; i++)
        S += arr[i];

    // Check if array can be split in
    // three equal sum sets or not.
    if(S % 3 != 0)
        return 0;

    // Variables to store sum S/3
    // and 2*(S/3).
    int S1 = S / 3;
    int S2 = 2 * S1;

      // Loop until second last index
    // as S2 should not be at the last
      for (i = 0; i < n-1; i++)
    {
        preSum += arr[i];

        // If prefix sum is equal to S/3
        // store current index.
        if (preSum == S1 && ind1 == -1)
            ind1 = i;

        // If prefix sum is equal to 2* (S/3)
        // store current index.
        else if(preSum  == S2 && ind1 != -1)
        {
            ind2 = i;

            // Come out of the loop as both the
            // required indices are found.
            break;
        }
    }

    // If both the indices are found
    // then print them.
    if (ind1 != -1 && ind2 != -1)
    {
        cout << "(" << ind1 << ", "
                                << ind2 << ")";
        return 1;
    }

    // If indices are not found return 0.
    return 0;
}

// Driver code
int main()
{
    int arr[] =  { 1, 3, 4, 0, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (findSplit(arr, n) == 0)
        cout << "-1";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to determine if array arr[]
// can be split into three equal sum sets.
import java.io.*;
import java.util.*;

public class GFG {

    // Function to determine if array arr[]
    // can be split into three equal sum sets.
    static int findSplit(int []arr, int n)
    {
        int i;

        // variable to store prefix sum
        int preSum = 0;

        // variables to store indices which
        // have prefix sum divisible by S/3.
        int ind1 = -1, ind2 = -1;

        // variable to store sum of
        // entire array.
        int S;

        // Find entire sum of the array.
        S = arr[0];
        for (i = 1; i < n; i++)
            S += arr[i];

        // Check if array can be split in
        // three equal sum sets or not.
        if(S % 3 != 0)
            return 0;

        // Variables to store sum S/3
        // and 2*(S/3).
        int S1 = S / 3;
        int S2 = 2 * S1;

        // Loop until second last index
        // as S2 should not be at the last
        for (i = 0; i < n-1; i++)
        {
            preSum += arr[i];

        // If prefix sum is equal to S/3
        // store current index.
            if (preSum == S1 && ind1 == -1)
                ind1 = i;

        // If prefix sum is equal to 2*(S/3)
        // store current index.
            else if(preSum == S2 && ind1 != -1)
            {
                ind2 = i;

                // Come out of the loop as both the
                // required indices are found.
                break;
            }
        }

        // If both the indices are found
        // then print them.
        if (ind1 != -1 && ind2 != -1)
        {
            System.out.print("(" + ind1 + ", "
                            + ind2 + ")");
            return 1;
        }

        // If indices are not found return 0.
        return 0;
    }

    // Driver code
    public static void main(String args[])
    {
        int []arr = { 1, 3, 4, 0, 4 };
        int n = arr.length;
        if (findSplit(arr, n) == 0)
            System.out.print("-1");
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to determine if array arr[]
# can be split into three equal sum sets.

# Function to determine if array arr[]
# can be split into three equal sum sets.
def findSplit(arr, n):
    # variable to store prefix sum
    preSum = 0

    # variables to store indices which
    # have prefix sum divisible by S/3.
    ind1 = -1
    ind2 = -1

    # variable to store sum of
    # entire array. S

    # Find entire sum of the array.
    S = arr[0]
    for i in range(1, n):
        S += arr[i]

    # Check if array can be split in
    # three equal sum sets or not.
    if(S % 3 != 0):
        return 0

    # Variables to store sum S/3
    # and 2*(S/3).
    S1 = S / 3
    S2 = 2 * S1

    # Loop until second last index
    # as S2 should not be at the last
    for i in range(0,n-1):
        preSum += arr[i]

        # If prefix sum is equal to S/3
        # store current index.
        if (preSum == S1 and ind1 == -1):
            ind1 = i
        # If prefix sum is equal to 2*(S/3)
        # store current index.       
        elif(preSum == S2 and ind1 != -1):
            ind2 = i

            # Come out of the loop as both the
            # required indices are found.
            break   

    # If both the indices are found
    # then print them.
    if (ind1 != -1 and ind2 != -1):
        print ("({}, {})".format(ind1,ind2))
        return 1

    # If indices are not found return 0.
    return 0

# Driver code
arr = [ 1, 3, 4, 0, 4 ]
n = len(arr)
if (findSplit(arr, n) == 0) :
    print ("-1")
# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to determine if array arr[]
// can be split into three equal sum sets.
using System;
using System.Collections.Generic;

class GFG {

    // Function to determine if array arr[]
    // can be split into three equal sum sets.
    static int findSplit(int []arr, int n)
    {
        int i;

        // variable to store prefix sum
        int preSum = 0;

        // variables to store indices which
        // have prefix sum divisible by S/3.
        int ind1 = -1, ind2 = -1;

        // variable to store sum of
        // entire array.
        int S;

        // Find entire sum of the array.
        S = arr[0];
        for (i = 1; i < n; i++)
            S += arr[i];

        // Check if array can be split in
        // three equal sum sets or not.
        if(S % 3 != 0)
            return 0;

        // Variables to store sum S/3
        // and 2*(S/3).
        int S1 = S / 3;
        int S2 = 2 * S1;

        // Loop until second last index
        // as S2 should not be at the last
        for (i = 0; i < n-1; i++)
        {
            preSum += arr[i];

        // If prefix sum is equal to S/3
        // store current index.
            if (preSum ==  S1 && ind1 == -1)
                ind1 = i;

        // If prefix sum is equal to S/3
        // store current index.
            else if(preSum == S2 && ind1 != -1)
            {
                ind2 = i;

                // Come out of the loop as both the
                // required indices are found.
                break;
            }
        }

        // If both the indices are found
        // then print them.
        if (ind1 != -1 && ind2 != -1)
        {
            Console.Write("(" + ind1 + ", "
                             + ind2 + ")");
            return 1;
        }

        // If indices are not found return 0.
        return 0;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 3, 4, 0, 4 };
        int n = arr.Length;
        if (findSplit(arr, n) == 0)
            Console.Write("-1");
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to determine if array arr[]
// can be split into three equal sum sets.

// Function to determine if array arr[]
// can be split into three equal sum sets.
function findSplit( $arr,  $n)
{
     $i;

    // variable to store prefix sum
     $preSum = 0;

    // variables to store indices which
    // have prefix sum divisible by S/3.
     $ind1 = -1; $ind2 = -1;

    // variable to store sum of
    // entire array.
     $S;

    // Find entire sum of the array.
    $S = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $S += $arr[$i];

    // Check if array can be split in
    // three equal sum sets or not.
    if($S % 3 != 0)
        return 0;

    // Variables to store sum S/3
    // and 2*(S/3).
     $S1 = $S / 3;
     $S2 = 2 * $S1;

    // Loop until second last index
    // as S2 should not be at the last
    for ($i = 0; $i < $n-1; $i++)
    {
        $preSum += $arr[$i];

        // If prefix sum is equal to S/3
        // store current index.
        if ($preSum == $S1 and $ind1 == -1)
            $ind1 = $i;

        // If prefix sum is equal to S/3
        // store current index.
        else if($preSum == $S2 and $ind1 != -1)
        {
            $ind2 = $i;

            // Come out of the loop as both the
            // required indices are found.
            break;
        }
    }

    // If both the indices are found
    // then print them.
    if ($ind1 != -1 and $ind2 != -1)
    {
        echo "(" , $ind1 , ", " , $ind2 , ")";
        return 1;
    }

    // If indices are not found return 0.
    return 0;
}

// Driver code
$arr = array( 1, 3, 4, 0, 4 );
$n = count($arr);
if (findSplit($arr, $n) == 0)
    echo "-1";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to determine if array arr[]
// can be split into three equal sum sets.

// Function to determine if array arr[]
// can be split into three equal sum sets.
function findSplit(arr, n)
{
    var i;

    // variable to store prefix sum
    var preSum = 0;

    // variables to store indices which
    // have prefix sum divisible by S/3.
    var ind1 = -1, ind2 = -1;

    // variable to store sum of
    // entire array.
    var S;

    // Find entire sum of the array.
    S = arr[0];
    for (i = 1; i < n; i++)
        S += arr[i];

    // Check if array can be split in
    // three equal sum sets or not.
    if(S % 3 != 0)
        return 0;

    // Variables to store sum S/3
    // and 2*(S/3).
    var S1 = S / 3;
    var S2 = 2 * S1;

      // Loop until second last index
    // as S2 should not be at the last
    for (i = 0; i < n-1; i++)
    {
        preSum += arr[i];

        // If prefix sum is equal to S/3
        // store current index.
        if (preSum == S1 && ind1 == -1)
            ind1 = i;

        // If prefix sum is equal to 2* (S/3)
        // store current index.
        else if(preSum  == S2 && ind1 != -1)
        {
            ind2 = i;

            // Come out of the loop as both the
            // required indices are found.
            break;
        }
    }

    // If both the indices are found
    // then print them.
    if (ind1 != -1 && ind2 != -1)
    {
        document.write( "(" + ind1 + ", "
                                + ind2 + ")");
        return 1;
    }

    // If indices are not found return 0.
    return 0;
}

// Driver code
var arr =  [ 1, 3, 4, 0, 4 ];
var n = arr.length;
if (findSplit(arr, n) == 0)
    document.write( "-1");

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
(1, 2)
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)