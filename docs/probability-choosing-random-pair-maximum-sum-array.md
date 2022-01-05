# 选择数组中和最大的随机对的概率

> 原文:[https://www . geesforgeks . org/概率-选择-随机-对-最大和-数组/](https://www.geeksforgeeks.org/probability-choosing-random-pair-maximum-sum-array/)

给定一个 N 个整数的数组，你必须找到选择随机对(I，j)的概率，i < j such that A[i] + A[j] is maximum.
**例:**

```
Input : A[] = {3, 3, 3, 3}
Output : 1.0000 
Explanation :
Here, maximum sum we can get by selecting 
any pair is 6.
Total number of pairs possible = 6.
Pairs with maximum sum = 6.
Probability = 6/6 = 1.0000

Input : A[] = {1, 2, 2, 3}
Output : 0.3333
Explanation : 
Here, maximum sum we can get by selecting 
a pair is 5.
Total number of pairs possible = 6.
Pairs with maximum sum = {2, 3} and {2, 3} = 2.
Probability = 2/6 = 0.3333
```

```
Probability(event) = Number of favorable outcomes / 
                     Total number of outcomes
```

**天真的方法:**我们可以使用蛮力解整体对(I，j)来解决这个问题，i < j 获得可能的最大值，然后再次执行蛮力来计算达到最大值的次数。
**有效方法:**注意，只有当对由数组的第一个和第二个最大元素组成时，我们才能得到最大对和。因此，问题是计算这些元素出现的次数，并使用公式计算有利的结果。

```
Favorable outcomes = f2 (frequency of second maximum 
element(f2), if maximum element occurs only once).
      or
Favorable outcomes = f1 * (f1 - 1) / 2, 
(when frequency of maximum element(f1) 
is greater than 1).
```

## C++

```
// CPP program of choosing a random pair
// such that A[i]+A[j] is maximum.
#include <bits/stdc++.h>
using namespace std;

// Function to get max first and second
int countMaxSumPairs(int a[], int n)
{
    int first = INT_MIN, second = INT_MIN;
    for (int i = 0; i < n; i++) {

        /* If current element is smaller than
          first,  then update both first and
          second */
        if (a[i] > first) {
            second = first;
            first = a[i];
        }

        /* If arr[i] is in between first and
        second then update second */
        else if (a[i] > second && a[i] != first)
            second = a[i];
    }

    int cnt1 = 0, cnt2 = 0;
    for (int i = 0; i < n; i++) {
        if (a[i] == first)
            cnt1++; // frequency of first maximum
        if (a[i] == second)
            cnt2++; // frequency of second maximum
    }
    if (cnt1 == 1)
        return cnt2;

    if (cnt1 > 1)
        return cnt1 * (cnt1 - 1) / 2;   
}

// Returns probability of choosing a pair with
// maximum sum.
float findMaxSumProbability(int a[], int n)
{
    int total = n * (n - 1) / 2;
    int max_sum_pairs = countMaxSumPairs(a, n);
    return (float)max_sum_pairs/(float)total;
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << findMaxSumProbability(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program of choosing a random pair
// such that A[i]+A[j] is maximum.
import java.util.Scanner;
import java.io.*;

class GFG {

    // Function to get max first and second
    static int countMaxSumPairs(int a[], int n)
    {
        int first = Integer.MIN_VALUE, second = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {

            /* If current element is smaller than
            first, then update both first and
            second */
            if (a[i] > first)
            {
                second = first;
                first = a[i];
            }

            /* If arr[i] is in between first and
            second then update second */
            else if (a[i] > second && a[i] != first)
                second = a[i];
        }

        int cnt1 = 0, cnt2 = 0;
        for (int i = 0; i < n; i++) {
            if (a[i] == first)

                // frequency of first maximum
                cnt1++;
            if (a[i] == second)

                // frequency of second maximum
                cnt2++;
        }
        if (cnt1 == 1)
            return cnt2;

        if (cnt1 > 1)
            return cnt1 * (cnt1 - 1) / 2;
            return 0;
    }

    // Returns probability of choosing a pair with
    // maximum sum.
    static float findMaxSumProbability(int a[], int n)
    {
        int total = n * (n - 1) / 2;
        int max_sum_pairs = countMaxSumPairs(a, n);
        return (float)max_sum_pairs/(float)total;
    }

    // Driver Code
    public static void main (String[] args) {

        int a[] = { 1, 2, 2, 3 };
        int n = a.length;;
        System.out.println(findMaxSumProbability(a, n));

// This code is contributed by ajit
    }
}
```

## 蟒蛇 3

```
# Python 3 program of choosing a random
# pair such that A[i]+A[j] is maximum.

# Function to get max first and second
def countMaxSumPairs(a, n):

    first = 0
    second = 0
    for i in range(n):

        # If current element is smaller than
        # first, then update both first and
        # second
        if (a[i] > first) :
            second = first
            first = a[i]

        # If arr[i] is in between first and
        # second then update second
        elif (a[i] > second and a[i] != first):
            second = a[i]

    cnt1 = 0
    cnt2 = 0
    for i in range(n):
        if (a[i] == first):
            cnt1 += 1 # frequency of first maximum
        if (a[i] == second):
            cnt2 += 1 # frequency of second maximum

    if (cnt1 == 1) :
        return cnt2

    if (cnt1 > 1) :
        return cnt1 * (cnt1 - 1) / 2

# Returns probability of choosing a pair
# with maximum sum.
def findMaxSumProbability(a, n):

    total = n * (n - 1) / 2
    max_sum_pairs = countMaxSumPairs(a, n)
    return max_sum_pairs / total

# Driver Code
if __name__ == "__main__":

    a = [ 1, 2, 2, 3 ]
    n = len(a)
    print(findMaxSumProbability(a, n))

# This code is contributed by ita_c
```

## C#

```
// C# program of choosing a random pair
// such that A[i]+A[j] is maximum.
using System;

public class GFG{

    // Function to get max first and second
    static int countMaxSumPairs(int []a, int n)
    {
        int first = int.MinValue, second = int.MinValue;
        for (int i = 0; i < n; i++) {

            /* If current element is smaller than
            first, then update both first and
            second */
            if (a[i] > first)
            {
                second = first;
                first = a[i];
            }

            /* If arr[i] is in between first and
            second then update second */
            else if (a[i] > second && a[i] != first)
                second = a[i];
        }

        int cnt1 = 0, cnt2 = 0;
        for (int i = 0; i < n; i++) {
            if (a[i] == first)

                // frequency of first maximum
                cnt1++;
            if (a[i] == second)

                // frequency of second maximum
                cnt2++;
        }
        if (cnt1 == 1)
            return cnt2;

        if (cnt1 > 1)
            return cnt1 * (cnt1 - 1) / 2;
            return 0;
    }

    // Returns probability of choosing a pair with
    // maximum sum.
    static float findMaxSumProbability(int []a, int n)
    {
        int total = n * (n - 1) / 2;
        int max_sum_pairs = countMaxSumPairs(a, n);
        return (float)max_sum_pairs/(float)total;
    }

    // Driver Code
    static public void Main ()
    {
        int []a = { 1, 2, 2, 3 };
        int n = a.Length;;
        Console.WriteLine(findMaxSumProbability(a, n));

    }
}
// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program of choosing a random pair
// such that A[i]+A[j] is maximum.

// Function to get max first and second
function countMaxSumPairs($a, $n)
{
    $first = PHP_INT_MIN;
    $second = PHP_INT_MIN;
    for ($i = 0; $i < $n; $i++)
    {

        // If current element is
        // smaller than first,
        // then update both first
        // and second
        if ($a[$i] > $first)
        {
            $second = $first;
            $first = $a[$i];
        }

        // If arr[i] is in between
        // first and second then
        // update second
        else if ($a[$i] > $second &&
                 $a[$i] != $first)
            $second = $a[$i];
    }

    $cnt1 = 0;
    $cnt2 = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] == $first)

            // frequency of first maximum
            $cnt1++;
        if ($a[$i] == $second)

            // frequency of second maximum
            $cnt2++;
    }
    if ($cnt1 == 1)
        return $cnt2;

    if ($cnt1 > 1)
        return $cnt1 * ($cnt1 - 1) / 2;
}

// Returns probability of
// choosing a pair with
// maximum sum.
function findMaxSumProbability($a, $n)
{
    $total = $n * ($n - 1) / 2;
    $max_sum_pairs = countMaxSumPairs($a, $n);
    return (float)$max_sum_pairs / (float) $total;
}

    // Driver Code
    $a= array (1, 2, 2, 3 );
    $n = sizeof($a);
    echo findMaxSumProbability($a, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program of choosing a random pair
// such that A[i]+A[j] is maximum.

    // Function to get max first and second
    function countMaxSumPairs(a, n)
    {
        let first = Number.MIN_VALUE,
        second = Number.MIN_VALUE;
        for (let i = 0; i < n; i++)
        {

            /* If current element is smaller than
            first, then update both first and
            second */
            if (a[i] > first)
            {
                second = first;
                first = a[i];
            }

            /* If arr[i] is in between first and
            second then update second */
            else if (a[i] > second && a[i] != first)
                second = a[i];
        }

        let cnt1 = 0, cnt2 = 0;
        for (let i = 0; i < n; i++) {
            if (a[i] == first)

                // frequency of first maximum
                cnt1++;
            if (a[i] == second)

                // frequency of second maximum
                cnt2++;
        }
        if (cnt1 == 1)
            return cnt2;

        if (cnt1 > 1)
            return cnt1 * (cnt1 - 1) / 2;
            return 0;
    }

    // Returns probability of choosing a pair with
    // maximum sum.
    function findMaxSumProbability(a, n)
    {
        let total = n * (n - 1) / 2;
        let max_sum_pairs = countMaxSumPairs(a, n);
        return max_sum_pairs/total;
    }

// Driver code

        let a = [ 1, 2, 2, 3 ];
        let n = a.length;;
        document.write(findMaxSumProbability(a, n));

</script>
```

**输出:**

```
0.333333
```