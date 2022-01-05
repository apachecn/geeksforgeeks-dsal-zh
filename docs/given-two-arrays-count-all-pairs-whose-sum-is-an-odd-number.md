# 给定两个数组，计算所有和为奇数的对

> 原文:[https://www . geesforgeks . org/给定-两个数组-计数-所有对-其和是奇数/](https://www.geeksforgeeks.org/given-two-arrays-count-all-pairs-whose-sum-is-an-odd-number/)

给定 N 和 M 个整数的两个数组。任务是从两个数组中找出由元素组成的无序对的数量，这样它们的和就是奇数。
**注**:一个元素只能是一对。
**示例:**

> **输入:** a[] = {9，14，6，2，11}，b[] = {8，4，7，20}
> **输出:** 3
> {9，20}，{14，7}和{11，8}
> **输入:** a[] = {2，4，6}，b[] = {8，10，12}
> **输出:** 0

**逼近**:统计两个数组中奇数和偶数的个数，对个数的答案会是 min(odd1，even2) + min(odd2，even1)，因为奇数+偶数只是奇数。
以下是上述办法的实施情况:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the number of pairs
int count_pairs(int a[], int b[], int n, int m)
{

    // Count of odd and even numbers
    int odd1 = 0, even1 = 0;
    int odd2 = 0, even2 = 0;

    // Traverse in the first array
    // and count the number of odd
    // and evene numbers in them
    for (int i = 0; i < n; i++) {
        if (a[i] % 2)
            odd1++;
        else
            even1++;
    }

    // Traverse in the second array
    // and count the number of odd
    // and evene numbers in them
    for (int i = 0; i < m; i++) {
        if (b[i] % 2)
            odd2++;
        else
            even2++;
    }

    // Count the number of pairs
    int pairs = min(odd1, even2) + min(odd2, even1);

    // Return the number of pairs
    return pairs;
}

// Driver code
int main()
{
    int a[] = { 9, 14, 6, 2, 11 };
    int b[] = { 8, 4, 7, 20 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = sizeof(b) / sizeof(b[0]);
    cout << count_pairs(a, b, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

class GFG {

    // Function that returns the number of pairs
    static int count_pairs(int a[], int b[], int n, int m)
    {

        // Count of odd and even numbers
        int odd1 = 0, even1 = 0;
        int odd2 = 0, even2 = 0;

        // Traverse in the first array
        // and count the number of odd
        // and evene numbers in them
        for (int i = 0; i < n; i++) {
            if (a[i] % 2 == 1) {
                odd1++;
            }
            else {
                even1++;
            }
        }

        // Traverse in the second array
        // and count the number of odd
        // and evene numbers in them
        for (int i = 0; i < m; i++) {
            if (b[i] % 2 == 1) {
                odd2++;
            }
            else {
                even2++;
            }
        }

        // Count the number of pairs
        int pairs = Math.min(odd1, even2) + Math.min(odd2, even1);

        // Return the number of pairs
        return pairs;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 9, 14, 6, 2, 11 };
        int b[] = { 8, 4, 7, 20 };
        int n = a.length;
        int m = b.length;
        System.out.println(count_pairs(a, b, n, m));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function that returns
# the number of pairs
def count_pairs(a, b, n, m):

    # Count of odd and even numbers
    odd1 = 0
    even1 = 0
    odd2 = 0
    even2 = 0

    # Traverse in the first array
    # and count the number of odd
    # and evene numbers in them
    for i in range(n):
        if (a[i] % 2):
            odd1 += 1
        else:
            even1 += 1

    # Traverse in the second array
    # and count the number of odd
    # and evene numbers in them
    for i in range(m):
        if (b[i] % 2):
            odd2 += 1
        else:
            even2 += 1

    # Count the number of pairs
    pairs = (min(odd1, even2) +
             min(odd2, even1))

    # Return the number of pairs
    return pairs

# Driver code
if __name__ == '__main__':
    a = [9, 14, 6, 2, 11]
    b = [8, 4, 7, 20]
    n = len(a)
    m = len(b)
    print(count_pairs(a, b, n, m))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG {

    // Function that returns the number of pairs
    static int count_pairs(int[] a, int[] b, int n, int m)
    {

        // Count of odd and even numbers
        int odd1 = 0, even1 = 0;
        int odd2 = 0, even2 = 0;

        // Traverse in the first array
        // and count the number of odd
        // and evene numbers in them
        for (int i = 0; i < n; i++) {
            if (a[i] % 2 == 1) {
                odd1++;
            }
            else {
                even1++;
            }
        }

        // Traverse in the second array
        // and count the number of odd
        // and evene numbers in them
        for (int i = 0; i < m; i++) {
            if (b[i] % 2 == 1) {
                odd2++;
            }
            else {
                even2++;
            }
        }

        // Count the number of pairs
        int pairs = Math.Min(odd1, even2) + Math.Min(odd2, even1);

        // Return the number of pairs
        return pairs;
    }

    // Driver code
    static public void Main()
    {
        int[] a = { 9, 14, 6, 2, 11 };
        int[] b = { 8, 4, 7, 20 };
        int n = a.Length;
        int m = b.Length;
        Console.WriteLine(count_pairs(a, b, n, m));
    }
}

// This code contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above approach

// Function that returns the number of pairs
function count_pairs($a, $b, $n, $m)
{
    // Count of odd and even numbers
    $odd1 = 0; $even1 = 0;
    $odd2 = 0; $even2 = 0;

    // Traverse in the first array
    // and count the number of odd
    // and evene numbers in them
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] % 2)
            $odd1++;
        else
            $even1++;
    }

    // Traverse in the second array
    // and count the number of odd
    // and evene numbers in them
    for ($i = 0; $i < $m; $i++)
    {
        if ($b[$i] % 2)
            $odd2++;
        else
            $even2++;
    }

    // Count the number of pairs
    $pairs = min($odd1, $even2) + min($odd2, $even1);

    // Return the number of pairs
    return $pairs;
}

    // Driver code
    $a = array( 9, 14, 6, 2, 11 );
    $b = array( 8, 4, 7, 20 );
    $n = count($a) ;
    $m = count($b) ;

    echo count_pairs($a, $b, $n, $m);

    // This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function that returns the number of pairs
function count_pairs(a, b, n, m)
{

    // Count of odd and even numbers
    let odd1 = 0, even1 = 0;
    let odd2 = 0, even2 = 0;

    // Traverse in the first array
    // and count the number of odd
    // and even numbers in them
    for (let i = 0; i < n; i++) {
        if (a[i] % 2)
            odd1++;
        else
            even1++;
    }

    // Traverse in the second array
    // and count the number of odd
    // and even numbers in them
    for (let i = 0; i < m; i++) {
        if (b[i] % 2)
            odd2++;
        else
            even2++;
    }

    // Count the number of pairs
    let pairs = Math.min(odd1, even2) + Math.min(odd2, even1);

    // Return the number of pairs
    return pairs;
}

// Driver code
    let a = [ 9, 14, 6, 2, 11 ];
    let b = [ 8, 4, 7, 20 ];
    let n = a.length;
    let m = b.length;
    document.write(count_pairs(a, b, n, m));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3
```