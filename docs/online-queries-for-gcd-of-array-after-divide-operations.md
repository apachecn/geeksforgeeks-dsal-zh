# 除法运算后数组 GCD 的在线查询

> 原文:[https://www . geeksforgeeks . org/online-查询除法运算后的阵列 gcd/](https://www.geeksforgeeks.org/online-queries-for-gcd-of-array-after-divide-operations/)

给你一个由 N 个整数值和 M 个更新操作组成的数组。更新包括选择数组中的一个元素，并将其除以一个给定值。可以保证元素可以被所选的值整除。每次更新后，您应该计算数组所有元素的最大公约数。
**例:**

```
Input : 3 3
        36 24 72
        1 3
        3 12
        2 4
Output :12
        6
        6
After each operation the array values will be:
1\. 12, 24, 72
2\. 12, 24, 6
3\. 12, 6, 6

Input :5 6
       100 150 200 600 300
       4 6
       2 3
       4 4
       1 4
       2 5
       5 25
Output : 50
         50
         25
         25
         5
         1
```

**逼近**
首先，你要计算所有初始数的最大公约数(gcd)。因为查询包括将一个数除以它的除数，这意味着在每个查询之后，新的 gcd 是旧 gcd 的除数。因此，对于每个查询，您应该简单地计算更新值和前一个 gcd 之间的 gcd。

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

void print_gcd_online(int n, int m,
                      int query[][2], int arr[])
{
    // stores the gcd of the initial array elements
    int max_gcd = 0;
    int i = 0;

    // calculates the gcd
    for (i = 0; i < n; i++)
        max_gcd = __gcd(max_gcd, arr[i]);

    // performing online queries
    for (i = 0; i < m; i++)
    {
        // index is 1 based
        query[i][0]--;

        // divide the array element
        arr[query[i][0]] /= query[i][1];

        // calculates the current gcd
        max_gcd = __gcd(arr[query[i][0]], max_gcd);

        // print the gcd after each step
        cout << max_gcd << endl;
    }
}

// Driver code
int main()
{
    int n = 3;
    int m = 3;
    int query[m][2];
    int arr[] = {36, 24, 72};
    query[0][0] = 1;
    query[0][1] = 3;
    query[1][0] = 3;
    query[1][1] = 12;
    query[2][0] = 2;
    query[2][1] = 4;

    print_gcd_online(n, m, query, arr);
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

    // returns the gcd after all updates
    // in the array
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    static void print_gcd_online(int n, int m,
                    int[][] query, int[] arr)
    {

        // stores the gcd of the initial array elements
        int max_gcd = 0;

        int i = 0;
        for (i = 0; i < n; i++) // calculates the gcd
            max_gcd = gcd(max_gcd, arr[i]);

        // performing online queries
        for (i = 0; i < m; i++) {

            query[i][0]--; // index is 1 based

            // divide the array element
            arr[query[i][0]] /= query[i][1];

            // calculates the current gcd
            max_gcd = gcd(arr[query[i][0]], max_gcd);

            // print the gcd after each step
            System.out.println(max_gcd);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        int m = 3;
        int[][] query = new int[m][2];
        int[] arr = new int[] { 36, 24, 72 };
        query[0][0] = 1;
        query[0][1] = 3;
        query[1][0] = 3;
        query[1][1] = 12;
        query[2][0] = 2;
        query[2][1] = 4;

        print_gcd_online(n, m, query, arr);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Returns the gcd after all
# updates in the array
def gcd(a, b):

    if a == 0:
        return b

    return gcd(b % a, a)

def print_gcd_online(n, m, query, arr):

    # Stores the gcd of the initial
    # array elements
    max_gcd = 0

    for i in range(0, n): # calculates the gcd
        max_gcd = gcd(max_gcd, arr[i])

    # performing online queries
    for i in range(0, m):

        query[i][0] -= 1 # index is 1 based

        # divide the array element
        arr[query[i][0]] //= query[i][1]

        # calculates the current gcd
        max_gcd = gcd(arr[query[i][0]], max_gcd)

        # Print the gcd after each step
        print(max_gcd)

# Driver code
if __name__ == "__main__":

    n, m = 3, 3
    query = [[1,3], [3,12], [2,4]]
    arr = [36, 24, 72]

    print_gcd_online(n, m, query, arr)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// returns the gcd after all
// updates in the array
static int gcd(int a, int b)
{
    if (a == 0)
        return b;

    return gcd(b % a, a);
}

static void print_gcd_online(int n, int m,
                             int[,] query,
                             int[] arr)
{

    // stores the gcd of the
    // initial array elements
    int max_gcd = 0;

    int i = 0;
    for (i = 0; i < n; i++) // calculates the gcd
        max_gcd = gcd(max_gcd, arr[i]);

    // performing online queries
    for (i = 0; i < m; i++)
    {

        query[i,0]--; // index is 1 based

        // divide the array element
        arr[query[i, 0]] /= query[i, 1];

        // calculates the current gcd
        max_gcd = gcd(arr[query[i, 0]], max_gcd);

        // print the gcd after each step
        Console.WriteLine(max_gcd);
    }
}

// Driver code
public static void Main()
{
    int n = 3;
    int m = 3;
    int[,] query = new int[m, 2];
    int[] arr = new int[] { 36, 24, 72 };
    query[0, 0] = 1;
    query[0, 1] = 3;
    query[1, 0] = 3;
    query[1, 1] = 12;
    query[2, 0] = 2;
    query[2, 1] = 4;

    print_gcd_online(n, m, query, arr);
}
}

// This code is contributed
// by Subhadeep Gupta
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// returns the gcd after all updates
// in the array
function gcd($a, $b)
{
    if ($a == 0)
        return $b;

    return gcd($b % $a, $a);
}

function print_gcd_online($n, $m,
                          $query, $arr)
{

    // stores the gcd of the
    // initial array elements
    $max_gcd = 0;

    $i = 0;

    // calculates the gcd
    for ($i = 0; $i < $n; $i++)
        $max_gcd = gcd($max_gcd,
                       $arr[$i]);

    // performing online queries
    for ($i = 0; $i < $m; $i++)
    {

        $query[$i][0]--; // index is 1 based

        // divide the array element
        $arr[$query[$i][0]] /= $query[$i][1];

        // calculates the current gcd
        $max_gcd = gcd($arr[$query[$i][0]],
                            $max_gcd);

        // print the gcd after each step
        echo ($max_gcd),"\n";
    }
}

// Driver code
$n = 3; $m = 3; $query;
$arr = array( 36, 24, 72 );
$query[0][0] = 1; $query[0][1] = 3;
$query[1][0] = 3; $query[1][1] = 12;
$query[2][0] = 2; $query[2][1] = 4;

print_gcd_online($n, $m, $query, $arr);

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // returns the gcd after all updates
    // in the array
    function gcd(a, b)
    {
        if (a == 0)
            return b;

        return gcd(b % a, a);
    }

    function print_gcd_online(n,m,query,arr)
    {
        // stores the gcd of the initial array elements
        let max_gcd = 0;
        let i = 0;

        // calculates the gcd
        for (i = 0; i < n; i++)
            max_gcd = gcd(max_gcd, arr[i]);

        // performing online queries
        for (i = 0; i < m; i++)
        {
            // index is 1 based
            query[i][0]--;

            // divide the array element
            arr[query[i][0]] /= query[i][1];

            // calculates the current gcd
            max_gcd = gcd(arr[query[i][0]], max_gcd);

            // print the gcd after each step
            document.write(max_gcd + "</br>");
        }
    }

    // Driver code

    let n = 3;
    let m = 3;
    let query = new Array(m);
    for(let i = 0; i < m; i++)
    {
        query[i] = new Array(2);
        for(let j = 0; j < 2; j++)
        {
            query[i][j] = 0;
        }
    }
    let arr = [36, 24, 72];
    query[0][0] = 1;
    query[0][1] = 3;
    query[1][0] = 3;
    query[1][1] = 12;
    query[2][0] = 2;
    query[2][1] = 4;

    print_gcd_online(n, m, query, arr);

</script>
```

**Output:** 

```
12
6
6
```

**时间复杂度** : O(m + n)