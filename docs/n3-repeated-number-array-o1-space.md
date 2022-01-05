# N/3 个重复数在一个有 O(1)个空格的数组中

> 原文:[https://www . geesforgeks . org/n3-repeated-number-array-O1-space/](https://www.geeksforgeeks.org/n3-repeated-number-array-o1-space/)

给我们一个 n 个整数的只读数组。在线性时间和恒定的附加空间中，找出在数组中出现 n/3 次以上的任何元素。如果不存在这样的元素，返回-1。

**示例:**

```
Input : [10, 10, 20, 30, 10, 10]
Output : 10
10 occurs 4 times which is more than 6/3.

Input : [20, 30, 10, 10, 5, 4, 20, 1, 2]
Output : -1
```

这个想法是基于[摩尔的投票算法](https://www.geeksforgeeks.org/majority-element/)。我们先找两个候选人。然后我们检查这两个候选人中是否有任何一个实际上是多数。以下是上述方法的解决方案。

## C++

```
// CPP program to find if any element appears
// more than n/3.
#include <bits/stdc++.h>
using namespace std;

int appearsNBy3(int arr[], int n)
{
    int count1 = 0, count2 = 0;
    int first=INT_MAX    , second=INT_MAX    ;

    for (int i = 0; i < n; i++) {

        // if this element is previously seen,
        // increment count1.
        if (first == arr[i])
            count1++;

        // if this element is previously seen,
        // increment count2.
        else if (second == arr[i])
            count2++;

        else if (count1 == 0) {
            count1++;
            first = arr[i];
        }

        else if (count2 == 0) {
            count2++;
            second = arr[i];
        }

        // if current element is different from
        // both the previously seen variables,
        // decrement both the counts.
        else {
            count1--;
            count2--;
        }
    }

    count1 = 0;
    count2 = 0;

    // Again traverse the array and find the
    // actual counts.
    for (int i = 0; i < n; i++) {
        if (arr[i] == first)
            count1++;

        else if (arr[i] == second)
            count2++;
    }

    if (count1 > n / 3)
        return first;

    if (count2 > n / 3)
        return second;

    return -1;
}

int main()
{
    int arr[] = { 1, 2, 3, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << appearsNBy3(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if any element appears
// more than n/3.
class GFG {

    static int appearsNBy3(int arr[], int n)
    {
        int count1 = 0, count2 = 0;

        // take the integers as the maximum
        // value of integer hoping the integer
        // would not be present in the array
        int first =  Integer.MIN_VALUE;;
        int second = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++) {

            // if this element is previously
            // seen, increment count1.
            if (first == arr[i])
                count1++;

            // if this element is previously
            // seen, increment count2.
            else if (second == arr[i])
                count2++;

            else if (count1 == 0) {
                count1++;
                first = arr[i];
            }

            else if (count2 == 0) {
                count2++;
                second = arr[i];
            }

            // if current element is different
            // from both the previously seen
            // variables, decrement both the
            // counts.
            else {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;

        // Again traverse the array and
        // find the actual counts.
        for (int i = 0; i < n; i++) {
            if (arr[i] == first)
                count1++;

            else if (arr[i] == second)
                count2++;
        }

        if (count1 > n / 3)
            return first;

        if (count2 > n / 3)
            return second;

        return -1;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 1, 1 };
        int n = arr.length;
        System.out.println(appearsNBy3(arr, n));

    }
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find if
# any element appears more than
# n/3.
import sys

def appearsNBy3(arr, n):

    count1 = 0
    count2 = 0
    first = sys.maxsize
    second = sys.maxsize

    for i in range(0, n):

        # if this element is
        # previously seen,
        # increment count1.
        if (first == arr[i]):
            count1 += 1

        # if this element is
        # previously seen,
        # increment count2.
        elif (second == arr[i]):
            count2 += 1

        elif (count1 == 0):
            count1 += 1
            first = arr[i]

        elif (count2 == 0):
            count2 += 1
            second = arr[i]

        # if current element is
        # different from both
        # the previously seen
        # variables, decrement
        # both the counts.
        else:
            count1 -= 1
            count2 -= 1

    count1 = 0
    count2 = 0

    # Again traverse the array
    # and find the actual counts.
    for i in range(0, n):
        if (arr[i] == first):
            count1 += 1

        elif (arr[i] == second):
            count2 += 1

    if (count1 > n / 3):
        return first

    if (count2 > n / 3):
        return second

    return -1

# Driver code
arr = [1, 2, 3, 1, 1 ]
n = len(arr)
print(appearsNBy3(arr, n))

# This code is contributed by
# Smitha
```

## C#

```
// C# program to find if any element appears
// more than n/3.
using System;

public class GFG {

    static int appearsNBy3(int []arr, int n)
    {
        int count1 = 0, count2 = 0;

        // take the integers as the maximum
        // value of integer hoping the integer
        // would not be present in the array
        int first = int.MaxValue;
        int second = int.MaxValue;

        for (int i = 1; i < n; i++) {

            // if this element is previously
            // seen, increment count1.
            if (first == arr[i])
                count1++;

            // if this element is previously
            // seen, increment count2.
            else if (second == arr[i])
                count2++;

            else if (count1 == 0) {
                count1++;
                first = arr[i];
            }

            else if (count2 == 0) {
                count2++;
                second = arr[i];
            }

            // if current element is different
            // from both the previously seen
            // variables, decrement both the
            // counts.
            else {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;

        // Again traverse the array and
        // find the actual counts.
        for (int i = 0; i < n; i++) {
            if (arr[i] == first)
                count1++;

            else if (arr[i] == second)
                count2++;
        }

        if (count1 > n / 3)
            return first;

        if (count2 > n / 3)
            return second;

        return -1;
    }

    // Driver code
    static public void Main(String []args)
    {
        int []arr = { 1, 2, 3, 1, 1 };
        int n = arr.Length;
        Console.WriteLine(appearsNBy3(arr, n));
    }
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find if any element appears
// more than n/3.

function appearsNBy3( $arr,  $n)
{
     $count1 = 0; $count2 = 0;
    $first = PHP_INT_MAX ; $second = PHP_INT_MAX ;

    for ( $i = 0; $i < $n; $i++) {

        // if this element is previously seen,
        // increment count1.
        if ($first == $arr[$i])
            $count1++;

        // if this element is previously seen,
        // increment count2.
        else if ($second == $arr[$i])
            $count2++;

        else if ($count1 == 0) {
            $count1++;
            $first = $arr[$i];
        }

        else if ($count2 == 0) {
            $count2++;
            $second = $arr[$i];
        }

        // if current element is different from
        // both the previously seen variables,
        // decrement both the counts.
        else {
            $count1--;
            $count2--;
        }
    }

    $count1 = 0;
    $count2 = 0;

    // Again traverse the array and find the
    // actual counts.
    for ($i = 0; $i < $n; $i++) {
        if ($arr[$i] == $first)
            $count1++;

        else if ($arr[$i] == $second)
            $count2++;
    }

    if ($count1 > $n / 3)
        return $first;

    if ($count2 > $n / 3)
        return $second;

    return -1;
}

// Driver code
$arr = array( 1, 2, 3, 1, 1 );
$n = count($arr);
echo appearsNBy3($arr, $n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find if any element appears more than n/3.

    function appearsNBy3(arr, n)
    {
        let count1 = 0, count2 = 0;

        // take the integers as the maximum
        // value of integer hoping the integer
        // would not be present in the array
        let first = Number.MAX_VALUE;
        let second = Number.MAX_VALUE;

        for (let i = 1; i < n; i++) {

            // if this element is previously
            // seen, increment count1.
            if (first == arr[i])
                count1++;

            // if this element is previously
            // seen, increment count2.
            else if (second == arr[i])
                count2++;

            else if (count1 == 0) {
                count1++;
                first = arr[i];
            }

            else if (count2 == 0) {
                count2++;
                second = arr[i];
            }

            // if current element is different
            // from both the previously seen
            // variables, decrement both the
            // counts.
            else {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;

        // Again traverse the array and
        // find the actual counts.
        for (let i = 0; i < n; i++) {
            if (arr[i] == first)
                count1++;

            else if (arr[i] == second)
                count2++;
        }

        if (count1 > parseInt(n / 3, 10))
            return first;

        if (count2 > parseInt(n / 3, 10))
            return second;

        return -1;
    }

    let arr = [ 1, 2, 3, 1, 1 ];
    let n = arr.length;
    document.write(appearsNBy3(arr, n));

// This cde is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
1
```

**复杂度分析:**

*   **时间复杂度** : **O(n)**
    算法的第一次遍历完成了对 O(n)有贡献的数组，另一个 O(n)用于检查 count1 和 count2 是否大于 floor(n/3)次。
*   **空间复杂度:O(1)**
    由于不需要额外的空间，所以空间复杂度是恒定的