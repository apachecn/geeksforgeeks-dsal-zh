# L-R 范围内元素的总和，其中前半部分和后半部分用奇数和偶数填充

> 原文:[https://www . geesforgeks . org/范围内元素之和-l-r-其中-前半部分-后半部分-用奇数和偶数填充/](https://www.geeksforgeeks.org/sum-of-elements-in-range-l-r-where-first-half-and-second-half-is-filled-with-odd-and-even-numbers/)

给定一个数字 N，创建一个数组，数组的前半部分用奇数填充到 N，数组的后半部分用偶数填充。还给出了 L 和 R 索引，任务是打印数组中[L，R]范围内的元素之和。

**示例:**

> **输入:** N = 12，L = 1，R = 11
> **输出:** 66
> 这样形成的数组是{1，3，5，7，9，11，2，4，6，8，10，12}
> 索引 1 和索引 11 之和是 66 {1+3+5+7+9+11+2+4+6+8+10}
> 
> **输入:** N = 11，L = 3，R = 7
> **输出:** 34
> 形成的数组为{1，3，5，7，9，11，2，4，6，8，10}
> 索引 3 和索引 7 之和为 34 {5+7+9+11+2}

一种**天真的方法**将是形成大小为 N 的数组，从 L 迭代到 R 并返回和。

## C++

```
// C++ program to find the sum between L-R
// range by creating the array
// Naive Approach
#include<bits/stdc++.h>
using namespace std;

    // Function to find the sum between L and R
    int rangesum(int n, int l, int r)
    {
        // array created
        int arr[n];

        // fill the first half of array
        int c = 1, i = 0;
        while (c <= n) {
            arr[i++] = c;
            c += 2;
        }

        // fill the second half of array
        c = 2;
        while (c <= n) {
            arr[i++] = c;
            c += 2;
        }
        int sum = 0;

        // find the sum between range
        for (i = l - 1; i < r; i++) {
            sum += arr[i];
        }

        return sum;
    }

    // Driver Code
    int  main()
    {
        int n = 12;
        int l = 1, r = 11;
        cout<<(rangesum(n, l, r));
    }
// This code is contributed by
// Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum between L-R
// range by creating the array
// Naive Approach
import java.io.*;
public class GFG {

    // Function to find the sum between L and R
    static int rangesum(int n, int l, int r)
    {
        // array created
        int[] arr = new int[n];

        // fill the first half of array
        int c = 1, i = 0;
        while (c <= n) {
            arr[i++] = c;
            c += 2;
        }

        // fill the second half of array
        c = 2;
        while (c <= n) {
            arr[i++] = c;
            c += 2;
        }
        int sum = 0;

        // find the sum between range
        for (i = l - 1; i < r; i++) {
            sum += arr[i];
        }

        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 12;
        int l = 1, r = 11;
        System.out.println(rangesum(n, l, r));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the sum between L-R
# range by creating the array
# Naive Approach

# Function to find the sum between L and R
def rangesum(n, l, r):

    # array created
    arr = [0] * n;

    # fill the first half of array
    c = 1; i = 0;
    while (c <= n):
        arr[i] = c;
        i += 1;
        c += 2;

    # fill the second half of array
    c = 2;
    while (c <= n):
        arr[i] = c;
        i += 1;
        c += 2;

    sum = 0;

    # find the sum between range
    for i in range(l - 1, r, 1):
        sum += arr[i];

    return sum;

# Driver Code
if __name__ == '__main__':

    n = 12;
    l, r = 1, 11;
    print(rangesum(n, l, r));

# This code contributed by PrinciRaj1992
```

## C#

```
// C# program to find the sum
// between L-R range by creating
// the array Naive Approach
using System;

class GFG
{

    // Function to find the
    // sum between L and R
    static int rangesum(int n,
                        int l, int r)
    {
        // array created
        int[] arr = new int[n];

        // fill the first
        // half of array
        int c = 1, i = 0;
        while (c <= n)
        {
            arr[i++] = c;
            c += 2;
        }

        // fill the second
        // half of array
        c = 2;
        while (c <= n)
        {
            arr[i++] = c;
            c += 2;
        }
        int sum = 0;

        // find the sum
        // between range
        for (i = l - 1; i < r; i++)
        {
            sum += arr[i];
        }

        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int n = 12;
        int l = 1, r = 11;
        Console.WriteLine(rangesum(n, l, r));
    }
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the sum between
// L-R range by creating the array
// Naive Approach

// Function to find the sum between L and R
function rangesum($n, $l, $r)
{
    // array created
    $arr = array_fill(0, $n, 0);

    // fill the first half of array
    $c = 1;
    $i = 0;
    while ($c <= $n)
    {
        $arr[$i++] = $c;
        $c += 2;
    }

    // fill the second half of array
    $c = 2;
    while ($c <= $n)
    {
        $arr[$i++] = $c;
        $c += 2;
    }
    $sum = 0;

    // find the sum between range
    for ($i = $l - 1; $i < $r; $i++)
    {
        $sum += $arr[$i];
    }

    return $sum;
}

// Driver Code
$n = 12;
$l = 1;
$r = 11;
echo(rangesum($n, $l, $r));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the sum between L-R
// range by creating the array
// Naive Approach

    // Function to find the sum between L and R
    function rangesum(n, l, r)
    {
        // array created
        let arr = new Array(n);

        // fill the first half of array
        let c = 1, i = 0;
        while (c <= n) {
            arr[i++] = c;
            c += 2;
        }

        // fill the second half of array
        c = 2;
        while (c <= n) {
            arr[i++] = c;
            c += 2;
        }
        let sum = 0;

        // find the sum between range
        for (i = l - 1; i < r; i++) {
            sum += arr[i];
        }

        return sum;
    }

    // Driver Code
    let n = 12;
    let l = 1, r = 11;
    document.write(rangesum(n, l, r));

    // This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
66
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)

**有效方法:**不构建数组，问题可以用 O(1)复杂度解决。考虑这样形成的序列的中点。那么 L 和 r 可以有 3 种可能。

*   l 和 r 都在中间点的右边。
*   l 和 r 都在中点的左边。
*   l 在中间点的左边，r 在中间点的左边。

对于第一种和第二种情况，只需找到从开始或中间对应第 l 个位置的数字和从开始或中间对应第 r 个位置的数字。下面的公式可以用来计算总和:

```
sum = (no. of terms in the range)*(first term + last term)/2
```

对于第三种情况，将其视为[L-mid]和[mid-R]，然后应用上述情况 1 和情况 2 公式。
下面是上述方法的实现:

## C++

```
// C++ program to find the sum between L-R
// range by creating the array
// Naive Approach
#include<bits/stdc++.h>
using namespace std;

// // Function to calculate the sum if n is even
int sumeven(int n, int l, int r)
{
    int sum = 0;
    int mid = n / 2;

    // both l and r are to the left of mid
    if (r <= mid)
    {
        // first and last element
        int first = (2 * l - 1);
        int last = (2 * r - 1);

        // Total number of terms in
        // the sequence is r-l+1
        int no_of_terms = r - l + 1;

        // use of formula derived
        sum = ((no_of_terms) * ((first + last))) / 2;
    }

    // both l and r are to the right of mid
    else if (l >= mid)
    {
        // first and last element
        int first = (2 * (l - n / 2));
        int last = (2 * (r - n / 2));

        int no_of_terms = r - l + 1;

        // Use of formula derived
        sum = ((no_of_terms) * ((first + last))) / 2;
    }

    // left is to the left of mid and
    // right is to the right of mid
    else
    {

        // Take two sums i.e left and
        // right differently and add
        int sumleft = 0, sumright = 0;

        // first and last element
        int first_term1 = (2 * l - 1);
        int last_term1 = (2 * (n / 2) - 1);

        // total terms
        int no_of_terms1 = n / 2 - l + 1;

        // no of terms
        sumleft = ((no_of_terms1) *
                  ((first_term1 + last_term1))) / 2;

        // The first even number is 2
        int first_term2 = 2;

        // The last element is given by 2*(r-n/2)
        int last_term2 = (2 * (r - n / 2));
        int no_of_terms2 = r - mid;

        // formula applied
        sumright = ((no_of_terms2) *
                   ((first_term2 + last_term2))) / 2;
        sum = (sumleft + sumright);
    }
    return sum;
}

// Function to calculate the sum if n is odd
int sumodd(int n, int l, int r)
{

    // take ceil value if n is odd
    int mid = n / 2 + 1;
    int sum = 0;

    // // both l and r are to the left of mid
    if (r <= mid)
    {
        // first and last element
        int first = (2 * l - 1);
        int last = (2 * r - 1);

        // number of terms
        int no_of_terms = r - l + 1;

        // formula
        sum = ((no_of_terms) *
             ((first + last))) / 2;
    }

    // // both l and r are to the right of mid
    else if (l > mid)
    {

        // first and last term,
        int first = (2 * (l - mid));
        int last = (2 * (r - mid));

        // no of terms
        int no_of_terms = r - l + 1;

        // formula used
        sum = ((no_of_terms) *
              ((first + last))) / 2;
    }

    // If l is on left and r on right
    else
    {

        // calculate separate sums
        int sumleft = 0, sumright = 0;

        // first half
        int first_term1 = (2 * l - 1);
        int last_term1 = (2 * mid - 1);

        // calculate terms
        int no_of_terms1 = mid - l + 1;
        sumleft = ((no_of_terms1) *
                  ((first_term1 + last_term1))) / 2;

        // second half
        int first_term2 = 2;
        int last_term2 = (2 * (r - mid));
        int no_of_terms2 = r - mid;
        sumright = ((no_of_terms2) *
                   ((first_term2 + last_term2))) / 2;

        // add both halves
        sum = (sumleft + sumright);
    }
    return sum;
}

// Function to find the sum between L and R
int rangesum(int n, int l, int r)
{
    int sum = 0;

    // If n is even
    if (n % 2 == 0)
        return sumeven(n, l, r);

    // If n is odd
    else
        return sumodd(n, l, r);
}

// Driver Code
int main()
{
    int n = 12;
    int l = 1, r = 11;
    cout << (rangesum(n, l, r));
}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum between L-R
// range by creating the array
// Efficient Approach
import java.io.*;
public class GFG {

    // // Function to calculate the sum if n is even
    static int sumeven(int n, int l, int r)
    {
        int sum = 0;
        int mid = n / 2;

        // both l and r are to the left of mid
        if (r <= mid) {
            // first and last element
            int first = (2 * l - 1);
            int last = (2 * r - 1);

            // Total number of terms in
            // the sequence is r-l+1
            int no_of_terms = r - l + 1;

            // use of formula derived
            sum = ((no_of_terms) * ((first + last))) / 2;
        }
        // both l and r are to the right of mid
        else if (l >= mid) {
            // // first and last element
            int first = (2 * (l - n / 2));
            int last = (2 * (r - n / 2));

            int no_of_terms = r - l + 1;

            // Use of formula derived
            sum = ((no_of_terms) * ((first + last))) / 2;
        }

        // left is to the left of mid and
        // right is to the right of mid
        else {
            // Take two sums i.e left and
            // right differently and add
            int sumleft = 0, sumright = 0;

            // first and last element
            int first_term1 = (2 * l - 1);
            int last_term1 = (2 * (n / 2) - 1);

            // total terms
            int no_of_terms1 = n / 2 - l + 1;

            // no of terms
            sumleft = ((no_of_terms1) * ((first_term1 + last_term1))) / 2;

            // The first even number is 2
            int first_term2 = 2;

            // The last element is given by 2*(r-n/2)
            int last_term2 = (2 * (r - n / 2));
            int no_of_terms2 = r - mid;

            // formula applied
            sumright = ((no_of_terms2) * ((first_term2 + last_term2))) / 2;
            sum = (sumleft + sumright);
        }

        return sum;
    }

    // Function to calculate the sum if n is odd
    static int sumodd(int n, int l, int r)
    {

        // take ceil value if n is odd
        int mid = n / 2 + 1;
        int sum = 0;

        // // both l and r are to the left of mid
        if (r <= mid) {
            // first and last element
            int first = (2 * l - 1);
            int last = (2 * r - 1);

            // number of terms
            int no_of_terms = r - l + 1;

            // formula
            sum = ((no_of_terms) * ((first + last))) / 2;
        }

        // // both l and r are to the right of mid
        else if (l > mid) {

            // first and last term,
            int first = (2 * (l - mid));
            int last = (2 * (r - mid));

            // no of terms
            int no_of_terms = r - l + 1;

            // formula used
            sum = ((no_of_terms) * ((first + last))) / 2;
        }

        // If l is on left and r on right
        else {

            // calculate separate sums
            int sumleft = 0, sumright = 0;

            // first half
            int first_term1 = (2 * l - 1);
            int last_term1 = (2 * mid - 1);

            // calculate terms
            int no_of_terms1 = mid - l + 1;
            sumleft = ((no_of_terms1) * ((first_term1 + last_term1))) / 2;

            // second half
            int first_term2 = 2;
            int last_term2 = (2 * (r - mid));
            int no_of_terms2 = r - mid;
            sumright = ((no_of_terms2) * ((first_term2 + last_term2))) / 2;

            // add both halves
            sum = (sumleft + sumright);
        }

        return sum;
    }
    // Function to find the sum between L and R
    static int rangesum(int n, int l, int r)
    {
        int sum = 0;

        // If n is even
        if (n % 2 == 0)
            return sumeven(n, l, r);

        // If n is odd
        else
            return sumodd(n, l, r);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 12;
        int l = 1, r = 11;
        System.out.println(rangesum(n, l, r));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# the sum between L-R range
# by creating the array
# Naive Approach

# Function to calculate
# the sum if n is even
def sumeven(n, l, r):

    sum = 0
    mid = n // 2

    # Both l and r are
    # to the left of mid
    if (r <= mid):

        # First and last element
        first = (2 * l - 1)
        last = (2 * r - 1)

        # Total number of terms in
        # the sequence is r-l+1
        no_of_terms = r - l + 1

        # Use of formula derived
        sum = ((no_of_terms) *
              ((first + last))) // 2

    # Both l and r are to the right of mid
    elif (l >= mid):

        # First and last element
        first = (2 * (l - n // 2))
        last = (2 * (r - n // 2))

        no_of_terms = r - l + 1

        # Use of formula derived
        sum = ((no_of_terms) *
              ((first + last))) // 2

    # Left is to the left of mid and
    # right is to the right of mid
    else :

        # Take two sums i.e left and
        # right differently and add
        sumleft, sumright = 0, 0

        # First and last element
        first_term1 = (2 * l - 1)
        last_term1 = (2 * (n // 2) - 1)

        # total terms
        no_of_terms1 = n // 2 - l + 1

        # no of terms
        sumleft = (((no_of_terms1) *
                  ((first_term1 +
                    last_term1))) // 2)

        # The first even number is 2
        first_term2 = 2

        # The last element is
        #
        last_term2 = (2 * (r - n // 2))
        no_of_terms2 = r - mid

        # formula applied
        sumright = (((no_of_terms2) *
                   ((first_term2 +
                     last_term2))) // 2)
        sum = (sumleft + sumright);

    return sum

# Function to calculate
# the sum if n is odd
def sumodd(n, l, r):

    # Take ceil value if n is odd
    mid = n // 2 + 1;
    sum = 0

    # Both l and r are to
    # the left of mid
    if (r <= mid):

        # First and last element
        first = (2 * l - 1)
        last = (2 * r - 1)

        # number of terms
        no_of_terms = r - l + 1

        # formula
        sum = (((no_of_terms) *
              ((first + last))) // 2)

    # both l and r are to the right of mid
    elif (l > mid):

        # first and last term,
        first = (2 * (l - mid))
        last = (2 * (r - mid))

        # no of terms
        no_of_terms = r - l + 1

        # formula used
        sum = (((no_of_terms) *
              ((first + last))) // 2)

    # If l is on left and r on right
    else :

        # calculate separate sums
        sumleft, sumright = 0, 0

        # first half
        first_term1 = (2 * l - 1)
        last_term1 = (2 * mid - 1)

        # calculate terms
        no_of_terms1 = mid - l + 1
        sumleft = (((no_of_terms1) *
                  ((first_term1 +
                    last_term1))) // 2)

        # second half
        first_term2 = 2
        last_term2 = (2 * (r - mid))
        no_of_terms2 = r - mid
        sumright = (((no_of_terms2) *
                   ((first_term2 +
                     last_term2))) // 2)

        # add both halves
        sum = (sumleft + sumright)

    return sum

# Function to find the
# sum between L and R
def rangesum(n, l, r):

    sum = 0

    # If n is even
    if (n % 2 == 0):
        return sumeven(n, l, r);

    # If n is odd
    else:
        return sumodd(n, l, r)

# Driver Code
if __name__ == "__main__":
    n = 12
    l = 1
    r = 11;
    print (rangesum(n, l, r))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find the sum
// between L-R range by creating
// the array Efficient Approach
using System;

class GFG
{

    // Function to calculate
    // the sum if n is even
    static int sumeven(int n,
                       int l, int r)
    {
        int sum = 0;
        int mid = n / 2;

        // both l and r are
        // to the left of mid
        if (r <= mid)
        {
            // first and last element
            int first = (2 * l - 1);
            int last = (2 * r - 1);

            // Total number of terms in
            // the sequence is r-l+1
            int no_of_terms = r - l + 1;

            // use of formula derived
            sum = ((no_of_terms) *
                  ((first + last))) / 2;
        }

        // both l and r are
        // to the right of mid
        else if (l >= mid)
        {
            // first and last element
            int first = (2 * (l - n / 2));
            int last = (2 * (r - n / 2));

            int no_of_terms = r - l + 1;

            // Use of formula derived
            sum = ((no_of_terms) *
                  ((first + last))) / 2;
        }

        // left is to the left of
        // mid and right is to the
        // right of mid
        else
        {
            // Take two sums i.e left and
            // right differently and add
            int sumleft = 0, sumright = 0;

            // first and last element
            int first_term1 = (2 * l - 1);
            int last_term1 = (2 * (n / 2) - 1);

            // total terms
            int no_of_terms1 = n / 2 - l + 1;

            // no of terms
            sumleft = ((no_of_terms1) *
                      ((first_term1 +
                        last_term1))) / 2;

            // The first even
            // number is 2
            int first_term2 = 2;

            // The last element is
            // given by 2*(r-n/2)
            int last_term2 = (2 * (r - n / 2));
            int no_of_terms2 = r - mid;

            // formula applied
            sumright = ((no_of_terms2) *
                       ((first_term2 +
                         last_term2))) / 2;
            sum = (sumleft + sumright);
        }

        return sum;
    }

    // Function to calculate
    // the sum if n is odd
    static int sumodd(int n,
                      int l, int r)
    {

        // take ceil value
        // if n is odd
        int mid = n / 2 + 1;
        int sum = 0;

        // both l and r are
        // to the left of mid
        if (r <= mid)
        {
            // first and last element
            int first = (2 * l - 1);
            int last = (2 * r - 1);

            // number of terms
            int no_of_terms = r - l + 1;

            // formula
            sum = ((no_of_terms) *
                  ((first + last))) / 2;
        }

        // both l and r are
        // to the right of mid
        else if (l > mid)
        {

            // first and last term,
            int first = (2 * (l - mid));
            int last = (2 * (r - mid));

            // no of terms
            int no_of_terms = r - l + 1;

            // formula used
            sum = ((no_of_terms) *
                  ((first + last))) / 2;
        }

        // If l is on left
        // and r on right
        else
        {

            // calculate separate sums
            int sumleft = 0, sumright = 0;

            // first half
            int first_term1 = (2 * l - 1);
            int last_term1 = (2 * mid - 1);

            // calculate terms
            int no_of_terms1 = mid - l + 1;
            sumleft = ((no_of_terms1) *
                      ((first_term1 +
                        last_term1))) / 2;

            // second half
            int first_term2 = 2;
            int last_term2 = (2 * (r - mid));
            int no_of_terms2 = r - mid;
            sumright = ((no_of_terms2) *
                       ((first_term2 +
                         last_term2))) / 2;

            // add both halves
            sum = (sumleft + sumright);
        }

        return sum;
    }

    // Function to find the
    // sum between L and R
    static int rangesum(int n,
                        int l, int r)
    {

        // If n is even
        if (n % 2 == 0)
            return sumeven(n, l, r);

        // If n is odd
        else
            return sumodd(n, l, r);
    }

    // Driver Code
    public static void Main()
    {
        int n = 12;
        int l = 1, r = 11;
        Console.WriteLine(rangesum(n, l, r));
    }
}

// This code is contributed
// by chandan_jnu.
```

## java 描述语言

```
<script>
// Javascript program to find the sum between L-R
// range by creating the array
// Efficient Approach

     // Function to calculate the sum if n is even
    function sumeven(n,l,r)
    {
        let sum = 0;
        let mid = Math.floor(n / 2);

        // both l and r are to the left of mid
        if (r <= mid) {
            // first and last element
            let first = (2 * l - 1);
            let last = (2 * r - 1);

            // Total number of terms in
            // the sequence is r-l+1
            let no_of_terms = r - l + 1;

            // use of formula derived
            sum = ((no_of_terms) * ((first + last))) / 2;
        }
        // both l and r are to the right of mid
        else if (l >= mid) {
            // // first and last element
            let first = (2 * (l - n / 2));
            let last = (2 * (r - n / 2));

            let no_of_terms = r - l + 1;

            // Use of formula derived
            sum = ((no_of_terms) * ((first + last))) / 2;
        }

        // left is to the left of mid and
        // right is to the right of mid
        else {
            // Take two sums i.e left and
            // right differently and add
            let sumleft = 0, sumright = 0;

            // first and last element
            let first_term1 = (2 * l - 1);
            let last_term1 = (2 * (n / 2) - 1);

            // total terms
            let no_of_terms1 = n / 2 - l + 1;

            // no of terms
            sumleft = ((no_of_terms1) * ((first_term1 + last_term1))) / 2;

            // The first even number is 2
            let first_term2 = 2;

            // The last element is given by 2*(r-n/2)
            let last_term2 = (2 * (r - n / 2));
            let no_of_terms2 = r - mid;

            // formula applied
            sumright = ((no_of_terms2) * ((first_term2 + last_term2))) / 2;
            sum = (sumleft + sumright);
        }

        return sum;
    }

    // Function to calculate the sum if n is odd
    function sumodd(n,l,r)
    {
        // take ceil value if n is odd
        let mid = Math.floor(n / 2) + 1;
        let sum = 0;

        // // both l and r are to the left of mid
        if (r <= mid) {
            // first and last element
            let first = (2 * l - 1);
            let last = (2 * r - 1);

            // number of terms
            let no_of_terms = r - l + 1;

            // formula
            sum = ((no_of_terms) * ((first + last))) / 2;
        }

        // // both l and r are to the right of mid
        else if (l > mid) {

            // first and last term ,
            let first = (2 * (l - mid));
            let last = (2 * (r - mid));

            // no of terms
            let no_of_terms = r - l + 1;

            // formula used
            sum = ((no_of_terms) * ((first + last))) / 2;
        }

        // If l is on left and r on right
        else {

            // calculate separate sums
            let sumleft = 0, sumright = 0;

            // first half
            let first_term1 = (2 * l - 1);
            let last_term1 = (2 * mid - 1);

            // calculate terms
            let no_of_terms1 = mid - l + 1;
            sumleft = ((no_of_terms1) * ((first_term1 + last_term1))) / 2;

            // second half
            let first_term2 = 2;
            let last_term2 = (2 * (r - mid));
            let no_of_terms2 = r - mid;
            sumright = ((no_of_terms2) * ((first_term2 + last_term2))) / 2;

            // add both halves
            sum = (sumleft + sumright);
        }

        return sum;
    }

    // Function to find the sum between L and R
    function rangesum(n,l,r)
    {
        let sum = 0;

        // If n is even
        if (n % 2 == 0)
            return sumeven(n, l, r);

        // If n is odd
        else
            return sumodd(n, l, r);
    }

    // Driver Code
    let n = 12;
    let l = 1, r = 11;
    document.write(rangesum(n, l, r));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
66
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)