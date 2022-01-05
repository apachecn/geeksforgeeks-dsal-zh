# 使数组总和相等的最小移除量

> 原文:[https://www . geesforgeks . org/minimum-removes-to-make-array-sum-even/](https://www.geeksforgeeks.org/minimum-removals-to-make-array-sum-even/)

给定一个由 N 个整数组成的数组 Arr[]。我们需要写一个程序来找到需要从数组中移除的元素的最小数量，这样剩余元素的总和就是偶数。
示例:

```
Input : {1, 2, 3, 4}
Output : 0
Sum is already even

Input : {4, 2, 3, 4}
Output : 1
We need to remove 3 to make
sum even.
```

解决这个问题的思路是先回忆一下 ODDs 和 EVENs 的以下性质:

*   奇数+奇数=偶数
*   奇数+偶数=奇数
*   偶数+偶数=偶数
*   奇数*偶数=偶数
*   偶数*偶数=偶数
*   奇数*奇数=奇数

因此，我们只需要计算数组元素的总和，如果需要，甚至可以从数组中移除一些元素。我们可以注意到任何偶数的和总是偶数。但是奇数的奇数之和是奇数。也就是说，3 + 3 + 3 = 9 这是奇数，但 3 + 3 + 3 + 3 = 12 这是偶数。所以，我们只需要计算数组中奇数元素的数量。如果数组中奇数元素的计数是偶数，那么我们不需要从数组中移除任何元素，但是如果数组中奇数元素的计数是奇数，那么通过从数组中移除任何一个奇数元素，数组的总和将变成偶数。
以下是上述思路的实现:

## C++

```
// CPP program to find minimum number of
// elements to be removed to make the sum
// even

#include <iostream>
using namespace std;

int findCount(int arr[], int n)
{
    int count = 0;

    for (int i = 0; i < n; i++)
        if (arr[i] % 2 == 1)
            count++; /* counts only odd numbers */

    /* if the counter is even return 0
       otherwise return 1 */
    if (count % 2 == 0)
        return 0;
    else
        return 1;
}

// Driver Code
int main()
{
    int arr[] = {1, 2, 4, 5, 1};
    int n = sizeof(arr)/sizeof(arr[0]);

    cout <<findCount(arr,n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of
// elements to be removed to make the sum
// even
class GFG {

    static int findCount(int arr[], int n)
    {
        int count = 0;

        for (int i = 0; i < n; i++)
            if (arr[i] % 2 == 1)

                /* counts only odd numbers */
                count++;

        /* if the counter is even return 0
        otherwise return 1 */
        if (count % 2 == 0)
            return 0;
        else
            return 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {1, 2, 4, 5, 1};
        int n = arr.length;

        System.out.println(findCount(arr, n));
    }
}

// This code is contribute by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# program to find minimum number
# of elements to be removed to
# make the sum even

def findCount(arr, n):

    count = 0

    for i in range(0, n):
        if (arr[i] % 2 == 1):

            # counts only odd
            # numbers
            count += -1

    # if the counter is
    # even return 0
    # otherwise return 1
    if (count % 2 == 0):
        return 0
    else:
        return 1

# Driver Code
arr = [1, 2, 4, 5, 1]
n = len(arr)

print(findCount(arr, n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find minimum number of
// elements to be removed to make the sum
// even
using System;

public class GFG{

    static int findCount(int[] arr, int n)
    {
        int count = 0;

        for (int i = 0; i < n; i++)
            if (arr[i] % 2 == 1)

                /* counts only odd numbers */
                count++;

        /* if the counter is even return 0
        otherwise return 1 */
        if (count % 2 == 0)
            return 0;
        else
            return 1;
    }

    // Driver code
    static public void Main ()
    {
        int[] arr = {1, 2, 4, 5, 1};
        int n = arr.Length;

        Console.WriteLine(findCount(arr, n));
    }
}

// This code is contributed by Ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number of
// elements to be removed to make the sum
// even

function findCount($arr,$n)
{
    $count = 0;

    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] % 2 == 1)

            // counts only odd numbers
            $count++;      

    /* if the counter is even return
       0 otherwise return 1 */
    if ($count % 2 == 0)
        return 0;
    else
        return 1;
}

// Driver Code
$arr = array(1, 2, 4, 5, 1);
$n = 5;
echo findCount($arr,$n);

// This code is contributed by
// Manish Shaw (manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum number of
// elements to be removed to make the sum
// even
function findCount( arr, n)
{
    let count = 0;

    for (let i = 0; i < n; i++)
        if (arr[i] % 2 == 1)
            count++; /* counts only odd numbers */

    /* if the counter is even return 0
    otherwise return 1 */
    if (count % 2 == 0)
        return 0;
    else
        return 1;
}

    // Driver Code
    let arr = [1, 2, 4, 5, 1];
    let n = arr.length;

    document.write(findCount(arr,n));

// This code is contributed by jana_sayantan.   

</script>
```

输出:

```
1
```

**时间复杂度** : O(n)，其中 n 为数组中的元素个数。