# 数组中两个奇数出现的元素，所有其他元素出现偶数次

> 原文:[https://www . geeksforgeeks . org/两个奇发生元素-数组-发生-偶发生次数/](https://www.geeksforgeeks.org/two-odd-occurring-elements-array-occur-even-times/)

给定一个数组，其中除两个元素外，所有元素都出现偶数次，打印两个出现奇数次的元素。可以假设数组的大小至少为-2。

**示例:**

```
Input : arr[] = {2, 3, 8, 4, 4, 3, 7, 8}
Output : 2 7

Input : arr[] = {15, 10, 10, 50 7, 5, 5, 50, 50, 50, 50, 50}
Output : 7 15
```

一个**简单的解决方案**是使用两个嵌套循环。外部循环遍历所有元素。内部循环计算当前元素的出现次数。我们打印出现次数为奇数的元素。如果此解决方案为 0(n<sup>2</sup>，则时间复杂度为 0)

一个**更好的解决方案**是使用哈希。这个解决方案的时间复杂度是 O(n)，但是需要额外的空间。

一个**有效的解决方案**是使用按位运算符。这个想法基于在[两个缺失元素](https://www.geeksforgeeks.org/find-two-missing-numbers-set-2-xor-based-solution/)和[两个重复元素](https://www.geeksforgeeks.org/find-the-two-repeating-elements-in-a-given-array/)中使用的方法。

## C++

```
// CPP code to find two odd occurring elements
// in an array where all other elements appear
// even number of times.
#include <bits/stdc++.h>
using namespace std;

void printOdds(int arr[], int n)
{
    // Find XOR of all numbers
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];

    // Find a set bit in the XOR (We find
    // rightmost set bit here)
    int set_bit = res & (~(res - 1));

    // Traverse through all numbers and
    // divide them in two groups
    // (i) Having set bit set at same
    //     position as the only set bit
    //     in set_bit
    // (ii) Having 0 bit at same position
    //      as the only set bit in set_bit
    int x = 0, y = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] & set_bit)
            x = x ^ arr[i];
        else
            y = y ^ arr[i];
    }

    // XOR of two different sets are our
    // required numbers.
    cout << x << " " << y;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 3, 4, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    printOdds(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find two
// odd occurring elements
// in an array where all
// other elements appear
// even number of times.

class GFG
{
static void printOdds(int arr[],
                      int n)
{
    // Find XOR of
    // all numbers
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];

    // Find a set bit in the
    // XOR (We find rightmost
    // set bit here)
    int set_bit = res &
                  (~(res - 1));

    // Traverse through all
    // numbers and divide them
    // in two groups (i) Having
    // set bit set at same position
    // as the only set bit in
    // set_bit (ii) Having 0 bit at
    // same position as the only
    // set bit in set_bit
    int x = 0, y = 0;
    for (int i = 0; i < n; i++)
    {
        if ((arr[i] & set_bit) != 0)
            x = x ^ arr[i];
        else
            y = y ^ arr[i];
    }

    // XOR of two different
    // sets are our required
    // numbers.
    System.out.println( x + " " + y);
}

// Driver code
public static void main(String [] args)
{
    int arr[] = { 2, 3, 3,
                  4, 4, 5 };
    int n = arr.length;
    printOdds(arr, n);
}
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 code to find two
# odd occurring elements in
# an array where all other
# elements appear even number
# of times.
def printOdds(arr, n):

    # Find XOR of all numbers
    res = 0
    for i in range(0, n):
        res = res ^ arr[i]

    # Find a set bit in
    # the XOR (We find
    # rightmost set bit here)
    set_bit = res & (~(res - 1))

    # Traverse through all numbers
    # and divide them in two groups
    # (i) Having set bit set at
    # same position as the only set
    # bit in set_bit
    # (ii) Having 0 bit at same
    # position as the only set
    # bit in set_bit
    x = 0
    y = 0
    for i in range(0, n):
        if (arr[i] & set_bit):
            x = x ^ arr[i]
        else:
            y = y ^ arr[i]

    # XOR of two different
    # sets are our
    # required numbers.
    print(x , y, end = "")

# Driver code
arr = [2, 3, 3, 4, 4, 5 ]
n = len(arr)
printOdds(arr, n)

# This code is contributed
# by Smitha
```

## C#

```
// C# code to find two
// odd occurring elements
// in an array where all
// other elements appear
// even number of times.
using System;

class GFG
{
static void printOdds(int []arr,
                      int n)
{
    // Find XOR of
    // all numbers
    int res = 0;
    for (int i = 0; i < n; i++)
        res = res ^ arr[i];

    // Find a set bit in the
    // XOR (We find rightmost
    // set bit here)
    int set_bit = res &
               (~(res - 1));

    // Traverse through all
    // numbers and divide them
    // in two groups (i) Having
    // set bit set at same position
    // as the only set bit in
    // set_bit (ii) Having 0 bit at
    // same position as the only
    // set bit in set_bit
    int x = 0, y = 0;
    for (int i = 0; i < n; i++)
    {
        if ((arr[i] & set_bit) != 0)
            x = x ^ arr[i];
        else
            y = y ^ arr[i];
    }

    // XOR of two different
    // sets are our required
    // numbers.
    Console.WriteLine(x + " " + y);
}

// Driver code
public static void Main()
{
    int []arr = { 2, 3, 3,
                  4, 4, 5 };
    int n = arr.Length;
    printOdds(arr, n);
}
}

// This code is contributed by
// Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find two odd
// occurring elements in an
// array where all other elements
// appear even number of times.
function printOdds($arr, $n)
{
    // Find XOR of all numbers
    $res = 0;
    for ($i = 0; $i < $n; $i++)
        $res = $res ^ $arr[$i];

    // Find a set bit in the
    // XOR (We find rightmost
    // set bit here)
    $set_bit = $res & (~($res - 1));

    // Traverse through all numbers
    // and divide them in two groups
    // (i) Having set bit set at same
    // position as the only set bit
    // in set_bit
    // (ii) Having 0 bit at same position
    // as the only set bit in set_bit
    $x = 0;
    $y = 0;
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] & $set_bit)
            $x = $x ^ $arr[$i];
        else
            $y = $y ^ $arr[$i];
    }

    // XOR of two different sets
    // are our required numbers.
    echo($x . " " . $y);
}

// Driver code
$arr = array( 2, 3, 3, 4, 4, 5 );
$n = sizeof($arr);
printOdds($arr, $n);

// This code is contributed by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript code to find two odd
// occurring elements in an array
// where all other elements appear
// even number of times.
function printOdds(arr, n)
{

    // Find XOR of all numbers
    let res = 0;
    for(let i = 0; i < n; i++)
        res = res ^ arr[i];

    // Find a set bit in the XOR (We find
    // rightmost set bit here)
    let set_bit = res & (~(res - 1));

    // Traverse through all numbers and
    // divide them in two groups
    // (i) Having set bit set at same
    //     position as the only set bit
    //     in set_bit
    // (ii) Having 0 bit at same position
    //      as the only set bit in set_bit
    let x = 0, y = 0;
    for(let i = 0; i < n; i++)
    {
        if (arr[i] & set_bit)
            x = x ^ arr[i];
        else
            y = y ^ arr[i];
    }

    // XOR of two different sets are our
    // required numbers.
    document.write(x + " " + y);
}

// Driver code
let arr = [ 2, 3, 3, 4, 4, 5 ];
let n = arr.length;

printOdds(arr, n);

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
5 2
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)