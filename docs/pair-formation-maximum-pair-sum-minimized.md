# 配对形成，使得最大配对总和最小化

> 原文:[https://www . geesforgeks . org/pair-formation-maximum-pair-sum-minimum/](https://www.geeksforgeeks.org/pair-formation-maximum-pair-sum-minimized/)

给定一个大小为 2 * N 的整数数组。将数组分成 N 对，使最大对和最小化。换句话说，将数组最佳分割成 N 对应该导致最大对和，该最大对和是所有可能性的其他最大对和的最小值。
**例:**

> 输入:N = 2
> arr[] = { 5，8，3，9 }
> 输出:(3，9) (5，8)
> **解释:**
> 可能的配对为:
> 1。(8，9) (3，5)一对的最大和= 17
> 2。(5，9) (3，8)一对的最大和= 14
> 3。(3，9) (5，8)一对的最大和= 13
> 因此，在情况 3 中，最大对和是所有其他情况中的最小值。因此，答案是(3，9) (5，8)。
> 输入:N = 2
> arr[] = { 9，6，5，1 }
> 输出:(1，9) (5，6)

**方法:**想法是首先对给定的数组进行排序，然后遍历循环以形成对(I，j)，其中我将从 0 开始，j 将相应地从数组的末尾开始。递增 I 和递减 j 形成下一对，以此类推。
以下是上述办法的实施情况。

## C++

```
// CPP Program to divide the array into
// N pairs such that maximum pair is minimized
#include <bits/stdc++.h>

using namespace std;

void findOptimalPairs(int arr[], int N)
{
    sort(arr, arr + N);

    // After Sorting Maintain two variables i and j
    // pointing to start and end of array Such that
    // smallest element of array pairs with largest
    // element
    for (int i = 0, j = N - 1; i <= j; i++, j--)
        cout << "(" << arr[i] << ", " << arr[j] << ")" << " ";
}

// Driver Code
int main()
{
    int arr[] = { 9, 6, 5, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    findOptimalPairs(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to divide the array into
// N pairs such that maximum pair is minimized
import java.io.*;
import java.util.Arrays;

class GFG {

static void findOptimalPairs(int arr[], int N)
{
    Arrays.sort(arr);

    // After Sorting Maintain two variables i and j
    // pointing to start and end of array Such that
    // smallest element of array pairs with largest
    // element
    for (int i = 0, j = N - 1; i <= j; i++, j--)
        System.out.print( "(" + arr[i] + ", " + arr[j] + ")" + " ");
}

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = {9, 6, 5, 1};
        int N = arr.length;

        findOptimalPairs(arr, N);
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 Program to divide the array into
# N pairs such that maximum pair is minimized

def findOptimalPairs(arr, N):
    arr.sort(reverse = False)

    # After Sorting Maintain two variables
    # i and j pointing to start and end of
    # array Such that smallest element of
    # array pairs with largest element
    i = 0
    j = N - 1
    while(i <= j):
        print("(", arr[i], ",",
                   arr[j], ")", end = " ")
        i += 1
        j -= 1

# Driver Code
if __name__ == '__main__':
    arr = [9, 6, 5, 1]
    N = len(arr)

    findOptimalPairs(arr, N)

# This code is contributed by
# Sahil_Shelangia
```

## C#

```
// C# Program to divide the array into
// N pairs such that maximum pair is minimized

using System;

public class GFG{
    static void findOptimalPairs(int []arr, int N)
{
    Array.Sort(arr);

    // After Sorting Maintain two variables i and j
    // pointing to start and end of array Such that
    // smallest element of array pairs with largest
    // element
    for (int i = 0, j = N - 1; i <= j; i++, j--)
        Console.Write( "(" + arr[i] + ", " + arr[j] + ")" + " ");
}

    // Driver Code
    static public void Main (){

        int []arr = {9, 6, 5, 1};
        int N = arr.Length;
        findOptimalPairs(arr, N);

// This code is contributed by ajit.

    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to divide the array into
// N pairs such that maximum pair is minimized

function findOptimalPairs($arr, $N)
{
    sort($arr);

    // After Sorting Maintain two variables
    // i and j pointing to start and end of
    // array Such that smallest element of
    // array pairs with largest element
    for ($i = 0, $j = $N - 1; $i <= $j; $i++, $j--)
            echo "(", $arr[$i],
                 ", ", $arr[$j], ")", " ";
}

// Driver Code
$arr = array( 9, 6, 5, 1 );
$N = sizeof($arr);

findOptimalPairs($arr, $N);

// This code is contributed by jit_t
?>
```

## java 描述语言

```
<script>

/// Javascript Program to divide the array into
// N pairs such that maximum pair is minimized
function findOptimalPairs(arr, N)
{
    arr.sort(function(a,b){ return a-b;});

    // After Sorting Maintain two variables i and j
    // pointing to start and end of array Such that
    // smallest element of array pairs with largest
    // element
    for (var i = 0, j = N - 1; i <= j; i++, j--)
        document.write("(" + arr[i] + ", " + arr[j] + ")" + " ");
}

// Driver Code
var arr = [ 9, 6, 5, 1 ];
var N = arr.length;
findOptimalPairs(arr, N);

</script>
```

**Output:** 

```
(1, 9) (5, 6)
```