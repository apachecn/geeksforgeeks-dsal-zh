# 打印数组等和集(分区问题)|集 1

> 原文:[https://www . geesforgeks . org/print-equal-sum-set-array-partition-problem/](https://www.geeksforgeeks.org/print-equal-sum-sets-array-partition-problem/)

给定数组 arr[]。确定是否可以将数组拆分为两组，使两组中的元素之和相等。如果可能，打印两套。如果不可能，则输出-1。

**示例:**

```

Input : arr = {5, 5, 1, 11}
Output : Set 1 = {5, 5, 1}, 
         Set 2 = {11}
Sum of both the sets is 11 and equal.

Input : arr = {1, 5, 3}
Output : -1
No partitioning results in equal sum sets.
```

我们已经在[分区问题](https://www.geeksforgeeks.org/dynamic-programming-set-18-partition-problem/)中讨论了一个解决方案，来看看数组是否可以分区。在这篇文章中，我们打印了两套也是打印的。我们传递两个向量 set1 和 set2 以及两个和变量 sum1 和 sum2。递归遍历数组。在每个数组位置都有两个选择:要么将当前元素添加到集合 1，要么添加到集合 2。递归调用这两个条件，并相应地更新向量 set1 和 set2。如果当前元素被添加到集合 1，那么将当前元素添加到 sum1，并将其插入向量集合 1。如果当前元素包含在集合 2 中，重复相同的步骤。在数组遍历结束时，比较两者的总和。如果两个和相等，则打印两个向量，否则回溯以检查其他可能性。

**实施:**

## C++

```
// CPP program to print equal sum two subsets of
// an array if it can be partitioned into subsets.
#include <bits/stdc++.h>
using namespace std;

/// Function to print the equal sum sets of the array.
void printSets(vector<int> set1, vector<int> set2)
{
    int i;

    /// Print set 1.
    for (i = 0; i < set1.size(); i++) {
        cout << set1[i] << " ";
    }

    cout << "\n";

    /// Print set 2.
    for (i = 0; i < set2.size(); i++) {
        cout << set2[i] << " ";
    }
}

/// Utility function to find the sets of the array which
/// have equal sum.
bool findSets(int arr[], int n, vector<int>& set1,
              vector<int>& set2, int sum1, int sum2,
              int pos)
{

    /// If entire array is traversed, compare both the sums.
    if (pos == n) {

        /// If sums are equal print both sets and return
        /// true to show sets are found.
        if (sum1 == sum2) {
            printSets(set1, set2);
            return true;
        }

        /// If sums are not equal then return sets are not
        /// found.
        else
            return false;
    }

    /// Add current element to set 1.
    set1.push_back(arr[pos]);

    /// Recursive call after adding current element to
    /// set 1.
    bool res = findSets(arr, n, set1, set2, sum1 + arr[pos],
                        sum2, pos + 1);

    /// If this inclusion results in equal sum sets
    /// partition then return true to show desired sets are
    /// found.
    if (res)
        return res;

    /// If not then backtrack by removing current element
    /// from set1 and include it in set 2.
    set1.pop_back();
    set2.push_back(arr[pos]);

    /// Recursive call after including current element to
    /// set 2.
    res = findSets(arr, n, set1, set2, sum1,
                   sum2 + arr[pos], pos + 1);
    if (res == false)
        if (!set2.empty())
            set2.pop_back();

    return res;
}

/// Return true if array arr can be partitioned
/// into two equal sum sets or not.
bool isPartitionPoss(int arr[], int n)
{
    /// Calculate sum of elements in array.
    int sum = 0;

    for (int i = 0; i < n; i++)
        sum += arr[i];

    /// If sum is odd then array cannot be
    /// partitioned.
    if (sum % 2 != 0)
        return false;

    /// Declare vectors to store both the sets.
    vector<int> set1, set2;

    /// Find both the sets.
    return findSets(arr, n, set1, set2, 0, 0, 0);
}

// Driver code
int main()
{
    int arr[] = { 5, 5, 1, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    if (!isPartitionPoss(arr, n)) {
        cout << "-1";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print equal sum two subsets
// of an array if it can be partitioned into
// subsets.
import java.io.*;
import java.util.*;

public class GFG {

    // Declare Lists to store both
    // the sets.
    static List<Integer> set1 = new ArrayList<Integer>();
    static List<Integer> set2 = new ArrayList<Integer>();
    /// Function to print the equal sum sets
    // of the array.
    static void printSets()
    {
        int i;

        /// Print set 1.
        for (i = 0; i < set1.size(); i++) {
            System.out.print(set1.get(i) + " ");
        }

        System.out.println();

        /// Print set 2.
        for (i = 0; i < set2.size(); i++) {
            System.out.print(set2.get(i) + " ");
        }
    }

    // Utility function to find the sets
    // of the array which have equal sum.
    static boolean findSets(Integer[] arr, int n,
                            int sum1, int sum2,
                            int pos)
    {

        // If entire array is traversed,
        // compare both the sums.
        if (pos == n) {

            // If sums are equal print
            // both sets and return true
            // to show sets are found.
            if (sum1 == sum2) {
                printSets();
                return true;
            }

            // If sums are not equal
            // then return sets are not
            // found.
            else
                return false;
        }

        // Add current element to set 1.
        set1.add(arr[pos]);

        // Recursive call after adding
        // current element to set 1.
        boolean res = findSets(arr, n, sum1 + arr[pos],
                               sum2, pos + 1);

        // If this inclusion results in
        // equal sum sets partition then
        // return true to show desired
        // sets are found.
        if (res == true)
            return res;

        // If not then backtrack by removing
        // current element from set1 and
        // include it in set 2.
        set1.remove(set1.size() - 1);
        set2.add(arr[pos]);

        // Recursive call after including
        // current element to set 2.
        res = findSets(arr, n, sum1, sum2
                                         + arr[pos],
                       pos + 1);

        if (res == false)
            if (set2.size() > 0)
                set2.remove(set2.size() - 1);

        return res;
    }

    // Return true if array arr can be
    // partitioned into two equal sum
    // sets or not.
    static boolean isPartitionPoss(Integer[] arr,
                                   int n)
    {
        // Calculate sum of elements in
        // array.
        int sum = 0;

        for (int i = 0; i < n; i++)
            sum += arr[i];

        // If sum is odd then array cannot
        // be partitioned.
        if (sum % 2 != 0)
            return false;

        /// Find both the sets.
        return findSets(arr, n, 0, 0, 0);
    }

    // Driver code
    public static void main(String args[])
    {
        Integer[] arr = { 5, 5, 1, 11 };
        int n = arr.length;
        if (isPartitionPoss(arr, n) == false) {
            System.out.print("-1");
        }
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to print equal sum two subsets of
# an array if it can be partitioned into subsets.

# Function to print the equal sum sets of the array.
def printSets(set1, set2) :

    # Print set 1.
    for i in range(0, len(set1)) :
        print ("{} ".format(set1[i]), end ="");
    print ("")

    # Print set 2.
    for i in range(0, len(set2)) :
        print ("{} ".format(set2[i]), end ="");
    print ("")

# Utility function to find the sets of the
# array which have equal sum.
def findSets(arr, n, set1, set2, sum1, sum2, pos) :

    # If entire array is traversed, compare both
    # the sums.
    if (pos == n) :

        # If sums are equal print both sets and
        # return true to show sets are found.
        if (sum1 == sum2) :
            printSets(set1, set2)
            return True

        # If sums are not equal then return
        # sets are not found.
        else :
            return False    

    # Add current element to set 1.
    set1.append(arr[pos])

    # Recursive call after adding current
    # element to set 1.
    res = findSets(arr, n, set1, set2,
               sum1 + arr[pos], sum2, pos + 1)

    # If this inclusion results in an equal sum
    # sets partition then return true to show
    # desired sets are found.
    if (res) :
        return res

    # If not then backtrack by removing current
    # element from set1 and include it in set 2.
    set1.pop()
    set2.append(arr[pos])

    # Recursive call after including current
    # element to set 2 and removing the element
    # from set 2 if it returns False
    res= findSets(arr, n, set1, set2, sum1,
                     sum2 + arr[pos], pos + 1)
    if not res:       
        set2.pop()
    return res

# Return true if array arr can be partitioned
# into two equal sum sets or not.
def isPartitionPoss(arr, n) :

    # Calculate sum of elements in array.
    sum = 0

    for i in range(0, n):
        sum += arr[i]

    # If sum is odd then array cannot be
    # partitioned.
    if (sum % 2 != 0) :
        return False

    # Declare vectors to store both the sets.
    set1 = []
    set2 = []

    # Find both the sets.
    return findSets(arr, n, set1, set2, 0, 0, 0)

# Driver code
arr = [5, 5, 1, 11]
n = len(arr)
if (isPartitionPoss(arr, n) == False) :
    print ("-1")

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# program to print equal sum two subsets
// of an array if it can be partitioned into
// subsets.
using System;
using System.Collections.Generic;
using System.Linq;
using System.Collections;

class GFG {

    /// Function to print the equal sum sets
    // of the array.
    static void printSets(List<int> set1,
                          List<int> set2)
    {
        int i;

        /// Print set 1.
        for (i = 0; i < set1.Count; i++) {
            Console.Write(set1[i] + " ");
        }

        Console.WriteLine();

        /// Print set 2.
        for (i = 0; i < set2.Count; i++) {
            Console.Write(set2[i] + " ");
        }
    }

    // Utility function to find the sets
    // of the array which have equal sum.
    static bool findSets(int[] arr, int n,
                         ref List<int> set1,
                         ref List<int> set2,
                         int sum1, int sum2,
                         int pos)
    {

        // If entire array is traversed,
        // compare both the sums.
        if (pos == n) {

            // If sums are equal print
            // both sets and return true
            // to show sets are found.
            if (sum1 == sum2) {
                printSets(set1, set2);
                return true;
            }

            // If sums are not equal
            // then return sets are not
            // found.
            else
                return false;
        }

        // Add current element to set 1.
        set1.Add(arr[pos]);

        // Recursive call after adding
        // current element to set 1.
        bool res = findSets(arr, n, ref set1,
                            ref set2, sum1 + arr[pos],
                            sum2, pos + 1);

        // If this inclusion results in
        // equal sum sets partition then
        // return true to show desired
        // sets are found.
        if (res == true)
            return res;

        // If not then backtrack by removing
        // current element from set1 and
        // include it in set 2.
        set1.RemoveAt(set1.Count - 1);
        set2.Add(arr[pos]);

        // Recursive call after including
        // current element to set 2.
        res = findSets(arr, n, ref set1,
                       ref set2, sum1, sum2
                                           + arr[pos],
                       pos + 1);

        if (res == false)
            if (set2.Count > 0)
                set2.RemoveAt(set2.Count - 1);

        return res;
    }

    // Return true if array arr can be
    // partitioned into two equal sum
    // sets or not.
    static bool isPartitionPoss(int[] arr,
                                int n)
    {
        // Calculate sum of elements in
        // array.
        int sum = 0;

        for (int i = 0; i < n; i++)
            sum += arr[i];

        // If sum is odd then array cannot
        // be partitioned.
        if (sum % 2 != 0)
            return false;

        // Declare Lists to store both
        // the sets.
        List<int> set1 = new List<int>();
        List<int> set2 = new List<int>();

        /// Find both the sets.
        return findSets(arr, n, ref set1,
                        ref set2, 0, 0, 0);
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 5, 5, 1, 11 };
        int n = arr.Length;
        if (isPartitionPoss(arr, n) == false) {
            Console.Write("-1");
        }
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print equal sum
// two subsets of an array if it
// can be partitioned into subsets.

// Function to print the equal
// sum sets of the array.
function printSets($set1, $set2)
{
    $i = 0;

    // Print set 1.
    for ($i = 0; $i < count($set1); $i++)
    {
        echo ($set1[$i]." ");
    }

    echo ("\n");

    // Print set 2.
    for ($i = 0; $i < count($set2); $i++)
    {
        echo ($set2[$i]." ");
    }
}

// Utility function to find the
// sets of the array which have
// equal sum.
function findSets($arr, $n, &$set1,
                     &$set2, $sum1,
                     $sum2, $pos)
{

    // If entire array is traversed,
    // compare both the sums.
    if ($pos == $n)
    {

        // If sums are equal print
        // both sets and return
        // true to show sets are found.
        if ($sum1 == $sum2)
        {
            printSets($set1, $set2);
            return true;
        }

        // If sums are not equal then
        // return sets are not found.
        else
            return false;    
    }

    // Add current element to set 1.
    array_push($set1, $arr[$pos]);

    // Recursive call after adding
    // current element to set 1.
    $res = findSets($arr, $n, $set1, $set2,
                    $sum1 + $arr[$pos],
                    $sum2, $pos + 1);

    // If this inclusion results in
    // equal sum sets partition then 
    // return true to show desired
    // sets are found.
    if ($res)
        return $res;

    // If not then backtrack by
    // removing current element
    // from set1 and include it
    // in set 2.
    array_pop($set1);
    array_push($set2, $arr[$pos]);

    // Recursive call after including
    // current element to set 2.
    return findSets($arr, $n, $set1, $set2,
                    $sum1, $sum2 + $arr[$pos],
                                    $pos + 1);
}

// Return true if array arr
// can be partitioned into
// two equal sum sets or not.
function isPartitionPoss($arr, $n)
{
    // Calculate sum of
    // elements in array.
    $sum = 0;

    for ($i = 0; $i < $n; $i++)
        $sum += $arr[$i];

    // If sum is odd then array
    // cannot be partitioned.
    if ($sum % 2 != 0)
        return false;

    // Declare vectors to
    // store both the sets.
    $set1 = array();
    $set2 = array();

    // Find both the sets.
    return findSets($arr, $n, $set1,
                    $set2, 0, 0, 0);
}

// Driver code
$arr= array( 5, 5, 1, 11 );
$n = count($arr);
if (isPartitionPoss($arr, $n) == false)
    echo ("-1");

// This code is contributed by
// Manish Shaw (manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to print equal sum two
// subsets of an array if it can be partitioned
// into subsets.

// Function to print the equal sum
// sets of the array.
function printSets(set1, set2)
{
    var i;

    // Print set 1.
    for(i = 0; i < set1.length; i++)
    {
        document.write( set1[i] + " ");
    }
    document.write("<br>");

    // Print set 2.
    for(i = 0; i < set2.length; i++)
    {
        document.write( set2[i] + " ");
    }
}

// Utility function to find the sets of the
// array which have equal sum.
function findSets(arr, n, set1, set2,
                  sum1, sum2, pos)
{

    // If entire array is traversed,
    // compare both the sums.
    if (pos == n)
    {

        // If sums are equal print both sets
        // and return true to show sets are found.
        if (sum1 == sum2)
        {
            printSets(set1, set2);
            return true;
        }

        // If sums are not equal then
        // return sets are not found.
        else
            return false;
    }

    // Add current element to set 1.
    set1.push(arr[pos]);

    // Recursive call after adding current
    // element to set 1.
    var res = findSets(arr, n, set1, set2,
                       sum1 + arr[pos],
                       sum2, pos + 1);

    // If this inclusion results in equal sum
    // sets partition then return true to show
    // desired sets are found.
    if (res)
        return res;

    // If not then backtrack by removing
    // current element from set1 and
    // include it in set 2.
    set1.pop();
    set2.push(arr[pos]);

    // Recursive call after including
    // current element to set 2.
    res = findSets(arr, n, set1, set2,
                   sum1, sum2 + arr[pos],
                          pos + 1);
    if (res == false)
        if (!set2.length == 0)
            set2.pop();

    return res;
}

// Return true if array arr can be partitioned
// into two equal sum sets or not.
function isPartitionPoss(arr, n)
{
    // Calculate sum of elements in array.
    var sum = 0;

    for(var i = 0; i < n; i++)
        sum += arr[i];

    // If sum is odd then array cannot be
    // partitioned.
    if (sum % 2 != 0)
        return false;

    // Declare vectors to store both the sets.
    var set1 = [];
    var set2 = [];

    // Find both the sets.
    return findSets(arr, n, set1, set2, 0, 0, 0);
}

// Driver code
var arr = [ 5, 5, 1, 11 ];
var n = arr.length;
if (!isPartitionPoss(arr, n))
{
    document.write( "-1");
}

// This code is contributed by SoumikMondal

</script>
```

**输出:**

```
5 5 1
11
```

**时间复杂度:**指数 O(2^n)
**辅助空间:** O(n)(不考虑函数调用栈的大小)

[**打印等和集数组(分区问题)|集 2**](https://www.geeksforgeeks.org/print-equal-sum-sets-array-partition-problem-set-2/)