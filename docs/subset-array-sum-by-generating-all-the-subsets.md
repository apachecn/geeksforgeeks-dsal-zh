# 通过生成所有子集

进行子集数组求和

> 原文:[https://www . geesforgeks . org/subset-array-sum-by-generation-all-the-subset/](https://www.geeksforgeeks.org/subset-array-sum-by-generating-all-the-subsets/)

给定一个大小为 N 的数组和一个和，任务是检查一些数组元素是否可以加起来和 N 相加。
**注意:**至少要包含一个元素才能组成和。(即总和不能为零)
**示例:**

```
Input: array = -1, 2, 4, 121, N = 5
Output: YES
The array elements 2, 4, -1 can be added to sum to N

Input: array = 1, 3, 7, 121, N = 5
Output:NO 
```

**方法:**思想是使用[生成所有子集，生成数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的所有子序列，并相应地检查是否有任何子序列的和等于给定的和。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Find way to sum to N using array elements atmost once
void find(int arr[], int length, int s)
{
    // loop for all 2^n combinations
    for (int i = 1; i < (pow(2, length)); i++) {

        // sum of a combination
        int sum = 0;

        for (int j = 0; j < length; j++)

            // if the bit is 1 then add the element
            if (((i >> j) & 1))
                sum += arr[j];

        // if the sum is equal to given sum print yes
        if (sum == s) {
            cout << "YES" << endl;
            return;
        }
    }

    // else print no
    cout << "NO" << endl;
}

// driver code
int main()
{
    int sum = 5;
    int array[] = { -1, 2, 4, 121 };
    int length = sizeof(array) / sizeof(int);

    // find whether it is possible to sum to n
    find(array, length, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

        // Find way to sum to N using array elements atmost once
        static void find(int [] arr, int length, int s)
        {
            // loop for all 2^n combinations
            for (int i = 1; i <= (Math.pow(2, length)); i++) {

                // sum of a combination
                int sum = 0;

                for (int j = 0; j < length; j++)

                    // if the bit is 1 then add the element
                    if (((i >> j) & 1) % 2 == 1)
                        sum += arr[j];

                // if the sum is equal to given sum print yes
                if (sum == s) {
                    System.out.println("YES");
                    return;
                }
            }

            // else print no
            System.out.println("NO");
        }

        // driver code
        public static void main(String[] args)
        {
            int sum = 5;
            int []array = { -1, 2, 4, 121 };
            int length = array.length;

            // find whether it is possible to sum to n
            find(array, length, sum);

        }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation
from itertools import combinations

def find(lst, n):
    print('YES' if [1 for r in range(1, len(lst) + 1)
                      for subset in combinations(lst, r)
                      if sum(subset) ==   n] else 'NO')

find([-1, 2, 4, 121], 5)

#This code is contributed by signi dimitri
```

## C#

```

// C# implementation of the above approach
using System;
public class GFG
{

        // Find way to sum to N using array elements atmost once
        static void find(int [] arr, int length, int s)
        {
            // loop for all 2^n combinations
            for (int i = 1; i <= (Math.Pow(2, length)); i++) {

                // sum of a combination
                int sum = 0;

                for (int j = 0; j < length; j++)

                    // if the bit is 1 then add the element
                    if (((i >> j) & 1) % 2 == 1)
                        sum += arr[j];

                // if the sum is equal to given sum print yes
                if (sum == s) {
                    Console.Write("YES");
                    return;
                }
            }

            // else print no
            Console.Write("NO");
        }

        // driver code
        public static void Main()
        {
            int sum = 5;
            int []array = { -1, 2, 4, 121 };
            int length = array.Length;

            // find whether it is possible to sum to n
            find(array, length, sum);

        }

}

// This code is contributed by PrinciRaj19992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Find way to sum to N using array elements atmost once

function find($arr, $length, $s)
{
    // loop for all 2^n combinations
    for ( $i = 1; $i < (pow(2, $length)); $i++)
    {

        // sum of a combination
        $sum = 0;

        for ($j = 0; $j < $length; $j++)

            // if the bit is 1 then add the element
            if ((($i >> $j) & 1))
                $sum += $arr[$j];

        // if the sum is equal to given sum print yes
        if ($sum == $s)
        {
            echo "YES","\n";
            return;
        }
    }

    // else print no
    echo "NO","\n";
}

    // Driver code
    $sum = 5;
    $array = array(-1, 2, 4, 121 );
    $length = sizeof($array) / sizeof($array[0]);

    // find whether it is possible to sum to n
    find($array, $length, $sum);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Find way to sum to N using array
// elements atmost once
function find(arr, length, s)
{
    // loop for all 2^n combinations
    for (var i = 1; i < (Math.pow(2, length)); i++)
    {

        // sum of a combination
        var sum = 0;

        for (var j = 0; j < length; j++)

            // if the bit is 1 then add the element
            if (((i >> j) & 1))
                sum += arr[j];

        // if the sum is equal to given sum print yes
        if (sum == s) {
            document.write( "YES" + "<br>");
            return;
        }
    }

    // else print no
    document.write( "NO" + "<br>");
}

var sum = 5;
var array = [ -1, 2, 4, 121 ];
var length = array.length;

// find whether it is possible to sum to n
find(array, length, sum);

// This code is contributed bby SoumikMondal

</script>
```

**Output:** 

```
YES
```

**注意:**这个程序不会运行于大尺寸的数组。