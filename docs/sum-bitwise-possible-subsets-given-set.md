# 给定集合的所有可能子集的按位“与”的和

> 原文:[https://www . geesforgeks . org/sum-按位-可能-子集-给定-集合/](https://www.geeksforgeeks.org/sum-bitwise-possible-subsets-given-set/)

给定一个数组，我们需要计算给定数组的所有可能子集的位与和。
示例:

```
Input : 1 2 3
Output : 9
For [1, 2, 3], all possible subsets are {1}, 
{2}, {3}, {1, 2}, {1, 3}, {2, 3}, {1, 2, 3}
Bitwise AND of these subsets are, 1 + 2 + 
3 + 0 + 1 + 2 + 0 = 9.
So, the answer would be 9.

Input : 1 2 3 4
Output : 13
```

关于[计数设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)
**天真**方法，我们可以使用[功率设置](https://www.geeksforgeeks.org/power-set/)产生所有子集，然后按位计算所有子集的和。
在**更好的**方法中，我们试图计算哪个数组元素负责产生子集的和。
我们从最低有效位开始。为了消除其他位的影响，我们计算集合中所有数字的“与”位。任何包含 0 的子集都不会有任何贡献。所有只包含 1 的非空子集将贡献 1。总共将有 2^n-1 个这样的子集，每个子集贡献 1。另一部分也是如此。我们得到[0，2，2]，3 个子集，每个子集给出 2。总计 3*1 + 3*2 = 9

```
Array = {1, 2, 3}
Binary representation
positions       2 1 0    
        1       0 0 1
        2       0 1 0
        3       0 1 1
              [ 0 2 2 ]
Count set bit for each position
[ 0 3 3 ] subset produced by each 
position 2^n -1 i.e. n is total sum 
for each position [ 0, 3*2^1, 3*2^0 ] 
Now calculate the sum by multiplying 
the position value i.e 2^0, 2^1 ... . 
 0 + 6 + 3 = 9
```

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to calculate sum of Bit-wise
// and sum of all subsets of an array
#include <bits/stdc++.h>
using namespace std;

#define BITS 32

int andSum(int arr[], int n)
{
    int ans = 0;

    // assuming representation of each element is
    // in 32 bit
    for (int i = 0; i < BITS; i++) {
        int countSetBits = 0;

        // iterating array element
        for (int j = 0; j < n; j++) {

            // Counting the set bit of array in
            // ith position
            if (arr[j] & (1 << i))
                countSetBits++;
        }

        // counting subset which produce sum when
        // particular bit position is set.
        int subset = (1 << countSetBits) - 1;

        // multiplying every position subset with 2^i
        // to count the sum.
        subset = (subset * (1 << i));

        ans += subset;
    }

    return ans;
}

// Drivers code
int main()
{
    int arr[] = { 1, 2, 3};
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << andSum(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate sum of Bit-wise
// and sum of all subsets of an array
class GFG {

    static final int BITS = 32;

    static int andSum(int arr[], int n)
    {
        int ans = 0;

        // assuming representation of each
        // element is in 32 bit
        for (int i = 0; i < BITS; i++) {
            int countSetBits = 0;

            // iterating array element
            for (int j = 0; j < n; j++) {

                // Counting the set bit of
                // array in ith position
                if ((arr[j] & (1 << i)) != 0)
                    countSetBits++;
            }

            // counting subset which produce
            // sum when particular bit
            // position is set.
            int subset = (1 << countSetBits) - 1;

            // multiplying every position
            // subset with 2^i to count the
            // sum.
            subset = (subset * (1 << i));

            ans += subset;
        }

        return ans;
    }

    // Drivers code
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3};
        int size = 3;
        System.out.println (andSum(arr, size));

    }
}

// This code is contributed by Arnab Kundu.
```

## 蟒蛇 3

```
# Python3 program to calculate sum of
# Bit-wise and sum of all subsets of
# an array

BITS = 32;

def andSum(arr, n):
    ans = 0

    # assuming representation
    # of each element is
    # in 32 bit
    for i in range(0, BITS):
        countSetBits = 0

        # iterating array element
        for j in range(0, n) :

            # Counting the set bit
            # of array in ith
            # position
            if (arr[j] & (1 << i)) :
                countSetBits = (countSetBits
                                       + 1)

        # counting subset which
        # produce sum when
        # particular bit position
        # is set.
        subset = ((1 << countSetBits)
                                 - 1)

        # multiplying every position
        # subset with 2^i to count
        # the sum.
        subset = (subset * (1 << i))

        ans = ans + subset

    return ans

# Driver code
arr = [1, 2, 3]
size = len(arr)
print (andSum(arr, size))

# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# program to calculate sum of Bit-wise
// and sum of all subsets of an array
using System;

class GFG {

static int BITS = 32;

    static int andSum(int[] arr, int n)
    {
        int ans = 0;

        // assuming representation of each
        // element is in 32 bit
        for (int i = 0; i < BITS; i++) {
            int countSetBits = 0;

            // iterating array element
            for (int j = 0; j < n; j++) {

                // Counting the set bit of
                // array in ith position
                if ((arr[j] & (1 << i)) != 0)
                    countSetBits++;
            }

            // counting subset which produce
            // sum when particular bit position
            // is set.
            int subset = (1 << countSetBits) - 1;

            // multiplying every position subset
            // with 2^i to count the sum.
            subset = (subset * (1 << i));

            ans += subset;
        }

        return ans;
    }

    // Drivers code
    static public void Main()
    {
        int []arr = { 1, 2, 3};
        int size = 3;
        Console.WriteLine (andSum(arr, size));

    }
}

// This code is contributed by Arnab Kundu.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate sum of Bit-wise
// and sum of all subsets of an array

$BITS = 32;

function andSum( $arr, $n)
{
    global $BITS;
    $ans = 0;

    // assuming representation
    // of each element is
    // in 32 bit
    for($i = 0; $i < $BITS; $i++)
    {
        $countSetBits = 0;

        // iterating array element
        for ( $j = 0; $j < $n; $j++) {

            // Counting the set bit
            // of array in ith position
            if ($arr[$j] & (1 << $i))
                $countSetBits++;
        }

        // counting subset which
        // produce sum when
        // particular bit position
        // is set.
        $subset = (1 << $countSetBits) - 1;

        // multiplying every position
        // subset with 2^i to count
        // the sum.
        $subset = ($subset * (1 << $i));

        $ans += $subset;
    }

    return $ans;
}

    // Driver code
    $arr = array(1, 2, 3);
    $size = count($arr);
    echo andSum($arr, $size);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// javascript program to calculate sum of Bit-wise
// and sum of all subsets of an array   
var BITS = 32;

    function andSum(arr , n) {
        var ans = 0;

        // assuming representation of each
        // element is in 32 bit
        for (i = 0; i < BITS; i++) {
            var countSetBits = 0;

            // iterating array element
            for (j = 0; j < n; j++) {

                // Counting the set bit of
                // array in ith position
                if ((arr[j] & (1 << i)) != 0)
                    countSetBits++;
            }

            // counting subset which produce
            // sum when particular bit
            // position is set.
            var subset = (1 << countSetBits) - 1;

            // multiplying every position
            // subset with 2^i to count the
            // sum.
            subset = (subset * (1 << i));

            ans += subset;
        }

        return ans;
    }

    // Drivers code

        var arr = [ 1, 2, 3 ];
        var size = 3;
        document.write(andSum(arr, size));

// This code contributed by gauravrajput1
</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N)*

***辅助空间:** O(1)*