# 奇数索引和偶数索引的元素之和相等的排列数

> 原文:[https://www . geeksforgeeks . org/排列数这样奇数索引和偶数索引的元素之和相等/](https://www.geeksforgeeks.org/number-of-permutations-such-that-sum-of-elements-at-odd-index-and-even-index-are-equal/)

给定 N 个数，求奇数索引处的元素之和与偶数索引处的元素之和相等的置换数。
**例:**

> **输入:** 1 2 3
> **输出:** 2
> 排列为:
> 1 3 2 奇数索引处的和= 1+2 = 3，偶数索引处的和= 3
> 2 3 1 奇数索引处的和= 2+1 = 3，偶数索引处的和= 3
> **输入:** 1 2 1 2
> **输出:** 3
> 排列为:
> 1 2 1

解决这个问题的**方法**是在 C++ STL 中使用[next _ replacement()](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)，这有助于生成 N 个数字的所有可能的置换。如果奇数索引元素的总和等于生成的置换的偶数索引元素的总和，则增加计数。检查所有排列后，打印计数。
以下是上述方法的实施:

## C++

```
// C++ program to find number of permutations
// such that sum of elements at odd index
// and even index are equal
#include <bits/stdc++.h>
using namespace std;

// Function that returns the number of permutations
int numberOfPermutations(int a[], int n)
{
    int sumEven, sumOdd, c = 0;

    // iterate for all permutations
    do {
        // stores the sum of odd and even index elements
        sumEven = sumOdd = 0;

        // iterate for elements in permutation
        for (int i = 0; i < n; i++) {

            // if odd index
            if (i % 2)
                sumOdd += a[i];
            else
                sumEven += a[i];
        }

        // If condition holds
        if (sumOdd == sumEven)
            c++;

    } while (next_permutation(a, a + n));

    // return the number of permutations
    return c;
}
// Driver Code
int main()
{

    int a[] = { 1, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    // Calling Function
    cout << numberOfPermutations(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of permutations
// such that sum of elements at odd index
// and even index are equal
class GFG {

// Function that returns the number of permutations
    static int numberOfPermutations(int a[], int n) {
        int sumEven, sumOdd, c = 0;

        // iterate for all permutations
        do {
            // stores the sum of odd and even index elements
            sumEven = sumOdd = 0;

            // iterate for elements in permutation
            for (int i = 0; i < n; i++) {

                // if odd index
                if (i % 2 == 0) {
                    sumOdd += a[i];
                } else {
                    sumEven += a[i];
                }
            }

            // If condition holds
            if (sumOdd == sumEven) {
                c++;
            }

        } while (next_permutation(a));

        // return the number of permutations
        return c;
    }

    static boolean next_permutation(int[] p) {
        for (int a = p.length - 2; a >= 0; --a) {
            if (p[a] < p[a + 1]) {
                for (int b = p.length - 1;; --b) {
                    if (p[b] > p[a]) {
                        int t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        for (++a, b = p.length - 1; a < b; ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
                }
            }
        }
        return false;
    }
// Driver Code

    public static void main(String args[]) {
        int a[] = {1, 2, 3};
        int n = a.length;
        System.out.println(numberOfPermutations(a, n));
    }
}
/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python3 program to find number of permutations
# such that sum of elements at odd index
# and even index are equal

def next_permutation(arr):

    arrCount = len(arr);

    # the head of the suffix
    i = arrCount - 1;

    # find longest suffix
    while (i > 0 and arr[i] <= arr[i - 1]):
        i-=1;

    # are we at the last permutation already?
    if (i <= 0):
        return [False,arr];

    # get the pivot
    pivotIndex = i - 1;

    # find rightmost element that exceeds the pivot
    j = arrCount - 1;
    while (arr[j] <= arr[pivotIndex]):
        j-=1;

    # swap the pivot with j
    temp = arr[pivotIndex];
    arr[pivotIndex] = arr[j];
    arr[j] = temp;

    # reverse the suffix
    j = arrCount - 1;
    while (i < j):
            temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i+=1;
            j-=1;

    return [True,arr];

# Function that returns the number
# of permutations
def numberOfPermutations(a, n):

    sumEven=0;
    sumOdd=0;
    c = 0;

    # iterate for all permutations
    while (True):

        # stores the sum of odd and
        # even index elements
        sumEven = 0;
        sumOdd = 0;

        # iterate for elements in permutation
        for i in range(n):

            # if odd index
            if (i % 2):
                sumOdd += a[i];
            else:
                sumEven += a[i];

        # If condition holds
        if (sumOdd == sumEven):
            c+=1;
        xx=next_permutation(a);
        if(xx[0]==False):
            break;
        a=xx[1];

    # return the number of permutations
    return c;

# Driver Code
a = [1, 2, 3];
n = len(a);

# Calling Function
print(numberOfPermutations(a, n));

# This code is contributed by mits
```

## C#

```
// C# program to find number of permutations
// such that sum of elements at odd index
// and even index are equal
using System;

public class GFG {

// Function that returns the number of permutations
    static int numberOfPermutations(int []a, int n) {
        int sumEven, sumOdd, c = 0;

        // iterate for all permutations
        do {
            // stores the sum of odd and even index elements
            sumEven = sumOdd = 0;

            // iterate for elements in permutation
            for (int i = 0; i < n; i++) {

                // if odd index
                if (i % 2 == 0) {
                    sumOdd += a[i];
                } else {
                    sumEven += a[i];
                }
            }

            // If condition holds
            if (sumOdd == sumEven) {
                c++;
            }

        } while (next_permutation(a));

        // return the number of permutations
        return c;
    }

    static bool next_permutation(int[] p) {
        for (int a = p.Length - 2; a >= 0; --a) {
            if (p[a] < p[a + 1]) {
                for (int b = p.Length - 1;; --b) {
                    if (p[b] > p[a]) {
                        int t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        for (++a, b = p.Length - 1; a < b; ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
                }
            }
        }
        return false;
    }
// Driver Code

    public static void Main() {
        int []a = {1, 2, 3};
        int n = a.Length;
        Console.WriteLine(numberOfPermutations(a, n));
    }
}
/*This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of permutations
// such that sum of elements at odd index
// and even index are equal

function next_permutation(&$input)
{
    $inputCount = count($input);

    // the head of the suffix
    $i = $inputCount - 1;

    // find longest suffix
    while ($i > 0 && $input[$i] <= $input[$i - 1])
    {
        $i--;
    }

    // are we at the last permutation already?
    if ($i <= 0)
    {
        return false;
    }

    // get the pivot
    $pivotIndex = $i - 1;

    // find rightmost element that exceeds the pivot
    $j = $inputCount - 1;
    while ($input[$j] <= $input[$pivotIndex])
    {
        $j--;
    }

    // swap the pivot with j
    $temp = $input[$pivotIndex];
    $input[$pivotIndex] = $input[$j];
    $input[$j] = $temp;

    // reverse the suffix
    $j = $inputCount - 1;
    while ($i < $j)
    {
            $temp = $input[$i];
            $input[$i] = $input[$j];
            $input[$j] = $temp;
            $i++;
            $j--;
    }
    return true;
}

// Function that returns the number
// of permutations
function numberOfPermutations($a, $n)
{
    $sumEven;
    $sumOdd;
    $c = 0;

    // iterate for all permutations
    do {

        // stores the sum of odd and
        // even index elements
        $sumEven = $sumOdd = 0;

        // iterate for elements in permutation
        for ($i = 0; $i < $n; $i++)
        {

            // if odd index
            if ($i % 2)
                $sumOdd += $a[$i];
            else
                $sumEven += $a[$i];
        }

        // If condition holds
        if ($sumOdd == $sumEven)
            $c++;

    } while (next_permutation($a));

    // return the number of permutations
    return $c;
}

// Driver Code
$a = array(1, 2, 3);
$n = count($a);

// Calling Function
echo numberOfPermutations($a, $n);

// This code is contributed by
// Rajput-Ji
?>
```

## java 描述语言

```
<script>

// javascript program to find number of permutations
// such that sum of elements at odd index
// and even index are equal     // Function that returns the number of permutations
    function numberOfPermutations( a , n) {
        var sumEven, sumOdd, c = 0;

        // iterate for all permutations
        do {
            // stores the sum of odd and even index elements
            sumEven = sumOdd = 0;

            // iterate for elements in permutation
            for (var i = 0; i < n; i++) {

                // if odd index
                if (i % 2 == 0) {
                    sumOdd += a[i];
                } else {
                    sumEven += a[i];
                }
            }

            // If condition holds
            if (sumOdd == sumEven) {
                c++;
            }

        } while (next_permutation(a));

        // return the number of permutations
        return c;
    }

    function next_permutation(p) {
        for (var a = p.length - 2; a >= 0; --a) {
            if (p[a] < p[a + 1]) {
                for (var b = p.length - 1;; --b) {
                    if (p[b] > p[a]) {
                        var t = p[a];
                        p[a] = p[b];
                        p[b] = t;
                        for (++a, b = p.length - 1; a < b; ++a, --b) {
                            t = p[a];
                            p[a] = p[b];
                            p[b] = t;
                        }
                        return true;
                    }
                }
            }
        }
        return false;
    }
    // Driver Code

        var a = [ 1, 2, 3 ];
        var n = a.length;
        document.write(numberOfPermutations(a, n));

// This code contributed by Princi Singh
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N！* N)